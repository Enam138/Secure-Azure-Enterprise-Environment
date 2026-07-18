# Security Configuration Guide

# Secure Azure Enterprise Environment

| Document Information | |
|----------------------|--------------------------------|
| Project | Secure Azure Enterprise Environment |
| Organization | Contoso Health Services (Fictional) |
| Cloud Platform | Microsoft Azure |
| Document Type | Security Configuration Guide |
| Version | 1.0 |
| Status | Completed |
| Author | Manyo Sampson |
| Last Updated | July 2026 |

# Revision History

| Version | Date | Author | Description |
|----------|------|---------|-------------|
| 1.0 | July 2026 | Manyo Sampson | Initial Security Configuration Guide |

# Table of Contents

1. Introduction
2. Security Objectives
3. Security Principles
4. Security Architecture Overview
5. Identity and Access Management
6. Network Security
7. References

# 1. Introduction

## Purpose

This document describes the security controls implemented within the Secure Azure Enterprise Environment.

The objective is to document how Microsoft Azure native security services were configured to protect cloud resources against unauthorized access while supporting secure communication, centralized identity management, and defense-in-depth.

The implemented controls follow Microsoft's cloud security recommendations and establish a secure foundation for future Azure workloads.

# 2. Security Objectives

The security architecture was designed to achieve the following objectives.

- Protect Azure resources from unauthorized access.
- Reduce exposure to the public internet.
- Implement identity-based authorization.
- Secure sensitive information.
- Enable encrypted communication.
- Support Zero Trust principles.
- Apply Microsoft's defense-in-depth strategy.
- Improve governance and administrative control.

# 3. Security Principles

The environment follows several core security principles.

## Security by Design

Security controls were incorporated during deployment rather than added after infrastructure provisioning.

Examples include:

- Network segmentation
- Azure RBAC
- Private Endpoints
- Encryption

## Least Privilege

Administrative permissions are granted using Azure Role-Based Access Control.

Only authorized identities receive permissions necessary to perform their assigned responsibilities.

## Defense in Depth

Multiple security layers work together to reduce organizational risk.

The architecture combines:

- Microsoft Entra ID
- Azure RBAC
- Azure Virtual Network
- Network Security Groups
- Azure Private Endpoints
- Azure Key Vault
- Azure Storage Encryption

## Zero Trust

The environment assumes that no user, device, or network location should be trusted automatically.

Authentication, authorization, and secure connectivity are required before access is granted.

# 4. Security Architecture Overview

The implemented environment consists of several complementary security layers.

```
                                           Administrator

                                                ↓

                                        Microsoft Entra ID

                                                 ↓

                                             Azure RBAC

                                                 ↓

                                       Azure Virtual Network

                                                 ↓

                                        Network Security Groups

                                                 ↓

                                          Private Endpoints

                                                 ↓

                                           Azure Storage
                                          Azure Key Vault
```

Each layer provides independent protection against unauthorized access.

No single security control is relied upon exclusively.

# 5. Identity and Access Management

## Microsoft Entra ID

Microsoft Entra ID provides centralized identity management for Azure resources.

Authentication is performed before access is granted to Azure services.

Benefits include:

- Centralized authentication
- Identity lifecycle management
- Integration with Azure services
- Secure administrator access

## Azure Role-Based Access Control (RBAC)

Azure RBAC was selected as the authorization model for Azure Key Vault.

Role assignments determine what authenticated users are permitted to do after successful sign-in.

## Configured Role

| Role | Purpose |
|------|----------|
| Key Vault Administrator | Manage Key Vault configuration and secrets |

## Security Benefits

- Least privilege
- Centralized authorization
- Simplified administration
- Improved governance

## Identity Security Flow

```
                                             Administrator

                                                   ↓

                                      Microsoft Entra ID Authentication

                                                    ↓

                                           Azure RBAC Authorization
 
                                                    ↓

                                              Azure Resource
```

Authentication and authorization remain separate processes, improving security and operational flexibility.

# 6. Network Security

## Azure Virtual Network

