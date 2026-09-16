# Security Controls

## Security Objectives

The security design focuses on:

- Network segmentation
- Least-privilege communication
- Layer 2 access protection
- DHCP protection
- ARP protection
- Centralized logging

## VLAN Segmentation

Traffic is separated into:

- Users
- Servers
- Security
- Management
- Guest

This limits unnecessary communication between network segments.

## Extended ACLs

Extended ACLs are used to control communication between VLANs.

### User VLAN Restrictions

VLAN 10 users are restricted from accessing:

- VLAN 30 Security
- VLAN 40 Management

Required infrastructure traffic such as DHCP is explicitly permitted.

### Guest VLAN Restrictions

VLAN 50 is isolated from internal VLANs including:

- VLAN 10 Users
- VLAN 20 Servers
- VLAN 30 Security
- VLAN 40 Management

This allows guest access to permitted destinations without giving guests direct access to internal resources.

## Port Security

Port Security is configured on endpoint-facing access ports.
The purpose is to limit unauthorized devices from connecting to protected switchports.
The access layer is the primary enforcement point because endpoint devices connect directly to the access switches.

## DHCP Snooping

DHCP Snooping is enabled for the client VLANs.
Interfaces toward the distribution layer are configured as trusted interfaces.
Endpoint-facing interfaces remain untrusted.
This helps prevent rogue DHCP servers from responding to client DHCP requests.

## Dynamic ARP Inspection

Dynamic ARP Inspection (DAI) is enabled on the appropriate client VLANs.
DAI uses DHCP Snooping information to validate IP-to-MAC mappings contained in ARP traffic.
This helps mitigate ARP spoofing and ARP poisoning attacks.

## Centralized Logging

A dedicated Security VLAN contains the Syslog server:

```text
SECURITY-SYSLOG
192.168.30.10

