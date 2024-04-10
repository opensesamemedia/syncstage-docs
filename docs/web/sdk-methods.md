### Constructor 

```typescript
class SyncStage implements ISyncStage{
    constructor(
        userDelegate: ISyncStageUserDelegate | null,
        connectivityDelegate: ISyncStageConnectivityDelegate | null,
        discoveryDelegate: ISyncStageDiscoveryDelegate | null,
        desktopAgentDelegate: ISyncStageDesktopAgentDelegate | null,
        onTokenExpired: (() => Promise<string>) | null,
    );
}
```

Constructor parameters:

* `userDelegate` - delegate object to receive events about users in session state

* `connectivityDelegate` - delegate object to receive events with information about stream connection to Studio Server state

* `desktopAgentDelegate` - delegate object to receive events with information of desktop agent acquisition and release to prevent users from using SyncStage in multiple browser tabs at once

* `onTokenExpired` - callback to be called when `jwt` expires, callback should return new refetched `jwt`

### Initialize

Initializes the SDK SyncStage object.

```typescript
async init(
        jwt: string,
    ): Promise<SyncStageSDKErrorCode>
```

Parameters:

* `jwt` - token obtained in the [provisioning](provisioning.md) process.


### Update JWT

You can update JWT anytime you want, even before expiration takes place.

```typescript
async updateToken(jwt: string): Promise<SyncStageSDKErrorCode>
```

* `jwt` - token obtained in the [provisioning](provisioning.md) process.

### Get is desktop agent connected

Checks if desktop agent is running and available on the localhost.

```typescript
isDesktopAgentConnected(): boolean
```


### Get SDK version

Gets SDK version.

```typescript
getSDKVersion(): string
```


### Gets autoselected Studio Server
Get autoselected server instance info

```typescript
async getSelectedServer(): Promise<[IServerInstance | null, SyncStageSDKErrorCode]>;
```



### Get best available Studio Server DEPRECATED

Get best available server, where a session can be created

```typescript
async getBestAvailableServer(): Promise<[IServerInstance | null, SyncStageSDKErrorCode]>
```


### Update SDK to SyncStage backend connected callback

```typescript
  updateOnWebsocketReconnected(onWebsocketReconnected: () => void): void
```

Parameters:

* `onWebsocketReconnected` - method to be called when the browser SDK reconnects to the SyncStage services. Session state should be refetched and synchronized on the UI in this callback.


### Get server instances

Get server instances so you can select the server that is suitable for your session.

```typescript
  async getServerInstances(): Promise<[IServerInstances | null, SyncStageSDKErrorCode]>
```



### Create a session

Creates a session in a given zone by a given user from your user pool.

```typescript
createSession(
    userId: string,
    zoneId?: string | null,
    studioServerId?: string | null,
  ): Promise<[ISessionIdentifier | null, SyncStageSDKErrorCode]>
```

Parameters:

* `zoneId` - zone in which your session is hosted
* `studioServerId` - studio server where you are running your session
* `userId` - id of your app user to match the data between SyncStage and your backend

### Join the session

Joins a particular session identified by `sessionCode`.

```typescript
async join(
    sessionCode: string,
    userId: string,
    displayName?: string | null,
    zoneId?: string | null,
    studioServerId?: string | null,
  ): Promise<[ISession | null, SyncStageSDKErrorCode]>;
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `zoneId` - zone in which your session is hosted

* `studioServerId` - studio server where you are running your session

* `displayName` - your app user display name

### Get session state

Gets state of currently joined session.

```typescript
async session(): Promise<[ISession | null, SyncStageSDKErrorCode]> 
```


### Leave the session

Leaves currently joined session.

```typescript
async leave(): Promise<SyncStageSDKErrorCode> 
```

### Mute / unmute microphone

Enables or disables microphone stream.

```typescript
async toggleMicrophone(mute: boolean): Promise<SyncStageSDKErrorCode>
```

Parameters:

* `mute` - desired state of the mute option

### Is muted

Returns state of microphone stream.

```typescript
async isMicrophoneMuted(): Promise<[boolean | null, SyncStageSDKErrorCode]>
```

### Get receiver network measurements
Returns Measurements object with network delay, jitter, and calculated network quality indicators.

```typescript
async getReceiverMeasurements(identifier: string): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
```

Parameters:

* `identifier` - receiver's identifier


### Get transmitter network measurements
Returns Measurements object with network delay, jitter, and calculated network quality indicators.

```typescript
async getTransmitterMeasurements(): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
```

### Start recording

```typescript
async startRecording(): Promise<SyncStageSDKErrorCode>
```

### Stop recording

```typescript
async stopRecording(): Promise<SyncStageSDKErrorCode>
```


### Register Desktop Agent Reconnected Callback
In case of reconnection UI application should be aware of this fact, to refetch the session state to keep it synchronized.

```typescript
registerDesktopAgentReconnectedCallback(onWebsocketReconnected: () => void): void;
```

Parameters:

* `onWebsocketReconnected` - callback


### Unregister Desktop Agent Reconnected Callback
Remove the callback in the SyncStage.

```typescript
unregisterDesktopAgentReconnectedCallback(): void;
```

### Get URI for opening SyncStage Agent on Windows
```typescript
getDesktopAgentProtocolHandler(): string;
```

<!-- Available in 0.1.0 but not tested - no ui -->
<!-- ### Change latency optimization level
Change the latency optimization level using of the following options: highQuality, optimized, bestPerformance, ultraFast.

```typescript
async changeLatencyOptimizationLevel(level: number): Promise<SyncStageSDKErrorCode>
```
Parameters:

* `level`- latency optimization level value.

### Get latency optimization level
Returns latency optimization level.

```typescript
async getLatencyOptimizationLevel(): Promise<[IZoneLatency | null, SyncStageSDKErrorCode]>
``` -->

