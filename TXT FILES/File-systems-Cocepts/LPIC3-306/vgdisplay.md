# vgdisplay
The `vgdisplay` command in Linux is used to display detailed information about a volume group (VG) in the Logical Volume Manager (LVM). This command shows various aspects of a volume group, including its size, the physical volumes (PVs) it contains, the logical volumes (LVs) it holds, and free space available for allocation.

### Syntax
```bash
vgdisplay [VolumeGroupName]
```

- **`VolumeGroupName`**: (Optional) The name of the volume group you want to display information about. If not specified, `vgdisplay` will display information for all volume groups.

### Common Use Cases

#### 1. **Display Information About a Specific Volume Group**

If you want to display information about a specific volume group, you can provide the volume group name as an argument.

##### Example:
```bash
sudo vgdisplay vgname
```

This will display detailed information about the volume group `vgname`.

#### 2. **Display Information for All Volume Groups**

If you want to see information about all the volume groups in the system, simply run the `vgdisplay` command without specifying a volume group name.

##### Example:
```bash
sudo vgdisplay
```

This will list details about all volume groups on the system.

### Output Information

When you run the `vgdisplay` command, the following information will be displayed:

- **VG Name**: The name of the volume group.
- **System ID**: (optional) System identifier.
- **Format**: The format of the volume group (usually LVM2).
- **Metadata Areas**: The number of areas storing metadata for the VG.
- **Metadata Copies**: The number of copies of the metadata.
- **VG Access**: The access mode for the VG.
- **VG Status**: Whether the volume group is active, unavailable, etc.
- **Max LV**: The maximum number of logical volumes allowed in the VG.
- **Cur LV**: The current number of logical volumes in the VG.
- **Open LV**: The number of logical volumes currently open.
- **Max PV**: The maximum number of physical volumes that the VG can have.
- **Cur PV**: The number of physical volumes currently in the VG.
- **Act PV**: The number of physical volumes currently active.
- **VG Size**: The total size of the volume group (including all physical volumes).
- **PE Size**: The size of a physical extent (PE). This is the basic unit of storage in LVM.
- **Total PE**: The total number of physical extents in the VG.
- **Alloc PE / Size**: The amount of physical extents allocated and the corresponding size.
- **Free PE / Size**: The free space (physical extents) in the volume group and its corresponding size.
- **VG UUID**: The unique identifier for the volume group.

---

### Example Output

```bash
$ sudo vgdisplay vgname
  --- Volume group ---
  VG Name               vgname
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Copies       1
  VG Access             read/write
  VG Status             available
  MAX LV                255
  Cur LV                2
  Open LV               2
  MAX PV                16
  Cur PV                1
  Act PV                1
  VG Size               100.00 GiB
  PE Size               4.00 MiB
  Total PE              25600
  Alloc PE / Size       10240 / 40.00 GiB
  Free  PE / Size       15360 / 60.00 GiB
  VG UUID               Xyz123-abc456-def789
```


### Key Points

- **VG Name**: Identifies the volume group.
- **VG Size**: The total size of the volume group.
- **Free PE / Size**: The free space available for new logical volumes or other allocations.
- **Alloc PE / Size**: The amount of space that is already allocated within the volume group.
- **Cur LV and Cur PV**: Show the number of logical and physical volumes in use.

### Common Options

- **`-v`**: Displays more detailed information in verbose mode.
- **`-s`**: Shows information about the physical extents in the volume group.
- **`--units`**: Allows you to specify units for displaying the sizes (e.g., `-s M` to display the size in megabytes).

### Conclusion

The `vgdisplay` command is a powerful tool for inspecting the details of volume groups in LVM. It provides insights into the size, usage, and structure of the volume group, which can be helpful for troubleshooting or managing storage configurations.
