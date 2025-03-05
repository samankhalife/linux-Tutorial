# mdadm
`mdadm` (Multiple Devices Admin) is a Linux utility used for managing and monitoring **software RAID** arrays. It is an essential tool for configuring, creating, managing, and troubleshooting RAID arrays using the **MD (Multiple Devices)** subsystem in Linux. `mdadm` works with both **RAID devices** managed by the kernel's RAID functionality and **RAID1, RAID5, RAID6, RAID10**, and **RAID0** configurations.

### Key Features of `mdadm`:

1. **Creating RAID Arrays**: 
   - `mdadm` can be used to create new software RAID arrays, specify RAID level (RAID 0, 1, 5, 6, etc.), and assign devices to the array.

2. **Managing RAID Arrays**:
   - It supports operations such as adding, removing, or replacing disks in a RAID array. Additionally, it helps in managing RAID components, setting RAID array parameters, and more.

3. **Monitoring RAID Arrays**:
   - `mdadm` can monitor the health of RAID arrays, alerting users to potential failures or degraded arrays. It can also check for resync/rebuild progress.

4. **Resync and Rebuild**:
   - When a disk fails in a RAID array, `mdadm` helps rebuild the array by resyncing the data. It also manages the process of replacing failed disks and restoring redundancy.

5. **RAID Array Maintenance**:
   - It can trigger operations such as array reshaping, expanding, or shrinking, as well as performing various maintenance tasks.

6. **Logging and Alerting**:
   - `mdadm` can send email alerts for RAID status changes, array failures, and rebuild completions.

### Common `mdadm` Commands and Their Usage:

1. **Creating a RAID Array**:
   - To create a RAID 1 array with two devices (`/dev/sda` and `/dev/sdb`):
     ```bash
     mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda /dev/sdb
     ```
   - This command creates a **RAID 1** array (`/dev/md0`) using two devices.

2. **Viewing RAID Array Information**:
   - To check the status of RAID arrays:
     ```bash
     mdadm --detail /dev/md0
     ```
   - This provides detailed information about the array `/dev/md0`, including the devices used, RAID level, and array health.

3. **Assembling a RAID Array**:
   - To assemble a previously created RAID array, you can use:
     ```bash
     mdadm --assemble /dev/md0 /dev/sda /dev/sdb
     ```
   - This command is used when reassembling a degraded or missing RAID array after booting.

4. **Adding a New Disk to a RAID Array**:
   - To add a new disk (`/dev/sdc`) to an existing RAID 5 array (`/dev/md0`):
     ```bash
     mdadm --add /dev/md0 /dev/sdc
     ```
   - This adds `/dev/sdc` to the existing RAID array, which will then start the resynchronization process to integrate the new disk into the array.

5. **Removing a Disk from a RAID Array**:
   - To remove a failed or unused disk from an array:
     ```bash
     mdadm --remove /dev/md0 /dev/sda
     ```
   - This command removes `/dev/sda` from the RAID array `/dev/md0`.

6. **Monitoring RAID Array Status**:
   - You can use `mdadm` to monitor the status of your RAID array continuously. To monitor the status and automatically send alerts on failures:
     ```bash
     mdadm --monitor --scan --daemonise
     ```
   - This runs `mdadm` in monitoring mode, which checks the array's health and will send alerts if any problems arise.

7. **Checking the Health of All RAID Arrays**:
   - To check the health of all RAID arrays:
     ```bash
     mdadm --examine --scan
     ```

8. **Growing a RAID Array**:
   - To expand the size of a RAID array after adding new disks (e.g., adding `/dev/sdc` to a RAID 5 array):
     ```bash
     mdadm --grow /dev/md0 --raid-devices=4 /dev/sdc
     ```
   - This increases the number of devices in the array, initiating a reshaping process.

9. **Stopping and Assembling RAID Arrays**:
   - If you want to stop a RAID array (e.g., `/dev/md0`), use:
     ```bash
     mdadm --stop /dev/md0
     ```
   - This will stop the RAID array. It is commonly used before removing the array from the system.

10. **Rebuilding a RAID Array**:
   - If a disk has failed and needs rebuilding, `mdadm` can monitor and manage this:
     ```bash
     mdadm --manage /dev/md0 --add /dev/sda
     ```

11. **Creating RAID Configuration File**:
    - To generate the configuration file for RAID arrays:
      ```bash
      mdadm --detail --scan > /etc/mdadm/mdadm.conf
      ```

### Example Output from `mdadm`:

```bash
$ mdadm --detail /dev/md0
/dev/md0:
        Version : 1.2
  Creation Time : Sun Mar  7 10:25:39 2021
     Raid Level : raid5
     Array Size : 9766481920 (9311.94 GiB 10000.16 GB)
  Used Dev Size : 4883240960 (4655.97 GiB 5000.08 GB)
   Raid Devices : 3
  Total Devices : 3
    Persistence : Superblock is persistent

    Update Time : Wed Mar  9 12:53:01 2021
          State : clean
 Active Devices : 3
Working Devices : 3
 Failed Devices : 0
  Spare Devices : 0

           Name : server:0  (local to host server)
           UUID : c29f1f6e:0eaa7d5b:fd5bb16d:b38a30b4
         Events : 184

    Number   Major   Minor   RaidDevice State
       0     8        1        0      active sync   /dev/sda
       1     8       17        1      active sync   /dev/sdb
       2     8       33        2      active sync   /dev/sdc
```

### Key Fields:
- **Version**: Version of the RAID superblock used.
- **Creation Time**: When the array was created.
- **RAID Level**: RAID type (RAID 5 in this example).
- **Array Size**: Total size of the array.
- **Used Dev Size**: Size of each individual device in the array.
- **Active Devices**: Number of devices currently active in the array.
- **State**: The current state of the array (e.g., `clean`, `resync`, `degraded`).
- **Name**: The name of the RAID array.
- **UUID**: Unique identifier for the array.
- **Devices**: Information about each device in the array, including its status.

### Conclusion:
`mdadm` is a powerful tool for creating, managing, and monitoring software RAID arrays in Linux. It provides administrators with the necessary capabilities to manage disk redundancy, array health, and rebuilding processes, while also offering monitoring and alerting features to ensure that RAID arrays remain in optimal condition. The flexibility and reliability of `mdadm` make it the go-to tool for managing software RAID in Linux systems.
