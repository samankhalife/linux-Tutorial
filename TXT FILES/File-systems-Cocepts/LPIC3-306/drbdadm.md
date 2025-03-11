# drbdadm

`drbdadm` is a command-line administration tool for managing DRBD (Distributed Replicated Block Device) resources. It was widely used with earlier versions of DRBD (such as DRBD8) to control replication, manage device states, and coordinate configuration settings as defined in `/etc/drbd.conf` and the `/etc/drbd.d/` directory. In more recent versions of DRBD (version 9 and later), `drbdsetup` has largely replaced `drbdadm` for many tasks, but `drbdadm` remains relevant for legacy systems.



## Purpose

- **Resource Management:**  
  `drbdadm` is used to bring DRBD devices up or down, promote them to primary status, or demote them to secondary. This is essential in managing which node is actively serving data and which is in standby for replication.

- **Configuration Coordination:**  
  It reads DRBD configurations from global and resource-specific files, ensuring that devices are initialized and managed according to defined parameters.

- **Operational Control:**  
  Provides commands to check the current status of DRBD devices, verify synchronization states, and adjust runtime parameters when necessary.



## Key Commands and Operations

`drbdadm` supports several key commands that operate on a given DRBD resource (typically identified by its resource name, as defined in your configuration):

- **up:**  
  Activates a DRBD resource, starting the replication process.
  
  ```bash
  drbdadm up <resource>
  ```
  
  *Example:*  
  ```bash
  drbdadm up r0
  ```

- **down:**  
  Deactivates a DRBD resource, stopping replication and detaching the DRBD device.
  
  ```bash
  drbdadm down <resource>
  ```
  
  *Example:*  
  ```bash
  drbdadm down r0
  ```

- **primary/secondary:**  
  Manages the role of a DRBD device.  
  - **primary:** Promotes the resource to primary, enabling read/write access.
    
    ```bash
    drbdadm primary <resource>
    ```
    
  - **secondary:** Demotes the resource to secondary.
    
    ```bash
    drbdadm secondary <resource>
    ```

- **status:**  
  Displays the current status of DRBD resources, including connection state, synchronization progress, and role (primary/secondary).
  
  ```bash
  drbdadm status <resource>
  ```
  
- **verify:**  
  Verifies the consistency and health of DRBD metadata or the replication status.
  
  ```bash
  drbdadm verify <resource>
  ```

Additional commands may exist for advanced operations or for interacting with DRBD metadata.



## Example Workflow

1. **Bring a Resource Online:**
   ```bash
   drbdadm up r0
   ```
   This command initializes the DRBD resource `r0` based on its configuration.

2. **Promote the Resource to Primary:**
   ```bash
   drbdadm primary r0
   ```
   With this command, the resource `r0` is promoted to primary status, allowing it to handle read/write operations.

3. **Check the Status of the Resource:**
   ```bash
   drbdadm status r0
   ```
   This command shows the current state of `r0`, including its role, connection state, and synchronization details.

4. **Take the Resource Down for Maintenance:**
   ```bash
   drbdadm down r0
   ```
   This stops the DRBD service for resource `r0` safely, which is useful during maintenance or configuration changes.



## Transition to drbdsetup

While `drbdadm` has been the traditional tool for DRBD management, in DRBD version 9 and newer, `drbdsetup` is now recommended for most administrative tasks. `drbdsetup` offers a modernized and unified interface that consolidates several functions, making it more straightforward to manage DRBD devices. However, understanding `drbdadm` remains important when working with legacy systems or when maintaining older configurations.



## Conclusion

`drbdadm` is a critical administration tool for managing DRBD resources in older DRBD implementations. It enables system administrators to control the lifecycle of DRBD devices through operations such as bringing devices up or down, promoting/demoting their roles, and checking their status. Although its functionality has been largely superseded by `drbdsetup` in modern DRBD versions, `drbdadm` continues to be an essential tool in environments that run legacy DRBD systems.
