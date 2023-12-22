Define flexible algorithm on routers that you have identified in your network. Assign an ID for the flexible algorithm definition (FAD) ranging from 128 through 255.
Map a BGP color community to the defined FAD. By default each flexible algorithm is associated with a value equal to the flex algorithm. Define the admin groups.
```
set policy-options community blue members color:1:129
set policy-options community red members color:0:128
set routing-options flex-algorithm 128 definition metric-type igp-metric
set routing-options flex-algorithm 128 definition spf
set routing-options flex-algorithm 128 definition admin-group include-any RED
set routing-options flex-algorithm 128 color 228
set routing-options flex-algorithm 129 definition metric-type igp-metric
set routing-options flex-algorithm 129 definition spf
set routing-options flex-algorithm 129 definition admin-group include-any BLUE
set routing-options flex-algorithm 129 color 229
```
Advertise prefix segments through policy configuration
```
set policy-options policy-statement FLEX-ALGO from route-filter 1.1.0.5/32 exact
set policy-options policy-statement FLEX-ALGO then prefix-segment algorithm 128 index 1005
set policy-options policy-statement FLEX-ALGO then prefix-segment algorithm 128 node-segment
set policy-options policy-statement FLEX-ALGO then prefix-segment algorithm 129 index 1105
set policy-options policy-statement FLEX-ALGO then prefix-segment algorithm 129 node-segment
set policy-options policy-statement FLEX-ALGO then prefix-segment index 5
set policy-options policy-statement FLEX-ALGO then prefix-segment node-segment
set policy-options policy-statement FLEX-ALGO then accept
```
Identify the participating routers and configure participation on those routers
```
set protocols isis source-packet-routing flex-algorithm 128
set protocols isis source-packet-routing flex-algorithm 129
set protocols isis traffic-engineering advertisement always
set protocols isis export FLEX-ALGO
```
Configure admin-groups
```
set protocols mpls admin-groups RED 0
set protocols mpls admin-groups BLUE 1
set protocols mpls interface ae4.0 admin-group RED
set protocols mpls interface ae6.0 admin-group RED
set protocols mpls interface ae8.0 admin-group RED
set protocols mpls interface ae9.0 admin-group RED
set protocols mpls interface ae10.0 admin-group RED
set protocols mpls interface ae11.0 admin-group RED
set protocols mpls interface ae31.0 admin-group RED
set protocols mpls interface ae31.0 admin-group BLUE
```

Show commands

ISIS Database
```
# run show isis database extensive | match ALGO
      Node SID, Flags: 0x40(R:0,N:1,P:0,E:0,V:0,L:0), Algo: SPF(0), Value: 5
      Node SID, Flags: 0x40(R:0,N:1,P:0,E:0,V:0,L:0), Algo: Flex-Algo(129), Value: 1105
      Node SID, Flags: 0x40(R:0,N:1,P:0,E:0,V:0,L:0), Algo: Flex-Algo(128), Value: 1005
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: SPF(0), Value: 3
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: Flex-Algo(129), Value: 1103
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: Flex-Algo(128), Value: 1003
      Flex-Algo metric: 15, Algorithm: 129
      Flex-Algo metric: 10, Algorithm: 128
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: SPF(0), Value: 4
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: Flex-Algo(129), Value: 1104
      Node SID, Flags: 0xe0(R:1,N:1,P:1,E:0,V:0,L:0), Algo: Flex-Algo(128), Value: 1004
      Flex-Algo metric: 25, Algorithm: 129
      Flex-Algo metric: 10, Algorithm: 128
```
Inetcolor.0
```
# run show route table inetcolor.0

inetcolor.0: 17 destinations, 17 routes (17 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.0.1-228<c>/64
                   *[L-ISIS/14] 1d 01:45:25, metric 20
                    >  to 10.100.0.9 via ae4.0, Push 17001
                       to 10.100.0.1 via ae6.0, Push 17001
1.1.0.1-229<c>/64
                   *[L-ISIS/14] 1d 01:45:25, metric 25
                    >  to 10.100.0.37 via ae31.0, Push 17101
1.1.0.3-228<c>/64
                   *[L-ISIS/14] 1d 01:45:25, metric 10
                    >  to 10.100.0.9 via ae4.0
                       to 10.100.0.1 via ae6.0, Push 17003
1.1.0.3-229<c>/64
                   *[L-ISIS/14] 1d 01:45:25, metric 15
                    >  to 10.100.0.37 via ae31.0, Push 17103
```
Inet6color.0
```
# run show route table inet6color.0

inet6color.0: 17 destinations, 17 routes (17 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

::ffff:1.1.0.1-228<c6>/160
                   *[L-ISIS/14] 2d 19:44:31, metric 20
                    >  to 10.100.0.9 via ae4.0, Push 17001
                       to 10.100.0.1 via ae6.0, Push 17001
::ffff:1.1.0.1-229<c6>/160
                   *[L-ISIS/14] 2d 19:44:31, metric 25
                    >  to 10.100.0.37 via ae31.0, Push 17101
::ffff:1.1.0.3-228<c6>/160
                   *[L-ISIS/14] 1d 01:46:33, metric 10
                    >  to 10.100.0.9 via ae4.0
                       to 10.100.0.1 via ae6.0, Push 17003
::ffff:1.1.0.3-229<c6>/160
                   *[L-ISIS/14] 2d 19:48:13, metric 15
                    >  to 10.100.0.37 via ae31.0, Push 17103
```
