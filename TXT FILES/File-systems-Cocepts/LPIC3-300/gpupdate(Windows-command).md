# gpupdate

`gpupdate` is a Windows command-line utility used to refresh local and Active Directory-based Group Policy settings. It forces an update of both computer and user policy settings, allowing changes made by administrators to be applied immediately without waiting for the next scheduled policy refresh.

## Purpose

- **Immediate Policy Refresh**:  
  Apply new or modified Group Policy settings immediately on the local machine.
- **Troubleshooting**:  
  Useful for troubleshooting Group Policy issues by forcing an update and verifying that the correct policies are applied.
- **Selective Update**:  
  Allows you to refresh either computer or user policies, or both.

## Basic Syntax

```cmd
gpupdate [options]
```

## Common Options

- **`/force`**:  
  Reapplies all policies, even those that have not changed. This is useful when you want to ensure that all settings are refreshed.
  
  ```cmd
  gpupdate /force
  ```

- **`/target:{computer|user}`**:  
  Specifies whether to update the computer policy or the user policy only.
  
  - Update only computer policies:
    ```cmd
    gpupdate /target:computer
    ```
  - Update only user policies:
    ```cmd
    gpupdate /target:user
    ```

- **`/wait:<value>`**:  
  Specifies the amount of time (in seconds) to wait for policy processing to finish before returning control to the command prompt. The default value is 600 seconds. A value of 0 means that the command returns immediately.
  
  ```cmd
  gpupdate /wait:0
  ```

- **`/logoff`**:  
  In some cases, certain Group Policy settings (like those affecting user profiles) require the user to log off to take effect. This option logs off the user after the update is complete.
  
  ```cmd
  gpupdate /logoff
  ```

- **`/boot`**:  
  Forces a restart of the computer after the policy update. This is necessary if the policy change requires a reboot.
  
  ```cmd
  gpupdate /boot
  ```

## Examples

1. **Basic Policy Update**:
   ```cmd
   gpupdate
   ```
   This command updates both computer and user policies with the default wait time.

2. **Force Reapplication of All Policies**:
   ```cmd
   gpupdate /force
   ```
   Forces a full refresh, reapplying all Group Policy settings regardless of whether they have changed.

3. **Update Only Computer Policies with Immediate Return**:
   ```cmd
   gpupdate /target:computer /wait:0
   ```
   Refreshes only the computer policies and returns immediately without waiting.

4. **Update and Log Off User**:
   ```cmd
   gpupdate /logoff
   ```
   Applies the policies and logs off the user if necessary for the changes to take effect.

5. **Update and Force Reboot**:
   ```cmd
   gpupdate /boot
   ```
   Updates the policies and then forces a restart of the computer if required by the policy changes.


## Conclusion

The `gpupdate` command is a critical tool for Windows administrators and users alike, enabling immediate application of Group Policy changes. Whether you need to troubleshoot policy settings or enforce a complete refresh, `gpupdate` provides the necessary options to update policies efficiently and effectively.
