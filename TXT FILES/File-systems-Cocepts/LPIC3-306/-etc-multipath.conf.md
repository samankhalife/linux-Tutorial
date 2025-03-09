# /etc/multipath.conf
`/etc/multipath.conf` is the configuration file for the **Device Mapper Multipath** daemon (`multipathd`), which manages multipath I/O (Input/Output) in Linux systems. Multipath I/O allows a system to utilize multiple physical paths to storage devices, providing failover and load balancing capabilities for high-availability setups and performance improvements.

### Purpose of `multipath.conf`

- **Manage Multipath Devices**:  
  This file configures how multipath devices are detected and handled, defining multipath policies, device path selection algorithms, and error recovery mechanisms.

- **Enhance Redundancy and Performance**:  
  By utilizing multiple paths to the same storage device, `multipath.conf` ensures redundancy in case of path failures, as well as performance improvements through path load balancing.

### Key Configuration Sections

1. **Defaults**  
   Defines global settings for multipath devices.
   
   ```bash
   defaults {
       user_friendly_names yes
       find_multipaths yes
       path_selector "round-robin 0"
   }
   ```

   - `user_friendly_names`: Assigns human-readable aliases to multipath devices instead of the default complex identifiers.
   - `find_multipaths`: Automatically enables multipathing for devices that present multiple paths.
   - `path_selector`: Specifies the algorithm for selecting the path to use, such as `round-robin`.

2. **Multipaths**  
   Configures specific settings for individual multipath devices, identified by their `wwid` (World Wide Identifier).

   ```bash
   multipaths {
       multipath {
           wwid 3600508b1001cce8d0000900000a22000
           alias mpath1
           path_grouping_policy multibus
           path_checker tur
           failback immediate
       }
   }
   ```

   - `wwid`: Unique identifier for the multipath device.
   - `alias`: Human-readable name for the multipath device.
   - `path_grouping_policy`: Specifies how paths are grouped. `multibus` means all paths are in a single group.
   - `path_checker`: Method used to verify the health of paths. Common options are `tur` (Test Unit Ready) and `readsector0`.
   - `failback`: Controls the behavior when a failed path becomes healthy again (`immediate` means immediately switch back to the preferred path).

3. **Blacklists**  
   Defines devices that should be excluded from multipathing, either by device name, WWID, or device type.

   ```bash
   blacklist {
       devnode "^sda"
       wwid 3600508b1001cce8d0000900000a22000
   }
   ```

   - `devnode`: Prevents the device `/dev/sda` from being managed by `multipathd`.
   - `wwid`: Blacklists specific devices based on their unique identifier.

4. **Devices**  
   This section provides per-device defaults for specific storage device types, which can override global settings.

   ```bash
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

   - `vendor` and `product`: Specifies the type of storage device (in this case, a Dell MD3000).
   - `prio_callout`: Defines the script to determine the priority of each path.
   - `no_path_retry`: Specifies how many retries should occur before giving up on a failed path.

### Example Configuration

Here’s a sample configuration file that illustrates typical multipath settings for redundancy and load balancing.

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

### Key Sections of `multipath.conf`

1. **Defaults**:  
   Defines general behavior for all multipath devices, such as naming conventions, failover policies, and path selection algorithms.

2. **Multipaths**:  
   Configures per-device multipath behavior using the device's `wwid`. This section allows the customization of specific devices, overriding the global settings in the `defaults` section.

3. **Blacklists**:  
   Blacklists are useful when excluding specific devices or paths from being handled by the multipath daemon. You can use this section to exclude certain devices (like local storage) from multipathing.

4. **Devices**:  
   This section is for vendor-specific overrides, typically used to apply device-specific configurations. This can be crucial for optimizing the behavior of multipathing for specific types of storage arrays.

### Key Options Explained

- **`user_friendly_names`**:  
  If set to `yes`, multipath devices are assigned names like `mpath0`, `mpath1`, instead of long WWIDs.
  
- **`path_selector`**:  
  The algorithm used for path selection. Common values include:
  - `round-robin 0`: Alternates I/O requests between all available paths.
  - `service-time 0`: Selects the path with the shortest estimated service time.

- **`path_checker`**:  
  Specifies the method used to check the health of the path:
  - `tur` (Test Unit Ready): Common for modern storage arrays.
  - `readsector0`: Reads the first sector of the device to check health.

- **`failback`**:  
  Controls the behavior when a previously failed path recovers:
  - `immediate`: Immediately switch back to the preferred path.
  - `manual`: Only switch back when manually triggered.

- **`no_path_retry`**:  
  Specifies the number of times to retry a failed path before giving up. Can be set to `fail` to not retry, or `queue` to queue I/O indefinitely while waiting for a path to recover.

### Best Practices

- **Blacklist Local Disks**:  
  In many configurations, local disks (e.g., `/dev/sda`) should be blacklisted to avoid confusion, as they do not require multipathing.

- **Device-Specific Settings**:  
  Ensure that storage devices have appropriate configurations based on vendor recommendations, as different storage arrays may require specific settings for optimal performance and stability.

- **Monitoring**:  
  Regularly monitor the health of multipath devices using the `multipath -ll` or `multipath -v3` commands to ensure all paths are healthy and behaving as expected.

### Conclusion

The `/etc/multipath.conf` file allows for fine-grained control over how multipath devices are managed on a Linux system, improving redundancy, performance, and fault tolerance. By properly configuring multipath devices and paths, system administrators can ensure high availability and optimized performance for critical storage systems.
