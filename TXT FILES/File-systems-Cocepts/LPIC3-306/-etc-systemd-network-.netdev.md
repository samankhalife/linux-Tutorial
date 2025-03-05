# /etc/systemd/network/*.netdev
The `/etc/systemd/network/*.netdev` files are used for configuring **network devices** in `systemd-networkd`. These files define network devices such as virtual network interfaces, bridges, VLANs, bonding, and other specialized network devices. A `.netdev` file specifies settings related to the creation and configuration of these devices, which are then managed by the `systemd-networkd` service.

### Overview of `/etc/systemd/network/*.netdev` Files

These `.netdev` files are used to define virtual network devices or network interfaces that are not automatically detected or managed by systemd. Examples include:
- **Bridges**
- **VLANs**
- **Bonds**
- **Tunnels**
- **Virtual devices** like virtual Ethernet interfaces (veth)

### Basic Structure of a `.netdev` File

A `.netdev` file typically consists of multiple sections that define different aspects of the network device. The key sections usually involve setting up the type of device, parameters for the device, and additional properties.

Here is the basic structure of a `.netdev` file:

```ini
[NetDev]
Name=bridge0
Kind=bridge

[Bridge]
STP=enabled
```

### Common Sections in a `.netdev` File

1. **[NetDev]**
   - This section specifies the type and name of the network device.
   - The **`Kind`** field specifies the type of the device, which can be:
     - `bridge`: For configuring a network bridge.
     - `bond`: For configuring network bonding.
     - `vlan`: For configuring VLAN interfaces.
     - `tunnel`: For configuring tunneling devices (e.g., GRE, VXLAN, etc.).
     - `macvlan`: For configuring a MACVLAN device.
     - `veth`: For configuring a virtual Ethernet device (commonly used in containers).

   - Common keys in this section:
     - `Name`: Specifies the name of the device (e.g., `bridge0`, `bond0`, `vlan10`, etc.).
     - `Kind`: The type of device (bridge, bond, vlan, tunnel, etc.).

   **Example:**
   ```ini
   [NetDev]
   Name=br0
   Kind=bridge
   ```

2. **[Bridge]**
   - This section is used when creating a **bridge** device. It configures bridge-specific settings.
   - Common keys in this section:
     - `STP`: Spanning Tree Protocol (`enabled` or `disabled`).
     - `ForwardDelaySec`: The delay for forwarding decisions in the bridge (usually a default value).
   
   **Example:**
   ```ini
   [Bridge]
   STP=enabled
   ```

3. **[VLAN]**
   - This section is used when creating a **VLAN** device.
   - Common keys in this section:
     - `VLANId`: The VLAN ID (e.g., `10` for VLAN 10).
   
   **Example:**
   ```ini
   [VLAN]
   VLANId=10
   ```

4. **[Bond]**
   - This section is used when configuring a **bonding** device.
   - Common keys in this section:
     - `Mode`: The bonding mode (e.g., `balance-rr`, `active-backup`, `802.3ad`, etc.).
     - `MIIMonitorSec`: The time interval to check for link status.

   **Example:**
   ```ini
   [Bond]
   Mode=802.3ad
   MIIMonitorSec=100ms
   ```

5. **[Tunnel]**
   - This section is used when configuring **tunnel devices** like GRE or VXLAN.
   - Common keys in this section:
     - `Kind`: Tunnel type (e.g., `gre`, `vxlan`).
     - `Local`: The local endpoint IP for the tunnel.
     - `Remote`: The remote endpoint IP for the tunnel.
   
   **Example:**
   ```ini
   [Tunnel]
   Kind=gre
   Local=192.168.1.1
   Remote=192.168.2.1
   ```

6. **[MacVlan]**
   - This section is used when configuring a **macvlan** device.
   - Common keys in this section:
     - `Mode`: The macvlan mode (e.g., `bridge`, `private`, `vepa`, `passthru`).
   
   **Example:**
   ```ini
   [MacVlan]
   Mode=bridge
   ```

### Example Configurations

#### Example 1: Creating a Bridge Device

```ini
[NetDev]
Name=br0
Kind=bridge

[Bridge]
STP=enabled
```

- This configuration creates a bridge interface named `br0` with Spanning Tree Protocol (STP) enabled.

#### Example 2: Creating a Bonding Device

```ini
[NetDev]
Name=bond0
Kind=bond

[Bond]
Mode=active-backup
MIIMonitorSec=100ms
```

- This configuration creates a bonding interface named `bond0` with the `active-backup` mode (failover mode) and link monitoring set to `100ms`.

#### Example 3: Creating a VLAN Device

```ini
[NetDev]
Name=vlan10
Kind=vlan

[VLAN]
VLANId=10
```

- This configuration creates a VLAN device named `vlan10` with VLAN ID 10.

#### Example 4: Creating a Virtual Ethernet (veth) Pair

```ini
[NetDev]
Name=veth0
Kind=veth

[NetDev]
Name=veth1
Kind=veth
```

- This configuration creates a pair of virtual Ethernet interfaces `veth0` and `veth1`, typically used in containerized environments to create network bridges between containers.

#### Example 5: Configuring a GRE Tunnel

```ini
[NetDev]
Name=gre0
Kind=tunnel

[Tunnel]
Kind=gre
Local=192.168.1.1
Remote=192.168.2.1
```

- This configuration creates a GRE tunnel `gre0` with `192.168.1.1` as the local endpoint and `192.168.2.1` as the remote endpoint.

### Applying Changes

To apply the changes after modifying or adding `.netdev` files, you need to restart or reload `systemd-networkd`:

```bash
sudo systemctl restart systemd-networkd
```

Alternatively, you can reload the configurations:

```bash
sudo networkctl reload
```

### Conclusion

The `.netdev` files under `/etc/systemd/network/` are used to configure various network devices in `systemd-networkd`, such as bridges, bonds, VLANs, macvlan, tunnels, and virtual Ethernet devices. These files provide a structured way to manage network devices directly and allow detailed configuration for complex network setups, especially in server environments and containerized applications.
