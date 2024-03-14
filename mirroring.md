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
