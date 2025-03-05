# pvmove 

The `pvmove` command in Linux is used to migrate data from one physical volume (PV) to another within a volume group (VG). It is typically used when you want to remove or replace a physical volume, but you have logical volumes (LVs) that are using the space on that PV. The command moves data from one PV to another without affecting the logical volumes themselves.

### Syntax:
```bash
pvmove [options] <SourcePhysicalVolume> [DestinationPhysicalVolume]
```

- **`<SourcePhysicalVolume>`**: The physical volume from which data will be moved (e.g., `/dev/sda1`).
- **`[DestinationPhysicalVolume]`** (optional): The physical volume to which the data will be moved. If not specified, the system will automatically select another PV in the same volume group.

### Key Options:
- **`-d, --debug`**: Enable debug output for troubleshooting.
- **`-h, --help`**: Display help information.
- **`-v, --verbose`**: Enable verbose output to show more details during the operation.
- **`--priority <level>`**: Set the priority for the migration process. A higher priority number means a higher priority for migration. Default is `0`.
- **`--size <size>`**: Limits the number of bytes moved in a single operation. This option can be used to break the move process into smaller chunks.
- **`--alloc <policy>`**: Controls how space is allocated during the move (e.g., `anywhere`, `contiguous`).

### How `pvmove` Works:
- The `pvmove` command moves extents (the chunks of data that logical volumes are made of) from one physical volume to another within the same volume group.
- It will automatically move extents from the source physical volume to available space on other physical volumes within the same volume group (if no destination is specified).
- The process is generally non-disruptive to the logical volumes, meaning the data in the logical volumes remains intact, and the logical volumes remain accessible during the operation.

### Example Usage:

#### 1. **Move Data from One Physical Volume to Another**
If you want to move data from `/dev/sda1` to `/dev/sdb1` within the same volume group, you can use:

```bash
sudo pvmove /dev/sda1 /dev/sdb1
```

This command will start migrating data from `/dev/sda1` to `/dev/sdb1`. The operation may take some time, depending on the size of the data.

#### 2. **Move Data Automatically to Any Available Physical Volume**
If you do not specify a destination, `pvmove` will attempt to move the data from the source PV to any available space on other PVs within the same volume group.

```bash
sudo pvmove /dev/sda1
```

This will move data from `/dev/sda1` to other PVs in the volume group automatically.

#### 3. **Verbose Output for Detailed Information**
To see detailed progress of the move operation, use the `-v` option for verbose output:

```bash
sudo pvmove -v /dev/sda1 /dev/sdb1
```

#### 4. **Move Data in Smaller Chunks**
If you want to limit the amount of data moved in one operation, use the `--size` option to specify the size of data to be moved per operation (in bytes):

```bash
sudo pvmove --size 1G /dev/sda1 /dev/sdb1
```

This will move 1 GB of data at a time.

#### 5. **Set Migration Priority**
If there are multiple migration processes running, you can set the priority of the move operation:

```bash
sudo pvmove --priority 10 /dev/sda1 /dev/sdb1
```

Higher numbers indicate higher priority.

### Example Output:
When you run the `pvmove` command, you will typically see output indicating the progress of the data migration. Here's an example of what the output might look like:

```bash
  Moving 8 extents (1.00 GiB) from /dev/sda1 to /dev/sdb1
  Moved 8 extents (1.00 GiB)
```

The output will show how many extents have been moved and provide a summary of the total amount of data transferred.

### Error Handling:
- **No space left on destination PV**: If there is not enough space on the destination PV, the `pvmove` command will fail. Ensure that there is enough free space on the destination PV or that other PVs in the VG have enough available space.
- **Data corruption**: In rare cases, if the move process is interrupted (e.g., due to hardware failure), data corruption can occur. Always ensure proper backups before performing operations on volumes.

### Considerations:
- **Performance impact**: The `pvmove` operation can be I/O intensive and may impact system performance, especially on busy servers. It’s advisable to run this operation during low-traffic times if possible.
- **Non-disruptive**: While the operation should not disrupt the availability of logical volumes, it is always recommended to back up important data before performing any LVM operations.

### Summary:

- **`pvmove`** is a command used to move data from one physical volume to another within a volume group.
- It is useful for removing or replacing disks in a volume group or redistributing data.
- The operation is generally non-disruptive, but it is advisable to monitor the process and ensure that there is enough space on the destination physical volume.
- You can use options such as `-v` for verbose output and `--size` to control how much data is moved at once.
