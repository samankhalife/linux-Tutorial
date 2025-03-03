# /etc/exports

`/etc/exports` is a term that typically refers to the `/etc/exports` file in Linux-based systems, particularly in the context of NFS (Network File System) configuration. This file is crucial for defining which directories on an NFS server are shared with clients and what permissions those clients have for accessing the shared directories.

## Purpose

- **Define NFS Shares**:  
  The `/etc/exports` file is used to specify directories that should be made available (exported) to NFS clients.
  
- **Control Access**:  
  You can define which clients (by IP address or hostname) are allowed to access the shared directories and specify the level of access (read-only, read-write).

## Structure of `/etc/exports`

The file typically contains a list of shared directories along with the clients allowed to access them and their respective permissions. Each entry follows this basic syntax:

```bash
<directory> <client1>(options) <client2>(options)
```

- **`<directory>`**: The path to the directory being shared.
- **`<client>`**: The IP address, hostname, or network range of the client allowed to access the shared directory.
- **`(options)`**: A list of options specifying how the client can access the directory.

## Example Entry

```bash
/home/shared 192.168.1.100(rw,sync,no_root_squash) 192.168.1.0/24(ro,sync)
```

In this example:
- `/home/shared` is the directory being shared.
- `192.168.1.100` is allowed read-write (`rw`) access.
- Clients from the `192.168.1.0/24` subnet are allowed read-only (`ro`) access.
- Both clients use the `sync` option, meaning data is written to disk before the client is notified.
- The `no_root_squash` option allows the root user on `192.168.1.100` to access files as root, which is typically disabled for security.

## Common Export Options

- **`rw`**:  
  Allows the client to read and write to the shared directory.

- **`ro`**:  
  Allows the client to only read from the shared directory.

- **`sync`**:  
  Requires the server to write changes to disk before responding to the client.

- **`async`**:  
  Allows the server to respond before changes are written to disk, which can improve performance but may lead to data loss in case of a crash.

- **`no_root_squash`**:  
  Allows the client’s root user to have root privileges on the shared directory. Without this, root on the client is mapped to a non-privileged user on the server for security.

- **`root_squash`**:  
  Ensures that the root user on the client is mapped to an unprivileged user (`nfsnobody` or another UID) on the server for security reasons.

- **`no_subtree_check`**:  
  Disables subtree checking, improving performance when the shared directory is large or deeply nested. It prevents the NFS server from verifying that a file accessed by the client is within the exported subtree.

- **`secure`**:  
  Restricts the client to using ports below 1024 for NFS communication. This is the default for added security.

## Managing Exports

After editing the `/etc/exports` file, you need to apply the changes by either restarting the NFS service or using the `exportfs` command.

- **Export All Filesystems**:  
  To immediately export all filesystems defined in `/etc/exports`, run:
  ```bash
  sudo exportfs -a
  ```

- **Display Active Exports**:  
  To view all currently exported filesystems:
  ```bash
  sudo exportfs -v
  ```

- **Unexport a Directory**:  
  To unexport a specific directory:
  ```bash
  sudo exportfs -u /path/to/directory
  ```

## Example Workflow

1. **Edit `/etc/exports`**:
   Open the file with a text editor like `nano` or `vi` to define NFS shares.
   ```bash
   sudo nano /etc/exports
   ```

2. **Define Export**:
   Add an entry for the directory you want to share:
   ```bash
   /srv/nfs 192.168.0.0/24(rw,sync,no_subtree_check)
   ```

3. **Apply Changes**:
   Use `exportfs` to apply the changes:
   ```bash
   sudo exportfs -ra
   ```

4. **Start or Restart NFS**:
   Ensure the NFS service is running:
   ```bash
   sudo systemctl restart nfs-kernel-server
   ```

5. **Verify Exports**:
   Use `exportfs` to check active exports:
   ```bash
   sudo exportfs -v
   ```

## Best Practices

- **Use Subnet Masks**:  
  When exporting directories, it's best to use network ranges (e.g., `192.168.1.0/24`) rather than individual IP addresses to simplify configuration and ensure all clients in a network have access.

- **Avoid `no_root_squash` Unless Necessary**:  
  This option can pose a security risk, as it allows root users on the client system to have root access on the server.

- **Use `sync` for Data Integrity**:  
  While `async` may improve performance, it's safer to use `sync` to ensure data is written to disk before the client is notified.

## Conclusion

The `/etc/exports` file plays a vital role in NFS server configuration, defining which directories are shared and controlling client access. Understanding its structure and options is essential for configuring NFS shares securely and efficiently.
