# `ip` Command

The `ip` command in Linux is used to display and manipulate routing, network devices, interfaces, and tunnels. It is a powerful utility provided by the `iproute2` package and is considered a replacement for the older `ifconfig` and `route` commands.

## Common Usage

```bash
ip [OPTIONS] OBJECT { COMMAND | help }
```

- **OBJECT**: Specifies the type of object to manipulate or view (e.g., `address`, `link`, `route`).
- **COMMAND**: The action to be performed on the object (e.g., `add`, `delete`, `show`).

## Common OBJECTs

1. **`link`**: Manage network interfaces.
2. **`addr`**: Display and configure IP addresses.
3. **`route`**: Manipulate the routing table.
4. **`neigh`**: Display and manipulate ARP entries (neighbor cache).
5. **`maddr`**: Manage multicast addresses.
6. **`rule`**: Manage rule-based routing.
7. **`tunnel`**: Configure tunnel interfaces (e.g., GRE, IPIP).

## Basic Examples

### 1. **Display Network Interfaces (Link)**

To view the status of all network interfaces:

```bash
ip link show
```

This will show a list of all network interfaces, including their statuses (up, down), and other information like MTU (Maximum Transmission Unit).

To view a specific interface:

```bash
ip link show dev eth0
```

### 2. **Display IP Addresses**

To view all IP addresses configured on the system:

```bash
ip addr show
```

This shows IP addresses for all interfaces, including IPv4 and IPv6 addresses. To view details for a specific interface:

```bash
ip addr show dev eth0
```

### 3. **Assign IP Address to Interface**

To assign an IP address to an interface, use the following syntax:

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

This command assigns the IP `192.168.1.100` with a subnet mask of `255.255.255.0` to the `eth0` interface.

### 4. **Delete an IP Address from Interface**

To remove an IP address from an interface:

```bash
sudo ip addr del 192.168.1.100/24 dev eth0
```

### 5. **Bring Interface Up or Down**

To bring an interface up (enable it):

```bash
sudo ip link set dev eth0 up
```

To bring an interface down (disable it):

```bash
sudo ip link set dev eth0 down
```

### 6. **Display Routing Table**

To view the system's routing table:

```bash
ip route show
```

This will display the routing table entries, including default gateways and other routes.

### 7. **Add a Static Route**

To add a new static route to a network:

```bash
sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
```

This adds a route to the `192.168.2.0/24` network through the gateway `192.168.1.1` using the `eth0` interface.

### 8. **Delete a Static Route**

To delete a static route:

```bash
sudo ip route del 192.168.2.0/24
```

### 9. **Configure a Default Gateway**

To set a default gateway:

```bash
sudo ip route add default via 192.168.1.1 dev eth0
```

This configures `192.168.1.1` as the default gateway for all outbound traffic.

### 10. **Display ARP Cache (Neighbor Entries)**

To display the ARP (Address Resolution Protocol) cache:

```bash
ip neigh show
```

### 11. **Flush IP Addresses**

To flush all IP addresses on an interface:

```bash
sudo ip addr flush dev eth0
```

## Advanced Examples

### 1. **View Multicast Group Memberships**

To view the multicast group memberships on an interface:

```bash
ip maddr show dev eth0
```

### 2. **Configure Policy Routing**

To add a rule that routes traffic from a specific source IP through a specific table:

```bash
sudo ip rule add from 192.168.1.100 table 100
```

Then, configure the routes for table `100`:

```bash
sudo ip route add default via 192.168.1.1 dev eth0 table 100
```

### 3. **Configure Tunnels**

To configure a GRE tunnel:

```bash
sudo ip tunnel add gre1 mode gre remote 192.168.2.1 local 192.168.1.100 ttl 255
sudo ip link set gre1 up
sudo ip addr add 10.10.10.1/30 dev gre1
```

This sets up a GRE tunnel between `192.168.1.100` (local) and `192.168.2.1` (remote).

## IP Command Syntax Overview

- **`ip link`**: Manage network interfaces (view, up/down, configure).
- **`ip addr`**: Manage IP addresses (view, add, delete).
- **`ip route`**: Manage the routing table (view, add, delete, change).
- **`ip neigh`**: Manage neighbor cache (ARP entries).
- **`ip maddr`**: Manage multicast addresses.

## Conclusion

The `ip` command provides a versatile and modern way to manage network configurations in Linux. By replacing older utilities such as `ifconfig` and `route`, it offers a more consistent and extensible way to handle network interfaces, IP addresses, routes, and tunnels. It is a crucial tool for Linux system administrators and network engineers.
