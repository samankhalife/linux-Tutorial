# /etc/drbd.d/

The `/etc/drbd.d/` directory is the default location where DRBD (Distributed Replicated Block Device) stores its resource configuration files on many Linux systems. These files define the settings and parameters for each DRBD resource that manages replicated block devices between cluster nodes.



## Purpose

- **Resource Definitions:**  
  The directory contains individual resource files (typically with a `.res` extension) that describe each DRBD resource. These definitions include details such as the resource name, device paths, network settings, and metadata options for both local and remote nodes.

- **Configuration Management:**  
  It allows for modular configuration. Rather than having a single monolithic configuration file, you can manage multiple DRBD resource files separately, making it easier to add, remove, or modify resources as needed.

- **Integration with Global Configuration:**  
  The global DRBD configuration file (usually located at `/etc/drbd.conf`) typically includes a directive to load all configuration files from the `/etc/drbd.d/` directory, ensuring that all resource definitions are applied at startup.



## Typical Structure and Content

- **File Naming:**  
  Resource configuration files are generally named with a `.res` suffix. For example, a resource might be defined in a file like `/etc/drbd.d/myresource.res`.

- **Example Resource File:**

  ```ini
  resource r0 {
      protocol C;
      on node1 {
          device    /dev/drbd0;
          disk      /dev/sda1;
          address   192.168.1.1:7788;
          meta-disk internal;
      }
      on node2 {
          device    /dev/drbd0;
          disk      /dev/sdb1;
          address   192.168.1.2:7788;
          meta-disk internal;
      }
  }
  ```

  In this example:
  - **`resource r0`** defines a DRBD resource named "r0".
  - The **`protocol C`** line specifies the replication protocol.
  - Each **`on <node>`** block provides the configuration for a specific node, including the local DRBD device, disk partition, network address, and metadata storage options.



## How It Works

1. **Global Inclusion:**  
   The main DRBD configuration file (`/etc/drbd.conf`) usually contains an inclusion directive such as:
   ```ini
   include "drbd.d/*.res";
   ```
   This instructs DRBD to read all resource definition files within the `/etc/drbd.d/` directory.

2. **Dynamic Configuration:**  
   When DRBD starts, it parses the files in `/etc/drbd.d/` to initialize and manage each defined resource. Any changes to these files typically require a DRBD reload or service restart to take effect.



## Conclusion

The `/etc/drbd.d/` directory is a critical component of DRBD's configuration architecture. It organizes and stores individual resource definitions that enable DRBD to manage replicated block devices across multiple nodes efficiently. By breaking configuration into modular files, administrators can more easily maintain and update the DRBD setup in high-availability and data replication environments.
