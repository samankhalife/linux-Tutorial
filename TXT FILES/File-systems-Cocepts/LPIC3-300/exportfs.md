# exportfs 

The `exportfs` command is used in Linux systems to manage NFS (Network File System) file system exports. It allows administrators to view, add, and remove NFS shares without directly modifying the `/etc/exports` file. This command is part of the NFS server utilities and is essential for dynamically managing shared file systems.

## Purpose

- **Export NFS Directories**:  
  The primary purpose of `exportfs` is to export or unexport directories specified in the `/etc/exports` file, making them available to NFS clients.
  
- **Manage Active Exports**:  
  The command can be used to modify the list of currently exported directories without restarting the NFS server, providing real-time control over NFS exports.

## Common Usage

Here are the most common options and examples of how to use `exportfs`:

### 1. **Export All Filesystems**
   This exports all the filesystems defined in the `/etc/exports` file. This is useful after editing the `/etc/exports` file.

   ```bash
   sudo exportfs -a
   ```

   - **`-a`**: Export or unexport all directories listed in `/etc/exports`.

### 2. **Display Active Exports**
   You can display a list of all currently exported directories along with their options using:

   ```bash
   sudo exportfs -v
   ```

   - **`-v`**: Shows detailed information about the exported filesystems, including client access rights.

### 3. **Unexport a Specific Directory**
   You can unexport a specific directory (remove it from being shared with clients) by using the following command:

   ```bash
   sudo exportfs -u /path/to/directory
   ```

   - **`-u`**: Unexports the specified directory, making it unavailable to clients.

### 4. **Unexport All Directories**
   To unexport all exported directories, use:

   ```bash
   sudo exportfs -ua
   ```

   This removes all active exports, making all shared directories inaccessible to clients.

### 5. **Export a Directory Manually**
   You can also export a directory manually without editing the `/etc/exports` file. For example:

   ```bash
   sudo exportfs -o rw,sync 192.168.1.0/24:/path/to/share
   ```

   In this case, the directory `/path/to/share` is exported to all clients in the `192.168.1.0/24` subnet with read-write (`rw`) and synchronous (`sync`) options.

   - **`-o`**: Specifies the export options (same options as in `/etc/exports`).

### 6. **Refresh Exports**
   If you modify the `/etc/exports` file and want to apply the changes without restarting the NFS server, use:

   ```bash
   sudo exportfs -r
   ```

   - **`-r`**: Reexports all filesystems, incorporating any changes made to the `/etc/exports` file.

## Example Scenarios

### Scenario 1: Dynamically Adding an Export

Suppose you want to temporarily share a directory with a specific subnet:

```bash
sudo exportfs -o rw,no_subtree_check 192.168.1.0/24:/srv/shared
```

This exports `/srv/shared` to the `192.168.1.0/24` subnet with read-write access and without performing subtree checks.

### Scenario 2: Unexporting a Directory

To stop sharing the `/srv/shared` directory:

```bash
sudo exportfs -u /srv/shared
```

This unexports the directory, making it inaccessible to clients.

### Scenario 3: Verifying Active Exports

After setting up your exports, you can check the current active exports using:

```bash
sudo exportfs -v
```

This will display a list of all active exports, along with client permissions and options.

## exportfs Options Summary

Here’s a quick summary of some key options for the `exportfs` command:

- **`-a`**: Export all filesystems listed in `/etc/exports`.
- **`-u`**: Unexport the specified directory.
- **`-r`**: Reexport all directories, useful for applying changes made in `/etc/exports`.
- **`-v`**: Show detailed information about exported filesystems.
- **`-o`**: Manually specify export options for a directory.
  
## Conclusion

The `exportfs` command is an essential tool for managing NFS exports on Linux systems. It allows for the dynamic exporting and unexporting of directories without requiring a restart of the NFS server, making it a convenient utility for real-time management of file-sharing environments.
