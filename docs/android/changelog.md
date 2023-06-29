???+ warning

    SyncStage SDK for Android is currently available only in PREVIEW-ONLY mode, which means it is not yet recommended for production usage.

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
