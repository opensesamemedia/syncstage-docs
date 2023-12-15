SyncStage SDK for Web brings low latency communication capabilities to your desktop.

It consists of two three:

* SyncStage Web SDK (TypeScript & JavaScript) embedded into your web application.
* SyncStage Agent running on your desktop.

SyncStage SDK for Web latest version: `{{ latest_web_sdk_version }}` ([View changelog](changelog.md))

[Get SDK](quickstart.md){ .md-button .md-button--primary}
[Test SyncStage Web SDK on macOS](https://github.com/opensesamemedia/syncstage-sdk-npm-package-tester){ .md-button target=_blank }

## Why do I need SyncStage Agent?

To provide low-latency capabilities SyncStage uses platform-specific optimizations, not available from the browser's engine. Therefore, we have introduced a SyncStage Agent, an application that be installed in the system and run in the background.

## Requirements

### Platform

SyncStage Agent, necessary to establish audio communications, is currently available only for macOS. Both Intel and Apple chips are supported. We are working to bring SyncStage to other platforms, i.e. Windows and Linux.

| Browser                              | Support                        |       Comment             |
| ------------------------------------ | -----------------------------: | ------------------------: |
| :fontawesome-brands-apple: MacOS     |  :fontawesome-solid-check:{ .icon-check }     |                           |
| :fontawesome-brands-windows: Windows  |  :fontawesome-solid-x:{ .icon-x }         |   Work in progress        |
| :fontawesome-brands-linux: Linux     |  :fontawesome-solid-x:{ .icon-x }         |   Work in progress        |
