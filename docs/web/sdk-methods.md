### Constructor 

```typescript
class SyncStage implements ISyncStage{
    constructor(
        public userDelegate: ISyncStageUserDelegate | null,
        public connectivityDelegate: ISyncStageConnectivityDelegate | null,
        desktopAgentPort: number = 18080,
    );
}
```

Constructor parameters:

* `userDelegate` - delegate object to receive events about users in session state

* `connectivityDelegate` - delegate object to receive events with information about stream connection to Studio Server state

* `desktopAgentPort` - port for communication with local desktop agent, 18080 by default

### Initialize

Initializes the SDK SyncStage object.

```typescript
async init(
        applicationSecretId: string,
        applicationSecretKey: string
    ): Promise<SyncStageSDKErrorCode>
```

Parameters:

* `applicationSecretKey` - secret for SDK provisioning

* `applicationSecretId` - id of secret for SDK provisioning

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


### Get zones list

Gets available Zones list, where a session can be created

```typescript
async zoneList(): Promise<[IZonesInRegionsList | null, SyncStageSDKErrorCode]>
```

### Create a session

Creates a session in a given zone by a given user from your user pool.

```typescript
async createSession(
    zoneId: string,
    userId: string
): Promise<[ISessionIdentifier | null, SyncStageSDKErrorCode]>
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend

### Join the session

Joins a particular session identified by `sessionCode`.

```typescript
async join(
    sessionCode: string,
    userId: string,
    displayName?: string | null,
    latitude?: number | null,
    longitude?: number | null,
): Promise<[ISession | null, SyncStageSDKErrorCode]>
```

Parameters:

* `sessionCode` - the session code

* `userId` - id of your app user to match de data between SyncStage and your backend

* `displayName` - your app user display name

* `latitude` - current location latitude

* `longitude` - current location longitude

!!! note

    Latitude and longitude are now optional parameters, in the future releases it will be used to further optimize the latency.

!!! warning

    SyncStage **Web** SDK is available only in a preview version. It is expected to be available to use by the end of May 2023.

    
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
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```typescript
async getReceiverMeasurements(identifier: string): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
```

Parameters:

* `identifier` - receiver's identifier


### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```typescript
async getTransmitterMeasurements(): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
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
