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


## BID, priority & selection criterion
Priority is priority plus <em>sys-id-ext</em> (which is VLAN number).  
Default priority is 32,768.  

Logic of selection criterion
1. Interface associated to lowest path cost.  
2. Interface associated to the l;owest system priority of the advertising switch.  
3. Interface associated to the lowest system MAC address of the advertising switch.  
4. With multiple link to the same switch, the lowest port priority from the advertising switch.  
5. With multiple link to the same switch, the lower port number from the advertising switch.

## STP election steps
1. Identify the root bridge : switch with superior BPDU (lower BID) win election.
2. On every non-root switch, determine root port (RP).  
3. All others ports are considered designated ports. On non-root switch connected to each other on their designated ports, one of those switch ports mist be set to a blocking state.

## MST
**MSTI** : MST instance, mapping of one or multiple VLANs onto a single STP tree.  
**MST region** : a grouping of MST switches with the same high-level configuration.  
**IST** : internal spanning tree, first instance, instance 0.  

### MST Configuration
1. Define MST as the STP : <code>spanning-tree mode mst</code>  
2. (Optional) Define MST instance priority, priority is between 0 and 61,440, in increments of 4096. If using <code>root</code>, primary sets to 24,576 (if the local bridge MAC is lower than the current root bridge's MAC) or 4096 lower than the current root's priority (if the local bridge MAC is higher than the current root bridge's MAC) and secondary sets to 28,672.  
	- <code>spanning-tree mst <em>instance-number</em> priority <em>priority</em></code>
	- <code>spanning-tree mst <em>instance-number</em> root {primary | secondary}[diameter <em>diameter</em>]</code>	
3. Associate VLANs to MSTI.  
	1. <code>spanning-tree mst configuration</code>  
	2. <code>instance <em>instance-number</em> vlan <em>vlan-id</em></code>
4. Specify the MST version number : in mst configuration submode <code>revision <em>version</em></code>  
5. (Optional) Define the MST region name : <code>name <em>mst-region-name</em></code>

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

### MST
<code>spanning-tree mode mst</code>  
<code>spanning-tree mst <em>instance-number</em> priority <em>priority</em></code>  
<code>spanning-tree mst <em>instance-number</em> root {primary | secondary}[diameter <em>diameter</em>]</code>  
<code>spanning-tree mst configuration</code>  
<code>instance <em>instance-number</em> vlan <em>vlan-id</em></code>  
<code>revision <em>version</em></code>  
<code>name <em>mst-region-name</em></code>  
In interface configuration mode
<code>spanning-tree mst <em>instance-number</em> cost <em>cost</em></code>  
<code>spanning-tree mst <em>instance-number</em> port-priority <em>priority</em></code>  

### Verification
<code>show spanning-tree</code>  
<code>show spanning-tree [vlan <em>vlan-id</em>] detail</code>  
<code>show spanning-tree root</code>
<code>show spanning-tree interface <em>interface-id</em> [detail]</code>  
<code>show spanning-tree mst configuration</code>  
<code>show spanning-tree mst</code>  
<code>show spanning-tree mst [<em>instance-number</em>]</code>
<code>show spanning-tree mst interface [<em>interface-id</em>]</code>