The Virtual Network establishes the secure communication boundary for all deployed Azure resources.

All network communication occurs within this controlled environment unless explicitly permitted.

## Network Segmentation

Four dedicated subnets were created.

| Subnet | Purpose |
|---------|----------|
| Management | Administrative resources |
| Application | Business workloads |
| Data | Backend services |
| Private Endpoint | Azure Private Link |

Separating workloads into dedicated subnets reduces lateral movement and simplifies policy enforcement.

## Network Security Groups

Dedicated Network Security Groups were associated with the Management, Application, and Data subnets.

These NSGs provide subnet-level traffic filtering and strengthen network isolation.

## Security Benefits

- Traffic filtering
- Network isolation
- Reduced attack surface
- Defense in depth
- Administrative simplicity

# 7. Azure Storage Security Configuration

## Overview

Azure Storage was configured using Microsoft's recommended security settings to ensure that stored data remains protected against unauthorized access while supporting secure communication within the Azure environment.

Multiple security controls were implemented to protect both the storage account and the data it contains.

## Security Configuration

| Security Setting | Configuration |
|------------------|---------------|
| Secure Transfer Required | Enabled |
| Encryption at Rest | Enabled |
| Encryption Keys | Microsoft-Managed Keys |
| Public Network Access | Disabled |
| Private Endpoint | Configured |
| Private DNS | Configured |

## Secure Transfer

Secure Transfer was enabled to require encrypted communication using HTTPS.

This prevents clients from connecting over unencrypted protocols and protects data while it is transmitted.

### Benefits

- Protects data in transit
- Prevents insecure connections
- Supports industry security standards

## Encryption at Rest

Azure Storage automatically encrypts all stored data using Microsoft-managed encryption keys.

Encryption at rest helps protect sensitive information if physical storage media were ever compromised.

### Benefits

- Automatic encryption
- No application changes required
- Transparent to users
- Meets Microsoft's recommended security baseline

## Private Endpoint Integration

Azure Storage communicates through a Private Endpoint deployed within the Azure Virtual Network.

This ensures that traffic remains on Microsoft's private backbone instead of traversing the public internet.

### Benefits

- Reduced attack surface
- Private connectivity
- Improved network security
- Better compliance with Zero Trust principles

## Public Network Access

After validating the Private Endpoint, public network access to the Storage Account was disabled.

As a result, access is restricted to approved private communication paths within the Azure Virtual Network.

# 8. Azure Key Vault Security Configuration

## Overview

Azure Key Vault provides centralized and secure storage for sensitive information such as application secrets.

The service reduces the risk associated with storing secrets directly within application code or configuration files.

## Security Configuration

| Security Setting | Configuration |
|------------------|---------------|
| Authorization Model | Azure RBAC |
| Private Endpoint | Configured |
| Private DNS | Configured |
| Public Network Access | Disabled |
| Secret Storage | Enabled |

## Azure RBAC Authorization

The Key Vault was configured to use Azure Role-Based Access Control (RBAC) instead of the legacy access policy model.

Azure RBAC centralizes authorization and supports consistent permission management across Azure resources.

### Benefits

- Centralized permission management
- Improved governance
- Least-privilege administration
- Integration with Microsoft Entra ID

## Secret Management

A test secret was successfully created to validate Key Vault functionality.

The successful creation confirmed:

- Administrative permissions
- Azure RBAC functionality
- Key Vault availability
- Operational readiness

Secrets remain encrypted and accessible only to authorized identities.

## Private Endpoint

A dedicated Private Endpoint was deployed for Azure Key Vault.

This configuration removes dependency on public network communication and ensures secure access through the Azure Virtual Network.

## Public Network Access

After verifying successful private connectivity, public network access was disabled.

This significantly reduces exposure to internet-based attacks.

# 9. Private Endpoint Security

## Overview

Azure Private Link was implemented to provide secure communication between Azure resources and Azure platform services.

Unlike traditional public endpoints, Private Endpoints assign private IP addresses within the Azure Virtual Network.

## Implemented Private Endpoints

