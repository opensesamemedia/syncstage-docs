### 0.6.2 <small>May 21, 2024</small> { id="0.6.2" }

### Changed

* Extended NAT support for better IPv6 networks handling

### 0.6.1 <small>April 25, 2024</small> { id="0.6.1" }

#### Added

* Fixed network latency test to Studio Servers
* Added Privacy Manifest required by Apple

### 0.6.0 <small>April 9, 2024</small> { id="0.6.0" }

#### Added

*  Added Noise Cancellation

### 0.5.2 <small>March 19, 2024</small> { id="0.5.2" }

#### Added

* Session code
* Is Direct Monitor enabled


### 0.5.1 <small>October 18, 2023</small> { id="0.5.1" }

#### Added

* Session name
* Session tags
* Prefer fast routing option


### 0.5.0 <small>August 14, 2023</small> { id="0.5.0" }

#### Added

* Session recording
* Analytics

### 0.4.0 <small>June 27, 2023</small> { id="0.4.0" }

SyncStage SDK v0.4.0 for iOS is the first production-ready release!

#### Added

* Security improvements
* Get best available server
* Get server instances
* Change latency optimization level
* Get latency optimization level
* SyncStage discovery delegate

#### Changed

* Create session parameters
* Join session parameters

#### Removed

* Zone list (Replaced by: [getServerInstances](sdk-methods.md/#get-server-instances){ target=_blank})
* Change quality coefficient (Replaced by: [changeLatencyOptimizationLevel](sdk-methods.md/#change-latency-optimization-level){ target=_blank})
* Get quality coeffient (Replaced by: [getLatencyOptimizationLevel](sdk-methods.md/#get-latency-optimization-level){ target=_blank})


???+ warning

    SyncStage SDK v0.4.0 for iOS is incompatible with the previous SDK versions.


### 0.3.1 <small>April 14, 2023</small> { id="0.3.1" }
#### Added
* Audio quality and latency improvements
* Change quality coefficient
* Get quality coefficient

### 0.3.0 <small>April 2, 2023</small> { id="0.3.0" }
#### Added
* TCP fallback resolving NAT issues
* Audio quality and latency improvements

### 0.2.0 <small>December 2, 2022</small> { id="0.2.0" }
#### Added

* Displaying network measurements

#### Changed

* Transmitter identifier is removed from the leave session method.

### 0.1.0 <small>November 18, 2022</small> { id="0.1.0" }
#### Added

* Create session
* Join session
* Leave session
* Mute streams
* Change stream volumes
