# Using Web Worker

The SyncStage SDK uses WebSocket to communicate with the Desktop Agent, maintaining a persistent connection that allows real-time communication between the two system components.

## The Problem with Browsers
When a browser tab is not active or the browser is running in the background, the browser optimizes its resources. This optimization can lead to the freezing and disconnection of WebSocket connections. This behavior can corrupt the state of SyncStage for users, leading to an inconsistent user experience.

## The Solution: Web Workers
To circumvent this issue, in the SyncStage web [test application](https://github.com/opensesamemedia/syncstage-sdk-npm-package-tester){ target=_blank } we run the SyncStage class within a [Web Worker](https://developer.mozilla.org/en-US/docs/Web/API/Web_Worker){target=_blank}. Web Workers are a simple means for web content to run scripts in background threads. The worker thread can perform tasks without interfering with the user interface.

In addition, workers utilize thread-like message passing to achieve parallelism. They're perfect for performing processing or computation that would otherwise block the UI thread.

When SyncStage is run within a Web Worker, the WebSocket connection is not disturbed by the browser's optimization process. This ensures that the SyncStage state remains consistent for users, regardless of whether the browser tab is active or not.

## Web Worker
Below you can find our implementation of the web worker in the [test application](https://github.com/opensesamemedia/syncstage-sdk-npm-package-tester){ target=_blank }. Folowing script should be saved as  `worker.js` in the application project scope.

```javascript
import SyncStage from '@opensesamemedia/syncstage-sdk-npm-package-development';
import SyncStageUserDelegate from './SyncStageUserDelegate';
import SyncStageConnectivityDelegate from './SyncStageConnectivityDelegate';
import SyncStageDiscoveryDelegate from './SyncStageDiscoveryDelegate';
import SyncStageDesktopAgentDelegate from './SyncStageDesktopAgentDelegate';

let syncStage;

self.onmessage = function (e) {
  const { id, method, args } = e.data;

  const userDelegate = new SyncStageUserDelegate(
    (connection) => {
      self.postMessage({ id: -1, result: { callback: 'onUserJoined', data: connection } });
    }, //onUserJoined
    (identifier) => {
      self.postMessage({ id: -1, result: { callback: 'onUserLeft', data: identifier } });
    }, //onUserLeft
    (identifier) => {
      self.postMessage({ id: -1, result: { callback: 'onUserMuted', data: identifier } });
    }, //onUserMuted
    (identifier) => {
      self.postMessage({ id: -1, result: { callback: 'onUserUnmuted', data: identifier } });
    }, //onUserUnmuted
    () => {
      self.postMessage({ id: -1, result: { callback: 'onRecordingStarted' } });
    }, //onRecordingStarted
    () => {
      self.postMessage({ id: -1, result: { callback: 'onRecordingStopped' } });
    }, //onRecordingStopped
    () => {
      self.postMessage({ id: -1, result: { callback: 'onSessionOut' } });
    }, //onSessionOut
  );
  const connectivityDelegate = new SyncStageConnectivityDelegate(
    (connected) => {
      self.postMessage({ id: -1, result: { callback: 'onTransmitterConnectivityChanged', data: connected } });
    }, //onTransmitterConnectivityChanged
    (identifier, connected) => {
      self.postMessage({ id: -1, result: { callback: 'onReceiverConnectivityChanged', data: { identifier, connected } } });
    }, //onReceiverConnectivityChanged
  );

  const discoveryDelegate = new SyncStageDiscoveryDelegate(
    (zones) => {
      self.postMessage({ id: -1, result: { callback: 'onDiscoveryResults', data: zones } });
    }, //onDiscoveryResults
    (results) => {
      self.postMessage({ id: -1, result: { callback: 'onDiscoveryLatencyTestResults', data: results } });
    }, //onDiscoveryLatencyTestResults
    (selectedServer) => {
      self.postMessage({ id: -1, result: { callback: 'onServerSelected', data: selectedServer } });
    }, //onServerSelected
  );
  const desktopAgentDelegate = new SyncStageDesktopAgentDelegate(
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentAquired' } });
    }, //onDesktopAgentAquired
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentReleased' } });
    }, //onDesktopAgentReleased
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentConnected' } });
    }, //onDesktopAgentConnected
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentDisconnected' } });
    }, //onDesktopAgentDisconnected
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentDeprovisioned' } });
    }, //onDesktopAgentDeprovisioned
    () => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentProvisioned' } });
    },
  );

  const onTokenExpired = () => {
    self.postMessage({ id: -1, result: { callback: 'onTokenExpired' } });
  };

  if (method === 'constructor') {
    syncStage = new SyncStage(userDelegate, connectivityDelegate, discoveryDelegate, desktopAgentDelegate, onTokenExpired);
    syncStage.updateOnDesktopAgentReconnected(() => {
      self.postMessage({ id: -1, result: { callback: 'onDesktopAgentReconnected' } });
    });
    self.postMessage({ id, result: 'SyncStage initialized in worker.' });
  } else if (syncStage && typeof syncStage[method] === 'function') {
    Promise.resolve(syncStage[method](...args))
      .then((result) => {
        self.postMessage({ id, result });
      })
      .catch((error) => {
        self.postMessage({ id, error: error.message });
      });
  }
};
```

## SyncStageWorkerWrapper

In our implementation, we use the SyncStageWorkerWrapper class to manage the Web Worker. This class creates a new worker that runs the SyncStage class. It also provides methods to communicate with the worker and handle responses from it. The interface is compliant with the SyncStage class itself. It should be added as `SyncStageWorkerWrapper.js` to the application code:

```javascript
class SyncStageWorkerWrapper {
  constructor(userDelegate, connectivityDelegate, discoveryDelegate, desktopAgentDelegate, onTokenExpired) {
    console.log('SyncStageWorkerWrapper constructor');

    this.userDelegate = userDelegate;
    this.connectivityDelegate = connectivityDelegate;
    this.discoveryDelegate = discoveryDelegate;
    this.desktopAgentDelegate = desktopAgentDelegate;
    this.onTokenExpired = onTokenExpired;
    // eslint-disable-next-line @typescript-eslint/no-empty-function
    this.onDesktopAgentReconnected = () => {};

    this.worker = new Worker(new URL('worker.js', import.meta.url)); //NEW SYNTAX

    this.worker.onmessage = async (event) => {
      const { id, result, error } = event.data;

      if (this.promises[id]) {
        if (error) {
          this.promises[id].reject(new Error(error));
        } else {
          this.promises[id].resolve(result);
        }

        delete this.promises[id];
      } else {
        switch (result.callback) {
          case 'onUserJoined':
            this.userDelegate?.userJoined(result.data);
            break;
          case 'onUserLeft':
            this.userDelegate?.userLeft(result.data);
            break;
          case 'onUserMuted':
            this.userDelegate?.userMuted(result.data);
            break;
          case 'onUserUnmuted':
            this.userDelegate?.userUnmuted(result.data);
            break;
          case 'onRecordingStarted':
            this.userDelegate?.sessionRecordingStarted();
            break;
          case 'onRecordingStopped':
            this.userDelegate?.sessionRecordingStopped();
            break;
          case 'onSessionOut':
            this.userDelegate?.sessionOut();
            break;
          case 'onTransmitterConnectivityChanged':
            this.connectivityDelegate?.transmitterConnectivityChanged(result.data);
            break;
          case 'onReceiverConnectivityChanged':
            this.connectivityDelegate?.receiverConnectivityChanged(result.data.identifier, result.data.connected);
            break;
          case 'onDiscoveryResults':
            this.discoveryDelegate?.discoveryResults(result.data);
            break;
          case 'onDiscoveryLatencyTestResults':
            this.discoveryDelegate?.discoveryLatencyTestResults(result.data);
            break;
          case 'onServerSelected':
            this.discoveryDelegate?.serverSelected(result.data);
            break;
          case 'onDesktopAgentAquired':
            this.desktopAgentDelegate?.onDesktopAgentAquired();
            break;
          case 'onDesktopAgentReleased':
            this.desktopAgentDelegate?.onDesktopAgentReleased();
            break;
          case 'onDesktopAgentConnected':
            this.desktopAgentDelegate?.onDesktopAgentConnected();
            break;
          case 'onDesktopAgentDisconnected':
            this.desktopAgentDelegate?.onDesktopAgentDisconnected();
            break;
          case 'onDesktopAgentDeprovisioned':
            this.desktopAgentDelegate?.onDesktopAgentDeprovisioned();
            break;
          case 'onDesktopAgentProvisioned':
            this.desktopAgentDelegate?.onDesktopAgentProvisioned();
            break;
          case 'onTokenExpired':
            try {
              if (typeof this.onTokenExpired === 'function') {
                const jwt = await this.onTokenExpired();
                this.updateToken(jwt);
              } else {
                console.error('onTokenExpired is not a function');
              }
            } catch (error) {
              console.error('An error occurred in onTokenExpired or updateToken:', error);
            }
            break;
          case 'onDesktopAgentReconnected':
            this.onDesktopAgentReconnected();
            break;
          default:
            console.log(`No implementation for callback ${result.callback}`);
            break;
        }
      }
    };

    this.promises = {};
    this.nextId = 0;

    this.callWorker('constructor');
  }

  callWorker(method, ...args) {
    return new Promise((resolve, reject) => {
      const id = this.nextId++;
      this.promises[id] = { resolve, reject, method };
      this.worker.postMessage({ id, method, args });
    });
  }

  updateOnDesktopAgentReconnected(onDesktopAgentReconnected) {
    this.onDesktopAgentReconnected = onDesktopAgentReconnected;
  }

  isCompatible() {
    let os;

    if (window.navigator.userAgent.indexOf('Mac') !== -1) {
      os = 'macOS';
    } else if (window.navigator.userAgent.indexOf('Win') !== -1) {
      os = 'Windows';
    }

    return this.callWorker('isCompatible', os);
  }

  getLatestCompatibleDesktopAgentVersion() {
    let os;

    if (window.navigator.userAgent.indexOf('Mac') !== -1) {
      os = 'macOS';
    } else if (window.navigator.userAgent.indexOf('Win') !== -1) {
      os = 'Windows';
    }

    return this.callWorker('getLatestCompatibleDesktopAgentVersion', os);
  }

  init(jwt) {
    return this.callWorker('init', jwt);
  }

  async updateToken(token) {
    console.log('SyncStageWorkerWrapper updateToken');
    return this.callWorker('updateToken', token);
  }

  isDesktopAgentConnected() {
    return this.callWorker('isDesktopAgentConnected');
  }

  getSDKVersion() {
    return this.callWorker('getSDKVersion');
  }

  getServerInstances() {
    return this.callWorker('getServerInstances');
  }

  createSession(userId, zoneId, studioServerId) {
    return this.callWorker('createSession', userId, zoneId, studioServerId);
  }

  join(sessionCode, userId, displayName, zoneId, studioServerId) {
    return this.callWorker('join', sessionCode, userId, displayName, zoneId, studioServerId);
  }

  leave() {
    return this.callWorker('leave');
  }

  session() {
    return this.callWorker('session');
  }

  changeReceiverVolume(identifier, volume) {
    return this.callWorker('changeReceiverVolume', identifier, volume);
  }

  getReceiverVolume(identifier) {
    return this.callWorker('getReceiverVolume', identifier);
  }

  toggleMicrophone(mute) {
    return this.callWorker('toggleMicrophone', mute);
  }

  isMicrophoneMuted() {
    return this.callWorker('isMicrophoneMuted');
  }

  getReceiverMeasurements(identifier) {
    return this.callWorker('getReceiverMeasurements', identifier);
  }

  getTransmitterMeasurements() {
    return this.callWorker('getTransmitterMeasurements');
  }

  getDesktopAgentProtocolHandler() {
    return this.callWorker('getDesktopAgentProtocolHandler');
  }

  getSelectedServer() {
    return this.callWorker('getSelectedServer');
  }

  getBestAvailableServer() {
    return this.callWorker('getBestAvailableServer');
  }

  startRecording() {
    return this.callWorker('startRecording');
  }

  stopRecording() {
    return this.callWorker('stopRecording');
  }
  checkProvisionedStatus() {
    return this.callWorker('checkProvisionedStatus');
  }

  getSessionSettings() {
    return this.callWorker('getSessionSettings');
  }

  setInputDevice(identifier) {
    return this.callWorker('setInputDevice', identifier);
  }

  setOutputDevice(identifier) {
    return this.callWorker('setOutputDevice', identifier);
  }

  setNoiseCancellation(enabled) {
    return this.callWorker('setNoiseCancellation', enabled);
  }

  setDisableGain(disabled) {
    return this.callWorker('setDisableGain', disabled);
  }

  setDirectMonitor(enabled) {
    return this.callWorker('setDirectMonitor', enabled);
  }

  setLatencyOptimizationLevel(level) {
    return this.callWorker('setLatencyOptimizationLevel', level);
  }
}

export default SyncStageWorkerWrapper;

```

The SyncStageWorkerWrapper class ensures that the SyncStage class and its WebSocket connection continue to run smoothly, providing a seamless user experience.

## Configuring Web Workers in React.js
To use Web Workers in a React.js project, you need to configure your project in a specific way. 

Here are the steps:

1. Create a Worker File: Create a new JavaScript file (`worker.js`). This file will contain the code that the worker will execute.

2. Instantiate the Worker: In your React component, instantiate the worker using the Worker constructor, passing the path to your worker file as an argument (we do it in `SyncStageWorkerWrapper.js`).

3. Communicate with the Worker: Use the `postMessage` method to send data to the worker. The worker can send data back to the main thread using its own `postMessage` method. To receive messages from the worker, add an event listener for the message event to the worker instance (we do it in (`SyncStageWorkerWrapper.js`).

4. Configure Webpack (if used): If your project uses Webpack, you may need to add a loader to handle worker files. The `worker-loader` package is a popular choice. Install it with npm `npm install --save-dev worker-loader`, and add a rule to your Webpack configuration as `config-overrides.js` file in the root directory:

```javascript
//config-overrides.js

module.exports = function override(config, env) {
  config.output.globalObject = 'this';
  config.module.rules.push({
    test: /\.worker\.js$/,
    use: [{ loader: 'worker-loader' }],
  });
  return config;
};

```
