# AZ-104 Lab 01: Microsoft Entra ID Identity Management

##  Project Overview

This project implements **Identity and Access Management (IAM)** using Microsoft Entra ID (formerly Azure AD). It demonstrates:

- Creation of internal and guest user accounts
- Security group configuration with assigned membership
- Group ownership delegation
- Infrastructure as Code (IaC) using Bicep
- Mandatory cleanup phase to prevent resource drift and unnecessary spend

##  Security Focus (CompTIA Security+ Alignment)

This lab directly addresses several **CompTIA Security+ SY0-701** objectives:

| Security+ Domain | How This Lab Applies It |
|-----------------|-------------------------|
| **3.2** – Identity and access management | Creation of user accounts with least privilege |
| **3.4** – Authentication and authorization | Password policies and guest user invitations |
| **3.5** – Identity and access services | Security groups for role-based access control (RBAC) |
| **3.8** – Account management best practices | Owner delegation and group membership controls |

**Key security principles demonstrated:**
-  **Least privilege** – Users get only the access their group provides
-  **Separation of duties** – Group owners can manage members without tenant admin rights
-  **Account lifecycle management** – Users can be created, modified, and deleted via code
-  **External identity governance** – Guest users have restricted user type `Guest`

##  Technologies Used

| Technology | Purpose |
|------------|---------|
| **Microsoft Entra ID** | Cloud identity and access management |
| **Bicep** | Infrastructure as Code language |
| **Microsoft Graph API** | Programmatic access to Entra ID resources |
| **Azure CLI** | Deployment and management |
| **GitHub** | Version control and project documentation |

##  What This Lab Creates

| Resource Type | Name | Purpose |
|--------------|------|---------|
| Internal User | `az104-user1` | IT Lab Administrator (employee) |
| Guest User | `guest_[email]#EXT#@tenant.onmicrosoft.com` | External collaborator |
| Security Group | `IT Lab Administrators` | Role-based access group |
| Group Membership | Both users added | Access control enforcement |
| Group Owner | Your admin account | Delegated group management |

##  How to Deploy

### Prerequisites

- Azure subscription
- Azure CLI installed (`az --version`)
- Microsoft Entra ID permissions (User Administrator or Global Admin)

### Deployment Steps

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/AZ-104-EntraID-Lab.git
cd AZ-104-EntraID-Lab

# 2. Log into Azure
az login

# 3. Create a temporary resource group (required for Bicep deployment context)
az group create --name TempForLab01 --location eastus

# 4. Deploy the Bicep template
az deployment group create \
  --resource-group TempForLab01 \
  --template-file main.bicep

# 5. Verify deployment (see screenshots below)

# 6. Clean up resources when done
# Delete users and groups via portal or remove the resource group
