### Initialize

Initializes the SDK SyncStage object.

```swift
init(
    applicationSecretKey: String? = nil,
    completion: @escaping (_ error: SyncStageError?) -> Void
)
```

Constructor parameters:

* `applicationSecretKey` - if set to nil, SDK will look for applicationSecretKey in the SyncStageSecret.plist file

* `completion` - closure informs if setup error occurs

### Get zones list

Gets available Zones list, where a session can be created

```swift
zoneList(completion: @escaping (Result<[Zone], Error>)
```

Parameters:

* `completion` - returns zones list

### Create a session

Creates a session in a given zone by a given user from your user pool.

```swift
createSession(
    zoneId: String,
    userId: String,
    completion: @escaping (Result<SessionIdentifier, SyncStageError>) -> Void
)
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend
* `completion` -  if succeeded returns a SessionIdentifier (session Id and session code)

### Join the session

Joins a particular session identified by `sessionCode`.

```swift
join(
    sessionCode: String,
    userId: String,
    displayName: String? = nil,
    latitude: Decimal? = nil,
    longitude: Decimal? = nil,
    completion: @escaping (Result<Session, SyncStageError>) -> Void
)
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `displayName` - your app user display name

* `latitude` - current location latitude

* `longitude` - current location longitude

* `completion` - if succeeded returns a Session object

!!! note

    Latitude and longitude are now optional parameters, in the future releases it will be used to further optimize the latency.


### Get session state

Gets state of currently joined session.

```swift
session(completion: @escaping (Result<Session, SyncStageError>)
```

Parameters:

* `completion` - returns session state


### Leave the session

Leaves currently joined session.

```swift
leave(completion: @escaping (_ error: SyncStageError?) -> Void)
```

Parameters:

* `completion` - closure informs if leave session error occurs

### Mute / unmute microphone

Enables or disables microphone stream.

```swift
toggleMicrophone(mute: Bool)
```

Parameters:

* `mute`- desired state of the mute option

### Is muted

Returns state of microphone stream.

```swift
isMicrophoneMuted() -> Bool
```

### Change receiver volume

Return error code if error occured

```swift
changeReceiverVolume(identifier: Swift.String, volume: Swift.Float) -> SyncStageSDK.SyncStageErrorCode
```
Parameters:

* `identifier`- Session receiver identifier.
* `volume`- volume float value between 0 and 100.

### Get receiver volume

Returns receiver volume float value.

```swift
getReceiverVolume(identifier: Swift.String) -> Swift.Float
```
Parameters:

* `identifier`- Session receiver identifier.

### Turn on / of direct monitor
Turns on / of direct monitor.

```swift
toggleDirectMonitor(enable: Bool)
```
Parameters:

* `enable`- `true` for turning on direct monitor

### Get direct monitor volume value
Returns direct monitor volume float value.

```swift
getDirectMonitorVolume() -> Swift.Float
```
### Change direct monitor volume value

```swift
changeDirectMonitorVolume(volume: Swift.Float)
```
Parameters:

* `volume`- volume float value between 1 and 100.

### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```swift
toggleInternalMic(enable: Bool)
```
Parameters:

* `enable`- `true` for turning on internal microphone

### Get receiver measurements
Retruns session receiver measurements structure.

```swift
getReceiverMeasurements(identifier: Swift.String) -> SyncStageSDK.Measurements
```
Parameters:

* `identifier`- session receiver identifier

### Get transmitter measurements
Retruns session transmitter measurements structure.

```swift
func getTransmitterMeasurements() -> SyncStageSDK.Measurements
```
Parameters:

* `identifier`- session transmitter identifier.

### Get SDK version
Returns SDK version.

```swift
getSDKVersion() -> String
```
