# Born2beRoot

![42 Badge](https://img.shields.io/badge/42-Born2beRoot-brightgreen)
![System Administration Badge](https://img.shields.io/badge/Type-System%20Administration-red)
![Status Badge](https://img.shields.io/badge/Status-Completed-success)

## What I Learned

Through this comprehensive system administration project at 42 School, I developed essential DevOps and infrastructure skills:

- **Virtualization technologies** - Gained hands-on experience with VirtualBox/UTM and virtual machine management
- **Linux system administration** - Mastered user management, permissions, and system configuration
- **Security hardening** - Implemented strong password policies, sudo restrictions, and firewall configurations
- **Network security** - Configured SSH services, port management, and firewall rules (UFW/firewalld)
- **Disk management** - Created encrypted partitions using LVM and understood storage optimization
- **Process monitoring** - Built system monitoring scripts and automated reporting systems
- **Service configuration** - Set up and managed system services, daemons, and scheduled tasks
- **Shell scripting** - Developed bash scripts for system monitoring and automation
- **Package management** - Learned differences between package managers (apt vs aptitude)
- **Security frameworks** - Configured AppArmor/SELinux for enhanced system security

This project reinforced my understanding of Linux internals, security best practices, and system administration fundamentals essential for any infrastructure role.

## About the Project

Born2beRoot is a system administration project focused on creating a secure, well-configured virtual server. The project emphasizes security, monitoring, and proper system setup following industry best practices for:

- Secure server configuration
- User and permission management
- System monitoring and logging
- Network security implementation
- Automated system reporting
- Service management and deployment

## Implementation Details

The project consists of mandatory requirements and bonus features across multiple system administration domains:

### Core System Setup

**Operating System & Virtualization:**
- Debian (latest stable) or Rocky Linux installation
- VirtualBox/UTM virtualization platform
- Headless server configuration (no GUI)
- SELinux/AppArmor security framework active

**Disk Management:**
- Minimum 2 encrypted partitions using LVM
- Proper partition structure for system optimization
- Storage monitoring and usage tracking

### Security Configuration

**User Management:**
| Component | Configuration |
|-----------|---------------|
| Root Access | SSH root login disabled |
| User Creation | Personal user + user42 group membership |
| Sudo Access | Restricted to sudo group with custom rules |
| Password Policy | 30-day expiry, complexity requirements |

**Network Security:**
| Service | Configuration |
|---------|---------------|
| SSH | Custom port 4242, root access disabled |
| Firewall | UFW/firewalld with port 4242 only |
| Monitoring | Connection tracking and logging |

### Password Policy Implementation

**Strength Requirements:**
- Minimum 10 characters with uppercase, lowercase, and numbers
- No more than 3 consecutive identical characters
- Cannot contain username
- 7 characters different from previous password (non-root)
- 30-day expiration with 7-day warning
- 2-day minimum between changes

### Sudo Configuration

**Security Restrictions:**
- 3 authentication attempts maximum
- Custom error messages for failed attempts
- Complete logging of inputs/outputs in `/var/log/sudo/`
- TTY mode enforcement
- Restricted PATH environment

```bash
# Example sudo configuration
Defaults    passwd_tries=3
Defaults    badpass_message="Custom error message"
Defaults    logfile="/var/log/sudo/sudo.log"
Defaults    log_input,log_output
Defaults    requiretty
Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

### System Monitoring Script

**Monitoring.sh Features:**
- Architecture and kernel version reporting
- Physical/virtual processor count
- RAM usage statistics with percentages
- Storage utilization tracking
- CPU load monitoring
- Last reboot timestamp
- LVM status verification
- Active connection counting
- User session tracking
- Network interface information (IP/MAC)
- Sudo command execution counter

**Automation:**
- Cron job execution every 10 minutes
- Wall broadcast to all terminals
- Error-free operation requirement
- Real-time system status display

## Bonus Implementation

### Advanced Partitioning
- Complex partition structure following provided schema
- Optimized disk layout for server performance
- Enhanced storage management practices

### Web Server Stack
- **lighttpd** - Lightweight HTTP server
- **MariaDB** - Database management system
- **PHP** - Server-side scripting language
- **WordPress** - Content management system

### Additional Service
- **Minecraft Server** - Game server implementation
- Custom service configuration and management
- Port management and firewall rules adaptation
- Service monitoring and maintenance

## Usage

### Initial Setup
```bash
# Check system information
hostnamectl
lsblk
sudo ufw status

# Verify services
systemctl status ssh
systemctl status ufw
```

### User Management
```bash
# Create new user
sudo adduser newuser
sudo usermod -aG user42 newuser
sudo usermod -aG sudo newuser

# Password management
sudo passwd newuser
sudo chage -l newuser
```

### Monitoring
```bash
# Run monitoring script
sudo ./monitoring.sh

# Check cron jobs
sudo crontab -l

# View logs
sudo tail -f /var/log/sudo/sudo.log
```

## Technical Challenges Overcome

- **Secure configuration management** - Balancing security with usability in system setup
- **Automated monitoring** - Creating reliable scripts that handle edge cases and system variations
- **Service integration** - Properly configuring multiple services to work together securely
- **Network security** - Implementing proper firewall rules while maintaining functionality
- **User permission management** - Setting up granular access controls without breaking workflows
- **System hardening** - Applying security best practices without compromising system stability

## Evaluation Preparation

**Key Knowledge Areas:**
- Differences between `apt` and `aptitude` package managers
- Understanding of AppArmor/SELinux security frameworks
- SSH configuration and security principles
- LVM and disk encryption concepts
- Sudo mechanism and security implications
- System monitoring and process management
- Firewall configuration and network security

**Demo Capabilities:**
- Create new users and assign groups
- Modify hostname during evaluation
- Explain monitoring script functionality
- Demonstrate password policy enforcement
- Show sudo logging and restrictions

---

*This project was completed as part of the 42 School curriculum, demonstrating proficiency in Linux system administration, security configuration, and infrastructure management.*

---

## License

This project is licensed under the [MIT License](./LICENSE).
