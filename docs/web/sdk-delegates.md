???+ warning

    SyncStage Web SDK is currently available only in PREVIEW-ONLY mode, which means it is not yet recommended for production usage.

SyncStage class provide two delegate:, `ISyncStageUserDelegate` and `ISyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```typescript
interface ISyncStageUserDelegate {
  userJoined(connection: IConnection): void;
  userLeft(identifier: string): void;
  userMuted(identifier: string): void;
  userUnmuted(identifier: string): void;
  sessionOut(): void;
}

```

### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```typescript
interface ISyncStageConnectivityDelegate {
  transmitterConnectivityChanged(connected: boolean): void;
  receiverConnectivityChanged(identifier: string, connected: boolean): void;
  desktopAgentReconnected(): void;
}
```

`transmitterConnectivityChanged` and `receiverConnectivityChanged` can be used to update connectivity indicator of particular connections. The `desktopAgentReconnected` callback is suggested to be used to trigger rebuild of the session state in the application (during the disconnection, new connections might be added or removed to the session which result in the ui state inconsistency).


### SyncStageDiscoveryDelegate
Responsible for getting callbacks about available zones latency.

```typescript
export default interface ISyncStageDiscoveryDelegate {
  discoveryResults(zones: string[]): void;
  discoveryLatencyTestResults(results: IZoneLatency[]): void;
}
```
