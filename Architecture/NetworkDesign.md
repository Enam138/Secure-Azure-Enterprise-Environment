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


# 9. Network Traffic Flow

## Overview

The network architecture was designed to ensure that communication between Azure resources remains secure, predictable, and isolated.

Rather than allowing unrestricted communication, traffic is directed through the Azure Virtual Network where segmentation, Network Security Groups (NSGs), and Private Endpoints provide multiple layers of protection.

The design minimizes exposure to the public internet while enabling secure access to Azure platform services.

## Administrative Access Flow

Administrative access follows Azure's identity-first security model.

```text
                                                                     Administrator

                                                                           ↓

                                                                    Microsoft Entra ID

                                                                            ↓

                                                             Azure Role-Based Access Control (RBAC)

                                                                             ↓

                                                                      Azure Subscription

                                                                             ↓

                                                                      Azure Resource Group

                                                                              ↓

                                                                        Azure Resources
```

Authentication occurs through Microsoft Entra ID, while authorization decisions are enforced through Azure RBAC before access to Azure resources is granted.

## Storage Traffic Flow

Communication with Azure Storage occurs through a Private Endpoint.

```text
                                                        Application / Azure Resource

                                                                    ↓

                                                           Azure Virtual Network

                                                                    ↓

                                                             Private Endpoint

                                                                    ↓

                                                           Azure Storage Account
```

This design keeps traffic on Microsoft's private backbone network and prevents direct public access to the Storage Account.

## Key Vault Traffic Flow

Secure access to Azure Key Vault also uses a Private Endpoint.

```text
                                                   Administrator or Azure Resource

                                                                 ↓

                                                        Azure Virtual Network

                                                                 ↓

                                                          Private Endpoint

                                                                 ↓

                                                          Azure Key Vault
```

Application secrets remain protected because communication never relies on the public internet.

# 10. Private Endpoint Design

## Overview

Azure Private Endpoints were implemented to provide secure, private connectivity to Azure platform services.

Unlike public endpoints, Private Endpoints assign private IP addresses from the Azure Virtual Network, allowing Azure resources to communicate internally.

## Implemented Private Endpoints

| Azure Service | Private Endpoint | Status |
|---------------|------------------|--------|
| Azure Storage Account | Configured | ✅ |
| Azure Key Vault | Configured | ✅ |

## Benefits

Implementing Private Endpoints provides several advantages.

- Eliminates public internet communication
- Reduces the attack surface
- Supports Zero Trust networking
- Improves network isolation
- Enables secure communication over Microsoft's backbone network

# 11. Private DNS Design

## Overview

Private DNS Zones enable Azure resources within the Virtual Network to resolve the private IP addresses associated with Private Endpoints.

Without Private DNS, applications would require manual DNS configuration to reach Azure platform services privately.

## Implemented DNS Configuration

Private DNS Zones were automatically created during the deployment of:

- Azure Storage Private Endpoint
- Azure Key Vault Private Endpoint

These zones ensure that DNS queries resolve to private IP addresses instead of public endpoints.

## Benefits

- Automatic private name resolution
- Simplified administration
- Secure connectivity
- Improved reliability

# 12. Storage Network Security

The Azure Storage Account was configured with multiple networking controls to protect stored data.

## Implemented Controls

| Security Control | Status |
|------------------|--------|
| Private Endpoint | ✅ |
| Public Network Access Disabled | ✅ |
| Secure Transfer Required | ✅ |
| Encryption at Rest | ✅ |

These controls ensure that access to the Storage Account is restricted to authorized private network paths.

# 13. Key Vault Network Security

Azure Key Vault stores sensitive application secrets and therefore requires additional network protection.

## Implemented Controls

| Security Control | Status |
|------------------|--------|
| Azure RBAC Authorization | ✅ |
| Private Endpoint | ✅ |
| Private DNS | ✅ |
| Public Network Access Disabled | ✅ |

Restricting Key Vault to private connectivity helps prevent unauthorized network access while maintaining secure administrative operations.

# 14. Routing Considerations

The deployed environment uses Azure's default system routes.

Because no custom route tables were required for this implementation, Azure automatically manages traffic routing within the Virtual Network and to Azure platform services.

Communication to Azure Storage and Azure Key Vault occurs through their associated Private Endpoints.

This approach keeps the network design simple while maintaining secure connectivity.

# 15. Network Security Architecture

The implemented network security model follows Microsoft's defense-in-depth strategy.

Each layer contributes to protecting Azure resources.

