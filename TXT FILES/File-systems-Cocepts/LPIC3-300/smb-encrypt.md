# smb-encrypt

**`smb-encrypt`** is a Samba configuration parameter that controls the encryption of SMB (Server Message Block) traffic between a Samba server and its clients. Enabling SMB encryption helps protect sensitive data during transit, ensuring that communications are secure even over untrusted networks.

## Overview

- **Purpose**:  
  To encrypt data transmitted between the Samba server and its clients, protecting it from eavesdropping and interception.

- **Configuration Level**:  
  This setting can be applied globally in the `[global]` section of `smb.conf` or on a per-share basis within individual share definitions.

- **Encryption Modes**:  
  Common values for `smb encrypt` include:
  - **desired**:  
    Encrypt the connection if the client supports it; however, non-encrypted connections are still allowed.
  - **required**:  
    Enforce encryption for all connections; non-encrypted clients will be denied access.
  - **enabled**:  
    Force encryption on all connections without negotiation.
  - **off**:  
    Disable SMB encryption.

## Configuration Examples

### Global Configuration

To require encryption for all SMB traffic on the server, add the following line in your `[global]` section of `smb.conf`:

```ini
[global]
   smb encrypt = required
```

### Per-Share Configuration

You can also enforce encryption on specific shares. For example, to require encryption for a share named `secure_share`:

```ini
[secure_share]
   path = /srv/samba/secure
   read only = no
   smb encrypt = required
```

In this configuration, any client accessing `secure_share` must use an encrypted connection.

## Use Cases

- **Sensitive Data Transfer**:  
  Enforce encryption on shares containing confidential or sensitive data to protect it from interception.

- **Remote Access Over Untrusted Networks**:  
  When clients connect from outside a secure corporate network (e.g., over the Internet), encryption ensures data privacy.

- **Regulatory Compliance**:  
  Meet compliance requirements (such as HIPAA, PCI-DSS, or GDPR) that mandate encrypted data transmission.

## Considerations

- **Performance Impact**:  
  Encrypted connections may incur a performance overhead. Test the configuration to ensure that it meets your performance requirements.

- **Client Compatibility**:  
  Ensure that client systems support SMB encryption. Most modern Windows and Unix clients do, but older systems may not.

- **Balanced Security**:  
  Choose the appropriate mode based on your environment. Use `desired` in less-critical environments where performance is a priority, and `required` or `enabled` where security is paramount.

## Conclusion

The `smb-encrypt` parameter is essential for securing SMB communications in a Samba environment. By configuring it either globally or on a per-share basis, administrators can protect data in transit, ensure compliance with security policies, and provide a secure network experience for all users.
