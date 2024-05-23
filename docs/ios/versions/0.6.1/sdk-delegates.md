## [:octicons-tag-24: 0.6.1][0.6.1]{target=_blank}
[0.6.1]: https://github.com/opensesamemedia/SyncStageSwiftPackage/releases/tag/0.6.1

### SyncStage delegates
SyncStage class provide two delegate:, `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage.

#### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```swift
protocol SyncStageUserDelegate: NSObject {
    // called when a user joins a session
    func userJoined(connection: Connection)

    // called when a user leaves a session
    func userLeft(identifier: String)

    // called when a user mutes himself
    func userMuted(identifier: String)

    // called when a user unmutes himself
    func userUnmuted(identifier: String)
    
    // called when session recording started
    func sessionRecordingStarted()
    
    // called when session recording stopped
    func sessionRecordingStopped()

    // called when the your application lose connectivity with Studio Server, after a while user will be dismissed from the session
    func sessionOut()
}
```

#### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```swift
protocol SyncStageConnectivityDelegate: NSObject {
    // called when user loses partial connectivity as a transmitter or when get recover.
    func transmitterConnectivityChanged(connected: Bool)
    
    // called when the receiver loses partial connectivity for a specific user or when it recovers
    func receiverConnectivityChanged(identifier: String, connected: Bool)
}
```

#### SyncStageDiscoveryDelegate
Responsible for getting callbacks about available zones latency.

```swift
public protocol SyncStageDiscoveryDelegate: NSObject {
    func discoveryResults(zones: [String])
    func discoveryLatencyTestResults(results: [ZoneLatency])
}
```
