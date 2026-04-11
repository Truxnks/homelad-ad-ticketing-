# homelad-ad-ticketing-
Active Directory Homelab with ManageEngine ServiceDesk Plus - Complete IT ticketing system setup
> Complete IT Service Management environment with Active Directory and ManageEngine ServiceDesk Plus

This project simulates a real-world corporate IT environment where I act as the helpdesk technician. I built a Windows Server domain controller, configured Active Directory, deployed DHCP/DNS, created domain-joined client machines, and will integrate a professional ticketing system (ManageEngine ServiceDesk Plus).

**Purpose:** Demonstrate hands-on experience with technologies used daily in helpdesk, desktop support, and junior system administrator roles.
---

## Infrastructure Architecture
┌─────────────────────────────────────┐
│ Internal Network (homelab) │
│ 192.168.1.0/24 │
└─────────────────────────────────────┘
│
┌─────────────┬───────────────┼───────────────┬─────────────┐
│ │ │ │ │
▼ ▼ ▼ ▼ ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ DC01 │ │ CLIENT01 │ │ CLIENT02 │ │ ITSM01 │
│ 192.168.1.10 │ │ DHCP │ │ DHCP │ │192.168.1.30 │
│──────────────│ │──────────────│ │──────────────│ │──────────────│
│ AD Domain │ │ Win10 Pro │ │ Win10 Pro │ │ ServiceDesk │
│ DNS Server │ │ Domain-Joined│ │ Domain-Joined│ │ Plus │
│ DHCP Server │ │ │ │ │ │ (Planned) │
└──────────────┘ └──────────────┘ └──────────────┘ └──────────────┘

##  Completed Tasks

### Domain Controller (DC01)
- [x] Windows Server 2022 installed (Desktop Experience)
- [x] Static IP: 192.168.1.10
- [x] Active Directory Domain: `corp.local`
- [x] DNS server configured
- [x] DHCP server with scope 192.168.1.100-200
- [x] DHCP options: DNS=192.168.1.10, Gateway=192.168.1.1

### Active Directory Structure
- [x] OUs: CORP → Departments → IT, HR, Sales
- [x] Sub-OUs: Users under each department
- [x] Security Groups: IT_Admins, HR_Users, Sales_Team
- [x] Test Users: John Doe (IT), Sarah Smith (HR), Mike Jones (Sales)

### Client Machines
- [x] CLIENT01 VM created (Windows 10 Pro)
- [ ] Install Windows 10 Pro
- [ ] Join to `corp.local` domain
- [ ] CLIENT02 VM (planned)

### Ticketing System
- [ ] ManageEngine ServiceDesk Plus installation (in progress)
- [ ] AD/LDAP integration
- [ ] Ticket creation and tracking

---

##  Problems Solved & Lessons Learned

| Problem | Root Cause | Solution | Skill Demonstrated |
|---------|-----------|----------|---------------------|
| VM wouldn't boot | Insufficient RAM (4MB allocated) | Increased RAM to 4096MB | Virtual machine configuration |
| "No bootable device found" | EFI conflict with ISO | Disabled EFI for Windows 10 VM | BIOS/EFI troubleshooting |
| Windows 11 TPM requirement | VirtualBox lacks TPM 2.0 by default | Switched to Windows 10 Pro | OS selection for homelab |
| VMs couldn't communicate | Mixed network types (NAT vs Internal) | Standardized on Internal Network | Virtual networking |
| DHCP authorization failed | Homelab domain limitations | Registry bypass method | Windows Server configuration |
| Domain join failed | Wrong DNS configuration | Set DNS to 192.168.1.10 | DNS troubleshooting |

---

##  Technologies Used

| Technology | Purpose |
|------------|---------|
| Oracle VirtualBox | Virtualization platform |
| Windows Server 2022 | Domain Controller, DNS, DHCP |
| Windows 10 Pro | Domain-joined client machines |
| Active Directory | User/group management, authentication |
| PowerShell | Automation and configuration |
| ManageEngine ServiceDesk Plus | Ticketing system (planned) |
| GitHub | Documentation and portfolio |

---

##  Repository Structure
homelab-helpdesk-lab/
├── README.md # This file
├── docs/
│ ├── setup-guide.md # Step-by-step installation
│ ├── troubleshooting.md # Common issues and fixes
│ └── tickets.md # Simulated helpdesk tickets
├── scripts/
│ ├── ad-setup.ps1 # AD automation script
│ ├── dhcp-setup.ps1 # DHCP configuration
│ ├── create-users.ps1 # User creation script
│ └── domain-join.ps1 # Automated domain join
├── screenshots/
│ ├── 01-dc01-desktop.png
│ ├── 02-dc01-ipconfig.png
│ ├── 03-ad-users-computers.png
│ ├── 04-dhcp-scope.png
│ └── 05-domain-join.png
└── resume/ # How to add this to your resume
└── resume-bullet-points.md

text

---

##  Screenshots

| Screenshot | Description |
|------------|-------------|
| [01-dc01-desktop.png](screenshots/01-dc01-desktop.png) | DC01 desktop after installation |
| [02-dc01-ipconfig.png](screenshots/02-dc01-ipconfig.png) | Static IP and DNS configuration |
| [03-ad-users-computers.png](screenshots/03-ad-users-computers.png) | AD Users and Computers console showing OUs |
| [04-dhcp-scope.png](screenshots/04-dhcp-scope.png) | DHCP scope configuration |
| [05-domain-join.png](screenshots/05-domain-join.png) | Client successfully joined to domain |

---

##  How to Replicate This Lab

### Prerequisites
- VirtualBox installed
- Windows Server 2022 ISO (180-day eval)
- Windows 10 Pro ISO
- 16GB+ RAM on host machine
- 100GB+ free disk space

### Quick Start Commands

**On DC01 (PowerShell as Admin):**
```powershell
# Set static IP
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress "192.168.1.10" -PrefixLength 24

# Install AD
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSForest -DomainName "corp.local" -DomainNetbiosName "CORP" -InstallDns -Force

# Install DHCP
Install-WindowsFeature DHCP -IncludeManagementTools
Add-DhcpServerv4Scope -Name "Corp Network" -StartRange 192.168.1.100 -EndRange 192.168.1.200 -SubnetMask 255.255.255.0
