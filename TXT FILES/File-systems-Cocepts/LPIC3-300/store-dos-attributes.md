# store-dos-attributes

`store-dos-attributes` is a Samba configuration parameter that controls whether Windows (DOS) file attributes—such as the archive, hidden, system, and readonly flags—are stored persistently on files and directories. When enabled, these attributes are saved (typically in extended attributes or alternate data streams) so that they are preserved even on filesystems that do not natively support DOS attributes.

## Purpose

- **Preservation of Windows Attributes**:  
  Ensures that files retain important DOS attributes when stored on a Unix-like filesystem, which might not support these attributes by default.

- **Interoperability**:  
  Improves compatibility with Windows clients by preserving attributes like hidden, system, and archive bits, allowing files to appear with the correct properties when accessed from Windows.

## How It Works

- When `store dos attributes` is set to `yes`, Samba stores the DOS attribute flags in the file's extended attributes (or alternate data streams).  
- This allows the attributes to be maintained across file operations, such as copying or moving files, and ensures that they are visible to both Samba and Windows systems.

## Configuration

Add the following line to the `[global]` section of your `smb.conf` file to enable the feature:

```ini
[global]
   store dos attributes = yes
```

- **`yes`**: Enables the storage of DOS attributes.
- **`no`**: Disables this feature, meaning that DOS attributes may not be preserved when files are written to the share.

## Use Cases

- **Mixed-OS Environments**:  
  Ideal for networks where files are shared between Windows and Unix systems, ensuring that Windows-specific file attributes are maintained.
  
- **File Migration and Backup**:  
  Helps preserve the integrity of file attributes during migration from Windows to Samba shares hosted on Unix systems.
  
- **User Experience**:  
  Ensures that files appear with the expected attributes (e.g., hidden or system files remain hidden) when accessed from Windows clients.

## Considerations

- **Filesystem Support**:  
  The underlying filesystem must support extended attributes (xattrs) or alternate data streams. Filesystems like ext4, XFS, or Btrfs typically support these features.
  
- **Performance Impact**:  
  Storing extended attributes might introduce a slight performance overhead. Evaluate the impact in your environment, especially on high-performance systems.
  
- **Compatibility with Other Modules**:  
  Ensure that this setting does not conflict with other VFS modules (like `streams_xattr` or `acl_xattr`) that manage file metadata.

## Conclusion

Enabling `store dos attributes` in Samba allows you to maintain Windows-specific file attributes on Unix filesystems, ensuring a consistent experience for Windows clients and preserving file metadata during transfers. This is especially useful in mixed operating system environments or during file migrations. Proper filesystem support and configuration testing are essential to ensure smooth operation.
