# `mount.cifs`

`mount.cifs` is a command used to mount a CIFS (Common Internet File System) or SMB (Server Message Block) network file system in Linux. It allows a client to access files and directories on a remote server (typically a Windows or Samba server) by mounting the network share to a local directory. CIFS is an implementation of the SMB protocol that is widely used for file sharing between Linux/Unix systems and Windows systems.

## Basic Usage

```bash
sudo mount.cifs //server_name/share_name /local_mount_point -o username=user,password=pass
```

- **//server_name/share_name**: The address of the CIFS/SMB server and the name of the shared folder.
- **/local_mount_point**: The directory on the local system where the remote share will be mounted.
- **-o options**: Options passed to the command (e.g., authentication, permissions, etc.).

## Common Options for `mount.cifs`

1. **Authentication Options**
   - `username=user`: The username required to access the share.
   - `password=pass`: The password for the specified username.
   - `domain=domain`: The domain or workgroup to which the server belongs (optional).
   - `sec=ntlmv2`: Specifies the security mode (e.g., `ntlm`, `ntlmv2`, `krb5`).
   - `credentials=path_to_file`: Specifies a file that contains the username, password, and optional domain for accessing the share.

   Example using credentials file:
   ```bash
   sudo mount.cifs //server/share /mnt/share -o credentials=/root/cifs_credentials
   ```

   **Credentials file format**:
   ```
   username=myuser
   password=mypassword
   domain=mydomain
   ```

2. **Permissions and Ownership**
   - `uid=uid`: Specifies the UID of the owner of the files on the mounted share.
   - `gid=gid`: Specifies the GID of the group for the files.
   - `file_mode=0644`: Specifies the permissions for files on the mounted share.
   - `dir_mode=0755`: Specifies the permissions for directories on the mounted share.

3. **Network Settings**
   - `vers=version`: Specifies the SMB protocol version to use. Common versions include `1.0`, `2.0`, `2.1`, `3.0`.
     Example:
     ```bash
     sudo mount.cifs //server/share /mnt/share -o vers=3.0,username=user,password=pass
     ```
   - `rw/ro`: Mount the share read-write (`rw`) or read-only (`ro`).
   - `noserverino`: Disables the use of server-provided inode numbers (sometimes useful to avoid issues with certain applications).

4. **Additional Options**
   - `noexec`: Prevents execution of binaries from the mounted filesystem.
   - `nolock`: Disables locking on the mounted filesystem.
   - `soft/hard`: Specifies whether the mount should return an error (`soft`) or retry indefinitely (`hard`) if the server is unresponsive.

## Examples

### 1. Mounting a Windows Share with Authentication

```bash
sudo mount.cifs //windows-server/share /mnt/windows-share -o username=myuser,password=mypassword
```

This mounts the Windows share `//windows-server/share` to the local directory `/mnt/windows-share` using the specified username and password.

### 2. Mounting a Samba Share Using SMB Version 2.0

```bash
sudo mount.cifs //samba-server/data /mnt/data -o vers=2.0,username=myuser,password=mypassword
```

This mounts a Samba share using SMB protocol version 2.0.

### 3. Using a Credentials File for Secure Authentication

```bash
sudo mount.cifs //fileserver/docs /mnt/docs -o credentials=/etc/cifs_creds,vers=3.0
```

In this example, the credentials (username and password) are stored in `/etc/cifs_creds`, which allows for more secure mounting by avoiding plain text passwords in the command.

### 4. Mounting a Share with Specific User and Group Permissions

```bash
sudo mount.cifs //smb-server/share /mnt/share -o username=myuser,password=mypassword,uid=1000,gid=1000,file_mode=0644,dir_mode=0755
```

This mounts the share and assigns the specified user (`uid=1000`), group (`gid=1000`), and file/directory permissions.

## Unmounting a CIFS Share

To unmount a CIFS share, use the `umount` command:

```bash
sudo umount /mnt/windows-share
```

## Checking Mounted CIFS Shares

To verify which shares are mounted, use the following command:

```bash
mount | grep cifs
```

This will list all currently mounted CIFS shares.

## Troubleshooting

1. **Invalid Protocol Version**
   - If you receive an error regarding the protocol version, you may need to explicitly specify the SMB version with the `vers` option (e.g., `vers=2.0`, `vers=3.0`).

   Example error:
   ```
   mount error(112): Host is down
   Refer to the mount.cifs(8) manual page (e.g. man mount.cifs)
   ```

   Solution:
   ```bash
   sudo mount.cifs //server/share /mnt/share -o vers=2.1,username=myuser,password=mypassword
   ```

2. **Permission Denied**
   - Ensure that the username, password, and domain (if required) are correct. Also, verify that the local user has the necessary permissions to access the local mount point directory.

3. **Slow Performance**
   - Using newer versions of the SMB protocol (e.g., `vers=3.0`) may provide better performance compared to older versions (e.g., `vers=1.0`).
   - Use the `cache=loose` or `cache=strict` options for caching file attributes, which might improve performance in certain scenarios.

## Conclusion

`mount.cifs` is a flexible and powerful command for mounting CIFS/SMB network shares on Linux systems. It allows Linux clients to access files and directories on remote Windows or Samba servers, making it an essential tool for cross-platform file sharing. By configuring appropriate options for authentication, file permissions, and SMB protocol versions, users can achieve efficient and secure access to remote resources.
