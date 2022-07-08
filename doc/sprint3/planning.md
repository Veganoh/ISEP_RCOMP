RCOMP 2021-2022 Project - Sprint 3 planning
===========================================
### Sprint master: 1201045 ###
(This file is to be created/edited by the sprint master only)

# 1. Sprint's backlog #
| **Task** | **Task description** |
| ---- | ---- |
| T.3.1 | Update the **building1.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 1.|
| T.3.2 | Update the **building2.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 2.Final integration of each member’s Packet Tracer simulation into a single simulation (**campus.pkt**).|
| T.3.3 | Update the **building3.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 3.|
| T.3.4 | Update the **building4.pkt** layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building 4.|

# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned. 		Most importantly, all technical decisions impacting on the subtasks implementation must be settled on this 		meeting and specified here.

## OSPF Dynamic Routing

### Areas

|  **AREA**    |  **BUILDING**  |
|     ----     |      ----      |
|      0       |    Backbone    |
|      1       |   Building 1   |
|      2       |   Building 2   |
|      3       |   Building 3   |
|      4       |   Building 4   |

## VoIP Service

### Phone numbers schema

|  **BUILDING**  |     **E NUMBER**     |
|     ----       |        ----          |
|       1        |    1001,1002...1999  |
|       2        |    2001,2002...2999  |
|       3        |    3001,3002...3999  |
|       4        |    4001,4002...4999  |

## DNS

### Domain name and IPv4 node address

|  **BUILDING**  | **IPv4 NODE ADDRESS**|        **DOMAIN NAME**          |
|     ----       |        ----          |             ----                |
|       1        |    172.16.139.130    |       ns.rcomp-21-22-dc-g3      |
|       2        |    172.16.140.226    | ns.building-2.rcomp-21-22-dc-g3 |
|       3        |    172.16.141.227    | ns.building-3.rcomp-21-22-dc-g3 |
|       4        |    172.16.142.243    | ns.building-4.rcomp-21-22-dc-g3 |
