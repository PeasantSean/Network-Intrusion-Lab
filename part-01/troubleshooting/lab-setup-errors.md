# Network Intrusion Lab Setup — Phase 1: Errors and Troubleshooting

*A brief log of general issues I encountered* 



***

<br>

## Suricata & OpenSSH

- Used `which suricata` to confirm installation status (uncertainty during initial checks)
- Ubuntu Server failed to install OpenSSH initially  
  - Likely a network issue  
  - Rebooted and retried — success confirmed  
  -  `ubuntu-server-openssh-success.png`
- Suricata failed to run on Ubuntu Desktop  
  -  `ubuntu-desktop-suricata-fail.png`
- OpenSSH showed as “disabled” in `systemctl` despite appearing active  
  - Status: *active*, but `Loaded:` showed *disabled; preset: enabled*  
  - Eventually confirmed active  
  - `openssh-disabled.png`, `openssh-enabled.png`

<br>

***

<br>

## Network Configuration

- No valid IP address on VMs (loopback only)  
  - Resolved by setting static IPs using Netplan and adjusting VirtualBox network settings
- Kali VM struggled to acquire an IP address  
  - `kali-ip-issue.png`

<br>

***

<br>

## VirtualBox Interaction with Host Machine

- Copy/paste between host and VM not working  
  - Resolved by enabling *bidirectional clipboard* in VirtualBox settings
- Guest Additions failed to download (likely due to lack of Ethernet)  
  - Guest Additions required for shared folder support
- Permission denied when accessing shared folder in Kali  
  - Expected fix by following same procedure used on Ubuntu Desktop  
  - `kali-permission-error.png`

<br>

***

<br>

## VM Stability Issues

- Kali Linux VM wouldn’t boot after setup  
  - Reinstalled Kali from scratch  
  - `kali-linux-install vid`
- Ubuntu Desktop glitched after installing Guest Additions  
  - Rebuilt the VM  
  - `ubuntu-desktop-glitch vid`
