## 📦 Phase 1: Lab Setup

<br>

### 🔧 1. Initialize the Project
- Create a new GitHub repo: `network-intrusion-lab`
- Add a short `README.md`:
  - What the project is
  - Tools being used
  - What I hope to learn

  ***
  <br>


### 🖥️ 2. Configure Virtual Machines
- Set up 3 VMs in VirtualBox:
  - Ubuntu Server → Target
  - Kali Linux → Attacker
  - Ubuntu Desktop → Detection (with Suricata)

  ***
  <br>


### 🌐 3. Set Up Internal Networking
- Place all VMs on an **Internal Network**
- Ensure all machines can ping each other
- Install `openssh-server` on the target VM



> 🛠 [Unique IP address troubleshooting](./troubleshooting/unique-ip-setup.md)

***
<br>

### 🌐 4. Assign Static IPs
- Use `netplan` to configure static IPs on all VMs  
  (e.g., 192.168.56.10, .20, .30)

> 📓 [Detailed notes in logs](./logs/notes.md#ip-setup)

***
<br>


### 📂 5. Create Shared Folders
- Set up host-to-VM shared folders in VirtualBox
- Mount them inside each VM for easy file transfer

> 🛠 [Guest Additions troubleshooting](./troubleshooting/guest-additions.md)

***
***

<br>

## ⚔️ Phase 2: Attack & Detect

<br>

### 🎯 1. Reconnaissance (Scanning the Target)

- Run an aggressive scan on the Ubuntu Server from Kali

- Document open ports, running services, and potential vulnerabilities



***
<br>

### 🔓 2. Launch Basic Attacks

- Choose a target service (e.g. SSH or HTTP) and run an attack:

	- Hydra for SSH brute-force
	
	- Burp Suite to simulate a basic web login attack



***
<br>

### 🛡 3. Detect the Activity

- Monitor traffic on the Ubuntu Desktop (Suricata) VM

- Use fast.log, eve.json, or Wireshark to inspect alerts

- Label:

	- What was detected?
	
	- What was missed?
	
	- Severity level?



***
<br>

### 📁 4. Export & Archive Evidence

- Save important logs or packet captures

	- Suricata alerts
	
	- Nmap scan results
	
	- Screenshots of attack or detection
  