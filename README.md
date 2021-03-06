
# Pusher.cfc - Pusher.com REST API Library For ColdFusion

by Ben Nadel 
([www.bennadel.com][3])

A ColdFusion wrapper for the [Pusher.com][5] REST API. This ColdFusion 
component has been tested with [version 1.12 of the Pusher.com client][2]. 
The actual Pusher.cfc exposes two different methods for publication:

* pushToAllSubscribers( channel, eventType, message )
* pushToAllSubscribersExcept( channel, eventType, message, socketID )

The latter method prevents the echoing of a message back to the originating
client. Meaning, if a client posts a message to the server (and communicates
its socketID), the server can then "push" a message to all subscribers, less
the client that posted the message in the first place.

The Pusher.cfc also exposes two additional methods for authenticating users
trying to connect to a Private channel or a Presence channel:

* getPresenceChannelAuthentication( socketID, channel, data );
* getPrivateChannelAuthentication( socketID, channel );

Private channels use a [multi-step authentication process][4] that requires you
to expose a (local) end-point on your server. This end-point provides your 
application with the opportunity to approve or reject the subscription to a 
given channel by a given user.

## ColdFusion 10 - No Dependencies

ColdFusion 10 introduced the new hmac() function for natively creating Hashed 
Message Authentication Codes (Hmac). I have created a ColdFusion 10 branch in
the repo in which the Crypto.cfc is replaced with the hmac() function.

Branch: [ColdFusion 10][6]

## ColdFusion 8 Compatible

I have created a __very quick__ translation of the ColdFusion 9.0.1 version
(this one) over to a ColdFusion 8 version for users on older systems. I made
sure that the Example worked; but, I did not other further testing.

Branch: [ColdFusion 8][7]

## Flash Fallback

In the event that the user's browser doesn't support WebSockets, the Pusher 
client will fallback to using Flash WebSockets. In previous versions of the 
Pusher client, you had to host the "swf" fallback file yourself; this is no
longer the case. Now, the Pusher client will load the fallback "swf" as 
needed from its own servers.

## Vendor Libraries

* [Crypto.cfc by Ben Nadel][1]


[1]: https://github.com/bennadel/Crypto.cfc
[2]: http://js.pusher.com/1.12/pusher.min.js
[3]: http://www.bennadel.com
[4]: http://pusher.com/docs/authenticating_users
[5]: http://pusher.com
[6]: https://github.com/bennadel/Pusher.cfc/tree/coldfusion10
[7]: https://github.com/bennadel/Pusher.cfc/tree/coldfusion8