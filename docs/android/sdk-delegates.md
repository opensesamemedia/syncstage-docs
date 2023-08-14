## [:octicons-tag-24: 0.4.1][0.4.1]{target=_blank}
[0.4.1]: https://github.com/opensesamemedia/syncstage-test-app-android/releases/tag/0.4.1

SyncStage class provide two delegates: `SyncStageUserDelegate` and `SyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```kotlin
interface SyncStageUserDelegate {
    fun userJoined(connection: Connection)
    fun userLeft(identifier: String)
    fun userMuted(identifier: String)
    fun userUnmuted(identifier: String)
    fun sessionOut()
}
```

### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```kotlin
interface SyncStageConnectivityDelegate {
    fun transmitterConnectivityChanged(connected: Boolean)
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
