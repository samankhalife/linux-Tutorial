# bonding.ko
The `bonding.ko` module in Linux is responsible for network interface bonding, which is a technique for combining multiple network interfaces into a single virtual interface. This is typically used for increasing network throughput, providing fault tolerance, and improving network reliability. The `bonding.ko` kernel module is commonly used with **Ethernet interfaces** and can be configured to operate in various bonding modes.

### Key Features of `bonding.ko`:

- **Load balancing**: Distributes traffic across multiple interfaces to increase throughput.
- **Failover**: Provides redundancy by automatically switching to a backup interface if the active one fails.
- **Team-based networking**: Allows for a single logical interface combining multiple physical interfaces.
- **Automatic interface failover**: Automatically switches to a backup network interface in case of failure.

### Loading the `bonding.ko` module

To use network bonding, the `bonding.ko` module needs to be loaded into the kernel. You can load the module with the following command:

```bash
sudo modprobe bonding
```

To verify that the bonding module is loaded, you can check with:

```bash
lsmod | grep bonding
```

Alternatively, you can check the system logs using `dmesg`:

```bash
dmesg | grep bonding
```

### Module Options for `bonding.ko`

The `bonding.ko` module can be configured with a variety of options when it is loaded. Here are some common options:

1. **mode=<mode>**: Defines the bonding mode (load balancing or failover strategy). Valid values are:
   - `mode=0`: **Round-robin** (balance-rr) - Transmit packets in a round-robin manner across the interfaces.
   - `mode=1`: **Active-backup** (failover) - One interface is active, and others are backups. If the active interface fails, a backup interface is used.
   - `mode=2`: **XOR** (balance-xor) - Transmit packets based on the XOR of the MAC address of the sender and receiver, providing load balancing and fault tolerance.
   - `mode=3`: **Broadcast** - Send all traffic on all interfaces, providing fault tolerance.
   - `mode=4`: **802.3ad (LACP)** - Use the **IEEE 802.3ad** Link Aggregation Control Protocol (LACP) for dynamic link aggregation.
   - `mode=5`: **Adaptive transmit load balancing** (balance-tlb) - Distribute outbound traffic based on the current load.
   - `mode=6`: **Adaptive load balancing** (balance-alb) - A combination of both adaptive transmit and receive load balancing.

   Example:

   ```bash
   sudo modprobe bonding mode=1
   ```

2. **miimon=<milliseconds>**: Specifies the monitoring frequency for link status, in milliseconds. This is used in modes that require active monitoring of interfaces, such as `active-backup`, `balance-alb`, and `balance-tlb`.
   - Example: Monitor the interface link every 100 milliseconds:
   
   ```bash
   sudo modprobe bonding miimon=100
   ```

3. **updelay=<milliseconds>**: Defines how long to wait before bringing up a backup interface after a failure is detected.
   - Example: 200 milliseconds delay before bringing up a backup interface:
   
   ```bash
   sudo modprobe bonding updelay=200
   ```

4. **downdelay=<milliseconds>**: Defines how long to wait before taking down a failed interface. Typically used in `active-backup` mode.
   - Example: 200 milliseconds delay before taking down a failed interface:
   
   ```bash
   sudo modprobe bonding downdelay=200
   ```

5. **fail_over_mac=<mac-address>**: Specifies the MAC address to use for failover purposes in `active-backup` mode.
   - Example:
   
   ```bash
   sudo modprobe bonding fail_over_mac=00:11:22:33:44:55
   ```

6. **arp_interval=<seconds>**: Defines the interval for sending ARP requests when using ARP monitoring in the `active-backup` mode. This helps in detecting link failure.
   - Example: Set ARP interval to 200 seconds:
   
   ```bash
   sudo modprobe bonding arp_interval=200
   ```

7. **arp_ip_target=<ip-address>**: Specifies the target IP address for ARP monitoring.
   - Example: Monitor the IP address `192.168.1.1` for link failure:
   
   ```bash
   sudo modprobe bonding arp_ip_target=192.168.1.1
   ```

8. **lacp_rate=<fast|slow>**: Specifies the rate at which the Link Aggregation Control Protocol (LACP) packets are sent, used in `802.3ad` mode.
   - `fast`: Sends LACP packets every 1 second.
   - `slow`: Sends LACP packets every 30 seconds.
   - Example:
   
   ```bash
   sudo modprobe bonding lacp_rate=fast
   ```

9. **primary=<interface>**: Specifies the primary interface in an `active-backup` configuration. This is the interface that will be used as long as it is up and functional.
   - Example:
   
   ```bash
   sudo modprobe bonding primary=eth0
   ```

10. **xmit_hash_policy=<policy>**: Defines how the outgoing traffic is distributed across the slave interfaces. Common policies include:
    - `layer2`: Use the MAC address for hashing.
    - `layer3+4`: Use the IP addresses and ports for hashing.
    - Example:
    
    ```bash
    sudo modprobe bonding xmit_hash_policy=layer3+4
    ```

11. **miimon=<milliseconds>**: Sets the link monitoring frequency for detecting link failures. Used in most bonding modes, especially in `balance-tlb`, `balance-alb`, and `active-backup`.

    ```bash
    sudo modprobe bonding miimon=100
    ```

### Example: Configuring Bonding on a System

Here’s an example of how to configure bonding on a system with two network interfaces (`eth0` and `eth1`) using the `active-backup` mode with monitoring:

```bash
sudo modprobe bonding mode=1 miimon=100 updelay=200 downdelay=200 primary=eth0
```

This would configure bonding with the following settings:
- **Active-backup mode** (`mode=1`)
- Link monitoring every 100 milliseconds (`miimon=100`)
- 200 milliseconds delay to bring up a backup interface (`updelay=200`)
- 200 milliseconds delay to take down a failed interface (`downdelay=200`)
- `eth0` is the primary interface (`primary=eth0`)

### Creating a Bonding Interface Configuration

After loading the bonding module and setting the appropriate options, you can configure the bonding interface in the `/etc/network/interfaces` file or the **systemd network configuration** (depending on your system's setup).

For example, the `/etc/network/interfaces` configuration for bonding might look like this:

```ini
# /etc/network/interfaces

# Loopback interface
auto lo
iface lo inet loopback

# Bonding interface eth0 + eth1
auto bond0
iface bond0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    bond-mode 1
    bond-miimon 100
    bond-updelay 200
    bond-downdelay 200
    bond-primary eth0
    slaves eth0 eth1
```

This configuration would create a bonding interface `bond0`, use `eth0` and `eth1` as slaves, and apply the previously mentioned bonding settings.

### Conclusion

The `bonding.ko` module allows you to combine multiple network interfaces into one virtual interface for enhanced performance and fault tolerance. It supports various bonding modes, such as active-backup, round-robin, and 802.3ad LACP, and can be configured with a variety of options, including link monitoring, delays, and primary interface settings. The configuration can be done using the `modprobe` command to set module options or by adding settings to the appropriate network configuration files.
