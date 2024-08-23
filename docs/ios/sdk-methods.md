## [:octicons-tag-24: 0.7.0][0.7.0]{target=_blank}
[0.7.0]: https://github.com/opensesamemedia/SyncStageSwiftPackage/releases/tag/0.7.0

### General

#### Initialize

Initializes the SDK SyncStage object.

```swift
init(
    applicationSecretId: String? = nil, 
    applicationSecretKey: String? = nil,
    completion: @escaping (_ error: SyncStageError?) -> Void
)
```

Constructor parameters:

* `applicationSecretId` - if set to nil, SDK will look for applicationSecretId in the SyncStageSecret.plist file

* `applicationSecretKey` - if set to nil, SDK will look for applicationSecretKey in the SyncStageSecret.plist file

* `completion` - closure informs if setup error occurs

<br />

#### Get SDK version
Returns SDK version.

```swift
func getSDKVersion() -> String
```

<br />

#### Get best available server

Get best available server, where a session can be created

```swift
func getBestAvailableServer(completion: @escaping (Swift.Result<SyncStageSDK.ServerInstance, SyncStageSDK.SyncStageError>) -> Swift.Void)
```

Parameters:

* `completion` - returns a server instance.
  
<br />

#### Get server instances

Get server instances so you can select the server that is suitable for your session.

```swift
func getServerInstances(completion: @escaping (Swift.Result<[SyncStageSDK.ServerInstance], SyncStageSDK.SyncStageError>) -> Swift.Void)
```

Parameters:

* `completion` - returns a list of servers.

<br />

### Session

#### Create a session

Creates a session in a given zone by a given user from your user pool.

```swift
func createSession(
    zoneId: String,
    userId: String,
    studioServerId: String,
    completion: @escaping (Result<SessionIdentifier, SyncStageError>) -> Void
)
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend
* `studioServerId` - id of the selected studio server
* `preferFastRouting` - prefer fast routing allows better network performance
* `completion` -  if succeeded returns a SessionIdentifier (session Id and session code)

<br />

#### Join the session

Joins a particular session identified by `sessionCode`.

```swift
func join(
    sessionCode: String,
    userId: String,
    displayName: String? = nil,
    zoneId: String,
    studioServerId: String,
    preferFastRouting: Swift.Bool = false,
    completion: @escaping (Result<Session, SyncStageError>) -> Void
)
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `displayName` - your app user display name

* `zoneId` - zone in which your session is hosted

* `studioServerId` - studio server where you are running your session

* `completion` - if succeeded returns a Session object

<br />

#### Get session state

Gets state of currently joined session.

```swift
func session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state

<br />

#### Leave the session

Leaves currently joined session.

```swift
func leave(completion: @escaping (_ error: SyncStageError?) -> Void)
```

Parameters:

* `completion` - closure informs if leave session error occurs

<br />

### Audio setup

#### Mute / unmute microphone

Enables or disables microphone stream.

```swift
func toggleMicrophone(mute: Bool)
```

Parameters:

* `mute`- desired state of the mute option

<br />

#### Is muted

Returns state of microphone stream.

```swift
func isMicrophoneMuted() -> Bool
```

<br />

#### Change receiver volume

Return error code if error occured

```swift
func changeReceiverVolume(identifier: String, volume: Float) -> SyncStageSDK.SyncStageErrorCode
```

Parameters:

* `identifier`- Session receiver identifier.
* `volume`- volume float value between 0 and 100.

<br />

#### Get receiver volume

Returns receiver volume float value.

```swift
func getReceiverVolume(identifier: String) -> Float
```

Parameters:

* `identifier`- Session receiver identifier.

<br />

#### Turn on / off direct monitor
Turns on / off direct monitor.

```swift
func toggleDirectMonitor(enable: Bool)
```
Parameters:

* `enable`- `true` for turning on direct monitor

<br />

#### Get direct monitor volume value
Returns direct monitor volume float value.

```swift
func getDirectMonitorVolume() -> Float
```

<br />

#### Change direct monitor volume value

```swift
func changeDirectMonitorVolume(volume: Float)
```

Parameters:

* `volume`- volume float value between 1 and 100.

<br />

#### Is direct monitor enabled
Returns a Bool indicating if the direct monitor is enabled

```swift
func isDirectMonitorEnabled() -> Bool
```

<br />

#### Turn on / off internal microphone
Turns on / off internal microphone to be used instead of default audio input i.e. headphones mic.

```swift
func toggleInternalMic(enable: Bool)
```

Parameters:

* `enable`- `true` for turning on internal microphone

<br />

### Network measurements
#### Get receiver measurements
Returns session receiver measurements structure.

```swift
func getReceiverMeasurements(identifier: String) -> SyncStageSDK.Measurements
```

Parameters:

* `identifier`- session receiver identifier

<br />

#### Get transmitter measurements
Returns session transmitter measurements structure.

```swift
func getTransmitterMeasurements() -> SyncStageSDK.Measurements
```

Parameters:

* `identifier`- session transmitter identifier.

<br />

### Latency Optimization Level
Click [here](/guides/music-collaboration/latency-optimization-levels/){ target=_blank} to learn more about the Latency 
Optimization Level.


#### Change latency Optimization Level
Change the latency optimization level using of the following options:

* highQuality
* optimized
* bestPerformance
* ultraFast

```swift
func changeLatencyOptimizationLevel(value: SyncStageSDK.LatencyOptimizationLevel)
```
Parameters:

* `value`- latency optimization level value.

<br />

#### Get Latency Optimization Level
Returns latency optimization level.

```swift
func getLatencyOptimizationLevel() -> SyncStageSDK.LatencyOptimizationLevel
```

<br />

#### Turn on / off noise cancellation
Turns on / off noise cancellation. This filter is applied on the transmitter (e.g. microphone).

```swift
func toggleNoiseCancellation(enabled: Bool)
```

<br />

### Session recording
#### Start recording

```swift
func startRecording(completion: @escaping (SyncStageError?) -> Void)
```

Parameters:

* `completion` - closure informs if start session recording error occurs

<br />

#### Stop recording

```swift
func stopRecording(completion: @escaping (SyncStageError?) -> Void)
```

Parameters:

* `completion` - closure informs if stop session recording error occurs

<br />


