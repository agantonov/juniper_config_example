## EVPN-ELAN
### EVO
MAC-VRF Instance (vlan-based)
```
set routing-instances evpn_elan_1 instance-type mac-vrf
set routing-instances evpn_elan_1 protocols evpn encapsulation mpls
set routing-instances evpn_elan_1 protocols evpn no-control-word
set routing-instances evpn_elan_1 service-type vlan-based
set routing-instances evpn_elan_1 route-distinguisher 1.1.0.7:21
set routing-instances evpn_elan_1 vrf-target target:65100:200001
set routing-instances evpn_elan_1 vlans bd1 vlan-id 1
set routing-instances evpn_elan_1 vlans bd1 interface ae17.1
```
CE-facing Interface
```
set interfaces ae17 description "CE-facing interface"
set interfaces ae17 flexible-vlan-tagging
set interfaces ae17 mtu 9192
set interfaces ae17 encapsulation flexible-ethernet-services
set interfaces ae17 esi 00:14:15:00:00:00:00:00:17:00
set interfaces ae17 esi all-active
set interfaces ae17 esi df-election-type preference value 100
set interfaces ae17 aggregated-ether-options lacp active
set interfaces ae17 aggregated-ether-options lacp periodic fast
set interfaces ae17 aggregated-ether-options lacp fast-failover
set interfaces ae17 aggregated-ether-options lacp system-id 00:00:00:00:17:00
set interfaces ae17 aggregated-ether-options lacp aggregate-wait-time 120
set interfaces ae17 unit 1 encapsulation vlan-bridge
set interfaces ae17 unit 1 vlan-id 1
```
Show commands
```
# run show mac-vrf forwarding mac-table instance evpn_elan_1

MAC flags (S - static MAC, D - dynamic MAC, L - locally learned, P - Persistent static, C - Control MAC
           SE - statistics enabled, NM - non configured MAC, R - remote PE MAC, O - ovsdb MAC
           GBP - group based policy, B - Blocked MAC)


Ethernet switching table : 2 entries, 2 learned
Routing instance : evpn_elan_1
    Vlan                MAC                 MAC         Age   GBP     Logical                NH        RTR
    name                address             flags             Tag     interface              Index     ID
    bd1                 00:16:17:00:00:01   D             -            ae17.1                 0         0
    bd1                 00:1f:19:00:00:01   DC            -                                   59147     59147
```
### Junos
MAC-VRF Instance (vlan-based)
```
set routing-instances evpn_elan_1 instance-type evpn
set routing-instances evpn_elan_1 protocols evpn
set routing-instances evpn_elan_1 vlan-id none
set routing-instances evpn_elan_1 no-normalization
set routing-instances evpn_elan_1 interface ae29.1
set routing-instances evpn_elan_1 route-distinguisher 1.1.0.1:21
set routing-instances evpn_elan_1 vrf-target target:65100:200001
```
CE-facing Interface
```
set interfaces ae29 flexible-vlan-tagging
set interfaces ae29 mtu 9192
set interfaces ae29 encapsulation flexible-ethernet-services
set interfaces ae29 esi 00:16:17:00:00:00:00:00:29:00
set interfaces ae29 esi all-active
set interfaces ae29 esi df-election-type preference value 100
set interfaces ae29 aggregated-ether-options lacp active
set interfaces ae29 aggregated-ether-options lacp periodic fast
set interfaces ae29 aggregated-ether-options lacp fast-failover
set interfaces ae29 aggregated-ether-options lacp system-id 00:00:00:00:29:00
set interfaces ae29 unit 1 encapsulation vlan-bridge
set interfaces ae29 unit 1 vlan-id 1
```
Show commands
```
# run show evpn mac-table instance evpn_elan_1

MAC flags       (S -static MAC, D -dynamic MAC, L -locally learned, C -Control MAC
    O -OVSDB MAC, SE -Statistics enabled, NM -Non configured MAC, R -Remote PE MAC, P -Pinned MAC)

Routing instance : evpn_elan_1
 Bridging domain : __evpn_elan_1__, VLAN : none
   MAC                 MAC      Logical          NH     MAC         active
   address             flags    interface        Index  property    source
   00:14:29:00:00:01   D        ae29.1
   00:16:17:00:00:01   DC                        1062658            00:14:15:00:00:00:00:00:17:00
   00:1f:19:00:00:01   DC                        1056588            00:02:03:01:00:00:00:00:19:00
```
