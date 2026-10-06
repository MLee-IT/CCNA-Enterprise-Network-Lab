# DHCP Configuration Lab

## Objective

Configure DHCP on a Cisco router so devices in different VLANs automatically receive their network configuration.

## Network Scenario

The enterprise network contains two departments:

- VLAN 10 - IT
- VLAN 20 - Accounting

The router provides DHCP services for both VLANs.

## VLAN Information

| VLAN | Name | Network | Gateway |
|---|---|---|---|
| 10 | IT | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Accounting | 192.168.20.0/24 | 192.168.20.1 |

## DHCP Configuration

### VLAN 10 DHCP Pool

```cisco
ip dhcp pool IT
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
exit
```

## VLAN 20 DHCP Pool

```cisco
ip dhcp pool Accounting
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8
exit
```

## PC Configuration

PC0 was configured to obtain its network settings automatically using DHCP.

PC0 received:

- IP Address: `192.168.20.2`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.20.1`

## Connectivity Test

A ping was performed from PC0 to PC1:

`ping 192.168.20.2`

The ping was successful and returned replies from PC1.

## DHCP Verification

The router DHCP bindings were verified using:

```cisco
show ip dhcp binding
```

The DHCP bindings confirmed that the router successfully assigned IP addresses to the PCs.

## Result

DHCP was successfully configured for VLAN 10 and VLAN 20.

Both PCs automatically received valid IP addresses, subnet masks, and default gateways.

Inter-VLAN connectivity was also successfully verified.

## Troubleshooting

The router CLI initially returned an invalid input message when the DHCP binding command was entered from the incorrect CLI mode.

The issue was resolved by entering privileged EXEC mode:

```cisco
enable
```

The DHCP bindings were then successfully verified using:

```cisco
show ip dhcp binding
```