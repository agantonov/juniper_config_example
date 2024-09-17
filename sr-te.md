#### Static SR-TE
```
set groups SR-TE protocols source-packet-routing preference 6
set groups SR-TE protocols source-packet-routing maximum-segment-list-depth 8
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 AN1 label 16915
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 TN1 label 16913
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 BN1 label 16911
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 CR1 label 1000001
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 CR3 label 16933
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 CR4 label 16934
set groups SR-TE protocols source-packet-routing segment-list SL-to-AN5 AN5 label 16922
set groups SR-TE protocols source-packet-routing source-routing-path to-BN1 to 1.1.0.1
set groups SR-TE protocols source-packet-routing source-routing-path to-BN1 primary SL-to-BN1
set groups SR-TE protocols source-packet-routing source-routing-path SR-TE-Path-to-AN5 to 2.2.0.2
set groups SR-TE protocols source-packet-routing source-routing-path SR-TE-Path-to-AN5 primary SL-to-AN5
set groups SR-TE protocols source-packet-routing inherit-label-nexthops
```
Show command output:
```
# run show route 2.2.0.2 table inet.3

inet.3: 14 destinations, 30 routes (14 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2.2.0.2/32         *[SPRING-TE/6] 00:02:53, metric 1, metric2 16777215
                    >  to 10.100.0.1 via ae0.0, Push 16922, Push 16934, Push 16933, Push 1000001, Push 16911, Push 16913(top)
                    [RSVP/7/1] 03:58:33, metric 16777215
                    >  to 10.100.0.1 via ae0.0, label-switched-path to-AN5
                    [BGP/170] 03:22:30, localpref 100, from 1.1.0.3
                      AS path: 63000 63536 I, validation-state: unverified
                    >  to 10.100.0.1 via ae0.0, Push 1791, Push 16911, Push 16913(top)
                    [BGP/170] 04:20:15, localpref 100, from 1.1.0.4
                      AS path: 63000 63536 I, validation-state: unverified
                    >  to 10.100.0.1 via ae0.0, Push 345, Push 16912(top)
```
```
# run show spring-traffic-engineering lsp name SR-TE-Path-to-AN5 detail
E = Entropy-label Capability

Name: SR-TE-Path-to-AN5
  Tunnel-source: Static configuration
  Tunnel Forward Type: SRMPLS
  To: 2.2.0.2
  Te-group-id: 0
  State: Up
    Path: SL-to-AN5
    Path Status: NA
    Outgoing interface: NA
    Auto-translate status: Disabled Auto-translate result: N/A
    Compute Status:Disabled , Compute Result:N/A , Compute-Profile Name:N/A
    BFD status: N/A BFD name: N/A
    BFD remote-discriminator: N/A
    Segment ID : 128
    ERO Valid: true
      SR-ERO hop count: 7
        Hop 1 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16915
        Hop 2 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16913
        Hop 3 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16911
        Hop 4 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 1000001
        Hop 5 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16933
        Hop 6 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16934
        Hop 7 (Strict):
          NAI: None
          SID type: 20-bit label, Value: 16922


Total displayed LSPs: 1 (Up: 1, Down: 0, Initializing: 0)
```
#### Inter domain TE link
```
set protocols bgp group GR-eBGP-CR neighbor 10.100.0.17 description CR1
set protocols bgp group GR-eBGP-CR neighbor 10.100.0.17 egress-te-adj-segment BN1-to-CR1 label 1000001
set protocols bgp group GR-eBGP-CR neighbor 10.100.0.17 egress-te-adj-segment BN1-to-CR1 next-hop 10.100.0.17
```
```
# run show route table mpls.0 label 1000001

mpls.0: 298 destinations, 299 routes (298 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1000001            *[BGP-LS-EPE/170] 00:00:17
                    >  to 10.100.0.17 via ae8.0, Pop
1000001(S=0)       *[BGP-LS-EPE/170] 00:00:17
                    >  to 10.100.0.17 via ae8.0, Pop
```
