# vgreduce

The `vgreduce` command is used in Linux Logical Volume Manager (LVM) to remove a physical volume (PV) from a volume group (VG). This is typically done after removing a disk from the system or when the physical volume is no longer needed.

### Syntax
```bash
vgreduce [--removemissing] VolumeGroupName PhysicalVolumePath
```

Where:
- **`VolumeGroupName`**: The name of the volume group from which the physical volume is being removed.
- **`PhysicalVolumePath`**: The path to the physical volume (e.g., `/dev/sdb1`).

### Common Use Cases

### 1. **Remove a Physical Volume from a Volume Group**

If you want to remove a physical volume (PV) from an existing volume group (VG), you can use the `vgreduce` command. Before removing a physical volume, you need to ensure that there are no logical volumes (LVs) using space on that PV or that all data is migrated.

#### Example: Remove a Physical Volume

```bash
sudo vgreduce vgname /dev/sdb1
```

- **`vgname`**: The volume group from which you want to remove the physical volume.
- **`/dev/sdb1`**: The physical volume you want to remove.

This command will remove `/dev/sdb1` from the volume group `vgname`. However, it is important to ensure that no logical volumes are using space from this PV. If any logical volumes are using space from this PV, you must move the data to other physical volumes using the `pvmove` command before running `vgreduce`.

### 2. **Removing a Missing Physical Volume**

If a physical volume has failed and is missing, you can use the `--removemissing` flag. This option removes the physical volume from the volume group, even if it is not available. This is typically used in situations where the device is physically removed or has failed.

#### Example: Remove a Missing Physical Volume

```bash
sudo vgreduce --removemissing vgname
```

- **`--removemissing`**: Removes the missing physical volume from the volume group.
- **`vgname`**: The volume group from which you want to remove the missing physical volume.

This will remove any missing physical volumes from the specified volume group.


### 3. **Checking the Status After Running `vgreduce`**

After running the `vgreduce` command, you can check the status of the volume group to ensure the physical volume has been successfully removed using the `vgdisplay` command.

#### Example: Check Volume Group Status

```bash
sudo vgdisplay vgname
```

This will show the updated status of the volume group `vgname`, including the list of physical volumes still part of the group.


### Important Considerations Before Running `vgreduce`

1. **Ensure Data Migration**: Before removing a physical volume, ensure that there are no logical volumes using the physical volume you are removing. You can migrate the data using the `pvmove` command.

2. **Use `vgreduce` with Caution**: Removing a physical volume from a volume group will reduce the storage capacity of the volume group, and you must ensure that no data will be lost.

---

### Example Workflow to Remove a PV:

If you're going to remove a physical volume from a volume group, follow this general workflow:

1. **Check the Volume Group**:
   ```bash
   sudo vgdisplay vgname
   ```

2. **Migrate Data (if necessary)**: If any logical volumes are using the physical volume, move the data to another physical volume using the `pvmove` command.
   ```bash
   sudo pvmove /dev/sdb1
   ```

3. **Remove the Physical Volume**:
   ```bash
   sudo vgreduce vgname /dev/sdb1
   ```

4. **Verify the Changes**:
   ```bash
   sudo vgdisplay vgname
   ```

### Conclusion

The `vgreduce` command is a key tool for managing volume groups in LVM. It allows you to safely remove physical volumes from a volume group. However, it is crucial to ensure that there are no logical volumes using the space of the PV you wish to remove and that data is not lost during the process. Always check and migrate data before performing the operation.