| Azure Service | Status |
|---------------|--------|
| Azure Storage | ✅ |
| Azure Key Vault | ✅ |

## Security Advantages

Private Endpoints provide several important security benefits.

- Removes public exposure
- Supports Zero Trust networking
- Improves workload isolation
- Keeps traffic on Microsoft's private backbone
- Reduces attack surface

## Private Communication Flow

```text
                                                                      Azure Resource

                                                                             ↓

                                                                    Azure Virtual Network

                                                                              ↓

                                                                       Private Endpoint

                                                                              ↓

                                                                     Azure Platform Service
```

No communication occurs over the public internet.

# 10. Private DNS Configuration

## Overview

Private DNS Zones were configured to support secure name resolution for Azure Storage and Azure Key Vault.

Instead of resolving public service addresses, DNS queries return private IP addresses associated with the deployed Private Endpoints.

## Configured Private DNS

| Service | Status |
|----------|--------|
| Azure Storage | ✅ |
| Azure Key Vault | ✅ |

## Benefits

- Automatic DNS resolution
- Simplified administration
- Reliable private connectivity
- Reduced configuration complexity

# 11. Encryption

## Data at Rest

Azure Storage encrypts all stored data using Microsoft-managed encryption keys.

Azure Key Vault also encrypts stored secrets before they are written to storage.

## Data in Transit

Secure communication is protected using HTTPS.

Combined with Private Endpoints, encrypted traffic remains within Microsoft's private network.

## Encryption Summary

| Area | Protection |
|------|------------|
| Data at Rest | Azure Encryption |
| Data in Transit | HTTPS |
| Secrets | Azure Key Vault Encryption |

Encryption protects sensitive information throughout its lifecycle.

# 12. Public Network Access

One of the primary security objectives of this implementation was to minimize unnecessary public exposure.

Initially, public access remained enabled during deployment and validation.

After confirming that Private Endpoints functioned correctly, public network access was disabled for:

- Azure Storage
- Azure Key Vault

This approach ensured uninterrupted deployment while ultimately enforcing a more secure network posture.

# 13. Security Incident and Resolution

## Overview

During the implementation of Azure Key Vault networking controls, an error occurred while updating the firewall configuration.

## Error

Azure rejected the configured IP address because it belonged to a private RFC1918 address range.

The deployment failed with an error indicating that private IP addresses cannot be used in Key Vault firewall rules.

## Root Cause

A private IP address was mistakenly added to the Key Vault firewall allow list.

Azure Key Vault firewall rules only support public IPv4 addresses.

## Investigation

The issue was investigated by reviewing:

- Azure Activity Logs
- Key Vault networking configuration
- Azure RBAC permissions
- Azure Resource Provider registration
- Firewall settings

## Resolution

The private IP address was removed and replaced with the administrator's public IP address.

After updating the firewall configuration:

- Administrative access was restored.
- Secret creation succeeded.
- Key Vault networking configuration completed successfully.

## Lessons Learned

The incident reinforced several important security concepts.

- Azure firewall rules require public IP addresses.
- Azure Activity Logs simplify troubleshooting.
- Proper validation prevents deployment issues.
- Understanding Azure networking concepts is essential for secure cloud administration.

# 14. Defense-in-Depth Implementation

## Overview

The Secure Azure Enterprise Environment was designed using Microsoft's Defense-in-Depth security strategy.

Rather than depending on a single security control, multiple independent security layers work together to protect cloud resources. If one layer is compromised, additional controls continue to provide protection.

## Security Layers

| Layer | Azure Service | Purpose |
|--------|---------------|---------|
| Identity | Microsoft Entra ID | User authentication |
| Authorization | Azure RBAC | Least-privilege access control |
| Network | Azure Virtual Network | Secure communication boundary |
| Segmentation | Dedicated Subnets | Workload isolation |
| Traffic Filtering | Network Security Groups | Control inbound and outbound traffic |
| Private Connectivity | Azure Private Link | Secure communication with Azure services |
| Name Resolution | Private DNS Zones | Secure internal DNS resolution |
| Data Protection | Azure Storage Encryption | Protect stored data |
| Secret Management | Azure Key Vault | Secure storage of sensitive information |

