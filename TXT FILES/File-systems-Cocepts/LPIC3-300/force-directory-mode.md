# force-directory-mode

`force-directory-mode` is a Samba configuration parameter that forces new directories created on a share to have specific permission bits. It works by ensuring that, regardless of the permissions requested by the client, the new directories will include the bits specified by `force-directory-mode`.

## Purpose

- **Enforce Consistent Permissions**:  
  Ensures that all directories created on the share have a consistent permission set, which is critical for security and proper access control.
  
- **Enhance Security**:  
  Prevents files or directories from being created with overly permissive settings that might allow unauthorized access.
  
- **Simplify Administration**:  
  Automates the assignment of directory permissions, reducing the need for manual adjustments after creation.

## How It Works

When a directory is created on a Samba share, Samba uses a combination of parameters to determine its final permissions. `force-directory-mode` is applied using a bitwise OR operation with the permissions requested by the client. This guarantees that the resulting permission bits include those specified in `force-directory-mode`.

## Configuration

`force-directory-mode` is configured in the share definition within the `smb.conf` file. It is often used alongside `directory mask` and `force create mode` for files to ensure both files and directories have the intended security settings.

### Example Configuration

```ini
[shared]
   path = /srv/samba/shared
   writable = yes
   directory mask = 0770
   force-directory-mode = 0770
```

In this example:
- **`directory mask = 0770`** sets the maximum allowed permissions for directories.
- **`force-directory-mode = 0770`** guarantees that every directory created on the share will have at least the permissions `rwxrwx---`, ensuring that both the owner and the group have full access, while others have no access.

## Use Cases

- **Collaborative Environments**:  
  In workgroups or departments where multiple users need to access shared directories, enforcing a consistent directory permission model prevents accidental exposure of sensitive data.
  
- **Security Policies**:  
  Organizations with strict security requirements can ensure that all directories adhere to defined access controls, minimizing the risk of unauthorized access.

- **Automated File Management**:  
  When directories are created automatically (e.g., by scripts or applications), `force-directory-mode` ensures they conform to the organization's permission policies.

## Considerations

- **Interaction with Other Permissions Settings**:  
  Be sure to configure `directory mask` and `force-directory-mode` in harmony so that the final permissions meet your security requirements.
  
- **Testing**:  
  Test the configuration on a non-critical share first to verify that the expected permissions are applied to newly created directories.

## Conclusion

`force-directory-mode` is a powerful Samba parameter that ensures newly created directories on a share have a predefined set of permission bits. This feature is essential for maintaining consistent security settings and simplifying administration in environments where precise control over directory access is necessary.

