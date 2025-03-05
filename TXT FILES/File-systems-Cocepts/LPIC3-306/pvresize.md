# pvresize
The `pvresize` command in Linux is used to resize a physical volume (PV) in the Logical Volume Manager (LVM). This command allows you to increase or decrease the size of an existing physical volume. Typically, this is done when you have extended or reduced the size of the underlying storage device (such as a hard disk or partition), and you want LVM to recognize the changes and adjust the physical volume size accordingly.

### Syntax
```bash
pvresize [options] <PhysicalVolumePath>
```

- **`<PhysicalVolumePath>`**: The path to the physical volume you want to resize (e.g., `/dev/sda1`, `/dev/vgname/lvname`).

### Options
- **`-d, --debug`**: Enables debugging output.
- **`-h, --help`**: Displays help information.
- **`--setphysicalvolumesize`**: Specifies the new size for the physical volume.
- **`-v, --verbose`**: Shows verbose output.

### Example Usage

#### 1. **Resize a Physical Volume**

If you expand or shrink the underlying disk or partition (e.g., `/dev/sda1`), you can use `pvresize` to resize the physical volume to match the new disk size. For example:

```bash
sudo pvresize /dev/sda1
```

This command rescans the `/dev/sda1` physical volume and adjusts the size to match any changes that have been made to the underlying disk.

#### 2. **Resize a Physical Volume with a Specific Size**

You can also manually specify the new size for the physical volume (though this is not common unless you have a very specific requirement). For example, to resize the physical volume `/dev/sda1` to 50 GB:

```bash
sudo pvresize --setphysicalvolumesize 50G /dev/sda1
```

This will adjust the size of the physical volume to 50 GB.

#### 3. **Resizing After Expanding a Partition**

If you have expanded a partition (say using `fdisk` or `parted`), you can run `pvresize` to make the physical volume take up the entire space of the resized partition. For example, after resizing the partition `/dev/sda1`, you would use:

```bash
sudo pvresize /dev/sda1
```

This will allow LVM to detect the additional space and make it available for use.

### Example Output
When you successfully run the `pvresize` command, you should see output similar to the following:

```bash
  Physical volume "/dev/sda1" changed
  1 physical volume(s) resized / 0 physical volume(s) not resized
```

This indicates that the physical volume `/dev/sda1` was resized successfully.

### Important Notes

- **Resizing Physical Volumes**: You cannot shrink a physical volume that is part of an active volume group if there is not enough free space in the volume group. You must ensure that there is enough free space in the volume group before resizing down a physical volume.
- **Extending Physical Volumes**: Extending a physical volume is more common, especially when adding new disk space to the system. In this case, `pvresize` will automatically adjust to the new disk size and make additional space available.
- **Resizing with Caution**: Always ensure that you back up important data before performing operations like resizing, as there can be risks of data loss if something goes wrong.

### Conclusion
`pvresize` is a powerful command for resizing physical volumes in LVM. It's especially useful when your underlying storage device changes size (such as when increasing disk space). This flexibility allows you to manage storage efficiently and scale your systems dynamically.
