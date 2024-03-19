### SyncStage data interfaces

```typescript
interface IHostInfo {
  port: number;
  address: string;
  audioServerId: string;
  streamingUrl: string;
}
```



```typescript
interface IConnectionInfo {
  connectionId: string;
  createdAt: string;
  updatedAt: string;
  userId: string;
  isMuted: boolean;
  displayName?: string | null;
  hostInfo?: IHostInfo | null;

  connection(): Connection;
}
```

```typescript
interface ILatencyOptimizationLevel {
  level: number;
}

```

```typescript
interface IMeasurements {
  networkDelayMs: number;
  networkJitterMs: number;
  quality: number;
}

```


```typescript
interface IServerInstance {
  zoneId: string;
  zoneName: string;
  studioServerId: string;
}
```

```typescript
interface ISessionIdentifier {
  sessionId: string;
  sessionCode: string;
  createdAt: string;
}
```

```typescript
interface ISession {
  sessionId: string;
  sessionCode: string | null;
  createdAt: string;
  updatedAt: string;
  transmitter?: IConnection | null;
  receivers: Array<IConnection>;
  isRecording: boolean;
}
```


```typescript
interface IConnection {
  identifier: string;
  userId: string;
  displayName?: string | null;
  isMuted: boolean;
  createdAt: string;
  updatedAt: string;
}
```


```typescript
interface ISessionInfo {
  sessionId: string;
  sessionCode: string | null;
  sessionStatus: string;
  serverIsReady: boolean;
  websocketUrl: string;
  transmitter?: IConnectionInfo | null;
  receivers: Array<IConnectionInfo>;
  createdAt: string;
  updatedAt: string;
  recordingStatus: string;
}
```

```typescript
export interface IZoneLatency {
  name: string;
  latency: string;
}
```
