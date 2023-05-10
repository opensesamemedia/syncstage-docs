## Before you begin

Before you start developing your application with the SyncStage SDK, you need to opt-in to Early Access Developer program and get your SyncStage SDK secrets. Once you have opted-in we will contact you to provide you with your SDK secrets.
The SDK secrets are your credentials that authenticates requests associated with your project. 

[Become an Early Access Deveoper](https://sync-stage.com/){ .md-button target=_blank}


## Stat with an example project
The best way to start with SyncStage is by trying out our example project available on GitHub [SyncStage Test App for Web](https://github.com/opensesamemedia/syncstage-sdk-npm-package-tester){target=_blank}. 


[Learn more](test-app.md){ .md-button }




## Use SyncStage SDK in your application
### 1. Add package dependency.
To get the latest npm package of the SyncStage SDK install it from: https://www.npmjs.com/package/@opensesamemedia/syncstage


### 2. Get SyncStage Desktop Agent

To use test application you need to install SyncStage Desktop Agent on your Mac.

[Download SyncStage Desktop Agent for macOS](https://syncstage.s3.amazonaws.com/Agent/SyncStageAgent_1.0.0.dmg){ .md-button}


### 3. Add SyncStageSecret to your .env file.
Create or update a `.env` file with SyncStageSecrets:
    ```bash
    REACT_APP_SYNCSTAGE_SECRET_ID=
    REACT_APP_SYNCSTAGE_SECRET_KEY=
    ```


### 4. Integrate the SyncStage class with your app.
Here you can find a list of:

* [SDK Methods](sdk-methods.md)
* [SDK Delegates](sdk-delegates.md)
* [SDK Error Codes](sdk-error-codes.md)

### 5. Switch to local SDK dependency
To work with local SDK package run:

```bash
yarn remove @opensesamemedia/syncstage
npm link ../syncstage-sdk-npm-package
```
