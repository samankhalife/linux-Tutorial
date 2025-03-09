# iscsiadm
**`iscsiadm`** is a command-line utility used to manage iSCSI connections on a Linux system. It is part of the Open-iSCSI package and is used to discover, log in to, log out of, and manage iSCSI sessions and targets. iSCSI (Internet Small Computer System Interface) is a protocol that allows SCSI commands to be sent over IP networks, enabling network-based storage.


### Common Usage Scenarios of `iscsiadm`:

1. **Discover iSCSI Targets**:
   You can discover available iSCSI targets on a remote iSCSI server using the **discovery** command. There are different types of discovery methods:
   - **sendtargets**: A discovery method where the initiator requests a list of available targets from the target.

   Example command:
   ```bash
   iscsiadm -m discovery -t sendtargets -p <target_ip>
   ```
   - `-m discovery`: Specifies the mode of the operation (discovery mode).
   - `-t sendtargets`: Uses the SendTargets method of discovery.
   - `-p <target_ip>`: Specifies the IP address of the iSCSI target server.

2. **Login to an iSCSI Target**:
   After discovering the available targets, you can log in to a specific target using the **login** command.

   Example command:
   ```bash
   iscsiadm -m node -T <target_iqn> -p <target_ip> --login
   ```
   - `-m node`: Specifies node management mode.
   - `-T <target_iqn>`: Specifies the target IQN (iSCSI Qualified Name) you want to log in to.
   - `-p <target_ip>`: The IP address of the iSCSI target.
   - `--login`: Initiates a session with the iSCSI target.

3. **Logout from an iSCSI Target**:
   To log out from a connected iSCSI target, use the **logout** command.

   Example command:
   ```bash
   iscsiadm -m node -T <target_iqn> --logout
   ```
   - `--logout`: Terminates the session with the specified target.

4. **List Active iSCSI Sessions**:
   To check the active iSCSI sessions, use the following command:

   ```bash
   iscsiadm -m session
   ```
   This will display information about the current iSCSI sessions, including target IQN, session ID, and the IP address of the target.

5. **Display Node Information**:
   To display detailed information about a specific iSCSI target (node):

   ```bash
   iscsiadm -m node -T <target_iqn> -p <target_ip>
   ```

6. **Remove iSCSI Target**:
   If you want to remove a discovered iSCSI target, use the following command:

   ```bash
   iscsiadm -m node -o delete -T <target_iqn> -p <target_ip>
   ```
   - `-o delete`: Deletes the specified iSCSI target configuration.

7. **Configure iSCSI Authentication**:
   You can set CHAP (Challenge-Handshake Authentication Protocol) authentication credentials for logging into a target.

   Example command:
   ```bash
   iscsiadm -m node -T <target_iqn> -p <target_ip> --op update -n node.session.auth.username -v <username>
   iscsiadm -m node -T <target_iqn> -p <target_ip> --op update -n node.session.auth.password -v <password>
   ```
   - `--op update`: Updates the specified authentication settings for the target.
   - `-n node.session.auth.username`: Specifies the CHAP username to be used during login.
   - `-n node.session.auth.password`: Specifies the CHAP password to be used during login.

8. **Rescan iSCSI Targets**:
   After logging in, you can rescan for new or updated LUNs (Logical Unit Numbers) from the connected iSCSI targets.

   ```bash
   iscsiadm -m node -R
   ```
   - `-R`: Rescans the active iSCSI sessions for new LUNs.

### Key `iscsiadm` Command Options:

- **-m**: Specifies the mode of operation (discovery, node, session, etc.).
- **-T**: Specifies the target IQN (iSCSI Qualified Name).
- **-p**: Specifies the target's IP address.
- **--login**: Logs in to the specified iSCSI target.
- **--logout**: Logs out from the specified iSCSI target.
- **-R**: Rescans the target for new LUNs.
- **-o delete**: Removes the target from the configuration.
- **-n**: Specifies the node/session option to configure, such as CHAP username or password.
- **-v**: Specifies the value for the option being updated (e.g., username or password).

### iSCSI Configuration Files:

- **`/etc/iscsi/initiatorname.iscsi`**: Contains the initiator name (IQN) for the system.
- **`/etc/iscsi/iscsid.conf`**: The configuration file for the iSCSI daemon (`iscsid`). It includes settings for authentication, timeouts, and logging.

### Conclusion:
`iscsiadm` is a powerful and versatile tool for managing iSCSI targets and sessions on Linux systems. It allows administrators to easily discover, connect to, manage, and disconnect from iSCSI storage targets over a network. The flexibility of `iscsiadm` to manage authentication, perform rescans for new LUNs, and control iSCSI sessions makes it an essential tool for handling network-attached storage in Linux environments.
