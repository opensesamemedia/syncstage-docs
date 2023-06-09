Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using the following enum.

```swift
public enum SyncStageErrorCode: Int {
  case unknownError = -1
  case ok = 0
  case configurationError = 1
  case apiError = 2
  case apiUnauthorized = 3
  case audioStreamingError = 4
  case streamDoesNotExist = 5
  case badVolumeValue = 6
  case userAlreadyUsed = 7
  case audioServerNotReachable = 8
}
```