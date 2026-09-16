# Routing and Redundancy

## Inter-VLAN Routing

DIST1 and DIST2 are multilayer switches and provide Layer 3 routing between VLANs using Switch Virtual Interfaces (SVIs).
IP routing is enabled on both distribution switches.

## HSRP

Hot Standby Router Protocol (HSRP) provides first-hop redundancy.
Each VLAN uses a virtual gateway address shared between DIST1 and DIST2.
The virtual gateway remains available if the active distribution switch fails.

### HSRP Design

| VLAN | Virtual Gateway |
|------|-----------------|
| 10 | 192.168.10.1 |
| 20 | 192.168.20.1 |
| 30 | 192.168.30.1 |
| 40 | 192.168.40.1 |
| 50 | 192.168.50.1 |

The active/standby roles are distributed between the two distribution switches.

## OSPF

OSPF is used as the dynamic routing protocol between R1-EDGE, DIST1, and DIST2.
All OSPF routing is performed in Area 0.

### Routed Links

- R1-EDGE ↔ DIST1: 10.0.0.0/30
- R1-EDGE ↔ DIST2: 10.0.0.4/30

Loopback interfaces are used for stable router identification and are configured as passive interfaces.

## EtherChannel

DIST1 and DIST2 use LACP to create a Layer 2 EtherChannel.

The EtherChannel provides redundancy between the distribution switches.
If one physical member fails, the remaining member can continue forwarding traffic through the logical Port-Channel.

## Rapid-PVST+

Rapid-PVST+ is used for spanning-tree protection.
The distribution layer is used as the spanning-tree root layer for the appropriate VLANs.
This provides predictable Layer 2 forwarding paths and prevents switching loops.

## Redundancy Testing

Three primary failure scenarios were tested:

1. EtherChannel physical member failure
2. OSPF routed-link failure
3. HSRP gateway failure

The purpose of these tests was to verify that redundant paths and gateways continued to provide network connectivity.