## Security Model

```text
                                                                               Administrator
                                                                                     │
                                                                                     ▼
                                                                              Microsoft Entra ID
                                                                              (Authentication)
                                                                                     │
                                                                                     ▼
                                                                                Azure RBAC
                                                                              (Authorization)
                                                                                     │
                                                                                     ▼
                                                                            Azure Virtual Network
                                                                                     │
                                                                                     ▼
                                                                          Network Security Groups
                                                                                     │
                                                                                     ▼
                                                                              Private Endpoints
                                                                                     │
                                                                                     ▼
                                                                       Azure Storage / Azure Key Vault
```

Each layer contributes independently to the overall security posture of the environment.

# 15. Zero Trust Implementation

## Overview

The deployed environment aligns with Microsoft's Zero Trust security model.

Zero Trust assumes that no user, device, or network should be trusted automatically. Every request must be authenticated, authorized, and validated before access is granted.

## Zero Trust Principles

### Verify Explicitly

Every administrative action requires authentication through Microsoft Entra ID.

### Use Least Privilege

Azure RBAC ensures permissions are assigned based on roles rather than unrestricted administrative access.

The Key Vault Administrator role provides only the permissions required to manage Azure Key Vault resources.

### Assume Breach

The network architecture assumes that a compromise is always possible.

To reduce risk, the environment includes:

- Dedicated subnets
- Network Security Groups
- Private Endpoints
- Disabled public network access

These controls help reduce lateral movement and limit potential exposure.

## Zero Trust Summary

| Principle | Implementation |
|------------|----------------|
| Verify Explicitly | Microsoft Entra ID |
| Use Least Privilege | Azure RBAC |
| Assume Breach | Network Segmentation |
| Secure Resources | Private Endpoints |
| Protect Data | Encryption & Key Vault |

# 16. Security Validation

The implemented security controls were validated after deployment.

## Identity Validation

| Validation | Status |
|------------|--------|
| Microsoft Entra ID Authentication | ✅ |
| Azure RBAC Enabled | ✅ |
| Key Vault Administrator Assigned | ✅ |

## Network Validation

| Validation | Status |
|------------|--------|
| Azure Virtual Network | ✅ |
| Four Subnets | ✅ |
| Network Security Groups | ✅ |
| Private Endpoint Subnet | ✅ |

## Storage Validation

| Validation | Status |
|------------|--------|
| Encryption Enabled | ✅ |
| Secure Transfer Enabled | ✅ |
| Private Endpoint Operational | ✅ |
| Public Access Disabled | ✅ |

## Key Vault Validation

| Validation | Status |
|------------|--------|
| Key Vault Operational | ✅ |
| Secret Created Successfully | ✅ |
| Private Endpoint Operational | ✅ |
| Public Access Disabled | ✅ |

## DNS Validation

| Validation | Status |
|------------|--------|
| Storage Private DNS | ✅ |
| Key Vault Private DNS | ✅ |

# 17. Security Best Practices Applied

The following Microsoft security best practices were implemented throughout the project.

### Identity

- Microsoft Entra ID authentication
- Azure RBAC authorization
- Least-privilege permissions

### Networking

- Dedicated Azure Virtual Network
- Network segmentation
- Network Security Groups
- Private Endpoints

### Data Protection

- Encryption at rest
- HTTPS communication
- Azure Key Vault secret management

### Governance

- Resource Group organization
- Resource tagging
- Consistent naming standards

### Exposure Reduction

- Public network access disabled
- Private DNS configured
- Azure platform services accessible through Private Link

# 18. Security Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| Unauthorized administrative access | High | Microsoft Entra ID and Azure RBAC |
| Public exposure of Azure services | High | Private Endpoints and disabled public access |
| Secret compromise | High | Azure Key Vault |
| Lateral movement | Medium | Network segmentation |
| Unauthorized network communication | Medium | Network Security Groups |
| Data exposure | High | Encryption at rest and secure transfer |

The implemented controls significantly reduce these risks and strengthen the overall security posture of the environment.

