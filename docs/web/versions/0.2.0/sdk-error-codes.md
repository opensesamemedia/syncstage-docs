Most of the SDK methods return SyncStageSDKErrorCode which can be decoded using following enum class.

```typescript
enum SyncStageSDKErrorCode {
  'SYNCSTAGE_OPENED_IN_ANOTHER_TAB' = -1001,
  'API_UNAUTHORIZED' = -1000,
  'DESKTOP_AGENT_COMMUNICATION_ERROR' = -10,
  'UNKNOWN_ERROR' = -1,
  'OK' = 0,
  'CONFIGURATION_ERROR' = 1,
  'API_ERROR' = 2,
  'STREAM_DOES_NOT_EXIST' = 3,
  'BAD_VOLUME_VALUE' = 4,
  'NO_ZONE_AVAILABLE' = 5,
  'NO_STUDIO_SERVER_AVAILABLE' = 6,
}
```
