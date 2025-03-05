# smartd
**`smartd`** is the **SMART Daemon** used to monitor the health and status of storage devices (hard drives, SSDs, etc.) that support **Self-Monitoring, Analysis, and Reporting Technology (SMART)**. It runs in the background on Linux and Unix-like operating systems, periodically checking the SMART status of the devices to ensure they are functioning correctly and to alert administrators if there are any signs of failure or other issues. 

### Key Features of `smartd`:
1. **Monitoring SMART Attributes**:
   - `smartd` continuously monitors the SMART attributes of the storage devices, which include various health-related parameters like temperature, bad sectors, wear, reallocated sectors, and more. If any of these values reach critical thresholds, `smartd` can send notifications or take predefined actions.

2. **Notifications**:
   - It can notify the system administrator of issues with storage devices. Notifications can be sent via email, log files, or syslog messages, depending on the configuration.
   
3. **Scheduled Checks**:
   - `smartd` can be configured to perform regular, scheduled checks to monitor device health. It can execute tests like short or long self-tests on the drives to identify potential failures.

4. **Test Execution**:
   - The daemon can be configured to initiate SMART self-tests (e.g., **short** and **long tests**) on the drives. This helps catch potential problems like surface defects, bad sectors, or electrical issues.

5. **Logging and Alerts**:
   - It can log warnings to system logs and send alerts for critical events. This includes issuing warnings when the SMART attributes of a drive exceed specified thresholds.

6. **Failure Prediction**:
   - `smartd` is designed to predict hard disk failures based on the SMART data provided by the device. The tool can detect signs of impending failure, such as increasing numbers of bad sectors or an increasing temperature, and send alerts before the device fails completely.

7. **Configurability**:
   - The `smartd` configuration file allows fine-grained control over the monitoring behavior. You can specify which drives to monitor, how frequently to check them, what thresholds to trigger alerts, and where to send the notifications.

### Installation:

On most Linux distributions, `smartd` is included in the **`smartmontools`** package. You can install it using the package manager of your distribution.

- **Debian/Ubuntu**:
  ```bash
  sudo apt install smartmontools
  ```

- **Red Hat/CentOS**:
  ```bash
  sudo yum install smartmontools
  ```

- **Fedora**:
  ```bash
  sudo dnf install smartmontools
  ```

### Configuration:

The configuration file for `smartd` is typically located at **`/etc/smartd.conf`**. You can edit this file to specify which drives to monitor and customize the behavior of the daemon.

Example of `/etc/smartd.conf`:

```bash
# Monitoring a single device
/dev/sda -a -o on -S on -s (S/../.././02|L/../../6/03) -m admin@example.com

# Monitoring multiple devices with different configurations
/dev/sdb -a -o on -S on -s (S/../.././02|L/../../6/03) -m admin@example.com
/dev/sdc -a -o on -S on -s (S/../.././02|L/../../6/03)
```

### Configuration Parameters:

- **Device** (`/dev/sda`, `/dev/sdb`): Specifies the device to be monitored.
- **`-a`**: Tells `smartd` to check all attributes (useful for monitoring all SMART attributes).
- **`-o on`**: Enables automatic offline data collection.
- **`-S on`**: Enables automatic surface scan of the device.
- **`-s (S/../.././02|L/../../6/03)`**: Specifies the schedule for short (`S`) and long (`L`) self-tests.
- **`-m`**: Specifies the email address to send alerts to.

### Commands and Operations:

- **Start the `smartd` service**:
  On most systems, you can start the `smartd` daemon using the following commands:

  - **Systemd-based systems**:
    ```bash
    sudo systemctl start smartd
    sudo systemctl enable smartd
    ```

  - **SysV init-based systems**:
    ```bash
    sudo service smartd start
    ```

- **Check the status of `smartd`**:
  To see the status of `smartd` and check if it's running, use:
  ```bash
  sudo systemctl status smartd
  ```

- **Manual SMART Check**:
  If you want to manually perform a SMART test on a drive, you can use the `smartctl` command:
  ```bash
  sudo smartctl -t short /dev/sda
  ```

  This will initiate a short test on `/dev/sda`. You can also initiate a long test or other SMART tests.

- **Get SMART Information**:
  You can use `smartctl` to retrieve detailed SMART data about a drive:
  ```bash
  sudo smartctl -a /dev/sda
  ```

  This will provide detailed information about the drive's health, temperature, reallocated sectors, and other SMART attributes.

### Example Use Cases:

1. **Disk Health Monitoring**:
   - You can configure `smartd` to monitor critical system disks to ensure they are in good health, proactively identifying issues like failing sectors or temperature spikes.

2. **Automated Notifications**:
   - By setting up email notifications through `smartd`, you can receive alerts for potential disk issues without needing to constantly monitor each device manually.

3. **Scheduled Self-Tests**:
   - For improved reliability, `smartd` can be configured to perform regular self-tests on devices, allowing you to catch minor issues early before they become major failures.

### Logging:

The log entries generated by `smartd` will typically be written to the system's log files (e.g., `/var/log/syslog`, `/var/log/messages`) depending on your configuration.

Example log message:
```
May 5 15:22:14 myserver smartd[1234]: Device: /dev/sda [SAT], SMART Usage Attribute: 9 (Power-on Hours) exceeded threshold: 500 (current: 550)
```

This log entry indicates that the "Power-on Hours" attribute for `/dev/sda` exceeded the specified threshold.


### Conclusion:

**`smartd`** is a useful daemon for monitoring the health of storage devices through SMART attributes, allowing administrators to proactively monitor for early signs of failure. It integrates well with system logging and alerting mechanisms, and with proper configuration, it can ensure that any issues with storage devices are detected and communicated promptly. It is an essential tool for maintaining data integrity and ensuring the long-term reliability of storage systems.
