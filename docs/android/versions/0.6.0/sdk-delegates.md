## [:octicons-tag-24: 0.6.0][0.6.0]{target=_blank}
[0.6.0]: https://github.com/opensesamemedia/syncstage-test-app-android/releases/tag/0.6.0

SyncStage class provide two delegates: `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```kotlin
interface SyncStageUserDelegate {
    // called when a user joins a session
    fun userJoined(connection: Connection)
    // called when a user leaves a session
    fun userLeft(identifier: String)
    // called when a user mutes himself
    fun userMuted(identifier: String)
    // called when a user unmutes himself
    fun userUnmuted(identifier: String)
    // called when session recording started
    fun sessionRecordingStarted()
    // called when session recording stopped
    fun sessionRecordingStopped()
    // called when the your application lose connectivity with Studio Server, after a while user will be dismissed from the session
    fun sessionOut()
}
```

### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```kotlin
interface SyncStageConnectivityDelegate {
    // called when user loses partial connectivity as a transmitter or when get recover.
    fun transmitterConnectivityChanged(connected: Boolean)
    // called when the receiver loses partial connectivity for a specific user or when it recovers
    fun receiverConnectivityChanged(identifier: String, connected: Boolean)
}
```

#### SyncStageDiscoveryDelegate
Responsible for getting callbacks about available zones latency.

```kotlin
interface SyncStageDiscoveryDelegate {
    fun discoveryResults(zones: List<String>)
    fun discoveryLatencyTestResults(zoneLatencyMap: Map<String, Int>)
}
```

The key of `zoneLatencyMap` is zoneId, and the value is latency represented in miliseconds.
