### Constructor 
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

### Initialize

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


### Get SyncStage SDK version

Gets SyncStage SDK version

```
fun getSDKVersion(): String
```

### Get zone list

Gets available zone list, where a session can be created

```
suspend fun zoneList(): Pair<ZonesInRegionsList?, SyncStageSDKErrorCode> 
```

### Create a session

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

### Join the session

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

### Get session state

Gets state of currently joined session.

```
session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state


### Leave the session

Leaves currently joined session.

```
suspend fun leave(): SyncStageSDKErrorCode
```

### Mute / unmute microphone

Enables or disables microphone stream.

```
fun toggleMicrophone(mute: Boolean): SyncStageSDKErrorCode 
```

Parameters:

* `mute`- desired state of the mute option

### Is muted

Returns state of microphone stream.

```
fun isMicrophoneMuted(): Boolean
```

### Turn on / of direct monitor
Turns on / of direct monitor.

```
fun toggleDirectMonitor(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on direct monitor

### Get direct monitor volume
Returns current direct monitor volume.

```
fun getDirectMonitorVolume(): Int
```

### Change direct monitor volume
Changes volume of the direct monitor.

```
fun changeDirectMonitorVolume(volume: Int): SyncStageSDKErrorCode 
```

Parameters:

* `volume`- value from range [0;100]

### Get direct monitor state
Gets direct monitor enabled state

```
fun getDirectMonitorEnabled(): Boolean
```

### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```
fun toggleInternalMic(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on internal microphone

### Get internal microphone state
Gets internal microphone enabled state

```
fun getInternalMicEnabled(): Boolean
```

### Get receiver network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
fun getReceiverMeasurements(identifier: String): Measurements
```

Parameters:

* `identifier`- receiver's identifier


### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
fun getTransmitterMeasurements(): Measurements
```


## SyncStage delegates
SyncStage class provide two delegate:, `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

### SyncStageUserDelegate
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
