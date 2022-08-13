# BGP
## Autonomous System
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