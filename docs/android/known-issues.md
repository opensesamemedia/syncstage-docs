## SDK
SyncStage SDK `0.6.1` for Android contains some known issues. However, we are diligently working to resolve them in upcoming releases.

* When headphones without a microphone are connected, the internal microphone must be manually enabled.
* Bluetooth audio devices, e.g. headsets, speakers, are not yet fully supported.

## Test App
Additionally, there are known issues in the SyncStage Test App that are not related to the SDK itself.

* State of internal microphone and direct monitor will be not up to date after plugging in / out headphones
* After a few hours of remaining idle, the background app becomes UNAUTHORIZED. The user needs to either restart the application or return to the welcome screen and navigate through the entire application flow again.
