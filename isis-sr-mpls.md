Policy to leak routes from L2 to L1
```
set policy-options policy-statement leak-L2-to-L1 from protocol isis
set policy-options policy-statement leak-L2-to-L1 from level 2
set policy-options policy-statement leak-L2-to-L1 from route-filter 0.0.0.0/0 prefix-length-range /32-/32
set policy-options policy-statement leak-L2-to-L1 to protocol isis
set policy-options policy-statement leak-L2-to-L1 to level 1
set policy-options policy-statement leak-L2-to-L1 then accept
set policy-options policy-statement leak-L2-to-L1-v6 from family inet6
set policy-options policy-statement leak-L2-to-L1-v6 from protocol isis
set policy-options policy-statement leak-L2-to-L1-v6 from level 2
set policy-options policy-statement leak-L2-to-L1-v6 from route-filter ::/0 prefix-length-range /128-/128
set policy-options policy-statement leak-L2-to-L1-v6 to protocol isis
set policy-options policy-statement leak-L2-to-L1-v6 to level 1
set policy-options policy-statement leak-L2-to-L1-v6 then accept
set policy-options policy-statement export-default-to-L1 term 1 from route-filter 0.0.0.0/0 exact
set policy-options policy-statement export-default-to-L1 term 1 to protocol isis
set policy-options policy-statement export-default-to-L1 term 1 to level 1
set policy-options policy-statement export-default-to-L1 term 1 then accept
```
ISIS/SR-MPLS
```
set protocols isis interface ae5.0 level 2 post-convergence-lfa node-protection cost 16777214
set protocols isis interface ae5.0 point-to-point
set protocols isis interface ae12.0 level 1 post-convergence-lfa node-protection cost 16777214
set protocols isis interface ae12.0 point-to-point
set protocols isis interface lo0.0 passive
set protocols isis interface ae31.0 level 2 post-convergence-lfa node-protection cost 16777214
set protocols isis interface ae31.0 level 1 post-convergence-lfa node-protection cost 16777214
set protocols isis interface ae31.0 point-to-point
set protocols isis source-packet-routing srgb start-label 16000
set protocols isis source-packet-routing srgb index-range 80000
set protocols isis source-packet-routing node-segment ipv4-index 6
set protocols isis source-packet-routing node-segment ipv6-index 106
set protocols isis source-packet-routing traffic-statistics statistics-granularity per-interface
set protocols isis level 2 wide-metrics-only
set protocols isis level 1 wide-metrics-only
set protocols isis spf-options microloop-avoidance post-convergence-path delay 5000
set protocols isis spf-options delay 50
set protocols isis spf-options rapid-runs 5
set protocols isis backup-spf-options use-post-convergence-lfa maximum-labels 8
set protocols isis backup-spf-options use-source-packet-routing
set protocols isis export leak-L2-to-L1
set protocols isis export leak-L2-to-L1-v6
set protocols isis reference-bandwidth 4000g
set protocols isis traffic-engineering l3-unicast-topology
set protocols isis traffic-engineering advertisement always
```
Separate topology for IPv6 unicast
```
set groups ISIS-GROUP protocols isis topologies ipv6-unicast
```
