## L3VPN with vGW
Routing Instance
```
set routing-instances l3vpn_irb_3501 instance-type vrf
set routing-instances l3vpn_irb_3501 routing-options rib l3vpn_irb_3501.inet6.0 multipath
set routing-instances l3vpn_irb_3501 routing-options rib l3vpn_irb_3501.inet6.0 protect core
set routing-instances l3vpn_irb_3501 routing-options router-id 1.1.0.7
set routing-instances l3vpn_irb_3501 routing-options multipath
set routing-instances l3vpn_irb_3501 routing-options protect core
set routing-instances l3vpn_irb_3501 routing-options auto-export
set routing-instances l3vpn_irb_3501 interface irb.3501
set routing-instances l3vpn_irb_3501 route-distinguisher 1.1.0.7:33501
set routing-instances l3vpn_irb_3501 vrf-target target:65100:300003501
set routing-instances l3vpn_irb_3501 vrf-table-label
```
MAC-VRF Instance (EVO)
```
set routing-instances evpn_l3_3501 instance-type mac-vrf
set routing-instances evpn_l3_3501 protocols evpn default-gateway no-gateway-community
set routing-instances evpn_l3_3501 service-type vlan-based
set routing-instances evpn_l3_3501 interface ae17.3501
set routing-instances evpn_l3_3501 route-distinguisher 1.1.0.7:43501
set routing-instances evpn_l3_3501 vrf-target target:65100:300103501
set routing-instances evpn_l3_3501 vlans bd3501 vlan-id 3501
set routing-instances evpn_l3_3501 vlans bd3501 interface ae17.3501
set routing-instances evpn_l3_3501 vlans bd3501 l3-interface irb.3501
```
IRB Interface
```
set interfaces irb unit 3501 virtual-gateway-accept-data
set interfaces irb unit 3501 family inet address 17.0.0.2/24 virtual-gateway-address 17.0.0.1
set interfaces irb unit 3501 family inet6 address 2001:17:10::2/64 virtual-gateway-address 2001:17:10::1
set interfaces irb unit 3501 interface-state local
```
L2 Interface
```
set interfaces ae17 unit 3501 encapsulation vlan-bridge
set interfaces ae17 unit 3501 vlan-id 3501
set interfaces ae17 unit 3501 input-vlan-map pop //optional
set interfaces ae17 unit 3501 output-vlan-map push //optional
```
MAC-VRF Instance (Junos)
```
set routing-instances evpn_l3_3501 instance-type evpn
set routing-instances evpn_l3_3501 protocols evpn
set routing-instances evpn_l3_3501 vlan-id none
set routing-instances evpn_l3_3501 routing-interface irb.3501
set routing-instances evpn_l3_3501 no-normalization
set routing-instances evpn_l3_3501 interface ae29.3501
set routing-instances evpn_l3_3501 route-distinguisher 1.1.0.1:43501
set routing-instances evpn_l3_3501 vrf-target target:65100:300123501
```

### Show commands
```
# run show mac-vrf forwarding mac-ip-table instance evpn_l3_3501

MAC IP flags  (S - Static, D - Dynamic, L - Local , R - Remote, Lp - Local Proxy,
               Rp - Remote Proxy, K - Kernel, RT - Dest Route, (N)AD - (Not) Advt to remote,
               RE - Re-ARP/ND, RO - Router, OV - Override, Ur - Unresolved,
               RTS - Dest Route Skipped, RGw - Remote Gateway, GBP - Group Based Policy,
               RTF - Dest Route Forced)
 Routing instance : evpn_l3_3501
 Bridging domain : bd3501
   IP                           MAC                  Flags              GBP    Logical            Active
   address                      address                                 Tag    Interface          source
   17.0.0.1                     00:00:5e:00:01:01    S,K                       irb.3501
   2001:17:10::1                00:00:5e:00:02:01    S,K                       irb.3501
   17.0.0.10                    00:2a:01:00:00:01    DLRp,K,RT,AD              ae17.3501
   2001:17:10::10               00:2a:01:00:00:01    DLR,K,RT,AD               ae17.3501
   fe80::22a:1ff:fe00:1         00:2a:01:00:00:01    DLR,K,RT,AD               ae17.3501
   17.0.0.3                     e8:24:a6:69:0e:86    SR,K,RT                                      1.1.0.8
   2001:17:10::3                e8:24:a6:69:0e:86    SR,K,RT                                      1.1.0.8
   fe80::ea24:a60d:ad69:e86     e8:24:a6:69:0e:86    SR,K,RTS                                     1.1.0.8
   17.0.0.2                     e8:24:a6:69:6e:86    S,K                       irb.3501
   2001:17:10::2                e8:24:a6:69:6e:86    S,K                       irb.3501
   fe80::ea24:a60d:ad69:6e86    e8:24:a6:69:6e:86    S,K                       irb.3501
```
