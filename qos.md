#### CoS 
```
set class-of-service classifiers dscp DSCP forwarding-class BEST-EFFORT loss-priority high code-points be
set class-of-service classifiers dscp DSCP forwarding-class BEST-EFFORT loss-priority low code-points cs1
set class-of-service classifiers dscp DSCP forwarding-class BEST-EFFORT loss-priority low code-points af11
set class-of-service classifiers dscp DSCP forwarding-class BEST-EFFORT loss-priority low code-points af12
set class-of-service classifiers dscp DSCP forwarding-class BEST-EFFORT loss-priority low code-points af13
set class-of-service classifiers dscp DSCP forwarding-class BUSINESS loss-priority low code-points cs4
set class-of-service classifiers dscp DSCP forwarding-class BUSINESS loss-priority low code-points af41
set class-of-service classifiers dscp DSCP forwarding-class BUSINESS loss-priority low code-points af42
set class-of-service classifiers dscp DSCP forwarding-class BUSINESS loss-priority low code-points af43
set class-of-service classifiers dscp DSCP forwarding-class CONTROL loss-priority low code-points cs6
set class-of-service classifiers dscp DSCP forwarding-class CONTROL loss-priority low code-points cs7
set class-of-service classifiers dscp DSCP forwarding-class MEDIUM loss-priority high code-points cs2
set class-of-service classifiers dscp DSCP forwarding-class MEDIUM loss-priority high code-points af21
set class-of-service classifiers dscp DSCP forwarding-class MEDIUM loss-priority high code-points af22
set class-of-service classifiers dscp DSCP forwarding-class MEDIUM loss-priority high code-points af23
set class-of-service classifiers dscp DSCP forwarding-class REALTIME loss-priority low code-points cs5
set class-of-service classifiers dscp DSCP forwarding-class REALTIME loss-priority low code-points ef
set class-of-service classifiers dscp DSCP forwarding-class SIG-OAM loss-priority low code-points cs3
set class-of-service classifiers dscp DSCP forwarding-class SIG-OAM loss-priority low code-points af31
set class-of-service classifiers dscp DSCP forwarding-class SIG-OAM loss-priority low code-points af32
set class-of-service classifiers dscp DSCP forwarding-class SIG-OAM loss-priority low code-points af33
set class-of-service classifiers exp EXP forwarding-class BEST-EFFORT loss-priority high code-points 000
set class-of-service classifiers exp EXP forwarding-class BEST-EFFORT loss-priority low code-points 001
set class-of-service classifiers exp EXP forwarding-class BUSINESS loss-priority low code-points 100
set class-of-service classifiers exp EXP forwarding-class CONTROL loss-priority low code-points 110
set class-of-service classifiers exp EXP forwarding-class CONTROL loss-priority low code-points 111
set class-of-service classifiers exp EXP forwarding-class MEDIUM loss-priority high code-points 010
set class-of-service classifiers exp EXP forwarding-class REALTIME loss-priority low code-points 101
set class-of-service classifiers exp EXP forwarding-class SIG-OAM loss-priority low code-points 011
set class-of-service classifiers ieee-802.1 8021P forwarding-class BEST-EFFORT loss-priority high code-points 000
set class-of-service classifiers ieee-802.1 8021P forwarding-class BEST-EFFORT loss-priority low code-points 001
set class-of-service classifiers ieee-802.1 8021P forwarding-class BUSINESS loss-priority low code-points 100
set class-of-service classifiers ieee-802.1 8021P forwarding-class CONTROL loss-priority low code-points 110
set class-of-service classifiers ieee-802.1 8021P forwarding-class CONTROL loss-priority low code-points 111
set class-of-service classifiers ieee-802.1 8021P forwarding-class MEDIUM loss-priority high code-points 010
set class-of-service classifiers ieee-802.1 8021P forwarding-class REALTIME loss-priority low code-points 101
set class-of-service classifiers ieee-802.1 8021P forwarding-class SIG-OAM loss-priority low code-points 011
set class-of-service forwarding-classes class BEST-EFFORT queue-num 0
set class-of-service forwarding-classes class BUSINESS queue-num 5
set class-of-service forwarding-classes class CONTROL queue-num 4
set class-of-service forwarding-classes class MEDIUM queue-num 1
set class-of-service forwarding-classes class REALTIME queue-num 2
set class-of-service forwarding-classes class SIG-OAM queue-num 3
set class-of-service traffic-control-profiles 10GBPS_UNTRUSTED_TCP shaping-rate 10g
set class-of-service traffic-control-profiles 10M_TCP shaping-rate 10m
set class-of-service traffic-control-profiles 5GBPS_UNTRUSTED_TCP shaping-rate 5g
set class-of-service interfaces et-0/0/37 output-traffic-control-profile 5GBPS_UNTRUSTED_TCP
set class-of-service interfaces et-0/0/37 unit * output-traffic-control-profile 10M_TCP
deactivate class-of-service interfaces et-0/0/37 unit * output-traffic-control-profile
deactivate class-of-service interfaces et-0/0/37
set class-of-service interfaces ae100 scheduler-map SCHEDULER
set class-of-service interfaces ae100 shaping-rate 100m
deactivate class-of-service interfaces ae100
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class BEST-EFFORT loss-priority high code-point be
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class BEST-EFFORT loss-priority low code-point cs1
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class BUSINESS loss-priority low code-point cs5
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class CONTROL loss-priority low code-point cs6
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class MEDIUM loss-priority high code-point cs2
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class REALTIME loss-priority low code-point ef
set class-of-service rewrite-rules dscp DSCP-REWRITE forwarding-class SIG-OAM loss-priority low code-point cs3
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class BEST-EFFORT loss-priority high code-point 000
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class BEST-EFFORT loss-priority low code-point 001
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class BUSINESS loss-priority low code-point 100
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class CONTROL loss-priority low code-point 111
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class MEDIUM loss-priority high code-point 010
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class REALTIME loss-priority low code-point 101
set class-of-service rewrite-rules exp EXP-REWRITE forwarding-class SIG-OAM loss-priority low code-point 011
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class BEST-EFFORT loss-priority high code-point 000
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class BEST-EFFORT loss-priority low code-point 001
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class BUSINESS loss-priority low code-point 100
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class CONTROL loss-priority low code-point 111
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class MEDIUM loss-priority high code-point 010
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class REALTIME loss-priority low code-point 101
set class-of-service rewrite-rules ieee-802.1 8021P-REWRITE forwarding-class SIG-OAM loss-priority low code-point 011
set class-of-service scheduler-maps SCHEDULER forwarding-class BEST-EFFORT scheduler BEST-EFFORT-SC
set class-of-service scheduler-maps SCHEDULER forwarding-class BUSINESS scheduler BUSINESS-SC
set class-of-service scheduler-maps SCHEDULER forwarding-class CONTROL scheduler CONTROL-SC
set class-of-service scheduler-maps SCHEDULER forwarding-class MEDIUM scheduler MEDIUM-SC
set class-of-service scheduler-maps SCHEDULER forwarding-class REALTIME scheduler REALTIME-SC
set class-of-service scheduler-maps SCHEDULER forwarding-class SIG-OAM scheduler SIG-OAM-SC
set class-of-service schedulers BEST-EFFORT-SC transmit-rate remainder
set class-of-service schedulers BEST-EFFORT-SC buffer-size remainder
set class-of-service schedulers BEST-EFFORT-SC priority low
set class-of-service schedulers BUSINESS-SC transmit-rate percent 20
set class-of-service schedulers BUSINESS-SC buffer-size percent 20
set class-of-service schedulers BUSINESS-SC priority low
set class-of-service schedulers CONTROL-SC transmit-rate percent 5
set class-of-service schedulers CONTROL-SC buffer-size percent 2
set class-of-service schedulers CONTROL-SC priority low
set class-of-service schedulers MEDIUM-SC transmit-rate percent 20
set class-of-service schedulers MEDIUM-SC buffer-size percent 20
set class-of-service schedulers MEDIUM-SC priority low
set class-of-service schedulers REALTIME-SC shaping-rate percent 40
set class-of-service schedulers REALTIME-SC buffer-size percent 30
set class-of-service schedulers REALTIME-SC priority strict-high
set class-of-service schedulers SIG-OAM-SC transmit-rate percent 5
set class-of-service schedulers SIG-OAM-SC buffer-size percent 2
set class-of-service schedulers SIG-OAM-SC priority low
```
### Heirarchical Policer
```
set firewall family inet filter H-Pol-Inet interface-specific
set firewall family inet filter H-Pol-Inet term platinum from dscp af11
set firewall family inet filter H-Pol-Inet term platinum from dscp cs6
set firewall family inet filter H-Pol-Inet term platinum then enhanced-hierarchical-policer H-Pol
set firewall family inet filter H-Pol-Inet term platinum then enhanced-hierarchical-policer traffic-priority high
set firewall family inet filter H-Pol-Inet term gold from dscp af12
set firewall family inet filter H-Pol-Inet term gold then enhanced-hierarchical-policer H-Pol
set firewall family inet filter H-Pol-Inet term gold then enhanced-hierarchical-policer traffic-priority medium-high
set firewall family inet filter H-Pol-Inet term silver from dscp af13
set firewall family inet filter H-Pol-Inet term silver then enhanced-hierarchical-policer H-Pol
set firewall family inet filter H-Pol-Inet term silver then enhanced-hierarchical-policer traffic-priority medium-low
set firewall family inet filter H-Pol-Inet term dflt then enhanced-hierarchical-policer H-Pol
set firewall family inet filter H-Pol-Inet term dflt then enhanced-hierarchical-policer traffic-priority low
set firewall enhanced-hierarchical-policer H-Pol filter-specific
set firewall enhanced-hierarchical-policer H-Pol high committed-burst-size 5k
set firewall enhanced-hierarchical-policer H-Pol high committed-information-rate 5m
set firewall enhanced-hierarchical-policer H-Pol high max-committed-information-rate 5m
set firewall enhanced-hierarchical-policer H-Pol high then discard
set firewall enhanced-hierarchical-policer H-Pol medium-high committed-burst-size 15k
set firewall enhanced-hierarchical-policer H-Pol medium-high committed-information-rate 10m
set firewall enhanced-hierarchical-policer H-Pol medium-high max-committed-information-rate 15m
set firewall enhanced-hierarchical-policer H-Pol medium-high then discard
set firewall enhanced-hierarchical-policer H-Pol medium-low committed-burst-size 35k
set firewall enhanced-hierarchical-policer H-Pol medium-low committed-information-rate 20m
set firewall enhanced-hierarchical-policer H-Pol medium-low max-committed-information-rate 35m
set firewall enhanced-hierarchical-policer H-Pol medium-low then discard
set firewall enhanced-hierarchical-policer H-Pol low committed-burst-size 65k
set firewall enhanced-hierarchical-policer H-Pol low committed-information-rate 30m
set firewall enhanced-hierarchical-policer H-Pol low max-committed-information-rate 65m
set firewall enhanced-hierarchical-policer H-Pol low then discard
set interfaces et-0/0/37 hierarchical-scheduler
set interfaces et-0/0/37 unit 2000 family inet filter input H-Pol-Inet
set interfaces et-0/0/37 unit 2000 family inet filter output H-Pol-Inet
```
### L2 Policer
```
set groups EVPN interfaces et-0/0/50 ether-options 802.3ad ae100
set groups EVPN interfaces ae100 encapsulation ethernet-bridge
set groups EVPN interfaces ae100 esi 00:11:44:00:00:00:00:00:01:00
set groups EVPN interfaces ae100 esi single-active
set groups EVPN interfaces ae100 esi df-election-granularity per-esi lacp-oos-on-ndf
set groups EVPN interfaces ae100 esi df-election-type preference value 200
set groups EVPN interfaces ae100 aggregated-ether-options lacp active
set groups EVPN interfaces ae100 aggregated-ether-options lacp periodic fast
set groups EVPN interfaces ae100 aggregated-ether-options lacp system-id 00:11:44:00:00:01
set groups EVPN interfaces ae100 unit 0 family ethernet-switching filter input POLICE_100M_ES
set groups EVPN interfaces ae100 unit 0 family ethernet-switching filter output POLICE_100M_ES
set groups EVPN interfaces ae100 unit 0 etree-ac-role leaf
set groups EVPN interfaces et-0/0/37 unit 100 encapsulation vlan-bridge
set groups EVPN interfaces et-0/0/37 unit 100 vlan-id-list 101-210
set groups EVPN interfaces et-0/0/37 unit 100 family ethernet-switching filter input POLICE_100M_ES
set groups EVPN interfaces et-0/0/37 unit 100 family ethernet-switching filter output POLICE_100M_ES
set groups EVPN interfaces et-0/0/37 unit 100 etree-ac-role leaf
set groups EVPN firewall family ethernet-switching filter POLICE_100M_ES interface-specific
set groups EVPN firewall family ethernet-switching filter POLICE_100M_ES term ALLOW_LACP from ether-type 0x8809
set groups EVPN firewall family ethernet-switching filter POLICE_100M_ES term ALLOW_LACP then accept
set groups EVPN firewall family ethernet-switching filter POLICE_100M_ES term POLICE then accept
set groups EVPN firewall family ethernet-switching filter POLICE_100M_ES term POLICE then policer POLICE_100M
```
