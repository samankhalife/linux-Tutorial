# map-acl-inherit

The `map-acl-inherit` parameter in Samba is used to control how Windows NT ACL inheritance is translated into the underlying Unix filesystem permissions. This setting affects the behavior of ACL inheritance on files and directories when they are created or modified through Samba, ensuring that inherited permissions from parent objects are correctly applied in a manner that is compatible with Unix permissions.

## Purpose

- **Windows-to-Unix ACL Translation**:  
  When Windows clients create or modify files on a Samba share, they may specify inheritance flags in their ACLs. The `map-acl-inherit` option determines whether these inherited ACL entries are mapped into the standard Unix permission model.

- **Consistent Permission Management**:  
  By enabling this parameter, administrators can achieve more consistent permission inheritance across platforms, ensuring that new files and directories receive appropriate permissions based on their parent objects.

## Configuration

`map-acl-inherit` is typically set in the Samba configuration file (`smb.conf`), either globally under the `[global]` section or per-share if specific behavior is needed for a given share.

### Example

To enable ACL inheritance mapping, add the following line to your `smb.conf`:

```ini
[global]
   map acl inherit = yes
```

- **`yes`**: Inherited ACL entries from Windows are mapped into Unix permissions.
- **`no`**: Inheritance is not mapped, and Samba may rely solely on explicit Unix permission settings.

## How It Works

- **Inheritance Mapping**:  
  When a new file or directory is created, Samba checks for any inheritance flags set on the parent directory. If `map-acl-inherit` is enabled, Samba attempts to map these inherited ACL entries into the file's or directory's permission bits (and possibly into extended ACLs if supported by the filesystem).

- **Compatibility**:  
  This mapping is crucial in mixed-OS environments where Windows and Unix systems share files. It helps ensure that permission changes made on Windows systems are respected on Unix systems and vice versa.

## Use Cases

- **Mixed Environment Deployments**:  
  In networks where both Windows and Unix systems coexist, enabling `map-acl-inherit` ensures that files and directories maintain consistent inherited permissions, reducing administrative overhead and potential access issues.

- **Enhanced Security Control**:  
  By correctly mapping inherited ACLs, administrators can enforce security policies that mimic the behavior of Windows ACL inheritance, providing more granular control over file and directory access.

## Considerations

- **Filesystem Support**:  
  Ensure that the underlying filesystem supports the required extended attributes (xattrs) if you intend to use advanced ACL features. Filesystems like ext4, XFS, or Btrfs generally provide good support.

- **Testing**:  
  Before deploying `map-acl-inherit` in a production environment, test the configuration on a small set of shares to verify that the ACL inheritance behaves as expected.

- **Interaction with Other VFS Modules**:  
  If you are using other VFS modules for ACL handling (such as `vfs_acl_xattr` or `vfs_acl_tdb`), make sure that their settings are compatible with `map-acl-inherit` to avoid conflicts or unexpected permission results.

## Conclusion

The `map-acl-inherit` parameter is an important option in Samba for translating Windows ACL inheritance into the Unix permission model. When enabled, it helps maintain consistent and secure access control on Samba shares in mixed operating system environments. Proper configuration and testing of this parameter, along with compatible VFS ACL modules, ensure that file and directory permissions are correctly inherited and enforced across the network.

