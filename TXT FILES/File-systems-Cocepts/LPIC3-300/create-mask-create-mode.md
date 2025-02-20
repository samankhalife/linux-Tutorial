# create-mask and create-mode

In Samba, the `create mask` and `force create mode` parameters are used to control the file permissions applied to new files created on a share. These settings ensure that files are created with the proper security settings, regardless of the permissions requested by the client.

## create mask

- **Purpose**:  
  The `create mask` parameter defines which permission bits _may_ be set on a newly created file. It acts as a filter, ensuring that no extra permission bits are applied beyond what is allowed by the mask.

- **How It Works**:  
  When a file is created, Samba performs a bitwise AND between the permissions requested by the client and the value specified in `create mask`.

- **Example**:
  ```ini
  [share]
     path = /srv/samba/share
     create mask = 0644
  ```
  In this example, regardless of the client’s requested permissions, new files will have permissions limited to 0644 (owner read/write, group read, others read).

## force create mode

- **Purpose**:  
  The `force create mode` parameter specifies permission bits that will _always_ be set on newly created files. This means that these bits are enforced even if the client requests more restrictive permissions.

- **How It Works**:  
  Samba performs a bitwise OR between the client's requested permissions and the value specified in `force create mode`, ensuring that the defined bits are present.

- **Example**:
  ```ini
  [share]
     path = /srv/samba/share
     force create mode = 0644
  ```
  Here, Samba guarantees that at minimum, the file will have the permissions 0644.

## Using Both Together

Often, administrators use both parameters to tightly control the resulting permissions of new files. For example:

```ini
[share]
   path = /srv/samba/share
   create mask = 0660
   force create mode = 0640
```

- **create mask = 0660**:  
  Limits the permissions so that files cannot have more than read/write access for the owner and group (no permissions for others).

- **force create mode = 0640**:  
  Ensures that every file will at least have read/write for the owner and read for the group, regardless of what the client requested.

The final permissions on a new file are determined by:
1. Taking the client's requested permissions.
2. Applying the `create mask` (bitwise AND) to remove any bits that aren’t allowed.
3. Then applying the `force create mode` (bitwise OR) to ensure specific bits are set.

## Best Practices

- **Security**:  
  Choose values that minimize exposure. For sensitive data, ensure that files are not inadvertently made world-accessible.

- **Consistency**:  
  Align the Samba permission settings with your organization's security policies and the underlying filesystem permissions.

- **Testing**:  
  Test your configuration on a small share before deploying it network-wide to ensure the resulting permissions meet your expectations.

## Conclusion

By using `create mask` and `force create mode`, Samba administrators can precisely control the file permissions for new files created on shares. This mechanism helps maintain security and consistency, ensuring that files are not created with overly permissive settings while enforcing a baseline level of access control.
