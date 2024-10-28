#### SCP from VRF
```
$ ssh an1
an1> start shell
an1:~$ chvrf mgmt_junos scp /var/tmp/jinstall-host-qfx-5e-x86-64-22.4R3-S4.5-secure-signed.tgz <username>@<host>:/var/tmp/
```
#### Become root
```
an1:~$ su root
Password:
sh-5.1#
```
### Login to vmhost
```
vhclient -s
```
### MX80/104 FPC
```
vty afeb0
```
### Resource monitoring
```
show system resource-monitor fpc
show system resource-monitor summary
```
vty
```
show jnh 0 pool summary
show jnh 0 pool summary verbose
```
