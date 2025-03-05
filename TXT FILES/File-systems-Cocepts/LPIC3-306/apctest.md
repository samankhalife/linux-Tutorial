# apctest
**`apctest`** is a command-line utility that is part of the **APC UPS Daemon (apcupsd)** package, which is commonly used for managing and monitoring APC (American Power Conversion) UPS (Uninterruptible Power Supply) devices. The `apctest` command is used to test the functionality of your APC UPS device and to troubleshoot or verify the communication between the UPS and the apcupsd service.

### Purpose of `apctest`:

- **Test Communication**: It helps ensure that the apcupsd daemon can communicate properly with the UPS, allowing the system to monitor the UPS status (e.g., battery level, input voltage, etc.) and take action if necessary (such as shutting down the system in case of power failure).
- **Test UPS Features**: You can use it to test various UPS features, such as power status, battery status, and other UPS-related data.

### Key Features of `apctest`:

1. **Check UPS Communication**: Verify that the UPS is correctly connected and responding to commands.
2. **Test UPS Battery and Power Status**: Check battery health, load, input/output voltage, and other metrics.
3. **Simulate a Power Failure**: Simulate a power failure and see how the system responds (e.g., triggers shutdown or alert).
4. **Identify Errors**: Identify any potential issues in the UPS setup, including connection issues, incorrect configurations, or software malfunctions.

### Common Use Cases for `apctest`:

1. **Basic Communication Test**:
   Run the following command to initiate a simple test and check if communication is established between your UPS and the apcupsd daemon:
   ```bash
   apctest
   ```

2. **Testing UPS Shutdown**:
   This test can simulate a power failure and check whether the UPS triggers the system's automatic shutdown as expected. This is especially useful when setting up the UPS to work with server systems.

3. **Display UPS Data**:
   After running `apctest`, you can observe information such as battery charge, remaining time, input voltage, and more. The output is typically used for verifying the UPS's operational status and performance.

4. **Troubleshooting**:
   If there are issues with UPS communication, running `apctest` will provide helpful diagnostic information that can help pinpoint the problem, such as whether the UPS is not properly connected or whether there are issues with apcupsd.

### Example of Running `apctest`:

```bash
$ apctest
```

Upon running the command, you may see output that looks something like this:

```text
apctest 3.14.14 (23 September 2020) 
Checking device communication...
Testing UPS: /dev/ttyS0 (Port used by UPS)

Battery capacity: 98%
Input voltage: 120V
Output voltage: 120V
Remaining battery time: 35 minutes
Load: 70%
```

This output shows the battery status, input/output voltage, remaining time on battery, and the load on the UPS.

### Configuration and Troubleshooting:

If `apctest` returns errors or fails to establish communication, the following troubleshooting steps can be helpful:
- **Check UPS Connection**: Ensure that the UPS is connected to the system via a supported interface (usually serial or USB).
- **Check Permissions**: Ensure that the user running `apctest` has the necessary permissions to access the device file (e.g., `/dev/ttyS0` or `/dev/usb0`).
- **Verify apcupsd Configuration**: Ensure that the `apcupsd.conf` configuration file is properly set up, and the correct UPS device is specified.

### Conclusion:

`apctest` is a useful tool for verifying and troubleshooting communication between an APC UPS and the `apcupsd` software. It helps ensure that the UPS is functioning as expected and can provide important insights into battery health, power status, and other key metrics. This makes it invaluable for managing critical infrastructure that relies on uninterrupted power supplies, such as servers, workstations, and network equipment.
