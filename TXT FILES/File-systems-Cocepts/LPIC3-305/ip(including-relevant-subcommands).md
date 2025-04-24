The `ip` command in Linux is a powerful and flexible tool for network configuration and management. It is used for a wide range of tasks related to networking, such as assigning IP addresses, routing, managing network interfaces, and controlling network devices. The `ip` command is part of the `iproute2` package, which is the preferred set of utilities for network management on Linux.

### Overview of the `ip` Command

The basic syntax of the `ip` command is:

```bash
ip [ OPTIONS ] OBJECT [ COMMAND ]
```

Where:
- **OPTIONS**: Optional flags and parameters to modify the behavior of the command.
- **OBJECT**: The type of object to operate on (e.g., `link`, `addr`, `route`).
- **COMMAND**: The action to perform on the object (e.g., `add`, `delete`, `show`).

### Common Subcommands and Use Cases

#### 1. **`ip link` - Manage Network Interfaces**

The `ip link` command is used to manage network interfaces. This includes actions like bringing interfaces up or down, setting interface parameters, and viewing interface details.

- **Show all network interfaces**:
  
  ```bash
  ip link show
  ```

- **Bring an interface up**:

  ```bash
  ip link set dev eth0 up
  ```

- **Bring an interface down**:

  ```bash
  ip link set dev eth0 down
  ```

- **Change interface MTU (Maximum Transmission Unit)**:

  ```bash
  ip link set dev eth0 mtu 1400
  ```

- **Rename a network interface**:

  ```bash
  ip link set dev eth0 name newname
  ```

#### 2. **`ip addr` - Manage IP Addresses**

The `ip addr` command is used to show and configure IP addresses assigned to network interfaces.

- **Show IP addresses for all interfaces**:

  ```bash
  ip addr show
  ```

- **Assign an IP address to an interface**:

  ```bash
  ip addr add 192.168.1.100/24 dev eth0
  ```

- **Delete an IP address from an interface**:

  ```bash
  ip addr del 192.168.1.100/24 dev eth0
  ```

- **Assign an alias (secondary IP address)**:

  ```bash
  ip addr add 192.168.1.101/24 dev eth0 label eth0:0
  ```

#### 3. **`ip route` - Manage Routing Table**

The `ip route` command is used to view and modify the system's routing table. This is useful for controlling how network traffic is directed.

- **Show the routing table**:

  ```bash
  ip route show
  ```

- **Add a new route**:

  ```bash
  ip route add 192.168.2.0/24 via 192.168.1.1
  ```

- **Delete a route**:

  ```bash
  ip route del 192.168.2.0/24
  ```

- **Add a default route**:

  ```bash
  ip route add default via 192.168.1.1
  ```

#### 4. **`ip link set` - Change Link Parameters**

This command allows you to modify the configuration of a network interface.

- **Set the interface to promisc mode (for packet sniffing)**:

  ```bash
  ip link set dev eth0 promisc on
  ```

- **Disable promiscuous mode**:

  ```bash
  ip link set dev eth0 promisc off
  ```

#### 5. **`ip addr flush` - Remove IP Addresses**

This command is used to remove all IP addresses from a network interface.

- **Flush all IP addresses from an interface**:

  ```bash
  ip addr flush dev eth0
  ```

#### 6. **`ip link set` - Change Interface MTU**

You can adjust the Maximum Transmission Unit (MTU) size for network interfaces.

- **Set MTU size for an interface**:

  ```bash
  ip link set dev eth0 mtu 1500
  ```

#### 7. **`ip maddr` - Manage Multicast Addresses**

The `ip maddr` command is used to show and configure multicast addresses for network interfaces.

- **Show multicast addresses**:

  ```bash
  ip maddr show
  ```

- **Add a multicast address to an interface**:

  ```bash
  ip maddr add 224.0.0.1 dev eth0
  ```

- **Delete a multicast address from an interface**:

  ```bash
  ip maddr del 224.0.0.1 dev eth0
  ```

#### 8. **`ip tunnel` - Manage Tunnels**

Tunnels allow network packets to be encapsulated for transmission over a network.

- **Create a new GRE tunnel**:

  ```bash
  ip tunnel add gre1 mode gre remote 192.168.1.1 local 192.168.1.2
  ```

- **Bring up a tunnel interface**:

  ```bash
  ip link set gre1 up
  ```

- **Delete a tunnel**:

  ```bash
  ip tunnel del gre1
  ```

#### 9. **`ip netns` - Manage Network Namespaces**

Network namespaces allow the creation of isolated network environments.

- **Create a new network namespace**:

  ```bash
  ip netns add ns1
  ```

- **Assign a network interface to a namespace**:

  ```bash
  ip link set eth0 netns ns1
  ```

- **List all network namespaces**:

  ```bash
  ip netns list
  ```

#### 10. **`ip link set dev` - Change Interface States**

- **Set interface to up**:

  ```bash
  ip link set dev eth0 up
  ```

- **Set interface to down**:

  ```bash
  ip link set dev eth0 down
  ```

### Advanced Examples

- **Show all IP addresses for a specific interface**:

  ```bash
  ip addr show dev eth0
  ```

- **Set the default route to a new gateway**:

  ```bash
  ip route add default via 192.168.1.1
  ```

- **Add a static route to a network**:

  ```bash
  ip route add 10.10.10.0/24 via 192.168.1.1
  ```

- **Change the MTU of an interface**:

  ```bash
  ip link set dev eth0 mtu 1400
  ```

- **Remove an interface's IP address**:

  ```bash
  ip addr del 192.168.1.100/24 dev eth0
  ```

### Conclusion

The `ip` command is an essential tool for network management on Linux systems. It offers a broad range of functionalities, including managing network interfaces, routing, and IP addresses. Mastering this tool is crucial for anyone managing Linux network configurations, whether for personal use or in large-scale enterprise environments.
