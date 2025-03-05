# smartctl

**`smartctl`** is a command-line utility that is part of the **smartmontools** package, used for monitoring and managing the **SMART (Self-Monitoring, Analysis, and Reporting Technology)** system built into modern hard drives, SSDs, and other storage devices. It provides detailed information about the health, status, and diagnostics of storage devices, helping to predict potential failures before they happen.

### Key Features of `smartctl`:
1. **Monitor SMART Health**:
   - `smartctl` can retrieve SMART attributes of storage devices (such as temperature, reallocated sectors, power-on hours, etc.) and report any anomalies that might indicate potential failure.

2. **Run SMART Tests**:
   - It allows users to initiate self-tests on the device, including **short tests**, **long tests**, and **conveyance tests**. These tests assess the physical condition of the drive and provide diagnostic data.

3. **View SMART Data**:
   - It can display detailed SMART data, including raw values, thresholds, and status flags, for a drive. This data can help identify issues like bad sectors or rising temperature.

4. **Predictive Failure Analysis**:
   - `smartctl` can help detect early signs of failure, such as an increasing number of bad sectors or a decreasing overall health score. It alerts you before critical failures occur.

5. **Control Device Features**:
   - `smartctl` can enable or disable SMART features, control power management settings, and issue commands to the device.

### Installation:

On most Linux distributions, `smartctl` is included in the **smartmontools** package. You can install it via your system’s package manager.

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

### Basic Usage:

1. **Check SMART Status of a Drive**:

   To check the SMART status of a drive (e.g., `/dev/sda`), use:
   ```bash
   sudo smartctl -H /dev/sda
   ```
   - **`-H`**: This option checks the SMART health of the device. If SMART is enabled and the drive is healthy, it will output "PASSED." If there are issues, it will output "FAILED."

2. **Display SMART Information**:

   To view detailed SMART data for a drive, use:
   ```bash
   sudo smartctl -a /dev/sda
   ```
   - **`-a`**: This option displays all available SMART data for the specified device.

   Example output:
   ```
   smartctl 7.2 2020-12-30 r5205 [x86_64-linux-5.4.0-77-generic] (local build)
   Copyright (C) 2002-20, Bruce Allen, Christian Franke, www.smartmontools.org

   === START OF INFORMATION SECTION ===
   Model Family:     Western Digital Red
   Device Model:     WDC WD60EFRX-68MYMN1
   Serial Number:    WD-WCC7K0L0K0Z9
   LU WWN Device Id: 5 0014ee 2b65c65b
   Firmware Version: 82.00A82
   User Capacity:    6,001,011,720,704 bytes [6.00 TB]
   Sector Size:      512 bytes logical/physical
   Rotation Rate:    5400 rpm
   Device Type:      disk

   SMART Status:     Passed
   ...

   === START OF SMART DATA SECTION ===
   SMART Health Status: OK
   Temperature_Celsius    0x0022   121   118   000    Old_age   Always       -       39 (Min/Max 24/49)
   ...
   ```

3. **Run SMART Tests**:

   - **Short Test**: A quick test that takes only a few minutes.
     ```bash
     sudo smartctl -t short /dev/sda
     ```

   - **Long Test**: A more comprehensive test that can take several hours.
     ```bash
     sudo smartctl -t long /dev/sda
     ```

   - **Conveyance Test**: A test designed to detect issues caused by transportation or shipping (for new devices).
     ```bash
     sudo smartctl -t conveyance /dev/sda
     ```

   After initiating a test, you can check the results:
   ```bash
   sudo smartctl -a /dev/sda
   ```

4. **Enable/Disable SMART**:

   You can enable or disable the SMART feature on a device (useful for older devices or troubleshooting).
   - Enable SMART:
     ```bash
     sudo smartctl -s on /dev/sda
     ```
   - Disable SMART:
     ```bash
     sudo smartctl -s off /dev/sda
     ```

5. **Perform Device Reset**:
   If you're troubleshooting a drive, you might want to reset the SMART data:
   ```bash
   sudo smartctl -S on /dev/sda
   ```

### SMART Attributes:

When using `smartctl -a`, you will see a table of SMART attributes. These attributes provide data on the health of the device, such as:

- **Reallocated Sectors Count**: The number of bad sectors that have been reallocated to spare areas of the drive. A high number indicates potential disk failure.
- **Temperature**: The temperature of the drive. Overheating can lead to premature failure.
- **Power-On Hours**: The total number of hours the drive has been powered on.
- **Seek Error Rate**: Indicates the number of errors encountered during the drive's seek operations. High numbers may indicate issues with the drive’s mechanics.


### Example Commands:

1. **List Available Drives**:
   To list all available drives on your system, use:
   ```bash
   sudo smartctl --scan
   ```

2. **Show the Drive's Serial Number and Firmware**:
   To show the serial number and firmware version of a drive, use:
   ```bash
   sudo smartctl -i /dev/sda
   ```

3. **Check Temperature**:
   To check the temperature of the drive, use:
   ```bash
   sudo smartctl -A /dev/sda | grep Temperature
   ```

### Conclusion:

**`smartctl`** is a powerful tool for managing and monitoring storage devices' health through SMART data. By regularly checking SMART attributes and running self-tests, you can get ahead of potential hard drive failures and take action before data loss occurs. Whether you're managing a single system or a large server farm, `smartctl` can be a critical part of your disk monitoring strategy.
