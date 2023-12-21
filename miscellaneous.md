Routing options
```
set routing-options router-id 1.1.0.2
set routing-options autonomous-system 65100
set routing-options forwarding-table export LB
set routing-options forwarding-table dynamic-list-next-hop
set routing-options forwarding-table evpn-egress-link-protection
set routing-options forwarding-table chained-composite-next-hop ingress evpn
set routing-options forwarding-table chained-composite-next-hop ingress l3vpn
set routing-options multicast stream-protection
```
Load balance policy
```
set policy-options policy-statement LB then load-balance per-flow
set policy-options policy-statement LB then accept
```
Forwading options (ACX)
```
set forwarding-options hash-key family inet layer-3
set forwarding-options hash-key family inet layer-4
set forwarding-options hash-key family inet6 layer-3
set forwarding-options hash-key family inet6 layer-4
set forwarding-options hash-key family mpls all-labels
set forwarding-options hash-key family mpls payload ether-pseudowire
set forwarding-options hash-key family mpls payload ip
```
System
```
set system syslog user * any emergency
set system syslog file messages any notice
set system syslog file messages authorization info
set system syslog time-format millisecond
set system services ssh client-alive-interval 120
set system services ftp
set system services telnet
set system services xnm-clear-text
set system services netconf ssh
set system services web-management http
set system domain-name <domain_name>
set system time-zone Europe/Amsterdam
set system authentication-order radius
set system ports console log-out-on-disconnect
set system name-server <name_server>
set system radius-server <radius_server> secret "****"
set system radius-server <radius_server> retry 3
set system compress-configuration-files
set system ddos-protection protocols resolve aggregate bandwidth 100000
set system ddos-protection protocols resolve aggregate burst 100000
set system ddos-protection protocols igmp aggregate bandwidth 100000
set system ddos-protection protocols igmp aggregate burst 100000
set system ntp server <ntp_server>
```
