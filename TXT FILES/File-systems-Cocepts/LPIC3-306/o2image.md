# o2image

The `o2image` command is a utility used in the context of Oracle ZFS Storage Appliance (formerly Sun ZFS Storage Appliance). It is primarily used for creating and managing ZFS snapshots, or for performing data protection tasks, including backing up and restoring ZFS-based datasets. The `o2image` tool can work with the image-based snapshot system in Oracle ZFS to provide quick backups and restores.

This command is commonly used by administrators in environments where Oracle ZFS Storage Appliances are deployed, ensuring that critical data is protected and easily restorable.

## Purpose

- **Create ZFS Snapshots**:  
  The `o2image` command allows you to create snapshots of datasets or volumes, which can be used for backups or rollbacks to a previous state.
  
- **Backup and Restore Operations**:  
  Facilitates creating backup images of ZFS datasets and volumes. It also allows for restoring these datasets from the created snapshots.

- **Data Protection**:  
  Ensures that data is consistently protected and can be easily restored in case of failure or corruption, leveraging ZFS’s snapshot and cloning features.

## Basic Syntax

```bash
o2image [OPTIONS] <COMMAND> <ARGUMENTS>
```

Where:
- **<COMMAND>**: The specific action to be performed, such as creating, listing, or restoring images.
- **<ARGUMENTS>**: Additional parameters needed for the specific command.

## Common Options

- **create**:  
  Create a new image (snapshot) from an existing ZFS dataset or volume.
  
```bash
o2image create -v -d <dataset> -n <snapshot_name>
```

- **list**:  
  List all available images (snapshots) for a specified dataset or volume.
  
```bash
o2image list <dataset>
```

- **restore**:  
  Restore a dataset or volume from a previously created snapshot.
  
```bash
o2image restore -n <snapshot_name> -d <dataset>
```

- **delete**:  
  Delete an existing snapshot.
  
```bash
o2image delete -n <snapshot_name>
```

- **-v**:  
  Verbose output, providing detailed information about the operation.

- **-d <dataset>**:  
  Specifies the dataset or volume to operate on.

- **-n <snapshot_name>**:  
  Specifies the name of the snapshot being created, restored, or deleted.

## Example Usage

1. **Creating a Snapshot**

```bash
o2image create -v -d /tank/mydata -n backup_2025_03_09
```
This command creates a snapshot named `backup_2025_03_09` for the dataset `/tank/mydata`. The `-v` option provides verbose output, showing the status of the operation.

2. **Listing Snapshots**

```bash
o2image list /tank/mydata
```
This command lists all available snapshots for the dataset `/tank/mydata`.

3. **Restoring a Snapshot**

```bash
o2image restore -n backup_2025_03_09 -d /tank/mydata
```
This command restores the dataset `/tank/mydata` from the snapshot `backup_2025_03_09`.

4. **Deleting a Snapshot**

```bash
o2image delete -n backup_2025_03_09
```
This command deletes the snapshot `backup_2025_03_09` from the system.

## Best Practices

- **Regular Snapshots**:  
  Take regular snapshots of critical datasets or volumes to ensure you have a point-in-time backup in case of system failure.

- **Snapshot Naming**:  
  Use descriptive and consistent naming conventions for snapshots, such as including timestamps, to make it easier to identify and restore specific snapshots.

- **Test Restores**:  
  Periodically test restoring from snapshots to ensure that the backup and recovery process works as expected.

- **Clean Up Old Snapshots**:  
  Regularly remove old or unnecessary snapshots to free up storage space and prevent the system from becoming cluttered with outdated backups.

## Conclusion

`o2image` is an essential tool for administrators working with Oracle ZFS Storage Appliances, offering functionality to manage snapshots, backups, and restores. By leveraging the ZFS snapshot technology, `o2image` enables fast, efficient, and reliable data protection, ensuring critical datasets are safely stored and easily restorable in the event of data loss or corruption.
