# VLAN Configuration Lab

## Objective

Configure VLANs on a Cisco switch and assign switch ports to the appropriate VLANs.

## Network Scenario

A small enterprise network has two departments:

- VLAN 10 - IT
- VLAN 20 - Accounting

Each department needs to be separated into its own broadcast domain.

## VLAN Information

| VLAN | Name | Department |
|---|---|---|
| 10 | IT | IT Department |
| 20 | Accounting | Accounting Department |

## Switch Configuration

Enter the following commands on the Cisco switch:

```cisco
enable
configure terminal

vlan 10
name IT
exit

vlan 20
name Accounting
exit

interface range fastethernet 0/1-10
switchport mode access
switchport access vlan 10
exit

interface range fastethernet 0/11-20
switchport mode access
switchport access vlan 20
exit

end
```

## Verification

Use the following command to verify the VLAN configuration:

```cisco
show vlan brief
```

The output should show VLAN 10 and VLAN 20 with the appropriate switch ports assigned.

## Troubleshooting

If a device cannot communicate with other devices in the expected VLAN:

1. Verify the VLAN exists.
2. Verify the switch port is assigned to the correct VLAN.
3. Verify the port is configured as an access port.
4. Check the physical or simulated connection.
5. Use `show vlan brief` to verify the configuration.

## Expected Result

The switch should contain VLAN 10 and VLAN 20, with the appropriate access ports assigned to each VLAN.

Devices connected to different VLANs should remain separated until inter-VLAN routing is configured.

## Connectivity Test

PC0 was configured with IP address `192.168.10.10` on VLAN 10.

PC1 was configured with IP address `192.168.20.10` on VLAN 20.

A ping was performed from PC0 to PC1:

```text
ping 192.168.20.10
```

The ping resulted in `Request timed out`.

This result is expected becauses PC0 and PC1 are assigned to different VLANs and no inter-VLAN routing has been configured.

## Result

The VLAN configuration was successfully verified.
Devices in VLAN 10 and VLAN 20 remain separated at Layer 2.