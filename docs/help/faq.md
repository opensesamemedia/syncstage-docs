## Network

### Can users use SyncStage when not connected to the 5G network?
Yes, 5G is not required. Users can use any type of internet connection.

### NAT issues
SyncStage is UDP-based by default. However, in some networks where UDP connections are not allowed due to firewall or NAT configuration, SyncStage will switch to TCP. This may result in increased audio latency.

## Sessions

### What is the accepted format for session codes?
Session codes consist of 9 letters or digits and are case insensitive. For readability, they are presented in the format `xyz-xyz-xyz`, but hyphens can be omitted. Therefore, `xyzxyzxyz` is a valid representation of `xyz-xyz-xyz`.

### How long is a session code valid for?
Sessions expire 6 months after the last use of a given session.
 
### What will happen when the session code expire?
The `Join()` method will raise an error.

### How long can a session last?
There are no defined limits regarding on the session lenght. Nevertheless, a connection of a given user should not last for more than 24h continuously. 
There are no defined limits for session length. However, a connection from a user should not last continuously for more than 24 hours.

### How many users can a session accommodate?
The maximum number of users in a session depends on the platform and device. On iOS and macOS, it can accommodate up to 30 users. On Android, depending on the device, it can accommodate up to 8 users.

## Costs
### How does SyncStage calculate SDK usage?
SyncStage calcutales the number of minutes each user was connected to a session. Developers can track the usage in the Developer Console. 

### How do I pay for SyncStage?
During the Early Access Phase, developers will receive monthly invoices. The total amount on the invoice will depend on the usage and the selected plan.
