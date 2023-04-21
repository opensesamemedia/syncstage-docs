## NPM package

To get the latest npm package of the SyncStage SDK install it from: https://www.npmjs.com/package/@opensesamemedia/syncstage

## SDK methods

#### Constructor 
```
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

#### Initialize

Initializes the SDK SyncStage object.

```
async init(
        applicationSecretId: string,
        applicationSecretKey: string
    ): Promise<SyncStageSDKErrorCode>
```

Parameters:

* `applicationSecretKey` - secret for SDK provisioning

* `applicationSecretId` - id of secret for SDK provisioning

#### Get zones list

Gets available Zones list, where a session can be created

```
async zonesList(): Promise<[IZonesInRegionsList | null, SyncStageSDKErrorCode]>
```

#### Create a session

Creates a session in a given zone by a given user from your user pool.

```
async createSession(
    zoneId: string,
    userId: string
): Promise<[ISessionIdentifier | null, SyncStageSDKErrorCode]>
```

Parameters:

* `zoneId` - zone in which we want to host our session
* `userId` - id of your app user to match the data between SyncStage and your backend

#### Join the session

Joins a particular session identified by `sessionCode`.

```
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

__Note:__ latitude and longitude are now optional parameters, in the future releases it will be used to improve the synchrinization throughout sessions.

#### Get session state

Gets state of currently joined session.

```
async session(): Promise<[ISession | null, SyncStageSDKErrorCode]> 
```


#### Leave the session

Leaves currently joined session.

```
async leave(): Promise<SyncStageSDKErrorCode> 
```

#### Mute / unmute microphone

Enables or disables microphone stream.

```
async toggleMicrophone(mute: boolean): Promise<SyncStageSDKErrorCode>
```

Parameters:

* `mute` - desired state of the mute option

#### Is muted

Returns state of microphone stream.

```
async isMicrophoneMuted(): Promise<[boolean | null, SyncStageSDKErrorCode]>
```

#### Get receiver network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
async getReceiverMeasurements(identifier: string): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
```

Parameters:

* `identifier` - receiver's identifier


#### Get transmitter network measurements
Returns Mesurements object with network delay, jitter, and calculated network quality indicators.

```
async getTransmitterMeasurements(): Promise<[IMeasurements | null, SyncStageSDKErrorCode]>
```


### SyncStage delegates
SyncStage class provide two delegate:, `ISyncStageUserDelegate` and `ISyncStageConnectivityDelegate` which provide a set of callbacks to inform your application about asynchronous events from the SyncStage. You can define those object and provide to the SyncStage constructor or update public SyncStage properties `userDelegate` and `connectivityDelegate` anytime.

#### SyncStageUserDelegate
Responsible for getting callbacks about users' state in the session.

```
interface ISyncStageUserDelegate {
  userJoined(connection: IConnection): void;
  userLeft(identifier: string): void;
  userMuted(identifier: string): void;
  userUnmuted(identifier: string): void;
  sessionOut(): void;
}

```

#### SyncStageConnectivityDelegate
Responsible for getting callbacks about users' connectivity in the session.

```
interface ISyncStageConnectivityDelegate {
  transmitterConnectivityChanged(connected: boolean): void;
  receiverConnectivityChanged(identifier: string, connected: boolean): void;
}
```

### SyncStage SDK Error Codes

Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using following enum class.

```
enum SyncStageSDKErrorCode {
    'UNKNOWN_ERROR'=-1, 
    'OK'=0,
    'CONFIGURATION_ERROR'=1,
    'API_ERROR'=2,
    'API_UNAUTHORIZED'=3,
    'AUDIO_STREAMING_ERROR'=4,
    'STREAM_DOES_NOT_EXIST'=5, 
    'BAD_VOLUME_VALUE'=6,
    'SESSION_NOT_JOINED'=7,
    'AUDIO_SERVER_NOT_REACHABLE'=8,
    'DESKTOP_AGENT_COMMUNICATION_ERROR' = 9,
}
```
