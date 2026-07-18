# Deployment Guide

# Secure Azure Enterprise Environment

| Document Information | |
|----------------------|--------------------------------|
| Project | Secure Azure Enterprise Environment |
| Organization | Contoso Health Services (Fictional) |
| Cloud Platform | Microsoft Azure |
| Document Type | Deployment Guide |
| Version | 1.0 |
| Status | Completed |
| Author | Manyo Sampson |
| Last Updated | July 2026 |

# Revision History

| Version | Date | Author | Description |
|----------|------|---------|-------------|
| 1.0 | July 2026 | Manyo Sampson | Initial Deployment Guide |

# Table of Contents

1. Introduction
2. Deployment Objectives
3. Solution Overview
4. Deployment Prerequisites
5. Azure Environment
6. Resource Naming Convention
7. Deployment Sequence
8. Phase 1 – Azure Foundation
9. Phase 2 – Virtual Network
10. Phase 3 – Network Security Groups

# 1. Introduction

## Purpose

This document provides a detailed record of the deployment process for the **Secure Azure Enterprise Environment**.

It describes the sequence followed to provision Azure resources, the configuration decisions made during implementation, and the validation performed after deployment.

The guide serves as both implementation documentation and a reference for reproducing a similar secure Azure landing zone using Microsoft Azure services.

# 2. Deployment Objectives

The deployment was designed to achieve the following objectives:

- Establish a secure Azure foundation.
- Deploy Azure networking components.
- Secure Azure Storage.
- Deploy Azure Key Vault.
- Implement Azure RBAC.
- Configure Azure Private Endpoints.
- Disable unnecessary public network access.
- Validate all deployed resources.

# 3. Solution Overview

The deployment followed a phased approach to ensure that dependencies were created in the correct order.

Each phase built upon the previous one, reducing deployment errors and simplifying validation.

The deployment sequence consisted of:

1. Azure Foundation
2. Virtual Network
3. Network Security Groups
4. Azure Storage
5. Storage Private Endpoint
6. Azure Key Vault
7. Azure RBAC
8. Key Vault Secret
9. Key Vault Private Endpoint
10. Validation

# 4. Deployment Prerequisites

Before deployment began, the following prerequisites were verified.

## Azure Subscription

An active Azure subscription was available.

## Azure Permissions

The deployment account had sufficient permissions to create Azure resources.

Owner permissions were available throughout the implementation.

## Azure Resource Provider

The required Azure resource providers were registered and available.

Examples include:

- Microsoft.Network
- Microsoft.Storage
- Microsoft.KeyVault

## Azure Region

All resources were deployed within the same Azure region to simplify management and reduce latency.

# 5. Azure Environment

The project was implemented within a single Azure subscription.

Resources were grouped inside a dedicated Resource Group to simplify administration and lifecycle management.

The deployment environment consisted entirely of Azure-native Platform-as-a-Service (PaaS) resources.

No virtual machines were deployed as part of this implementation.

# 6. Resource Naming Convention

Consistent naming standards were applied to all deployed resources.

| Resource | Example |
|----------|---------|
| Resource Group | rg-contoso-prod-001 |
| Virtual Network | vnet-contoso-prod-001 |
| Storage Account | *(Insert Storage Account Name)* |
| Key Vault | kv-contoso-prod-001 |
| Network Security Group | nsg-management-prod-001 |

The naming convention improves readability, administration, and long-term maintainability.

# 7. Deployment Sequence

The environment was deployed in the following order.

| Phase | Component | Status |
|---------|-----------|--------|
| Phase 1 | Resource Group | ✅ |
| Phase 2 | Virtual Network | ✅ |
| Phase 3 | Network Security Groups | ✅ |
| Phase 4 | Azure Storage Account | ✅ |
| Phase 5 | Storage Private Endpoint | ✅ |
| Phase 6 | Azure Key Vault | ✅ |
| Phase 7 | Azure RBAC | ✅ |
| Phase 8 | Secret Creation | ✅ |
| Phase 9 | Key Vault Private Endpoint | ✅ |
| Phase 10 | Validation | ✅ |

Following this sequence ensured that dependencies such as the Virtual Network and Resource Group were available before dependent resources were created.

# 8. Phase 1 – Azure Foundation

## Objective

Create the foundational Azure resources required for the environment.

## Resources Deployed

- Azure Resource Group

## Configuration

A dedicated Resource Group was created to logically organize all project resources.

Resource tags were also applied to improve governance and resource management.

## Validation

The following checks were completed:

- Resource Group successfully created.
- Tags verified.
- Deployment completed without errors.

**Status:** ✅ Completed

# 9. Phase 2 – Azure Virtual Network

## Objective

Deploy the secure Azure Virtual Network that will host all networking components.

