#### Interface Statistics
OID: ````1.3.6.1.4.1.2636.3.3```` 
MIB Path: ````/iso/org/dod/internet/private/enterprises/juniperMIB/jnxMibs/ifJnx````
```
show snmp mib walk ifJnx
```
Telemetry Sensor: ````/interfaces/interface````

#### Box Anatomy (CPU, Memory, Tempepature, FRU, etc)
OID: ````1.3.6.1.4.1.2636.3.1````
MIB Path: ````/iso/org/dod/internet/private/enterprises/juniperMIB/jnxMibs/jnxBoxAnatomy````
```
show snmp mib walk jnxBoxAnatomy
```
Telemetry sensor: ````/components/component````

#### CoS
OID: ````1.3.6.1.4.1.2636.3.15````
MIB Path: ````/iso/org/dod/internet/private/enterprises/juniperMIB/jnxMibs/jnxCos````
```
show snmp mib walk jnxCos
```
Telemetry sensor: ````/qos````

#### PSU
OID: ````1.3.6.1.4.1.2636.3.58````
MIB Path: ````/iso/org/dod/internet/private/enterprises/juniperMIB/jnxMibs/jnxPsuMIBRoot````
```
show snmp mib walk jnxPsuMIBRoot
```
#### BGP
OID: ````1.3.6.1.4.1.2636.5.1````
MIB Path: ````/iso/org/dod/internet/private/enterprises/juniperMIB/jnxExperiment/jnxBgpM2Experiment````

OID: ````1.3.6.1.2.1.15````
MIB Path: ````/iso/org/dod/internet/mgmt/mib-2/bgp````
```
show snmp mib walk jnxBgpM2Experiment
show snmp mib walk bgp
```
Telemetry sensor: ````/bgp-rib````

#### Fabric Statistics
Telemetry sensor: ````/junos/fabric-statistics````
