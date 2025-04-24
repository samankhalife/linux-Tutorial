# `ip` — Network Management Command

## What is `ip`?

The `ip` command is a powerful, versatile tool used to configure and manage network interfaces, routes, IP addresses, and other network-related tasks on Linux systems. It is part of the **iproute2** package, which provides modern tools for network management, replacing older tools like `ifconfig`, `route`, and `netstat`.

`ip` offers a wide range of functionalities for network configuration and troubleshooting, including the management of network interfaces, routing tables, network addresses, tunnels, and more.

---

## Key Features of `ip`

- **Interface Management**: View and modify network interfaces, assign IP addresses, bring interfaces up or down.
- **Routing**: View and configure network routes and IP forwarding.
- **Network Address Management**: Assign and remove IP addresses to network interfaces.
- **Multicast and Tunnels**: Handle multicast addresses and set up network tunnels.
- **Advanced Options**: Provides detailed control over various networking features, including link-layer configuration and quality of service.

---

## Basic Syntax

```bash
ip [options] OBJECT {COMMAND | help}
```

Where:
- **OBJECT** is the network object (e.g., `link`, `addr`, `route`).
- **COMMAND** is the action you want to perform (e.g., `show`, `add`, `del`).

---

## Common `ip` Subcommands

### 1. **`ip link` — Manage Network Interfaces**

Used to manage network interfaces (e.g., Ethernet, Wi-Fi, virtual interfaces).

#### Example Commands

- **Show all network interfaces**:
  ```bash
  ip link show
  ```

- **Bring an interface up**:
  ```bash
  sudo ip link set eth0 up
  ```

- **Bring an interface down**:
  ```bash
  sudo ip link set eth0 down
  ```

- **Change the MAC address of an interface**:
  ```bash
  sudo ip link set eth0 address 00:11:22:33:44:55
  ```

- **Enable promiscuous mode**:
  ```bash
  sudo ip link set eth0 promisc on
  ```

### 2. **`ip addr` — Manage IP Addresses**

Used to manage IP addresses assigned to network interfaces.

#### Example Commands

- **Show all IP addresses**:
  ```bash
  ip addr show
  ```

- **Add an IP address**:
  ```bash
  sudo ip addr add 192.168.1.100/24 dev eth0
  ```

- **Remove an IP address**:
  ```bash
  sudo ip addr del 192.168.1.100/24 dev eth0
  ```

- **Assign an IP address with a specific scope**:
  ```bash
  sudo ip addr add 192.168.1.100/24 dev eth0 scope global
  ```

### 3. **`ip route` — Manage Routing Tables**

Used to display and modify routing tables.

#### Example Commands

- **Show the routing table**:
  ```bash
  ip route show
  ```

- **Add a route**:
  ```bash
  sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
  ```

- **Delete a route**:
  ```bash
  sudo ip route del 192.168.2.0/24 via 192.168.1.1 dev eth0
  ```

- **Add a default route**:
  ```bash
  sudo ip route add default via 192.168.1.1
  ```

### 4. **`ip link set` — Change Interface Settings**

Used to change the settings of network interfaces (e.g., bring interfaces up/down, assign addresses).

#### Example Commands

- **Set an interface to promiscuous mode**:
  ```bash
  sudo ip link set eth0 promisc on
  ```

- **Set an interface to non-promiscuous mode**:
  ```bash
  sudo ip link set eth0 promisc off
  ```

- **Change interface MTU (Maximum Transmission Unit)**:
  ```bash
  sudo ip link set eth0 mtu 1500
  ```

### 5. **`ip tunnel` — Create Tunnels**

Used to manage IP tunnels (e.g., GRE tunnels, IPsec tunnels).

#### Example Commands

- **Create a GRE tunnel**:
  ```bash
  sudo ip tunnel add tun0 mode gre remote 192.168.1.1 local 192.168.1.2
  sudo ip link set tun0 up
  ```

- **Show tunnel information**:
  ```bash
  ip tunnel show
  ```

### 6. **`ip link set` — Set Interface Attributes**

You can set various attributes of network interfaces, including the interface’s name, MTU, and MAC address.

#### Example Commands

- **Set a new name for the interface**:
  ```bash
  sudo ip link set eth0 name new_eth0
  ```

---

## Example Use Cases

### Use Case 1: Configuring a Static IP Address

To set a static IP address on a network interface:

1. **Assign the IP address**:
   ```bash
   sudo ip addr add 192.168.1.100/24 dev eth0
   ```

2. **Bring the interface up**:
   ```bash
   sudo ip link set eth0 up
   ```

3. **Add the default route**:
   ```bash
   sudo ip route add default via 192.168.1.1
   ```

### Use Case 2: Setting Up a Virtual Network Interface

For setting up a virtual interface (e.g., `eth0:0`):

1. **Assign the IP address to the virtual interface**:
   ```bash
   sudo ip addr add 192.168.2.100/24 dev eth0 label eth0:0
   ```

2. **Bring the interface up**:
   ```bash
   sudo ip link set eth0:0 up
   ```

---

## Comparison with Older Tools

| Feature             | `ip` Command                          | `ifconfig`/`route`        |
|---------------------|---------------------------------------|---------------------------|
| Interface Management| Full-featured management              | Limited functionality      |
| IP Address Handling | Advanced capabilities                 | Basic address assignment  |
| Routing             | Advanced routing features             | Limited routing features   |
| Tunnels             | Supports advanced tunnels (GRE, IPsec) | Limited tunnel support     |
| Efficiency          | Preferred tool for modern Linux setups| Deprecated and less efficient |

---

## Alternatives to `ip`

| Tool                | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `ifconfig`          | Older tool for managing network interfaces, largely replaced by `ip`.       |
| `netplan`           | For managing network configuration in newer Ubuntu versions (YAML-based).  |
| `nmcli`             | NetworkManager's command-line interface for managing network connections.  |

---

## Summary

| Feature             | `ip` Command                                  |
|---------------------|-----------------------------------------------|
| Purpose             | Manage network interfaces, addresses, and routes on Linux |
| Common Use Cases    | IP configuration, route management, interface management |
| Alternatives        | `ifconfig`, `nmcli`, `netplan`, `brctl`      |
| Key Commands        | `ip link`, `ip addr`, `ip route`, `ip tunnel` |

---

The `ip` command is a robust and modern tool for network configuration on Linux, offering extensive features for managing interfaces, IP addresses, routing, and more. It is the preferred tool for most modern Linux systems, providing superior functionality compared to older tools like `ifconfig` and `route`.
