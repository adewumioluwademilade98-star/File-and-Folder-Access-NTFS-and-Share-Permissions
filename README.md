# File-and-Folder-Access-NTFS-and-Share-Permissions
Hands-on Active Directory home lab documenting Windows Server administration, user and group management, organizational units (OUs), shared folders, NTFS and share permissions, and group-based access control.

## Overview

This lab explores how Windows file-sharing permissions and NTFS permissions work together to control access to shared resources in an Active Directory domain.

My goal is to configure a shared Sales folder and assign access through the `Sales-Team` security group rather than granting permissions to individual users.

**Environment:** Windows Server / Active Directory Domain Services  
**Domain:** `corp.lab.local` (example lab domain)  
**Server:** `DC01` (example lab hostname)  
**Tools:** File Explorer, folder Properties, Advanced Sharing, and Advanced Security Settings

## Objectives

- Create a shared folder on Windows Server.
- Configure network share permissions.
- Configure NTFS permissions.
- Understand permission inheritance.
- Assign folder access to a security group.
- Apply the principle of least privilege.
- Understand how group membership determines resource access.

## Lab Tasks

### 1. Create the Sales Folder

Created a folder at:

`C:\Shares\Sales`

This folder represents a department resource that authorized Sales team members would access over the network.

### 2. Configure Share Permissions

I configured the folder for network sharing through Advanced Sharing.

I allowed `Authenticated Users` with Full Control at the share-permission layer, leaving detailed access restrictions to NTFS permissions.

### 3. Configure NTFS Permissions

I opened the folder's Advanced Security Settings and disabled permission inheritance by converting inherited permissions into explicit permissions.

I reviewed broad permission entries and removed entries that would grant unintended access, while retaining essential administrative and system permissions.

I added the `Sales-Team` security group and assigned Modify permission.

**Intended access model:**
- Administrators: retain administrative access.
- SYSTEM: retain system access.
- Sales-Team: Modify permission.
- Other users: no access through the configured permissions.

### 4. Connect Group Membership to Folder Access

The lab builds on the previous user and group exercise:

`jsmith` → member of `Sales-Team` → `Sales` folder

This demonstrates group-based access management. Administrators can manage resource access by updating group membership rather than assigning folder permissions separately to every user.

## Key Concepts Learned

**Share permissions:** Control access through a network share.

**NTFS permissions:** Control access to files and folders, including permissions such as Read, Modify, and Full Control.

**Permission inheritance:** Allows child folders and files to inherit permissions from their parent unless inheritance is changed.

**Security groups:** Provide a centralized way to assign and manage access to resources.

**Least privilege:** Grant only the access required for a user's job responsibilities.

**Effective permissions:** Actual access depends on applicable share permissions, NTFS permissions, group memberships, and other security rules.

## Troubleshooting Notes

Common causes of shared-folder access problems include:

- The user is not a member of the required security group.
- The share permissions restrict access.
- NTFS permissions do not grant the required access.
- Inherited permissions grant broader access than intended.
- The user has not refreshed their logon session after a group-membership change.

## Validation and Evidence

I added screenshots after completing and verifying the configuration:

