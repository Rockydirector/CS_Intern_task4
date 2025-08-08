# Firewall Configuration with UFW on Linux

## Task Objective
Configure and test Uncomplicated Firewall (UFW) on Ubuntu to:
- Allow secure inbound SSH connections (port 22)
- Block insecure Telnet traffic (port 23)
- Document the process for audit and verification

---

## Basic Concepts

### What is a Firewall?
A firewall filters network traffic to protect systems from unauthorized access. UFW simplifies this process on Linux by managing iptables rules.

### Key Terms:
- **Inbound Rules**: Control incoming connections (e.g., SSH).

- **Outbound Rules**: Manage outgoing traffic (allowed by default in UFW).

- **Port-Based Filtering**: Rules apply to specific ports (e.g., port 22 for SSH).

### Why UFW?
- **Simplifies iptables**: UFW provides an easy interface for managing complex iptables rules.
- **Default Security**: Denies all incoming traffic by default, reducing attack surface.
- **Port-Based Filtering**: Controls access to services using port numbers.

---

## Steps Performed

### 1. Initial Setup
```bash
# Check initial firewall status
sudo ufw status

# Enable UFW
sudo ufw enable
```
### 2. Rule Configuration
```bash
# Allow SSH (port 22)
sudo ufw allow 22/tcp

# Block Telnet (port 23)
sudo ufw deny 23/tcp
# verification
sudo ufw status numbered
```
### 3. Testing
```bash
# Install Telnet client (for testing)
sudo apt install telnet

# Verify Telnet block
telnet localhost 23
```
## Sample Outputs

### UFW Status Before Configuration
[UFW Initial Status](screenshots/setup1.png) *Default inactive state before configuration*

### UFW Status After Configuration
[UFW Final Status](screenshots/setup2.png) *Showing allowed SSH (22/tcp) and blocked Telnet (23/tcp),Connection refused as expected*

## Configuration Files

### Firewall Rules Backup
[`📁 ufw_backup.rules`](configuration/ufw_backup.rules)  
Exported firewall configuration containing all active rules. Generated with `sudo ufw export`.

### Default Settings 
[`📁 ufw_default`](configuration/ufw_default)  
System-wide UFW configuration file controlling default policies and IPv6 settings.

## Expected Outcomes
| Test | Result |
|------|--------|
| SSH Connection | ✅ Success | 
| Telnet Connection | ❌ Blocked | 
| Configuration Persistence | ✔️ Maintained | 
## Security Best Practices
- **Default Deny Policy**: UFW defaults to blocking all incoming traffic

- **Service Hardening**: Telnet was blocked due to unencrypted communication

- **Selective Access**: Only SSH (port 22) was permitted for remote administration

- **Configuration Backups**: Rules were exported for documentation and recovery

## Conclusion
The UFW firewall was successfully configured to:
- 🔐 Permit encrypted SSH access (port 22)
- 🛡️ Block insecure Telnet traffic (port 23)
- ⚙️ Maintain secure defaults (`deny incoming, allow outgoing`)

Next Steps:
- Consider adding rate limiting: `sudo ufw limit 22/tcp`
- Review rules periodically: `sudo ufw status numbered`
