## SDK
SyncStage SDK `0.4.0` for Android contains some known issues. However, we are diligently working to resolve them in upcoming releases.

* When headphones without a microphone are connected, the internal microphone must be manually enabled.
* Bluetooth audio devices, e.g. headsets, speakers, are not yet fully supported.

## Test App
Additionally, there are known issues in the SyncStage Test App that are not related to the SDK itself.

* Some of the user participants records get duplicated in the test app its due to race conditions. List of users needs to be changed to map of users in the session.

* State of internal microphone and direct monitor will be not up to date after plugging in / out headphones