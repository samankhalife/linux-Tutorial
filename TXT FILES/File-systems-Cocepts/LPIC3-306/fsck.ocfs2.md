# fsck.ocfs2

The `fsck.ocfs2` command is used to **check and repair** OCFS2 (Oracle Cluster File System 2) file systems. This tool is essential for maintaining the integrity of OCFS2 volumes, particularly in the event of an unclean shutdown or suspected corruption.

Since OCFS2 is a shared disk file system that can be accessed by multiple nodes in a cluster, it's important to ensure that the file system is healthy and consistent across all nodes.

### Purpose

- **File System Consistency Check**:  
  The primary purpose of `fsck.ocfs2` is to check the consistency of an OCFS2 file system.
  
- **Repair Corruption**:  
  It can also repair any inconsistencies or corruption found during the check. This is important when a file system becomes damaged due to system crashes, power failures, or hardware issues.

### Basic Syntax

```bash
fsck.ocfs2 [OPTIONS] <DEVICE>
```

- **`<DEVICE>`**: The block device or partition containing the OCFS2 file system that you want to check or repair (e.g., `/dev/sdb1`).

### Common Options

- **`-a` or `--auto`**:  
  Automatically attempt to fix file system problems without user interaction.

  Example:
  ```bash
  fsck.ocfs2 -a /dev/sdb1
  ```

- **`-y`**:  
  Assume "yes" to all questions, similar to the `-a` option. This is useful when you want `fsck.ocfs2` to proceed without prompting the user for confirmation during repairs.

  Example:
  ```bash
  fsck.ocfs2 -y /dev/sdb1
  ```

- **`-n`**:  
  Do not modify the file system. This performs a read-only check, useful for diagnosing issues without making any changes to the file system.

  Example:
  ```bash
  fsck.ocfs2 -n /dev/sdb1
  ```

- **`-r`**:  
  Repair file system errors without prompting. This is similar to the `-y` option but can be used in cases where you want to skip certain interactive prompts.

  Example:
  ```bash
  fsck.ocfs2 -r /dev/sdb1
  ```

- **`-v`** or **`--verbose`**:  
  Provide verbose output during the file system check and repair process. This is useful for getting detailed information about what `fsck.ocfs2` is doing.

  Example:
  ```bash
  fsck.ocfs2 -v /dev/sdb1
  ```

- **`-f`** or **`--force`**:  
  Force a file system check even if the file system appears clean. Normally, `fsck.ocfs2` skips checking a file system that was cleanly unmounted.

  Example:
  ```bash
  fsck.ocfs2 -f /dev/sdb1
  ```

- **`-C`** or **`--cluster-name`**:  
  Specify the cluster name if the file system belongs to a cluster with a specific name. This is used to target the correct OCFS2 cluster when running checks.

  Example:
  ```bash
  fsck.ocfs2 -C mycluster /dev/sdb1
  ```

### Example Usage

1. **Perform a Basic File System Check**

   To check the OCFS2 file system on `/dev/sdb1`:

   ```bash
   fsck.ocfs2 /dev/sdb1
   ```

   This performs a read-only check of the file system for inconsistencies. If any issues are found, `fsck.ocfs2` will prompt you for action.

2. **Automatically Fix Errors**

   To automatically attempt to fix any file system errors found:

   ```bash
   fsck.ocfs2 -a /dev/sdb1
   ```

   This will run the check and repair any issues without asking for user confirmation.

3. **Force a Check**

   To force a check even if the file system is marked as clean:

   ```bash
   fsck.ocfs2 -f /dev/sdb1
   ```

   This can be useful if you suspect corruption but the system believes the file system was cleanly unmounted.

4. **Read-Only Check**

   To run `fsck.ocfs2` in read-only mode without making any modifications:

   ```bash
   fsck.ocfs2 -n /dev/sdb1
   ```

   This will display any detected problems but will not attempt to fix them.

5. **Verbose Check with Automatic Repair**

   To check and repair a file system with detailed output, use:

   ```bash
   fsck.ocfs2 -v -a /dev/sdb1
   ```

   This provides verbose information about the file system check and repairs while automatically fixing any issues.

### Automating with `cron`

You can schedule periodic file system checks using `cron` to ensure that the OCFS2 file system remains healthy over time. For example, you can create a `cron` job that runs `fsck.ocfs2` on a regular basis.

Example:

```bash
0 2 * * 1 root fsck.ocfs2 -a /dev/sdb1
```

This cron job will automatically run a file system check every Monday at 2 AM and attempt to repair any issues without user intervention.

### Best Practices

- **Perform Regular Checks**:  
  Even though OCFS2 is designed for high availability, performing regular checks ensures that any latent file system issues are caught before they cause problems.

- **Backup Data Before Repair**:  
  Always back up critical data before running `fsck.ocfs2` with repair options, especially on production systems. Although `fsck.ocfs2` is designed to repair issues, there is always a small risk of data loss when repairing file system corruption.

- **Use Read-Only Mode for Diagnosis**:  
  Run `fsck.ocfs2` in read-only mode (`-n`) when diagnosing potential issues, especially in shared or clustered environments where other nodes may be accessing the file system.

- **Unmount Before Running**:  
  It is generally best to ensure that the OCFS2 file system is unmounted before running `fsck.ocfs2`, especially when making repairs, to avoid conflicts with running applications.

### Example Output

When running `fsck.ocfs2`, you may see output like the following:

```bash
fsck.ocfs2 1.8.2
Checking OCFS2 file system in /dev/sdb1:
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking reference counts
Pass 4: Checking group summary
/dev/sdb1: 1059/130000 files (0.0% non-contiguous), 12000/520000 blocks
```

This output shows the progress of the file system check through its various phases and reports any issues encountered.

### Conclusion

The `fsck.ocfs2` command is essential for ensuring the health and integrity of OCFS2 file systems in clustered environments. By regularly checking and repairing file systems, administrators can avoid corruption and maintain high availability for critical applications using OCFS2. It’s important to use this tool with care, particularly when performing repairs, and always have backups of important data before proceeding with file system modifications.
