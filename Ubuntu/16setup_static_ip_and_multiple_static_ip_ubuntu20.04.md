__configure static ip in ubuntu20.04__

To find default gateway 
```
# ip r | grep default
```
List Network Interfaces Using ip
```
# ip link show
or
# ip a
```
create the file
```
# vim /etc/netplan/01-network-manager-all.yaml

network:
    version: 2
    renderer: networkd
    ethernets:
        enp1s0: 
            dhcp4: no
            addresses: [192.168.122.141/24]
            gateway4: 192.168.122.1
        nameservers:
            addresses: [8.8.8.8/32,8.8.4.4/32]
            
:wq! save and exit
```
\
__configure multiple static ip to single interface__

open the file
```
# vim /etc/netplan/01-network-manager-all.yaml

network:
    version: 2
    renderer: networkd
    ethernets:
        enp1s0: 
            dhcp4: no
            addresses: [192.168.122.141/24]
            addresses: [192.168.122.142/24]
            addresses: [192.168.122.143/24]
            addresses: [192.168.122.144/24]
            gateway4: 192.168.122.1
        nameservers:
            addresses: [8.8.8.8/32,8.8.4.4/32]
            
:wq! save and exit
```
set DHCP to dhcp4: no\
specify the static IP address. Under addresses. 
we can add one or more IP addresses assigned to the network interface\
specify the gateway\
set the IP addresses of the nameservers
\
netplan generate command converts the settings in the yaml files to configurations
appropriate to the renderer in use, but does not apply them
```
# netplan generate
```
apply the changes
```
# netplan apply
```
login and logout
```
# ip a 
```
