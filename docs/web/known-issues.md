## SDK
SyncStage Web SDK `0.2.0` for Web contains some known issues. However, we are diligently working to resolve them in upcoming releases.

### Possible secrets leak
Currently, SyncStage SDK secrets are passed between the Web SDK and the Desktop Agent in an unencrypted manner. Application users can sniff and reuse them. For this reason, SyncStage SDK `0.2.0` for Web is not yet recommended for production use.
