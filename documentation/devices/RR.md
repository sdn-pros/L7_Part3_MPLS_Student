# RR

## Table of Contents

- [Management](#management)
  - [DNS Domain](#dns-domain)
  - [Management API HTTP](#management-api-http)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [MPLS](#mpls)
  - [MPLS and LDP](#mpls-and-ldp)
  - [MPLS Interfaces](#mpls-interfaces)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [EOS CLI](#eos-cli)

## Management

### DNS Domain

#### DNS domain: atd.lab

#### DNS Domain Device Configuration

```eos
dns domain atd.lab
!
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_BL1-DC1_Ethernet5 | routed | - | 10.0.0.85/31 | default | 1500 | False | - | - |
| Ethernet5 | P2P_LINK_TO_BL1-DC2_Ethernet5 | routed | - | 10.0.0.87/31 | default | 1500 | False | - | - |

##### ISIS

| Interface | Channel Group | ISIS Instance | ISIS Metric | Mode | ISIS Circuit Type | Hello Padding | Authentication Mode |
| --------- | ------------- | ------------- | ----------- | ---- | ----------------- | ------------- | ------------------- |
| Ethernet1 | - | CORE | 50 | point-to-point | level-2 | False | - |
| Ethernet5 | - | CORE | 50 | point-to-point | level-2 | False | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_BL1-DC1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 10.0.0.85/31
   mpls ip
   isis enable CORE
   isis circuit-type level-2
   isis metric 50
   no isis hello padding
   isis network point-to-point
!
interface Ethernet5
   description P2P_LINK_TO_BL1-DC2_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 10.0.0.87/31
   mpls ip
   isis enable CORE
   isis circuit-type level-2
   isis metric 50
   no isis hello padding
   isis network point-to-point
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 3.3.0.90/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | MPLS_Overlay_peering | default | - |

##### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | CORE | - | passive |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description MPLS_Overlay_peering
   no shutdown
   ip address 3.3.0.90/32
   isis enable CORE
   isis passive
   node-segment ipv4 index 90
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT | 0.0.0.0/0 | 192.168.0.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 192.168.0.1
```

### Router ISIS

#### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | CORE |
| Net-ID | 49.0001.0000.0001.0090.00 |
| Type | level-2 |
| Router-ID | 3.3.0.90 |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |

#### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | CORE | 50 | point-to-point |
| Ethernet5 | CORE | 50 | point-to-point |
| Loopback0 | CORE | - | passive |

#### ISIS Segment-routing Node-SID

| Loopback | IPv4 Index | IPv6 Index |
| -------- | ---------- | ---------- |
| Loopback0 | 90 | - |

#### ISIS IPv4 Address Family Summary

| Settings | Value |
| -------- | ----- |
| IPv4 Address-family Enabled | True |
| Maximum-paths | 4 |

#### Router ISIS Device Configuration

```eos
!
router isis CORE
   net 49.0001.0000.0001.0090.00
   is-type level-2
   router-id ipv4 3.3.0.90
   log-adjacency-changes
   !
   address-family ipv4 unicast
      maximum-paths 4
   !
   segment-routing mpls
      no shutdown
```

### Router BGP

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65300|  3.3.0.90 |

| BGP AS | Cluster ID |
| ------ | --------- |
| 65300|  3.3.0.90 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN_RRClient

| Settings | Value |
| -------- | ----- |
| Address Family | mpls |
| Remote AS | 65300 |
| Route Reflector Client | Yes |
| Source | Loopback0 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### RR-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | mpls |
| Remote AS | 65300 |
| Source | Loopback0 |
| BFD | True |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- |
| 3.3.0.91 | Inherited from peer group EVPN_RRClient | default | - | Inherited from peer group EVPN_RRClient | Inherited from peer group EVPN_RRClient | - | - | - | Inherited from peer group EVPN_RRClient | - |
| 3.3.0.95 | Inherited from peer group EVPN_RRClient | default | - | Inherited from peer group EVPN_RRClient | Inherited from peer group EVPN_RRClient | - | - | - | Inherited from peer group EVPN_RRClient | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Encapsulation |
| ---------- | -------- | ------------- |
| EVPN_RRClient | True | default |
| RR-OVERLAY-PEERS | True | default |

##### EVPN Neighbor Default Encapsulation

| Neighbor Default Encapsulation | Next-hop-self Source Interface |
| ------------------------------ | ------------------------------ |
| mpls | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65300
   router-id 3.3.0.90
   maximum-paths 4 ecmp 4
   no bgp default ipv4-unicast
   bgp cluster-id 3.3.0.90
   neighbor EVPN_RRClient peer group
   neighbor EVPN_RRClient remote-as 65300
   neighbor EVPN_RRClient update-source Loopback0
   neighbor EVPN_RRClient route-reflector-client
   neighbor EVPN_RRClient send-community
   neighbor EVPN_RRClient maximum-routes 0
   neighbor RR-OVERLAY-PEERS peer group
   neighbor RR-OVERLAY-PEERS remote-as 65300
   neighbor RR-OVERLAY-PEERS update-source Loopback0
   neighbor RR-OVERLAY-PEERS bfd
   neighbor RR-OVERLAY-PEERS send-community
   neighbor RR-OVERLAY-PEERS maximum-routes 0
   neighbor 3.3.0.91 peer group EVPN_RRClient
   neighbor 3.3.0.91 description BL1-DC1
   neighbor 3.3.0.95 peer group EVPN_RRClient
   neighbor 3.3.0.95 description BL1-DC2
   !
   address-family evpn
      neighbor default encapsulation mpls
      neighbor EVPN_RRClient activate
      neighbor RR-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN_RRClient activate
      no neighbor RR-OVERLAY-PEERS activate
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## MPLS

### MPLS and LDP

#### MPLS and LDP Summary

| Setting | Value |
| -------- | ---- |
| MPLS IP Enabled | True |
| LDP Enabled | False |
| LDP Router ID | - |
| LDP Interface Disabled Default | - |
| LDP Transport-Address Interface | - |

#### MPLS and LDP Configuration

```eos
!
mpls ip
```

### MPLS Interfaces

| Interface | MPLS IP Enabled | LDP Enabled | IGP Sync |
| --------- | --------------- | ----------- | -------- |
| Ethernet1 | True | - | - |
| Ethernet5 | True | - | - |

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

## EOS CLI

```eos
!

router bgp 65300
  address-family evpn
     neighbor EVPN_RRClient activate
     neighbor EVPN_RRClient encapsulation mpls next-hop-self source-interface Loopback0

     
 address-family ipv4
    no neighbor EVPN_RRClient activate
    network 13.3.0.90/32


interface Ethernet1,5
  no switchport
  isis enable CORE
  traffic-engineering
  isis network point-to-point
  isis circuit-type level-2
  no isis hello padding

router isis CORE
  segment-routing mpls
   router-id 3.3.0.90
    no shutdown


  traffic-engineering
    no shutdown
    is-type level-2

router traffic-engineering
 segment-routing
 router-id ipv4 3.3.0.90
```
