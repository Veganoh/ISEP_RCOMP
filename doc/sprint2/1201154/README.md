RCOMP 2021-2022 Project - Sprint 2 - Member 1201154 folder
===========================================

# Building 4

## IPv4 Networks

### Backbone

The simulation contains the campus backbone for the encompassing of several networks for all the different buildings.
This leads up to selecting a backbone IP to each building. In this case, building 4 has 172.16.136.4/25.

### VLAN Networks

In order to use the entirety of the give address assigned to this building we will need to divide it
in the necessary VLAN's.

As such, we should consider the following:
- End user outlets on the ground floor: 28 nodes
- End user outlets on floor one: 55 nodes
- Wi-Fi network: 70 nodes
- DMZ (Servers, administration workstations, and network infrastructure devices): 10 nodes
- VoIP (IP-phones): 12 nodes

Then, the networks will look like this:

| **VLANID** | **VLANNAME** | **IPv4 Network**  |
|------------|--------------|-------------------|
| 216        | B4-Wifi      | 172.16.142.0/25   |
| 217        | B4-floor1    | 172.16.142.128/26 |
| 218        | B4-floor0    | 172.16.142.192/27 |
| 219        | B4-VoIP      | 172.16.142.224/28 |
| 220        | B4-DMZ       | 172.16.142.240/28 |

## Equipment Configuration

### Switches

All switches are in trunk mode when communicating with each others. This is done so that we can pin point a main switch, in this case the Intermediate Cross-Connect (IC).
Doing so allows for the whole VLAN database to be managed by one switch, this allows for a setup of the VTP domain and of all the VLAN's that every switch needs.

The connection between the IC and the Main Router is made in trunk mode while using VLAN's.

### Router

Routers are configurated in such a way that allows for multiple VLAN use, which in turn, allows the router to connect to a various amount of defined networks.

A routing table is also needed, since all the other networks aren't tied to the same router. The routing table allows this building's router to communicate
with all the other buildings. It's also worth mentioning that, in case an unknown signal is sent, that signal will end up on Building 1, in order to send it to the ISP.

### End devices

To demonstrate that the network is working, an end device is connected to each VLAN. In this way, you can test the network by trying to communicate with each device on different VLAN's 
