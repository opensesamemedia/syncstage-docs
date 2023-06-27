Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using the following enum.

```swift
public enum SyncStageErrorCode: Int {
    case unknownError = -1
    case ok = 0
    case configurationError = 1
    case apiError = 2
    case streamDoesNotExist = 3
    case badVolumeValue = 4
    case noZoneAvailable = 5
    case noStudioServerAvailable = 6
}
```
