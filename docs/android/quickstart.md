???+ warning

    SyncStage SDK for Android is currently available only in PREVIEW-ONLY mode, which means it is not yet recommended for production usage.
## Before you begin

Before you start developing your application with the SyncStage SDK, you need to opt-in to Early Access Developer program and get your SyncStage SDK secrets. Once you have opted-in we will contact you to provide you with your SDK secrets.
The SDK secrets are your credentials that authenticates requests associated with your project. 

[Become an Early Access Developer](https://console.sync-stage.com/request-a-demo){ .md-button target=_blank}


## Start with an example project
The best way to start with SyncStage is by trying out our example project available on GitHub [SyncStage Test App for Android](https://github.com/opensesamemedia/syncstage-test-app-android){target=_blank}.


[Learn more](test-app.md){ .md-button }

## Use SyncStage SDK in your application
### 1. Add package dependency.
In the `settings.gradle` add SyncStage maven repository under `dependencyResolutionManagement` block. Please define `githubProperties` which will be used for package repository authentication.

```java
def githubProperties = new Properties()
githubProperties.load(new FileInputStream("github.properties"))

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven {
            url = uri("https://maven.pkg.github.com/opensesamemedia/syncstagesdkpackage")
            credentials {
                username = githubProperties['gpr.usr'] ?: System.getenv("GPR_USER")
                password = githubProperties['gpr.key'] ?: System.getenv("GPR_API_KEY")
            }
        }
    }
}

```

Android studio needs GitHub credentials with `read:packages` permission to fetch the SDK package.

In order to provide GitHub credentials please create a `github.properties` file in the root directory and paste following code:

```
gpr.usr=
gpr.key=
```

Under `gpr.usr` please provide you GitHub login, and under `gpr.key` paste GitHub token with `read:packages` permission. For information how to generate token please refer [here](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token){target=_blank}.

### 2. Add the following permissions to AndroidManifest.xml. 

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO"/>
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

Please note that most of those notifications must accepted by user explicitly.

### 3. Add SyncStageSecret.json to your Android Studio project to the assets folder.

SyncStageSecret.json is assigned to one application. File contains confidential credentials that allow access to your SyncStage resources. 

!!! warning

    We strongly recommend storing applicationSecretKey securely in your backend and provide it as a parameter at SyncStage SDK object instantiation. Having implemented the supply of the applicationSecretKey from your protected backend, you can remove that parameter from the .json.


### 4. Integrate the SyncStage class with your app.
Here you can find a list of:

* [SDK Methods](sdk-methods.md)
* [SDK Delegates](sdk-delegates.md)
* [SDK Error Codes](sdk-error-codes.md)


### 5. Use SyncStage in background

To allow SyncStage work in background you need to create a [foreground service](https://developer.android.com/guide/components/foreground-services){target=_blank} of `microphone` type.
Service and additional permissions must be added to `AndroidManifest.xml`.

```xml
...

    <service
        android:name=".YourForegoundServiceName"
        android:foregroundServiceType="microphone" 
    />
</application>

<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
```


## Troubleshooting
### SDK does not work as expected, but the application is building and running, what can I do about it?
Some problems might occur if the application user did not grant all required permissions on their device. Before using the SyncStage object, make sure that all of the required permissions are granted.

