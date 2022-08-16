# BGP
### Autonomous System
An autonomous system (AS) is a collection of routers under a single organization's control, using one or more IGPs and common metrics to route packets within the AS.  

### Autonomous System Numbers
Require for organisation requiring connectivity to the Internet.  
ASNs originals: 2 bytes (16-bit), 65,535 ASNs.  
RFC 4893: 4 bytes (32-bit), 4,294,967,295 ASNs.  
  
Internet Assigned Numbers Authority (IANA) is responsible for assigning public ASNs.  


#### Private ASNs  
16-bit ASNs: 64,512-65,535  
32-bit ASNs: 4,200,000,000-4,294,967,295  

### BGP path attributes (PA)
Provide BGP with granularity and control of routing policies  

##### PA classification
- Well-know mandatory
	- Must be reconized by all BGP implementations. Must be included with every prefix advertisement.
- Well-know discretionary
	- Must be reconized by all BGP implementations. May or may not be included with a prefix advertisement.
- Optional transitive
	- Do not have to be reconized by all BGP implementations. Stay with the route advertisement from AS to AS.
- Optional non-transitive
	- Do not have to be reconized by all BGP implementations. Cannot be shared from AS to AS.

  
The **Network Layer Reachability Information (NLRI)** is a routing update that consist of the network prefix, prefix lenght, and any BGP PAs for the specifirc route.  

#### AS_Path BGP attribute
Well-know mandatory attribute.  
Include a complete list of all the ASNs that the prefix advertisement has traverses from its source AS.  
Used as a loop-prevention mechanism: if a BGP router receives a prefix advertisement with is AS listed in the AS_Path, it discards the prefix because the router thinks the advertisement forms a loop.  

### Inter-Router communication
BGP neighbors are defined by IP address.  
BGP uses TCP port 179 to communicate with other routers. By using TCP, BGP can form neighbor adjacencies to directly connected neighbors or multiple hops away neighbors.  
BGP session = a established adacency between two BGP routers.  

#### BGP Session Types
- Internal BGP (iBGP)
	- Session established with router in the same AS or same BGP confederation.
	- Assigned an AD of 200 in RIB.
- External BGP (eBGP)
	- Session established with a router in a different AS.
	- Assigned an AD of 20 in RIB.

#### BGP Messages
##### BGP Packet Types
Type | Name         | Functional Overview|
|:-- | :---         | :------------------|
| 1  | OPEN         | Sets up and established BGP adjacency|
| 2  | UPDATE       | Advertises, updates, or withdraws routes|
| 3  | NOTIFICATION | Indicates an error condition to a BGP neighbor|
| 4  | KEEPALIVE    | Ensure that BGP neighbors ar still alive |

- OPEN: includes BGP version number, ASN of the originating router, hold time, BGP identiifer, other optional paramaters that establish the session capabilities.
- KEEPALIVE: exchanged every one-third of the hold timer. Cisco default hold timer is 180s, so keepalive interval is 60s. If hold time is 0, no keepalive is sent.
- UPDATE: advertises feasible routes, withdraws previously advertised routes, or can do both. Include NLRI, such as the prefix and associate BGP PAs when advertising prefixes. Withdrawn NLRI include only the prefix. Can act as a keepalive.
- NOTICATION: sen when an error is detected with the BGP session (hold timer expiring, neighbor capabilities changing, or BGP session reset being requested). Cause the BGP session to close.

- BGP identifier: BGP RI is a 32-bit unique number. Can be set manually or dynamically by BGP.  

#### BGP Neighbor States
BGP uses hte finite-state machine (MSF) to maintain a table of all BGP peers and their operational status.
##### BGP session states
- Idle
- Connect
- Active
- OpenSent
- OpenConfirm
- Established

### BGP Basic Configuration
BGP router configuration require the following components:  

- BGP session paramaters  
- Address family initialization  
- Activate the address family on the BGP peer

Initialize the BGP process in global configuration  
<code>router bgp <em>as-number</em></code>  
#### RID
1. Statically define router ID (RID)
2. Highest IP address of any up loopback interfaces.
3. Highest IP address of any up interfaces.

Configure static RID in router mode
<code>bgp router-id <em>router-id</em></code>  
Identify BGP neighbor's IP address and AS in router mode  
<code>neighbor <em>ip-address</em> remote-as <em>as-number</em></code>  

IOS activates the IPv4 address family by default and the safi is unicast by default.   
To disables automatic activation of IPv4 AFI  
<code>no bgp default ipv4-unicast</code>  
If IPv4 AFI is disable, initialize IPv4 address family in router mode
<code>address-family <em>afi safi</em></code>  
afi = IPV4 or IPV6  
safi = unicast or multicast  

**Verification**  
<code>show bgp <em>afi safi</em> summary</code>  
<code>show bgp <em>afi safi</em> neighbors <em>ip-address</em></code>  

