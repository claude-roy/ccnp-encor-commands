# IP Address
In interface submode  
<code>ip address <em>ip-address subnet-mask</em></code>  
Adding a IPv4 secondary address  
<code>ip address <em>ip-address subnet-mask</em> secondary</code>  
<code>ipv6 address <em>ipv6-address/prefix-length</em></code>

#### Routed Subinterfaces
In subinterface submode  
<code>encapsulation dot1q <em>vlan-id</em></code>  
<code>encapsulation dot1q <em>vlan-id</em> native</code>

#### Switched Virtual Interfaces
<code>interface vlan <em>vlan-id</em></code>

#### Routed Switch Ports
In interface submode  
<code>no switchport</code>

## Verification
<code>show ip interface [brief | <em>interface-id</em> | vlan <em>vlan-id</em></code>  
<code>show ipv6 interface [brief | <em>interface-id</em> | vlan <em>vlan-id</em></code>  

