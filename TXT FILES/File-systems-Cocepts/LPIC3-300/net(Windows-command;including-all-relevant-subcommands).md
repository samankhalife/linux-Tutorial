# net

The `net` command is a versatile Windows command-line utility used for managing and configuring various network resources and services. It provides a wide range of subcommands that allow administrators and power users to perform tasks such as managing user accounts, network shares, services, sessions, and more.

## Key Subcommands

### 1. **net use**
Used to connect, disconnect, and manage network drives or printers.

- **Purpose**:  
  Map a network share to a local drive letter, view existing connections, or disconnect them.
  
- **Examples**:
  - **Map a drive:**
    ```cmd
    net use Z: \\Server\Share
    ```
  - **Connect with credentials:**
    ```cmd
    net use Z: \\Server\Share /user:DOMAIN\username password
    ```
  - **List active connections:**
    ```cmd
    net use
    ```
  - **Disconnect a mapped drive:**
    ```cmd
    net use Z: /delete
    ```

### 2. **net user**
Manages user accounts on the local machine or domain.

- **Purpose**:  
  Create, modify, and delete user accounts.
  
- **Examples**:
  - **Display user information:**
    ```cmd
    net user username
    ```
  - **Create a new user:**
    ```cmd
    net user newuser password /add
    ```
  - **Delete a user:**
    ```cmd
    net user username /delete
    ```
  - **Change a user password:**
    ```cmd
    net user username newpassword
    ```



### 3. **net group**
Manages global groups on a domain (if executed in a domain context).

- **Purpose**:  
  Create, modify, and display domain groups.
  
- **Examples**:
  - **List group members:**
    ```cmd
    net group GroupName
    ```
  - **Add a user to a group:**
    ```cmd
    net group GroupName username /add
    ```
  - **Remove a user from a group:**
    ```cmd
    net group GroupName username /delete
    ```

### 4. **net localgroup**
Manages local groups on a computer.

- **Purpose**:  
  Create, modify, and display local groups.
  
- **Examples**:
  - **List local group members:**
    ```cmd
    net localgroup GroupName
    ```
  - **Add a user to a local group:**
    ```cmd
    net localgroup GroupName username /add
    ```
  - **Remove a user from a local group:**
    ```cmd
    net localgroup GroupName username /delete
    ```

### 5. **net share**
Manages shared resources on a computer.

- **Purpose**:  
  Create, delete, and display network shares.
  
- **Examples**:
  - **List shares:**
    ```cmd
    net share
    ```
  - **Create a share:**
    ```cmd
    net share ShareName=C:\Path\To\Folder /grant:username,full
    ```
  - **Delete a share:**
    ```cmd
    net share ShareName /delete
    ```

### 6. **net start / net stop**
Starts or stops Windows services.

- **Purpose**:  
  Control the running state of services.
  
- **Examples**:
  - **List running services:**
    ```cmd
    net start
    ```
  - **Start a service:**
    ```cmd
    net start ServiceName
    ```
  - **Stop a service:**
    ```cmd
    net stop ServiceName
    ```

### 7. **net session**
Manages sessions between the local computer and others on the network.

- **Purpose**:  
  Display or disconnect sessions with other computers.
  
- **Examples**:
  - **List active sessions:**
    ```cmd
    net session
    ```
  - **Disconnect a session:**
    ```cmd
    net session \\ComputerName /delete
    ```



### 8. **net file**
Manages shared files that are open on a server.

- **Purpose**:  
  List open files and disconnect files that are being used.
  
- **Examples**:
  - **Display open files:**
    ```cmd
    net file
    ```
  - **Close an open file by its ID:**
    ```cmd
    net file <ID> /close
    ```



### 9. **net time**
Synchronizes the computer's clock with a time server.

- **Purpose**:  
  Query and set the system time.
  
- **Examples**:
  - **Display the current time from a server:**
    ```cmd
    net time \\TimeServer
    ```
  - **Synchronize the system clock with a server:**
    ```cmd
    net time \\TimeServer /set /yes
    ```

### 10. **net statistics**
Displays network statistics, including server and workstation statistics.

- **Purpose**:  
  Provide diagnostic information about network performance.
  
- **Examples**:
  - **Show workstation statistics:**
    ```cmd
    net statistics workstation
    ```
  - **Show server statistics:**
    ```cmd
    net statistics server
    ```

### 11. **net accounts**
Manages password and logon requirements for user accounts.

- **Purpose**:  
  Set policies related to passwords, lockout thresholds, and logon hours.
  
- **Examples**:
  - **Display current account policies:**
    ```cmd
    net accounts
    ```
  - **Set minimum password length:**
    ```cmd
    net accounts /minpwlen:8
    ```
  
### 12. **net config**
Configures server and workstation settings.

- **Purpose**:  
  Display or modify configuration settings for network services.
  
- **Examples**:
  - **Display server configuration:**
    ```cmd
    net config server
    ```
  - **Display workstation configuration:**
    ```cmd
    net config workstation
    ```
  
## Conclusion

The `net` command is a powerful tool that enables administrators and users to manage various network tasks directly from the Windows command line. Whether you need to manage user accounts, configure network shares, control services, or handle network sessions, the numerous subcommands of `net` provide a comprehensive set of functionalities essential for everyday network administration. Each subcommand addresses a specific area of network management, making `net` a central command for troubleshooting and configuring Windows network resources.
