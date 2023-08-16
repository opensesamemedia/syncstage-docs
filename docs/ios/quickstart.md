## Before you begin

Before you start developing your application with the SyncStage SDK, you need to opt-in to Early Access Developer program and get your SyncStage SDK secrets. Once you have opted-in we will contact you to provide you with your SDK secrets.
The SDK secrets are your credentials that authenticates requests associated with your project. 

[Become an Early Access Developer](https://console.sync-stage.com/request-a-demo){ .md-button target=_blank}


## Start with an example project
The best way to start with SyncStage is by trying out our example project available on GitHub [SyncStage Test App on iOS](https://github.com/opensesamemedia/syncstage-test-app-ios){target=_blank}.


## Use SyncStage SDK in your application
### 1. Add package dependency.

```
dependencies: [
    .package(url: "https://github.com/opensesamemedia/SyncStageSwiftPackage.git", .upToNextMajor(from: "0.5.0"))
]
```

### 2. Add the following permissions to info.plist. 

```
Privacy - Microphone Usage Description (Need microphone access for audio recording)
Privacy - Camera Usage Description (No need for camera access), required by ffmpeg
Privacy - Location When In Use Usage Description, required to get better service results
Privacy - Location Default Accuracy Reduced, set it to YES, no need for accurate location.

```

### 3. Enable background modes.

SyncStage SDK requires the audio background mode to be enabled to allow streaming, recording in background.

`Audio, AirPlay, Picture in Picture`

### 4. Add SyncStageSecret.plist to your xcode project, and make sure that it is added to the “Copy Bundle Resources” in the target build phases.

SyncStageSecret.plist is assigned to one application. File contains confidential credentials that allow access to your SyncStage resources. 

!!! security "Security tip"
    
    We strongly recommend storing applicationSecretKey securely in your backend and provide it as a parameter at SyncStage SDK object instantiation. Having implemented the supply of the applicationSecretKey from your protected backend, you can remove that parameter from the .plist.


### 5. Integrate the SyncStage class with your app.
Here you can find a list of:

* [SDK Methods](sdk-methods.md)
* [SDK Delegates](sdk-delegates.md)
