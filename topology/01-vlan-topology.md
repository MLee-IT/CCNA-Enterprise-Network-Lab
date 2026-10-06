# VLAN Configuration Topology

## Overview

This topology represents a small enterprise network with two departments separated into different VLANs.

## Network Devices

- 1 Cisco switch
- 10 IT workstations
- 10 Accounting workstations

## VLAN Design

| VLAN | Name | Ports | Department |
|---|---|---|---|
| 10 | IT | Fa0/1-Fa0/10 | IT |
| 20 | Accounting | Fa0/11-Fa0/20 | Accounting |

## Topology

```text
                    Cisco Switch
                  +--------------+
                  |              |
        Fa0/1     |              |    Fa0/11
      +-----------+              +----------+
      |                                     |
   PC0 - IT                         PC1 - Accounting
   VLAN 10                              VLAN 20
```

## Network Segmentation

VLAN 10 separates the IT department fromVLAN 20, which is used by the Accounting department.

Devices within the same VLAN can communicate at Layer 2.

Communication between VLAN 10 and VLAN 20 requires inter-VLAN routing.

## Purpose

This topology demonstrates basic network segmentation using VLANs and provides the foundation for future routing and troubleshooting labs.

## Inter-VLAN Routing Topology

```text
                         Router
                    Gig0/0
                       |
                       |
                    Gig0/1
                  +--------+
                  | Switch |
                  +--------+
                   /      \
                Fa0/1    Fa0/11
                  |        |
                PC0       PC1
             VLAN 10    VLAN 20
          192.168.10.10 192.168.20.10
```

The switch-to-router connection is configured as a trunk, allowing VLAN 10 and VLAN 20 traffic to reach the router.

The router uses subinterfaces to provide a default gateway for each VLAN:

- VLAN 10 - `192.168.10.1`
- VLAN 20 - `192.168.20.1`

This configuration allows devices in different VLANs to communicate through the router.