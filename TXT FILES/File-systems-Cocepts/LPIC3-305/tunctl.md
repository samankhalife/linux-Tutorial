# `tunctl` — TUN/TAP Device Control Utility

## What is `tunctl`?

`tunctl` is a userspace utility from the **`uml-utilities`** package that allows administrators to **create and delete TUN/TAP network interfaces**. These interfaces are commonly used in **virtual networking**, VPNs, and **User Mode Linux (UML)** setups.

- **TUN** = Network layer device (IP packets)
- **TAP** = Data link layer device (Ethernet frames)

---

## Typical Use Cases

| Use Case                     | Description                                       |
|------------------------------|---------------------------------------------------|
| Virtual Machine Networking   | Bridge TAP interfaces to VMs for layer-2 traffic |
| VPN Software                 | Create secure point-to-point tunnels             |
| Network Emulation            | Used in labs and testbeds for simulating networks|
| Container Networking         | Lightweight setup for L2/L3 interfaces            |

---

## Key Commands

### 1. **Create a TAP Interface**

```bash
sudo tunctl -t tap0
```
Creates a TAP device named `tap0`.

### 2. **Create TAP Device with Owner**

```bash
sudo tunctl -u username -t tap0
```
Assigns ownership of the device to `username` so that unprivileged users can access it.

### 3. **Delete TAP Interface**

```bash
sudo tunctl -d tap0
```
Removes the `tap0` device.

---

## After Creation: Bring Interface Up

```bash
sudo ip link set tap0 up
sudo ip addr add 192.168.100.1/24 dev tap0
```

Or use with a bridge:

```bash
sudo brctl addif br0 tap0
```

---

## Alternatives to `tunctl`

| Tool         | Description                                            |
|--------------|--------------------------------------------------------|
| `ip tuntap`  | Modern equivalent via `iproute2`. Replaces `tunctl`.  |
| `openvpn`    | Manages tun/tap internally for VPNs.                  |
| `bridge-utils` | Works in combination with tap interfaces.           |

### Example with `ip tuntap`:
```bash
sudo ip tuntap add dev tap0 mode tap user $(whoami)
sudo ip link set tap0 up
```

---

## Dependency

`tunctl` is part of the `uml-utilities` package:

```bash
# Debian/Ubuntu
sudo apt install uml-utilities

# RHEL/CentOS/Fedora
sudo dnf install tunctl (may need EPEL or similar)
```

---

## Summary

| Feature         | tunctl                     |
|------------------|----------------------------|
| Role             | Create/delete TUN/TAP interfaces |
| Scope            | Virtual networking (L2/L3)  |
| Replacement      | `ip tuntap` (recommended modern alternative) |
| Common Use Cases | VMs, VPNs, emulated networks |
