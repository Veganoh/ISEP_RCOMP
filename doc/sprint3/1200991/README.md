RCOMP 2021-2022 Project - Sprint 3 - Member 1200991 folder
===========================================

In this sprint many changes were performed in the layer 3 simulation as such all those changes will be talked about in this file:

# OSPF dynamic routing

At the very beginning static routing was retired and changed to dynamic routing.
To achieve this feat the networks of each building were changed to represent areas that would represent each campus private area as well with a bonus area for the backbone.

Building 1's area was area 1 and the backbone area was 0, making sure that every other area relates to area 0 makes it possible for every building to be connected dynamically.
But since the internet does not represent a area it was a necessity that at least one static default route would be kept in the main router.

# HTTP servers

A new Server was Added to the DMZ network, this server serves as the main server that everyone can access.
Furthermore, the server that was added in the last sprint will now be used to house the DNS.

net we have the servers Ip addresses

| **Server** | **IP** |
| ---- | ---- |
|   DNS   | 172.16.139.130 |
|   HTTP   | 172.16.139.131 |

# DHCPv4 service

This step can be summed as the application of a service that will forward to every device a automatically Ip address that is to be used in said network except for the DMZ network.
The VoIP network is a special case as it needs to use *option 150* that enables communication between ephones.

# VoIP service

Adding a VoIP service required the use of a voice vlan in every switch that was connected with an IP phone as well as the aforementioned DHCPv4 service to work.
A standard phone numbers were decided for every building making so that the call forwarding between building would be accessible.
In building1's case the numbers should start with 1 and rout to every other building which number start with 2,3 and 4.

# DNS

The DNS required the information of all the other building as it is the main DNS of the entire campus.
As such it will encompass the information of its own server as well as it's HTTP server and the DNS servers of every other building to connect every single domain in the campus.
Furthermore, The DNS server has the responsibility to register it's domains under the "www","web" and "dns" names. 

The connections made can be viewed in the following image:

![DNS Setup](DNS-Setup.png)

# NAT 

Static Nat is used here to redirect traffic directly to the servers.
Using the type of request and the port of said request the router is now able to redirect the packet to the specified server (TCP/80, TCP/443 to the server and TCP/53, UDP/53 to the DNS server)
Important note: NAT Could not be made to work in this sprint

# ACL

## Backbone network

    1-deny ip 172.16.138.0 0.0.1.255 any
    2-permit icmp any any
    3-permit tcp any 172.16.139.128 0.0.0.127 eq 80
    4-permit tcp any 172.16.139.128 0.0.0.127 eq 443
    5-permit tcp any 172.16.139.128 0.0.0.127 eq 53
    6-permit udp any 172.16.139.128 0.0.0.127 eq 53 
    7-deny ip any 172.16.139.128 0.0.0.127
    8-permit ospf any host 172.16.136.1 
    9-permit tcp any host 172.16.136.1 eq 80
    10-permit tcp any host 172.16.136.1 eq 443
    11-permit tcp any host 172.16.136.1 eq 53
    12-permit udp any host 172.16.136.1 eq 53
    13-permit tcp any host 172.16.136.1 eq 1028
    14-permit tcp any host 172.16.136.1 eq 1720
    15-permit tcp any eq 1720 host 172.16.136.1
    16-deny ip any host 172.16.136.1
    17-permit ip any any

(1) - deny external spoofing
(2) - allows any echo request and reply
(3 - 6) - allows http, https, and dns requests to the DMZ network
(7) - Denies all other requests
(8) - allows the ospf service to work
(9 - 12) - allows the router to receive http, https, and dns requests
(13 - 15) - allows call forwarding between Ip phones
(16) - Denies any other type of request to the given router
(17) - allows every other type of access to the network

## Private network

For Wi-Fi, floor 1 and floor 0 the acl used are:

    1-permit icmp 172.16.138.0 0.0.0.127 any
    2-permit ip 172.16.139.128 0.0.0.127 any
    3-permit ip host 0.0.0.0 host 255.255.255.255
    4-deny ip any host 172.16.138.1 
    5-permit ip 172.16.138.0 0.0.0.127 any

(1) - permits echo request and echo replies sent through the network
(2) - allows access to the DMZ network
(3) - Makes sure that the DHCP service works
(4 - 5) - Denies any further use of the router and stops spoofing

The DMZ uses the same ACLS except for those meant to reduce spoofing as this is a trusted network

The VoIP network used extra acls to accommodate the heightened need of the IP phones:
    permit icmp 172.16.138.192 0.0.0.63 any
    permit ip host 0.0.0.0 host 255.255.255.255
    6-permit tcp any host 172.16.138.193 eq 2000
    7-permit tcp any host 172.16.138.193 eq 1028
    8-permit tcp any host 172.16.138.193 eq 1720
    9-permit tcp any eq 1720 host 172.16.138.193 
    deny ip any host 172.16.138.193 
    permit ip 172.16.138.192 0.0.0.63 any

(6 - 9) - Allows the use of VoIP function to operate ephones

