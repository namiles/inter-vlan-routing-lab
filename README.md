# Inter-VLAN Routing
You can find the full configuration for my inter-vlan routing labs below. See more at https://www.nicksnetwork.com.

## Router-on-a-Stick

### R1
```
router ospf 1
 router-id 1.1.1.1
 network 10.1.1.0 0.0.0.3 area 0
 network 10.1.2.0 0.0.0.3 area 0
 network 10.1.3.0 0.0.0.3 area 0

interface Loopback0
 ip ospf 1 area 0
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
ipv6 router ospf 1
 router-id 1.1.1.1
 
interface Loopback0
 ipv6 ospf 1 area 1

interface GigabitEthernet0/0
 ipv6 ospf 1 area 1
```
