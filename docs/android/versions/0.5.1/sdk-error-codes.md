## [:octicons-tag-24: 0.5.1][0.5.1]{target=_blank}
[0.5.1]: https://github.com/opensesamemedia/syncstage-test-app-android/releases/tag/0.5.1

Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using following enum class.

```kotlin
enum class SyncStageSDKErrorCode(val errorCode: Int) {
    UNKNOWN_ERROR(-1),
    OK(0),
    CONFIGURATION_ERROR(1),
    API_ERROR(2),
    API_UNAUTHORIZED(3),
    AUDIO_STREAMING_ERROR(4),
    STREAM_DOES_NOT_EXIST(5),
    BAD_VOLUME_VALUE(6),
    SESSION_NOT_JOINED(7),
    AUDIO_SERVER_NOT_REACHABLE(8),
}
```