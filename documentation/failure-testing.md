# Failure Testing

## Purpose

Failure testing was performed to verify that the redundancy mechanisms configured in the network operate as expected.
The tests intentionally introduced failures and then verified whether network connectivity and redundancy mechanisms remained operational.

---

## Test 1: EtherChannel Failure

### Objective

Verify that the Layer 2 EtherChannel remains operational when one physical member link fails.

### Procedure

1. Verify the normal EtherChannel state.
2. Shut down one physical EtherChannel member.
3. Verify the Port-Channel state.
4. Test client connectivity.
5. Restore the failed interface.
6. Verify that the EtherChannel returns to its normal state.

### Expected Result

The Port-Channel should remain operational using the remaining physical member.

### Evidence

Add the relevant screenshots below:

- EtherChannel normal state
- EtherChannel during failure
- Connectivity during failure
- EtherChannel after recovery

---

## Test 2: OSPF Path Failure

### Objective

Verify that routing remains available if one routed path between the distribution layer and edge router fails.

### Procedure

1. Verify OSPF neighbor relationships.
2. Shut down one routed path.
3. Verify the OSPF neighbor relationship changes.
4. Test client connectivity.
5. Restore the interface.
6. Verify OSPF recovery.

### Expected Result

Traffic should continue through the remaining available routed path.

### Evidence

Add the relevant screenshots below:

- OSPF normal state
- OSPF during failure
- Connectivity during failure
- OSPF after recovery

---

## Test 3: HSRP Failure

### Objective

Verify that the standby distribution switch assumes the gateway role when the active VLAN 10 SVI fails.

### Procedure

1. Verify HSRP status.
2. Shut down the active VLAN 10 SVI on DIST1.
3. Verify HSRP status on DIST2.
4. Test client connectivity.
5. Restore the VLAN 10 SVI.
6. Verify the normal HSRP state.

### Expected Result

DIST2 should become Active for VLAN 10 and clients should continue to use the HSRP virtual gateway.

### Evidence

Add the relevant screenshots below:

- HSRP baseline
- HSRP failover
- Connectivity during failover
- HSRP recovery

---

## Overall Result

The failure tests are intended to demonstrate that the network can tolerate selected physical-link, routed-path, and gateway failures without complete loss of connectivity.

