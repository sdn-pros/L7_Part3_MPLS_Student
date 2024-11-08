# MPLS_FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [ISIS CLNS interfaces](#isis-clns-interfaces)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| MPLS_FABRIC | pe | BL1-DC1 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | pe | BL1-DC2 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | p | P1 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | p | P2 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | p | P3 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | p | P4 | - | cEOS | Provisioned | - |
| MPLS_FABRIC | rr | RR | - | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| pe | BL1-DC1 | Ethernet1 | p | P1 | Ethernet1 |
| pe | BL1-DC1 | Ethernet5 | rr | RR | Ethernet1 |
| pe | BL1-DC2 | Ethernet1 | p | P3 | Ethernet1 |
| pe | BL1-DC2 | Ethernet4 | p | P4 | Ethernet3 |
| pe | BL1-DC2 | Ethernet5 | rr | RR | Ethernet5 |
| p | P1 | Ethernet2 | p | P3 | Ethernet2 |
| p | P1 | Ethernet4 | p | P2 | Ethernet4 |
| p | P2 | Ethernet2 | p | P4 | Ethernet2 |
| p | P3 | Ethernet4 | p | P4 | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| BL1-DC1 | Ethernet1 | 10.0.0.80/31 | P1 | Ethernet1 | 10.0.0.81/31 |
| BL1-DC1 | Ethernet5 | 10.0.0.84/31 | RR | Ethernet1 | 10.0.0.85/31 |
| BL1-DC2 | Ethernet1 | 10.0.0.82/31 | P3 | Ethernet1 | 10.0.0.83/31 |
| BL1-DC2 | Ethernet4 | 10.0.0.97/31 | P4 | Ethernet3 | 10.0.0.96/31 |
| BL1-DC2 | Ethernet5 | 10.0.0.86/31 | RR | Ethernet5 | 10.0.0.87/31 |
| P1 | Ethernet2 | 10.0.0.88/31 | P3 | Ethernet2 | 10.0.0.89/31 |
| P1 | Ethernet4 | 10.0.0.90/31 | P2 | Ethernet4 | 10.0.0.91/31 |
| P2 | Ethernet2 | 10.0.0.95/31 | P4 | Ethernet2 | 10.0.0.94/31 |
| P3 | Ethernet4 | 10.0.0.92/31 | P4 | Ethernet4 | 10.0.0.93/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 7 | 2.74 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| MPLS_FABRIC | BL1-DC1 | 192.168.255.91/32 |
| MPLS_FABRIC | BL1-DC2 | 192.168.255.95/32 |
| MPLS_FABRIC | P1 | 192.168.255.93/32 |
| MPLS_FABRIC | P2 | 192.168.255.94/32 |
| MPLS_FABRIC | P3 | 192.168.255.97/32 |
| MPLS_FABRIC | P4 | 192.168.255.98/32 |
| MPLS_FABRIC | RR | 192.168.255.90/32 |

### ISIS CLNS interfaces

| POD | Node | CLNS Address |
| --- | ---- | ------------ |
| MPLS_FABRIC | BL1-DC1 | 49.0001.0000.0001.0091.00 |
| MPLS_FABRIC | BL1-DC2 | 49.0001.0000.0001.0095.00 |
| MPLS_FABRIC | P1 | 49.0001.0000.0001.0093.00 |
| MPLS_FABRIC | P2 | 49.0001.0000.0001.0094.00 |
| MPLS_FABRIC | P3 | 49.0001.0000.0001.0097.00 |
| MPLS_FABRIC | P4 | 49.0001.0000.0001.0098.00 |
| MPLS_FABRIC | RR | 49.0001.0000.0001.0090.00 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
