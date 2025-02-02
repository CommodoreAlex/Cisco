# Cisco Packet Tracer & Real-World Device Setup

This guide walks you through setting up a **Cisco router or switch** in both **Cisco Packet Tracer** and real-world environments. It covers connecting to the device, navigating the CLI, and performing initial configurations.

---

## **Hardware Selection Advisory**

In Packet Tracer, choose routers, switches, and other devices based on the required features and network complexity. While basic devices perform similar tasks, advanced models offer specific capabilities (e.g., routing protocols, VLANs, security). Select hardware that matches the scenario’s needs to ensure realistic and efficient simulations

In short: Hardware selection in Packet Tracer matters primarily for simulating specific features or protocols, but most devices can handle basic tasks without significant impact on functionality.

## 1. Connecting to a Cisco Device

### Using a Console Cable (Real-World)

For initial setup, use a **console cable** and a terminal emulator:

1. **Connect** the console cable to the **console port** of the Cisco device and the **USB/serial port** of your PC.
2. Open a terminal emulator like **PuTTY** (Windows) or **Minicom** (Linux/Mac).
3. Set the connection parameters:
    - **Baud rate**: 9600
    - **Data bits**: 8
    - **Parity**: None
    - **Stop bits**: 1
    - **Flow control**: None
4. Press **Enter** to access the CLI.

### Using the CLI in Packet Tracer

Open **Cisco Packet Tracer** and **drag a router/switch** into the workspace:
![1](https://github.com/user-attachments/assets/f57f39b0-5108-40c5-9817-aea5bb046ee1)


Click the device and go to the **CLI tab** to start configuration:
![2](https://github.com/user-attachments/assets/83d952d0-1a26-4b79-a776-a53b28300522)


Notice the message when you open the CLI tab (optional pathway):
![3](https://github.com/user-attachments/assets/7674ab3f-ce69-4879-a0dd-922b598249d7)

The initial configuration dialog for routers and switches in Packet Tracer typically covers the following key areas:

1. **Hostname**: Sets the device name for identification.
2. **Passwords**: Configures basic security, including setting enable and console passwords.
3. **IP Addressing**: Optionally assigns an IP address to the device's interfaces for network connectivity.
4. **Interfaces**: Allows configuration of specific interfaces, such as enabling or disabling them.
5. **Routing**: Optionally configures routing protocols (e.g., RIP, OSPF) for the router.
6. **Management**: Sets up remote management access via protocols like Telnet or SSH.
7. **Exit/Save**: Prompts you to save the configuration or exit without saving.

This initial dialog helps quickly configure the device for basic operations, often serving as a starting point for further detailed setup.


---

## 2. Basic CLI Navigation

|Command|Description|
|---|---|
|`enable`|Enter privileged EXEC mode|
|`disable`|Exit privileged mode|
|`configure terminal`|Enter global configuration mode|
|`exit`|Exit the current mode|
|`show running-config`|View current configuration|
|`show startup-config`|View saved configuration|
|`write memory`|Save configuration|

---


## **Router Modes and Commands Overview:**

1. **User EXEC Mode (`Router>`)**:
    - This is the default mode when you first access the router. It's for basic commands like checking statuses or performing simple tests.
    - You can only run commands like `show` or `ping` here.

2. **Privileged EXEC Mode (`Router#`)**:
    - To enter this mode, type `enable` from User EXEC Mode.
    - In this mode, you can run more advanced commands like `show running-config`, `show interfaces`, and access configuration modes.
    - **Command**: `enable`

3. **Global Configuration Mode (`Router(config)#`)**:
    - After entering Privileged EXEC Mode, type `configure terminal` to access this mode.
    - This mode is where you configure device settings like hostname, interfaces, routing, etc.
    - **Command**: `configure terminal`

4. **Interface Configuration Mode (`Router(config-if)#`)**:
    - Used to configure specific interfaces (e.g., `GigabitEthernet0/1`).
    - You access it from Global Configuration Mode by typing `interface [interface-name]`.
    - **Command**: `interface GigabitEthernet0/1`

5. **Line Configuration Mode (`Router(config-line)#`)**:
    - Used to configure lines (console, VTY) for remote or local access.
    - You access it from Global Configuration Mode by typing `line console 0` or `line vty 0 4`.
    - **Command**: `line console 0` or `line vty 0 4`

Once you are in the appropriate mode, you can configure things like the hostname, for example:
```shell
Router(config)# hostname MyCiscoDevice
MyCiscoDevice(config)#
```

This is what will happen if you don't enter the correct routing modes (you will fail to make changes):
![4](https://github.com/user-attachments/assets/e8a4d54c-6748-4a5c-bce8-2029b5fb9491)


---

### Typical Flow to Configure the Router:

**Enter User EXEC Mode**:
```shell
Router> 
```

**Enter Privileged EXEC Mode**:
```shell
Router> enable
Router#
```

**Enter Global Configuration Mode**:
```shell
Router# configure terminal
Router(config)#
```

**Enter Interface Configuration Mode (if needed)**:
```shell
Router(config)# interface GigabitEthernet0/1
Router(config-if)#
```

Once in the correct mode, you'll be able to enter commands like `hostname`, configure interfaces, and other settings without seeing the invalid input errors!

## 3. Initial Device Configuration

### Setting a Hostname

```bash
configure terminal
hostname MyCiscoDevice
exit
```

### Creating a Secure Password

```bash
configure terminal
enable secret MyStrongPassword
exit
```

### Creating a User Account

```bash
configure terminal
username admin privilege 15 secret StrongPass123
exit
```

### Assigning an IP Address to an Interface

```bash
configure terminal
interface GigabitEthernet0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

### Enabling SSH for Remote Access

```bash
configure terminal
ip domain-name mynetwork.local
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 4
transport input ssh
login local
exit
```

### Using SSH (If Enabled)

If SSH is enabled, connect remotely:
```bash
ssh admin@<device-ip>
```

### Saving the Configuration

```bash
write memory
```

---

## 4. Upgrading the IOS Firmware (Real-World)

Download the latest IOS firmware from **Cisco.com** and transfer it using **TFTP**:

```bash
copy tftp://<server-ip>/ios-image.bin flash:
```

Set the new IOS image as the boot file:

```bash
configure terminal
boot system flash:/ios-image.bin
exit
```

Save and reboot:

```bash
write memory
reload
```

---

## 5. Resetting a Cisco Device to Factory Defaults

If you need to reset the device:

```bash
write erase
reload
```

Confirm the reload when prompted.
