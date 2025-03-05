# /etc/sysconfig/networking-scripts/ifcfg-*
The `/etc/sysconfig/networking-scripts/ifcfg-*` files are used for configuring network interfaces on **Red Hat-based Linux distributions** (such as RHEL, CentOS, Fedora, and others). These configuration files define network settings for each network interface and are processed by **NetworkManager** or the **network** service to configure and bring up network interfaces during system boot or when network settings are modified.

### Overview of `/etc/sysconfig/networking-scripts/ifcfg-*` Files

Each `ifcfg-*` file corresponds to a specific network interface (e.g., `ifcfg-eth0`, `ifcfg-enp0s3`, `ifcfg-eth1`, etc.) and contains key-value pairs that specify configuration details such as IP addressing, DNS settings, interface status, and more.

These configuration files are generally used for **static IP configuration**, but can also be used for **DHCP**, **bonding**, **VLANs**, **bridging**, and other complex networking setups.

### Structure of `ifcfg-*` Files

The basic structure of an `ifcfg-*` file consists of key-value pairs, where each line defines a specific network configuration option. Below are the commonly used parameters and examples of their configuration.

#### Common Parameters

- **DEVICE**: The name of the network interface (e.g., `eth0`, `enp0s3`).
- **BOOTPROTO**: Defines how the network interface obtains its IP address.
  - `none`: Static IP.
  - `dhcp`: Dynamically via DHCP.
- **ONBOOT**: Determines whether the network interface is activated at boot.
  - `yes`: Activate on boot.
  - `no`: Do not activate on boot.
- **IPADDR**: The static IP address to be assigned to the interface (used with `BOOTPROTO=none`).
- **NETMASK**: The subnet mask for the interface (used with `BOOTPROTO=none`).
- **GATEWAY**: The default gateway for the network (used with `BOOTPROTO=none`).
- **DNS1/DNS2**: Primary and secondary DNS servers.
- **HWADDR**: The MAC address of the network interface.
- **MTU**: The Maximum Transmission Unit size.
- **TYPE**: The type of network interface (e.g., `Ethernet` or `Bridge`).
- **VLAN**: Used to define VLAN interfaces.

#### Example Configurations

1. **Static IP Configuration** (no DHCP)

   ```ini
   DEVICE=eth0
   BOOTPROTO=none
   ONBOOT=yes
   IPADDR=192.168.1.100
   NETMASK=255.255.255.0
   GATEWAY=192.168.1.1
   DNS1=8.8.8.8
   DNS2=8.8.4.4
   ```

   - This configuration sets a static IP address `192.168.1.100` for the `eth0` interface with a netmask `255.255.255.0`, default gateway `192.168.1.1`, and DNS servers `8.8.8.8` and `8.8.4.4`.

2. **DHCP Configuration**

   ```ini
   DEVICE=eth0
   BOOTPROTO=dhcp
   ONBOOT=yes
   ```

   - This configuration uses DHCP to automatically obtain an IP address for the `eth0` interface when the system boots.

3. **VLAN Configuration**

   If you're using VLANs, you can create a virtual network interface by adding a `VLAN` configuration.

   ```ini
   DEVICE=eth0.10
   BOOTPROTO=none
   ONBOOT=yes
   VLAN=yes
   IPADDR=192.168.10.100
   NETMASK=255.255.255.0
   GATEWAY=192.168.10.1
   ```

   - This configuration creates a VLAN interface `eth0.10` for VLAN ID 10 with a static IP configuration.

4. **Bonding Configuration**

   For network bonding, you typically have two or more physical interfaces that are bonded together for increased throughput or redundancy. The configuration for the bonding interface is done using the `ifcfg-bond0` file.

   **Bonding configuration (`ifcfg-bond0`)**:

   ```ini
   DEVICE=bond0
   TYPE=Bond
   BOOTPROTO=none
   ONBOOT=yes
   BONDING_OPTS="mode=1 miimon=100"
   IPADDR=192.168.1.200
   NETMASK=255.255.255.0
   GATEWAY=192.168.1.1
   ```

   **Slave interface configurations** (`ifcfg-eth0`, `ifcfg-eth1`):

   ```ini
   DEVICE=eth0
   MASTER=bond0
   SLAVE=yes
   ONBOOT=yes

   DEVICE=eth1
   MASTER=bond0
   SLAVE=yes
   ONBOOT=yes
   ```

   - This setup creates a bonded interface `bond0` using two physical interfaces (`eth0` and `eth1`). The bonding options specify `mode=1` (active-backup mode) and `miimon=100` (link monitoring interval of 100ms).

5. **Bridge Configuration**

   For configuring a bridge interface, you would typically configure `ifcfg-br0` and the physical interfaces connected to the bridge.

   **Bridge configuration (`ifcfg-br0`)**:

   ```ini
   DEVICE=br0
   TYPE=Bridge
   BOOTPROTO=none
   ONBOOT=yes
   IPADDR=192.168.1.10
   NETMASK=255.255.255.0
   GATEWAY=192.168.1.1
   ```

   **Physical interface configuration (`ifcfg-eth0`)**:

   ```ini
   DEVICE=eth0
   BOOTPROTO=none
   ONBOOT=yes
   BRIDGE=br0
   ```

   - This configuration creates a bridge `br0` and adds `eth0` to it, enabling the bridge interface to obtain a static IP.

### Network Configuration File Naming

Each interface configuration file in `/etc/sysconfig/networking-scripts/` is named as `ifcfg-<interface_name>`, where `<interface_name>` is the name of the network interface (e.g., `ifcfg-eth0`, `ifcfg-enp0s3`, `ifcfg-bond0`, `ifcfg-br0`).

### Other Configuration Files

Besides the `ifcfg-*` files, there are also a couple of other files that might be used in the networking scripts:

- **/etc/sysconfig/network**: Defines general network settings like the hostname, gateway, and network mode.
- **/etc/sysconfig/network-scripts/ifup-eth* and ifdown-eth***: Scripts that define actions to bring interfaces up or down.

### Managing Network Interfaces

To apply changes made to the `ifcfg-*` files, you can use the following commands:

- **Restart network service**:

  ```bash
  sudo systemctl restart network
  ```

- **Bring up an interface manually**:

  ```bash
  sudo ifup eth0
  ```

- **Bring down an interface manually**:

  ```bash
  sudo ifdown eth0
  ```

### Conclusion

The `/etc/sysconfig/networking-scripts/ifcfg-*` files are central to configuring network interfaces on Red Hat-based Linux distributions. These files enable static IP configuration, DHCP, VLANs, bonding, bridges, and other advanced networking setups. After editing these files, network interfaces can be brought up or down manually, or the system can be restarted to apply the changes at boot.
