Enable GRPC service
```
set system services extension-service request-response grpc clear-text port 32767
set system services extension-service request-response grpc max-connections 30
set system services extension-service request-response grpc skip-authentication
```
Enable Netconf and Restconf
```
set system services netconf rfc-compliant
set system services netconf yang-compliant
set system services rest http port 1055
set system services rest enable-explorer
set system schema openconfig unhide
```
Policy to export TE database
```
set policy-options policy-statement traf-eng-all term A from family traffic-engineering
set policy-options policy-statement traf-eng-all term A then accept
```
BGP session with controller
```
set protocols bgp group ns1 type internal
set protocols bgp group ns1 local-address 172.30.202.241
set protocols bgp group ns1 passive
set protocols bgp group ns1 family traffic-engineering unicast
set protocols bgp group ns1 export traf-eng-all
set protocols bgp group ns1 neighbor 172.30.188.152
```
Export TE database to BGP LS
```
set protocols isis traffic-engineering l3-unicast-topology
set protocols isis traffic-engineering advertisement always
set protocols mpls traffic-engineering database import l3-unicast-topology bgp-link-state
set protocols mpls traffic-engineering database import policy traf-eng-all
set protocols mpls traffic-engineering database export policy traf-eng-all
set protocols mpls traffic-engineering database export l3-unicast-topology
```
PCEP
```
set protocols source-packet-routing lsp-external-controller pccd
set protocols pcep disable-multipath-capability
set protocols pcep pce ns1 local-address 172.30.202.241
set protocols pcep pce ns1 destination-ipv4-address 172.30.188.155
set protocols pcep pce ns1 destination-port 4189
set protocols pcep pce ns1 pce-type active
set protocols pcep pce ns1 pce-type stateful
set protocols pcep pce ns1 lsp-provisioning
set protocols pcep pce ns1 p2mp-lsp-report-capability
set protocols pcep pce ns1 p2mp-lsp-update-capability
set protocols pcep pce ns1 p2mp-lsp-init-capability
set protocols pcep pce ns1 lsp-cleanup-timer 10
set protocols pcep pce ns1 spring-capability
set protocols pcep pce ns1 max-sid-depth 16
set protocols pcep pce ns1 delegation-cleanup-timeout 10
```
