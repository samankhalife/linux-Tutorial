# targets.conf
**`targets.conf`** is the main configuration file for the **TGT iSCSI Target Framework** (TGT daemon `tgtd`), used to define iSCSI targets, LUNs (Logical Unit Numbers), and various settings such as access controls, authentication, and backend storage. This file plays a central role in setting up and managing iSCSI targets for the system.

The configuration file typically resides at `/etc/tgt/targets.conf` and contains directives that describe the iSCSI targets, along with details of LUNs and ACLs (Access Control Lists). The format of the configuration file is hierarchical and human-readable.

### Key Sections and Parameters in `targets.conf`:

1. **Global Options**:
   You can define global options for all targets here, such as defaults for authentication methods or other iSCSI target settings.
   ```bash
   default-driver iscsi
   ```
   This sets the default driver to `iscsi`.

2. **Target Definitions**:
   A target represents a storage device that clients (initiators) can access over the network. Each target is identified by a unique **IQN** (iSCSI Qualified Name).

   Example target definition:
   ```bash
   <target iqn.2025-03.com.example:storage.target1>
       backing-store /dev/sdb1
       initiator-address 192.168.1.100
       incominguser iscsi_user secret_pass
       outgoinguser user2 secret2
       write-cache off
   </target>
   ```

   - **iqn.2025-03.com.example:storage.target1**: The unique IQN for this target.
   - **backing-store**: Specifies the storage resource used by the target, which can be a block device like `/dev/sdb1`, a file, or a partition.
   - **initiator-address**: Specifies which initiator (client) is allowed to access the target, based on its IP address.
   - **incominguser**: Sets the username and password for authentication from the initiator to the target.
   - **outgoinguser**: Specifies the username and password for authentication when the target communicates with the initiator (for bidirectional authentication).
   - **write-cache**: Option to disable or enable the write cache for this target.

3. **LUN (Logical Unit Number) Assignments**:
   LUNs are logical representations of physical or virtual storage devices. They allow initiators to access specific partitions or devices. You can assign multiple LUNs to a single target.

   Example LUN definition within a target:
   ```bash
   <logicalunit 1>
       backing-store /dev/sdb1
   </logicalunit>
   ```

   In this example, **LUN 1** is mapped to the physical device `/dev/sdb1`. Multiple LUNs can be assigned to a single target, giving access to various storage volumes.

4. **Access Control Lists (ACLs)**:
   ACLs are used to restrict access to specific initiators. You can specify allowed initiator names (IQNs) or initiator IP addresses.

   Example:
   ```bash
   <target iqn.2025-03.com.example:storage.target2>
       backing-store /dev/sdc1
       initiator-address 192.168.1.101
       initiator-name iqn.2025-03.com.client:client1
   </target>
   ```

   - **initiator-address**: Specifies which IP address can access the target.
   - **initiator-name**: Restricts access to a specific iSCSI initiator with the matching IQN.

5. **Authentication**:
   TGT allows the configuration of **CHAP (Challenge-Handshake Authentication Protocol)** for secure access control.

   Example configuration:
   ```bash
   <target iqn.2025-03.com.example:securetarget>
       backing-store /dev/sdd1
       incominguser iscsi_user secret123
   </target>
   ```

   - **incominguser**: Defines the username and password (in clear text) that the initiator must provide to authenticate.

6. **Optional Parameters**:
   - **write-cache**: Controls whether write caching is enabled or disabled for the backing store.
   - **data-sha256**: For enabling data digest checksums to improve data integrity.

### Example of a Full `targets.conf` Configuration File:
```bash
default-driver iscsi

<target iqn.2025-03.com.example:storage.target1>
    backing-store /dev/sdb1
    initiator-address 192.168.1.100
    incominguser iscsi_user secret_pass
    outgoinguser user2 secret2
    write-cache off
</target>

<target iqn.2025-03.com.example:storage.target2>
    backing-store /dev/sdc1
    initiator-address 192.168.1.101
    initiator-name iqn.2025-03.com.client:client1
    incominguser iscsi_user2 anothersecret
</target>
```

### Key Notes:
- **IQN Format**: iSCSI Qualified Names (IQNs) follow the format `iqn.YYYY-MM.<domain>:name`, where `YYYY-MM` is the date the domain name was registered.
- **Initiator and Target**: The `initiator-address` and `initiator-name` options are important to control which clients can connect to specific iSCSI targets, providing a mechanism for both IP-based and IQN-based access control.

### Conclusion:
The **`targets.conf`** file is essential for configuring the iSCSI targets managed by the TGT daemon. It provides a highly flexible way to define and manage iSCSI targets, LUNs, access control lists, and security settings (such as CHAP). Through this configuration, you can set up centralized, network-based storage systems and securely manage access for remote clients (initiators).
