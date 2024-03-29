# Test App

The best way to start you journey with SyncStage is by trying out our example project available on GitHub [SyncStage Test App for Android](https://github.com/opensesamemedia/syncstage-test-app-android){target=_blank}.
This tutorial shows you how to clone, build, and run the application on your device. The recommended development environment is Android Studio.

## Set up your development project

Follow these steps to create the Test App project in Android Studio.

1. Download and install [Android Studio](https://developer.android.com/studio){target=_blank}.
2. Clone or download the [SyncStage Test App for Android](https://github.com/opensesamemedia/syncstage-test-app-android){target=_blank} repository from GitHub.
3. Import the project:
   1. In Android Studio, select File > New > Import Project.
   2. Go to the location where you saved the SyncStage Test App for Android repository.
   3. Find SyncStage project at this location.
   4. Select the project directory, then click Open. Android Studio now builds your project, using the Gradle build tool.


## Get a SyncStage SDK secret
To run the SyncStage Test App you need to add a SyncStageSecret.json file to your Android Studio project to the assets folder.

**Don't know how to get the secret file?** See our [Quickstart Guide](quickstart.md) for more details.



## Build and run your app
To build and run the app:

1. Connect an Android device to your computer. 
2. Follow the provided guidelines to activate developer options on your Android device and configure your system to detect the connected device.
3. In Android Studio, click the Run menu option (or :fontawesome-solid-play: button)
4. Select a device.
5. Android Studio invokes Gradle to build the app, and then runs it.

!!! note

    Android SyncStage SDK is not optimized against x86-64 architecture. Audio transmission might not work correctly in using the virtual device (AVD).


## Use the app

### Create a session  
1. Provide a nickname, e.g. *User-1*.
2. Let SyncStage find the best Studio Server location.
3. Click on the New Session button.
4. Share the session code and wait for others to join you.


| Provide nickname  | Automated server discovery | Discovery results |
:-------------------------:|:-------------------------:|:-------------------------:
![alt Enter your name](../assets/android/profile.jpg){ width="300" }  |  ![alt Automated server discovery](../assets/android/automated_selection.jpg){ width="300" } |  ![alt Discovery results](../assets/android/discovery_results.jpg){ width="300" }

| Create a session | Invite others |
:-------------------------:|:-------------------------:
![alt Create a session](../assets/android/create_session.jpg){ width="300" }  | ![alt Invite others](../assets/android/session_1_user.jpg){ width="300" } 



### Join a session
1. Provide a nickname, e.g. *User-2*.
2. Let SyncStage find the best Studio Server location.
3. Input the session code.
4. Click on the Join button.
5. Now *User-1* and *User-2* are ready to have a session together!

!!! note
    Currently, Studio Server discovery results for users that are joining the session are ignored - they join the session in the same location as the session creator. This is going to change in future releases.


| Provide nickname  | Automated server discovery | Discovery results |
:-------------------------:|:-------------------------:|:-------------------------:
![alt Enter your name](../assets/android/user_2_profile.jpg){ width="300" }  |  ![alt Automated server discovery](../assets/android/user_2_automated_selection.jpg){ width="300" } |  ![alt Discovery results](../assets/android/user_2_discovery_results.jpg){ width="300" }

| Join a session | Invite others |
:-------------------------:|:-------------------------:
![alt Join a session](../assets/android/join_session.jpg){ width="300" }  | ![alt Invite others](../assets/android/user_2_joined.jpg){ width="300" } 


Currently, SyncStage’s audio pipeline supports sessions with **up to 8 users. **



### Other functionalities

You can control volume levels of all participants on your end, each app user can mix volumes according to their needs. Anytime you can mute / unmute yourself or simply leave the session.


## Enable crashlytics
You can track any issues in your app with SyncStage SDK using Firebase and crashlytics. In order to enable this feature you need to create a project in Firebase console and add `google-services.json` credentials to the `app/` directory and uncomment following lines in `app/build.gradle` file:

```groovy
...
//    // TO BE UNCOMMENTED FOR CRASHLYTICS
//    id 'com.google.gms.google-services'
//    id 'com.google.firebase.crashlytics'
...
//    // TO BE UNCOMMENTED FOR CRASHLYTICS
//    implementation platform('com.google.firebase:firebase-bom:31.2.2')
//    implementation 'com.google.firebase:firebase-crashlytics-ktx'
//    implementation 'com.google.firebase:firebase-analytics-ktx'
...

```