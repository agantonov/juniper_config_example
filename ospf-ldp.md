OSPF
```
set protocols ospf traffic-engineering l3-unicast-topology
set protocols ospf traffic-engineering advertisement always
set protocols ospf backup-spf-options per-prefix-calculation all
set protocols ospf area 0.0.0.0 interface lo0.0 passive
set protocols ospf area 0.0.0.0 interface ae5.0 interface-type p2p
set protocols ospf area 0.0.0.0 interface ae5.0 node-link-protection
set protocols ospf reference-bandwidth 4000g
```
LDP
```
set protocols ldp track-igp-metric
set protocols ldp make-before-break
set protocols ldp interface lo0.0
set protocols ldp interface ae5.0 link-protection
set protocols ldp p2mp
```
MPLS
```
set protocols mpls lsp-external-controller pccd
set protocols mpls log-updown syslog
set protocols mpls log-updown trap
set protocols mpls no-propagate-ttl
set protocols mpls icmp-tunneling
set protocols mpls revert-timer 180
set protocols mpls optimize-timer 180
set protocols mpls ipv6-tunneling
set protocols mpls interface lo0.0
set protocols mpls interface ae5.0
```
