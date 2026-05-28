# Active Directory Home Lab (Windows Server 2022 + Windows 11)

---

## Overview

This project is a home lab designed to simulate a small enterprise Active Directory environment. It demonstrates core Windows Server administration concepts including domain services, DNS, Group Policy, and role-based access control.

The environment was built using virtualization and configured from scratch to replicate real-world IT infrastructure scenarios.

---

## Lab Architecture

- Domain: `lab.local`
- Domain Controller: DC01
- Client Machine: Client1
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

### Domain Setup
- Created domain: `lab.local`
- Promoted DC01 as Domain Controller
- Configured DNS integrated with Active Directory

### Organizational Units (OUs)
- LAB
  - Users
  - Computers
  - Groups

### Users
- HR users
- Finance users
- IT users

### Security Groups
- HR
- Finance
- IT

Role-based access control (RBAC) was implemented using security groups.

---

## File Server Configuration

A centralized file share was created on DC01 using SMB.

### Share Location
- `\\DC01\Shares$` (hidden share)

### Folder Structure
- HR
- Finance
- IT

### Permissions Model
- Share permissions: Authenticated Users (Change)
- NTFS permissions: Controlled via security groups

Access is restricted based on group membership (least privilege model).

---

## Group Policy Configuration

Group Policy was used to automate user environment configuration.

### Drive Mapping Policy
- HR → H: drive
- Finance → F: drive
- IT → I: drive

### Configuration Method
- Group Policy Preferences
- Item-level targeting based on security groups

---

## Security Model

This lab implements Role-Based Access Control (RBAC):

- Users are assigned to security groups
- Groups control NTFS permissions
- Access to resources is centrally managed through Active Directory

---

## Validation & Testing

The environment was validated through the following tests:

- Successful domain join of Windows 11 client
- DNS resolution of `lab.local`
- Group Policy application using `gpupdate /force`
- File share access via `\\DC01\Shares$`
- Drive mapping based on user groups
- NTFS permission enforcement

---

## Screenshots & Validation

Each screenshot represents a functional validation of a core system component.

---

### 01 - Active Directory Structure
Shows the Organizational Unit (OU) structure within Active Directory:
- LAB OU
- Users
- Groups
- Computers

---

### 02 - Users and Security Groups
Shows created user accounts and security groups:
- HR, Finance, IT groups
- Users assigned to groups

---

### 03 - DNS Resolution Test
Shows DNS lookup for `lab.local`, confirming:
- Proper DNS resolution
- Domain Controller handling DNS services

---

### 04 - Network Configuration (Client Machine)
Shows `ipconfig /all` output confirming:
- Correct internal IP assignment
- DNS pointing to Domain Controller

---

### 05 - Domain Login Verification
Shows `whoami` output confirming:
- Successful domain authentication
- User logged into `lab.local`

---

### 06 - File Share Access
Shows access to:
- `\\DC01\Shares$`
- HR, Finance, IT folders

---

### 07 - Group Policy Configuration
Shows Group Policy Management Console configuration:
- Drive mapping policy
- Group-based drive assignments

---

### 08 - NTFS Permissions
Shows security permissions on shared folders:
- Group-based access control
- Least privilege enforcement

---

### 09 - Group Policy Application Verification
Shows `gpresult /r` output confirming:
- Applied Group Policy Objects
- Drive mapping policies active

---

## How I Built This Environment

### 1. Virtual Environment Setup
- Created two VMs using VirtualBox:
  - Windows Server 2022 (DC01)
  - Windows 11 (Client1)

- Configured networking:
  - NAT for internet access
  - Internal Network (locallab) for domain communication

---

### 2. Domain Controller Configuration
- Installed AD DS and DNS roles
- Promoted server to Domain Controller
- Created forest: `lab.local`
- Configured static IP for DNS stability

---

### 3. Active Directory Structure
- Created LAB OU structure
- Created users and security groups
- Assigned users to appropriate groups for RBAC

---

### 4. File Sharing and Permissions
- Created SMB share on DC01
- Configured folder structure:
  - HR, Finance, IT
- Applied NTFS permissions using security groups

---

### 5. Group Policy Configuration
- Created GPO for drive mapping
- Configured:
  - HR → H:
  - Finance → F:
  - IT → I:
- Used item-level targeting for group-based assignment

---

### 6. Client Setup
- Joined Windows 11 machine to domain
- Verified DNS configuration
- Confirmed Group Policy application

---

### 7. Validation & Testing
- Verified domain authentication
- Tested DNS resolution
- Confirmed file access permissions
- Validated GPO drive mapping behavior

---

## Future Improvements

- Add second Domain Controller for redundancy
- Implement DHCP server role
- Add file auditing and logging
- Introduce firewall segmentation (pfSense)
- Automate user/group creation using PowerShell
