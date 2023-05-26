## Network

### Can users use SyncStage when not connected to the 5G network?
Yes, 5G is not a must. Your users can connect using their WiFi network or LTE connection.

### NAT issues
SyncStage is by default UDP-based. However, configuration of some networks (firewall, NAT configuration) does not allow for UDP connection. In cases like this SyncStage works over TCP what can negatively impact the audio latency.


## Sessions

### What is the accepted session code format?
Session codes consists of 9 letters or digits and are case insensitive. For readabilty, they are presented in the following format `xyz-xyz-xyz`, however, hyphens can be ommited. Therefore, `xyzxyzxyz` is a valid representation of `xyz-xyz-xyz`.

### For how long a given session code is valid?
Sessions expire 6 months after the last use of a given session.
 
### How long does the session can last?
There are no defined limits regarding on the session lenght. Nevertheless, a connection of a given user should not last for more than 24h continuously. 

### How many users a session can accomodate?
Currently, the max number of users in a session depends on the platform and device.
On iOS and macOS it can be up to 30 users. On Android, depentding on the device, up to 8.


## Costs
### How does SyncStage calculate the SDK usage?
SyncStage calcutales the number of minutes each user was connected to a session. Developers can track the usage in the Developer Console. 

### How do I pay for SyncStage?
In the Early Access Phase, the Developer will be receiving invoices monthly. The sum on the invoice will depend on the usage and the selected plan.
