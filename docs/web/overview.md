!!! warning

    SyncStage **Web** SDK is available only in a preview version. It is expected to be available to use by the end of June 2023.

SyncStage SDK for Web brings low latency communication capabilities to your desktop. 

It consists of two componens:

* SyncStage Web SDK (TypeScript & JavaScript) embedded into your web application.
* SyncStage Agent running on your destkop.

SyncStage SDK for Web current version: `v0.0.1` ([View changelog](changelog.md))

[Install SDK](quickstart.md){ .md-button .md-button--primary} 
<!-- [Test SyncStage Web SDK on macOS](https://syncstagebrowsersdktestapp.web.app/){ .md-button target=_blank } -->

## Requirements 
### Browser
Currently, **only Google Chrome is supported**. We are working to cover all the main browsers.

### Platform
SyncStage Agent, necessary to establish audio communications, is currently available only for macOS. Both Intel and Apple chips are supported. We are working to bring SyncStage to other platforms, i.e. Windows and Linux.


## Why do I need SyncStage Agent?
To provide low-latency capabilities SyncStage uses platform-specific optimizations, not available from the browser's engine. Therefore, we introduced a SyncStage Agent, an application that be installed in the system and run in the background. 
