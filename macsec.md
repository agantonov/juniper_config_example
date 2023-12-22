```
set security macsec connectivity-association CA cipher-suite gcm-aes-xpn-128
set security macsec connectivity-association CA security-mode static-cak
set security macsec connectivity-association CA pre-shared-key ckn abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234
set security macsec connectivity-association CA pre-shared-key cak "<connectivity association key>"
set security macsec interfaces et-1/3/0 connectivity-association CA
```
