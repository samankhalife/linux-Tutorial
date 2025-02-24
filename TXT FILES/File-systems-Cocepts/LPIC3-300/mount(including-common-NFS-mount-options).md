# mount

`mount` is a command-line utility in Unix-like operating systems used to attach filesystems to the directory tree. It supports a wide range of filesystem types including local filesystems (like ext4, xfs) and network filesystems such as NFS.

## Basic Syntax

```bash
mount [OPTIONS] DEVICE MOUNT_POINT
```

- **DEVICE**: The storage device, partition, or network share to be mounted.
- **MOUNT_POINT**: The directory where the filesystem will be attached.
- **OPTIONS**: Various flags to modify mount behavior.

## Common Options

- **`-t type`**: Specifies the filesystem type (e.g., `ext4`, `nfs`, `vfat`).
- **`-o options`**: A comma-separated list of mount options.
- **`-v`**: Verbose mode; displays detailed output.

## NFS Mount Options

When mounting an NFS share, you can fine-tune various options to optimize performance and reliability. Below are some commonly used NFS mount options:

### Basic Options

- **rw/ro**:  
  - `rw`: Mount the share as read-write.
  - `ro`: Mount the share as read-only.

- **vers=**:  
  Specifies the NFS protocol version (e.g., `vers=3` or `vers=4`).

### Performance Options

- **rsize and wsize**:  
  Define the maximum chunk sizes (in bytes) for read and write operations.
  - Example: `rsize=8192,wsize=8192`

- **async**:  
  Allows asynchronous writes, which can improve performance at the cost of data integrity in the event of a crash.

- **sync**:  
  Forces synchronous writes for improved data integrity, though it may reduce performance.

### Reliability Options

- **hard vs. soft**:  
  - `hard`: The client retries indefinitely if the server becomes unresponsive (recommended for data integrity).
  - `soft`: The client will eventually time out, which can lead to errors if the server remains unavailable.

- **intr**:  
  Allows NFS requests to be interrupted if the server is unresponsive, which is useful with hard mounts.

- **timeo**:  
  Sets the timeout (in tenths of a second) for NFS requests.
  - Example: `timeo=14`

- **retrans**:  
  Specifies the number of times to retry a request before giving up.
  - Example: `retrans=3`

### Locking Options

- **nolock**:  
  Disables NFS file locking. Useful if file locking is managed by another mechanism.

### Background and Foreground Options

- **bg**:  
  If the initial mount attempt fails, retry in the background.
  
- **fg**:  
  Forces the mount operation to run in the foreground (default behavior).

## Example: Mounting an NFS Share

To mount an NFS share exported from a server with IP address `192.168.1.100` (exporting `/export/shared`) to a local mount point `/mnt/shared`, you might use:

```bash
mount -t nfs -o rw,vers=4,rsize=8192,wsize=8192,hard,intr,timeo=14,retrans=3 192.168.1.100:/export/shared /mnt/shared
```

This command mounts the NFS share with the following options:
- **Read-Write** (`rw`)
- **Using NFS Version 4** (`vers=4`)
- **Optimized Read/Write Sizes** (`rsize=8192,wsize=8192`)
- **Hard Mount with Interrupts Enabled** (`hard,intr`)
- **Custom Timeout and Retransmission Settings** (`timeo=14,retrans=3`)

## Conclusion

The `mount` command is essential for attaching both local and network filesystems. When dealing with NFS, a variety of mount options are available to customize performance, reliability, and security. By using options like `rsize`, `wsize`, `hard`, `intr`, `timeo`, and `vers`, administrators can optimize NFS mounts to suit their specific environment.