## Resources Deployed

- Azure Virtual Network
- Management Subnet
- Application Subnet
- Data Subnet
- Private Endpoint Subnet

## Configuration

A Virtual Network was created using the **10.1.0.0/16** address space.

Four dedicated subnets were configured to separate workloads according to their function.

The subnet design supports future expansion while maintaining network isolation.

## Validation

The following checks were completed:

- Virtual Network deployed successfully.
- Address space verified.
- Four subnets created.
- Subnet configuration reviewed.

**Status:** ✅ Completed

# 10. Phase 3 – Network Security Groups

## Objective

Protect the network by implementing subnet-level traffic filtering.

## Resources Deployed

- Management NSG
- Application NSG
- Data NSG

## Configuration

Each Network Security Group was associated with its respective subnet.

This approach enables independent traffic control and supports Microsoft's defense-in-depth strategy.

## Validation

The following checks were completed:

- Management NSG associated successfully.
- Application NSG associated successfully.
- Data NSG associated successfully.
- Azure portal verification completed.

**Status:** ✅ Completed

# 11. Phase 4 – Azure Storage Account

## Objective

Deploy a secure Azure Storage Account to provide protected cloud storage while implementing Microsoft's recommended security controls.

## Resources Deployed

- Azure Storage Account

## Configuration

The Storage Account was configured using Azure's recommended security settings.

### Security Settings

| Setting | Configuration |
|----------|--------------|
| Secure Transfer Required | Enabled |
| Encryption at Rest | Enabled |
| Public Network Access | Enabled Initially |
| Storage Account Kind | General Purpose v2 |
| Performance Tier | Standard |

Encryption was enabled using Azure-managed keys to protect data stored within the account.

## Validation

The following checks were completed:

- Storage Account deployed successfully.
- Encryption verified.
- Storage Account accessible.
- Configuration reviewed.

**Status:** ✅ Completed

# 12. Phase 5 – Storage Private Endpoint

## Objective

Provide private connectivity to Azure Storage using Azure Private Link.

## Resources Deployed

- Storage Private Endpoint
- Private DNS Integration

## Configuration

A Private Endpoint was created within the dedicated Private Endpoint subnet.

The endpoint was connected to the Azure Storage Account and integrated with Private DNS.

This configuration allows resources within the Virtual Network to access Storage through a private IP address.

## Security Benefits

- Eliminates public internet communication.
- Reduces attack surface.
- Supports Zero Trust networking.
- Improves network isolation.

## Validation

The following checks were completed:

- Private Endpoint created successfully.
- Private DNS configured.
- Private connection approved.
- Azure portal verification completed.

## Public Access Configuration

After validating Private Endpoint functionality, public network access was disabled for the Storage Account.

This ensured that Storage could only be accessed through approved private network paths.

**Status:** ✅ Completed

# 13. Phase 6 – Azure Key Vault

## Objective

Deploy Azure Key Vault to securely store application secrets and sensitive configuration information.

## Resources Deployed

- Azure Key Vault

## Configuration

Azure Key Vault was deployed using Azure RBAC as the authorization model.

### Key Vault Security Configuration

| Setting | Configuration |
|----------|--------------|
| Authorization Model | Azure RBAC |
| Public Network Access | Enabled Initially |
| Soft Delete | Enabled |
| Purge Protection | Default Azure Configuration |

Azure RBAC was selected to align with Microsoft's modern identity and access management recommendations.

## Validation

The following checks were completed:

- Key Vault deployed successfully.
- Azure RBAC enabled.
- Key Vault accessible.
- Configuration verified.

**Status:** ✅ Completed

# 14. Phase 7 – Azure RBAC Configuration

## Objective

Implement role-based access control for Azure Key Vault administration.

## Configuration

The following Azure RBAC role assignment was configured:

| Role | Purpose |
|--------|----------|
| Key Vault Administrator | Full administrative management of Key Vault |

This assignment allows authorized administrators to manage secrets and Key Vault configuration without granting unnecessary permissions elsewhere in the environment.

## Security Benefits

- Centralized authorization
- Least-privilege access
- Improved governance
- Simplified administration

## Validation

The following checks were completed:

- Role assignment created successfully.
- Permissions verified.
- Administrative access confirmed.

**Status:** ✅ Completed

# 15. Deployment Challenge – Key Vault Firewall Issue

## Overview

During the implementation of Azure Key Vault networking controls, an issue occurred while attempting to update the Key Vault firewall configuration.

## Error Message

The following error was recorded within Azure Activity Logs:

```json
{
  "error": {
    "code": "BadRequest",
    "message": "Invalid value found at properties.networkAcls.ipRules[0].value: 172.20.10.5/32 belongs to forbidden range 172.16.0.0–172.31.255.255 (private IP addresses)"
  }
}
```

