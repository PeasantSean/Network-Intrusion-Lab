# Network Intrusion Lab Setup — Phase 1: Useful Commands
*This is a list of commands I learned/used while troubleshooting. They seem valuable so I wanted to make a quick-reference sheet for future me.*
<br>

- Check if Suricata is installed
`which suricata`
***
<br>

- Update package lists
`sudo apt updates`
***
<br>

- Install openssh server
`sudo apt install openssh-server -y`
***
<br>

- Start and enable ssh service
`sudo systemctl start ssh`
`sudo systemctl enable ssh`

***
<br>

- Check ssh service status
`sudo systemctl status ssh`
***
<br>

- Install Apache2 web server
`sudo apt install apache2 -y`
***
<br>

- View network interfaces and IP addresses
`ip a`
***
<br>

- Edit Netplan configuration (for static IPs)
`sudo nano /etc/netplan/00-installer-config.yaml`
***
<br>

- Apply Netplan configuration
`sudo netplan apply`
***
<br>

- Mount VirtualBox shared folder (after Guest Additions installed)

`sudo mkdir /mnt/shared`

`sudo mount -t vboxsf shared-folder-name /mnt/shared`