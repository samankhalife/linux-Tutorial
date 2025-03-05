# lvresize
The `lvresize` command is used in Linux to resize logical volumes (LVs) in LVM (Logical Volume Manager). You can use this command to increase or decrease the size of an existing logical volume. LVM allows for flexible disk management, and resizing logical volumes is one of the key features.

### Syntax

```bash
lvresize [options] <logical-volume>
```

Where:
- `<logical-volume>` is the path to the logical volume you want to resize, for example, `/dev/vgname/lvname`.
- Options specify how you want to resize the logical volume, either by increasing or decreasing its size.

### Common Options

1. **`-L` or `--size <size>`**: Specifies the new size for the logical volume.
   - You can specify the size in various units, such as `M` for megabytes, `G` for gigabytes, or `T` for terabytes.
   - Example: Resize the LV to 10 GB:
     ```bash
     sudo lvresize -L 10G /dev/vgname/lvname
     ```

2. **`-l` or `--extents <extents>`**: Specifies the size of the logical volume in terms of extents. An extent is a unit of space in the volume group. For example, `-l +100%FREE` would resize the LV to use all available free space in the volume group.
   - Example: Resize the LV to use all remaining free space in the volume group:
     ```bash
     sudo lvresize -l +100%FREE /dev/vgname/lvname
     ```

3. **`--resizefs`**: This option resizes the filesystem on the logical volume after resizing the LV. It is particularly useful when increasing the size of the LV.
   - Example: Resize the logical volume and filesystem:
     ```bash
     sudo lvresize -L +10G --resizefs /dev/vgname/lvname
     ```

4. **`--noresizefs`**: By default, `lvresize` resizes the filesystem if it is supported. This option disables that behavior, preventing the filesystem from being resized.
   - Example: Resize the LV without resizing the filesystem:
     ```bash
     sudo lvresize -L +10G --noresizefs /dev/vgname/lvname
     ```

5. **`-f` or `--force`**: Forces the resizing operation even if some checks fail.
   - Example:
     ```bash
     sudo lvresize -f -L 15G /dev/vgname/lvname
     ```

6. **`-d` or `--debug`**: Displays debugging information while running the command.
   - Example:
     ```bash
     sudo lvresize -d -L 15G /dev/vgname/lvname
     ```

7. **`--name`**: Renames the logical volume during the resize.
   - Example:
     ```bash
     sudo lvresize --name new_lvname /dev/vgname/old_lvname
     ```

### Resizing a Logical Volume

#### Increasing the size of a logical volume:
To increase the size of a logical volume, you can use the `-L` option. For example, to increase the logical volume `lvname` by 10 GB:

```bash
sudo lvresize -L +10G /dev/vgname/lvname
```

You can also resize the filesystem automatically by using the `--resizefs` option:

```bash
sudo lvresize -L +10G --resizefs /dev/vgname/lvname
```

#### Decreasing the size of a logical volume:
To decrease the size of a logical volume, you can specify the new size using the `-L` option. However, **decreasing the size of a logical volume** may cause data loss if not done carefully. Therefore, always ensure that the filesystem is resized before resizing the LV:

1. Resize the filesystem first (e.g., using `resize2fs` for ext4).
   - Example: Resize the filesystem to 15 GB before resizing the LV:
     ```bash
     sudo resize2fs /dev/vgname/lvname 15G
     ```

2. Then resize the logical volume:
   ```bash
   sudo lvresize -L 15G /dev/vgname/lvname
   ```

#### Resize the logical volume to use all free space:
If you want to resize the logical volume to use all remaining free space in the volume group, use the `-l +100%FREE` option:

```bash
sudo lvresize -l +100%FREE /dev/vgname/lvname
```

### Example Scenarios

1. **Increase the logical volume size to 50 GB**:
   ```bash
   sudo lvresize -L 50G /dev/vgname/lvname
   ```

2. **Increase the logical volume size by 20% of its current size**:
   ```bash
   sudo lvresize -l +20% /dev/vgname/lvname
   ```

3. **Resize the logical volume and automatically resize the filesystem**:
   ```bash
   sudo lvresize -L +20G --resizefs /dev/vgname/lvname
   ```

4. **Resize the logical volume to use all free space in the volume group**:
   ```bash
   sudo lvresize -l +100%FREE /dev/vgname/lvname
   ```

### Important Notes
- **Data Backup**: Always back up your data before resizing, especially when reducing the size of the logical volume, to avoid potential data loss.
- **Filesystem Resize**: When increasing the size of a logical volume, the filesystem should be resized accordingly to make use of the new space. This can usually be done with tools like `resize2fs` for ext4 or `xfs_growfs` for XFS. For decreasing, be sure to reduce the filesystem size before shrinking the logical volume to avoid data loss.
- **Non-Destructive Resize**: It’s typically safe to increase the size of a logical volume without any risk to data, but shrinking the volume requires caution, as it can cause data corruption if not performed carefully.

### Conclusion
The `lvresize` command is a powerful tool for resizing logical volumes in LVM, enabling you to adjust the size of your logical volumes based on your storage needs. Always be cautious when shrinking volumes to avoid data loss and ensure the filesystem is resized appropriately.
