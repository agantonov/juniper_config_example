```
set protocols vrrp version-3
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 vlan-id 500
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 virtual-address 192.168.201.1
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 priority 200
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 fast-interval 50
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 preempt hold-time 120
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 accept-data
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 track interface ae7.0 priority-cost 51
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 track interface ae5.0 priority-cost 51
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet address 192.168.201.2/29 vrrp-group 0 track route 192.168.210.0/29 routing-instance L3VPN_Hub priority-cost 51
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 virtual-inet6-address 2001::192:168:201:1
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 priority 200
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 fast-interval 50
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 preempt hold-time 120
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 accept-data
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 track interface ae7.0 priority-cost 51
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 track interface ae5.0 priority-cost 51
set groups L3VPN-H-and-S interfaces xe-1/0/5 unit 500 family inet6 address 2001::192:168:201:2/120 vrrp-inet6-group 0 track route 2001::192:168:210:0/120 routing-instance L3VPN_Hub priority-cost 51
```
