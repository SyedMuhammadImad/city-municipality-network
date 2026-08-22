[← Back to overview](../README.md)

# Lab Manual: Building the City Municipality Network

**Objective:** Design and implement a VLAN-based network for five
departments using Router-on-a-Stick, OSPF, and DHCP.

## Step 1: Devices Used

| Device Type | Model | Quantity | Purpose |
|---|---|---|---|
| Router | 1941 | 1 | Inter-VLAN routing (Router-on-a-Stick) |
| Switch | 2960 | 1 | Layer 2 VLAN switch |
| PCs | PC-PT | 10 | 2 PCs per department |
| Cables | Straight-through | Many | PC-to-switch & switch-to-router connections |

## Step 2: VLAN Planning

| Department | VLAN Name | VLAN ID | Subnet | Gateway IP |
|---|---|---|---|---|
| Water | VLAN_WATER | 10 | 192.168.10.0/24 | 192.168.10.1 |
| Electricity | VLAN_ELEC | 20 | 192.168.20.0/24 | 192.168.20.1 |
| Finance | VLAN_FIN | 30 | 192.168.30.0/24 | 192.168.30.1 |
| Complaints | VLAN_COMP | 40 | 192.168.40.0/24 | 192.168.40.1 |
| Admin | VLAN_ADMIN | 50 | 192.168.50.0/24 | 192.168.50.1 |

## Step 3: VLAN Creation and Port Assignment on Switch

Full commands: [`configs/switch-config.txt`](../configs/switch-config.txt)

```
enable
configure terminal

vlan 10
name VLAN_WATER
exit
vlan 20
name VLAN_ELEC
exit
vlan 30
name VLAN_FIN
exit
vlan 40
name VLAN_COMP
exit
vlan 50
name VLAN_ADMIN
exit

interface range fa0/1 - 2
switchport mode access
switchport access vlan 10
exit
interface range fa0/3 - 4
switchport mode access
switchport access vlan 20
exit
interface range fa0/5 - 6
switchport mode access
switchport access vlan 30
exit
interface range fa0/7 - 8
switchport mode access
switchport access vlan 40
exit
interface range fa0/9 - 10
switchport mode access
switchport access vlan 50
exit

interface fa0/24
switchport mode trunk
exit
```

## Step 4: Router Subinterface Configuration (Router-on-a-Stick)

Full commands: [`configs/router-config.txt`](../configs/router-config.txt)

```
enable
configure terminal

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
no shutdown

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
no shutdown

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
no shutdown

interface g0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
no shutdown

interface g0/0.50
encapsulation dot1Q 50
ip address 192.168.50.1 255.255.255.0
no shutdown

interface g0/0
no shutdown
exit
```

## Step 5: Assign IPs to PCs (Manual Method)

| PC | Department | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| PC0 | Water | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| PC1 | Water | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 |
| PC2 | Electricity | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC3 | Electricity | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 |
| PC4 | Finance | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |
| PC5 | Finance | 192.168.30.3 | 255.255.255.0 | 192.168.30.1 |
| PC6 | Complaints | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 |
| PC7 | Complaints | 192.168.40.3 | 255.255.255.0 | 192.168.40.1 |
| PC8 | Admin | 192.168.50.2 | 255.255.255.0 | 192.168.50.1 |
| PC9 | Admin | 192.168.50.3 | 255.255.255.0 | 192.168.50.1 |

## Step 6: Testing

- From each PC, ping its own default gateway
- Try inter-VLAN pings (e.g., PC0 to PC5)
- Use the `ping` command from the command prompt:

```
ping 192.168.X.X
```

**Project completed successfully.**

---

[← Back to overview](../README.md)
