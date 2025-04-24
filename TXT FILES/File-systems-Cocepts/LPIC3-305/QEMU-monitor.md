# `QEMU Monitor`

## What is the QEMU Monitor?

The **QEMU Monitor** is a command-line interface (CLI) that provides control over a running QEMU virtual machine (VM). Through the QEMU monitor, users can interact with the VM to perform administrative tasks such as managing the virtual machine's resources, configuring devices, or inspecting the system's state.

It is similar to a console for managing a QEMU virtual machine (VM) and allows for tasks like pausing, resuming, and shutting down a VM, as well as querying hardware information, managing snapshots, and performing other low-level operations.

### Key Features of the QEMU Monitor
- **Control and Management**: Pause, resume, or reset the virtual machine.
- **Inspection**: View and modify the state of the virtual machine, including memory, CPU, and devices.
- **Device Management**: Add, remove, or configure virtual devices (e.g., disk, network interfaces, serial ports).
- **Snapshotting**: Create, list, and manage snapshots.
- **State Queries**: Get information about the VM's running state (e.g., CPU usage, memory usage, and device status).

---

## Accessing the QEMU Monitor

There are several ways to access the QEMU monitor depending on how the VM is started.

1. **Through the `-monitor` option**:
   You can specify how the QEMU monitor is accessed when launching a virtual machine using the `-monitor` option:

   ```bash
   qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -monitor stdio
   ```

   - **`-monitor stdio`**: This option makes the monitor accessible through the terminal (standard input/output).
   - **Other options** include:
     - **`-monitor telnet::port`**: Open a monitor session over a TCP connection.
     - **`-monitor unix:/path/to/socket`**: Use Unix domain sockets for communication.

2. **Via the QEMU Monitor Console**:
   Once the monitor is accessible, you can enter commands interactively by typing them directly into the monitor console.

---

## Common QEMU Monitor Commands

### 1. **Help Command**

To get a list of available monitor commands, you can type:

```bash
help
```

This will return a list of commands available in the QEMU monitor, such as `info`, `device_add`, and `quit`.

### 2. **Exit/Quit the Monitor**

To exit the QEMU monitor, type:

```bash
quit
```

This will exit the monitor interface and terminate the QEMU process. You can also use `exit` or `Ctrl+D` to quit the monitor.

### 3. **View VM Information**

To get information about the virtual machine's status, such as the CPU, memory, and devices, use:

```bash
info
```

To get more detailed information on a specific aspect, you can query subcommands like:

- **`info cpus`**: Lists CPU information.
- **`info mem`**: Displays memory usage.
- **`info block`**: Shows information about block devices.

### 4. **Pause/Resume the Virtual Machine**

To pause the virtual machine:

```bash
stop
```

To resume the virtual machine:

```bash
cont
```

### 5. **Shutdown the Virtual Machine**

To gracefully shut down the virtual machine (equivalent to issuing a shutdown command inside the guest OS):

```bash
system_powerdown
```

### 6. **Reset the Virtual Machine**

To reset the virtual machine:

```bash
system_reset
```

This command will restart the VM, similar to pressing the reset button on a physical machine.

### 7. **Managing Virtual Devices**

You can manage virtual devices in a QEMU VM using monitor commands. Some examples include:

- **Add a new device**:
  ```bash
  device_add pci-bridge,id=pcie.0,bus=pcie.0
  ```
- **Remove a device**:
  ```bash
  device_del <device-id>
  ```

### 8. **Managing Snapshots**

Snapshots allow you to save the current state of a virtual machine and return to that state later. Some common snapshot-related commands include:

- **Take a snapshot**:
  ```bash
  snapshot_save snapshot-name
  ```

- **List snapshots**:
  ```bash
  snapshot_list
  ```

- **Revert to a snapshot**:
  ```bash
  snapshot_load snapshot-name
  ```

- **Delete a snapshot**:
  ```bash
  snapshot_delete snapshot-name
  ```

### 9. **Changing VM Configuration (e.g., CPU and Memory)**

While a VM is running, you can modify its configuration:

- **Add memory**:
  ```bash
  memory_add 512M
  ```
  This command adds 512MB of memory to the VM.

- **Change CPU**:
  ```bash
  cpu_add 1
  ```

### 10. **Access the Virtual Machine’s Console**

You can access the serial console of the virtual machine using the monitor interface:

```bash
console
```

This command will redirect the output to the VM’s console.

---

## Example Use Case

### Pausing and Resuming a VM

1. Start the VM with a monitor interface:

   ```bash
   qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -monitor stdio
   ```

2. In the QEMU monitor console, pause the VM:

   ```bash
   stop
   ```

3. Perform any necessary actions (e.g., check the VM state, change configurations).
   
4. Resume the VM:

   ```bash
   cont
   ```

### Taking and Reverting Snapshots

1. Start the VM with a monitor interface:

   ```bash
   qemu-system-x86_64 -hda /path/to/disk-image.qcow2 -m 2048 -monitor stdio
   ```

2. While the VM is running, take a snapshot:

   ```bash
   snapshot_save my-snapshot
   ```

3. Later, you can revert to the snapshot:

   ```bash
   snapshot_load my-snapshot
   ```

---

## Additional Resources

For a complete list of QEMU monitor commands, refer to the official documentation:

- **QEMU Monitor Documentation**: [QEMU Monitor Interface](https://qemu.readthedocs.io/en/latest/system/monitor.html)

The monitor interface is a powerful tool for controlling and managing virtual machines in real-time, making it an essential feature for advanced QEMU users.
