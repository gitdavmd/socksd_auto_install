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

## Installation

Clone the repository and make the script executable:

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
chmod +x socks5.sh

Security Note
Only use this script on servers that you own or administer. Use the whitelist feature to restrict access to trusted IP addresses and avoid exposing the SOCKS5 port unnecessarily.

Passwords provided directly through the -adduser command may temporarily appear in shell history or the process list. For sensitive environments, the interactive installation method is recommended.

License
Add the license you want to use for this project, such as the MIT License.


### Very Short GitHub “About” Description

```text
Bash script for installing and managing a Dante SOCKS5 proxy on AlmaLinux 10.
