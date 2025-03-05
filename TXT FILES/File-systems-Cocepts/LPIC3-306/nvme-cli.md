# nvme-cli 
**`nvme-cli`** is a command-line utility for managing and interacting with **NVMe (Non-Volatile Memory Express)** devices on Linux-based systems. NVMe is a high-speed storage protocol designed for solid-state drives (SSDs) that are connected through the PCIe interface. The `nvme-cli` tool allows you to perform various operations on NVMe devices, such as querying information, formatting, managing namespaces, performing diagnostics, and tuning performance.

### Key Features of `nvme-cli`:

1. **Querying Device Information**:
   - Get detailed information about the NVMe device, including model, serial number, firmware version, capacity, and health.
   - Example command:
     ```bash
     nvme list
     ```
     This lists all NVMe devices connected to the system along with their status.

2. **SMART Health Information**:
   - Retrieve SMART (Self-Monitoring, Analysis, and Reporting Technology) data for the NVMe device, which includes health status, temperature, error counts, and wear leveling.
   - Example command:
     ```bash
     nvme smart-log /dev/nvme0
     ```

3. **Namespace Management**:
   - NVMe devices can have multiple namespaces, which are essentially partitions on the device. You can create, delete, and list namespaces.
   - Example command to list namespaces:
     ```bash
     nvme list-ns /dev/nvme0
     ```

4. **Firmware Management**:
   - You can check the current firmware version of an NVMe device and update it if needed.
   - Example command to check firmware:
     ```bash
     nvme id-ctrl /dev/nvme0
     ```
   - Example command to update firmware (requires the firmware file):
     ```bash
     nvme fw-download /dev/nvme0 --fw=<firmware_file>
     nvme fw-activate /dev/nvme0
     ```

5. **Device Formatting**:
   - Format NVMe devices or namespaces with various options.
   - Example command to format a device:
     ```bash
     nvme format /dev/nvme0 --force
     ```

6. **Diagnostic and Performance Testing**:
   - `nvme-cli` can be used to run diagnostic tests on the device and check its performance.
   - Example command for a diagnostic self-test:
     ```bash
     nvme self-test /dev/nvme0
     ```

7. **Thermal Management**:
   - Get temperature readings and control thermal limits (if supported by the hardware).
   - Example command to check the temperature:
     ```bash
     nvme temperature /dev/nvme0
     ```

8. **Power Management**:
   - The tool allows you to manage power states for NVMe devices, including active and low-power states.
   - Example command to check power states:
     ```bash
     nvme power-state /dev/nvme0
     ```

9. **Log and Event Monitoring**:
   - `nvme-cli` allows you to monitor the device's event log for issues like errors, firmware updates, or other significant events.
   - Example command to retrieve event log:
     ```bash
     nvme get-log /dev/nvme0 --log-id=1
     ```

10. **Security Features**:
    - Enable or disable features like the secure erase of NVMe drives or manage the cryptographic protection of the device.
    - Example command to enable security erase:
      ```bash
      nvme sanitize /dev/nvme0 --sanitize-erase
      ```

### Installation:

On most Linux distributions, `nvme-cli` can be installed from the package manager:

- **Debian/Ubuntu**:
  ```bash
  sudo apt install nvme-cli
  ```

- **Red Hat/CentOS**:
  ```bash
  sudo yum install nvme-cli
  ```

- **Fedora**:
  ```bash
  sudo dnf install nvme-cli
  ```

### Basic Commands:

1. **Listing NVMe Devices**:
   ```bash
   nvme list
   ```

2. **Checking SMART Logs**:
   ```bash
   nvme smart-log /dev/nvme0
   ```

3. **Check Device Identity Information**:
   ```bash
   nvme id-ctrl /dev/nvme0
   ```

4. **Getting Temperature**:
   ```bash
   nvme temperature /dev/nvme0
   ```

5. **Running Self Test**:
   ```bash
   nvme self-test /dev/nvme0
   ```

6. **Formatting Device**:
   ```bash
   nvme format /dev/nvme0 --force
   ```

### Use Cases:

- **Health Monitoring**: You can use `nvme-cli` to regularly monitor the health of your NVMe devices, ensuring that they are operating properly and to detect early signs of failure (e.g., wear leveling, temperature issues).
  
- **Device Configuration and Tuning**: Configure and tune your NVMe devices for optimal performance, such as adjusting power management settings or managing namespaces.

- **Firmware Updates**: `nvme-cli` is a useful tool for keeping your NVMe devices up-to-date with the latest firmware to fix bugs or improve performance.

- **Security Management**: Securely erase data from NVMe devices when needed, useful for sensitive data environments.

### Conclusion:

`nvme-cli` is a powerful tool for managing NVMe storage devices on Linux systems. Whether you need to check device health, update firmware, manage namespaces, or run diagnostics, `nvme-cli` provides all the necessary commands to interact with NVMe devices at a low level. It is an essential tool for system administrators and professionals managing high-performance storage systems.
