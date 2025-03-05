# lvcreate

The `lvcreate` command in Linux is used to create a new logical volume (LV) within a volume group (VG) in a Logical Volume Manager (LVM) setup. It allows you to allocate space from a volume group and create a logical volume with a specified size and options.

### Syntax

```bash
lvcreate [options] -L <size> -n <lvname> <vgname>
```

Where:
- **`-L <size>`**: Specifies the size of the logical volume.
- **`-n <lvname>`**: Specifies the name of the logical volume.
- **`<vgname>`**: The name of the volume group where the logical volume will be created.

You can also create a logical volume with the `-l` option to specify the number of logical extents (instead of size in GiB).

### Common Options

- **`-L <size>`**: Specifies the size of the logical volume. The size can be specified in GB, MB, or other units (e.g., `-L 10G` for 10 GiB).
- **`-l <extents>`**: Specifies the number of extents to allocate for the logical volume (useful if you're working with extents instead of a specific size).
- **`-n <lvname>`**: Sets the name of the logical volume.
- **`-f`**: Forces the creation of the logical volume, even if it conflicts with an existing LV name.
- **`--size`**: Specifies the size of the logical volume in MB, GB, etc.
- **`--name`**: Specifies the name of the logical volume.
- **`--type`**: Specifies the type of logical volume (e.g., `thin` for thin provisioning).
- **`--stripes`**: Specifies the number of stripes across physical volumes in the volume group (for striped logical volumes).
- **`--mirror`**: Creates a mirrored logical volume (requires additional disks in the volume group).
- **`--size`**: Specifies the size of the logical volume.

### Example Usage

1. **Create a Logical Volume with a Specific Size**
   To create a 10 GiB logical volume named `lvdata` in the volume group `vgname`, use the following command:
   ```bash
   sudo lvcreate -L 10G -n lvdata vgname
   ```
   This creates a 10 GiB logical volume named `lvdata` within the `vgname` volume group.

2. **Create a Logical Volume Using Extents**
   Instead of specifying the size, you can specify the number of logical extents. For example, if each extent is 4 MiB and you want a 20 GiB volume, you would use:
   ```bash
   sudo lvcreate -l 5120 -n lvdata vgname
   ```

3. **Create a Thin-Provisioned Logical Volume**
   You can create a thin-provisioned logical volume by specifying the `--type thin` option. This type of logical volume allows for more flexible space management.
   ```bash
   sudo lvcreate --type thin -L 10G -n lvthin vgname
   ```

4. **Create a Striped Logical Volume (RAID 0)**
   You can create a striped logical volume to distribute data across multiple physical volumes for better performance.
   ```bash
   sudo lvcreate --stripes 2 -L 10G -n lvstripe vgname
   ```
   This creates a 10 GiB striped volume across 2 physical volumes in the `vgname` volume group.

5. **Create a Mirrored Logical Volume (RAID 1)**
   For redundancy, you can create a mirrored logical volume. This requires having at least two physical volumes in the volume group.
   ```bash
   sudo lvcreate --mirror 1 -L 10G -n lvmirror vgname
   ```
   This creates a mirrored 10 GiB logical volume.

6. **Create a Logical Volume and Format it**
   After creating a logical volume, you typically format it with a filesystem:
   ```bash
   sudo mkfs.ext4 /dev/vgname/lvdata
   ```

7. **Create a Logical Volume with a Specified Volume Group**
   You can also specify the volume group explicitly:
   ```bash
   sudo lvcreate -L 5G -n lvexample vgexample
   ```

### Example Output

When you successfully create a logical volume, you will see output similar to this:

```
  Logical volume "lvdata" created.
```

### Viewing the Created Logical Volume

After creating the logical volume, you can use `lvdisplay` to verify the details:

```bash
sudo lvdisplay /dev/vgname/lvdata
```

### Conclusion

The `lvcreate` command is essential for creating new logical volumes within a volume group in LVM. It allows for a variety of configurations, including striped volumes, mirrored volumes, and thin provisioning. You can specify the size of the volume or the number of extents and further customize the logical volume with various options like mirroring or striping for better performance and redundancy.
