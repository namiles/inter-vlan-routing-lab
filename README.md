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
### R2
```
router ospf 1
 router-id 2.2.2.2
 network 172.16.1.0 0.0.0.255 area 1
 network 10.1.1.0 0.0.0.3 area 0
 
interface Loopback0
 ip ospf 1 area 1
```
### R3
```
router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes
 network 172.16.2.0 0.0.0.255 area 2
 network 10.1.2.0 0.0.0.3 area 0
 
interface Loopback0
 ip ospf 1 area 2
```
### R4
```
router ospf 1
 router-id 4.4.4.4
 network 172.16.3.0 0.0.0.255 area 3
 network 10.1.3.0 0.0.0.3 area 0
 
interface Loopback0
 ip ospf 1 area 3
```
## Multilayer/Layer 3 Switch

### R1
```
ipv6 router ospf 1
 router-id 1.1.1.1
 
interface Loopback0
 ipv6 ospf 1 area 1

interface GigabitEthernet0/0
 ipv6 ospf 1 area 1
```
### R2
```
ipv6 router ospf 1
 router-id 2.2.2.2
 
interface Loopback0
 ipv6 ospf 1 area 0

interface GigabitEthernet0/0
 ipv6 ospf 1 area 1

interface GigabitEthernet0/1
 ipv6 ospf 1 area 0
```
### R3
```
ipv6 router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes
 
interface Loopback0
 ipv6 ospf 1 area 0

interface GigabitEthernet0/1
 ipv6 ospf 1 area 0

interface GigabitEthernet0/2
 ipv6 ospf 1 area 2
```
### R4
```
ipv6 router ospf 1
 router-id 4.4.4.4

interface Loopback0
 ipv6 ospf 1 area 2

interface GigabitEthernet0/2
 ipv6 ospf 1 area 2
```
