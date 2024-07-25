## [:octicons-tag-24: 0.6.0][0.6.0]{target=_blank}
[0.6.0]: https://github.com/opensesamemedia/syncstage-test-app-android/releases/tag/0.6.0


### General
#### Constructor 
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

#### Initialize

Initializes the SDK SyncStage object.

```kotlin
fun init(
        syncStageSecret: String? = null,
        onCompleted: (errorCode: SyncStageSDKErrorCode) -> Unit = {},
    )
```

Parameters:

* `syncStageSecret` - if set to null, SDK will look for the SyncStageSecret.json file

* `onCompleted` - callback informing about the result of initialization with `SyncStageSDKErrorCode`


#### Stop and dispose
This method stops and cleans up all background tasks SDK performs. 

```kotlin
fun stop()
```

!!! note
    It is crucial to call it onDestroy of the Activity where SyncStage has been initialized in.


```kotlin
    override fun onDestroy() {
        if (isFinishing) {
            syncStage.stop()
        }
        super.onDestroy()
    }
```


#### Get SyncStage SDK version

Gets SyncStage SDK version

```kotlin
fun getSDKVersion(): String
```

#### Get best available server

Get best available server, where a session can be created

```kotlin
suspend fun getBestAvailableServer(): Pair<ServerInstance?, SyncStageSDKErrorCode>
```

#### Get server instances

Get server instances so you can select the server that is suitable for your session.

```kotlin
suspend fun getServerInstances(): Pair<List<ServerInstance>?, SyncStageSDKErrorCode> 
```


### Session

#### Create a session

Creates a session in a given zone by a given user from your user pool.

```kotlin
suspend fun createSession(
    zoneId: String,
    studioServerId: String,
    userId: String
): Pair<SessionIdentifier?, SyncStageSDKErrorCode>
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `studioServerId` - id of the selected studio server
* `userId` - id of your app user to match the data between SyncStage and your backend

#### Join the session

Joins a particular session identified by `sessionCode`.

```kotlin
suspend fun join(
    sessionCode: String,
    userId: String,
    displayName: String? = null,
    zoneId: String,
    studioServerId: String,
): Pair<Session?, SyncStageSDKErrorCode> 
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `displayName` - your app user display name

* `zoneId` - zone in which your session is hosted

* `studioServerId` - studio server where you are running your session



#### Get session state

Gets state of currently joined session.

```kotlin
session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state


#### Leave the session

Leaves currently joined session.

```kotlin
suspend fun leave(): SyncStageSDKErrorCode
```
### Audio setup

#### Mute / unmute microphone

Enables or disables microphone stream.

```kotlin
fun toggleMicrophone(mute: Boolean): SyncStageSDKErrorCode 
```

Parameters:

* `mute`- desired state of the mute option

#### Is muted

Returns state of microphone stream.

```kotlin
fun isMicrophoneMuted(): Boolean
```

#### Turn on / of direct monitor
Turns on / of direct monitor.

```kotlin
fun toggleDirectMonitor(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on direct monitor

#### Get direct monitor volume
Returns current direct monitor volume.

```kotlin
fun getDirectMonitorVolume(): Int
```

#### Change direct monitor volume
Changes volume of the direct monitor.

```kotlin
fun changeDirectMonitorVolume(volume: Int): SyncStageSDKErrorCode 
```

Parameters:

* `volume`- value from range [0;100]

#### Get direct monitor state
Gets direct monitor enabled state

```kotlin
fun getDirectMonitorEnabled(): Boolean
```

#### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```kotlin
fun toggleInternalMic(enable: Boolean): SyncStageSDKErrorCode
```

Parameters:

* `enable`- `true` for turning on internal microphone

#### Get internal microphone state
Gets internal microphone enabled state

```kotlin
fun getInternalMicEnabled(): Boolean
```

### Network measurements

#### Get receiver network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```kotlin
fun getReceiverMeasurements(identifier: String): Measurements
```

Parameters:

* `identifier`- receiver's identifier


#### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```kotlin
fun getTransmitterMeasurements(): Measurements
```

### Latency Optimization Level
Click [here](../../../guides/music-collaboration/latency-optimization-levels.md){ target=_blank} to learn more about the Latency Optimization Level.
#### Change latency Optimization Level
Change the latency optimization level using of the following options:

* highQuality
* optimized
* bestPerformance
* ultraFast

```kotlin
fun changeLatencyOptimizationLevel(value: LatencyOptimizationLevel)
```
Parameters:

* `value`- latency optimization level value.


#### Get Latency Optimization Level
Returns latency optimization level.

```kotlin
fun getLatencyOptimizationLevel(): LatencyOptimizationLevel
```

### Session recording
#### Start recording

```kotlin
fun startRecording(): SyncStageSDKErrorCode
```

#### Stop recording

```kotlin
fun stopRecording(): SyncStageSDKErrorCode
```