## Root Cause

A private IPv4 address was mistakenly supplied when attempting to add a client IP address to the Key Vault firewall configuration.

Azure Key Vault firewall rules only support public IPv4 addresses.

Private RFC1918 addresses cannot be added to Key Vault firewall allow lists.

## Investigation

Troubleshooting involved:

- Reviewing Azure Activity Logs.
- Examining Key Vault networking settings.
- Validating Azure RBAC permissions.
- Reviewing Resource Provider registration.
- Verifying firewall configuration settings.

## Resolution

The private IP address was removed and replaced with the administrator's public IPv4 address.

After updating the firewall configuration:

- Key Vault access was restored.
- Networking configuration completed successfully.
- Secret management functionality was verified.

## Lessons Learned

This issue reinforced several important concepts:

- Azure Activity Logs are valuable troubleshooting tools.
- Public and private IP addresses serve different purposes.
- Azure Key Vault firewall rules only support public IP addresses.
- Proper network validation is essential before applying security controls.

# 16. Phase 8 – Secret Creation

## Objective

Validate Azure Key Vault functionality by securely storing a secret.

## Configuration

A test secret was created within Azure Key Vault.

The successful creation of the secret confirmed:

- Azure RBAC functionality.
- Key Vault accessibility.
- Administrative permissions.
- Operational readiness.

## Validation

The following checks were completed:

- Secret created successfully.
- Secret stored securely.
- Secret visible within Key Vault.
- RBAC permissions functioning correctly.

**Status:** ✅ Completed

# 17. Phase 9 – Key Vault Private Endpoint

## Objective

Secure Azure Key Vault through Azure Private Link.

## Resources Deployed

- Key Vault Private Endpoint
- Private DNS Integration

## Configuration

A Private Endpoint was deployed within the Private Endpoint subnet and connected to Azure Key Vault.

Private DNS integration was configured to support internal name resolution.

## Security Benefits

- Removes dependency on public internet access.
- Supports Zero Trust networking.
- Reduces attack surface.
- Improves network isolation.

## Validation

The following checks were completed:

- Private Endpoint deployed successfully.
- Private DNS integration verified.
- Key Vault accessible through private connectivity.
- Azure portal validation completed.

## Public Access Configuration

After validating private connectivity, public network access was disabled for Azure Key Vault.

This ensured that Key Vault could only be accessed through approved private communication paths.

**Status:** ✅ Completed

# 18. Phase 10 – Deployment Validation

## Objective

Perform a comprehensive validation of the deployed Azure environment to ensure that all planned resources were successfully provisioned, configured, and secured.

The validation process confirmed that the environment was operational and aligned with the project objectives.

## Infrastructure Validation

The following infrastructure components were verified.

| Component | Validation Result |
|-----------|-------------------|
| Resource Group | ✅ Successfully Created |
| Virtual Network | ✅ Successfully Created |
| Management Subnet | ✅ Verified |
| Application Subnet | ✅ Verified |
| Data Subnet | ✅ Verified |
| Private Endpoint Subnet | ✅ Verified |
| Management NSG | ✅ Associated Successfully |
| Application NSG | ✅ Associated Successfully |
| Data NSG | ✅ Associated Successfully |

## Platform Services Validation

| Azure Service | Validation Result |
|---------------|-------------------|
| Azure Storage Account | ✅ Successfully Deployed |
| Storage Private Endpoint | ✅ Operational |
| Azure Key Vault | ✅ Successfully Deployed |
| Key Vault Private Endpoint | ✅ Operational |
| Private DNS Zones | ✅ Successfully Configured |

## Security Validation

The following security controls were verified.

| Security Control | Status |
|------------------|--------|
| Azure RBAC | ✅ Configured |
| Key Vault Administrator Role | ✅ Assigned |
| Encryption at Rest | ✅ Enabled |
| Secure Transfer Required | ✅ Enabled |
| Storage Public Network Access Disabled | ✅ Confirmed |
| Key Vault Public Network Access Disabled | ✅ Confirmed |
| Secret Successfully Created | ✅ Verified |

## Connectivity Validation

The following connectivity checks were completed.

- Azure Storage accessible through Private Endpoint.
- Azure Key Vault accessible through Private Endpoint.
- Private DNS resolution functioning correctly.
- Azure resources successfully communicating through private connectivity.

## Deployment Outcome

All planned deployment objectives were successfully achieved.

The Azure environment is fully operational and provides a secure foundation for future cloud workloads.

# 19. Security Verification Checklist

The environment was reviewed against Microsoft's recommended cloud security practices.

