#### PTX (EVO)
```
set groups IPFIX chassis fpc 0 sampling-instance IPFIX
set groups IPFIX chassis fpc 1 sampling-instance IPFIX
set groups IPFIX services flow-monitoring version-ipfix template IPv4-IPFIX-template flow-active-timeout 30
set groups IPFIX services flow-monitoring version-ipfix template IPv4-IPFIX-template flow-inactive-timeout 60
set groups IPFIX services flow-monitoring version-ipfix template IPv4-IPFIX-template nexthop-learning enable
set groups IPFIX services flow-monitoring version-ipfix template IPv4-IPFIX-template template-refresh-rate seconds 10
set groups IPFIX services flow-monitoring version-ipfix template IPv4-IPFIX-template ipv4-template
set groups IPFIX services flow-monitoring version-ipfix template IPv6-IPFIX-template flow-active-timeout 30
set groups IPFIX services flow-monitoring version-ipfix template IPv6-IPFIX-template flow-inactive-timeout 60
set groups IPFIX services flow-monitoring version-ipfix template IPv6-IPFIX-template nexthop-learning enable
set groups IPFIX services flow-monitoring version-ipfix template IPv6-IPFIX-template ipv6-template
set groups IPFIX interfaces ae0 unit 2 family inet filter input IPFIX-IPv4
set groups IPFIX interfaces ae0 unit 2 family inet6 filter input IPFIX-IPv6
set groups IPFIX forwarding-options sampling instance IPFIX input rate 1000
set groups IPFIX forwarding-options sampling instance IPFIX family inet output flow-server 192.168.100.1 port 2055
set groups IPFIX forwarding-options sampling instance IPFIX family inet output flow-server 192.168.100.1 version-ipfix template IPv4-IPFIX-template
set groups IPFIX forwarding-options sampling instance IPFIX family inet output inline-jflow source-address 1.1.0.1
set groups IPFIX forwarding-options sampling instance IPFIX family inet6 output flow-server 192.168.100.1 port 2055
set groups IPFIX forwarding-options sampling instance IPFIX family inet6 output flow-server 192.168.100.1 version-ipfix template IPv6-IPFIX-template
set groups IPFIX forwarding-options sampling instance IPFIX family inet6 output inline-jflow source-address 1.1.0.1
set groups IPFIX firewall family inet filter IPFIX-IPv4 term 1 then sample
set groups IPFIX firewall family inet filter IPFIX-IPv4 term 1 then accept
set groups IPFIX firewall family inet6 filter IPFIX-IPv6 term 1 then sample
set groups IPFIX firewall family inet6 filter IPFIX-IPv6 term 1 then accept
```
#### nfdump
```
# nfdump -r nfcapd.202408211455 "host 200.1.0.1 or host 3020:1:1:1::1" -A srcip
```
