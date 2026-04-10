# homelad-ad-ticketing-
Active Directory Homelab with ManageEngine ServiceDesk Plus - Complete IT ticketing system setup
> Complete IT Service Management environment with Active Directory and ManageEngine ServiceDesk Plus

##  Architecture
┌─────────────────────────────────────────────────────────┐
│ Internal Network (192.168.1.0/24) │
├─────────────────────────────────────────────────────────┤
│ DC01 (192.168.1.10) │
│ ├── Windows Server 2022 │
│ ├── Active Directory (corp.homelab.local) │
│ ├── DNS Server │
│ └── DHCP Server │
├─────────────────────────────────────────────────────────┤
│ ITSM01 (192.168.1.30) │
│ ├── Windows Server 2022 (Desktop Experience) │
│ ├── Domain Joined │
│ └── ManageEngine ServiceDesk Plus │

##  What I Built

- **Active Directory Domain:** `corp.homelab.local`
- **DHCP Scope:** 192.168.1.100-200 with DNS pointing to DC
- **Organizational Units:** IT, HR, Finance, Sales
- **Security Groups:** IT_Admins, HR_Users, Finance_Team, Sales_Team
- **Test Users:** Created with PowerShell automation
- **Ticketing System VM:** Ready for ServiceDesk Plus installation

##  Problems Solved & Lessons Learned

| Problem | Root Cause | Solution |
|---------|-----------|----------|
| APIPA IP address (169.254.x.x) | No DHCP server | Set static IPs on DC and ticketing VM |
| VMs couldn't communicate | Different VirtualBox network types | Standardized on Internal Network |
| DHCP authorization failed | Homelab domain limitations | Registry bypass method |
| DNS resolution failures | Client not pointing to DC | Configured DNS to 192.168.1.10 |

##  Technologies Used

- **Virtualization:** Oracle VirtualBox
- **Operating Systems:** Windows Server 2022
- **Directory Services:** Active Directory Domain Services
- **Networking:** DHCP, DNS, Internal Networking
- **Ticketing:** ManageEngine ServiceDesk Plus (Professional Edition)
- **Scripting:** PowerShell

## Repository Structure
homelab-ad-ticketing/
├── README.md
├── docs/
│ ├── setup-guide.md
│ ├── troubleshooting.md
│ └── lessons-learned.md
├── scripts/
│ ├── ad-setup.ps1
│ ├── dhcp-setup.ps1
│ ├── ou-creation.ps1
│ └── user-creation.ps1
└── screenshots/


##  Skills Demonstrated

- Active Directory design and deployment
- DHCP server configuration and scope management
- DNS configuration for domain environments
- Virtual networking (VirtualBox Internal Networks)
- Windows Server administration (Core vs Desktop Experience)
- PowerShell scripting for automation
- Network troubleshooting (APIPA, DNS resolution, connectivity)

##  Next Steps

- [ ] Complete ServiceDesk Plus installation
- [ ] Configure AD integration with ticketing system
- [ ] Create service catalog and workflows
- [ ] Document ticket lifecycle

##  Contact

Project Link: 
