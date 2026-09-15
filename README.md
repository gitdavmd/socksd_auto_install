# Dante SOCKS5 Manager for AlmaLinux 10

A Bash script for installing and managing a Dante-based SOCKS5 proxy server on AlmaLinux 10.

The script automates the installation and configuration of Dante, user authentication management, firewall configuration, service management, log viewing, and IP whitelist administration.

## Features

- Interactive SOCKS5 proxy installation
- Automatic Dante service configuration
- Automatic detection of the external network interface
- Creation of an authentication user
- Add, update, and delete proxy users
- Automatic `firewalld` port configuration
- Service status and listening port verification
- Dante and systemd log viewing
- CIDR-based IP whitelist configuration
- Automatic configuration backups
- Complete Dante uninstallation

## Requirements

- AlmaLinux 10
- `root` access or `sudo` privileges
- `systemd`
- `dnf`
- `firewalld`, if automatic firewall configuration is required
- Internet access for package installation

Summary of what each option does
  Option	Behavior
(no args)	Interactive install: asks port, user, password, sets up Dante, firewall, verifies listener.
-uninstall	Stops/disables service, removes dante-server, deletes config and log, closes firewall ports. Does not delete auth users (safety).
-adduser USER PASS	Creates a system user (or updates password if exists) for proxy authentication.
-deluser USER	Deletes the proxy auth user from the system.
-log [N]	Tails the last N lines (default 50) of /var/log/sockd.log. Falls back to journalctl if the file is missing.
-whitelist=CIDR[:CIDR...]	Replaces the client pass block with a whitelist. Accepts : as separator. Example: -whitelist=1.2.3.0/24:5.6.7.8/32. Restarts service and rolls back on failure.

## Installation

Clone the repository and make the script executable:

```bash
git clone https://github.com/gitdavmd/REPOSITORY.git
cd REPOSITORY
chmod +x socks5.sh

**Usage**
sudo ./socks5.sh

**Add or update a proxy user**
sudo ./socks5.sh -adduser USERNAME PASSWORD
If the user already exists, their password will be updated.

**Delete a proxy user**
sudo ./socks5.sh -deluser USERNAME

**View logs**
Display the last 50 log lines:
sudo ./socks5.sh -log

**Configure the IP whitelist**
Allow a single IP address:
sudo ./socks5.sh -whitelist=1.2.3.4/32
Allow an entire network:
sudo ./socks5.sh -whitelist=1.2.3.0/24
Allow multiple IP addresses or networks separated by ::
sudo ./socks5.sh -whitelist=1.2.3.0/24:5.6.7.8/32
The configuration is backed up automatically, and the Dante service is restarted after the whitelist is updated.

**Uninstall Dante**
sudo ./socks5.sh -uninstall

The uninstall operation stops and disables the service, removes the Dante package, deletes configuration files and logs, and attempts to clean up firewall rules.
Authentication users are not removed automatically.

**Display help**
sudo ./socks5.sh --help

**Testing the Proxy**
After installation, test the SOCKS5 proxy with curl:
curl --socks5-basic \
  -u USERNAME:PASSWORD \
  -x socks5://SERVER_IP:1080 \
  https://ifconfig.me

Replace:

USERNAME with the configured proxy username
PASSWORD with the proxy password
SERVER_IP with the server IP address
1080 with the configured SOCKS5 port

**Files Used**
Depending on the Dante installation, the script may use:
/etc/sockd.conf
/etc/danted.conf
/var/log/sockd.log

Before modifying the configuration, the script creates timestamped backups such as:
/etc/sockd.conf.bak.TIMESTAMP

**Security Note**
Only use this script on servers that you own or administer. Use the whitelist feature to restrict
access to trusted IP addresses and avoid exposing the SOCKS5 port unnecessarily.

Passwords provided directly through the -adduser command may temporarily appear in shell history
or the process list. For sensitive environments, the interactive installation method is recommended.

**License**
Add the license you want to use for this project, such as the MIT License.


### Very Short GitHub “About” Description

```text
Bash script for installing and managing a Dante SOCKS5 proxy on AlmaLinux 10.
