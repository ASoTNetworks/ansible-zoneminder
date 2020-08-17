# Installing ZoneMinder
Use the playbook zm-install.yml to set up ZoneMinder

This playbook will install common system utils, set up network interfaces, install and configure ZoneMinder and Apache, configure OpenVPN client for remote management, configure system firewall, enable unattended-upgrades, and harden SSHd to allow only allow key login.

Before using the playbook ensure the following have been done:
1. System is configured with 2 network interfaces the playbook will overwrite and configure network settings for you.
    - eth0 for regular internet access (DHCP)
    - eth1 for camera network (192.0.2.1/24)
1. Install Debian 10 with standard setup, would recommand having a second partition or drive(s) if possible for storing footage.
1. Copy your SSH public key to ~/.ssh/authorized_keys on the new Debian 10 box or use `ssh-copy <ip-address>`
1. Have a OpenVPN server for remote management and export those keys to [roles/openvpn/files](roles/openvpn/files) all files in this directory will be copied to the ZoneMinder server main config file must be named `zoneminder-client.conf`.
1. Now you can run the playbook `ansible-playbook -i ip-address-of-zm, zm-install.yml --extra-vars "ansible_sudo_pass=your_sudo_password"`

After the playbook has successfully finished you can now access ZoneMinder at https://`ip-address-of-zm`:57167

To install a trusted certificate replace cert and key in `/etc/apache2/ssl/`