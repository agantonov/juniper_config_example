## NG-MVPN
### Multicast Source
Interfaces
```
set interfaces lo0 unit 1 family inet address 1.1.100.1/32
set interfaces et-0/2/0 unit 3999 vlan-id 3999
set interfaces et-0/2/0 unit 3999 family inet address 192.168.100.1/24
```
Policy to import routes from receivers
```
set policy-options policy-statement import-Mcast-Receivers-v3 from community mcast-receiver-v3
set policy-options policy-statement import-Mcast-Receivers-v3 then accept
set policy-options community mcast-receiver-v3 members target:65100:2001
set policy-options community mcast-receiver-v3 members target:65100:4041
```
Multicast VRF
```
set routing-instances ng-mvpn-v3 instance-type vrf
set routing-instances ng-mvpn-v3 protocols mvpn sender-site
set routing-instances ng-mvpn-v3 protocols mvpn mvpn-mode spt-only
set routing-instances ng-mvpn-v3 protocols mvpn sender-based-rpf
set routing-instances ng-mvpn-v3 protocols pim rp local address 1.1.100.1
set routing-instances ng-mvpn-v3 protocols pim interface lo0.1 mode sparse
set routing-instances ng-mvpn-v3 protocols pim interface et-0/2/0.3999 mode sparse
set routing-instances ng-mvpn-v3 protocols pim interface all mode sparse
set routing-instances ng-mvpn-v3 interface lo0.1
set routing-instances ng-mvpn-v3 interface et-0/2/0.3999
set routing-instances ng-mvpn-v3 route-distinguisher 1.1.0.1:3999
set routing-instances ng-mvpn-v3 vrf-import import-Mcast-Receivers-v3
set routing-instances ng-mvpn-v3 vrf-target target:65100:3999
set routing-instances ng-mvpn-v3 vrf-table-label
set routing-instances ng-mvpn-v3 provider-tunnel ldp-p2mp
```
### Multicast Receiver
IRB interface with virtual GW
```
set interfaces irb unit 2001 virtual-gateway-accept-data
set interfaces irb unit 2001 family inet address 17.0.0.2/24 virtual-gateway-address 17.0.0.1
set interfaces irb unit 2001 interface-state local
```
L2 interface
```
set interfaces ae17 unit 2001 encapsulation vlan-bridge
set interfaces ae17 unit 2001 vlan-id 2001
```
Policy to import routes from the source
```
set policy-options policy-statement import-Mcast-Source-v3 from community mcast-source-v3
set policy-options policy-statement import-Mcast-Source-v3 then accept
set policy-options community mcast-source-v3 members target:65100:3999
```
Multicast VRF
```
set routing-instances multicast_vrf_2001 instance-type vrf
set routing-instances multicast_vrf_2001 routing-options router-id 1.1.0.7
set routing-instances multicast_vrf_2001 protocols mvpn receiver-site
set routing-instances multicast_vrf_2001 protocols mvpn mvpn-mode spt-only
set routing-instances multicast_vrf_2001 protocols pim rp static address 1.1.100.1
set routing-instances multicast_vrf_2001 protocols pim interface irb.2001 mode sparse
set routing-instances multicast_vrf_2001 protocols pim interface irb.2001 distributed-dr
set routing-instances multicast_vrf_2001 interface irb.2001
set routing-instances multicast_vrf_2001 route-distinguisher 1.1.0.7:2001
set routing-instances multicast_vrf_2001 vrf-import import-Mcast-Source-v3
set routing-instances multicast_vrf_2001 vrf-target target:65100:2001
set routing-instances multicast_vrf_2001 vrf-table-label
```
EVPN Instance
```
set routing-instances evpn_l3_2001 instance-type mac-vrf
set routing-instances evpn_l3_2001 protocols igmp-snooping proxy
set routing-instances evpn_l3_2001 protocols igmp-snooping vlan bd2001 proxy
set routing-instances evpn_l3_2001 protocols igmp-snooping vlan bd2001 evpn-ssm-reports-only //required for IGMPv3
set routing-instances evpn_l3_2001 protocols igmp-snooping vlan bd2001 interface ae17.2001 host-only-interface
set routing-instances evpn_l3_2001 protocols evpn designated-forwarder-election-hold-time 1
set routing-instances evpn_l3_2001 protocols evpn default-gateway no-gateway-community
set routing-instances evpn_l3_2001 service-type vlan-based
set routing-instances evpn_l3_2001 interface ae17.2001
set routing-instances evpn_l3_2001 route-distinguisher 1.1.0.7:12001
set routing-instances evpn_l3_2001 vrf-target target:65100:12001
set routing-instances evpn_l3_2001 vlans bd2001 vlan-id 2001
set routing-instances evpn_l3_2001 vlans bd2001 interface ae17.2001
set routing-instances evpn_l3_2001 vlans bd2001 l3-interface irb.2001
```
IGMP Snooping
```
set protocols igmp interface irb.2001 version 3 //required for IGMPv3
```
Static IGMP Join (optional)
```
set protocols igmp interface irb.2001 static group 232.0.0.0 group-count 512
set protocols igmp interface irb.2001 static group 232.0.0.0 source 192.168.100.2
```

