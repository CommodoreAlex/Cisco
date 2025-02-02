# Router and Switch Configuration (Cisco Packet Tracer & Real-World)

## Introduction

Configuring Cisco routers and switches is a fundamental skill for network engineers and system administrators. This guide covers essential commands and best practices for **both Packet Tracer and real-world devices** to help you manage Cisco network infrastructure effectively.

---

## 0. Networking Cables / Interfaces

**Interfaces** are the ports on a router, switch, or other device that allow communication with other devices on the network.

- **Physical Interfaces**: These are actual ports (e.g., `GigabitEthernet0/1`) where you plug in network cables like Ethernet cables (Cat5e, Cat6).
- **Logical Interfaces**: Virtual ports, such as loopback or VLAN interfaces, that don’t correspond to physical connections.

**Network Cables**: These connect the physical interfaces of different devices, enabling them to send and receive data.

Example:
1. A **router** interface (`GigabitEthernet0/1`) is connected to a **switch** via a network cable.
2. Data flows from the router’s interface, through the cable, to the switch.
3. The switch then sends the data to connected devices (e.g., computers) via its own interfaces.

In short: **Interfaces are the ports on devices, and network cables physically connect them to enable communication.**

💡 **Packet Tracer Tip**:  
To connect devices in Packet Tracer, use the **"Connections" tool**. Select the appropriate cable (e.g., **straight-through cable** for a router to switch, **crossover cable** for connecting two routers) and click on the devices to establish the connection.

Types of networking cables:
- **Straight-Through**: Different devices (router to switch, computer to switch).
- **Crossover**: Similar devices (router to router, switch to switch).
- **Fiber Optic**: High-speed, long-distance communication.
- **Coaxial**: Older networking and cable TV.
- **Patch Cable**: Short connections (typically straight-through).
- **USB Cable**: Device management and configuration.
## 1. Configuring a Router

### 1.1 Assigning an IP Address to an Interface

To configure an IP address on a router interface:
```bash
configure terminal
interface GigabitEthernet0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

Verify with:
```bash
show ip interface brief
```

💡 **Packet Tracer Tip:**

- Click the router, go to the **CLI tab**, and enter the above commands.
- Use the **"Connections" tool** and select a **crossover cable** when connecting two routers.

### 1.2 Setting Up Static Routing

For small networks, static routes are useful:
```bash
configure terminal
ip route 192.168.2.0 255.255.255.0 192.168.1.2
exit
```

Verify with:
```bash
show ip route
```

💡 **Packet Tracer Tip:**

- Ensure that the **next-hop router** has a corresponding return route.
- Use **pings** to test connectivity between networks.

### 1.3 Configuring Dynamic Routing (OSPF Example)

OSPF (Open Shortest Path First) is a link-state routing protocol used to find the best path for data transmission within an IP network by exchanging routing information between routers.

For larger networks, dynamic routing is preferred:
```bash
configure terminal
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
exit
```

Verify with:
```bash
show ip ospf neighbor
```

💡 **Real-World Insight:**

- OSPF automatically **learns** new routes, reducing manual configuration.
- Ensure all OSPF routers have **matching area numbers**.

---

## 2. Configuring a Switch

### 2.1 Assigning a Hostname

```bash
configure terminal
hostname Switch01
exit
```

### 2.2 Setting Up VLANs

Creating VLANs to segment network traffic:
```bash
configure terminal
vlan 10
name Sales
exit
vlan 20
name IT
exit
```

Verify VLANs:
```bash
show vlan brief
```

💡 **Packet Tracer Tip:**

- Use the **"Add PC"** tool and assign VLANs using **static IPs** to simulate network segmentation.

### 2.3 Assigning VLANs to Ports

```bash
configure terminal
interface GigabitEthernet0/1
switchport mode access
switchport access vlan 10
exit
```

Verify port VLAN assignment:
```bash
show interfaces GigabitEthernet0/1 switchport
```

💡 **Real-World Insight:**

- VLANs help isolate network traffic, improving security and performance.
- Ensure inter-VLAN routing is enabled via a **Layer 3 device (Router-on-a-Stick or L3 switch).**

### 2.4 Configuring Trunk Ports

A trunk port is a network port that carries traffic for multiple VLANs, allowing the switch to transmit data for different VLANs over a single link.

To allow VLAN traffic between switches:
```bash
configure terminal
interface GigabitEthernet0/24
switchport mode trunk
switchport trunk allowed vlan 10,20
exit
```

Verify trunk configuration:
```bash
show interfaces trunk
```

💡 **Packet Tracer Tip:**

- Use the **"Connections" tool** and select a **straight-through cable** when connecting **switches** via trunk links.

### 2.5 Enabling SSH Access

```bash
configure terminal
ip domain-name example.com
crypto key generate rsa modulus 2048
username admin privilege 15 secret Cisco123
line vty 0 4
transport input ssh
login local
exit
```

Verify SSH access:
```bash
show ip ssh
```

💡 **Real-World Insight:**

- **Disable Telnet** and use only **SSH** for secure remote access.
- Ensure **SSH version 2** is enabled for enhanced security.

To disable Telnet on a switch or router in Packet Tracer, you can follow these steps:

### 3.0 Disabling Telnet Access

Enter global configuration mode:
```bash
Switch> enable
Switch# configure terminal
```

Disable Telnet by disabling the VTY (Virtual Terminal) lines:
```bash
Switch(config)# no transport input telnet
```

(Optional) You can also secure the VTY lines by requiring a password:
```bash
Switch(config)# line vty 0 15
Switch(config-line)# password yourpassword
Switch(config-line)# login
```

Exit configuration mode:
```bash
Switch(config-line)# exit
Switch(config)# exit
```

Now Telnet will be disabled for all remote access to the device.

---

## 3. Saving and Managing Configurations

### 3.1 Saving the Configuration

```bash
write memory
```

Or:
```bash
copy running-config startup-config
```

### 3.2 Restoring a Saved Configuration

```bash
copy startup-config running-config
```

### 3.3 Resetting to Factory Defaults

```bash
write erase
reload
```

---


Whether you're working in a simulated lab or configuring production hardware, these commands provide a strong foundation for managing Cisco routers and switches.
