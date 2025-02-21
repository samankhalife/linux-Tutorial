# profile-acls

`profile-acls` is a Samba configuration parameter used primarily in the `[profiles]` share to control how NT-style Access Control Lists (ACLs) are applied to roaming profiles. When enabled, it ensures that the ACLs associated with user profiles are preserved and enforced in a way that mirrors Windows behavior, providing a consistent security experience in Active Directory environments.

## Purpose

- **Roaming Profile Management**:  
  Ensures that user profile data stored on a Samba server retains its Windows ACL settings, so that access permissions are consistent with what is expected in a Windows environment.

- **Consistent Permission Enforcement**:  
  Helps maintain the integrity of security descriptors for profiles by applying inherited and explicit ACLs from the parent directory to newly created profile files and directories.

## How It Works

- **ACL Preservation**:  
  When a user accesses their roaming profile, the `profile-acls` setting causes Samba to apply the ACLs stored with the profile. This means that if a parent directory has specific ACLs, new files and subdirectories within a user’s profile will inherit those ACLs automatically.

- **Integration with VFS ACL Modules**:  
  This parameter typically works in conjunction with other Samba VFS modules that manage ACLs (e.g., `vfs_acl_xattr` or `vfs_acl_tdb`). These modules handle the storage and retrieval of ACL information—either in extended attributes or in a TDB file—so that Windows ACLs are properly maintained on Unix filesystems.

## Configuration

To enable `profile-acls`, add it to your `[profiles]` share definition in the `smb.conf` file. For example:

```ini
[profiles]
   path = /srv/samba/profiles
   read only = no
   browseable = no
   # Enable the use of Windows-style ACLs for roaming profiles
   profile acls = yes
```

- **`profile acls = yes`**:  
  Activates the feature so that the ACLs for user profiles are preserved and enforced.
  
- **`profile acls = no`**:  
  Disables the feature, meaning that Samba may apply default or inherited permissions instead.

## Use Cases

- **Active Directory Roaming Profiles**:  
  In AD environments, users' roaming profiles stored on a Samba server will retain their ACLs as set in Windows, ensuring a consistent security experience across platforms.

- **Security Consistency**:  
  For organizations that require strict control over user profile data, enabling `profile-acls` ensures that access permissions are uniformly enforced, minimizing the risk of unauthorized access.

- **Administrative Efficiency**:  
  Automatically applying ACLs based on parent directories reduces the need for manual intervention, simplifying the management of large numbers of roaming profiles.

## Considerations

- **Filesystem Support**:  
  Ensure that the underlying filesystem supports extended attributes if you are using modules like `vfs_acl_xattr`, as this is necessary for storing detailed ACL information.

- **Interaction with Other Modules**:  
  When using `profile-acls`, verify that it integrates correctly with other ACL-related VFS modules to prevent conflicts or unexpected permission results.

- **Performance Impact**:  
  Managing ACLs may add a slight performance overhead; it is recommended to test the configuration in your environment before deploying it widely.

## Conclusion

The `profile-acls` parameter in Samba is an essential setting for environments using roaming profiles, particularly in Windows Active Directory contexts. By enabling this feature, administrators ensure that NT-style ACLs are properly inherited and enforced for user profile data, leading to a consistent and secure user experience across mixed-OS networks.
