# VLANs & Trunking
### Create VLAN
In global configuration  
<code>vlan <em>vlan-id</em></code>  
In VLAN submode (max. 32 characters for the name)  
<code>name <em>vlanname</em></code>  
VLAN is not created until you exit VLAN ID.  
**Verification**  
<code>show vlan [{brief | id <em> vlan-id</em> | name <em>vlanname</em> | summary}]</code>
### Access and trunk ports
In interface subcommand  
**access mode**     
<code>switchport mode access</code>  
<code>switchport access {vlan <em>vlan-id</em> | name <em>vlanname</em>}</code>  
**trunk mode**  
<code>switchport mode trunk</code>  
<code>switchport trunk native vlan <em>vlan-id</em></code>  
<code>switchport trunk allowed vlan {<em>vlan-id</em> | all | none| add <em>vlan-ids</em> | remove <em>vlan-ids</em> | exept <em>vlans-ids</em>}</code>  
**Trunk verification**  
<code>show interface trunk</code>