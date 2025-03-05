# logon-path
The `logon-path` setting is used in the context of Windows user profiles in a domain environment, particularly when using Samba for integration with Active Directory or for managing a network of Windows clients. It specifies the network location (usually a shared folder) where a user's roaming profile is stored.

### **Roaming Profiles Overview**

A **roaming profile** allows a user's desktop settings, files, and preferences to be available no matter which machine they log in to within a domain. When the user logs in, the profile is copied from the network location to the local machine, and when the user logs off, the profile is synchronized back to the network location.

### **logon-path Syntax**
The `logon-path` directive is typically used in the Samba configuration file (`smb.conf`) to specify the path where user profiles will be stored.

```bash
logon path = \\<server>\<share>\%U\profile
```

- `\\<server>\<share>`: Network path to the server and shared folder where the profiles are stored.
- `%U`: Represents the username of the user logging in. This is a Samba variable that resolves to the actual username.

### **Example Configuration in smb.conf**

```bash
[global]
   workgroup = MYDOMAIN
   security = user
   logon path = \\server\profiles\%U\profile
   logon drive = H:
   logon home = \\server\%U
```

In this example:
- The **`logon path`** specifies that user profiles will be stored in a shared directory on `\\server\profiles` under a subdirectory for each user (`%U`).
- **`logon drive`** and **`logon home`** are additional settings that define the home directory for users, usually mapped to a network drive like `H:`.

### **Common Samba Variables in logon-path**

- **`%U`**: The username of the user logging in.
- **`%D`**: The domain name.
- **`%L`**: The server's NetBIOS name.
- **`%m`**: The client's NetBIOS name.

### **Usage in Active Directory and Samba**

If Samba is being used as a Primary Domain Controller (PDC) or integrated with Active Directory (AD), `logon-path` is important for managing Windows user profiles in a networked environment. If not configured properly, users may face issues like:
- Slow logons if profiles are large or network performance is poor.
- Profile corruption if there is a network interruption during logon or logoff.

### **Disabling Roaming Profiles**

If you don't want to use roaming profiles but want to ensure user settings are only local to the machine, you can disable the `logon path` setting:

```bash
logon path =
```

This effectively disables roaming profiles, causing users to use only local profiles.

### **Conclusion**

The `logon-path` directive is a crucial part of managing roaming profiles in a domain environment, allowing for centralized profile management in networked Windows clients. Proper configuration ensures that users' profiles are accessible and synchronized across machines, while misconfiguration can lead to slow logins or corrupted profiles.
