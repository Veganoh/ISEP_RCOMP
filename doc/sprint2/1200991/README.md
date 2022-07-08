RCOMP 2021-2022 Project - Sprint 2 - Member 1200991 folder
===========================================

# Building 1

## IPv4 networks

### Backbone

For the encompassing of several networks distributed through the different buildings present in the campus there was a need to decide between every member which network is available to who.
As such this building, which encompasses the location of the Main Cross-Connect was set to have the backbone ip of 172.16.136.1.

### Vlan networks

To properly use the entirety of the block of address' that were assigned to this building there was a need to divide it into all the necessary vlans

Considering the following conditions:
- End user outlets on the ground floor: 60 nodes
- End user outlets on floor one: 80 nodes
- Wi-Fi network: 120 nodes
- DMZ (Servers, administration workstations, and network infrastructure devices): 100 nodes
- VoIP (IP-phones): 40 nodes

The networks end up looking like this:

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|201|B1-floor1|172.16.138.0/25|
|202|B1-floor0|172.16.138.128/26|
|203|B1-VoIP|172.16.138.192/26|
|204|B1-Wifi|172.16.139.0/25|
|205|B1-DMZ|172.16.139.128/25|

### ISP network

The ISP network is already provided "15.203.47.61/30". 
Being a network with a mask of 30 it means that the other end to the ISP, the one that ends up connecting with the main Router of building 1 and as such the rest of the building is "15.203.47.62/30".

## Equipment configuration

### Switches

The switches were configured to have a trunk connection between themselves, this way we can appoint the main switch, the Intermediate Cross-Connect, to work as servers and the other to work as clients, this way the whole vlan database of the building can be directly managed by one switch which will setup the VTP domain and setup all the vlans that every switch needs.
The connection between the IC and the Main router is made in trunk mode using vlans, as the router may need access between multiple vlans.
On the other hand, the MC that is connecting every router from every building is using access mode connections as those connections will only be used in one VLAN.

### Router

Router are configured to accept multiple vlans when need, this means that the connection between a router and multiple networks is using vlans as it allows it to connect to multiple networks with only one cable and that when only one network is present access mode connections are made which only allow one specific vlan.
Furthermore, since every other network is not directly connected to the same routers a Routing table is required.
Building 1's main router is routed to send a signal with other building's network through its direct connection with other routers, furthermore it is configured to send unknown signals to the ISP as the default route, and it is the default route of every other router in the building.
Finally, the ISP router is configurated to send back any signals that are part of the address block that makes up all the campus.
It is important to note that every router in this building used the first ip address of every network meaning that those ip's cannot be used by any other devices

### End devices

Only one device per Vlan is needed to demonstrate if it is being effectively used, more specifically every end device is set up with the second value of its corresponding VLAN.