| Security Layer | Purpose |
|----------------|---------|
| Microsoft Entra ID | User authentication |
| Azure RBAC | Authorization |
| Virtual Network | Network isolation |
| Subnets | Workload separation |
| Network Security Groups | Traffic filtering |
| Private Endpoints | Private connectivity |
| Private DNS | Secure name resolution |

No single control is relied upon exclusively. Instead, multiple complementary controls work together to strengthen the overall security posture.

# 16. Zero Trust Networking

The network design aligns with Microsoft's Zero Trust principles.

| Zero Trust Principle | Network Implementation |
|----------------------|------------------------|
| Verify Explicitly | Authentication through Microsoft Entra ID |
| Use Least Privilege | Azure RBAC |
| Assume Breach | Network segmentation with dedicated subnets |
| Minimize Exposure | Private Endpoints and disabled public access |
| Protect Resources | NSGs, Private DNS, and encryption |

By assuming that no network location is inherently trusted, the architecture reduces opportunities for unauthorized access and lateral movement.

# 17. Network Design Decisions

Several design decisions were made to improve security and maintainability.

### Dedicated Virtual Network

A dedicated Azure Virtual Network was deployed to provide a secure communication boundary for all project resources.

### Network Segmentation

Separate subnets were created for management, application, data, and Private Endpoint resources.

This logical separation improves security and supports future scalability.

### Network Security Groups

NSGs were associated with the Management, Application, and Data subnets to provide traffic filtering and strengthen network isolation.


### Azure Private Link

Private Endpoints were selected for Azure Storage and Azure Key Vault to reduce public exposure and support secure communication.

### Public Network Access

Public network access was disabled for Azure Storage and Azure Key Vault after verifying successful private connectivity.

This significantly reduces the attack surface.

# 18. Risks and Mitigations

| Risk | Potential Impact | Mitigation |
|------|------------------|------------|
| Public exposure of services | Increased attack surface | Private Endpoints and disabled public access |
| Excessive network communication | Lateral movement | Subnet segmentation |
| Unauthorized administrative access | Security compromise | Microsoft Entra ID and Azure RBAC |
| Misconfigured DNS | Connectivity failures | Private DNS Zones |
| Unauthorized traffic | Unwanted network access | Network Security Groups |

The implemented controls collectively reduce these risks and improve the overall resilience of the network architecture.

# 19. Validation

The network implementation was validated through the Azure portal.

The following components were successfully deployed and verified.

| Component | Status |
|-----------|--------|
| Azure Virtual Network | ✅ |
| Address Space Configured | ✅ |
| Management Subnet | ✅ |
| Application Subnet | ✅ |
| Data Subnet | ✅ |
| Private Endpoint Subnet | ✅ |
| Management NSG | ✅ |
| Application NSG | ✅ |
| Data NSG | ✅ |
| Storage Private Endpoint | ✅ |
| Key Vault Private Endpoint | ✅ |
| Private DNS Zones | ✅ |
| Public Access Disabled (Storage) | ✅ |
| Public Access Disabled (Key Vault) | ✅ |

Validation confirms that the implemented network meets the project objectives.

# 20. Conclusion

The network architecture provides a secure and scalable foundation for the Secure Azure Enterprise Environment.

By combining Azure Virtual Network, subnet segmentation, Network Security Groups, Azure Private Link, and Private DNS, the solution reduces public exposure while enabling secure communication between Azure resources.

The design reflects Microsoft's networking best practices and establishes a strong foundation for future expansion as additional Azure services are introduced.

# References

The network design and implementation were guided by Microsoft's official documentation.

- Microsoft Learn
- Azure Virtual Network Documentation
- Azure Private Link Documentation
- Azure Private Endpoint Documentation
- Azure Private DNS Documentation
- Azure Network Security Groups Documentation
- Azure Well-Architected Framework
- Azure Security Benchmark

# Appendix A – Network Summary

| Area | Implementation |
|------|----------------|
| Virtual Network | Azure Virtual Network |
| Address Space | 10.1.0.0/16 |
| Network Segmentation | Four dedicated subnets |
| Traffic Filtering | Network Security Groups |
| Private Connectivity | Azure Private Endpoints |
| DNS | Private DNS Zones |
| Storage Access | Private Endpoint |
| Key Vault Access | Private Endpoint |
| Public Network Access | Disabled for Storage and Key Vault |

# Appendix B – Acronyms

| Acronym | Meaning |
|----------|---------|
| VNet | Virtual Network |
| NSG | Network Security Group |
| RBAC | Role-Based Access Control |
| DNS | Domain Name System |
| PE | Private Endpoint |
| PaaS | Platform as a Service |
| RFC | Request for Comments |
| ARM | Azure Resource Manager |
