# force-create-mode

`force-create-mode` is a Samba configuration parameter that forces specific permission bits to be set on newly created files on a share. It ensures that regardless of the permissions requested by the client, new files will always have certain minimum permission bits enabled. This is useful for enforcing a baseline security policy on files stored on a Samba share.

## Purpose

- **Enforce Baseline Security**:  
  Guarantees that all newly created files have a predefined set of permission bits, protecting them from being created with overly permissive settings.
  
- **Consistent Permissions**:  
  Helps maintain a uniform permission policy across all files on the share, regardless of client-side requests.

## How It Works

When a file is created on a Samba share:
1. The client's requested permissions are first filtered by the `create mask`.
2. Samba then applies the `force create mode` settings using a bitwise OR operation, ensuring that the specified bits are always set.
   
For example, if you set:
- `create mask = 0660`
- `force create mode = 0640`

This means that even if a client requests different permissions, the resulting file will always have at least read/write permissions for the owner and read permission for the group, within the limits of the `create mask`.

## Configuration

You set `force create mode` in the share definition within your `smb.conf` file.

### Example

```ini
[shared]
   path = /srv/samba/shared
   writable = yes
   create mask = 0660
   force create mode = 0640
```

- **create mask = 0660**: Limits the maximum permissions to read/write for the owner and group.
- **force create mode = 0640**: Ensures that every new file has at least read/write for the owner and read for the group.

## Use Cases

- **Security Enforcement**:  
  Ensures that all files have a minimum level of protection, preventing unauthorized access.
  
- **Simplified Administration**:  
  Automates permission management, reducing the need for manual corrections after file creation.
  
- **Mixed Environment Consistency**:  
  Helps maintain uniform permissions when files are created by users on different client systems.

## Considerations

- **Interplay with create mask**:  
  `create mask` sets an upper limit for permissions, while `force create mode` ensures that certain bits are always present. Both should be configured in tandem to achieve the desired permission set.
  
- **Testing**:  
  Always test these settings on a small share before rolling them out to production, to confirm that the final permissions meet your security requirements.

## Conclusion

The `force-create-mode` parameter in Samba is an effective way to enforce a baseline set of permissions on newly created files within a share. By guaranteeing that specific permission bits are always set, it helps maintain consistent security policies across your file system, ensuring that files are protected according to your organizational standards.
