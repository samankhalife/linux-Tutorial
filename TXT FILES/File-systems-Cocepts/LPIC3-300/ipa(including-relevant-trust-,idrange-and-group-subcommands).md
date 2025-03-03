# ipa

`ipa` is a command-line tool used to interact with the **FreeIPA** server, an integrated identity and authentication solution. FreeIPA includes multiple components like Kerberos, DNS, LDAP, and Certificate Authority, designed for managing users, groups, hosts, services, and other resources in an enterprise environment. 

The `ipa` command comes with several subcommands to manage **trusts**, **ID ranges**, and **groups**, among others. These commands are particularly useful for administrators who need to manage cross-realm trusts (e.g., Active Directory), configure ID ranges for user mappings, and handle group management in a centralized fashion.

## General `ipa` Command Syntax

The general structure of the `ipa` command is:

```bash
ipa [options] <command> [command-options] [arguments]
```

For example:

```bash
ipa group-add [OPTIONS] <group-name>
```

## Key Concepts

- **Trusts**: Enable users from trusted domains (e.g., Active Directory) to access services and resources in the FreeIPA domain.
- **ID Range**: A set of UIDs and GIDs used to map users and groups from external identity sources (like AD) to the local IPA environment.
- **Groups**: Used to manage users collectively in terms of permissions and access to resources.

### Trust Subcommands

Trusts allow FreeIPA to establish trust relationships with external identity providers like Active Directory. The relevant subcommands are:

1. **Add Trust**
   Adds a new trust relationship between FreeIPA and another domain, such as an Active Directory domain.

   ```bash
   ipa trust-add [OPTIONS] <domain>
   ```

   Common options:
   - **`--type`**: Type of the trust (e.g., `ad` for Active Directory).
   - **`--range`**: Specify the ID range for the trusted domain.
   - **`--admin`**: Username of the administrator on the remote domain.
   - **`--password`**: Password of the administrator (interactive).

   Example:

   ```bash
   ipa trust-add --type=ad --admin=administrator ad.example.com
   ```

2. **Show Trust**
   Displays details of a trust relationship.

   ```bash
   ipa trust-show <domain>
   ```

3. **Find Trust**
   Searches for trust relationships.

   ```bash
   ipa trust-find [OPTIONS] [criteria]
   ```

4. **Delete Trust**
   Removes a trust relationship.

   ```bash
   ipa trust-del <domain>
   ```

   Example:

   ```bash
   ipa trust-del ad.example.com
   ```

### ID Range Subcommands

ID ranges are important when integrating with external domains (like Active Directory) where users are mapped to FreeIPA’s UID and GID ranges.

1. **Add ID Range**
   Adds a new ID range.

   ```bash
   ipa idrange-add [OPTIONS] <id-range-name>
   ```

   Key options:
   - **`--base-id`**: Starting UID/GID for the range.
   - **`--range-size`**: Size of the range.
   - **`--rid-base`**: Starting RID for the range.
   - **`--dom-name`**: Domain name associated with the range.

   Example:

   ```bash
   ipa idrange-add --base-id=200000 --range-size=20000 --rid-base=1000 --dom-name=ad.example.com example-range
   ```

2. **Show ID Range**
   Displays details of an ID range.

   ```bash
   ipa idrange-show <id-range-name>
   ```

3. **Find ID Range**
   Searches for ID ranges.

   ```bash
   ipa idrange-find [OPTIONS] [criteria]
   ```

4. **Delete ID Range**
   Removes an ID range.

   ```bash
   ipa idrange-del <id-range-name>
   ```

   Example:

   ```bash
   ipa idrange-del example-range
   ```

### Group Subcommands

Groups in FreeIPA help organize users for access control and permission assignment.

1. **Add Group**
   Creates a new group.

   ```bash
   ipa group-add [OPTIONS] <group-name>
   ```

   Example:

   ```bash
   ipa group-add developers
   ```

2. **Add Members to Group**
   Adds users or other groups to an existing group.

   ```bash
   ipa group-add-member [OPTIONS] <group-name>
   ```

   Example:

   ```bash
   ipa group-add-member developers --users=johndoe
   ```

   You can also add multiple users or groups at once:

   ```bash
   ipa group-add-member developers --users=johndoe,janedoe --groups=admins
   ```

3. **Remove Members from Group**
   Removes users or groups from a group.

   ```bash
   ipa group-remove-member [OPTIONS] <group-name>
   ```

   Example:

   ```bash
   ipa group-remove-member developers --users=johndoe
   ```

4. **Show Group**
   Displays detailed information about a group.

   ```bash
   ipa group-show <group-name>
   ```

5. **Find Group**
   Searches for groups by criteria.

   ```bash
   ipa group-find [OPTIONS] [criteria]
   ```

6. **Delete Group**
   Deletes a group.

   ```bash
   ipa group-del <group-name>
   ```

   Example:

   ```bash
   ipa group-del developers
   ```

### Other Useful Subcommands

1. **User Subcommands**
   Manage users in the FreeIPA environment.

   - Add User: `ipa user-add`
   - Show User: `ipa user-show`
   - Delete User: `ipa user-del`

2. **Host Subcommands**
   Manage hosts in the FreeIPA environment.

   - Add Host: `ipa host-add`
   - Show Host: `ipa host-show`
   - Delete Host: `ipa host-del`

3. **Role Subcommands**
   Manage roles for RBAC (Role-Based Access Control).

   - Add Role: `ipa role-add`
   - Add Members to Role: `ipa role-add-member`
   - Remove Members from Role: `ipa role-remove-member`

## Example Scenario: Integrating FreeIPA with Active Directory

Let’s say you want to establish a trust relationship between FreeIPA and an Active Directory domain `ad.example.com`, and then assign specific users in Active Directory to a group within FreeIPA.

1. **Add Trust**

   ```bash
   ipa trust-add --type=ad --admin=administrator ad.example.com
   ```

2. **Create a Group in FreeIPA**

   ```bash
   ipa group-add external-users
   ```

3. **Map Active Directory Users to FreeIPA Group**

   ```bash
   ipa group-add-member external-users --external --users=ad_user1,ad_user2
   ```

In this example, we add a trust to Active Directory, create a group in FreeIPA, and map external users from AD to the newly created group.

## Conclusion

The `ipa` command with its various subcommands for managing **trusts**, **ID ranges**, and **groups** is essential for administrators working with FreeIPA in multi-domain or multi-realm environments, particularly when integrating with systems like Active Directory. These commands enable centralized and efficient management of users, groups, and identity mappings in enterprise setups.
