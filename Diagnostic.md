# Diagnostic commands
### General
**Arp table**  
<code>show ip arp [<em>mac-address</em> | <em>ip-address</em> | vlan <em>vlan-id</em> | <em>interface-id</em>]</code>  

### Layer 2
<code>show mac-address-table [address <em>mac-address</em> | dynamic | vlan <em>vlan-id</em></code>  
<code>clear mac address-table dynamic [{address <em>mac-address</em> | interface <em>interface-id</em> | vlan <em>vlan-id</em>}]</code>  
In global configuration  
<code>mac address-table static <em>mac-address</em> vlan <em>vlan-id</em> {drop | interface <em>interface-id</em>}</code>  
**Switch Port Status**  
<code>show interfaces switchport</code>  
<code>show interfaces <em>interface-id</em> switchport</code>  
<code>show interface status</code>

