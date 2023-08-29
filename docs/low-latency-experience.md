

## Music Collaboration with SyncStage Guide

We have prepared a guide explaining everything you need to now to have a low latency music collaboration with SyncStage.

[Download Music Collaboration with SyncStage Guide](https://public.sync-stage.com/docs/Music+Collaboration+with+SyncStage+-+Manual.pdf){ .md-button target=_blank}


## Distance impact

Each session can be created in one of multiple zones around the world. Make sure that the application users that are going to join the session are within geographical proximity to the zone location. Best experience is within 250 miles / 400 kilometers radius from the zone. You can freely choose the zone of the deployment during the ‘Create Session’ step.

Data transmission speed has its upper bounds. That’s physics, you cannot overtake photons that run at the speed of light. That speed is extremely high but not infinite, distance will add additional milliseconds to the latency.

If your users are connecting from distant places, they will probably not be able to sing or jam together. SDK provides information about the network quality and latencies so that your application can inform users that the current session might be not applicable for highly synchronous use cases. However, they will have much more synchronous experience compared to any other communication tools available on the market.

## Jitter impact

Application users connected to low quality networks with high traffic, or with a bad range of a mobile or WiFi signal may have problems with bandwidth consistency. In these scenarios, those application users' latency will fluctuate. High jitter can badly impact the overall audio latency. To help notify your application users of their network quality at their current location - you can get a network quality indicator to present in your application.

## Headphones

The most recommended way of communicating with the SyncStage audio pipeline is by using wired headphones. They provide the lowest latency and reduce the effort our SyncStage audio pipeline needs to do with removing noises, so we can save additional milliseconds for even better synchronization. Bluetooth technology is not well suited for real time communication eg. Bluetooth wireless technology can introduce itself at least 100 ms of latency.

## Audio interfaces

Your users can use their favorite instruments to play during the session. They can use audio interfaces to stream guitar, piano, bass, drums, and external microphones to jam together. If they do not own one a smartphone's internal microphone will be more than good to play together with satisfying audio quality.

The list of supported audio interfaces will be announced soon.

