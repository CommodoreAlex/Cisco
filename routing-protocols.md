### Routing Protocols: Real-Life Devices & Packet Tracer

## Overview

Routing protocols allow routers and other networking devices to automatically determine the best paths for forwarding data across the network. Using Cisco routers in Packet Tracer, you can simulate and configure different routing protocols to understand how data is routed between devices.

## Types of Routing

- **Static Routing**: You manually configure routes on devices. Suitable for small networks or simple setups where routes do not change.
- **Dynamic Routing**: Devices use routing protocols to learn and update the routes dynamically, making the network more adaptable to changes.

## Common Routing Protocols in Packet Tracer

### 1. **RIP (Routing Information Protocol)**

- **Type**: Distance-vector
- **Metric**: Hop count (maximum of 15 hops)
- **Best for**: Small networks with simpler configurations

**Packet Tracer Example**: In Packet Tracer, you can use RIP to enable routing between routers in a small network. Use the `router rip` command and configure the network.

**Configuration**:
```bash
router rip
version 2
network 192.168.1.0
no auto-summary
```

- **Steps in Packet Tracer**:
    - Drag two routers onto the workspace.
    - Connect them with appropriate cables (Ethernet or Serial).
    - Configure their IP addresses.
    - Enable RIP and add network entries.
    - Verify the configuration using `show ip route` and check that routes are exchanged between routers.

### 2. **EIGRP (Enhanced Interior Gateway Routing Protocol)**

- **Type**: Advanced distance-vector
- **Metric**: Bandwidth and delay
- **Best for**: Medium to large networks with faster convergence

**Packet Tracer Example**: EIGRP is a great choice for environments where quick convergence and efficient routing are needed. Configure EIGRP on routers to share routing information dynamically.

**Configuration**:
```bash
router eigrp 100
network 192.168.1.0
no auto-summary
```

- **Steps in Packet Tracer**:
    - Create a larger network with multiple routers and subnets.
    - Assign IP addresses and subnet masks to the routers and PCs.
    - Enable EIGRP and configure the network statements.
    - Use `show ip eigrp neighbors` and `show ip route` to verify routes.

### 3. **OSPF (Open Shortest Path First)**

- **Type**: Link-state
- **Metric**: Cost based on bandwidth
- **Best for**: Large networks with hierarchical design (areas)

**Packet Tracer Example**: OSPF is used in larger networks and allows for area-based configurations, improving scalability.

**Configuration**:
```bash
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
```

- **Steps in Packet Tracer**:
    - Set up a network with multiple areas for OSPF.
    - Configure OSPF with area designations on each router.
    - Verify with `show ip ospf neighbor` and check the OSPF topology.

### 4. **BGP (Border Gateway Protocol)**

- **Type**: Path-vector (inter-domain)
- **Metric**: AS Path
- **Best for**: Internet or large enterprise networks that require inter-domain routing

**Packet Tracer Example**: BGP is commonly used by ISPs and large enterprises for routing between different autonomous systems (ASes).

**Configuration**:
```bash
router bgp 65001
neighbor 192.168.1.2 remote-as 65002
```

- **Steps in Packet Tracer**:
    - Use BGP for inter-router communication between different ASes.
    - Assign AS numbers and configure BGP neighbors.
    - Verify BGP routes with `show ip bgp`.

## Advanced Routing Concepts

### Route Summarization

Summarizing routes helps reduce the size of routing tables and enhances network performance. You can configure route summarization in OSPF to combine multiple IP subnets into one.

**Configuration in OSPF**:
```bash
router ospf 1
summary-address 192.168.0.0 255.255.252.0
```

- **Steps in Packet Tracer**:
    - Configure OSPF in a network with multiple subnets.
    - Apply route summarization on an interface or in an OSPF area.
    - Check the routing table for summarized entries.

### Route Redistribution

Route redistribution allows one routing protocol to share routes with another, such as sharing RIP routes in OSPF.

**Configuration**:
```bash
router ospf 1
redistribute eigrp 100 metric 1000 100 255 1 1500
```

- **Steps in Packet Tracer**:
    - Set up both EIGRP and OSPF on different routers.
    - Configure route redistribution between them.
    - Verify the redistribution by checking the routing tables.

## Verification Commands in Packet Tracer

- **`show ip route`** – Displays the routing table to verify that routes are correctly learned.
- **`show ip protocols`** – Lists all active routing protocols on the router.
- **`show ip ospf neighbor`** – Verifies OSPF neighbor relationships.
- **`debug ip rip`** – Troubleshoots RIP updates and communication.

## Best Practices

- Use **OSPF** for large-scale networks where scalability is important.
- **EIGRP** is preferred in Cisco-exclusive environments where fast convergence is crucial.
- Always **summarize routes** where possible to keep routing tables optimized.
- **Filter routes** to control which networks are advertised to other routers, improving security and efficiency.

---

By simulating these protocols in Cisco Packet Tracer, you can better understand how they operate and practice configuration, verification, and troubleshooting in a controlled environment.
