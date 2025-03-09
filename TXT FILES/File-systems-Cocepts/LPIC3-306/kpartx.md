# kpartx

**kpartx** is a Linux command-line utility used to create device mappings for partitions in a disk image file or physical disk. It reads partition information from a disk (either physical or image) and creates corresponding devices in `/dev/mapper/`, which can then be used as if they were individual partitions.

This tool is commonly used in situations where you need to mount partitions inside disk images (such as `.iso`, `.img`, or other formats), or in cases where you have a physical disk with multiple partitions, but they are not automatically recognized.

### Purpose

- **Create Device Mappings for Partitions**:  
  It maps the partitions inside a disk image or physical device to `/dev/mapper/` devices, allowing users to access them separately.

- **Access Partitions in Disk Images**:  
  Helps in accessing partitions within disk images (e.g., `.iso`, `.img`, `.vmdk`), typically used when dealing with virtual machines or system recovery.

- **Manage LVM and MD RAID Devices**:  
  Can be used in environments with LVM (Logical Volume Management) or RAID (Redundant Array of Independent Disks) to map and manage partitions.

### Basic Syntax

```bash
kpartx [OPTIONS] <disk-image|device>
```

- **`<disk-image|device>`**: Path to the disk image file (e.g., `.img`, `.iso`) or a physical device (e.g., `/dev/sda`).

### Common Options

- **`-a`**:  
  Add partition mappings for the specified device or image.
  ```bash
  kpartx -a /dev/sda
  ```
  This will create mappings for all partitions on `/dev/sda` and add them under `/dev/mapper/`.

- **`-d`**:  
  Delete the partition mappings for the specified device or image.
  ```bash
  kpartx -d /dev/sda
  ```
  This will remove all partition mappings created by `kpartx` for the device.

- **`-l`**:  
  List the partitions of the specified device or disk image.
  ```bash
  kpartx -l /dev/sda
  ```
  This will list all the partitions on `/dev/sda`, showing the names and details of the partitions.

- **`-v`**:  
  Display verbose output to show more details about what is being done (e.g., mapping devices or adding/removing partitions).

### Example Usage

1. **Listing Partitions in a Disk Image**
   
   To list the partitions in a disk image:
   ```bash
   kpartx -l /path/to/disk-image.img
   ```
   This command will list all partitions inside the disk image `disk-image.img`.

2. **Creating Partition Mappings**
   
   After identifying the partitions in a disk image or physical device, you can create mappings for them:
   ```bash
   kpartx -a /path/to/disk-image.img
   ```
   This will create device mappings for each partition inside the disk image, allowing access to them via `/dev/mapper/`.

3. **Removing Partition Mappings**
   
   To remove the mappings created for a disk image or device:
   ```bash
   kpartx -d /path/to/disk-image.img
   ```
   This command will delete the mappings for the partitions in the specified disk image.

4. **Working with Physical Devices**
   
   You can also use `kpartx` on physical devices, such as `/dev/sda`, to map the partitions:
   ```bash
   kpartx -a /dev/sda
   ```
   This will add mappings for all partitions on `/dev/sda` under `/dev/mapper/`.

### Example Output

1. **Listing Partitions**
   ```bash
   $ kpartx -l /dev/sda
   /dev/sda1 : 0 12345678 /dev/sda1
   /dev/sda2 : 12345678 23456789 /dev/sda2
   ```

   This output shows two partitions on `/dev/sda`: `/dev/sda1` and `/dev/sda2`, with their respective partition sizes in sectors.

2. **Creating Mappings**
   ```bash
   $ kpartx -a /dev/sda
   add map sda1 (254:0) as /dev/mapper/sda1
   add map sda2 (254:1) as /dev/mapper/sda2
   ```

   This output shows that `kpartx` created two device mappings for the partitions `/dev/sda1` and `/dev/sda2` under `/dev/mapper/`.

### Best Practices

- **Use With Disk Images**:  
  `kpartx` is especially useful when dealing with disk images that contain multiple partitions. For example, when working with virtual machine disk images or recovering data from an image, `kpartx` helps map the partitions into accessible devices.

- **Backup Before Modifying**:  
  When working with physical devices, always ensure that you have backups of important data before creating or removing partition mappings.

- **Combine with Mounting**:  
  Once the partitions are mapped with `kpartx`, you can mount them like any other device using `mount`:
  ```bash
  mount /dev/mapper/sda1 /mnt
  ```

### Conclusion

`kpartx` is a useful tool for managing partition mappings in Linux, enabling users to work with multiple partitions in disk images or physical devices. It's ideal for environments where accessing individual partitions within disk images or creating mappings for RAID/LVM configurations is necessary. By using `kpartx`, administrators can easily mount and manipulate partitions that are not directly available as block devices.