# 19. Compliance Alignment

Although this project was not designed to achieve formal compliance certification, the implemented controls align with widely accepted cloud security practices.

The environment demonstrates alignment with:

- Microsoft Azure Security Benchmark
- Microsoft Zero Trust guidance
- Azure Well-Architected Framework (Security Pillar)
- Microsoft Identity Security recommendations

These practices provide a strong foundation for securing enterprise Azure environments.

# 20. Lessons Learned

Implementing this environment reinforced several important cloud security concepts.

### Identity Is the First Security Layer

Authentication and authorization should always be enforced before access to Azure resources is granted.

### Private Connectivity Improves Security

Azure Private Link significantly reduces exposure by allowing communication to remain on Microsoft's private network.

### Least Privilege Reduces Risk

Azure RBAC simplifies permission management while minimizing excessive administrative privileges.

### Encryption Should Be Enabled by Default

Azure-managed encryption protects sensitive information without increasing operational complexity.

### Troubleshooting Is Part of Security

Resolving the Key Vault firewall issue highlighted the importance of:

- Reviewing Azure Activity Logs
- Understanding firewall configuration
- Distinguishing between public and private IP addresses
- Validating networking settings before deployment

# 21. Conclusion

The Secure Azure Enterprise Environment demonstrates the implementation of a layered cloud security architecture using Microsoft Azure native services.

The environment integrates Microsoft Entra ID, Azure RBAC, Azure Virtual Network, Network Security Groups, Azure Storage, Azure Key Vault, Azure Private Link, Private DNS, and encryption to establish a secure and scalable cloud foundation.

The implemented controls align with Microsoft's Zero Trust principles and Defense-in-Depth strategy while reducing the attack surface through private connectivity and least-privilege access.

This security configuration provides a practical example of how Azure-native services can be combined to protect enterprise workloads and sensitive information.

# References

The security configuration was implemented using Microsoft's official guidance and documentation.

- Microsoft Learn
- Azure Security Benchmark
- Azure Well-Architected Framework
- Microsoft Zero Trust Guidance
- Microsoft Entra ID Documentation
- Azure RBAC Documentation
- Azure Virtual Network Documentation
- Azure Network Security Groups Documentation
- Azure Private Link Documentation
- Azure Storage Security Documentation
- Azure Key Vault Documentation

# Appendix A – Security Controls Summary

| Security Domain | Azure Service | Status |
|-----------------|---------------|--------|
| Identity | Microsoft Entra ID | ✅ |
| Authorization | Azure RBAC | ✅ |
| Networking | Azure Virtual Network | ✅ |
| Segmentation | Four Dedicated Subnets | ✅ |
| Traffic Filtering | Network Security Groups | ✅ |
| Storage Protection | Azure Storage Encryption | ✅ |
| Secret Management | Azure Key Vault | ✅ |
| Private Connectivity | Azure Private Link | ✅ |
| Name Resolution | Private DNS | ✅ |
| Public Exposure Reduction | Public Network Access Disabled | ✅ |

# Appendix B – Security Validation Checklist

| Security Control | Status |
|------------------|--------|
| Microsoft Entra ID Authentication | ✅ |
| Azure RBAC Configured | ✅ |
| Network Security Groups Associated | ✅ |
| Storage Encryption Enabled | ✅ |
| Secure Transfer Enabled | ✅ |
| Azure Key Vault Operational | ✅ |
| Secret Created | ✅ |
| Private Endpoints Operational | ✅ |
| Private DNS Configured | ✅ |
| Public Network Access Disabled | ✅ |

# Appendix C – Acronyms

| Acronym | Meaning |
|----------|---------|
| RBAC | Role-Based Access Control |
| VNet | Virtual Network |
| NSG | Network Security Group |
| DNS | Domain Name System |
| IAM | Identity and Access Management |
| PE | Private Endpoint |
| PaaS | Platform as a Service |
| ARM | Azure Resource Manager |
| RFC | Request for Comments |
| HTTPS | Hypertext Transfer Protocol Secure |
