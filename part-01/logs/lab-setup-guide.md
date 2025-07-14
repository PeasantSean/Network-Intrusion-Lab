
# Network Intrusion Lab Setup — General Instructions

*Here's the majority of my lab setup and steps I took to troubleshoot roadblocks*
*Note: IP addresses have been redacted for security. Replace with your own internal IP scheme.*
***
<br>

## VM Setup

### 1. Create Virtual Machines

- Create VMs for Ubuntu Desktop, Ubuntu Server and Kali Linux.
- Recommended settings:

  - **Base memory**: 2048 MB (minimum)
  - **CPUs**: 2
  - **Video Memory**: 128 MB
  - Disable 3D Acceleration

### 2. Network Settings (Initial)

- Start with **NAT** so you can update packages and install Guest Additions.

<br>

***

<br>

## Installing Guest Additions


**Step 1: Update and Install Build Tools**

`sudo apt update`

`sudo apt upgrade -y`

`sudo apt install build-essential dkms linux-headers-$(uname -r) -y`


<br>

**Step 2: Insert Guest Additions ISO**

From VirtualBox window menu:

> Devices → Insert Guest Additions CD Image...

*If prompted, allow it to download the ISO.*

<br>

**Step 3: Mount and Run Installer**

`sudo mkdir -p /mnt/cdrom`

`sudo mount /dev/cdrom /mnt/cdrom`

`cd /mnt/cdrom`

`sudo ./VBoxLinuxAdditions.run`


<br>

Step 4: Reboot

`sudo reboot`

<br>

***

<br>

**Troubleshooting**

* **bzip2 or tar not found**:

`sudo apt install bzip2 tar -y`


<br>

- **GUI glitching after Guest Additions**:

  - Power off VM
  - VirtualBox Settings  Display:
    - Set video memory to 128 MB
    - Disable 3D acceleration
  - Boot VM and uninstall Guest Additions:

`sudo /opt/VBoxGuestAdditions*/uninstall.sh`

`sudo reboot`


***

<br>

## Shared Folders Setup

### 1. Create a Folder on Host

`mkdir ~/vmshare`

<br>

### 2. In VirtualBox Settings (VM specific)

- Go to **Settings → Shared Folders**
- Add new folder:

  - Folder path: \~/vmshare
  - Folder name: vmshare
  - Check: Auto-mount, Make Permanent

<br>

### 3. Access Inside VM

- After installing Guest Additions and rebooting:

`ls /media`

`ls /media/$USER`


- If permission denied:

`sudo usermod -aG vboxsf $USER`

`sudo reboot`

***

<br>

## Installing Apache2 

### Install Apache2

`sudo apt update`

`sudo apt install apache2 -y`

<br>

### Check Status

`sudo systemctl status apache2`

<br>

### Serve Custom Page

`echo "Hello from Apache!" | sudo tee /var/www/html/index.html`

***

<br>

## Set Up Internal Network

### 1. Configure VirtualBox Network

- Shut down VMs
- Go to Settings → Network
- Adapter 1:
  - Attached to: **Internal Network**
  - Name: **intnet** (same on all VMs)

### 2. Ubuntu Static IP via Netplan

**Find interface name**

`ip a`

**Edit config**

`sudo nano /etc/netplan/01-internal.yaml`


**Example for VM1:**

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      addresses: [192.168.x.x/x]
      nameservers:
        addresses: [8.8.8.8]
```

**Fix permissions:**

`sudo chmod 644 /etc/netplan/01-internal.yaml`

`sudo netplan apply`


### 3. Kali Linux Static IP via interfaces file

Find interface name

`ip a`

Edit config

`sudo nano /etc/network/interfaces`

Example:

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.x.x
    netmask 255.255.255.0
```

Apply changes:

`sudo systemctl restart networking`
*or*
`sudo ifdown eth0 && sudo ifup eth0`


***

<br>


## Common Errors and Fixes

`No such file or directory` on YAML:

- You're on Kali — use `/etc/network/interfaces` instead.

 `gateway4 has been deprecated`:

- Just remove `gateway4` from YAML. It's not needed for internal-only networks.

`permissions are too open`:

`sudo chmod 644 /etc/netplan/01-internal.yaml`

`Destination Host Unreachable`:

- Make sure:
  - Both VMs are on the same internal network `intnet`
  - Static IPs are set properly
  - Interfaces are applied and active

---

<br>

## Final Testing

**Ping each VM from one another:**

`ping 192.168.x.x`


If pings succeed, you have internal VM communication working. You're now ready to begin intrusion detection experiments (e.g., scanning, exploiting, defending, etc.).
