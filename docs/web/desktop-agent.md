To provide low-latency capabilities SyncStage uses platform-specific optimizations, not available from the browser's engine. Therefore, we have introduced a SyncStage Agent, an application that be installed in the system and run in the background. 


## MAC OS

[Latest SyncStage Desktop Agent for macOS]({{ latest_desktop_agent_for_macos_url }}){ .md-button}

### Changelog
#### 0.3.0 <small>December 15, 2023</small> { id="0.3.0" }
##### Added

* Support for all main browsers
* Opening Desktop Agent from the browser

???+ note

    SyncStage Desktop Agent v0.3.0 for MacOS is incompatible Web SDK versions older than v0.3.0.


#### 0.2.0 <small>August 22, 2023</small> { id="0.2.0" }
##### Added

* Session recording

#### 0.1.1 <small>July 25, 2023</small> { id="0.1.1" }
##### Added

* Latency Optimization Level selection.

#### 0.1.0 <small>July 17, 2023</small> { id="0.1.0" }
First Desktop Agent release.


## Windows
!!! warning
    Desktop agent for Windows is preview-only, it does not implement all of the methods yet, and does not provide low latency performance yet.

[Latest SyncStage Desktop Agent for Windows]({{ latest_desktop_agent_for_windows_url }}){ .md-button}

### Changelog
#### 0.1.0 <small>January 1, 2024</small> { id="0.4.0" }
* Covers basic flow from provisioning to joining the session.
* Support for all main browsers
* Audio latency is not optimized
* Some of the responses are mocked e.g. getReceiverMeasurements, getTransmitterMeasurements
* Compatible with Web SDK >= 0.4.0