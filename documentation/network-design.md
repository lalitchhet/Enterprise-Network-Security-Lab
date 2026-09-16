# Network Design

## Objective

The objective of this project was to design and implement a small enterprise-style network using Cisco Packet Tracer.
The lab was built to demonstrate practical networking, redundancy, security, infrastructure services, troubleshooting, and failure testing.
The design separates endpoint, server, security, management, and guest traffic using VLANs while providing redundant gateways and network paths.

## Network Architecture

The network uses an enterprise-style hierarchical design consisting of:

- Edge routing
- Redundant multilayer distribution switches
- Access-layer switches
- Dedicated server and security VLANs

### Physical Topology

The topology consists of:

- R1-EDGE
- DIST1
- DIST2
- ACCESS1
- ACCESS2
- User endpoints
- Guest endpoints
- Management endpoint
- Infrastructure servers
- Security monitoring/Syslog server

The edge router connects to both distribution switches using Layer 3 routed links.

DIST1 and DIST2 are interconnected using LACP EtherChannel.

Both access switches have redundant uplinks toward the distribution layer.

## Distribution Layer

DIST1 and DIST2 are multilayer switches responsible for:

- Inter-VLAN routing
- HSRP
- OSPF
- DHCP relay
- ACL-based traffic filtering
- Spanning-tree root functions

## Access Layer

ACCESS1 and ACCESS2 provide Layer 2 connectivity for endpoint and server devices.

The access layer also implements security controls including:

- Port Security
- DHCP Snooping
- Dynamic ARP Inspection

## Network Segmentation

The network is divided into five VLANs:

| VLAN | Name | Purpose |
|------|------|---------|
| 10 | USERS | Employee/user devices |
| 20 | SERVERS | Infrastructure services |
| 30 | SECURITY | Security monitoring and logging |
| 40 | MANAGEMENT | Network management devices |
| 50 | GUEST | Guest devices |

## Design Goals

The network was designed to provide:

- Separation of network functions
- Redundant default gateways
- Redundant routing paths
- Link redundancy
- Layer 2 loop prevention
- Controlled inter-VLAN communication
- Protection against common Layer 2 attacks
- Centralized network logging
- Reliable infrastructure services
- Testable failure scenarios

## Design Philosophy

The lab was intentionally designed so that individual components could fail without immediately causing a complete network outage.

Redundancy was implemented at multiple layers using:

- HSRP
- OSPF
- EtherChannel

Security was implemented at both Layer 2 and Layer 3 using:

- VLAN segmentation
- ACLs
- Port Security
- DHCP Snooping
- Dynamic ARP Inspection

This allowed the project to demonstrate both network availability and security concepts within the same environment.

