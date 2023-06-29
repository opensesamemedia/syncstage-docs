???+ warning

    SyncStage SDK for Android is currently available only in PREVIEW-ONLY mode, which means it is not yet recommended for production usage.

### Constructor 
```kotlin
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

### Initialize

Initializes the SDK SyncStage object.

```kotlin
fun init(
        applicationSecretKey: String? = null,
        onCompleted: (errorCode: SyncStageSDKErrorCode) -> Unit = {},
    )
```

Parameters:

* `applicationSecretKey` - if set to null, SDK will look for applicationSecretKey in the SyncStageSecret.json file

* `onCompleted` - callback informing about the result of initialization with `SyncStageSDKErrorCode`


### Get SyncStage SDK version

Gets SyncStage SDK version

```kotlin
fun getSDKVersion(): String
```

### Get zone list

Gets available zone list, where a session can be created

```kotlin
suspend fun zoneList(): Pair<ZonesInRegionsList?, SyncStageSDKErrorCode> 
```

### Create a session

Creates a session in a given zone by a given user from your user pool.

```kotlin
suspend fun createSession(
    zoneId: String,
    userId: String
): Pair<SessionIdentifier?, SyncStageSDKErrorCode>
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend

### Join the session

Joins a particular session identified by `sessionCode`.

```kotlin
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

!!! note

    Latitude and longitude are now optional parameters, in the future releases it will be used to further optimize the latency.


### Get session state

Gets state of currently joined session.

```kotlin
session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state


### Leave the session

Leaves currently joined session.

```kotlin
suspend fun leave(): SyncStageSDKErrorCode
```

### Mute / unmute microphone

Enables or disables microphone stream.

```kotlin
fun toggleMicrophone(mute: Boolean): SyncStageSDKErrorCode 
```

Parameters:

* `mute`- desired state of the mute option

### Is muted

Returns state of microphone stream.

```kotlin
fun isMicrophoneMuted(): Boolean
```

### Turn on / of direct monitor
Turns on / of direct monitor.

```kotlin
fun toggleDirectMonitor(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on direct monitor

### Get direct monitor volume
Returns current direct monitor volume.

```kotlin
fun getDirectMonitorVolume(): Int
```

### Change direct monitor volume
Changes volume of the direct monitor.

```kotlin
fun changeDirectMonitorVolume(volume: Int): SyncStageSDKErrorCode 
```

Parameters:

* `volume`- value from range [0;100]

### Get direct monitor state
Gets direct monitor enabled state

```kotlin
fun getDirectMonitorEnabled(): Boolean
```

### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```kotlin
fun toggleInternalMic(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on internal microphone

### Get internal microphone state
Gets internal microphone enabled state

```kotlin
fun getInternalMicEnabled(): Boolean
```

### Get receiver network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```kotlin
fun getReceiverMeasurements(identifier: String): Measurements
```

Parameters:

* `identifier`- receiver's identifier


### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```kotlin
fun getTransmitterMeasurements(): Measurements
```
