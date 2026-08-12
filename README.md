# 🌐 Active Directory & Secure Network Enterprise Lab

## 📋 Project Overview
This project showcases the deployment of a fully isolated enterprise sandbox environment using **Oracle VirtualBox**. The goal of this lab was to simulate real-world IT infrastructure administration, mapping user organizational units, managing access controls, and deploying domain-wide security hardening policies.

## 🛠️ Technologies & Skills Demonstrated
* **Hypervisor:** Oracle VirtualBox
* **Server OS:** Windows Server 2022 (Desktop Experience)
* **Directory Services:** Active Directory Domain Services (AD DS)
* **Network Infrastructure:** Static IP Allocation, Internal Virtual Networking switches, DNS management
* **Security & Automation:** Group Policy Management (GPOs)

## 🔒 Implemented Security Protocols
1. **Account Lockout Policy:** Configured a global Domain Policy enforcing a 5-attempt invalid login lockout threshold to prevent brute-force attacks.
2. **Command Prompt Hardening:** Deployed a GPO restricting non-administrative domain users (e.g., standard employee profiles) from executing or accessing the CLI environment to reduce internal network vulnerability.

## 🛠️ Project Troubleshooting & Diagnostic Log

| Challenge Encountered | Root Cause | Technical Resolution Applied |
| :--- | :--- | :--- |
| **"Next" Button Greyed Out** on Drive Partition Screen | VirtualBox's automated disk allocation clashed with the standard Windows installation partition layout cache. | Wiped the drive tables completely clean using the **Command Line Interface (CLI)**. Launched `diskpart`, executed `select disk 0`, and ran the `clean` command to clear the partition blocks. |
| **Installation Boot Loop** (Server kept restarting back into the initial installation screen) | The VM rebooted after copying file binaries, but VirtualBox retained priority execution on the original installation ISO image. | Executed a hardware unmount. Opened VM Storage Settings, selected the optical drive tree, and chose **"Remove Disk from Virtual Drive"** to force the VM to boot from its newly provisioned virtual hard disk. |
| **Active Directory Pre-requisite Block** | Active Directory requires a permanent, unchangeable network destination to handle DNS routing updates. | Configured a **Static IP address (`192.168.10.10`)** via network adapter configurations and assigned the local loopback address (`127.0.0.1`) as the primary DNS destination. |
| **Host System Resource Bottleneck** | The physical laptop only possessed **8 GB of total physical RAM**. Running two separate virtual environments at 4 GB each would exhaust all system memory, causing host OS freezing or virtualization crashes. | **Resource Optimization Strategy:** Switched the client target machine from Windows 11 to a lightweight **Windows 10 Pro environment**. Throttled both the Windows Server and Windows 10 client allocations down to an optimized **2048 MB (2 GB) of RAM** each, safely freeing up 4 GB for the physical host machine. |
| **"PING: transmit failed. General failure."** on Client Machine | The client was configured to pull an IP automatically, but since it was disconnected from an external router to link to the isolated server network, it possessed an invalid/empty routing table. | Assigned a manual static IP block to the client (`192.168.10.20`) mapping to the same subnet, and verified VirtualBox network adapters on both VMs were bridged identically to the same **Internal Network (`intnet`)** configuration. |

<img width="1022" height="870" alt="image (3)" src="https://github.com/user-attachments/assets/ee603b97-1fc9-4a98-9b5c-e9d2e89542b4" />
<img width="1023" height="842" alt="image (4)" src="https://github.com/user-attachments/assets/d85a686f-ee75-449e-9da6-b082bebaf802" />
<img width="1025" height="870" alt="image (5)" src="https://github.com/user-attachments/assets/2807e101-6e21-4775-b2fc-10e749a961f8" />
<img width="747" height="526" alt="image (6)" src="https://github.com/user-attachments/assets/a41848a0-4715-44c8-9b80-d725d0088595" />

