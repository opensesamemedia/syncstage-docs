# Test App

The best way to start you joyrney with SyncStage is by trying out our example project available on GitHub [SyncStage Test App for iOS](https://github.com/opensesamemedia/syncstage-test-app-ios){target=_blank}.
This tutorial shows you how to clone, build, and run the application on your device.

## Set up your development project

Follow these steps to create the Test App project in Xcode.

1. Download and install [Xcode](https://developer.apple.com/xcode/){target=_blank}.
2. Clone or download the [SyncStage Test App for iOS](https://github.com/opensesamemedia/syncstage-test-app-ios){target=_blank} repository from GitHub.
3. Open (double-click) the project's project.xcworkspace file to open it in Xcode. You must use the .xcworkspace file to open the project.
 

## Get a SyncStage SDK secret
To run the SyncStage Test App you need to add a SyncStageSecret.plist to your Xcode project. Make sure that it is added to the “Copy Bundle Resources” in the target build phases.

**Don't know how to get the secret file?** See the [Quickstart Guide](quickstart.md) for more details.


## Build and run the app
To build and run the app:

1. Connect an iOS device to your computer, or select a simulator from the Xcode scheme pop-up menu.
2. In Xcode, click the Product/Run menu option (or :fontawesome-solid-play: button).
3, Xcode builds the app, and then runs the app on the device or on the simulator.


## Use the app

### Create a session  
You first provide an app username (in this example the first user is called ‘Mateusz’), then you can get a studio server using automated selection option where we provide you with the best available studio server, or you can select it manually from the list after disabling 'automated selection' option. To get the best latency experience choose the one that is the nearest to expected geolocation of your users. Next you can select the New session button. Once a session is created you will see yourself represented as ‘You’ and be able to share the session code, so that you can invite others. Share the code and wait for others to join you.
![alt Create a Session](../assets/createsession.png "Create a Session")

### Join a session
The second user - in this example ‘Steve’ - inputs the session code and joins the session (NOTE: you will see on his device, he has the app username of the first user, ‘Mateusz’). Now you are ready to have a synchonous session together!

![alt Join a session 1st user perspective](../assets/join_steve.png "Join a session 1st user perspective")

User Mateusz will be prompted that Steve has joined the session on his device. SyncStage’s audio pipeline supports sessions with up to 8 users. 

![alt Join a session 2nd user perspective](../assets/join_mateusz.png "Join a session 2nd user perspective")



### Other functionalities

You can control volume levels of all participants on your end, each app user can mix volumes according to one's needs. Anytime you can mute / unmute yourself or simply leave the session.
