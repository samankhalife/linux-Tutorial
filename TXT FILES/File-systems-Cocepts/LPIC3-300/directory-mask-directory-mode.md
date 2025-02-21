# Directory Mask and Force Directory Mode

In Samba, controlling directory permissions is crucial for maintaining security and consistency across shared resources. Two key parameters used to manage the permissions on newly created directories are **`directory mask`** and **`force directory mode`**. Together, they determine the final permission bits applied to directories created on a share.

## Overview

- **directory mask**:  
  This parameter sets the maximum permissions that a newly created directory can have. It acts as a filter by performing a bitwise AND operation on the permissions requested by the client, ensuring that no permission bits beyond those allowed by the mask are set.

- **force directory mode**:  
  This parameter ensures that specific permission bits are always enabled on newly created directories. It works by performing a bitwise OR operation with the permissions determined after applying the directory mask, thereby enforcing a minimum set of permissions.

## Purpose

- **Consistent Security**:  
  By using these parameters, administrators can guarantee that all directories created on a share adhere to a predetermined security policy, regardless of client requests.
  
- **Simplified Management**:  
  Automating directory permission settings minimizes the need for manual adjustments and helps prevent inadvertent permission misconfigurations.
  
- **Enhanced Access Control**:  
  These settings ensure that new directories always have the required access rights for the intended users and groups, contributing to a secure and well-organized file sharing environment.

## How They Work

1. **directory mask**:  
   When a directory is created, the requested permissions are first filtered through the `directory mask`. This operation ensures that only the allowed permission bits can be set. For example, if the `directory mask` is set to `0770`, the resulting permissions will never exceed read, write, and execute for the owner and group, and no permissions for others.

2. **force directory mode**:  
   After applying the `directory mask`, Samba applies the `force directory mode` by performing a bitwise OR operation. This guarantees that certain permission bits are always set, regardless of the client’s request. For instance, if `force directory mode` is set to `0700`, every new directory will at least have read, write, and execute permissions for the owner.

## Configuration

Both parameters are set within the share definition in the Samba configuration file (`smb.conf`).

### Example Configuration

```ini
[shared]
   path = /srv/samba/shared
   writable = yes
   directory mask = 0770
   force directory mode = 0700
```

- **directory mask = 0770**:  
  Limits the maximum permissions to ensure that directories are created with, at most, full access for the owner and group, and no access for others.
  
- **force directory mode = 0700**:  
  Ensures that, at a minimum, directories have read, write, and execute permissions for the owner, regardless of client requests.

## Practical Examples

1. **Scenario: Secure Shared Directory for a Department**  
   Suppose you want a shared directory where any new subdirectory must be fully accessible (read, write, execute) by the owner but not accessible by others. You could configure:
   
   ```ini
   [department]
      path = /srv/samba/department
      writable = yes
      directory mask = 0770
      force directory mode = 0700
   ```
   This setup ensures that while group permissions can be set up to allow full access (as allowed by the directory mask), every new directory will at least grant the owner full access.

2. **Scenario: Collaborative Environment with Restricted Access for Others**  
   In a situation where you want group members to have full access and ensure that directories are not accessible by users outside the group, you might use:
   
   ```ini
   [collab]
      path = /srv/samba/collab
      writable = yes
      directory mask = 0770
      force directory mode = 0770
   ```
   Here, both the maximum and the forced minimum are set to `0770`, meaning every directory created will exactly have permissions `rwxrwx---`.

## Best Practices

- **Plan Your Permissions**:  
  Determine the minimal access required for directory creation and set `force directory mode` accordingly, then use `directory mask` to restrict any extra permissions that clients might request.

- **Test Configurations**:  
  Before applying changes broadly, test your settings on a small share to confirm that the resulting permissions align with your security policies.

- **Document Your Settings**:  
  Keep a record of your Samba configuration settings, including these parameters, to assist in troubleshooting and future audits.

## Conclusion

The combination of `directory mask` and `force directory mode` in Samba provides granular control over directory permissions on shared resources. By filtering client-requested permissions and enforcing a minimum set of access rights, these parameters help ensure a secure, consistent, and manageable environment for file sharing. Proper configuration of these settings is key to maintaining both functionality and security in a Samba deployment.
