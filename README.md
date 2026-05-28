# Active Directory Home Lab (Windows Server 2022 + Windows 11)

## Overview

This project is a home lab designed to simulate a small enterprise Active Directory environment. It demonstrates core Windows Server administration concepts including domain services, DNS, Group Policy, and role-based access control.

The environment was built using virtualization and configured from scratch to replicate real-world IT infrastructure scenarios.

---

## Lab Architecture

- Domain: `lab.local`
- Domain Controller: dc01
- Client Machine: client1
- Network Configuration:
  - NAT Adapter: Internet access
  - Internal Network (locallab): Domain communication

---

## Technologies Used

- Windows Server 2022
- Windows 11
- Oracle VM VirtualBox
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy (GPO)
- NTFS File Permissions
- SMB File Sharing

---

## Active Directory Configuration

- Created domain: `lab.local`
- Promoted DC01 as Domain Controller
- Configured DNS integrated with Active Directory

### Organizational Units (OUs)
- LAB
  - Users
  - Computers
  - Groups

### User Accounts
- HR users
- Finance users
- IT users

### Security Groups
- HR
- Finance
- IT

Role-based access control was implemented using security groups.

---

## File Server Configuration

A centralized file share was created on DC01:

- `\\DC01\Shares$` (hidden share)

### Folder Structure:
- HR
- Finance
- IT

### Permissions Model:
- Share permissions: Authenticated Users (Change)
- NTFS permissions: Controlled via security groups

Access is restricted based on group membership.

---

## Group Policy Configuration

Group Policy was used to automate user environment configuration.

### Drive Mapping Policy:
- HR → H: drive
- Finance → F: drive
- IT → I: drive

### Configuration Method:
- Group Policy Preferences
- Item-level targeting based on security groups

---

## Security Model

This lab implements Role-Based Access Control (RBAC):

- Users are assigned to security groups
- Groups control NTFS permissions
- Access to resources is centrally managed through Active Directory

This follows the principle of least privilege.

---

## Validation & Testing

The following were verified during testing:

- Domain join successful on Windows 11 client
- DNS resolution working correctly
- Group Policy applied successfully using gpupdate
- File access restricted based on group membership
- Mapped drives applied based on user role

---

## Key Skills Demonstrated

- Active Directory administration
- DNS configuration and troubleshooting
- Group Policy management
- Windows file sharing and NTFS permissions
- Role-based access control (RBAC)
- Virtualized network configuration
- Windows client/server integration

---

## Future Improvements

- Add second Domain Controller for redundancy
- Deploy DHCP for automatic IP configuration
- Implement file auditing and logging
- Add firewall segmentation using pfSense
- Automate user and group creation with PowerShell
