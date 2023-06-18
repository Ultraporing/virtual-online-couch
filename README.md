# virtual-online-couch
Allowes for multiple players to play hot seat / couch coop over the internet. The host is streaming audio and video of the chosen application to the clients, and they are able to use their mouse, keyboard or controller in the hosts application by sending the inputs back.

# Quick note for architecture:
Whole connection and messages should optionally use encryption/validation/relay-server as chosen by the host. You would disable this within trusted networks to gain speed. More info in relay server.

## Host 
runs and selects the app to be streamed/interacted with  

<-------RECIEVE-----------------  
Receives Input (mouse, keyboard, controller) from selected source/s in control, (optionally) via relay server. forwarded exclusively to selected app (host can switch control between host/client/multiple)  

---------SEND------------------->  
sends A/V to relay server if used. otherwise directly to clients

## (Optional) Relay web server

uses possibly a static ip/url as public connection point for clients to prevent direct connections to Host, and works as relay for network messages between host and clients.
If not used, clients just directly connect to host via his ip.  

NOTES: 
- should maybe use encryption/some keys to validate messages are sent via the relay instead of direct connection to prevent malicious messages between clients and host.
- host and client have to do the validation of the relay messages too to prevent malicious constructed messages  

<-------RECIEVE-----------------  
receives input commands from clients if relay server is used and relays them to the host.  

---------SEND------------------->  
relays host A/V to clients if relay server is used.

## Single/Multiple Clients  

<-------RECIEVE-----------------  
receives host A/V from relay server if used. otherwise from host.  

---------SEND------------------->  
sends input (mouse, keyboard, controller) to relay server if used. otherwise directly to host.
