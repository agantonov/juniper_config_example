#### LAG to PE1 and PE2
```
set interfaces ae10 flexible-vlan-tagging
set interfaces ae10 encapsulation extended-vlan-bridge
set interfaces ae10 aggregated-ether-options lacp active
set interfaces ae10 aggregated-ether-options lacp periodic fast
set interfaces ae10 unit 0 vlan-id-list 4001-4010
set interfaces ae10 unit 0 input-vlan-map push
set interfaces ae10 unit 0 input-vlan-map vlan-id 10
set interfaces ae10 unit 0 output-vlan-map pop
```
#### PE2
```
set interfaces et-0/0/49 flexible-vlan-tagging
set interfaces et-0/0/49 encapsulation extended-vlan-bridge
set interfaces et-0/0/49 unit 0 vlan-id-list 1-4000
set interfaces et-0/0/49 unit 0 input-vlan-map push
set interfaces et-0/0/49 unit 0 input-vlan-map vlan-id 20
set interfaces et-0/0/49 unit 0 output-vlan-map pop
```
#### IXIA facing interface
```
set interfaces et-0/0/50 flexible-vlan-tagging
set interfaces et-0/0/50 encapsulation flexible-ethernet-services
set interfaces et-0/0/50 unit 10 encapsulation vlan-bridge
set interfaces et-0/0/50 unit 10 vlan-id-list 4001-4010
set interfaces et-0/0/50 unit 10 input-vlan-map push
set interfaces et-0/0/50 unit 10 input-vlan-map vlan-id 10
set interfaces et-0/0/50 unit 10 output-vlan-map pop
set interfaces et-0/0/50 unit 20 encapsulation vlan-bridge
set interfaces et-0/0/50 unit 20 vlan-id-list 1-4000
set interfaces et-0/0/50 unit 20 input-vlan-map push
set interfaces et-0/0/50 unit 20 input-vlan-map vlan-id 20
set interfaces et-0/0/50 unit 20 output-vlan-map pop
```
#### VLANs
```
set vlans PE2-et-0_0_0 interface et-0/0/49.0
set vlans PE2-et-0_0_0 interface et-0/0/50.20
set vlans PE1-PE2-ae10 interface ae10.0
set vlans PE1-PE2-ae10 interface et-0/0/50.10
```
