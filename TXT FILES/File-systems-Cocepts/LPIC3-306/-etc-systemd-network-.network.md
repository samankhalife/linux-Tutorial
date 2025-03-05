# /etc/systemd/network/*.network
The `/etc/systemd/network/*.network` files are used for configuring **network interfaces** with **systemd-networkd**, a system service in `systemd` that manages network configurations. These `.network` files define how network interfaces should behave, including network addresses, routes, and other networking-related settings.

### Overview of `/etc/systemd/network/*.network` files

These configuration files are typically stored in the `/etc/systemd/network/` directory, and each file typically corresponds to a network interface or a specific configuration group. The `.network` files allow administrators to configure various networking options for both Ethernet and Wi-Fi interfaces, such as IP addressing, routes, and DNS settings.

### Basic Structure of a `.network` File

A `.network` file typically consists of multiple sections that define different aspects of the network interface.

Here is the basic structure of a `.network` file:

```ini
[Match]
Name=eth0

[Network]
DHCP=yes

[DHCP]
ClientIdentifier=mac
```

### Common Sections in a `.network` File

1. **[Match]**
   - This section specifies the criteria to match the network interface. You can match by interface name, MAC address, or other attributes.
   - Common keys in this section:
     - `Name`: Specifies the name of the network interface (e.g., `eth0`, `enp0s3`).
     - `MACAddress`: Matches based on the MAC address.
     - `Driver`: Matches based on the network driver used.

   **Example:**
   ```ini
   [Match]
   Name=enp0s3
   ```

2. **[Network]**
   - This section defines the network configuration for the matched interface. You specify settings like IP addressing, routes, DNS, etc.
   - Common keys in this section:
     - `DHCP`: Enable or disable DHCP (set to `yes` or `no`).
     - `Address`: Assign static IP addresses.
     - `Gateway`: Define the default gateway.
     - `DNS`: Define DNS servers.
     - `Routes`: Add specific routes to be used.

   **Example:**
   ```ini
   [Network]
   DHCP=yes
   ```

   Or for static IP configuration:
   ```ini
   [Network]
   Address=192.168.1.100/24
   Gateway=192.168.1.1
   DNS=8.8.8.8
   ```

3. **[DHCP]**
   - This section provides specific DHCP client settings. It is only relevant when `DHCP=yes` in the `[Network]` section.
   - Common keys in this section:
     - `ClientIdentifier`: The identifier used by the DHCP client (usually MAC address or a custom identifier).
     - `Hostname`: The hostname assigned by DHCP.
     - `UseDNS`: Whether to use DNS information provided by DHCP.

   **Example:**
   ```ini
   [DHCP]
   ClientIdentifier=mac
   ```

4. **[Link]**
   - This section provides settings that control the interface link properties.
   - Common keys in this section:
     - `MTUBytes`: Set the Maximum Transmission Unit (MTU).
     - `WakeOnLan`: Enable or disable Wake-on-LAN.

   **Example:**
   ```ini
   [Link]
   MTUBytes=1500
   ```

5. **[VLAN]**
   - Used to configure VLAN interfaces.
   - Common keys in this section:
     - `VLANId`: The VLAN ID for this interface.

   **Example:**
   ```ini
   [VLAN]
   VLANId=10
   ```

### Example `.network` File Configurations

#### Example 1: Using DHCP for Network Configuration

```ini
[Match]
Name=enp0s3

[Network]
DHCP=yes
```

- This configuration automatically assigns an IP address to the `enp0s3` interface using DHCP.

#### Example 2: Static IP Configuration

```ini
[Match]
Name=enp0s3

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
```

- This configuration assigns a static IP address `192.168.1.100/24` to `enp0s3`, with a gateway at `192.168.1.1` and a DNS server at `8.8.8.8`.

#### Example 3: Using Static IP with Multiple Addresses

```ini
[Match]
Name=enp0s3

[Network]
Address=192.168.1.100/24
Address=192.168.2.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
```

- This configuration assigns two IP addresses to the interface `enp0s3`, `192.168.1.100/24` and `192.168.2.100/24`, and uses the same gateway and DNS.

#### Example 4: VLAN Configuration

```ini
[Match]
Name=enp0s3

[VLAN]
VLANId=10

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
```

- This configuration creates a VLAN interface with the ID `10` on the `enp0s3` interface and assigns it a static IP address.

### File Naming Convention

Network configuration files in `/etc/systemd/network/` typically follow a naming convention like `XX-<interface>.network`, where `XX` is a numeric prefix to control the order in which configurations are applied, and `<interface>` is the network interface name. Files with more specific names will override more generic configurations.

For example:
- `10-eth0.network`
- `20-wlan0.network`

### Applying Changes

To apply the changes made to `.network` files, you need to restart the `systemd-networkd` service:

```bash
sudo systemctl restart systemd-networkd
```

Alternatively, to reload the configurations without fully restarting:

```bash
sudo networkctl reload
```

### Conclusion

The `.network` files under `/etc/systemd/network/` are used to configure various aspects of network interfaces, such as IP addressing, DNS, and routes, using `systemd-networkd`. These files are an alternative to traditional network management tools like `ifup`/`ifdown` or `NetworkManager`, and are especially useful in server environments or minimal installations where you prefer direct control over network configurations.