### Show commands
Multicast route
```
run show multicast route instance multicast_vrf_2001
Instance: multicast_vrf_2001 Family: INET

Group: 232.0.0.0
    Source: 192.168.100.10/32
    Upstream interface: lsi.50
    Downstream interface list:
        irb.2001


Group: 232.0.0.1
    Source: 192.168.100.10/32
    Upstream interface: lsi.50
    Downstream interface list:
        irb.2001
```
IGMP Group
```
# run show igmp group
Interface: irb.2001, Groups: 2001
    Group: 224.0.0.13
        Source: 0.0.0.0
        Last reported by: 17.0.0.3
        Timeout:     169 Type: Dynamic
    Group: 232.0.0.0
        Group mode: Include
        Source: 192.168.100.10
        Last reported by: Local
        Timeout:       0 Type: EVPN
    Group: 232.0.0.1
        Group mode: Include
        Source: 192.168.100.10
        Last reported by: Local
        Timeout:       0 Type: EVPN
```
LDP
```
# run show ldp p2mp fec
LDP P2MP FECs:
 P2MP root-addr 1.1.0.1, lsp-id 16777217
  Fec type: Egress (Active)
  Label: 622
 P2MP root-addr 1.1.0.1, lsp-id 16777218
  Fec type: Egress (Active)
  Label: 623

# run show ldp p2mp path
P2MP path type: Transit/Egress
  Output Session (label): 1.1.0.5:0 (622) (Primary)
  Egress label: 622
  Attached FECs:  P2MP root-addr 1.1.0.1, lsp-id 16777217 (Active)
P2MP path type: Transit/Egress
  Output Session (label): 1.1.0.5:0 (623) (Primary)
  Egress label: 623
  Attached FECs:  P2MP root-addr 1.1.0.1, lsp-id 16777218 (Active)

# run show ldp traffic-statistics p2mp
P2MP FEC Statistics:

FEC(root_addr:lsp_id/grp,src)     Nexthop              Packets             Bytes Shared
1.1.0.1:16777217
                                  1.1.0.4           2507155275      446273638950 No
                                  1.1.0.3           1494505844      266022040232 No
1.1.0.1:16777218
                                  1.1.0.3                    0                 0 No

```
Routing table (receiver)
```
# run show route table multicast_vrf_2001.mvpn

multicast_vrf_2001.mvpn.0: 2002 destinations, 2003 routes (2002 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1:1.1.0.1:3999:1.1.0.1/240
                   *[BGP/170] 3d 02:40:47, localpref 100, from 1.1.0.101
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.7 via ae8.0, Push 16001
                       to 10.100.0.15 via ae12.0, Push 16001
                    [BGP/170] 3d 02:40:45, localpref 100, from 1.1.0.102
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.7 via ae8.0, Push 16001
                       to 10.100.0.15 via ae12.0, Push 16001
1:1.1.0.7:2001:1.1.0.7/240
                   *[MVPN/70] 6d 23:03:04, metric2 1
                       Indirect
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.0/240
                   *[PIM/105] 3d 02:36:43, metric 0
                       Multicast (IPv4) Composite
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.1/240
                   *[PIM/105] 3d 02:36:43, metric 0
                       Multicast (IPv4) Composite
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.2/240
                   *[PIM/105] 3d 02:36:43, metric 0
                       Multicast (IPv4) Composite
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.3/240
                   *[PIM/105] 3d 02:36:43, metric 0
                       Multicast (IPv4) Composite
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.4/240
                   *[PIM/105] 3d 02:36:43, metric 0
                       Multicast (IPv4) Composite

# run show route table multicast_vrf_2001.inet.1

multicast_vrf_2001.inet.1: 2003 destinations, 4003 routes (2003 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

224.0.0.0/4        *[Multicast/180] 6d 23:07:40
                    >  to 224.0.0.0
224.0.0.0/24       *[Multicast/180] 6d 23:07:40
                       MultiDiscard
232.0.0.0/8        *[Multicast/180] 6d 23:07:58
                    >  to 232.0.0.0
232.0.0.0,192.168.100.10/64*[Multicast/60] 3d 02:41:02
                       Multicast (IPv4) Composite
                    [MVPN/70] 3d 02:41:14
                       Multicast (IPv4) Composite
232.0.0.1,192.168.100.10/64*[Multicast/60] 3d 02:41:03
                       Multicast (IPv4) Composite
                    [MVPN/70] 3d 02:41:14
                       Multicast (IPv4) Composite
232.0.0.2,192.168.100.10/64*[Multicast/60] 3d 02:41:03
                       Multicast (IPv4) Composite
                    [MVPN/70] 3d 02:41:14
                       Multicast (IPv4) Composite
232.0.0.3,192.168.100.10/64*[Multicast/60] 3d 02:41:03
                       Multicast (IPv4) Composite
                    [MVPN/70] 3d 02:41:14
                       Multicast (IPv4) Composite
```

