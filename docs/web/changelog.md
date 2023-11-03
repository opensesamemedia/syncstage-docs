### 0.4.0 <small>September 15, 2023</small> { id="0.4.0" }
#### Added
* getDesktopAgentProtocolHandler method - returns URI that opens Desktop Agent on Windows

#### Modified

* Init method, removed agent port parameter.


### 0.3.0 <small>September 15, 2023</small> { id="0.3.0" }
#### Modified

* Init method now accepts a time-limited token instead of a SyncStage Secret.
* SyncStage constructor extended with onTokenExpired callback parameter.

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
