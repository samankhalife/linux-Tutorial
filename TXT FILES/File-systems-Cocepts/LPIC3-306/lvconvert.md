# lvconvert
The `lvconvert` command is used in Linux Logical Volume Manager (LVM) to modify the properties of an existing logical volume (LV). It allows you to convert a logical volume to a different type or configuration. For example, you can convert a regular volume into a thinly provisioned volume, a mirrored volume, or even add or remove mirrors.

### Syntax

```bash
lvconvert [options] <lvname>
```

Where:
- **`<lvname>`**: The name of the logical volume you want to modify (e.g., `/dev/vgname/lvname`).

### Common Use Cases

Here are some common ways to use `lvconvert`:

### 1. **Convert to a Mirrored Logical Volume**

If you have a non-mirrored logical volume (LV) and want to convert it to a mirrored LV, you can use the following syntax. The `--mirror` option allows you to create a mirrored volume.

#### Example: Convert to a Mirrored Volume (RAID 1)

```bash
sudo lvconvert --mirror 1 /dev/vgname/lvname
```

- **`--mirror 1`**: This option specifies that one mirror copy should be created. You need at least two physical volumes in the volume group for mirroring.
- This command will add a mirror to the logical volume, giving you redundancy (RAID 1).

### 2. **Convert to a Thin-Provisioned Logical Volume**

You can convert a standard logical volume to a thin-provisioned volume (thin provisioning allows you to allocate space as needed, rather than reserving it all upfront).

#### Example: Convert to Thin Volume

```bash
sudo lvconvert --type thin /dev/vgname/lvname
```

- **`--type thin`**: Specifies that the logical volume should be converted to a thin-provisioned volume.
- This command will allow you to make better use of space by allocating space only when the data is actually written to the volume.

### 3. **Convert Thin-Provisioned to Regular Volume**

If you no longer need the thin provisioning and want to convert it back to a regular volume, you can use `lvconvert` with the `--type` option set to `default`.

#### Example: Convert Thin Volume to Regular Volume

```bash
sudo lvconvert --type default /dev/vgname/lvname
```

- **`--type default`**: Converts the thin-provisioned LV back to a standard LV, with space allocated upfront.

### 4. **Convert to a Snapshot Volume**

You can convert a regular logical volume into a snapshot logical volume, which is a read-only copy of the original logical volume that can be used for backups or testing purposes.

#### Example: Convert to Snapshot

```bash
sudo lvconvert --snapshot /dev/vgname/lvname
```

- **`--snapshot`**: Converts the logical volume into a snapshot, which is a point-in-time copy of the LV.

### 5. **Add Mirrors to an Existing Logical Volume**

If you have a mirrored logical volume and want to add more mirrors (i.e., create RAID 1+N), you can use `lvconvert` with the `--addmirror` option.

#### Example: Add a Mirror to an Existing LV

```bash
sudo lvconvert --addmirror 1 /dev/vgname/lvname
```

- **`--addmirror 1`**: Adds one additional mirror to the logical volume.
- You can add multiple mirrors (e.g., `--addmirror 2` for two additional mirrors).

### 6. **Remove a Mirror from a Logical Volume**

If you want to reduce the number of mirrors in a mirrored LV, you can use the `--removemirror` option.

#### Example: Remove a Mirror

```bash
sudo lvconvert --removemirror /dev/vgname/lvname
```

- **`--removemirror`**: Removes one mirror copy of the logical volume. You cannot remove the last mirror if there's only one mirror left.

### 7. **Convert to a Striped Logical Volume (RAID 0)**

You can also convert a logical volume to a striped volume (RAID 0) for better performance.

#### Example: Convert to Striped Volume

```bash
sudo lvconvert --stripes 2 /dev/vgname/lvname
```

- **`--stripes 2`**: Specifies that the volume should be striped across two devices. You can increase this number for more stripes.

### 8. **Convert to a Linear Volume (Remove Striping)**

If you want to revert a striped logical volume to a regular linear volume, you can use the `--type` option:

#### Example: Convert to a Linear Volume

```bash
sudo lvconvert --type linear /dev/vgname/lvname
```

- **`--type linear`**: Converts a striped or mirrored volume back to a linear volume, removing any striping or mirroring configuration.

### Example Outputs

1. **Successfully converting to a mirrored volume**:
   ```bash
   Conversion of /dev/vgname/lvname to a mirrored volume successful.
   ```

2. **Successfully converting to a thin volume**:
   ```bash
   Logical volume /dev/vgname/lvname converted to thin provisioning.
   ```

3. **Adding a mirror to an existing volume**:
   ```bash
   Logical volume /dev/vgname/lvname now has 2 mirrors.
   ```

### Conclusion

The `lvconvert` command is a powerful tool in LVM that allows you to modify the characteristics of an existing logical volume, including converting it to a mirrored, striped, or thin-provisioned volume. It can also be used to add or remove mirrors from an existing logical volume, providing flexibility for RAID configurations and space management.

Key use cases include:
- Converting to or from mirrored (RAID 1) volumes.
- Converting to or from thin-provisioned volumes.
- Adding or removing mirrors and stripes for performance or redundancy purposes.
