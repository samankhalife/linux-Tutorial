# lvreduce
The `lvreduce` command in Linux is used to reduce the size of a logical volume (LV) in an LVM (Logical Volume Manager) setup. This is a potentially risky operation as reducing the size of a logical volume can result in data loss if not done correctly. Therefore, it's important to ensure the filesystem is shrunk before reducing the logical volume's size.

### Syntax

```bash
lvreduce [options] <logical-volume>
```

Where:
- `<logical-volume>` is the path to the logical volume you want to resize (e.g., `/dev/vgname/lvname`).

### Common Options

1. **`-L` or `--size <size>`**: Specifies the new size of the logical volume. This is used when reducing the size.
   - Example: Resize the LV to 20GB:
     ```bash
     sudo lvreduce -L 20G /dev/vgname/lvname
     ```

2. **`-l` or `--extents <extents>`**: Specifies the size of the logical volume in terms of extents. An extent is a unit of space in the volume group.
   - Example: Resize the LV to use only 50% of the available extents:
     ```bash
     sudo lvreduce -l 50%FREE /dev/vgname/lvname
     ```

3. **`--resizefs`**: Automatically resizes the filesystem on the logical volume to match the new size of the logical volume.
   - Example: Resize the LV and filesystem together:
     ```bash
     sudo lvreduce -L 20G --resizefs /dev/vgname/lvname
     ```

4. **`--noresizefs`**: Prevents the automatic resizing of the filesystem. You would need to manually shrink the filesystem before running the `lvreduce` command.
   - Example:
     ```bash
     sudo lvreduce -L 20G --noresizefs /dev/vgname/lvname
     ```

5. **`-f` or `--force`**: Forces the reduction of the logical volume, even if there are potential issues (not recommended unless you're sure).
   - Example:
     ```bash
     sudo lvreduce -f -L 20G /dev/vgname/lvname
     ```

6. **`-d` or `--debug`**: Displays debugging information during the execution of the command.
   - Example:
     ```bash
     sudo lvreduce -d -L 20G /dev/vgname/lvname
     ```

### How to Use `lvreduce`

Before you use `lvreduce`, ensure that:
1. **Backup your data**: Reducing the size of a logical volume, especially if you shrink it too much, can result in data loss. Always back up your data before performing such operations.
2. **Shrink the filesystem**: If you are reducing the size of a logical volume, it is important to shrink the filesystem first. Shrinking the filesystem ensures that no data will be lost during the reduction of the logical volume.

### Steps to Reduce the Size of a Logical Volume

#### 1. **Shrink the Filesystem**
Before you can safely reduce the size of the logical volume, you must shrink the filesystem. This step depends on the type of filesystem used.

- For **ext4** filesystems, you can use `resize2fs`:
  ```bash
  sudo resize2fs /dev/vgname/lvname 20G
  ```

- For **XFS** filesystems, you cannot shrink them directly. If you are using XFS, you will need to back up the data, recreate the volume, and restore the data.

#### 2. **Reduce the Logical Volume Size**
Once the filesystem is shrunk, you can safely reduce the logical volume size using `lvreduce`:

- To reduce the logical volume to 20GB:
  ```bash
  sudo lvreduce -L 20G /dev/vgname/lvname
  ```

- To reduce the logical volume by a certain number of extents (e.g., 50% of the free space):
  ```bash
  sudo lvreduce -l 50%FREE /dev/vgname/lvname
  ```

#### 3. **Resize the Filesystem**
If you didn't use `--resizefs` during the `lvreduce` command, you'll need to resize the filesystem manually after reducing the LV. For example:

- For **ext4** filesystems, use:
  ```bash
  sudo resize2fs /dev/vgname/lvname
  ```

#### 4. **Verify the Size**
Once you’ve reduced the logical volume and filesystem, verify the changes:

```bash
sudo lvdisplay /dev/vgname/lvname
```

You can also check the filesystem size with:

```bash
df -h /mountpoint
```

### Example of Reducing Logical Volume Size

1. **Shrink the ext4 filesystem** to 10GB:
   ```bash
   sudo resize2fs /dev/vgname/lvname 10G
   ```

2. **Reduce the size of the logical volume** to 10GB:
   ```bash
   sudo lvreduce -L 10G /dev/vgname/lvname
   ```

3. **Resize the filesystem** after reducing the logical volume size (optional if `--resizefs` was used):
   ```bash
   sudo resize2fs /dev/vgname/lvname
   ```

### Important Notes:
- **Data Backup**: Always backup data before performing any operation that reduces the size of a logical volume.
- **Shrinking the Filesystem**: Always shrink the filesystem before shrinking the logical volume to avoid data loss.
- **Filesystem Compatibility**: Not all filesystems support shrinking. XFS, for instance, does not support shrinking directly, and you may need to recreate the volume.
- **Use `--resizefs` Option**: When reducing the LV size, it’s advisable to use the `--resizefs` option to resize the filesystem automatically, especially when increasing the LV size.

### Conclusion
`lvreduce` is a powerful command for reducing the size of a logical volume in LVM. However, it requires careful handling, especially when shrinking volumes with existing data. Always make sure to shrink the filesystem first, and back up data before performing any size reductions.
