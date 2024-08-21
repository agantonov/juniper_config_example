#### Mirroring Instance on PTX (EVO) - Local
```
set groups PM interfaces ae0 unit 1 family inet filter input mirror_v4
set groups PM interfaces ae0 unit 1 family inet6 filter input mirror_v6
set groups PM interfaces et-1/0/35 unit 0 family inet address 192.168.100.2/24
set groups PM interfaces et-1/0/35 unit 0 family inet6 address 2001::192:168:100:2/120
set groups PM forwarding-options port-mirroring input rate 1000
set groups PM forwarding-options port-mirroring family inet output interface et-1/0/35.0 next-hop 192.168.100.1
set groups PM forwarding-options port-mirroring family inet6 output interface et-1/0/35.0 next-hop 2001::192:168:100:1
set groups PM firewall family inet6 filter mirror_v6 term 1 then port-mirror
set groups PM firewall family inet6 filter mirror_v6 term 1 then accept
set groups PM firewall filter mirror_v4 term 1 then port-mirror
set groups PM firewall filter mirror_v4 term 1 then accept
```
#### Mirroring Instance on PTX (EVO) - Remote
```
set groups PM interfaces ae0 unit 1 filter input MirrorAny
set groups PM interfaces et-1/0/35 unit 0 family inet address 192.168.100.2/24
set groups PM interfaces et-1/0/35 unit 0 family inet6 address 2001::192:168:100:2/120
set groups PM interfaces fti0 unit 0 tunnel encapsulation gre source address 1.1.0.1
set groups PM interfaces fti0 unit 0 tunnel encapsulation gre destination address 2.2.0.1
set groups PM interfaces fti0 unit 0 family ccc
set groups PM forwarding-options port-mirroring instance RemotePM input rate 1000
set groups PM forwarding-options port-mirroring instance RemotePM family any output interface fti0.0
set groups PM firewall family any filter MirrorAny term 1 then port-mirror-instance RemotePM
set groups PM firewall family any filter MirrorAny term 1 then accept
set groups PM routing-options static route 2.2.0.1/32 next-hop 192.168.100.1
```

#### Mirroring Instance on MX
```
set groups ANALYZER chassis fpc 0 port-mirror-instance INGRESS
set groups ANALYZER interfaces ae4 unit 0 family mpls filter input ingress
set groups ANALYZER interfaces et-0/0/2 unit 999 encapsulation vlan-bridge
set groups ANALYZER interfaces et-0/0/2 unit 999 vlan-id 999
set groups ANALYZER forwarding-options port-mirroring instance INGRESS input rate 1
set groups ANALYZER forwarding-options port-mirroring instance INGRESS family any output interface et-0/0/2.999
set groups ANALYZER forwarding-options port-mirroring instance INGRESS family any output no-filter-check
set groups ANALYZER firewall family mpls filter ingress term 1 then port-mirror-instance INGRESS
set groups ANALYZER firewall family mpls filter ingress term 1 then accept
set groups ANALYZER bridge-domains INGRESS domain-type bridge
set groups ANALYZER bridge-domains INGRESS vlan-id 999
set groups ANALYZER bridge-domains INGRESS interface et-0/0/2.999
```
Show status:
```
# run show forwarding-options port-mirroring
Instance Name: INGRESS
  Instance Id: 2
  Input parameters:
    Rate                  : 1
    Run-length            : 0
    Maximum-packet-length : 0
  Output parameters:
    Family              State     Destination          Next-hop
    any                 up        et-0/0/2.999         NA
```
#### Mirroring on ACX7k
```
set groups ANALYZER interfaces et-0/0/25 unit 0 encapsulation vlan-bridge
set groups ANALYZER interfaces et-0/0/25 unit 0 vlan-id 4090
set groups ANALYZER forwarding-options analyzer A0 input ingress interface ae5.0
set groups ANALYZER forwarding-options analyzer A0 output interface et-0/0/25.0
set groups ANALYZER vlans VLAN4090 vlan-id 4090
set groups ANALYZER vlans VLAN4090 interface et-0/0/25.0
```
VLAN Output:
```
set groups ANALYZER forwarding-options analyzer A0 output vlan VLAN4090
```
Show status:
```
# run show forwarding-options analyzer
  Analyzer name                    : A0
  Mirror rate                      : 1
  Maximum packet length            : 0
  State                            : up
  Ingress monitored interfaces     : ae5.0
  Output interface                 : et-0/0/25.0
```
