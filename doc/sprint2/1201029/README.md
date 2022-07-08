RCOMP 2021-2022 Project - Sprint 2 - Member 1201029 folder
===========================================

# Building 3
## IPv4 Networks
### **Backbone**
For this building the backbone IP decided was: 172.16.136.3/25.

This is an important decision to make as a team since every building is connected by the backbone which has its own network address, as such everyone in the team had to be in sync in order for every building's backbone to be part of the same network and for there to be no duplicate IP address as that would make comunications between buildings impossible.

___

### **VLAN Networks**

When it comes to VLAN Networks there was a need to keep in mind the number of nodes that were going to operate in this building and the network that this building would be using, which was decided in a reunion made with the rest of the team.  

The network address that this building will be using is 172.16.141.0/24 which has a Network Address space size of 256, therefore can have 254 node, since this building has a total of 188 nodes it is more than enough valid addresses. In this case we are unable to use the network 172.16.141.0/25 as it would only be able to have 126 nodes or valid addresses and that wouldn't be enough.

With the network address decided we have to take a look at the necessary VLANs and the number of nodes they have:

| **VLAN** | **Number of Nodes** |
|---|---|
| Floor 0 | 35
| Floor 1 | 45
| Wi-fi | 55
| VoIP | 25
| DMZ | 28

Having the number of nodes in mind, it is only necessary do some subnetting in order to cover all the nodes while still mantaining the unused addresses to a minimum, after doing that we end up with this address distribution:

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|211|B3-floor0|172.16.141.0/26|
|212|B3-floor1|172.16.141.64/26|
|213|B3-Wifi|172.16.141.128/26|
|214|B3-VoIP|172.16.141.192/27|
|215|B3-DMZ|172.16.141.224/27|

___
## Equipement Configuration

### **Switches**

The switches were configured to have a trunk connection between themselves, this allows us to configure at least one Switch to Server Mode which allows us to configure the VLAN Database only in that switch and it will spread that database to every switch that is connect. All other switches are configured to Client mode.

Having that in mind the switch chosen for this task was the switch that represents the IC (Intermideate Connect) since it is connected to every other switch and ends up being the center point of this building.

The connection from the switch to the building's router is also in trunk mode in order for the router to be able to receive Frames that belong to different VLANS and then route them through the right VLAN to the right end-node.
___

### **Router**

The router is configured to accept multiple vlans, this is made taking advantage of sub-interfaces which are all configured to a different VLAN. This works in a similar manner to having a Switch's port set to trunk mode. 

This configuration was made in the port that is connected to the IC switch.

With all that in mind the final configuration for this port looks something like this: 

| Port | Link | IP Address |
| --- | --- | --- |
| GigabitEthernet0/2/0.1 | Up | 172.16.141.1/26 |
| GigabitEthernet0/2/0.2 | Up | 172.16.141.65/26 |
| GigabitEthernet0/2/0.3 | Up | 172.16.141.129/26 |
| GigabitEthernet0/2/0.4 | Up | 172.16.141.193/27 |
| GigabitEthernet0/2/0.5 | Up | 172.16.141.255/26 |

Now that the internal network is configured we need to make the Router able to route Packets  to outside the internal network of the building, in other words, we need to make it so that the router can rout Packets to the other buildings in order for this building's end-devices to be able to communicate with other buildings' end-devices.

In order to do that we need to set up a Routing Table telling the Router where to send Packets that belong to a certain network. The router will be able to send the Packets to the Routers that are directly connected to it via the backbone network.

The Routing Table ended up looking like this:

| Network Address | Send Via |
| --- | --- | 
| 172.16.140.0/23 | 172.16.136.2 |
| 172.16.142.0/23 | 172.16.136.4 |
| 0.0.0.0/0 | 172.16.136.1 |


The default network is set to the Building 1 address since building 1 is the building that makes the connection to the internet.
___

### **End devices**

Only one device per VLAN is needed to demonstrate if it is being effectively used however sometimes there might be another device connected to the same VLAN just for testing porpuses. 

Every end-device's IP address is set up with the second value of its corresponding VLAN. 