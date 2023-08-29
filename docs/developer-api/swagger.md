<!-- <swagger-ui src="https://7gsdl864qk.execute-api.us-east-1.amazonaws.com/swagger.json"/> -->

For your convenience, we offer a developer API to facilitate backend integration. Below, you will find interactive Swagger documentation that describes the REST API in detail. In order to interact with the API, you are required to request a token that is associated with your organization within SyncStage. It is crucial to securely store this token. The API token grants access to sensitive information such as billing details, recordings, and session management.

Firstly, your backend needs to authenticate using the endpoint `/developer-api/login` and the provided token. The jwt will expire after the duration specified in the `expiresIn` [seconds] field of the response.

After obtaining the `/developer-api/login` response, your backend should include the JWT token in the `Authentication` header to execute any other methods.

```
GET /developer/<some-endpoint> HTTP/1.1
Host: api.syncstage.com
Authorization: Bearer <jwt>
```

<swagger-ui src="./swagger.json"/>
