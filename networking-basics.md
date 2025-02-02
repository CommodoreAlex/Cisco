# Networking Basics

Networking is a fundamental aspect of system administration. This guide covers essential concepts that every system administrator should understand when working with Cisco networking devices.

## 1. OSI and TCP/IP Models

Understanding how data flows through a network is crucial. The OSI and TCP/IP models provide structured frameworks for network communication.

### OSI Model (7 Layers):

1. **Physical Layer** - Cables, switches, and physical transmission.
2. **Data Link Layer** - MAC addresses, Ethernet, and switches.
3. **Network Layer** - IP addressing, routing, and subnetting.
4. **Transport Layer** - TCP/UDP, flow control, and error handling.
5. **Session Layer** - Manages communication sessions.
6. **Presentation Layer** - Data format translation and encryption.
7. **Application Layer** - Interfaces with applications (HTTP, FTP, DNS).

### TCP/IP Model (4 Layers):

8. **Network Interface** - Equivalent to OSI’s Physical and Data Link layers.
9. **Internet Layer** - Handles IP addressing and routing (OSI’s Network Layer).
10. **Transport Layer** - Ensures end-to-end communication (TCP, UDP).
11. **Application Layer** - Includes application protocols like HTTP, FTP, and SMTP.

## 2. IP Addressing and Subnetting

IP addressing is essential for network communication:
- **IPv4**: 32-bit address format (e.g., 192.168.1.1).
- **IPv6**: 128-bit address format (e.g., 2001:db8::ff00:42:8329).

### Subnetting:

Subnetting divides a network into smaller segments, improving efficiency and security.

**Subnet Mask**: Defines the network and host portions of an IP address.

Example: `255.255.255.0` means the first three octets are the network.

**CIDR Notation**: Alternative to subnet masks (e.g., `/24` = `255.255.255.0`).

- **Subnet Calculation Example:**
    - Network: `192.168.1.0/24`
    - Usable IPs: `192.168.1.1` - `192.168.1.254`
    - Broadcast Address: `192.168.1.255`

## 3. MAC Addressing and ARP

- **MAC Address**: Unique hardware identifier for network devices.
- **ARP (Address Resolution Protocol)**: Maps IP addresses to MAC addresses.


Example Command:
```cmd
arp -a  # Displays ARP table in Windows
```

## 4. Switching vs. Routing

### **Switching (Layer 2):**

- Operates at the Data Link layer.
- Uses MAC addresses to forward frames.
- No concept of IP addresses.

### **Routing (Layer 3):**

- Operates at the Network layer.
- Uses IP addresses to forward packets between networks.
- Requires routing protocols like RIP, OSPF, or BGP.

## 5. DNS, DHCP, and NAT

### **DNS (Domain Name System)**:

- Resolves domain names to IP addresses.
- Example: `www.google.com → 142.250.190.46`

Command:
```cmd
nslookup google.com
```

### **DHCP (Dynamic Host Configuration Protocol)**:

- Assigns IP addresses dynamically.
- Reduces manual IP configuration effort.

### **NAT (Network Address Translation)**:

- Translates private IPs to public IPs for internet access.

- Types:
    - **Static NAT**: One-to-one mapping.
    - **Dynamic NAT**: Uses a pool of public IPs.
    - **PAT (Port Address Translation)**: Maps multiple private IPs to a single public IP.

## Summary

Networking basics are foundational for system administrators. Understanding OSI/TCP-IP models, IP addressing, MAC addressing, switching, routing, and core protocols like DNS, DHCP, and NAT is essential for managing Cisco networks.
