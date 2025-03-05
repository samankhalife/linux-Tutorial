# /etc/smartd.conf
The `/etc/smartd.conf` file is the configuration file used by **`smartd`**, which is part of the **smartmontools** suite. It is responsible for monitoring the health of hard drives and SSDs via the **SMART** (Self-Monitoring, Analysis, and Reporting Technology) system. The `smartd` service continuously monitors the drives for any issues such as bad sectors, temperature warnings, or other signs of impending failure, and can take actions such as sending alerts or executing commands when issues are detected.

### Key Concepts:

- **`smartd`** runs as a daemon in the background and checks the SMART status of devices periodically.
- The configuration file allows users to define which drives to monitor, the frequency of checks, the thresholds for failure warnings, and the actions to take if an issue is found.

### `/etc/smartd.conf` Format:

The file consists of a series of configuration lines that specify monitoring settings for different devices. These lines are divided into **device definitions** and **options**.

#### Basic Structure:
```bash
# Device definition
/dev/sda -a -o on -S on -W 4,40,45 -m user@example.com
```

- **Device Path**: `/dev/sda`, `/dev/sdb`, etc. – The devices to be monitored.
- **Options**: Flags and settings for monitoring, testing, and alerting.

### Common Options:

1. **`-a`**: Enable all SMART attributes.
2. **`-o on/off`**: Enable/disable automatic offline testing of the device.
3. **`-S on/off`**: Enable/disable SMART self-tests.
4. **`-W`**: Set thresholds for **temperature warning**. Example: `-W 4,40,45` – Trigger a warning if the temperature rises above 40°C and a critical warning above 45°C.
5. **`-m`**: Define the email address to receive alerts. Example: `-m user@example.com`.
6. **`-t`**: Specify the self-test duration. Example: `-t short` or `-t long`.
7. **`-s`**: Schedule the periodic SMART check. Example: `-s (S/../.././..|L/../.././..)`.

### Example `/etc/smartd.conf` File:

Here’s an example configuration for **`smartd`**:

```bash
# Default settings for all drives
# Check all drives once per hour
/dev/sda -a -o on -S on -m root@example.com
/dev/sdb -a -o on -S on -m root@example.com

# Set temperature thresholds for device /dev/sda
/dev/sda -W 4,40,45 -m user@example.com

# Run short self-test once a day
/dev/sda -t short

# Set a critical email alert for device /dev/sdc if failure is detected
/dev/sdc -a -m critical@example.com -s (S/../.././..) -W 4,45,50
```

### Explanation of Configuration:

- **`/dev/sda -a -o on -S on -m root@example.com`**: This monitors `/dev/sda`, enabling all SMART attributes, enabling offline testing, enabling self-tests, and sending email alerts to `root@example.com`.
- **`/dev/sda -W 4,40,45 -m user@example.com`**: This monitors `/dev/sda`, setting temperature warning thresholds (4°C to 40°C) and critical thresholds (45°C), sending alerts to `user@example.com`.
- **`/dev/sda -t short`**: Runs a short self-test on `/dev/sda`.
- **`/dev/sdc -a -m critical@example.com -s (S/../.././..) -W 4,45,50`**: Monitors `/dev/sdc`, sends critical alerts to `critical@example.com`, runs tests periodically, and sets temperature thresholds.

### Advanced Configuration Options:

1. **Scheduling Tests** (`-s`):
   The `-s` option allows you to schedule periodic SMART tests.
   - Example:
     ```bash
     -s (S/../.././..|L/../.././..)
     ```
   - The **S** indicates a short self-test and **L** indicates a long test. This is the format for running tests on specific days of the week.

2. **Monitoring Specific SMART Attributes**:
   You can specify which SMART attributes to monitor by listing them. For example, you can monitor just the **Reallocated Sectors** attribute:
   ```bash
   /dev/sda -a -i 5
   ```

3. **Verbose Mode**:
   You can set the verbosity level for `smartd` logs. It will log detailed output that could be useful for debugging.
   - Example:
     ```bash
     -v
     ```

4. **Logging to File**:
   `smartd` can also log to a file for later inspection:
   ```bash
   -l /var/log/smartd.log
   ```

5. **Execute Command on Failure** (`-C`):
   You can define actions to take on SMART failure, such as executing a script or alerting an external system.
   ```bash
   -C /path/to/script.sh
   ```

### Example of `/etc/smartd.conf` with Actions:

```bash
# Monitor device /dev/sda
/dev/sda -a -o on -S on -m admin@example.com -W 4,40,45 -t short -C /usr/local/bin/alert_script.sh
```

In this example, if a SMART failure is detected on `/dev/sda`, the system will send an email to `admin@example.com`, alerting via the script `/usr/local/bin/alert_script.sh`.

### Conclusion:

The `/etc/smartd.conf` file is an essential configuration for automating disk monitoring with **SMART** technology. By setting up **`smartd`** correctly, system administrators can be alerted to potential disk failures before they cause irreparable damage, enabling proactive maintenance and reducing downtime. The flexibility of `smartd` allows it to be tailored to your needs, whether you're monitoring a single system or an enterprise network.
