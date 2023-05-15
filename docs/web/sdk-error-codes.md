!!! warning

    SyncStage **Web** SDK is available only in a preview version. It is expected to be available to use by the end of May 2023.

Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using following enum class.

```typescript
enum SyncStageSDKErrorCode {
    'UNKNOWN_ERROR'=-1, 
    'OK'=0,
    'CONFIGURATION_ERROR'=1,
    'API_ERROR'=2,
    'API_UNAUTHORIZED'=3,
    'AUDIO_STREAMING_ERROR'=4,
    'STREAM_DOES_NOT_EXIST'=5, 
    'BAD_VOLUME_VALUE'=6,
    'SESSION_NOT_JOINED'=7,
    'AUDIO_SERVER_NOT_REACHABLE'=8,
    'DESKTOP_AGENT_COMMUNICATION_ERROR' = 9,
}
```