

## Music Collaboration with SyncStage Guide

We have prepared a guide explaining everything you need to now to have a low latency music collaboration with SyncStage.

[Download Music Collaboration with SyncStage Guide](https://public.sync-stage.com/docs/Music+Collaboration+with+SyncStage+-+Manual.pdf){ .md-button target=_blank}


## Distance impact

Each session can be created in one of multiple zones around the world. Make sure that the application users that are going to join the session are within geographical proximity to the zone location. Best experience is within 250 miles / 400 kilometers radius from the zone. You can freely choose the zone of the deployment during the ‘Create Session’ step.

Data transmission speed has its upper bounds. That’s physics, you cannot overtake photons that run at the speed of light. That speed is extremely high but not infinite, distance will add additional milliseconds to the latency.

If your users are connecting from distant places, they will probably not be able to sing or jam together. SDK provides information about the network quality and latencies so that your application can inform users that the current session might be not applicable for highly synchronous use cases. However, they will have much more synchronous experience compared to any other communication tools available on the market.

## Jitter impact

Application users connected to low quality networks with high traffic, or with a bad range of a mobile or WiFi signal may have problems with bandwidth consistency. In these scenarios, those application users' latency will fluctuate. High jitter can badly impact the overall audio latency. To help notify your application users of their network quality at their current location - you can get a network quality indicator to present in your application.

## Latency Optimization Level
Each use case has its own latency and quality requirements. For voice communications, voice clarity is the key, whereas sub-100ms latency isn't required. For real-time music collaboration, there is nothing more important than low and stable latency. To address the needs of multiple use cases SyncStage offers `Latency Optimization Level` parameter that allows for setting up trade-off between latency level and network fluctuations resiliency. The table below shows available modes.


| Level name                           | Description                     
| ------------------------------------ | :--------------------------------------------------------------------------------------------------------- |
| High Quality                         |  SyncStage tries to maintain the highest possible quality regardless of the network fluctuations.          |
| Optimized                            |  Similar to High Quality but a bit more focused on reducing latency.                                       |
| Best Performance                     |  SyncStage is focused on delivering low latency. In poor network conditions, cracks in audio can occur.    |
| Ultra Fast                           |  SyncStage is focused on delivering possibly low and stable latency. Good network conditions needed.      |


Currently, Latency Optimization Level parameter **is only available on iOS.** We are working to bring it to Android and Web SDK for MacOS. 


## Headphones

The most recommended way of communicating with the SyncStage audio pipeline is by using wired headphones. They provide the lowest latency and reduce the effort our SyncStage audio pipeline needs to do with removing noises, so we can save additional milliseconds for even better synchronization. Bluetooth technology is not well suited for real time communication eg. Bluetooth wireless technology can introduce itself at least 100 ms of latency.

## Audio interfaces

Your users can use their favorite instruments to play during the session. They can use audio interfaces to stream guitar, piano, bass, drums, and external microphones to jam together. If they do not own one a smartphone's internal microphone will be more than good to play together with satisfying audio quality.

### Supported devices
The rule of thumb is that as long as the OS supports a given audio interface by default, SyncStage supports it as well.

Below there is a list of audio interfaces we have tested on:

* iRig HD 2
* Focusrite Scarlett
* Behringer U-PHORIA UMC22
* Behringer U-PHORIA UMC2

## Collected data by the SDK
In order to provide best experience with SyncStage, SDK gathers information about location of users and meta data of their network operators.
