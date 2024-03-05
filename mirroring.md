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
