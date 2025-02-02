# Cisco Networking Project: Building a Small Business Network in Cisco Packet Tracer

This project will guide you through setting up a small business network in Cisco Packet Tracer. You will configure essential components such as routers, switches, VLANs, ACLs, routing protocols, and security measures, culminating in a fully functional network with secure and segmented traffic.

## Project Overview

You will build a network that includes:

- Two departments (VLANs)
- Inter-VLAN routing
- Static and dynamic routing protocols (RIP or OSPF)
- ACLs to control traffic
- Basic network security
- A backup strategy for the configurations

## Table of Contents

1. [Network Design Overview](#network-design-overview)
2. [Step 1: Cisco Device Setup](#step-1-cisco-device-setup)
3. [Step 2: VLAN and Subnetting Configuration](#step-2-vlan-and-subnetting-configuration)
4. [Step 3: Inter-VLAN Routing](#step-3-inter-vlan-routing)
5. [Step 4: Routing Protocols](#step-4-routing-protocols)
6. [Step 5: Implementing ACLs](#step-5-implementing-acls)
7. [Step 6: Network Security](#step-6-network-security)
8. [Step 7: Backup and Recovery](#step-7-backup-and-recovery)
9. [Step 8: Troubleshooting](#step-8-troubleshooting)

---

## Network Design Overview

The network will consist of:

- **2 VLANs**: One for the Finance department and one for the HR department.
- **1 Router**: Used for inter-VLAN routing.
- **2 Switches**: Connecting devices within each VLAN.
- **PCs**: Representing end devices in each department.
- **Security Measures**: Including ACLs and SSH for secure device management.
- **Backup Strategy**: Using TFTP for configuration backup.

### Network Diagram

- **VLAN 10** - Finance (Subnet: 192.168.10.0/24)
- **VLAN 20** - HR (Subnet: 192.168.20.0/24)
- **Router**: Configured for inter-VLAN routing.
- **Switch 1** - Finance department switch.
- **Switch 2** - HR department switch.
- **PCs**: One in each VLAN for testing connectivity.

---

## Step 1: Cisco Device Setup

### Devices Needed:

- 1 Router (e.g., Cisco 2900 Series)
- 2 Switches (e.g., Cisco 2960 Series)
- 4 PCs

### Connecting the Devices:

**Router to Switches**:
- Use **Ethernet cables** to connect the router to both switches. Connect one end of an Ethernet cable to the router’s gigabit Ethernet interface (e.g., `Gig0/0`) and the other end to the **Uplink port** (usually any port labeled `Gig0/1` or `Gig0/2`) on Switch 1 and Switch 2.
- This allows the router to handle inter-VLAN routing between the two VLANs.

**Switches to PCs**:
- Connect each PC to the corresponding switch using **Ethernet cables**. For **Switch 1** (Finance VLAN), connect PCs (e.g., PC1 and PC2) to available ports on the switch (typically ports `fa0/1` to `fa0/24`). For **Switch 2** (HR VLAN), connect PCs (e.g., PC3 and PC4) to Switch 2 in the same manner.
- Ensure that each switch port is configured to the appropriate VLAN (as shown in Step 2).

**PC to Router for Management** (optional):
- To manage the router, connect a PC to the router’s Ethernet port using an **Ethernet cable**. This is useful if you want to directly configure the router from a PC in the network.

---

## Step 2: VLAN and Subnetting Configuration

### Configuring VLANs on Switches

On each switch, create VLANs and assign ports.

On **Switch 1** (Finance):
```bash
vlan 10
name Finance
exit
interface range fa0/1 - 24
switchport mode access
switchport access vlan 10
exit
```

On **Switch 2** (HR):
```bash
vlan 20
name HR
exit
interface range fa0/1 - 24
switchport mode access
switchport access vlan 20
exit
```

Configure IP addresses on the PCs:
- **PC1 (Finance)**: IP `192.168.10.10/24`, Gateway `192.168.10.1`
- **PC2 (Finance)**: IP `192.168.10.20/24`, Gateway `192.168.10.1`
- **PC3 (HR)**: IP `192.168.20.10/24`, Gateway `192.168.20.1`
- **PC4 (HR)**: IP `192.168.20.20/24`, Gateway `192.168.20.1`

---

## Step 3: Inter-VLAN Routing

### Configure Router for Inter-VLAN Routing

On the router, create sub-interfaces for each VLAN and assign IP addresses:
```bash
interface gig0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit

interface gig0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
```

Enable routing on the router to allow communication between VLANs:
```bash
ip routing
```

---

## Step 4: Routing Protocols

### Implement Static Routing (Optional for Simplicity)

If you want to simulate routing, use **RIP** (Routing Information Protocol):

Enable RIP on the router:
```bash
router rip
version 2
network 192.168.10.0
network 192.168.20.0
exit
```

Alternatively, you can configure **OSPF** for more complex routing.

---

## Step 5: Implementing ACLs

### Configuring Access Control Lists (ACLs)

You can apply an ACL to restrict communication between the Finance and HR departments. For example, allow only the Finance department to access HR resources:

Create an ACL to block communication from Finance (VLAN 10) to HR (VLAN 20):
```bash
access-list 100 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
access-list 100 permit ip any any
```

Apply the ACL to the router interface connecting to Switch 1 (Finance):
```bash
interface gig0/0.10
ip access-group 100 in
exit
```

---

## Step 6: Network Security

### Enable SSH for Secure Management

Configure the router to use SSH for remote management:
```bash
ip domain-name mynetwork.com
crypto key generate rsa
username admin privilege 15 secret mypassword
line vty 0 4
transport input ssh
login local
exit
```

Configure the switches to only allow SSH for management access.

---

## Step 7: Backup and Recovery

### Backing Up Configurations

Use **TFTP** to back up configurations from the router and switches:
```bash
copy running-config tftp:
```

Store backups in a remote server to ensure quick recovery if needed.

### Recovering Configurations

If configurations are lost, restore them from the TFTP server:
```bash
copy tftp: running-config
```

---

## Step 8: Troubleshooting

### Using Troubleshooting Commands

**Ping** devices to test connectivity between VLANs:
```bash
ping 192.168.10.10  # Test from HR PC to Finance PC
```

Use **show** and **debug** commands to identify issues:
```bash
show ip route
show vlan brief
debug ip icmp
```

---


By following these steps, you have built a small but functional network with Cisco Packet Tracer, implementing essential networking components such as VLANs, routing, ACLs, network security, and backup strategies. 

This setup is scalable and can be adapted for larger networks with more VLANs and more advanced routing protocols.
