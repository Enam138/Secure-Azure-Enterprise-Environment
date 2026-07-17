# Secure-Azure-Enterprise-Environment
Contoso Health Services is a healthcare organization migrating part of its infrastructure to Azure. The company stores sensitive patient records and internal business applications in Azure. The IT Security team has been tasked with designing a secure Azure landing zone that follows Microsoft's Zero Trust principles.

# 🛡️ Secure Azure Enterprise Environment

![Microsoft Azure](https://img.shields.io/badge/Microsoft-Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Azure Security](https://img.shields.io/badge/Azure-Security-0078D4?style=for-the-badge)
![Cloud Security](https://img.shields.io/badge/Cloud-Security-success?style=for-the-badge)
![Zero Trust](https://img.shields.io/badge/Zero-Trust-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)


## Project Overview

**Secure Azure Enterprise Environment** is a hands-on cloud security project that demonstrates how to design and implement a secure Azure landing zone using Microsoft Azure services and Microsoft's recommended security best practices.

The project simulates a real-world enterprise deployment for **Contoso Health Services**, a fictional healthcare organization migrating business-critical workloads to Microsoft Azure. The implementation focuses on establishing a secure cloud foundation through network segmentation, identity-based access control, private connectivity, secure secret management, and data protection.

Rather than simply deploying Azure resources, this project emphasizes **secure architecture**, **governance**, and **Zero Trust principles** to reduce the attack surface and provide a scalable foundation for future cloud workloads.


# Business Scenario

Contoso Health Services is a healthcare organization migrating part of its infrastructure from an on-premises environment to Microsoft Azure.

The organization plans to host:

- Internal business applications
- Patient records
- Secure file storage
- Application secrets
- Future cloud-native workloads

As the Cloud Security Engineer, the objective was to design and implement a secure Azure environment that follows Microsoft's recommended architecture while protecting sensitive healthcare data through identity, networking, and data security controls.


# Objectives

The primary objectives of this project were to:

- Build a secure Azure landing zone
- Implement network segmentation
- Secure Azure Storage using Private Link
- Protect sensitive secrets using Azure Key Vault
- Apply Azure Role-Based Access Control (RBAC)
- Eliminate unnecessary public exposure through Private Endpoints
- Follow Microsoft's Zero Trust security principles
- Gain practical experience with Azure security services


# Solution Architecture

The environment consists of a single Azure subscription containing a production resource group that hosts all infrastructure required for the project.

Resources are deployed inside a segmented Azure Virtual Network consisting of dedicated Management, Application, Data, and Private Endpoint subnets.

Sensitive platform services, including Azure Storage and Azure Key Vault, are accessed exclusively through Azure Private Endpoints, reducing exposure to the public internet.

Azure RBAC is used for authorization, while encryption and secure networking protect sensitive business data.


# Azure Services Used

| Service | Purpose |
|----------|---------|
| Azure Resource Group | Logical resource organization |
| Azure Virtual Network | Secure network foundation |
| Azure Subnets | Network segmentation |
| Network Security Groups | Network traffic filtering |
| Azure Storage Account | Secure cloud storage |
| Azure Private Endpoint | Private connectivity |
| Azure Key Vault | Secret management |
| Azure RBAC | Authorization |
| Azure Activity Log | Monitoring & Troubleshooting |
| Azure Private DNS | Private name resolution |


# Architecture Overview

```
Microsoft Entra ID
        │
Azure RBAC
        │
──────────────────────────────

Azure Subscription

└── Resource Group
    ├── Virtual Network
    │
    ├── Management Subnet
    │      └── NSG
    │
    ├── Application Subnet
    │      └── NSG
    │
    ├── Data Subnet
    │      └── NSG
    │
    └── Private Endpoint Subnet
           ├── Storage Private Endpoint
           └── Key Vault Private Endpoint

Azure Storage
Public Access Disabled

Azure Key Vault
Public Access Disabled
Azure RBAC Enabled
```


# Network Design

| Subnet | Purpose |
|---------|----------|
| Management | Administrative resources |
| Application | Business applications |
| Data | Backend services |
| Private Endpoint | Azure Private Link resources |

This segmented design improves security by separating workloads and reducing unnecessary communication between resources.


# Features Implemented

## Azure Foundation

- Azure Subscription
- Resource Group
- Resource Tagging
- Naming Standards


## Networking

- Azure Virtual Network
- Four Dedicated Subnets
- Network Security Groups
- Network Segmentation


## Storage Security

- Secure Storage Account
- Encryption at Rest
- Private Endpoint
- Public Network Access Disabled


## Azure Key Vault

- Azure RBAC Authorization
- Secure Secret Storage
- Private Endpoint
- Private DNS Integration
- Public Network Access Disabled


# Security Controls

This project implements multiple security layers following Microsoft's defense-in-depth strategy.

## Identity Security

- Azure RBAC
- Least Privilege Access

## Network Security

- Virtual Network
- Subnets
- NSGs
- Private Endpoints
- Private DNS

## Data Protection

- Azure Storage Encryption
- Azure Key Vault
- Secret Management

## Governance

- Resource Tags
- Naming Standards
- Resource Group Organization


# Zero Trust Principles

The project aligns with Microsoft's Zero Trust approach by implementing:

- Verify explicitly through Azure RBAC
- Use least-privilege access
- Minimize public exposure
- Protect sensitive data
- Secure cloud resources by default


# Deployment Summary

The project was completed in the following phases:

| Phase | Description |
|--------|-------------|
| Phase 1 | Azure Foundation |
| Phase 2 | Virtual Networking |
| Phase 3 | Network Security Groups |
| Phase 4 | Azure Storage Security |
| Phase 5 | Azure Key Vault |
| Phase 6 | Private Endpoints & Private DNS |


# Validation

The following items were verified after deployment:

- Resource Group created successfully
- Virtual Network deployed
- Four subnets configured
- NSGs associated correctly
- Storage Account encrypted
- Storage Private Endpoint approved
- Key Vault deployed
- Azure RBAC configured
- Secret created successfully
- Key Vault Private Endpoint approved
- Public network access disabled


# Troubleshooting

During deployment, a networking issue occurred while configuring Azure Key Vault firewall rules.

### Problem

A private IP address was mistakenly added to the Key Vault firewall.

### Root Cause

Azure Key Vault firewall rules only accept public IPv4 addresses.

### Resolution

- Investigated Azure Activity Logs
- Identified invalid firewall rule
- Replaced the private IP with the appropriate public IPv4 address
- Successfully completed deployment

This experience reinforced the importance of using Azure diagnostics to identify and resolve configuration issues.


# Skills Demonstrated

- Microsoft Azure Administration
- Azure Networking
- Azure Virtual Networks
- Network Security Groups
- Azure Storage Security
- Azure Key Vault
- Azure RBAC
- Azure Private Link
- Private DNS
- Cloud Security
- Zero Trust
- Azure Troubleshooting
- Secure Cloud Architecture


# Project Structure

```
Secure-Azure-Enterprise-Environment/
│
├── Architecture/
├── Deployment/
├── Security/
├── Screenshots/
├── Validation/
├── docs/
├── README.md
├── Troubleshooting.md
└── Lesson Learned.md
```

 Lessons Learned

This project reinforced several important cloud security concepts:

- Secure architecture begins with proper planning.
- Network segmentation reduces risk.
- Identity and network security must work together.
- Private Endpoints significantly reduce the attack surface.
- Azure RBAC simplifies secure authorization.
- Azure Activity Logs are essential for troubleshooting.
- Microsoft Zero Trust principles provide a strong security foundation.


# Future Improvements

Future enhancements may include:

- Azure Firewall
- Azure Bastion
- Virtual Machines
- Microsoft Defender for Cloud
- Microsoft Sentinel
- Managed Identities
- Azure Policy
- Azure Backup
- Azure Monitor


# References

This project was implemented using Microsoft's official documentation and security guidance.

- Microsoft Learn
- Azure Well-Architected Framework
- Azure Architecture Center
- Azure Security Benchmark
- Azure Virtual Network Documentation
- Azure Key Vault Documentation
- Azure Private Link Documentation
- Azure RBAC Documentation


# Author

**Manyo Sampson**

Cloud & AI Engineer | Cybersecurity Graduate | Azure Security Enthusiast

If you found this project helpful, consider giving the repository a ⭐.
