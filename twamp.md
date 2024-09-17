#### ACX (EVO)
Client
```
set groups TWAMP services monitoring twamp client control-connection C1 target 2.2.0.1
set groups TWAMP services monitoring twamp client control-connection C1 source-address 1.1.0.7
set groups TWAMP services monitoring twamp client control-connection C1 destination-port 862
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 target 2.2.0.1
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 source-address 1.1.0.7
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 data-size 100
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 probe-count 10
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 probe-interval 1
set groups TWAMP services monitoring twamp client control-connection C1 test-session TEST1 history-size 30
```
Server
```
set groups TWAMP services monitoring twamp server managed port 862
set groups TWAMP services monitoring twamp server managed client-list address 1.1.0.7/32
```
##### Show commands
Client
```
# run show services monitoring twamp client test-info
Control                Test                   Client                Server                Test
name                   name                   address:port          address:port          status
C1                     TEST1                  1.1.0.7:58053         2.2.0.1:10002         active
```
```
# run show services monitoring twamp client control-info
Control                Client                Server                Active   Control       Auth
name                   address:port          address:port          tests    status        mode
C1                     1.1.0.7:41194         2.2.0.1:862           1        testing       none
```
```
# run show services monitoring twamp client probe-results
Owner: C1, Test: TEST1
Target address: 2.2.0.1, Source address: 1.1.0.7, Probe type: twamp, Test size: 10
  Probe results:
    Probe response received
    Probe sent time: 09/17/24 03:01:40.533734
    Probe rcvd time: 09/17/24 03:01:40.534473, Client and server offload timestamping
    Rtt: 552 usec, Rtt jitter: 12 usec
    Egress jitter: 39 usec, Ingress jitter: 27 usec
  Results over current test:
    Probes sent: 5, Probes received: 5, Loss percentage: 0.00
    Measurement: Round trip time (usec)
      Samples: 5, Minimum: 508, Maximum: 564, Average: 541, Stddev: 31
    Measurement: Round trip jitter (usec)
      Samples: 4, Minimum: 4, Maximum: 56, Average: 23, Stddev: 19
    Measurement: Egress delay (usec)
      Samples: 5, Minimum: 165, Maximum: 205, Average: 178, Stddev: 20
```
```
# run show services monitoring twamp client history-results detail control-connection C1
Owner: C1, Test: TEST1, Probe type: twamp
  Probe results:
    Probe response received
    Probe sent time: 09/17/24 03:03:26.606525
    Probe rcvd time: 09/17/24 03:03:26.607216, Client and server offload timestamping
    Rtt: 531 usec, Rtt jitter: 0 usec
    Egress jitter: 0 usec, Ingress jitter: 0 usec
  Results over current test:
    Probes sent: 1, Probes received: 1, Loss percentage: 0.00
    Measurement: Round trip time (usec)
      Samples: 1, Minimum: 531, Maximum: 531, Average: 531, Stddev: 0
    Measurement: Egress delay (usec)
      Samples: 1, Minimum: 181, Maximum: 181, Average: 181, Stddev: 0
    Measurement: Ingress delay (usec)
      Samples: 1, Minimum: 350, Maximum: 350, Average: 350, Stddev: 0
```
Server
```
# run show services monitoring twamp server control-info
Control                Client                Server                Active   Control       Auth
name                   address:port          address:port          tests    status        mode
301                    1.1.0.7:41194         2.2.0.1:862           1        testing       none

[edit]
# run show services monitoring twamp server test-info
Control                Test                   Client                Server                Test
identifier             identifier             address:port          address:port          status
301                    513                    1.1.0.7:58053         2.2.0.1:10002         active
```
