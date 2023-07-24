## SDK
SyncStage SDK `0.1.0` for Web contains some known issues. However, we are diligently working to resolve them in upcoming releases.

### Possible secrets leak
Currently, SyncStage SDK secrets are passed between the Web SDK and the Desktop Agent in an unencrypted manner. Application users can sniff and reuse them. For this reason, SyncStage SDK `0.1.0` for Web is not yet recommended for production use.

### >100 ms latency
The default [Latency Optimization Level](../../low-latency-experience/#latency-optimization-level) in SyncStage SDK `0.1.0` for Web is `Optimized` and it cannot be changed. It means that SyncStage is set to focus on providing high audio quality, even in imperfect network conditions instead of delivering ultra low and stable latency. In result, audio latency rarely achieves sub-100 ms values. [Latency Optimization Level](../../low-latency-experience/#latency-optimization-level) selection will be available in future releases of Web SDK.
