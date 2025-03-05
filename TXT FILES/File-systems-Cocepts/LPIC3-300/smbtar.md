# smbtar

`smbtar` is a Samba utility designed for backing up and archiving SMB (Server Message Block) shares by creating tar archives of the share contents. It leverages the functionality of smbclient to connect to remote shares and stream their data into a tar file. This tool is especially useful in environments that use Samba for file sharing and require a simple method to back up or migrate the files stored on those shares.

## Purpose

- **Backup SMB Shares**:  
  Create a tar archive of files stored on a Samba share for backup or migration purposes.

- **Data Migration and Restoration**:  
  The generated tar file can later be used to restore the files either to the same share or to a different location.

- **Automation and Scripting**:  
  Ideal for integrating into automated backup routines or scheduled scripts, ensuring regular backups of SMB resources.

## Basic Syntax

```bash
smbtar [options] [destination.tar]
```

- **`destination.tar`**: The name (and optionally, path) of the tar archive file to create.

Note that `smbtar` typically uses smbclient configuration or additional command-line options (like specifying the share, server, and authentication details) to know which share to back up.

## Common Options and Subcommands

While `smbtar` is implemented as a script and its available options may vary slightly between Samba versions, the following options are commonly supported:

- **`-s <share>`**:  
  Specify the name of the SMB share to back up.

- **`-I <server>`**:  
  Provide the IP address or hostname of the server hosting the share.

- **`-U <user>`**:  
  Supply the username for authentication on the SMB server.

- **`-P <password>`**:  
  (Optional) Provide the password for authentication. If omitted, the script may prompt for it.

- **`-v`**:  
  Enable verbose mode for detailed output during the backup process.

- **Additional Options**:  
  Depending on your Samba version and configuration, other options may be available to tweak the behavior (such as excluding certain files or directories).

## Example Usage

1. **Basic Backup**

   Archive the SMB share named `Documents` from a server called `fileserver` into a tar file named `documents_backup.tar`:

   ```bash
   smbtar -s Documents -I fileserver -U backup_user documents_backup.tar
   ```

   *Note: If the `-P` option is omitted, you will be prompted to enter the password for `backup_user`.*

2. **Verbose Backup**

   Run the backup in verbose mode to see detailed progress:

   ```bash
   smbtar -v -s Documents -I fileserver -U backup_user documents_backup.tar
   ```

## Best Practices

- **Authentication Security**:  
  Avoid passing passwords directly on the command line when possible, as these may be exposed in process listings. Consider using configuration files or environment variables if supported.

- **Network Reliability**:  
  Ensure a stable network connection when backing up large shares, as interruptions can lead to incomplete or corrupted archives.

- **Testing Restorations**:  
  Regularly test the restoration process using the tar archive to ensure that backups are valid and complete.

- **Scheduling Backups**:  
  Integrate `smbtar` into cron jobs or other scheduling systems to automate regular backups of critical SMB shares.

## Conclusion

`smbtar` is a handy utility for administrators needing to back up or migrate data from Samba (SMB) shares. By creating tar archives of the share contents, it simplifies the backup process and can be seamlessly integrated into automated routines. Whether you're performing routine backups or migrating data to new servers, `smbtar` offers a reliable solution for managing SMB share archives.
