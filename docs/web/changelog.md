### 0.6.0 <small>May 7, 2024</small> { id="0.6.0" }
#### Added
* `isCompatible` method
* `checkProvisionedStatus` method
* `onDesktopAgentDeprovisioned` and `onDesktopAgentProvisioned` callbacks to 

#### Modified
* Renamed method `updateOnDesktopAgentReconnected` to `updateOnWebsocketReconnected` to `ISyncDesktopAgentDelegate`
* Renamed `isRecording` field in ISession to `recordingStatus` which can be set to values from list: `['stopped', 'started']`
* Extended `ISessionInfo` with `sessionName` field
* Updated type of `sessionCode` field within `ISessionInfo` to `string`

#### Fixed
* Fixed breaking websocket connections to Desktop Agent due to possibility to run the SyncStage SDK in the [web worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Worker){target=_blank}

### 0.5.0 <small>April 9, 2024</small> { id="0.5.0" }
This SDK version provides auto-location selection without explicit latency measurements and selection.
#### Removed
* removed location screens from the test application
* removed redundant `desktopAgentConnectionKeepAlive` and `desktopAgentLostConnection` from the ` ISyncStageDesktopAgentDelegate`

#### Modified
* reordered createSession method parameters
* `creteSession` zoneId and `studioServerId` parameters are optional and deprecated (likely to be removed in the next versions)
* reordered join method parameters
* join `zoneId` and `studioServerId` parameters are optional and deprecated (likely to be removed in the next versions)
* `getBestAvailableServer()` marked as deprecated
* extended `ISyncStageDiscoveryDelegate` with `serverSelected(selectedServer: IServerInstance): void;` callback
* fixed test application stability issues

#### Added
* `'STUDIO_SERVER_NOT_FOUND' = -12` SyncStageSDKErrorCode returned in case no Studio Server is available
* `getSelectedServer()` method

### 0.4.3 <small>March 22, 2024</small> { id="0.4.3" }

#### Modified
* Fixed SyncStage service websocket URL
* Updated test application:
    * fixed hanging updateMeasurements interval in the session screen
    * updated link to the Mac Desktop Agent


### 0.4.2 <small>March 19, 2024</small> { id="0.4.2" }
#### Modified
* Fixed communication issues with SyncStage Desktop Agent
* Updated SyncStageErrorCodes list
    * Changed `SYNCSTAGE_OPENED_IN_ANOTHER_TAB` value
    * Added `NOT_IN_SESSION`, `SYNCSTAGE_SERVICE_COMMUNICATION_ERROR`, `TIMEOUT_ERROR`
    * Removed `DESKTOP_AGENT_COMMUNICATION_ERROR`
* Extended ISyncStageDesktopAgentDelegate with two methods:
    * `desktopAgentConnectionKeepAlive(): void`
    *  `desktopAgentLostConnection(): void`
* Updated flow of test application which improves user experience, and reorganizes the project structure:
    * Caching last selected location, nickname
    * Auto SyncStage initialization
    * Joining session from URL
    * Desktop Agent Link indicator (based on keep alive callbacks from `ISyncStageDesktopAgentDelegate`)
    * Updated routing and navigation
* Added session code to `ISession` and `ISessionInfo` interfaces

### 0.4.1 <small>January 4, 2024</small> { id="0.4.1" }
#### Modified
* Fixed service websocket URL

### 0.4.0 <small>January 4, 2024</small> { id="0.4.0" }
#### Modified
* Added new error code NO_INPUT_DEVICE, returned on join session when no input device is detected
* Added two methods to the ISyncStageDesktopAgentDelegate interface: desktopAgentConnected and desktopAgentDisconnected
* Renamed method `updateOnDesktopAgentReconnected` to `updateOnWebsocketReconnected`
* Updated the test app to be compatible with the SDK 0.4.0

### 0.3.0 <small>December 15, 2023</small> { id="0.3.0" }
#### Modified
* getDesktopAgentProtocolHandler method - returns URI that opens Desktop Agent.
* Init method now accepts a time-limited token instead of a SyncStage Secret.
* SyncStage constructor extended with onTokenExpired callback parameter.
* Init method, removed agent port parameter.

#### Added
* New error code for expired token
* Method for updating token

### 0.2.0 <small>August 18, 2023</small> { id="0.2.0" }
#### Added

* Start and stop recording methods.

#### Modified

* SyncStageUserDelegate - new methods
### 0.1.0 <small>June 30, 2023</small> { id="0.1.0" }
#### Added

All SyncStage SDK methods implemented. Works with Desktop Agent on MAC.

### 0.0.1 <small>March 27, 2023</small> { id="0.0.1" }
#### Added

Mock methods for:

* Create session
* Join session
* Leave session
* Mute streams
* Change stream volumes
