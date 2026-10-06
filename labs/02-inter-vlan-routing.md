# Inter-VLAN Routing Lab

## Objective

Configure inter-VLAN routing using a Cisco router so devices in different VLANs can communicate.

## Network Scenario

The enterprise network contains two departments:

- VLAN 10 - IT
- VLAN 20 - Accounting

The departments are separated into different VLANs bur need to communicate through a router.

## VLAN Information

```text
| VLAN | Name | Network | Gateway |
|---|---|---|---|
| 10 | IT | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Accounting | 192.168.20.0/24 | 192.168.20.1 |
## Device Configuration

The switch port connected to the router was configured as a trunk.

The router was configured using router-on-a-stick with subinterfaces for each VLAN.

### VLAN 10 Subinterface

```cisco
interface gigabitethernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
```

### VLAN 20 Subinterface

```cisco
interface gigabitethernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

## PC Configuration

PC0 was configured with:

- IP Address: `192.168.10.10`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.10.1`

PC1 was configured with:
- IP Address: `192.168.20.10`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.20.1`

## Connectivity Test

A ping was performed from PC0 to PC1:

`ping 192.168.20.10`

The ping was successful and returned replies from PC1.

## Result

Inter-VLAN routing was successfully configured.

Devices in VLAN 10 and VLAN 20 were able to communicate through the router using router-on-a-stick.

## Troubleshooting

During configuration, VLAN 20 initially did not have an IP address assigned to its router subinterface.

The issue was identified by using:

```cisco
show ip interface brief
```

The VLAN 20 subinterface was then configured with:

```cisco
ip address 192.168.20.1 255.255.255.0
```

After the configuration was corrected, the connectivity test was successful.