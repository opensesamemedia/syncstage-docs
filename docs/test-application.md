## iOS and Android
Please visit our GitHub to clone and discover the [iOS project](https://github.com/opensesamemedia/syncstage-test-app-ios){target=_blank} or the  [Android project](https://github.com/opensesamemedia/syncstage-test-app-android){target=_blank} presenting how the SDK can be integrated into the application. To get authorized to the SyncStage backend you need to add SyncStageSecret file to your application. Instructions on how to do that can be found in the __'How to integrate SDK'__ section.

### Create a session  

![alt Create a Session](assets/createsession.png "Create a Session")

You first provide an app username (in this example the first user is called ‘Mateusz’), select the New session button and select location of the deployment. To get the best latency experience choose the one that is the nearest to expected geolocation of your users. Once a session is created you will see yourself represented as ‘You’ and be able to share the session code, so that you can invite others. Share the code and wait for others to join you.

### Join a session

![alt Join a session 1st user perspective](assets/join_steve.png "Join a session 1st user perspective")

The second user - in this example ‘Steve’ - inputs the session code and joins the session (NOTE: you will see on his devic, he has the app username of the first user, ‘Mateusz’). Now you are ready to synchronize together!

![alt Join a session 2nd user perspective](assets/join_mateusz.png "Join a session 2nd user perspective")

User Mateusz will be prompted that Steve has joined the session on his device. SyncStage’s audio pipeline supports sessions with up to 8 users. 

### Other functionalities

You can control volume levels of all participants on your end, each app user can mix volumes according to one's needs. Anytime you can mute / unmute yourself or simply leave the session.


## Webbrowser

Please visit our GitHub to clone and discover the [iOS project](https://github.com/opensesamemedia/syncstage-test-app-ios){target=_blank} or the  [Android project](https://github.com/opensesamemedia/syncstage-test-app-android){target=_blank} presenting how the SDK can be integrated into the application. To get authorized to the SyncStage backend you need to provision it with SyncStageSecret.

Deployed test application is available [here](https://syncstagebrowsersdktestapp.web.app/).

Firstly you will be asked to install Desktop Agent on your Mac.
![alt Install Desktop Agent](assets/browser/setup-1.png "Install Desktop Agent")

Once installed you will see
![alt Install Desktop Agent Installed](assets/browser/setup-2.png "Install Desktop Agent Installed")

Input nickname of the user that will join the session
![alt Nickname](assets/browser/profile.png "Nickname")

You can now join the existing session
![alt Nickname](assets/browser/join.png "Nickname")

or create a new one
![alt Nickname](assets/browser/create.png "Nickname")

Enjoy your low latency session
![alt Nickname](assets/browser/session.png "Nickname")