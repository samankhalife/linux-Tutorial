# /etc/drbd.conf

`/etc/drbd.conf` is the main configuration file for DRBD (Distributed Replicated Block Device) on Linux systems. It serves as the central point for defining global settings and default options, as well as for including additional resource definitions from separate files (often located in `/etc/drbd.d/`).



## Purpose

- **Global Configuration:**  
  Specifies global options that apply to all DRBD operations and resources, such as logging settings, usage counts, and protocol defaults.

- **Common Defaults:**  
  Provides a section for common settings that can be applied to all DRBD resources, ensuring consistent behavior across multiple devices.

- **Resource Inclusion:**  
  Includes additional resource configuration files (typically with a `.res` extension) from a dedicated directory, which allows for modular and organized configuration of multiple DRBD resources.



## Typical Structure

The `/etc/drbd.conf` file generally consists of three main parts:

1. **Global Section:**  
   Contains settings that affect the overall behavior of DRBD.

2. **Common Section:**  
   Sets default options for DRBD resources, such as replication protocol or disk options.

3. **Include Directive:**  
   Specifies one or more directories or files where individual DRBD resource definitions are stored.



## Example Content

A typical `/etc/drbd.conf` might look like this:

```ini
global {
    usage-count yes;
    # Optional logging or network options could be set here.
}

common {
    protocol C;
    # You can define additional default settings for DRBD resources here.
}

# Include all resource definitions from the /etc/drbd.d/ directory.
include "drbd.d/*.res";
```

### Explanation:

- **global Section:**  
  - `usage-count yes;` – Enables DRBD to keep track of resource usage statistics.

- **common Section:**  
  - `protocol C;` – Sets the default replication protocol for all DRBD resources. Protocol C is commonly used for its balance of performance and consistency.

- **Include Directive:**  
  - `include "drbd.d/*.res";` – Instructs DRBD to load additional resource definitions from files in the `/etc/drbd.d/` directory. Each file typically defines a specific DRBD resource with its own settings for individual nodes.



## How It Works

- **Initialization:**  
  When the DRBD service starts, it reads `/etc/drbd.conf` to determine global and common settings. It then processes the include directive to load all resource configuration files, initializing each DRBD resource accordingly.

- **Modular Configuration:**  
  By separating resource-specific settings into individual files within `/etc/drbd.d/`, administrators can manage multiple DRBD resources more easily. This modular approach simplifies updates and troubleshooting.



## Best Practices

- **Keep It Simple:**  
  Use the global and common sections to define settings that should apply uniformly across all resources. Customize individual resource files as needed.

- **Use Include Directives:**  
  Organize resource configurations in separate files within `/etc/drbd.d/` to make the setup easier to maintain.

- **Backup Configurations:**  
  Always back up your `/etc/drbd.conf` file and the entire `/etc/drbd.d/` directory before making significant changes, as misconfiguration can lead to data replication issues.

- **Test Changes:**  
  Validate configuration changes in a test environment before applying them to production systems to ensure that DRBD behaves as expected.



## Conclusion

The `/etc/drbd.conf` file is central to configuring DRBD on a Linux system. It defines global and common defaults for DRBD operations and includes resource-specific configuration files, allowing administrators to maintain a clean, modular setup. Proper configuration of this file is critical for ensuring reliable data replication and high availability in clustered environments.
