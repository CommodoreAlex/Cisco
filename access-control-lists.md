# Access Control Lists (ACLs)

Access Control Lists (ACLs) are a fundamental part of network security, allowing administrators to filter and control network traffic based on predefined rules. ACLs improve security by permitting or denying specific traffic based on IP addresses, protocols, and ports.

ACLs are commonly configured on **Cisco routers and Layer 3 switches**, which you can simulate in **Cisco Packet Tracer** or implement in a real network environment.

---

## 1. Types of ACLs

### Standard ACLs

- Filter traffic based only on the **source IP address**.
- Typically applied **close to the destination**.
- Numbered **1-99** and **1300-1999** (extended range).
- Used on **routers** or **Layer 3 switches** to control access.

Example (on a Cisco router or switch):
```bash
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny any
```

### Extended ACLs

- Filter traffic based on **source and destination IP, protocol, and port numbers**.
- Typically applied **close to the source**.
- Numbered **100-199** and **2000-2699** (extended range).
- Used for **firewall-like filtering** on **routers and Layer 3 switches**.

Example (blocking all traffic except HTTP from a subnet):
```bash
access-list 110 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 110 deny ip any any
```

---

## 2. Applying ACLs to Interfaces

Once an ACL is created, it must be applied to an interface in either an **inbound** or **outbound** direction.

### Syntax:

```bash
ip access-group <ACL_NUMBER> {in|out}
```

Example (applying an ACL to **GigabitEthernet0/1** on a **Cisco router** or **Layer 3 switch**):
```bash
interface GigabitEthernet0/1
 ip access-group 110 in
```

- **Inbound ACLs** filter packets before they enter the router.
- **Outbound ACLs** filter packets before they exit the router.

---

## 3. Named ACLs

Named ACLs provide better readability and management compared to numbered ACLs.

Example:
```bash
ip access-list extended WEB-ACCESS
 permit tcp any any eq 80
 deny ip any any
```

Applying it to an interface:
```bash
interface GigabitEthernet0/1
 ip access-group WEB-ACCESS in
```

Named ACLs are recommended for complex configurations as they are easier to modify and understand.

---

## 4. Verifying and Managing ACLs

### Viewing ACLs on a **Cisco router or Layer 3 switch**:

```bash
show access-lists
```

### Removing ACLs:

```bash
no access-list 110
```

To remove an ACL from an interface:
```bash
interface GigabitEthernet0/1
 no ip access-group 110 in
```

---

## 5. Best Practices for ACLs

- **Place Standard ACLs close to the destination** to minimize impact on other traffic.
- **Place Extended ACLs close to the source** to block unwanted traffic early.
- **Always include the 'deny any any' rule** at the end of extended ACLs for security.
- **Use named ACLs for better clarity** in large networks.
- **Regularly audit and document ACLs** to prevent misconfigurations and security gaps.

---

By effectively using ACLs, system administrators can enhance security and control over network traffic. This knowledge applies both in **Cisco Packet Tracer simulations** and **real-world network environments**. Next, we will cover **Routing Protocols** to optimize network efficiency and scalability.
