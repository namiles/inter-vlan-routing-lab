# Inter-VLAN Routing
You can find the full configuration for my inter-vlan routing labs below. See more at https://www.nicksnetwork.com.

## Router-on-a-Stick

### R1
```
interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 ip address 10.1.10.254 255.255.255.0

interface GigabitEthernet0/1.20
 encapsulation dot1Q 20
 ip address 10.1.20.254 255.255.255.0

interface GigabitEthernet0/1.30
 encapsulation dot1Q 30
 ip address 10.1.30.254 255.255.255.0

interface GigabitEthernet0/1.40
 encapsulation dot1Q 40
 ip address 10.1.40.254 255.255.255.0

interface GigabitEthernet0/1
 no shutdown

```
### S1
```
router ospf 1
 router-id 2.2.2.2
 network 172.16.1.0 0.0.0.255 area 1
 network 10.1.1.0 0.0.0.3 area 0
 
interface Loopback0
 ip ospf 1 area 1
```
## Multilayer/Layer 3 Switch

### S1
```
vlan 10
 name Administration
 
vlan 20
 name Accounting
 
vlan 30
 name HR
 
vlan 40
 name IT
 
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access

interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access

interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access

interface FastEthernet0/4
 switchport access vlan 40
 switchport mode access

interface FastEthernet0/5
 switchport access vlan 40
 switchport mode access

interface GigabitEthernet0/1
 switchport trunk allowed vlan 10,20,30,40
 switchport mode trunk

```
