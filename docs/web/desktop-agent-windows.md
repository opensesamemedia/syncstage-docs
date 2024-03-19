!!! warning
    Desktop Agent for Windows is currently in preview mode and may not fully reflect the final product. It may not yet implement all functionalities, and latency performance may not yet meet the desired level.

To provide low-latency capabilities SyncStage uses platform-specific optimizations, not available from the browser's engine. Therefore, we have introduced a SyncStage Agent, an application that be installed in the system and run in the background. 

[Latest SyncStage Desktop Agent for Windows]({{ latest_desktop_agent_for_windows_url }}){ .md-button}

### Versions
#### 0.1.0 <small>January 4, 2024</small> { id="0.1.0" }
##### Compatibility
* Compatible with Web SDK >= 0.4.0
  
##### Known issues
* Received audio streams may sound robotic.
* Audio latency levels are not yet optimized for the best possible user experience.
* Volume control sliders are not currently implemented.
* The ability to mute or unmute audio streams is not yet available.
* Some of the responses are mocked e.g. getReceiverMeasurements, getTransmitterMeasurements
* Certain responses, such as getReceiverMeasurements and getTransmitterMeasurements, are currently mocked for testing purposes.
* The initial state of the "microphone muted" indicator for receivers may not be accurate. This issue should be resolved after the first change in microphone mute status.
* The user connectivity status indicator may not be accurate.In some cases, it may indicate connection problems even when the connection is correct.
* The ability to dynamically change audio inputs and outputs is not yet supported.
* Audio devices, such as microphones or headphones, connected after Desktop Agent startup will not be detected automatically. Please restart Desktop Agent for these changes to take effect.


##### Changelog
###### Added
* Support for basic flow from provisioning to joining the session.
* Support for all main browsers.
