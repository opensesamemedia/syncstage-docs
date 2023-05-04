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
