#### VPLS-only PE
```
set interfaces ae83 unit 4010 encapsulation vlan-vpls
set interfaces ae83 unit 4010 vlan-id 4010
set interfaces ae83 unit 4010 family vpls
set routing-instances vpls_4010 instance-type vpls
set routing-instances vpls_4010 protocols vpls interface ae83.4010
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 pseudowire-status-tlv hot-standby-vc-on
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 switchover-delay 0
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 revert-time 30
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 backup-neighbor 1.1.0.2 psn-tunnel-endpoint 1.1.0.2
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 backup-neighbor 1.1.0.2 hot-standby
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 oam bfd-liveness-detection minimum-interval 100
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.1 oam bfd-liveness-detection multiplier 3
set routing-instances vpls_4010 protocols vpls encapsulation-type ethernet-vlan
set routing-instances vpls_4010 protocols vpls no-tunnel-services
set routing-instances vpls_4010 protocols vpls vpls-id 4010
set routing-instances vpls_4010 interface ae83.4010
```
#### EVPN-only PE
```
set interfaces ae19 unit 4010 encapsulation vlan-bridge
set interfaces ae19 unit 4010 vlan-id 4010
set routing-instances evpn_elan_4010 instance-type mac-vrf
set routing-instances evpn_elan_4010 protocols evpn encapsulation mpls
set routing-instances evpn_elan_4010 protocols evpn no-control-word
set routing-instances evpn_elan_4010 service-type vlan-based
set routing-instances evpn_elan_4010 route-distinguisher 1.1.0.9:4010
set routing-instances evpn_elan_4010 vrf-target target:65100:40104010
set routing-instances evpn_elan_4010 vlans bd4010 vlan-id 4010
set routing-instances evpn_elan_4010 vlans bd4010 interface ae19.4010
```
#### EVPN-VPLS PE (active)
```
set interfaces lt-0/2/3 unit 0 encapsulation vlan-bridge
set interfaces lt-0/2/3 unit 0 vlan-id 4010
set interfaces lt-0/2/3 unit 0 peer-unit 1
set interfaces lt-0/2/3 unit 1 encapsulation vlan-vpls
set interfaces lt-0/2/3 unit 1 vlan-id 4010
set interfaces lt-0/2/3 unit 1 peer-unit 0
set routing-instances evpn_elan_4010 instance-type evpn
set routing-instances evpn_elan_4010 protocols evpn
set routing-instances evpn_elan_4010 vlan-id none
set routing-instances evpn_elan_4010 no-normalization
set routing-instances evpn_elan_4010 interface lt-0/2/3.0
set routing-instances evpn_elan_4010 route-distinguisher 1.1.0.1:4010
set routing-instances evpn_elan_4010 vrf-target target:65100:40104010
set routing-instances vpls_4010 instance-type vpls
set routing-instances vpls_4010 protocols vpls interface lt-0/2/3.1
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 pseudowire-status-tlv hot-standby-vc-on
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 switchover-delay 0
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 oam bfd-liveness-detection minimum-interval 100
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 oam bfd-liveness-detection multiplier 3
set routing-instances vpls_4010 protocols vpls encapsulation-type ethernet-vlan
set routing-instances vpls_4010 protocols vpls no-tunnel-services
set routing-instances vpls_4010 protocols vpls vpls-id 4010
set routing-instances vpls_4010 interface lt-0/2/3.1
```
#### EVPN-VPLS PE (standby)
```
set interfaces lt-0/2/3 unit 0 encapsulation vlan-bridge
set interfaces lt-0/2/3 unit 0 vlan-id 4010
set interfaces lt-0/2/3 unit 0 peer-unit 1
set interfaces lt-0/2/3 unit 1 encapsulation vlan-vpls
set interfaces lt-0/2/3 unit 1 vlan-id 4010
set interfaces lt-0/2/3 unit 1 peer-unit 0
set routing-instances evpn_elan_4010 instance-type evpn
set routing-instances evpn_elan_4010 protocols evpn
set routing-instances evpn_elan_4010 vlan-id none
set routing-instances evpn_elan_4010 no-normalization
set routing-instances evpn_elan_4010 interface lt-0/2/3.0
set routing-instances evpn_elan_4010 route-distinguisher 1.1.0.2:4010
set routing-instances evpn_elan_4010 vrf-target target:65100:40104010
set routing-instances vpls_4010 instance-type vpls
set routing-instances vpls_4010 protocols vpls interface lt-0/2/3.1
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 pseudowire-status-tlv hot-standby-vc-on
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 switchover-delay 0
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 oam bfd-liveness-detection minimum-interval 100
set routing-instances vpls_4010 protocols vpls neighbor 1.1.0.11 oam bfd-liveness-detection multiplier 3
set routing-instances vpls_4010 protocols vpls encapsulation-type ethernet-vlan
set routing-instances vpls_4010 protocols vpls no-tunnel-services
set routing-instances vpls_4010 protocols vpls vpls-id 4010
set routing-instances vpls_4010 interface lt-0/2/3.1
```
### Show commands

