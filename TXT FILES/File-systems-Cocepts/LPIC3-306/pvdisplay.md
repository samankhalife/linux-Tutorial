# pvdisplay

The `pvdisplay` command in Linux is used to display detailed information about a physical volume (PV) in the Logical Volume Manager (LVM) system. This command helps administrators view the status, size, and allocation details of physical storage devices managed by LVM.

### Key Information Displayed by `pvdisplay`:
- **Physical Volume Name**: The name of the physical volume (e.g., `/dev/sda1`).
- **Volume Group**: The volume group (VG) to which the PV belongs.
- **Size**: The total size of the physical volume.
- **Free Space**: The free (unallocated) space within the physical volume.
- **Allocated Space**: The space already allocated to logical volumes (LVs).
- **Physical Extents (PE)**: The allocation units used by LVM to manage the physical volume. It shows the total number of extents and the size of each extent.
- **UUID**: A unique identifier for the physical volume.
- **Status**: Whether the physical volume is active, in use, or missing.

### Example:
```bash
$ pvdisplay /dev/sda1
  --- Physical volume ---
  PV Name               /dev/sda1
  VG Name               vg_data
  PV Size               500.00 GiB / not usable 4.00 MiB
  Allocatable           yes (but full)
  PE Size               4.00 MiB
  Total PE              127999
  Free PE               0
  Allocated PE          127999
  PV UUID               Ydk8Q6-YndF-GnF5-Fdoe-dfo9-MFCb-2fg4rQ
```

### Conclusion:
The `pvdisplay` command is a vital tool for managing physical volumes in LVM. It allows administrators to check the status of physical volumes, monitor their space allocation, and ensure that the physical volumes are properly allocated and functioning within their respective volume groups. This tool helps identify any issues such as insufficient free space or faulty devices within the LVM configuration.