| Control | Status |
|----------|--------|
| Dedicated Resource Group | ✅ |
| Azure Virtual Network Implemented | ✅ |
| Network Segmentation | ✅ |
| Network Security Groups Configured | ✅ |
| Azure Storage Encryption Enabled | ✅ |
| Azure Key Vault Implemented | ✅ |
| Azure RBAC Enabled | ✅ |
| Secrets Stored Securely | ✅ |
| Azure Private Link Implemented | ✅ |
| Private DNS Configured | ✅ |
| Public Network Access Disabled | ✅ |

The completed checklist demonstrates that multiple Azure-native security controls were successfully implemented.

# 20. Deployment Summary

The project followed a structured deployment approach that emphasized security, proper resource organization, and private connectivity.

### Azure Foundation

- Resource Group created
- Resource tags applied

### Networking

- Virtual Network deployed
- Four dedicated subnets created
- Network Security Groups associated

### Storage

- Azure Storage Account deployed
- Storage secured using Private Endpoint
- Public network access disabled

### Identity & Secrets

- Azure Key Vault deployed
- Azure RBAC configured
- Key Vault Administrator role assigned
- Test secret created successfully

### Private Connectivity

- Storage Private Endpoint deployed
- Key Vault Private Endpoint deployed
- Private DNS integrated

### Validation

- Infrastructure verified
- Security controls validated
- Connectivity confirmed

# 21. Lessons Learned

This project provided valuable hands-on experience with Azure networking and cloud security.

## Security by Design

Security should be incorporated during the planning and deployment stages rather than added after infrastructure has been provisioned.

## Importance of Network Segmentation

Separating workloads into dedicated subnets improves security, simplifies administration, and limits the impact of potential security incidents.

## Azure Private Link

Azure Private Link provides an effective method for securing Azure platform services by eliminating unnecessary public exposure.

## Azure RBAC

Role-Based Access Control simplifies permission management while supporting the principle of least privilege.

## Troubleshooting Azure

Resolving the Key Vault firewall issue reinforced the importance of:

- Reviewing Azure Activity Logs.
- Understanding Azure networking concepts.
- Distinguishing between private and public IP addresses.
- Validating security configurations before deployment.

## Documentation

Maintaining accurate technical documentation is as important as deploying the infrastructure itself.

Well-structured documentation supports knowledge sharing, troubleshooting, and long-term maintenance.

# 22. Future Enhancements

This deployment establishes a secure Azure foundation that can be expanded in future phases.

Potential enhancements include:

- Azure Firewall
- Azure Bastion
- Azure Monitor
- Log Analytics Workspace
- Microsoft Defender for Cloud
- Azure Backup
- Azure Policy
- Azure Virtual Machines
- Azure SQL Database
- Azure Application Gateway

These services were intentionally excluded from the current implementation to keep the project focused on foundational networking and security.

# 23. Conclusion

The Secure Azure Enterprise Environment was successfully deployed using Microsoft Azure and demonstrates the implementation of a secure cloud foundation based on Microsoft's recommended architecture and security practices.

The project incorporated secure networking, identity and access management, private connectivity, encryption, and centralized secret management to reduce the attack surface and protect sensitive resources.

By combining Azure Virtual Network, Network Security Groups, Azure Storage, Azure Key Vault, Azure Private Link, Private DNS, and Azure RBAC, the environment reflects a practical implementation of Microsoft's Defense-in-Depth and Zero Trust security principles.

This deployment serves as a strong foundation for future cloud workloads and demonstrates practical experience in designing, implementing, securing, and validating Azure infrastructure.

# References

This deployment was implemented using Microsoft's official documentation and best practices.

- Microsoft Learn
- Azure Architecture Center
- Azure Well-Architected Framework
- Azure Security Benchmark
- Azure Virtual Network Documentation
- Azure Network Security Groups Documentation
- Azure Private Link Documentation
- Azure Storage Documentation
- Azure Key Vault Documentation
- Azure RBAC Documentation

# Appendix A – Deployment Timeline

| Phase | Status |
|--------|--------|
| Azure Foundation | ✅ Completed |
| Virtual Network | ✅ Completed |
| Network Security Groups | ✅ Completed |
| Azure Storage | ✅ Completed |
| Storage Private Endpoint | ✅ Completed |
| Azure Key Vault | ✅ Completed |
| Azure RBAC | ✅ Completed |
| Secret Creation | ✅ Completed |
| Key Vault Private Endpoint | ✅ Completed |
| Validation | ✅ Completed |


# Appendix B – Acronyms

| Acronym | Meaning |
|----------|---------|
| VNet | Virtual Network |
| NSG | Network Security Group |
| RBAC | Role-Based Access Control |
| DNS | Domain Name System |
| PE | Private Endpoint |
| ARM | Azure Resource Manager |
| PaaS | Platform as a Service |
| IAM | Identity and Access Management |
| RFC | Request for Comments |
