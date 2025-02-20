# vfs_acl_tdb

**vfs_acl_tdb** is a Samba Virtual File System (VFS) module that provides support for Windows NT-style Access Control Lists (ACLs) by storing the ACL information in a TDB (Trivial Database) file rather than in extended attributes. This module is particularly useful in environments where the underlying filesystem does not support extended attributes (xattr) or when administrators prefer to manage ACL data separately from the files themselves.

## Purpose

- **Windows ACL Emulation**:  
  Enables Samba to emulate Windows ACLs on Unix-like filesystems by maintaining ACL information externally. This allows Windows clients to correctly interpret file permissions on Samba shares.

- **Alternative to Extended Attributes**:  
  When extended attributes are not available or reliable on the underlying filesystem, `vfs_acl_tdb` offers a viable alternative by storing ACLs in a TDB file.

## How It Works

- **External ACL Storage**:  
  Instead of using the native filesystem’s extended attribute mechanism, `vfs_acl_tdb` writes the ACL data into a dedicated TDB file. This file acts as a separate database for ACL information.
  
- **Integration with Samba**:  
  Once enabled, the module intercepts file operations on Samba shares to apply or modify the Windows ACLs stored in the TDB. This ensures that access permissions are enforced according to the ACLs defined for each file or directory.

## Configuration

To use `vfs_acl_tdb`, add it to the list of VFS objects in your Samba configuration file (`smb.conf`). It is usually specified alongside other VFS modules.

### Example Configuration

```ini
[global]
   # Load the VFS modules for ACL support
   vfs objects = vfs_acl_tdb

[share]
   path = /srv/samba/share
   read only = no
   # Additional share settings...
```

- **vfs objects**:  
  Adding `vfs_acl_tdb` tells Samba to use this module for handling ACLs on the share.

## Use Cases

- **Filesystems Without xattr Support**:  
  On filesystems that do not support extended attributes, `vfs_acl_tdb` provides a method to enforce Windows ACLs.

- **Centralized ACL Management**:  
  Storing ACLs in a TDB file can simplify backups and migrations since the ACL information is maintained in a single, external file rather than being dispersed across file metadata.

- **Legacy Environments**:  
  It is useful for older systems or specific configurations where native xattr support is either not available or not desired.

## Advantages and Considerations

### Advantages

- **Portability**:  
  Since ACLs are stored externally in a TDB file, they can be backed up or transferred independently of the filesystem.
  
- **Flexibility**:  
  Provides a method to support Windows ACLs on filesystems that lack extended attribute support.

### Considerations

- **Performance**:  
  Storing ACLs in a TDB file may introduce a slight performance overhead compared to using native extended attributes.
  
- **TDB File Integrity**:  
  The integrity and backup of the TDB file are crucial; corruption of this file can lead to incorrect or lost ACL information.
  
- **Configuration Complexity**:  
  Ensure that the TDB file is properly secured and that its location is backed up as part of your overall Samba configuration management.

## Conclusion

The `vfs_acl_tdb` module is an effective alternative for managing Windows NT-style ACLs on Samba shares when native extended attribute support is unavailable or not desired. By storing ACLs in a dedicated TDB file, it ensures that Windows clients receive the correct permissions and that administrators have a flexible, centralized way to manage ACLs. Proper configuration and regular backups are essential to maintain the integrity and performance of this solution.
