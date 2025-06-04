https://www.juniper.net/documentation/us/en/software/junos/flow-monitoring/topics/topic-map/resiliency-exception-reporting.html
https://community.juniper.net/blogs/julian-lucek/2024/01/02/detection-of-blackholes-in-networks-using-jri
https://community.juniper.net/blogs/anton-elita/2024/01/08/packets-lost-in-transit

#### On-box collector
```
set system resiliency exceptions routing
set system resiliency exceptions os
set system resiliency exceptions forwarding
set system resiliency store file jri.log
set system resiliency store file size 10m
set system resiliency store file files 2
set system resiliency store file world-readable
set system resiliency store fwding-file jri-fwd.log
set system resiliency store fwding-file size 10m
set system resiliency store fwding-file files 2
set system resiliency store fwding-file world-readable
```
#### IPFIX Template and Off-box collector
```
set services inline-monitoring template template_1 template-refresh-rate 30
set services inline-monitoring template template_1 option-template-refresh-rate 30
set services inline-monitoring template template_1 template-id 1024
set services inline-monitoring template template_1 primary-data-record-fields cpid-ingress-interface-index
set services inline-monitoring template template_1 primary-data-record-fields cpid-egress-interface-index
set services inline-monitoring template template_1 primary-data-record-fields cpid-forwarding-nexthop-id
set services inline-monitoring template template_1 primary-data-record-fields cpid-forwarding-exception-code
set services inline-monitoring template template_1 primary-data-record-fields cpid-forwarding-class-drop-priority
set services inline-monitoring template template_1 primary-data-record-fields ingress-interface-snmp-id
set services inline-monitoring template template_1 primary-data-record-fields egress-interface-snmp-id
set services inline-monitoring template template_1 primary-data-record-fields direction
set services inline-monitoring template template_1 primary-data-record-fields datalink-frame-size
set services inline-monitoring template template_1 primary-data-record-fields cpid-underlying-ingress-interface-index
set services inline-monitoring instance i1 template-name template_1
set services inline-monitoring instance i1 maximum-clip-length 126
set services inline-monitoring instance i1 collector c1 source-address 192.168.0.1
set services inline-monitoring instance i1 collector c1 destination-address 192.168.0.2
set services inline-monitoring instance i1 collector c1 dscp 21
set services inline-monitoring instance i1 collector c1 destination-port 4739
set services inline-monitoring instance i1 collector c1 routing-instance MANAGEMENT
set services inline-monitoring instance i1 collector localhost source-address 192.168.0.1
set services inline-monitoring instance i1 collector localhost destination-address 192.168.0.1
set services inline-monitoring instance i1 collector localhost destination-port 4739
set services inline-monitoring instance i1 collector localhost routing-instance MANAGEMENT
set services inline-monitoring observation-cloud-id 1
```
#### Subscribe to various exception types and configure exception reporting for a particular PFE and specify the inline-monitoring instance
```
set chassis fpc 0 pfe 0 exception-reporting category forwarding-state inline-monitoring-instance i1
set chassis fpc 0 pfe 0 exception-reporting category firewall inline-monitoring-instance i1
set chassis fpc 0 pfe 0 exception-reporting category layer2 inline-monitoring-instance i1
set chassis fpc 0 pfe 0 exception-reporting category layer3 inline-monitoring-instance i1
set chassis fpc 0 pfe 0 exception-reporting category packet-errors inline-monitoring-instance i1
set chassis fpc 0 pfe 1 exception-reporting category forwarding-state inline-monitoring-instance i1
set chassis fpc 0 pfe 1 exception-reporting category firewall inline-monitoring-instance i1
set chassis fpc 0 pfe 1 exception-reporting category layer2 inline-monitoring-instance i1
set chassis fpc 0 pfe 1 exception-reporting category layer3 inline-monitoring-instance i1
set chassis fpc 0 pfe 1 exception-reporting category packet-errors inline-monitoring-instance i1
```
