### Junos Config
```
set groups TELEMETRY-DIAL-OUT services analytics zero-suppression no-zero-suppression
set groups TELEMETRY-DIAL-OUT services analytics streaming-server telemetry-server remote-address 192.168.100.1
set groups TELEMETRY-DIAL-OUT services analytics streaming-server telemetry-server remote-port 50051
set groups TELEMETRY-DIAL-OUT services analytics export-profile export-params local-address 1.1.0.2
set groups TELEMETRY-DIAL-OUT services analytics export-profile export-params local-port 50051
set groups TELEMETRY-DIAL-OUT services analytics export-profile export-params reporting-rate 10
set groups TELEMETRY-DIAL-OUT services analytics export-profile export-params transport udp
set groups TELEMETRY-DIAL-OUT services analytics sensor sensor_1012 server-name telemetry-server
set groups TELEMETRY-DIAL-OUT services analytics sensor sensor_1012 export-name export-params
set groups TELEMETRY-DIAL-OUT services analytics sensor sensor_1012 resource "/interfaces/interface[name='et-0/0/0']/state/counters/"
```

### Troubleshooting
```
# run show agent sensors

Sensor Information :

    Name                                    : sensor_1012
    Resource                                : /interfaces/interface[name='et-0/0/0']/state/counters/
    Version                                 : 1.0
    Sensor-id                               : 562949953421314
    Subscription-ID                         : 562949953421314
    Component(s)                            : fpc0/evoaft-jvisiond-bt,fpc1/evoaft-jvisiond-bt,re0/mgmt-ethd,re0/mib2d,re1/mgmt-ethd

    Server Information :

        Name                                : telemetry-server
        Scope-id                            : 0
        Remote-Address                      : 192.168.100.1
        Remote-port                         : 50051
        Transport-protocol                  : UDP

    Profile Information :

        Name                                : export-params
        Reporting-interval                  : 10
        Payload-size                        : 5000
        Address                             : 1.1.0.2
        Port                                : 50051
        Timestamp                           : ntp
        Format                              : GPB
        DSCP                                : 0
        Forwarding-class                    : 0
```
On the collector:
1. Capture packets
```
# nc -ul 0.0.0.0 50051 >> test1.gpb
```
2. Decode raw data
```
# protoc --decode_raw  < test1.gpb
1: "ptx10004-205-re0"
2: 65534
3: 0
4: "sensor_1012:/interfaces/interface[name=\'et-0/0/0\']/state/counters/:/interfaces/interface[name=\'et-0/0/0\']/state/counters/:re1/mgmt-ethd"
5: 45
6: 1725527212429
7: 1
8: 0
101 {
  2636 {
    99: ""
  }
}
....
```
3. Decode with field names
```
# protoc --decode TelemetryStream port.proto -I /usr/include/protos/junos-telemetry-interface/ -I .  < test1.gpb
system_id: "ptx10004-205-re0:1.1.0.2"
component_id: 1
sub_component_id: 0
sensor_name: "sensor_1012:/interfaces/interface/state/counters/:/interfaces/interface[name=\'et-0/0/0\']/state/counters/:evo-aftmand-bt"
sequence_number: 59
timestamp: 1725527360437
version_major: 1
version_minor: 0
enterprise {
  [juniperNetworks] {
    99: ""
    158 {
      151 {
        51: "ae0"
        52: 1725432653
        151 {
          51: ""
          52: "DOWN"
          53: 0
          151 {
            51: 0
            52: 0
            53: 0
            54: 0
            55: 0
            56: 0
            57: 0
...
```
