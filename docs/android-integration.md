### 1. Add package dependency.
In the `settings.gradle` add SyncStage maven repository under `dependencyResolutionManagement` block. Please define `githubProperties` which will be used for package repository authentication.

```
def githubProperties = new Properties()
githubProperties.load(new FileInputStream("github.properties"))

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven {
            url = uri("https://maven.pkg.github.com/opensesamemedia/syncstagesdkpackage")
            credentials {
                username = githubProperties['gpr.usr'] ?: System.getenv("GPR_USER")
                password = githubProperties['gpr.key'] ?: System.getenv("GPR_API_KEY")
            }
        }
    }
}

```

Android studio needs GitHub credentials with `read:packages` permission to fetch the SDK package.

In order to provide GitHub credentials please create a `github.properties` file in the root directory and paste following code:

```
gpr.usr=
gpr.key=
```

Under `gpr.usr` please provide you GitHub login, and under `gpr.key` paste GitHub token with `read:packages` permission. For information how to generate token please refer [here](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token){target=_blank}.

### 2. Add the following permissions to AndroidManifest.xml. 

```
<uses-permission android:name="android.permission.RECORD_AUDIO"/>
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

### 3. Add SyncStageSecret.json to your Android Studio project to the assets folder.

SyncStageSecret.json is assigned to one application. File contains confidential credentials that allow access to your SyncStage resources. 

__Security Notice__

_We strongly recommend storing applicationSecretKey securely in your backend and provide it as a parameter at SyncStage SDK object instantiation. Having implemented the supply of the applicationSecretKey from your protected backend, you can remove that parameter from the .json._


### 4. Integrate the SyncStage class with your app.

## SDK methods

#### Constructor 
```
SyncStage(
        private val ctx: Context,
        var userDelegate: SyncStageUserDelegate? = null,
        var connectivityDelegate: SyncStageConnectivityDelegate? = null
    )
```

Constructor parameters:

* `ctx` - Android application context

* `userDelegate` - delegate object to receive events about users in session state

* `connectivityDelegate` - delegate object to receive events with information about stream connection to Studio Server state

#### Initialize

Initializes the SDK SyncStage object.

```
fun init(
        applicationSecretKey: String? = null,
        onCompleted: (errorCode: SyncStageSDKErrorCode) -> Unit = {},
    )
```

Parameters:

* `applicationSecretKey` - if set to null, SDK will look for applicationSecretKey in the SyncStageSecret.json file

* `onCompleted` - callback informing about the result of initialization with `SyncStageSDKErrorCode`

#### Get zones list

Gets available Zones list, where a session can be created

```
suspend fun zonesList(): Pair<ZonesInRegionsList?, SyncStageSDKErrorCode> 
```

#### Create a session

Creates a session in a given zone by a given user from your user pool.

```
suspend fun createSession(
    zoneId: String,
    userId: String
): Pair<SessionIdentifier?, SyncStageSDKErrorCode>
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend

#### Join the session

Joins a particular session identified by `sessionCode`.

```
suspend fun join(
    sessionCode: String,
    userId: String,
    displayName: String? = null,
    latitude: Double? = null,
    longitude: Double? = null,
): Pair<Session?, SyncStageSDKErrorCode> {
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `displayName` - your app user display name

* `latitude` - current location latitude

* `longitude` - current location longitude

__Note:__ latitude and longitude are now optional parameters, in the future releases it will be used to improve the synchrinization throughout sessions.

#### Get session state

Gets state of currently joined session.

```
session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state


#### Leave the session

Leaves currently joined session.

```
suspend fun leave(): SyncStageSDKErrorCode
```

#### Mute / unmute microphone

Enables or disables microphone stream.

```
fun toggleMicrophone(mute: Boolean): SyncStageSDKErrorCode 
```

Parameters:

* `mute`- desired state of the mute option

#### Is muted

Returns state of microphone stream.

```
fun isMicrophoneMuted(): Boolean
```

<!-- #### Turn on / of direct monitor
Turns on / of direct monitor.

```
fun toggleDirectMonitor(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on direct monitor -->

#### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```
fun toggleInternalMic(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on internal microphone

#### Get receiver network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
fun getReceiverMeasurements(identifier: String): Measurements
```

Parameters:

* `identifier`- receiver's identifier


#### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
fun getTransmitterMeasurements(): Measurements
```


### SyncStage delegates
SyncStage class provide two delegate:, `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

#### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```
interface SyncStageUserDelegate {
    fun userJoined(connection: Connection)
    fun userLeft(identifier: String)
    fun userMuted(identifier: String)
    fun userUnmuted(identifier: String)
    fun sessionOut()
}
```

#### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```
interface SyncStageConnectivityDelegate {
    fun transmitterConnectivityChanged(connected: Boolean)
    fun receiverConnectivityChanged(identifier: String, connected: Boolean)
}
```

### SyncStage SDK Error Codes

Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using following enum class.

```
enum class SyncStageSDKErrorCode(val errorCode: Int) {
    UNKNOWN_ERROR(-1),
    OK(0),
    CONFIGURATION_ERROR(1),
    API_ERROR(2),
    API_UNAUTHORIZED(3),
    AUDIO_STREAMING_ERROR(4),
    STREAM_DOES_NOT_EXIST(5),
    BAD_VOLUME_VALUE(6),
    SESSION_NOT_JOINED(7),
    AUDIO_SERVER_NOT_REACHABLE(8),
}
```

### 5. Use SyncStage in background

To allow SyncStage work in background you need to create a [foreground service](https://developer.android.com/guide/components/foreground-services){target=_blank} of `microphone` type.
Service and additional permission must be added to `AndroidManifest.xml`.

```
...

    <service
        android:name=".YourForegoundServiceName"
        android:foregroundServiceType="microphone" 
    />
</application>

<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
```
