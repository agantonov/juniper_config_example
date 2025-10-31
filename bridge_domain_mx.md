Without IRB
```
set interfaces ae0 flexible-vlan-tagging
set interfaces ae0 encapsulation flexible-ethernet-services
set interfaces ae0 unit 3 encapsulation vlan-bridge
set interfaces ae0 unit 3 vlan-id 3
set interfaces ae0 unit 3 family bridge
set interfaces ae1 flexible-vlan-tagging
set interfaces ae1 encapsulation flexible-ethernet-services
set interfaces ae1 unit 3 encapsulation vlan-bridge
set interfaces ae1 unit 3 vlan-id 3
set interfaces ae1 unit 3 family bridge
set interfaces ae4 encapsulation ethernet-bridge
set interfaces ae4 unit 0 family bridge vlan-id 3
set interfaces ae5 encapsulation ethernet-bridge
set interfaces ae5 unit 0 family bridge vlan-id 3
set bridge-domains BD3 vlan-id 3
set bridge-domains BD3 interface ae0.3
set bridge-domains BD3 interface ae1.3
set bridge-domains BD3 interface ae4.0
set bridge-domains BD3 interface ae5.0
```
With IRB and RA
```
set interfaces ae0 flexible-vlan-tagging
set interfaces ae0 encapsulation flexible-ethernet-services
set interfaces ae0 unit 3 encapsulation vlan-bridge
set interfaces ae0 unit 3 vlan-id 3
set interfaces ae0 unit 3 family bridge
set interfaces ae3 flexible-vlan-tagging
set interfaces ae3 encapsulation flexible-ethernet-services
set interfaces ae3 unit 3 encapsulation vlan-bridge
set interfaces ae3 unit 3 vlan-id 3
set interfaces ae3 unit 3 family bridge
set interfaces irb unit 3 family inet address 10.0.0.2/25 primary
set interfaces irb unit 3 family inet address 10.0.0.2/25 vrrp-group 1 virtual-address 10.0.0.1
set interfaces irb unit 3 family inet address 10.0.0.2/25 vrrp-group 1 priority 110
set interfaces irb unit 3 family inet address 10.0.0.2/25 vrrp-group 1 preempt hold-time 100
set interfaces irb unit 3 family inet address 10.0.0.2/25 vrrp-group 1 accept-data
set interfaces irb unit 3 family inet6 address fd00::2/64 vrrp-inet6-group 1 virtual-inet6-address fd00::1
set interfaces irb unit 3 family inet6 address fd00::2/64 vrrp-inet6-group 1 priority 110
set interfaces irb unit 3 family inet6 address fd00::2/64 vrrp-inet6-group 1 preempt hold-time 100
set interfaces irb unit 3 family inet6 address fd00::2/64 vrrp-inet6-group 1 accept-data
set protocols router-advertisement interface irb.3 preference high
set protocols router-advertisement interface irb.3 max-advertisement-interval 60
set protocols router-advertisement interface irb.3 managed-configuration
set protocols router-advertisement interface irb.3 other-stateful-configuration
set protocols router-advertisement interface irb.3 solicit-router-advertisement-unicast
set protocols router-advertisement interface irb.3 virtual-router-only
set protocols router-advertisement interface irb.3 default-lifetime 3600
set protocols router-advertisement interface irb.3 dns-server-address fd00:a:b::1
set protocols router-advertisement interface irb.3 prefix fd00::/64 valid-lifetime 3600
set protocols router-advertisement interface irb.3 prefix fd00::/64 preferred-lifetime 3600
set protocols lldp interface all
set bridge-domains BD3 vlan-id 3
set bridge-domains BD3 interface ae0.3
set bridge-domains BD3 interface ae3.3
set bridge-domains BD3 routing-interface irb.3
```
