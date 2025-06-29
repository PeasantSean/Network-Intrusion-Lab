⚠️ Troubleshooting / Issues Encountered

    Suricata check uncertainty
    → Used which suricata to confirm if installed.

    Ubuntu Server failed to install OpenSSH
    → Possible network issue. Rebooted, retried, and succeeded.
    → Screenshot: ubuntu-server-openssh-success.png

    Suricata failed to run on Ubuntu Desktop
    → Screenshot: ubuntu-desktop-suricata-fail.png

    OpenSSH showed as “disabled” in systemctl even after enabling
    → Status was active but Loaded: line said “disabled; preset: enabled”
    → Screenshot: openssh-disabled.png
    → Eventually successfully enabled (confirmed via: openssh-enabled.png)

    Apache2 failed to install on Ubuntu Server
    → Screenshot: apache2-failed-install.png

    No valid IP address (only loopback) on VMs initially
    → Resolved by configuring static IPs via Netplan and fixing VM network settings

    Kali VM had issues assigning IP address
    → Screenshot: kali-ip-issue.png

    Copy/paste between host and VM not working
    → Solved by enabling bidirectional clipboard in VirtualBox settings

    Failed to download Guest Additions (likely due to lack of Ethernet connection)
    → Guest Additions needed for shared folder setup

    Kali Linux VM wouldn’t boot after setup
    → Reinstalled Kali VM
    → Video: kali-linux-install vid

    Ubuntu Desktop glitched after Guest Additions install
    → Rebuilt the VM
    → Video: ubuntu-desktop-glitch vid

    Permission denied when accessing shared folder in Kali
    → Expected fix by replicating Ubuntu Desktop steps
    → Screenshot: kali-permission-error.png

