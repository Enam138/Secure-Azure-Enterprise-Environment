# Network Design Document

# Secure Azure Enterprise Environment

| Document Information | |
|----------------------|--------------------------------|
| Project | Secure Azure Enterprise Environment |
| Organization | Contoso Health Services (Fictional) |
| Cloud Platform | Microsoft Azure |
| Document Type | Network Design Document |
| Version | 1.0 |
| Status | Completed |
| Author | Manyo Sampson |
| Last Updated | July 2026 |

# Revision History

| Version | Date | Author | Description |
|----------|------|---------|-------------|
| 1.0 | July 2026 | Manyo Sampson | Initial Network Design Document |

# Table of Contents

1. Executive Summary
2. Network Objectives
3. Network Requirements
4. Network Overview
5. Virtual Network Design
6. IP Addressing Strategy
7. Subnet Design
8. Network Security Groups
9. References

# 1. Executive Summary

This document describes the network architecture implemented for the Secure Azure Enterprise Environment.

The network was designed to establish a secure Azure foundation by providing workload isolation, private connectivity, and controlled communication between Azure resources.

Microsoft Azure Virtual Network (VNet) serves as the primary network boundary, while dedicated subnets and Network Security Groups (NSGs) provide logical segmentation and traffic control.

Sensitive Azure platform services communicate through Azure Private Endpoints rather than the public internet, supporting Microsoft's Zero Trust networking principles.

The resulting network provides a scalable and secure foundation for enterprise workloads while minimizing unnecessary network exposure.

# 2. Network Objectives

The network architecture was designed to achieve the following objectives.

- Establish a secure Azure Virtual Network.
- Separate workloads using dedicated subnets.
- Implement network segmentation.
- Control traffic using Network Security Groups.
- Support Azure Private Link.
- Reduce public network exposure.
- Provide a scalable IP addressing scheme.
- Align with Microsoft's Zero Trust architecture.

# 3. Network Requirements

The following requirements guided the network design.

## NR-01

Deploy a dedicated Azure Virtual Network.

## NR-02

Separate workloads into dedicated subnets.

## NR-03

Deploy Network Security Groups.

## NR-04

Support Azure Private Endpoints.

## NR-05

Enable Private DNS resolution.

## NR-06

Allow secure communication with Azure Storage.

## NR-07

Allow secure communication with Azure Key Vault.

## NR-08

Disable unnecessary public network access.

# 4. Network Overview

The Azure Virtual Network provides the secure communication boundary for all deployed Azure resources.

Rather than deploying resources into a flat network, dedicated subnets were created to isolate administrative workloads, business applications, backend resources, and Azure Private Endpoints.

Traffic destined for Azure Storage and Azure Key Vault is redirected through Azure Private Endpoints, ensuring communication remains on Microsoft's private backbone network.

Network Security Groups provide additional protection by filtering traffic at the subnet level.

The implemented design supports Microsoft's defense-in-depth strategy by combining multiple network security controls.

# 5. Virtual Network Design

## Virtual Network

| Property | Value |
|----------|--------|
| Name | vnet-contoso-prod-001 |
| Address Space | 10.1.0.0/16 |
| Region | *East US 2* |

The Virtual Network provides the primary communication boundary for Azure resources deployed within the project.

All workloads communicate through this network unless explicitly restricted by Network Security Groups.

Using a dedicated Virtual Network provides several advantages.

- Network isolation
- Secure communication
- Private Endpoint support
- Simplified management
- Future scalability

# 6. IP Addressing Strategy

The selected address space for the Virtual Network is:

```
10.1.0.0/16
```

The address range belongs to the private IPv4 address space defined by RFC 1918 and is not routable over the public internet.

A /16 network provides sufficient address capacity for future expansion while maintaining a simple addressing structure.

The address space was divided into dedicated subnets based on workload function.

This approach improves organization, simplifies administration, and supports network isolation.

# IP Allocation Strategy

Rather than assigning resources randomly throughout the network, addresses are grouped according to workload type.

Benefits include:

- Easier troubleshooting
- Simplified routing
- Better security
- Future scalability
- Consistent administration

# Address Space Summary

| Network | Purpose |
|----------|----------|
| 10.1.0.0/16 | Azure Virtual Network |

# 7. Subnet Design

The Virtual Network is segmented into four dedicated subnets.

Each subnet performs a specific function within the environment.

This separation reduces unnecessary communication between resources while supporting Microsoft's defense-in-depth strategy.

## Management Subnet

Purpose

Administrative resources.

Responsibilities

- Administrative connectivity
- Management resources

Benefits

- Administrative isolation
- Simplified management
- Reduced attack surface

## Application Subnet

Purpose

Business application resources.

Responsibilities

- Application workloads
- Future application deployment

Benefits

- Workload isolation
- Easier security management

## Data Subnet

Purpose

Backend services and data resources.

Responsibilities

- Backend workloads
- Data services

Benefits

- Separation from applications
- Reduced lateral movement

## Private Endpoint Subnet

Purpose

Azure Private Link resources.

Responsibilities

- Azure Storage Private Endpoint
- Azure Key Vault Private Endpoint

Benefits

- Secure private connectivity
- Eliminates public internet communication
- Supports Private DNS

# Subnet Summary

| Subnet | Purpose |
|---------|----------|
| Management | Administrative resources |
| Application | Business workloads |
| Data | Backend services |
| Private Endpoint | Azure Private Link |

The subnet design allows additional Azure resources to be incorporated into the environment while maintaining logical separation and consistent network organization.

# 8. Network Security Groups

Network Security Groups (NSGs) provide subnet-level traffic filtering.

Dedicated NSGs were associated with the following subnets.

| NSG | Associated Subnet |
|------|-------------------|
| Management NSG | Management |
| Application NSG | Application |
| Data NSG | Data |

Each NSG provides an additional security layer by controlling network traffic entering and leaving its associated subnet.

Although Azure platform services communicate through Private Endpoints, NSGs remain an important component of the network security model by enforcing network segmentation.

# Benefits of NSGs

- Traffic filtering
- Network isolation
- Defense in depth
- Reduced attack surface
- Simplified security administration

# References

- Microsoft Learn
- Azure Virtual Network Documentation
- Azure Network Security Groups Documentation
- Azure Private Link Documentation
- Azure Private DNS Documentation
