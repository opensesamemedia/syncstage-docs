!!! warning
    Desktop agent for Windows is preview-only, it does not implement all of the methods yet, and does not provide low latency performance yet.

To provide low-latency capabilities SyncStage uses platform-specific optimizations, not available from the browser's engine. Therefore, we have introduced a SyncStage Agent, an application that be installed in the system and run in the background. 

[Latest SyncStage Desktop Agent for Windows]({{ latest_desktop_agent_for_windows_url }}){ .md-button}

### Versions
#### 0.1.0 <small>January 4, 2024</small> { id="0.4.0" }
##### Compatibility
* Compatible with Web SDK >= 0.4.0
  
##### Known issues
* Received audio streams may sound robotic.
* Audio latency level is not yet optimal.
* Volume sliders are not yet supported.
* Muting/unmuting is not yet supported.
* Some of the responses are mocked e.g. getReceiverMeasurements, getTransmitterMeasurements
* Receivers "microphone muted" states might be incorrect at the beginning of the session. They should synchronize after the first change.
* Connectivity status indicator may not reflect reality (can show indicate problems when the connection is fine).
* Changing the audio inputs/outputs on the fly is not handled.
* The audio device, e.g. microphone or headphones connected after the SyncStage Desktop Agent startup is not going to be detected. Restart the Desktop Agent to apply the change.


##### Changelog
###### Added
* Support for basic flow from provisioning to joining the session.
* Support for all main browsers.