Advertising-protocol BGP (receiver)
```
# run show route advertising-protocol bgp 1.1.0.101 table multicast_vrf_2001.mvpn

multicast_vrf_2001.mvpn.0: 2002 destinations, 2003 routes (2002 active, 0 holddown, 0 hidden)
  Prefix		  Nexthop	       MED     Lclpref    AS path
  1:1.1.0.7:2001:1.1.0.7/240
*                         Self                         100        I
  7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.0/240
*                         Self                 0       100        I
  7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.1/240
*                         Self                 0       100        I
  7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.2/240
*                         Self                 0       100        I
  7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.3/240
*                         Self                 0       100        I
  7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.4/240
*                         Self                 0       100        I
```
Routing table (source)
```
# run show route table ng-mvpn-v3.mvpn

ng-mvpn-v3.mvpn.0: 2001 destinations, 6001 routes (2001 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1:1.1.0.1:3999:1.1.0.1/240
                   *[MVPN/70] 2w3d 14:13:49, metric2 1
                       Indirect
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.0/240
                   *[PIM/105] 5d 23:46:47, metric 0
                       Multicast (IPv4) Composite
                    [BGP/170] 3d 02:38:44, MED 0, localpref 100, from 1.1.0.101
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004
                    [BGP/170] 3d 02:38:45, MED 0, localpref 100, from 1.1.0.102
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.1/240
                   *[PIM/105] 5d 23:46:47, metric 0
                       Multicast (IPv4) Composite
                    [BGP/170] 3d 02:38:44, MED 0, localpref 100, from 1.1.0.101
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004
                    [BGP/170] 3d 02:38:45, MED 0, localpref 100, from 1.1.0.102
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004
7:1.1.0.1:3999:65100:32:192.168.100.10:32:232.0.0.2/240
                   *[PIM/105] 5d 23:46:47, metric 0
                       Multicast (IPv4) Composite
                    [BGP/170] 3d 02:38:44, MED 0, localpref 100, from 1.1.0.101
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004
                    [BGP/170] 3d 02:38:45, MED 0, localpref 100, from 1.1.0.102
                      AS path: I, validation-state: unverified
                    >  to 10.100.0.33 via ae1.0
                       to 10.100.0.27 via ae0.0, Push 16004

# run show route table ng-mvpn-v3.inet.1

ng-mvpn-v3.inet.1: 2003 destinations, 2003 routes (2003 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

224.0.0.0/4        *[Multicast/180] 2w3d 14:14:34
                       MultiResolve
224.0.0.0/24       *[Multicast/180] 2w3d 14:14:34
                       MultiDiscard
232.0.0.0/8        *[Multicast/180] 2w3d 14:14:37
                       MultiResolve
232.0.0.0,192.168.100.10/64*[MVPN/70] 3d 02:39:26
                    >  to 10.100.0.33 via ae1.0, Push 391
                       to 10.100.0.27 via ae0.0, Push 391, Push 486(top)
                       to 10.100.0.27 via ae0.0, Push 526
                       to 10.100.0.33 via ae1.0, Push 526, Push 419(top)
232.0.0.1,192.168.100.10/64*[MVPN/70] 3d 02:39:26
                    >  to 10.100.0.33 via ae1.0, Push 391
                       to 10.100.0.27 via ae0.0, Push 391, Push 486(top)
                       to 10.100.0.27 via ae0.0, Push 526
                       to 10.100.0.33 via ae1.0, Push 526, Push 419(top)
232.0.0.2,192.168.100.10/64*[MVPN/70] 3d 02:39:26
                    >  to 10.100.0.33 via ae1.0, Push 391
                       to 10.100.0.27 via ae0.0, Push 391, Push 486(top)
                       to 10.100.0.27 via ae0.0, Push 526
                       to 10.100.0.33 via ae1.0, Push 526, Push 419(top)
232.0.0.3,192.168.100.10/64*[MVPN/70] 3d 02:39:26
                    >  to 10.100.0.33 via ae1.0, Push 391
                       to 10.100.0.27 via ae0.0, Push 391, Push 486(top)
                       to 10.100.0.27 via ae0.0, Push 526
                       to 10.100.0.33 via ae1.0, Push 526, Push 419(top)
```
Advertising-protocol BGP (source)
```
# run show route advertising-protocol bgp 1.1.0.101 table ng-mvpn-v3.mvpn

ng-mvpn-v3.mvpn.0: 2001 destinations, 6001 routes (2001 active, 0 holddown, 0 hidden)
  Prefix		  Nexthop	       MED     Lclpref    AS path
  1:1.1.0.1:3999:1.1.0.1/240
*                         Self                         100        I
```
