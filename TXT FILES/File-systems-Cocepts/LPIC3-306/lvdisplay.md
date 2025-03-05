# lvdisplay
The `lvdisplay` command in Linux is used to display detailed information about logical volumes (LVs) in a Logical Volume Manager (LVM) setup. It provides detailed information about the logical volume, such as its size, volume group, and the filesystem associated with it.

### Syntax

```bash
lvdisplay [options] <logical-volume>
```

Where:
- `<logical-volume>` is the path to the logical volume (e.g., `/dev/vgname/lvname`).
- If you don't specify a logical volume, `lvdisplay` will show information for all logical volumes in the system.

### Common Options

1. **`-v` or `--verbose`**: Displays verbose output, providing additional details like logical volume status, extent information, etc.
   - Example:
     ```bash
     sudo lvdisplay -v /dev/vgname/lvname
     ```

2. **`-o` or `--columns`**: Allows you to display specific columns of information.
   - Example:
     ```bash
     sudo lvdisplay -o lv_name,lv_size,lv_attr
     ```

3. **`--help`**: Displays help information about the command and its options.
   - Example:
     ```bash
     sudo lvdisplay --help
     ```

### Example of Using `lvdisplay`

1. **Display Information for a Specific Logical Volume**:
   To display detailed information about a specific logical volume, use:
   ```bash
   sudo lvdisplay /dev/vgname/lvname
   ```

   Example output:
   ```
   --- Logical volume ---
   LV Name                /dev/vgname/lvname
   VG Name                vgname
   LV UUID                LUVH-3YtP-j0gt-WGq1-8uKv-vWnG-WfiJ-0U6l5k
   LV Write Access        read/write
   LV Creation host, time host, 2025-03-05 15:25:55 +0000
   LV Status              available
   # open                 1
   LV Size                50.00 GiB
   Current LE             12800
   Segments               1
   Allocation             inherit
   Read ahead sectors     1024
   Block device           253:0
   ```

   In this output, the key fields are:
   - `LV Name`: The name of the logical volume.
   - `VG Name`: The volume group to which the logical volume belongs.
   - `LV Size`: The total size of the logical volume.
   - `LV Status`: Indicates whether the logical volume is available or not.
   - `Current LE`: The number of logical extents used by the logical volume.

2. **Display Information for All Logical Volumes**:
   To display information for all logical volumes in the system:
   ```bash
   sudo lvdisplay
   ```

   Example output (for multiple logical volumes):
   ```
   --- Logical volume ---
   LV Name                /dev/vgname/lvname
   VG Name                vgname
   LV UUID                LUVH-3YtP-j0gt-WGq1-8uKv-vWnG-WfiJ-0U6l5k
   LV Size                50.00 GiB
   ...
   
   --- Logical volume ---
   LV Name                /dev/vgname/lvdata
   VG Name                vgname
   LV UUID                LUVH-3YtP-j0gt-WGq1-8uKv-vWnG-WfiJ-0U6l5k
   LV Size                100.00 GiB
   ...
   ```

### Detailed Information Provided by `lvdisplay`

- **LV Name**: The name of the logical volume.
- **VG Name**: The volume group that contains the logical volume.
- **LV UUID**: The unique identifier of the logical volume.
- **LV Write Access**: Shows whether the logical volume is read-write or read-only.
- **LV Creation Host, Time**: The host and time the logical volume was created.
- **LV Status**: Indicates whether the logical volume is available, not available, or inactive.
- **Open Count**: The number of processes or applications using the logical volume.
- **LV Size**: The total size of the logical volume.
- **Current LE**: The number of logical extents allocated to the logical volume.
- **Segmentation**: Number of segments (typically 1).
- **Allocation**: Type of allocation used (inherit or contiguous).
- **Read Ahead Sectors**: The number of sectors to be read ahead for optimization.
- **Block Device**: The device associated with the logical volume (e.g., `/dev/mapper/vgname-lvname`).

### Example Use Cases

1. **Get Details of a Logical Volume**:
   You can use `lvdisplay` to check details like size, status, and other metadata for a specific logical volume.
   ```bash
   sudo lvdisplay /dev/vgname/lvdata
   ```

2. **Checking the Size of All Logical Volumes**:
   Use `lvdisplay` to check the sizes and other details of all logical volumes in the system:
   ```bash
   sudo lvdisplay
   ```

3. **Verbose Information**:
   For more in-depth details, you can use the `-v` option to get additional information like logical extents and attributes.
   ```bash
   sudo lvdisplay -v /dev/vgname/lvname
   ```

### Conclusion

`lvdisplay` is a useful command to obtain detailed information about logical volumes in an LVM setup. This command allows you to monitor and manage logical volumes by displaying information such as their size, status, and associated volume group. Use it to get insight into your logical volume configuration and health.
