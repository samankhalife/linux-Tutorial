# tgtadm
**`tgtadm`** is a command-line utility used to administer and manage iSCSI targets for the **TGT** iSCSI target framework, which is commonly used to set up and control **iSCSI storage** devices in Linux environments. **iSCSI** (Internet Small Computer Systems Interface) is a protocol that allows SCSI commands to be sent over IP networks, enabling the use of remote storage devices as though they were locally attached.

The **`tgtadm`** tool interacts with the **TGT** daemon (`tgtd`) to manage iSCSI targets, including creating, modifying, and removing targets, logical units (LUNs), and access control lists (ACLs).

### Key Concepts:
- **iSCSI Target**: A storage resource located on a server that can be accessed over a network by an iSCSI initiator (the client).
- **LUN (Logical Unit Number)**: A logical reference to a portion of a storage device or a whole storage device.
- **TGT Daemon**: The background process (`tgtd`) that manages the targets and handles the iSCSI protocol.


### Usage of `tgtadm`:

Here are common operations using **`tgtadm`** to manage iSCSI targets.

#### 1. **List existing targets**:
   ```bash
   tgtadm --mode target --op show
   ```
   This will list all the currently configured targets and their parameters.

#### 2. **Create a new target**:
   ```bash
   tgtadm --lld iscsi --mode target --op new --tid <target-id> --targetname <iqn>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode target --op new --tid 1 --targetname iqn.2025-03.com.example:storage.target1
   ```
   This creates a new target with the target ID (`tid`) of 1 and a unique iSCSI Qualified Name (IQN).

#### 3. **Bind the target to a network interface**:
   ```bash
   tgtadm --lld iscsi --mode target --op bind --tid <target-id> --initiator-address <IP>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode target --op bind --tid 1 --initiator-address 192.168.1.100
   ```
   This binds the target to a specific network interface so that only clients from the specified IP can access it.

#### 4. **Add a LUN to a target**:
   ```bash
   tgtadm --lld iscsi --mode logicalunit --op new --tid <target-id> --lun <lun-id> --backing-store /path/to/storage
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode logicalunit --op new --tid 1 --lun 1 --backing-store /dev/sdb1
   ```
   This creates a new LUN (with ID 1) that points to the block device `/dev/sdb1` for the target with ID 1.

#### 5. **Set access control (ACL)**:
   ```bash
   tgtadm --lld iscsi --mode target --op bind --tid <target-id> --initiator-name <initiator-iqn>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode target --op bind --tid 1 --initiator-name iqn.2025-03.com.client:client1
   ```
   This binds the iSCSI target to a specific initiator, identified by its IQN, ensuring that only this initiator can connect.

#### 6. **Delete a target**:
   ```bash
   tgtadm --lld iscsi --mode target --op delete --tid <target-id>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode target --op delete --tid 1
   ```
   This will remove the target with the specified ID (in this case, target 1).

#### 7. **Remove a LUN from a target**:
   ```bash
   tgtadm --lld iscsi --mode logicalunit --op delete --tid <target-id> --lun <lun-id>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode logicalunit --op delete --tid 1 --lun 1
   ```
   This will delete the logical unit (LUN) with ID 1 from target 1.

#### 8. **Modify target settings (e.g., authentication)**:
   ```bash
   tgtadm --lld iscsi --mode account --op new --user <username> --password <password>
   ```
   Example:
   ```bash
   tgtadm --lld iscsi --mode account --op new --user iscsi_user --password secret_pass
   ```
   This sets up authentication credentials for the iSCSI target, ensuring that clients need to authenticate using this username and password.

#### 9. **Show LUN information**:
   ```bash
   tgtadm --lld iscsi --mode logicalunit --op show --tid <target-id>
   ```
   This shows the status and configuration of all logical units (LUNs) associated with a specific target.

### Conclusion:
**`tgtadm`** is a powerful tool for managing iSCSI targets and logical units on Linux servers. It is essential for environments where centralized storage is required over an IP network, providing flexible control over iSCSI-based storage systems. With `tgtadm`, administrators can manage targets, allocate storage, set up access control, and configure various iSCSI parameters to ensure robust and efficient storage solutions.
