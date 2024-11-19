#### Match IPv6 DST using the first 64 bits from the prefix list and the last 64 bits with the flex mask
```
set groups FW-Flex-64-Limited firewall flexible-match v6-dst-lower-64-bits match-start layer-3
set groups FW-Flex-64-Limited firewall flexible-match v6-dst-lower-64-bits byte-offset 32
set groups FW-Flex-64-Limited firewall flexible-match v6-dst-lower-64-bits bit-length 64
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 from destination-prefix-list IPv6_Prefix_mask_64
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 from payload-protocol icmp6
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 from flexible-match-mask prefix my64bits
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 from flexible-match-mask flexible-mask-name v6-dst-lower-64-bits
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 then count icmp.in.v6
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Inbound-v6 term icmp-v6 then accept
```
#### Match IPv6 SRC using the first 64 bits from the prefix list and the last 64 bits with the flex mask
```
set groups FW-Flex-64-Limited firewall flexible-match v6-src-lower-64-bits match-start layer-3
set groups FW-Flex-64-Limited firewall flexible-match v6-src-lower-64-bits byte-offset 16
set groups FW-Flex-64-Limited firewall flexible-match v6-src-lower-64-bits bit-length 64
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 from source-prefix-list IPv6_Prefix_mask_64
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 from payload-protocol icmp6
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 from flexible-match-mask prefix my64bits
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 from flexible-match-mask flexible-mask-name v6-src-lower-64-bits
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 then count icmp.out.v6
set groups FW-Flex-64-Limited firewall family inet6 filter ISP-Outbound-v6 term icmp-v6 then accept
```
