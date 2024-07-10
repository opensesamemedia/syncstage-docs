# Impact of The Distance Between The Musicians on Network Latency
As the distance between users increases, so does the network latency, potentially impacting certain types of music collaboration. SyncStage uses a client-server architecture, routing all connections through its servers known as Studio Servers. Therefore, the geographical distance between users and the Studio Server must be considered.


<figure markdown="span">
    ![Latency vs. Distance](../../assets/guides/latency-vs-distance.png){ width="600" loading=lazy}
    <figcaption>Network latency increases with the distance</figcaption>
</figure>

| Distance in Kilometers | Distance in Miles | Network Latency Floor |
| :---------------------: | :----------------: | :--------------: |
| 200 km | ~124 mi | > 2 ms |
| 500 km | ~311 mi | > 5 ms |
| 1000 km | ~621 mi | > 10 ms |
| 2000 km | ~1243 mi | > 20 ms |
| 5000 km | ~3107 mi | > 50 ms |
| 10000 km | ~6214 mi | > 100 ms |


!!! note

    Network latency floor only considers the propagation delay due to the speed of light in the fiber and does not account for other factors that can contribute to latency. In reality, this value can be 2-5 times higher.
