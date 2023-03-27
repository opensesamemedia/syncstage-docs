### 1. Add package dependency.

```
dependencies: [
    .package(url: "https://github.com/opensesamemedia/SyncStageSwiftPackage.git", .upToNextMajor(from: "0.2.0"))
]

```

### 2. Add the following permissions to info.plist. 

```
Privacy - Microphone Usage Description (Need microphone access for audio recording)
Privacy - Camera Usage Description (No need for camera access), required by ffmpeg

```

### 3. Enable background modes.

SyncStage SDK requires the audio background mode to be enabled to allow streaming, recording in background.

`Audio, AirPlay, Picture in Picture`

### 4. Add SyncStageSecret.plist to your xcode project, and make sure that it is added to the “Copy Bundle Resources” in the target build phases.

SyncStageSecret.plist is assigned to one application. File contains confidential credentials that allow access to your SyncStage resources. 

__Security Notice__

_We strongly recommend storing applicationSecretKey securely in your backend and provide it as a parameter at SyncStage SDK object instantiation. Having implemented the supply of the applicationSecretKey from your protected backend, you can remove that parameter from the .plist._


### 5. Integrate the SyncStage class with your app.

## SDK methods
#### Initialize

Initializes the SDK SyncStage object.

```
init(
    applicationSecretKey: String? = nil,
    completion: @escaping (_ error: SyncStageError?) -> Void
)
```

Constructor parameters:

* `applicationSecretKey` - if set to nil, SDK will look for applicationSecretKey in the SyncStageSecret.plist file

* `completion` - closure informs if setup error occurs

#### Get zones list

Gets available Zones list, where a session can be created

```
zoneList(completion: @escaping (Result<[Zone], Error>)
```

Parameters:

* `completion` - returns zones list

#### Create a session

Creates a session in a given zone by a given user from your user pool.

```
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

#### Join the session

Joins a particular session identified by `sessionCode`.

```
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
leave(completion: @escaping (_ error: SyncStageError?) -> Void)
```

Parameters:

* `completion` - closure informs if leave session error occurs

#### Mute / unmute microphone

Enables or disables microphone stream.

```
toggleMicrophone(mute: Bool)
```

Parameters:

* `mute`- desired state of the mute option

#### Is muted

Returns state of microphone stream.

```
isMicrophoneMuted() -> Bool
```

#### Change receiver volume

Return error code if error occured

```
changeReceiverVolume(identifier: Swift.String, volume: Swift.Float) -> SyncStageSDK.SyncStageErrorCode
```
Parameters:

* `identifier`- Session receiver identifier.
* `volume`- volume float value between 0 and 100.

#### Get receiver volume

Returns receiver volume float value.

```
getReceiverVolume(identifier: Swift.String) -> Swift.Float
```
Parameters:

* `identifier`- Session receiver identifier.

#### Turn on / of direct monitor
Turns on / of direct monitor.

```
toggleDirectMonitor(enable: Bool)
```
Parameters:

* `enable`- `true` for turning on direct monitor

#### Get direct monitor volume value
Returns direct monitor volume float value.

```
getDirectMonitorVolume() -> Swift.Float
```
#### Change direct monitor volume value

```
changeDirectMonitorVolume(volume: Swift.Float)
```
Parameters:

* `volume`- volume float value between 1 and 100.

#### Turn on / of internal microphone
Turns on / of internal microphone to be used instead of default audio input i.e. headphones mic.

```
toggleInternalMic(enable: Bool)
```
Parameters:

* `enable`- `true` for turning on internal microphone

#### Get receiver measurements
Retruns session receiver measurements structure.

```
getReceiverMeasurements(identifier: Swift.String) -> SyncStageSDK.Measurements
```
Parameters:

* `identifier`- session receiver identifier

#### Get transmitter measurements
Retruns session transmitter measurements structure.

```
func getTransmitterMeasurements() -> SyncStageSDK.Measurements
```
Parameters:

* `identifier`- session transmitter identifier.

#### Get SDK version
Returns SDK version.

```
getSDKVersion() -> String
```

### SyncStage delegates
SyncStage class provide two delegate:, `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage.

#### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```
protocol SyncStageUserDelegate: NSObject {
    // called when a user joins a session
    func userJoined(connection: Connection)

    // called when a user leaves a session
    func userLeft(identifier: String)

    // called when a user mutes himself
    func userMuted(identifier: String)

    // called when a user unmutes himself
    func userUnmuted(identifier: String)

    // called when the your application lose connectivity with Studio Server, after a while user will be dismissed from the session
    func sessionOut()
}
```

#### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```
protocol SyncStageConnectivityDelegate: NSObject {
    // called when user loses partial connectivity as a transmitter or when get recover.
    func transmitterConnectivityChanged(connected: Bool)
    
    // called when the receiver loses partial connectivity for a specific user or when it recovers
    func receiverConnectivityChanged(identifier: String, connected: Bool)
}
```
