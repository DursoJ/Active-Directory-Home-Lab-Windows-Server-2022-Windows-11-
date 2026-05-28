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

## Screenshots & Validation

This section documents the key components of the Active Directory lab environment. Each screenshot represents a functional validation of a specific service or configuration.

---

### 01 - Active Directory Structure
This screenshot shows the Active Directory Organizational Unit (OU) structure created on the domain controller.

It includes:
- LAB OU
- Users container
- Groups container
- Computers container

This validates that the domain structure was properly designed and organized to support centralized identity management.

---

### 02 - Users and Security Groups
This screenshot displays the configured user accounts and security groups within Active Directory.

It includes:
- HR, Finance, and HelpDesk security groups
- User accounts assigned to a group

This demonstrates role-based access control (RBAC) implementation using Active Directory security groups.

---

### 03 - DNS Resolution Test
This screenshot shows DNS name resolution using `nslookup` for the domain `lab.local`.

The output confirms:
- The domain name resolves successfully
- DNS is being handled by the Domain Controller

This validates that Active Directory-integrated DNS is functioning correctly.

---

### 04 - Network Configuration (Client Machine)
This screenshot shows the network configuration of the Windows 11 client using `ipconfig /all`.

It confirms:
- Correct IP address assignment within the internal network
- DNS server pointing to the Domain Controller

This ensures proper network communication between client and domain services.

---

### 05 - Domain Login Verification
This screenshot shows the logged-in domain user using the `whoami` command.

It confirms:
- The Windows 11 machine is successfully joined to the `lab.local` domain
- User authentication is being handled by Active Directory

---

### 06 - Mapped Network Drives
This screenshot shows automatically mapped network drives on the Windows 11 client.

It confirms:
- Group Policy-driven drive mapping is functioning correctly
- Users receive different drives based on group membership

This demonstrates Group Policy Preferences and user-based configuration.

---

### 07 - Group Policy Configuration
This screenshot shows the Group Policy Management Console (GPMC) configuration for drive mapping.

It includes:
- Drive mapping policy creation
- Assignment of drive letters based on security groups

This validates centralized configuration management using Group Policy.

---

### 08 - NTFS Permissions
This screenshot shows NTFS security permissions configured on the Finance shared folder.

It includes:
- Security group-based access control
- Assigned permissions such as Modify and Read

This demonstrates file-level security enforcement using NTFS permissions.

---

### 9 - Group Policy Application Verification
This screenshot shows the output of `gpresult /r` on the client machine.

It confirms:
- Group Policy Objects are successfully applied
- Drive mapping and configuration policies are active

This validates end-to-end Group Policy deployment.

## Future Improvements

- Add second Domain Controller for redundancy
- Deploy DHCP for automatic IP configuration
- Implement file auditing and logging
- Add firewall segmentation using pfSense
- Automate user and group creation with PowerShell
