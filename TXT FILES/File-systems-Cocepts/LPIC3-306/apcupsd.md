# apcupsd
**`apcupsd`** (APC UPS Daemon) is a software package used to monitor and manage APC (American Power Conversion) Uninterruptible Power Supply (UPS) devices. It allows for monitoring UPS status (such as battery charge, load, voltage, etc.) and performing automated actions, such as shutting down a computer or sending notifications, during power events (like power failures or surges).

### Key Features of `apcupsd`:

1. **Monitor UPS Status**: Continuously monitor the UPS for vital information such as battery health, remaining battery time, input/output voltage, power consumption, and system load.
   
2. **Automatic Shutdown**: Automatically shuts down the system in the event of a power failure or when the UPS battery is running low to prevent data loss.

3. **Notifications and Logging**: Sends notifications via email, text, or other means when certain events occur (e.g., power failure, low battery). Logs system events for troubleshooting and historical reference.

4. **Remote Management**: Allows remote monitoring and control of UPS devices through web interfaces or network protocols like SNMP.

5. **Customizable Actions**: Users can configure specific actions for events such as power failure, low battery, or UPS overload. This can include sending alerts, starting or stopping services, or running custom scripts.

6. **Support for Multiple UPS Types**: While designed primarily for APC UPS devices, `apcupsd` also supports other UPS devices from different manufacturers, provided they use supported protocols.

### Basic Setup and Configuration of `apcupsd`:

1. **Installation**:
   On a Linux system, you can typically install `apcupsd` from your package manager:
   ```bash
   sudo apt-get install apcupsd       # For Debian-based distributions
   sudo yum install apcupsd           # For Red Hat-based distributions
   ```

2. **Configuration File (`apcupsd.conf`)**:
   The main configuration file for `apcupsd` is typically located at `/etc/apcupsd/apcupsd.conf`. This file contains settings for device communication, shutdown behavior, notification options, and other parameters. 

   Example:
   ```text
   UPSCABLE usb
   UPSTYPE usb
   DEVICE
   STARTDELAY 0
   SHUTDOWNTIME 20
   BATTERYLEVEL 5
   MINUTES 5
   ```

   - `UPSCABLE usb`: Specifies the UPS connection type (USB in this case).
   - `UPSTYPE usb`: Specifies that the UPS is connected via USB.
   - `DEVICE`: This field is left blank because the software automatically detects the device on USB.
   - `STARTDELAY`: Delay (in seconds) before starting to monitor the UPS after system boot.
   - `SHUTDOWNTIME`: Time before initiating shutdown when the power is lost.
   - `BATTERYLEVEL`: The battery level (in percentage) at which the system should start the shutdown procedure.
   - `MINUTES`: The number of minutes of remaining battery life when a shutdown is initiated.

3. **Service Start**:
   After configuring `apcupsd`, you can start the service:
   ```bash
   sudo systemctl start apcupsd
   ```

   To enable it to start automatically on boot:
   ```bash
   sudo systemctl enable apcupsd
   ```

4. **Testing Communication with UPS**:
   To verify that the `apcupsd` service is communicating with the UPS correctly, you can use the following command:
   ```bash
   apcaccess status
   ```
   This will provide a status report from the UPS, including battery level, input/output voltage, load, and other parameters.

5. **Log Files**:
   `apcupsd` logs its activities in `/var/log/apcupsd.events`. You can check this log to review events like power failures, battery warnings, or shutdown events.

6. **Managing the UPS**:
   - You can manually shut down the system with:
     ```bash
     apccontrol shutdown
     ```
   - To cancel shutdown during a power failure:
     ```bash
     apccontrol cancel
     ```

### Troubleshooting and Maintenance:

- **Device Connection Issues**: If `apcupsd` does not detect the UPS, ensure the UPS is correctly connected via USB or serial port and that the correct cable type is specified in the configuration file.
  
- **Permission Issues**: The user running `apcupsd` must have permission to access the UPS device (e.g., `/dev/usb/hiddev0`). Make sure the user is in the correct group, such as `dialout` for USB devices.

- **UPS Settings**: If you are using an APC UPS, you can configure it using the APC UPS tools like `apctest` to verify the connection and settings before integrating it into `apcupsd`.

### Conclusion:

`apcupsd` is a powerful tool for managing and monitoring APC UPS devices, providing essential features like power failure detection, automated shutdown, and detailed UPS status reporting. It is an invaluable tool for ensuring the reliability and safety of systems, especially critical ones like servers or workstations that rely on constant uptime. Through proper configuration, it helps prevent data loss during power failures and allows for remote monitoring and control, making it ideal for both home and enterprise environments.
