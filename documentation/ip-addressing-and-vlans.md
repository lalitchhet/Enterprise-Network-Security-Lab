# IP Addressing and VLANs

## VLAN Design

The lab uses five VLANs to separate different types of network traffic.

| VLAN | Name | Network | Default Gateway | Purpose |
|------|------|---------|-----------------|---------|
| 10 | USERS | 192.168.10.0/24 | 192.168.10.1 | User endpoints |
| 20 | SERVERS | 192.168.20.0/24 | 192.168.20.1 | Infrastructure servers |
| 30 | SECURITY | 192.168.30.0/24 | 192.168.30.1 | Security monitoring |
| 40 | MANAGEMENT | 192.168.40.0/24 | 192.168.40.1 | Management devices |
| 50 | GUEST | 192.168.50.0/24 | 192.168.50.1 | Guest endpoints |

## HSRP Virtual Gateways

The `.1` address for each VLAN is the HSRP virtual gateway.

| VLAN | HSRP Virtual IP |
|------|-----------------|
| 10 | 192.168.10.1 |
| 20 | 192.168.20.1 |
| 30 | 192.168.30.1 |
| 40 | 192.168.40.1 |
| 50 | 192.168.50.1 |

DIST1 and DIST2 use separate physical SVI addresses for each VLAN.

## Distribution Switch SVI Addresses

| VLAN | DIST1 | DIST2 |
|------|-------|-------|
| 10 | 192.168.10.2 | 192.168.10.3 |
| 20 | 192.168.20.2 | 192.168.20.3 |
| 30 | 192.168.30.2 | 192.168.30.3 |
| 40 | 192.168.40.2 | 192.168.40.3 |
| 50 | 192.168.50.2 | 192.168.50.3 |

## Server Addressing

| Device | IP Address | Role |
|--------|------------|------|
| SERVER1 | 192.168.20.10 | DHCP |
| SERVER2 | 192.168.20.11 | DNS |
| SERVER3 | 192.168.20.12 | FTP/TFTP |
| SECURITY-SYSLOG | 192.168.30.10 | Centralized logging |

## Routed Links

The distribution switches use Layer 3 routed links toward R1-EDGE.

| Link | Network |
|------|---------|
| R1-EDGE ↔ DIST1 | 10.0.0.0/30 |
| R1-EDGE ↔ DIST2 | 10.0.0.4/30 |

## DHCP

SERVER1 provides centralized DHCP services.

Remote client VLANs use DHCP relay with:

```text
ip helper-address 192.168.20.10

