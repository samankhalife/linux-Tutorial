# multipath
**Multipath I/O (MPIO)** is a technology used in Linux and other operating systems to provide multiple physical paths between a server and its storage. The goal is to enhance the availability and performance of storage systems by allowing multiple paths for data to travel, improving both redundancy and load balancing.

### Key Concepts

1. **Multipath Devices**:  
   A multipath device is a logical device that combines multiple physical paths (e.g., cables, switches) to a storage array. The OS and storage system can communicate with the device using any of these paths, with automatic failover to another path in case one fails.

2. **Path Grouping**:  
   Multipath devices can consist of several "paths" (physical connections), grouped into a single logical device. Path grouping determines how these paths are used for I/O operations.

3. **Failover and Load Balancing**:  
   If one path fails, another path will take over the I/O operations, ensuring high availability. On the other hand, load balancing algorithms allow distributing I/O requests across multiple available paths to optimize performance.

4. **Multipath Daemon**:  
   In Linux, the multipath daemon (`multipathd`) is responsible for managing multipath devices. It handles the discovery of paths, failure detection, and load balancing.

5. **Device Mapper Multipath**:  
   Linux uses the **Device Mapper** to create a virtual device from multiple paths, ensuring that the kernel treats it as a single device. This device is then used by applications like databases and file systems.

### How Multipath Works

1. **Device Discovery**:  
   Multipath discovers devices by looking at their unique World Wide Identifier (WWID) or other characteristics, such as vendor and model. When a device has multiple physical paths, the multipath subsystem treats these as a single logical device.

2. **Path Failover**:  
   If one of the paths fails (e.g., a cable is unplugged), the multipath system will detect the failure and automatically reroute traffic to the next available path, ensuring continuous access to the device.

3. **Path Selection Algorithm**:  
   Path selection algorithms control how traffic is distributed across multiple paths. Common algorithms include:
   - **Round-robin**: I/O operations are alternated between paths in a circular order.
   - **Least Queue Depth**: Selects the path with the least number of pending I/O operations.
   - **Service Time**: Chooses the path with the fastest response time.

4. **Multipath Configuration**:  
   Multipath behavior can be customized by editing configuration files (such as `/etc/multipath.conf`) to set up things like path failover policies, device-specific settings, and blacklist options.

### Configuration Files

- **`/etc/multipath.conf`**:  
  This is the main configuration file for the multipath daemon in Linux. It allows administrators to customize multipath device behavior, set policies for path selection, define device-specific rules, and blacklist certain devices.

### Common Commands for Multipath

- **`multipath`**:  
  This command is used to display the current state of multipath devices.
  ```bash
  multipath -ll
  ```
  This shows detailed information about all multipath devices, including path status and device aliases.

- **`multipath -v3`**:  
  Displays verbose output, showing the internal workings of the multipath subsystem, useful for debugging.

- **`multipathd`**:  
  This is the daemon that manages multipath devices. It can be manually restarted to apply changes or troubleshoot.
  ```bash
  systemctl restart multipathd
  ```

- **`multipath -f <device>`**:  
  This command flushes the multipath device specified, effectively removing it from the multipath list.

### Example `/etc/multipath.conf`

Here is an example configuration file to define how multipath should behave:

```bash
defaults {
    user_friendly_names yes
    find_multipaths yes
    path_selector "round-robin 0"
    failback immediate
    no_path_retry 5
}

blacklist {
    devnode "^sda"
}

multipaths {
    multipath {
        wwid 3600508b1001cce8d0000900000a22000
        alias mpath1
        path_grouping_policy multibus
        path_checker tur
        failback immediate
    }
}

devices {
    device {
        vendor "DELL"
        product "MD3000"
        path_grouping_policy group_by_prio
        path_checker tur
        prio_callout "/sbin/mpath_prio_alua"
        no_path_retry 5
    }
}
```

### Key Sections in `multipath.conf`

- **`defaults`**: Sets global options like `path_selector` for path selection algorithms and `failback` for controlling failover behavior.
- **`multipaths`**: Configures specific multipath devices using their WWID, such as setting aliases and path policies.
- **`blacklist`**: Used to blacklist certain devices, preventing them from being managed by multipath.
- **`devices`**: Used for setting device-specific configurations based on vendor/product.

### Multipath in High Availability (HA) Systems

Multipath I/O is critical in high-availability environments, such as large data centers or cloud environments, where uninterrupted access to storage is vital. By using multiple paths, multipath I/O ensures that if one path fails due to hardware issues (e.g., cable failure or switch malfunction), data traffic will automatically switch to another path, preventing downtime.

### Conclusion

Multipath I/O enhances redundancy, fault tolerance, and performance in storage systems. It is widely used in enterprise environments, where continuous access to storage is necessary, and high-availability and performance optimization are key. By configuring multipath devices correctly and using path selection algorithms, administrators can ensure reliable, optimized access to storage resources.
