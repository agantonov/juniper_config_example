## EVPN VPWS Service

Routing Instance
```
set routing-instances evpn_vpws_3001 instance-type evpn-vpws
set routing-instances evpn_vpws_3001 protocols evpn interface ae17.3001 vpws-service-id local 1
set routing-instances evpn_vpws_3001 protocols evpn interface ae17.3001 vpws-service-id remote 2
set routing-instances evpn_vpws_3001 protocols evpn no-control-word
set routing-instances evpn_vpws_3001 interface ae17.3001
set routing-instances evpn_vpws_3001 route-distinguisher 1.1.0.7:13001
set routing-instances evpn_vpws_3001 vrf-target target:65100:100023001
```
CE-facing interface
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
set interfaces ae17 unit 3001 encapsulation vlan-ccc
set interfaces ae17 unit 3001 vlan-id 3001
```
Show commands
```
run show evpn vpws-instance evpn_vpws_3001
Instance: evpn_vpws_3001, Instance type: EVPN VPWS, Encapsulation type: MPLS
  Route Distinguisher: 1.1.0.7:13001
  Number of local interfaces: 1 (1 up)

    Interface name  ESI                            Mode          Role       Status     Control-Word    Flow-Label-Tx    Flow-Label-Rx
    ae17.3001       00:14:15:00:00:00:00:00:17:00 all-active      Primary    Up         No              No               No
        Local SID: 1 Advertised Label: 626
            PE addr         ESI                           Label  End.Dx2 SID     Mode           Role     TS                      Status
            1.1.0.8         00:14:15:00:00:00:00:00:17:00 625                    all-active     Primary  2023-12-19 20:36:43.196 Resolved
        Remote SID: 2
            PE addr         ESI                           Label  End.Dx2 SID     Mode           Role     TS                      Status
            1.1.0.1         00:16:17:00:00:00:00:00:28:00 8018                   all-active     Primary  2023-12-18 11:32:01.499 Resolved
  Number of protect interfaces: 0

    Fast Convergence Information
    ESI: 00:14:15:00:00:00:00:00:17:00 Number of PE nodes: 1
        PE: 1.1.0.8
            Advertised SID: 1

    Fast Convergence Information
    ESI: 00:16:17:00:00:00:00:00:28:00 Number of PE nodes: 1
        PE: 1.1.0.1
            Advertised SID: 2
```
