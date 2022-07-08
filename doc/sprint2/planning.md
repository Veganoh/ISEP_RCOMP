RCOMP 2021-2022 Project - Sprint 2 planning
===========================================
### Sprint master: 1200991 ###
(This file is to be created/edited by the sprint master only)
# 1. Sprint's backlog #
| **Task** | **Task description** |
| ---- | ---- |
| T.2.1 | Development of a layer two and layer three Packet Tracer simulation for building one, encompassing the campus backbone. Integration of every member’s Packet Tracer simulation into a single simulation. |
| T.2.2 | Development of a layer two and layer three Packet Tracer simulation for building two, encompassing the campusbackbone. |
| T.2.3 | Development of a layer two and layer three Packet Tracer simulation for building three, encompassing the campus backbone. | 
| T.2.4 | Development of a layer two and layer three Packet Tracer simulation for building four, encompassing the campus backbone. |

# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned. 		Most importantly, all technical decisions impacting on the subtasks implementation must be settled on this 		meeting and specified here.

## VLAN configuration

### Backbone

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|200|backbone|172.16.136.0/25|
  
### Building 1

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|201|B1-floor1|172.16.138.0/25|
|202|B1-floor0|172.16.138.128/26|
|203|B1-VoIP|172.16.138.192/26|
|204|B1-Wifi|172.16.139.0/25|
|205|B1-DMZ|172.16.139.128/25|

### Building 2

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|206|B2-wifi|172.16.140.0/25|
|207|B2-floor1|172.16.140.128/26|
|208|B2-floor0|172.16.140.192/27|
|209|B2-DMZ|172.16.140.224/28|
|210|B2-VoIP|172.16.140.240/28|

### Building 3

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|211|B3-floor0|172.16.141.0/26|
|212|B3-floor1|172.16.141.64/26|
|213|B3-Wifi|172.16.141.128/26|
|214|B3-VoIP|172.16.141.192/27|
|215|B3-DMZ|172.16.141.224/27|

### Building 4

| **VLANID** | **VLANNAME** | **IPv4 Network** |
| ---- | ---- | ---- |
|216|B4-Wifi|172.16.142.0/25|
|217|B4-floor1|172.16.142.128/26|
|218|B4-floor0|172.16.142.192/27|
|219|B4-VoIP|172.16.142.224/28|
|220|B4-DMZ|172.16.142.240/28|


### Backbone configuration
This section explains the node address each mermber will use in ther backbone 

- Building 1 : 172.16.136.1/25
- Building 2 : 172.16.136.2/25
- Building 3 : 172.16.136.3/25
- Building 4 : 172.16.136.4/25

## ISP connection network

- 15.203.47.61/30

## Naming conventions

Every pice of the network system will have a naming convention following the following rules:
- Common equipment found in every building will be named with the format BuildingNumber-AbreviatedEquipmentType-number ex: B1-SW-5, B3-RT-1, B3-PC-2;
- Important equipment to the backbone infrastucture(MC) aswell as ISP connection equipment weill have specific names according to their funciton;

## VTP Domain
 The vtp domain name used was "rc22dcg3" for every vtp domain in the planning


# 3. Subtasks assignment #
(For each team member (sprint master included), the description of the assigned subtask in sprint 2)

#### Example: ####
  * 1200991 - (T.2.1) Development of a layer two and layer three Packet Tracer simulation for building one, encompassing the campus backbone. Integration of every member’s Packet Tracer simulation into a single simulation.
  * 1201029 - (T.2.3) Development of a layer two and layer three Packet Tracer simulation for building two, encompassing the campusbackbone.
  * 1201045 - (T.2.2) Development of a layer two and layer three Packet Tracer simulation for building three, encompassing the campusbackbone.
  * 1201154 - (T.2.4) Development of a layer two and layer three Packet Tracer simulation for building four, encompassing the campusbackbone.

