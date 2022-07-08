RCOMP 2021-2022 Project - Sprint 2 - Member 1201045 folder
===========================================

# Building 2

## IPv4 Networks

### Backbone

This simulation, includes the campus backbone for the encompassing of several networks distributed through the different buildings present in the campus there was a need to decide between every member which network is available to who.
As such this building was set to have the backbone IP of 172.16.136.2/25.

### VLAN Networks

To properly use the entirety of the block of address' that were assigned to this building there was a need to divide it into all the necessary VLAN's

Considering the following conditions:
- End user outlets on the ground floor: 25 nodes
- End user outlets on floor one: 50 nodes
- Wi-Fi network: 120 nodes
- DMZ (Servers, administration workstations, and network infrastructure devices): 12 nodes
- VoIP (IP-phones): 12 nodes

The networks end up looking like this:

| **VLANID** | **VLANNAME**  |  **IPv4 Network**  |
|    -----   |     ----      |        ----        |
|     206    |    B2-wifi    |  172.16.140.0/25   |
|     207    |   B2-floor1   |  172.16.140.128/26 |
|     208    |   B2-floor0   |  172.16.140.192/27 |
|     209    |    B2-DMZ     |  172.16.140.224/28 |
|     210    |    B2-VoIP    |  172.16.140.240/28 |

## Equipment Configuration

### Switches

The switches were configured to have a trunk connection between themselves, this way we can appoint the main switch, the Intermediate Cross-Connect, to work as servers and the other to work as clients, this way the whole VLAN database of the building can be directly managed by one switch which will setup the VTP domain and setup all the vlans that every switch needs.
The connection between the IC and the Main router is made in trunk mode using vlans, as the router may need access between multiple vlans.

### Router

Router are configured to accept multiple vlans when need, this means that the connection between a router and multiple networks is using vlans as it allows it to connect to multiple networks with only one cable and that when only one network is present access mode connections are made which only allow one specific vlan.
Furthermore, since every other network is not directly connected to the same routers a Routing table is required.
Building 2's main router is routed to send a signal with other building's network through its direct connection with other routers, furthermore it is configured to send unknown signals to building 1 so it can be sent to ISP.

### End devices

Only one device per Vlan is needed to demonstrate if it is being effectively used, more specifically every end device is set up with the second value of its corresponding VLAN however sometimes there might be
another of the same type of device just for testing purposes.