# VLANs and Subnetting

## Introduction

Virtual Local Area Networks (VLANs) and subnetting are essential for network segmentation, security, and efficient traffic management. This guide covers VLAN creation, inter-VLAN routing, and subnetting best practices for Cisco devices.

---

## Understanding VLANs

### What is a VLAN?

A **VLAN (Virtual Local Area Network)** is a logical grouping of network devices within a switch, isolating traffic between them. VLANs enhance security and efficiency by separating network segments without needing additional physical hardware.

### Benefits of VLANs:

- Improves network performance by reducing broadcast domains.
- Enhances security by segmenting sensitive data traffic.
- Allows for better network management and scalability.

### Creating VLANs on a Cisco Switch

To create and assign VLANs:
```bash
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name HR_VLAN
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name IT_VLAN
Switch(config-vlan)# exit
```

Assigning VLANs to Interfaces:
```bash
Switch(config)# interface FastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit

Switch(config)# interface FastEthernet 0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit
```

### Configuring a Trunk Port

A **trunk port** allows multiple VLANs to pass through a single link between switches.
```bash
Switch(config)# interface GigabitEthernet 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# exit
```

---

## Inter-VLAN Routing

By default, VLANs cannot communicate with each other. To enable communication, **inter-VLAN routing** is required.

### Using a Router (Router-on-a-Stick)

```bash
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet 0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface GigabitEthernet 0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit
```

### Using a Layer 3 Switch

```bash
Switch(config)# ip routing
Switch(config)# interface Vlan10
Switch(config-if)# ip address 192.168.10.1 255.255.255.0
Switch(config-if)# no shutdown

Switch(config)# interface Vlan20
Switch(config-if)# ip address 192.168.20.1 255.255.255.0
Switch(config-if)# no shutdown
```

---

## Understanding Subnetting

### What is Subnetting?

Subnetting divides a larger IP network into smaller, manageable subnetworks. This reduces congestion and improves security.

### Subnetting Example

If you have the network **192.168.1.0/24** and need to create two subnets:

- **Subnet 1:** 192.168.1.0/25 (Subnet Mask: 255.255.255.128)
- **Subnet 2:** 192.168.1.128/25 (Subnet Mask: 255.255.255.128)

### Calculating Subnets

Formula: **2^n = Number of subnets**

- **n** is the number of borrowed bits from the host portion.

To split **192.168.1.0/24** into four subnets:

- **New Mask:** /26 (255.255.255.192)
- **Subnets:** 192.168.1.0, 192.168.1.64, 192.168.1.128, 192.168.1.192

### Assigning Subnetted IP Addresses

```bash
Router(config)# interface GigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.192
Router(config-if)# no shutdown
```

---

## Best Practices

- Use VLANs to segment traffic based on department or function.
- Implement **trunking** for scalability while ensuring **pruning** to reduce unnecessary traffic.
- Use **Layer 3 switching** for efficient inter-VLAN routing instead of relying on a router.
- Apply proper **subnetting** to optimize IP address allocation and reduce broadcast traffic.

---


VLANs and subnetting are crucial for network design and management. By implementing VLANs, configuring inter-VLAN routing, and applying proper subnetting techniques, you can enhance performance, security, and scalability in Cisco-based networks.

