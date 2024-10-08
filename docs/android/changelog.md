### 0.6.1 <small>April 9, 2024</small> { id="0.6.1" }

#### Modified
* Enabled network slicing
* Extended analytics data collected by the SDK (network slicing)
* Fixed connectivity dot indicator
* minor improvements in the test application

### 0.6.0 <small>October 24, 2023</small> { id="0.6.0" }

#### Modified

* Modified `init` method of the `SyncStage` class


### 0.5.2 <small>September 22, 2023</small> { id="0.5.2" }

#### Added

* Methods for managing latency optimization level

#### Fixed

* Fixed sampling frequency issues on some devices with Android < 12
* Improved TCP/UDP switching

### 0.5.1 <small>September 1, 2023</small> { id="0.5.1" }

#### Fixed

* Fixed crash on latency measurement timeouts

### 0.5.0 <small>August 18, 2023</small> { id="0.5.0" }

#### Added

* Session recording

#### Changed

* Improved handover handling

### 0.4.1 <small>August 18, 2023</small> { id="0.4.1" }
#### Changed

* Improved auto input output device switching when headphones are connected / disconnected
* SyncStage collects analytics data for product improvement

### 0.4.0 <small>July 21, 2023</small> { id="0.4.0" }

#### Added

* Security improvements
* Get best available server
* Get server instances
* SyncStage discovery delegate
* stop() method for disposing all SyncStage background threads

#### Changed

* Create session parameters
* Join session parameters

#### Removed

* Zone list (Replaced by: [getServerInstances](sdk-methods.md/#get-server-instances){ target=_blank})


### 0.3.0 <small>May 12, 2023</small> { id="0.3.0" }

#### Fixed

* Disabling the internet connection during a session leads to an app crash.
* Losing network coverage results in the app crashing.
* Users may be removed from a session when the app runs in the background and the screen is locked.

### 0.2.0 <small>April 26, 2023</small> { id="0.2.0" }
#### Added

* Toggle direct monitor
* Get direct monitor volume
* Get direct monitor state
* Get internal microphone state
* Get SDK version

#### Changed
* method `zonesList` is renamed to `zoneList`

#### Fixed
* Internal microphone crashes
* Crashes of API calls when there is no internet connection

### 0.1.0 <small>January 3, 2023</small> { id="0.1.0" }
#### Added

* Create session
* Join session
* Leave session
* Mute streams
* Change stream volumes
* Toggle internal microphone
* Get network measurements
