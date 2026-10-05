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