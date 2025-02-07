### Junos
```
set groups TACACS system login user operator uid 2002
set groups TACACS system login user operator class read-only
set groups TACACS system login user SU uid 2003
set groups TACACS system login user SU class super-user
set groups TACACS system authentication-order tacplus
set groups TACACS system tacplus-server 10.49.99.70 port 49
set groups TACACS system tacplus-server 10.49.99.70 secret "$9$3-FAnA0B1hrK8RhdbY2aJn/9"
set groups TACACS system tacplus-server 10.49.99.70 source-address 10.49.99.11
set groups TACACS system accounting events change-log
set groups TACACS system accounting events interactive-commands
set groups TACACS system accounting events login
set groups TACACS system accounting destination tacplus server 10.49.99.70 secret "$9$/O.l9u1REyKWxcywY4oGU9At"
```

### TACACS
```
sudo docker run -td --name tacplus -p 49:49 -v ~/tac_plus.conf:/etc/tacacs+/tac_plus.conf llima3000/tacplus
```
```
# cat tac_plus.conf
# This is the 'secret' we specified in Junos

key = pass123

# This is the actual user who is a member of group 'SU'
user = user1 {
 member = SU
 login = cleartext password123
}

# Here is another user, who belongs in the other group.
user = netops {
 member = operator
 login = cleartext operator456
}

# Here is the SU group definition.  It specifies a
# junos-specific 'local-user-name' to pass back if
# authentication is successful.  This must match the
# local user we configured in Junos
group = SU {
   service = junos-exec {
     local-user-name = SU
   }
}
group = operator {
   service = junos-exec {
     local-user-name = operator
     allow-commands = "start shell"
   }
}
```
