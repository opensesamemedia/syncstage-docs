
### 0.4.0 <small>January 4, 2024</small> { id="0.4.0" }
#### Modified
* Added new error code NO_INPUT_DEVICE, returned on join session when no input device is detected
* Added two methods to the ISyncStageDesktopAgentDelegate interface: desktopAgentConnected and desktopAgentDisconnected
* Renamed method updateOnDesktopAgentReconnected to updateOnWebsocketReconnected
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
