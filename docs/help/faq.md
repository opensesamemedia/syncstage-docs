## Network

### Can users use SyncStage when not connected to the 5G network?
Yes, 5G is not required. Users can use any type of internet connection.

### NAT issues
SyncStage is UDP-based by default. However, in some networks where UDP connections are not allowed due to firewall or NAT configuration, SyncStage will switch to TCP. This may result in increased audio latency.

## Sessions

### What is the accepted format for session codes?
Session codes consist of 9 letters or digits and are case insensitive. For readability, they are presented in the format `xyz-xyz-xyz`, but hyphens can be omitted. Therefore, `xyzxyzxyz` is a valid representation of `xyz-xyz-xyz`.

### How long can a session last?
There are no defined limits regarding on the session length. Nevertheless, a connection of a given user should not last for more than 24h continuously. 
There are no defined limits for session length. However, a connection from a user should not last continuously for more than 24 hours.

### How many users can a session accommodate?
Currently, SyncStage can accommodate up to 8 users in a a session.

## Costs
### How does SyncStage calculate SDK usage?
SyncStage calcutales the number of minutes each user was connected to a session. Developers can track the usage in the Developer Console. 

### How do I pay for SyncStage?
During the Early Access Phase, developers will receive monthly invoices. The total amount on the invoice will depend on the usage and the selected plan.
