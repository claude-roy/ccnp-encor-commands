# STP - Spanning Tree Protocol
## STP Iterations
* **802.1d**, original specification
* **PVST**, Per-VLAN Spanning-Tree
* **PVST+**, Per-VLAN Spanning-Tree Plus
* **802.1w RSTP**, Rapid Spanning Tree Protocol
* **802.S MST**, Multiple Spanning Tree Protocol  

## 802.1D Port States
* **Disabled**: Administravely off (shut down)
* **Blocking**: Port enabled. Do not forward any traffic to ensure that a loop is not created.  Does not modify the MAC address table. Only receive BPDUs.
* **Listening**: Send and receive BPDUs. Do not forward any other traffic. (State duration: forwarding time)
* **Learning**: Can modify the MAC address table. Do not forward any other traffic. (State duration: forwarding time).
* **Forwarding**: Forward all network traffic and can update the MAC address table. Final state.
* **Broken**: Configuration or operational problem. Port discards packets.

## 802.1D Port Types
* **RP - Root port**: A network port that connects to the root bridge. One root port per VLAN on a switch.
* **DP - Designated port**: A network port that receives and forwards BPDU to others switch. Provide connectivity to downstream devices and switches. Only one DP on a link.
* **Blocking port**: A network port that is not forwarding traffic.

## STP Timers
* **Max age**: If a switch loses contact with the BPDUs source, it assumes that the BPDU information is still valid for the duration of the Max Age timer. The default value is 20 seconds.
* **Hello time**: Time the BPDUs are advertised out of a port. The default value is 2 seconds.
* **Forward delay**: The amount of time a port stys in a listening and learning state. The dafault value is 15 seconds.

## STP Path Cost
Short-mode : original STP cost is a 16-bit value  
Long-mode  : STP cost is a 32-bit value  

|Link Speed|Short-Mode STP Cost|Long-mode STP Cost|
|:---------|:----------------- |:-----------------|
|10 Mbps   |100                |2,000,000         |
|100 Mbps  |19                 |200,000           |
|1 Gbps    |4                  |20,000            |
|10 Gbps   |2                  |2,000             |
|20 Gbps   |1                  |1,000             |
|100 Gbps  |1                  |200               |
|1 Tbps    |1                  |20                |
|10 Tbps   |1                  |2                 |

## STP commands
### Timers
In global configuration mode.  
<code>spanning-tree vlan <em>vlan-id</em> max-age <em>maxage</em></code>
<code>spanning-tree vlan <em>vlan-id</em> hello-time <em>hellotime</em></code>  
Hello time can be between 1 and 10 seconds.
<code>spanning-tree vlan <em>vlan-id</em> forward-time <em>forwardtime</em></code>  
Forward timer can be between 4 and 30 seconds.

### Changing Path Cost to long-mode
In global configuration mode  
<code>spanning-tree pathcost method long</code>