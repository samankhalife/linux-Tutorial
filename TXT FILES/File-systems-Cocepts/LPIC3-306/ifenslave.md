# `ifenslave` Command

The `ifenslave` command is used to attach and detach slave network interfaces to a bonding device in Linux. Bonding, also known as network interface aggregation or NIC teaming, is a method that allows multiple network interfaces to be aggregated into a single logical interface, providing redundancy and potentially increased throughput.

## Basic Usage

```bash
ifenslave [OPTIONS] BOND_INTERFACE SLAVE_INTERFACE [SLAVE_INTERFACE...]
```

- **BOND_INTERFACE**: The bonding interface to which you want to attach or detach slave interfaces (e.g., `bond0`).
- **SLAVE_INTERFACE**: One or more network interfaces that you want to enslave (attach) to the bonding device.

## Example Usage

### 1. **Attach (enslave) interfaces to a bond**

To attach `eth0` and `eth1` to a bonding interface called `bond0`:

```bash
sudo ifenslave bond0 eth0 eth1
```

This command adds both `eth0` and `eth1` as slaves to the bonding interface `bond0`.

### 2. **Detach (release) a slave from a bond**

To detach `eth0` from the `bond0` interface:

```bash
sudo ifenslave -d bond0 eth0
```

This command releases `eth0` from the bonding interface.

## Bonding Configuration

The bonding interface must first be created and configured in the system. Here is a basic setup for bonding:

1. **Create the bond interface configuration** in `/etc/network/interfaces` (Debian/Ubuntu) or the appropriate configuration files in your distribution. 

```bash
# Example for Debian/Ubuntu /etc/network/interfaces
auto bond0
iface bond0 inet static
    address 192.168.1.10
    netmask 255.255.255.0
    bond-slaves eth0 eth1
    bond-mode 802.3ad
    bond-miimon 100
    bond-lacp-rate fast
```

- **bond-mode**: Specifies the bonding mode. Common modes include:
  - `balance-rr`: Round-robin (transmission load balancing).
  - `active-backup`: Only one slave is active, others are backup.
  - `balance-xor`: XOR hashing for load balancing.
  - `802.3ad`: IEEE 802.3ad dynamic link aggregation (LACP).
  
- **bond-miimon**: Specifies the monitoring frequency (in milliseconds) to check the status of each slave.
- **bond-lacp-rate**: Specifies the rate of LACP packets (used for 802.3ad mode).

2. **Restart networking services** or use the `ifup` command to activate the configuration.

```bash
sudo ifup bond0
```

### 3. **View bonding status**

To see the current bonding status, including which slaves are attached and their statuses:

```bash
cat /proc/net/bonding/bond0
```

This will show details about the bonding interface, such as active slaves, bonding mode, and link status of each interface.

## Bonding Modes

- **balance-rr (0)**: Round-robin policy, traffic is transmitted in order across all slaves, providing load balancing and fault tolerance.
- **active-backup (1)**: Only one slave is active at a time. If the active interface fails, another slave is activated. This provides fault tolerance.
- **balance-xor (2)**: Transmit based on XOR of source and destination MAC addresses, provides load balancing and fault tolerance.
- **broadcast (3)**: Sends traffic on all slaves, providing fault tolerance.
- **802.3ad (4)**: IEEE 802.3ad Dynamic link aggregation. Requires a switch that supports Link Aggregation Control Protocol (LACP).
- **balance-tlb (5)**: Adaptive transmit load balancing, dynamically balances outgoing traffic based on the load on each slave.
- **balance-alb (6)**: Adaptive load balancing, includes both transmit and receive load balancing for IPv4 traffic.

## Conclusion

The `ifenslave` command is an essential tool for managing bonded interfaces in Linux. It allows you to easily attach and detach network interfaces to a bond, enabling network redundancy and load balancing. Bonding interfaces, when configured correctly, can improve network performance and reliability in environments where high availability is a priority.
