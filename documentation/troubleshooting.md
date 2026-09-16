# Troubleshooting

## DHCP Failure During Development

### Symptoms

During development, DHCP clients in VLAN 10 and VLAN 50 received APIPA addresses in the `169.254.0.0/16` range instead of receiving addresses from the configured DHCP pools.

Static IP addressing worked correctly.

### Initial Investigation

The following were verified:

- VLAN 10 SVI was up/up
- VLAN 50 SVI was up/up
- DHCP server was reachable
- DHCP pools were configured
- DHCP helper addresses were configured
- ACLs were present
- HSRP was operational
- Inter-VLAN routing was operational

ACL counters also showed DHCP traffic reaching the ACLs.

### Root Cause

The DHCP relay configuration was not consistently configured on the required VLAN interfaces on DIST2.
Because both distribution switches participate in HSRP, either switch may become the active gateway for a VLAN.
When DIST2 handled the gateway traffic without the required DHCP helper configuration, DHCP relay did not function correctly.

### Resolution

The following helper address was added to the appropriate client VLAN interfaces on DIST2:

```text
ip helper-address 192.168.20.10
```