#### VPLS-only PE
```
# run show vpls connections
Layer-2 VPN connections:

Legend for connection status (St)
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present
CM -- control-word mismatch      -> -- only outbound connection is up
CN -- circuit not provisioned    <- -- only inbound connection is up
OR -- out of range               Up -- operational
OL -- no outgoing label          Dn -- down
LD -- local site signaled down   CF -- call admission control failure
RD -- remote site signaled down  SC -- local and remote site ID collision
LN -- local site not designated  LM -- local site ID not minimum designated
RN -- remote site not designated RM -- remote site ID not minimum designated
XX -- unknown connection status  IL -- no incoming label
MM -- MTU mismatch               MI -- Mesh-Group ID not available
BK -- Backup connection	         ST -- Standby connection
PF -- Profile parse failure      PB -- Profile busy
RS -- remote site standby	 SN -- Static Neighbor
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch           HS -- Hot-standby Connection

Legend for interface status
Up -- operational
Dn -- down

Instance: vpls_4010
  VPLS-id: 4010
    Neighbor                  Type  St     Time last up          # Up trans
    1.1.0.1(vpls-id 4010)     rmt   Up     Dec 19 11:37:07 2023           1
      Remote PE: 1.1.0.1, Negotiated control-word: No
      Incoming label: 1553, Outgoing label: 158017
      Negotiated PW status TLV: Yes
      local PW status code: 0x00000000, Neighbor PW status code: 0x00000000
      Local interface: lsi.1056010, Status: Up, Encapsulation: VLAN
        Description: Intf - vpls vpls_4010 neighbor 1.1.0.1 vpls-id 4010
      Flow Label Transmit: No, Flow Label Receive: No
    1.1.0.2(vpls-id 4010)     rmt   HS     -----                       ----
      Remote PE: 1.1.0.2, Negotiated control-word: No
      Incoming label: 1553, Outgoing label: 186710
      Negotiated PW status TLV: Yes
      local PW status code: 0x00000020, Neighbor PW status code: 0x00000000
      Local interface: lsi.1056010, Status: Up, Encapsulation: VLAN
        Description: Intf - vpls vpls_4010 neighbor 1.1.0.1 vpls-id 4010
      Flow Label Transmit: No, Flow Label Receive: No

# run show vpls mac-table

MAC flags       (S -static MAC, D -dynamic MAC, L -locally learned, C -Control MAC
    O -OVSDB MAC, SE -Statistics enabled, NM -Non configured MAC, R -Remote PE MAC, P -Pinned MAC)

Routing instance : vpls_4010
 Bridging domain : __vpls_4010__, VLAN : NA
   MAC                 MAC      Logical          NH     MAC         active
   address             flags    interface        Index  property    source
   00:31:01:00:00:01   D        ae83.4010
   00:32:01:00:00:01   D        lsi.1056010
```
#### EVPN-only PE
```
# run show mac-vrf forwarding mac-table instance evpn_elan_4010

MAC flags (S - static MAC, D - dynamic MAC, L - locally learned, P - Persistent static, C - Control MAC
           SE - statistics enabled, NM - non configured MAC, R - remote PE MAC, O - ovsdb MAC
           GBP - group based policy, B - Blocked MAC)


Ethernet switching table : 200 entries, 200 learned
Routing instance : evpn_elan_4010
    Vlan                MAC                 MAC         Age   GBP     Logical                NH        RTR
    name                address             flags             Tag     interface              Index     ID
    bd4010              00:31:01:00:00:01   DC            -                                   745200    745200
    bd4010              00:32:01:00:00:01   D             -            ae19.4010              0         0
```
#### EVPN-VPLS PE (active)
```
# run show vpls connections
Layer-2 VPN connections:

Legend for connection status (St)
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present
CM -- control-word mismatch      -> -- only outbound connection is up
CN -- circuit not provisioned    <- -- only inbound connection is up
OR -- out of range               Up -- operational
OL -- no outgoing label          Dn -- down
LD -- local site signaled down   CF -- call admission control failure
RD -- remote site signaled down  SC -- local and remote site ID collision
LN -- local site not designated  LM -- local site ID not minimum designated
RN -- remote site not designated RM -- remote site ID not minimum designated
XX -- unknown connection status  IL -- no incoming label
MM -- MTU mismatch               MI -- Mesh-Group ID not available
BK -- Backup connection	         ST -- Standby connection
PF -- Profile parse failure      PB -- Profile busy
RS -- remote site standby	 SN -- Static Neighbor
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch           HS -- Hot-standby Connection

Legend for interface status
Up -- operational
Dn -- down

Instance: vpls_4010
  VPLS-id: 4010
    Neighbor                  Type  St     Time last up          # Up trans
    1.1.0.11(vpls-id 4010)    rmt   Up     Dec 19 11:37:07 2023           1
      Remote PE: 1.1.0.11, Negotiated control-word: No
      Incoming label: 158017, Outgoing label: 1553
      Negotiated PW status TLV: Yes
      local PW status code: 0x00000000, Neighbor PW status code: 0x00000000
      Local interface: lsi.1055744, Status: Up, Encapsulation: VLAN
        Description: Intf - vpls vpls_4010 neighbor 1.1.0.11 vpls-id 4010
      Flow Label Transmit: No, Flow Label Receive: No

# run show vpls mac-table

MAC flags       (S -static MAC, D -dynamic MAC, L -locally learned, C -Control MAC
    O -OVSDB MAC, SE -Statistics enabled, NM -Non configured MAC, R -Remote PE MAC, P -Pinned MAC)

Routing instance : vpls_4010
 Bridging domain : __vpls_4010__, VLAN : NA
   MAC                 MAC      Logical          NH     MAC         active
   address             flags    interface        Index  property    source
   00:31:01:00:00:01   D        lsi.1055744
   00:32:01:00:00:01   D        lt-0/2/3.1

# run show evpn mac-table instance evpn_elan_4010

MAC flags       (S -static MAC, D -dynamic MAC, L -locally learned, C -Control MAC
    O -OVSDB MAC, SE -Statistics enabled, NM -Non configured MAC, R -Remote PE MAC, P -Pinned MAC)

Routing instance : evpn_elan_4010
 Bridging domain : __evpn_elan_4010__, VLAN : none
   MAC                 MAC      Logical          NH     MAC         active
   address             flags    interface        Index  property    source
   00:31:01:00:00:01   D        lt-0/2/3.0
   00:32:01:00:00:01   DC                        1062377            00:02:03:01:00:00:00:00:19:00
```
#### EVPN-VPLS PE (standby)
```
# run show vpls connections
Layer-2 VPN connections:

Legend for connection status (St)
EI -- encapsulation invalid      NC -- interface encapsulation not CCC/TCC/VPLS
EM -- encapsulation mismatch     WE -- interface and instance encaps not same
VC-Dn -- Virtual circuit down    NP -- interface hardware not present
CM -- control-word mismatch      -> -- only outbound connection is up
CN -- circuit not provisioned    <- -- only inbound connection is up
OR -- out of range               Up -- operational
OL -- no outgoing label          Dn -- down
LD -- local site signaled down   CF -- call admission control failure
RD -- remote site signaled down  SC -- local and remote site ID collision
LN -- local site not designated  LM -- local site ID not minimum designated
RN -- remote site not designated RM -- remote site ID not minimum designated
XX -- unknown connection status  IL -- no incoming label
MM -- MTU mismatch               MI -- Mesh-Group ID not available
BK -- Backup connection          ST -- Standby connection
PF -- Profile parse failure      PB -- Profile busy
RS -- remote site standby	 SN -- Static Neighbor
LB -- Local site not best-site   RB -- Remote site not best-site
VM -- VLAN ID mismatch           HS -- Hot-standby Connection

Legend for interface status
Up -- operational
Dn -- down

Instance: vpls_4010
  VPLS-id: 4010
    Neighbor                  Type  St     Time last up          # Up trans
    1.1.0.11(vpls-id 4010)    rmt   Up     Dec 19 11:37:09 2023           1
      Remote PE: 1.1.0.11, Negotiated control-word: No
      Incoming label: 186710, Outgoing label: 1553
      Negotiated PW status TLV: Yes
      local PW status code: 0x00000000, Neighbor PW status code: 0x00000020
      Local interface: lsi.1053696, Status: Up, Encapsulation: VLAN
        Description: Intf - vpls vpls_4010 neighbor 1.1.0.11 vpls-id 4010
      Flow Label Transmit: No, Flow Label Receive: No

# run show vpls mac-table

# run show evpn mac-table instance evpn_elan_4010

MAC flags       (S -static MAC, D -dynamic MAC, L -locally learned, C -Control MAC
    O -OVSDB MAC, SE -Statistics enabled, NM -Non configured MAC, R -Remote PE MAC, P -Pinned MAC)

Routing instance : evpn_elan_4010
 Bridging domain : __evpn_elan_4010__, VLAN : none
   MAC                 MAC      Logical          NH     MAC         active
   address             flags    interface        Index  property    source
   00:31:01:00:00:01   DC                        1051902            1.1.0.1
   00:32:01:00:00:01   DC                        1063155            00:02:03:01:00:00:00:00:19:00
```
