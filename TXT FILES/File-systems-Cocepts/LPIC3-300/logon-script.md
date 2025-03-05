# logon-script
The `logon-script` directive is used in Samba to specify a client-side script that runs automatically when a user logs on to a Windows system. This script is typically used to set up user-specific configurations, such as mapping network drives, setting environment variables, or performing other initializations that help configure the user's session.

### **Purpose**

- **Automate Session Setup**:  
  The logon script can perform tasks like drive mappings, printer setups, or executing custom commands to prepare the user’s environment.
  
- **Centralized Management**:  
  By defining a logon script on the server, administrators can ensure that every user receives consistent settings and configurations when they log on, regardless of which machine they use.

- **Enhance User Experience**:  
  The logon script can also help in automating tasks that otherwise would need to be performed manually by the user, thus streamlining the login process.

### **Configuration Syntax**

The `logon-script` directive is defined in the Samba configuration file (`smb.conf`) under the `[global]` section. The syntax is:

```bash
logon script = <script_name>
```

- **`<script_name>`**: The name of the script file that is stored in the share designated for logon scripts, typically the `netlogon` share.

---

### **Example Configuration**

In the `smb.conf` file, you might see a configuration like:

```ini
[global]
   workgroup = MYDOMAIN
   security = user
   domain logons = yes
   logon script = logon.bat

[netlogon]
   path = /var/lib/samba/sysvol/mydomain.local/scripts
   read only = yes
```

**Explanation:**

- **`domain logons = yes`**:  
  This directive enables domain logon functionality, which tells the Samba server to serve logon scripts to Windows clients.

- **`logon script = logon.bat`**:  
  Specifies that the script named `logon.bat` should be executed when a user logs on.

- **`[netlogon]` Share**:  
  The `[netlogon]` share points to the directory where logon scripts are stored. Windows clients automatically look in this share to retrieve the specified script.

### **How It Works**

1. **User Login**:  
   When a user logs into a Windows domain joined to the Samba server, the client looks for a logon script in the `netlogon` share.

2. **Script Execution**:  
   The specified script (e.g., `logon.bat`) is downloaded and executed on the client machine, performing the preconfigured tasks such as mapping network drives or setting up environment variables.

3. **Centralized Control**:  
   Since the logon script is centrally managed on the server, any changes to it will be applied to all users at the next logon, ensuring consistency across the network.

---

### **Best Practices**

- **Script Location**:  
  Ensure that the logon script is stored in the correct directory (usually within the `netlogon` share) and that it has the proper permissions so that it can be read by all domain users.

- **Testing**:  
  Test the logon script on a single client before deploying it network-wide to ensure that it performs the intended tasks without errors.

- **Keep It Simple**:  
  Complex scripts can delay the logon process. Aim for efficiency and simplicity in your script to minimize login delays.

- **Error Handling**:  
  Include error handling in your script to manage potential issues gracefully, preventing incomplete configurations or user frustration.

---

### **Troubleshooting**

- **Script Not Running**:  
  Verify that `domain logons` is enabled in `smb.conf`, and that the script is placed in the correct `netlogon` directory with the proper permissions.

- **Client Errors**:  
  Check the Windows Event Viewer on the client side for errors related to logon scripts. Also, review Samba logs on the server for any access or permission issues.

- **Network Issues**:  
  Ensure that network connectivity between the client and the Samba server is reliable, as any interruptions can prevent the logon script from being downloaded or executed.

### **Conclusion**

The `logon-script` directive in Samba is a powerful tool for automating and centralizing the configuration of Windows client sessions in a domain environment. By properly configuring and managing your logon scripts, you can streamline user logins, enforce consistent environment settings, and enhance overall productivity across the network.
