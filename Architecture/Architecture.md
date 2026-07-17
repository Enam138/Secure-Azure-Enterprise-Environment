# Enterprise Architecture Design Document

# Secure Azure Enterprise Environment

| Document Information | |
|----------------------|------------------------------------------------|
| Project Name | Secure Azure Enterprise Environment |
| Organization | Contoso Health Services (Fictional) |
| Cloud Platform | Microsoft Azure |
| Architecture Type | Secure Azure Landing Zone |
| Security Model | Microsoft Zero Trust |
| Environment | Production (Lab Simulation) |
| Version | 1.0 |
| Document Owner | Manyo Sampson |
| Status | Completed |
| Last Updated | July 2026 |

# Revision History

| Version | Date | Author | Description |
|----------|------|---------|-------------|
| 1.0 | July 2026 | Manyo Sampson | Initial Architecture Design Document |


# Table of Contents

1. Executive Summary
2. Business Scenario
3. Business Requirements
4. Functional Requirements
5. Non-Functional Requirements
6. Assumptions
7. Constraints
8. Architecture Principles
9. Solution Overview
10. References


# 1. Executive Summary

## Purpose

This document presents the architecture design for the **Secure Azure Enterprise Environment** developed for **Contoso Health Services**, a fictional healthcare organization migrating selected workloads from an on-premises environment to Microsoft Azure.

The primary objective of this project was to design and implement a secure Azure landing zone that demonstrates Microsoft's recommended cloud security practices. The solution emphasizes secure networking, identity-based access control, private connectivity, encryption, and governance to establish a secure foundation for enterprise cloud workloads.

Rather than deploying numerous Azure services, this project focuses on implementing a small set of core Azure services correctly and securely. Every architectural decision was made to support Microsoft's defense-in-depth strategy and Zero Trust security model while minimizing unnecessary exposure to the public internet.

The resulting environment provides a practical example of how Azure networking, Azure Storage, Azure Key Vault, Azure RBAC, and Private Link can be combined to create a secure cloud infrastructure suitable for hosting sensitive business data.


# 2. Business Scenario

## Organization Background

Contoso Health Services is a healthcare organization responsible for storing sensitive patient information, internal business records, and operational data.

To modernize its infrastructure, the organization has begun migrating selected workloads to Microsoft Azure.

Because healthcare data is highly sensitive, the cloud environment must be designed with security as a primary objective rather than an afterthought.

## Business Challenge

The organization requires an Azure environment capable of supporting secure cloud adoption while protecting confidential information from unauthorized access.

Several key challenges were identified:

- Protect sensitive healthcare information.
- Reduce exposure to the public internet.
- Secure access to cloud resources.
- Implement centralized identity and access management.
- Build a scalable cloud foundation for future services.

## Business Objective

The objective of this project was to implement a secure Azure environment that:

- follows Microsoft's recommended security practices;
- supports secure communication between Azure resources;
- protects sensitive information using Azure-native security services;
- demonstrates enterprise-ready cloud architecture principles.


# 3. Business Requirements

The implemented solution was designed to satisfy the following business requirements.

## BR-01 Secure Resource Organization

Azure resources shall be organized using Resource Groups to simplify administration and lifecycle management.


## BR-02 Secure Network Foundation

The environment shall provide a segmented Virtual Network that separates administrative, application, data, and private connectivity workloads.

## BR-03 Secure Data Storage

Business data shall be stored securely using Azure Storage with encryption enabled.

## BR-04 Secure Secret Management

Application secrets shall be stored within Azure Key Vault rather than embedded inside applications.

## BR-05 Private Connectivity

Sensitive Azure platform services shall be accessible through Private Endpoints whenever possible.

## BR-06 Least Privilege Access

Administrative permissions shall be managed using Azure Role-Based Access Control (RBAC).

## BR-07 Data Protection

Sensitive information shall remain encrypted while stored within Azure.

## BR-08 Reduced Public Exposure

Public network access shall be disabled for sensitive platform services after private connectivity has been established.

# 4. Functional Requirements

The environment must provide the following capabilities.

| ID | Requirement |
|----|-------------|
| FR-01 | Deploy Azure Resource Group |
| FR-02 | Deploy Azure Virtual Network |
| FR-03 | Create Management Subnet |
| FR-04 | Create Application Subnet |
| FR-05 | Create Data Subnet |
| FR-06 | Create Private Endpoint Subnet |
| FR-07 | Deploy Network Security Groups |
| FR-08 | Deploy Azure Storage Account |
| FR-09 | Configure Storage Private Endpoint |
| FR-10 | Deploy Azure Key Vault |
| FR-11 | Assign Azure RBAC permissions |
| FR-12 | Store application secret |
| FR-13 | Configure Key Vault Private Endpoint |
| FR-14 | Configure Private DNS |
| FR-15 | Disable Public Network Access |

All functional requirements were successfully implemented and validated within the Azure environment.

# 5. Non-Functional Requirements

In addition to functionality, the environment was designed to satisfy several quality attributes.

## Security

Security was the highest priority throughout the design and implementation process.

The architecture incorporates identity-based access control, encryption, network isolation, and private connectivity to reduce the overall attack surface.

## Availability

The environment is designed to use highly available Azure platform services managed by Microsoft.

## Scalability

The Virtual Network structure supports future expansion without requiring significant architectural redesign.

Additional Azure resources can be deployed into the existing network segmentation model.

## Manageability

Resources are organized using standardized naming conventions and Resource Groups to simplify administration.

Azure RBAC provides centralized authorization management.

## Maintainability

The environment uses Azure-native services that integrate with one another, reducing operational complexity while improving long-term maintainability.

# 6. Assumptions

The architecture was designed based on the following assumptions.

- Azure services remain available within the selected Azure region.
- Users authenticate using Microsoft Entra ID.
- Administrative access is granted through Azure RBAC.
- Azure manages the underlying cloud infrastructure.
- Network connectivity between Azure services is reliable.
- Private Endpoints are available for supported Azure services.

These assumptions align with Microsoft's shared responsibility model for cloud computing.

# 7. Constraints

The following constraints influenced the architecture.

## Azure Free Subscription

The environment was implemented using an Azure Free Subscription.

This required careful resource selection to remain within service availability and subscription limits.

## Cost Optimization

Only services required to meet the project objectives were deployed.

Enterprise services such as Azure Firewall, Azure Bastion, Microsoft Defender for Cloud, and Azure Monitor were intentionally excluded from this phase to control costs.

## Scope

The project focused on establishing a secure Azure foundation rather than deploying business applications or virtual machines.

# 8. Architecture Principles

The architecture follows several core design principles.

## Principle 1 Security by Design

Security was incorporated during planning and implementation rather than being added after deployment.

Examples include:

- Private Endpoints
- Azure RBAC
- Encryption
- Network Segmentation

## Principle 2 Least Privilege

Administrative permissions were granted using Azure Role-Based Access Control.

Users receive only the permissions required to perform their responsibilities.

## Principle 3 Defense in Depth

Multiple security layers work together to reduce organizational risk.

Examples include:

- Microsoft Entra ID
- Azure RBAC
- Network Security Groups
- Virtual Network Segmentation
- Private Endpoints
- Encryption
- Azure Key Vault

## Principle 4 Minimize Public Exposure

Sensitive Azure platform services were configured to communicate through Private Endpoints.

Public network access was disabled after validating private connectivity.

## Principle 5 Simplicity

Only services necessary to satisfy the project objectives were deployed.

Keeping the environment simple improves maintainability, reduces unnecessary complexity, and minimizes the attack surface.


## Principle 6 Scalability

The architecture provides a secure foundation that can accommodate additional Azure services without requiring major redesign.

Future resources can be integrated into the existing network and security model while maintaining consistency with Microsoft's best practices.

# 9. Solution Overview

## Overview

The Secure Azure Enterprise Environment was designed as a foundational cloud infrastructure that prioritizes security, governance, and scalability.

The solution follows Microsoft's recommended cloud architecture by combining identity, network segmentation, private connectivity, encryption, and secure secret management into a cohesive environment.

Rather than exposing Azure platform services directly to the public internet, sensitive resources are accessed through Azure Private Link and Private Endpoints. Administrative access is controlled using Microsoft Entra ID and Azure Role-Based Access Control (RBAC), while Network Security Groups (NSGs) provide an additional layer of network protection.

The resulting architecture establishes a secure landing zone capable of supporting future enterprise workloads while reducing the overall attack surface.

# 10. Solution Architecture

The diagram below illustrates the implemented Azure environment.

<p align="center">

<img width="1536" height="1024" alt="ChatGPT Image Jul 17, 2026, 12_45_24 AM" src="https://github.com/user-attachments/assets/b3d45b02-c634-48ee-8ebd-bc2a619385a4" />

</p>

The architecture demonstrates how Azure identity, networking, storage, and security services work together to implement Microsoft's defense-in-depth strategy.

The design consists of five primary layers:

- Identity Layer
- Resource Organization Layer
- Network Layer
- Platform Services Layer
- Security Layer

Each layer contributes independently to the overall security posture of the environment.

# 11. Component Architecture

The implemented solution consists of several Azure services that work together to provide secure cloud infrastructure.

| Component | Purpose |
|------------|---------|
| Microsoft Entra ID | Identity provider for Azure authentication |
| Azure Subscription | Administrative and billing boundary |
| Resource Group | Logical organization of Azure resources |
| Azure Virtual Network | Secure network boundary |
| Network Security Groups | Network traffic filtering |
| Azure Storage Account | Secure cloud storage |
| Azure Key Vault | Secure secret management |
| Azure Private Endpoint | Private connectivity to Azure services |
| Private DNS Zone | Private name resolution |
| Azure RBAC | Authorization and least-privilege access |

Each component was selected because it contributes to Microsoft's layered security model rather than functioning as an isolated security control.

# 12. Identity Architecture

## Overview

Identity forms the foundation of Microsoft's Zero Trust security model.

This implementation uses **Microsoft Entra ID** for authentication and **Azure Role-Based Access Control (RBAC)** for authorization.

Authentication verifies the identity of a user attempting to access Azure resources, while RBAC determines the actions that authenticated users are permitted to perform.

Separating authentication from authorization improves security and simplifies access management across Azure resources.

## Authentication

Authentication is provided through Microsoft Entra ID.

All administrative access to the Azure environment is authenticated through Azure's centralized identity platform.

Benefits include:

- Centralized identity management
- Single identity across Azure resources
- Integration with Azure RBAC
- Enterprise-grade authentication

## Authorization

Authorization is implemented using Azure RBAC.

Rather than assigning unrestricted permissions, Azure RBAC enables permissions to be granted based on predefined roles.

For this project, the **Key Vault Administrator** role was assigned to allow secure management of Azure Key Vault resources.

This approach aligns with Microsoft's recommendation to implement least-privilege access wherever possible.

## Identity Flow

```text
              User

               ↓

       Microsoft Entra ID

               ↓

         Authentication

                ↓

            Azure RBAC

                ↓

     Authorized Azure Resource
```

This layered identity model ensures that authentication occurs before authorization decisions are evaluated.

# 13. Resource Organization

All resources were deployed into a dedicated Resource Group.

```text
rg-contoso-prod-001
```

Using a Resource Group provides several operational advantages.

### Benefits

- Simplifies resource deployment
- Centralizes administration
- Supports Azure RBAC assignments
- Enables lifecycle management
- Improves cost tracking
- Simplifies resource discovery

Standardized naming conventions and resource tagging were applied to improve governance and maintain consistency across the environment.

# 14. Network Architecture

## Overview

The Azure Virtual Network provides the primary network boundary for the environment.

The network was designed to separate workloads into dedicated subnets, reducing unnecessary communication between resources while supporting Microsoft's defense-in-depth strategy.

## Address Space

```
10.10.0.0/16
```

The selected address space provides sufficient capacity for future expansion while maintaining a simple addressing scheme.

## Network Segmentation

The Virtual Network contains four dedicated subnets.

| Subnet | Purpose |
|---------|----------|
| Management | Administrative resources |
| Application | Business applications |
| Data | Backend services |
| Private Endpoint | Azure Private Link resources |

Each subnet isolates a specific workload category.

This design improves security by limiting lateral movement and allowing network policies to be applied independently.

## Network Security Groups

Dedicated Network Security Groups were associated with the Management, Application, and Data subnets.

These NSGs provide an additional layer of security by controlling inbound and outbound network traffic.

Benefits include:

- Traffic filtering
- Reduced attack surface
- Improved network isolation
- Layered network security

## Traffic Flow

The network architecture follows a controlled communication model.

```text
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

              Azure Resources
```

Traffic destined for Azure Storage and Azure Key Vault is redirected through Azure Private Endpoints rather than traversing the public internet.

# 15. Storage Architecture

Azure Storage provides secure cloud-based storage for enterprise workloads.

The Storage Account was configured using Microsoft's recommended security settings.

### Implemented Security Controls

- Encryption at rest enabled
- Secure transfer required
- Azure-managed encryption keys
- Private Endpoint connectivity
- Public network access disabled

Together, these controls ensure that stored data remains protected while restricting network access to authorized private connections.

## Storage Connectivity

```text
             Azure Virtual Network

                       ↓

                 Private Endpoint

                        ↓

              Azure Storage Account
```

This communication path remains entirely within Microsoft's private backbone network.

# 16. Key Vault Architecture

Azure Key Vault provides centralized storage for sensitive information, including application secrets.

The service eliminates the need to store secrets directly within application code or configuration files.

## Implemented Security Controls

- Azure RBAC authorization model
- Secure secret storage
- Private Endpoint
- Private DNS integration
- Public network access disabled

## Secret Management

A test secret was successfully created and stored within Azure Key Vault to validate secure secret management functionality.

Only authorized users with appropriate Azure RBAC permissions can manage or retrieve stored secrets.

## Key Vault Connectivity

```text
               Azure Virtual Network

                        ↓

                 Private Endpoint

                        ↓

                  Azure Key Vault
```

This configuration ensures that Azure Key Vault remains accessible only through private network connectivity.

# 17. Private Connectivity

## Overview

One of the primary security objectives of this project was to minimize exposure of Azure platform services to the public internet.

To achieve this, Azure Private Link was implemented for Azure Storage and Azure Key Vault. Private Endpoints provide private IP addresses within the Azure Virtual Network, allowing communication to occur over Microsoft's private backbone network rather than the public internet.

This approach significantly reduces the attack surface while maintaining secure connectivity between Azure resources.

## Private Endpoints Implemented

| Azure Service | Private Endpoint | Status |
|---------------|------------------|--------|
| Azure Storage Account | Configured | ✅ |
| Azure Key Vault | Configured | ✅ |

## Private DNS Integration

Private DNS Zones were configured during the deployment of the Private Endpoints.

This enables Azure resources within the Virtual Network to resolve the private IP addresses of Azure Storage and Azure Key Vault automatically without relying on public DNS resolution.

Private DNS integration provides:

- Seamless name resolution
- Secure internal communication
- Simplified administration
- Improved reliability

## Benefits

Implementing Private Link provides several security and operational benefits.

- Eliminates unnecessary exposure to the public internet.
- Reduces the organization's attack surface.
- Ensures traffic remains on Microsoft's private backbone.
- Improves protection of sensitive Azure platform services.
- Supports Zero Trust networking principles.

# 18. Security Architecture

## Overview

Security was the primary design consideration throughout the implementation of this Azure environment.

Rather than relying on a single security control, the architecture follows Microsoft's **Defense-in-Depth** strategy by implementing multiple independent layers of protection.

Each security layer complements the others to improve the overall security posture of the environment.

## Security Layers

| Security Layer | Azure Service | Purpose |
|----------------|---------------|---------|
| Identity | Microsoft Entra ID | User authentication |
| Authorization | Azure RBAC | Least-privilege access |
| Network | Azure Virtual Network | Network isolation |
| Traffic Control | Network Security Groups | Traffic filtering |
| Data Protection | Azure Storage Encryption | Protect stored data |
| Secret Management | Azure Key Vault | Secure storage of secrets |
| Private Connectivity | Azure Private Link | Private communication |
| Name Resolution | Private DNS Zone | Secure internal DNS |

## Defense in Depth

The implemented architecture applies multiple security controls at different layers.

```
                                            User

                                              ↓

                                      Microsoft Entra ID

                                              ↓

                                          Azure RBAC

                                              ↓

                                     Azure Virtual Network

                                              ↓

                                     Network Security Groups

                                              ↓

                                       Private Endpoint

                                              ↓

                                Azure Storage / Azure Key Vault
```

Each layer independently contributes to reducing organizational risk.

# 19. Governance

## Resource Organization

All deployed resources are organized within a dedicated Resource Group.

This approach provides:

- Centralized administration
- Simplified lifecycle management
- Consistent organization
- Easier resource discovery

## Naming Standards

Consistent naming conventions were applied throughout the project to improve readability and maintainability.

Examples include:

- Resource Group
- Virtual Network
- Storage Account
- Key Vault
- Network Security Groups

Standardized naming simplifies administration and supports long-term scalability.

## Resource Tagging

Resource tags were applied during deployment to support governance and future operational management.

Tagging improves:

- Resource identification
- Cost reporting
- Environment classification
- Administrative consistency

# 20. Zero Trust Alignment

The architecture aligns with Microsoft's Zero Trust security model by implementing security controls across identity, networking, and data protection.

| Zero Trust Principle | Implementation |
|----------------------|----------------|
| Verify explicitly | Microsoft Entra ID authentication |
| Use least privilege | Azure RBAC role assignments |
| Assume breach | Network segmentation and NSGs |
| Protect data | Azure Storage Encryption and Azure Key Vault |
| Minimize exposure | Azure Private Endpoints and disabled public access |

Rather than trusting users or network locations by default, access is granted only after identity verification and authorization.

# 21. Key Design Decisions

Several architectural decisions were made to improve security, simplify administration, and align with Microsoft's recommended cloud practices.

## Azure Virtual Network

A dedicated Virtual Network was created to provide a secure network boundary for Azure resources.

This establishes a controlled environment where communication between services can be managed and monitored.

## Network Segmentation

Separate subnets were created for:

- Management
- Application
- Data
- Private Endpoints

Segmenting workloads reduces unnecessary communication and limits the potential impact of security incidents.

## Azure RBAC

Azure RBAC was selected as the authorization model for Azure Key Vault instead of legacy access policies.

This provides centralized permission management and aligns with Microsoft's modern identity and access recommendations.

## Azure Private Link

Azure Storage and Azure Key Vault were configured with Private Endpoints to remove dependency on public network access.

This decision significantly reduces exposure to internet-based attacks.

## Public Network Access

Public network access was disabled only after validating successful private connectivity.

This ensures that administrative operations remain available while reducing the attack surface.

## Encryption

Azure-managed encryption protects data stored within Azure Storage without requiring additional administrative overhead.

# 22. Risks and Mitigations

| Risk | Potential Impact | Mitigation |
|------|------------------|------------|
| Excessive permissions | Unauthorized administrative actions | Azure RBAC with least privilege |
| Public exposure | Increased attack surface | Private Endpoints and disabled public access |
| Secret leakage | Credential compromise | Azure Key Vault |
| Unauthorized network access | Lateral movement | Network segmentation and NSGs |
| Data exposure | Confidentiality risks | Encryption at rest |

The implemented controls reduce these risks while supporting secure cloud operations.

# 23. Validation

The deployed environment was validated through the Azure portal after implementation.

The following components were successfully deployed and verified.

| Component | Status |
|-----------|--------|
| Resource Group | ✅ |
| Virtual Network | ✅ |
| Four Subnets | ✅ |
| Network Security Groups | ✅ |
| Azure Storage Account | ✅ |
| Storage Private Endpoint | ✅ |
| Azure Key Vault | ✅ |
| Azure RBAC Configuration | ✅ |
| Secret Creation | ✅ |
| Key Vault Private Endpoint | ✅ |
| Private DNS Zones | ✅ |
| Public Network Access Disabled | ✅ |

Deployment validation confirms that all planned project objectives were successfully achieved.

# 24. Lessons Learned

This project reinforced several important cloud security concepts.

- Security should be incorporated during the design phase rather than added after deployment.
- Network segmentation improves isolation and reduces risk.
- Azure RBAC provides centralized and scalable authorization.
- Azure Private Link is an effective method for securing Azure platform services.
- Azure Key Vault enables secure management of application secrets.
- Azure Activity Logs are valuable for diagnosing deployment and configuration issues.
- Accurate documentation is essential for communicating architectural decisions and supporting long-term maintenance.

These lessons demonstrate how Azure-native services can be combined to build a secure and manageable cloud environment.

# 25. Conclusion

The Secure Azure Enterprise Environment establishes a strong security foundation by combining identity, networking, encryption, governance, and private connectivity into a cohesive Azure architecture.

The implementation demonstrates how Microsoft Azure services can be configured to support secure cloud adoption while following Microsoft's Zero Trust principles and defense-in-depth strategy.

Although intentionally limited in scope, the environment provides a scalable foundation that can be extended with additional Azure services in future phases without requiring major architectural changes.

This project reflects practical experience in designing and implementing a secure Azure landing zone and highlights the importance of building cloud environments that prioritize security, governance, and maintainability from the outset.

# 26. References

The architecture and implementation were guided by Microsoft's official documentation and best practices.

- Microsoft Learn
- Azure Architecture Center
- Azure Well-Architected Framework
- Azure Security Benchmark
- Azure Virtual Network documentation
- Azure Private Link documentation
- Azure Storage documentation
- Azure Key Vault documentation
- Azure Role-Based Access Control (RBAC) documentation
- Azure Resource Manager documentation

# Appendix A – Architecture Summary

| Area | Implementation |
|------|----------------|
| Identity | Microsoft Entra ID |
| Authorization | Azure RBAC |
| Resource Organization | Azure Resource Group |
| Networking | Azure Virtual Network |
| Segmentation | Four Dedicated Subnets |
| Traffic Filtering | Network Security Groups |
| Storage | Azure Storage Account |
| Secret Management | Azure Key Vault |
| Private Connectivity | Azure Private Endpoints |
| DNS | Private DNS Zones |
| Data Protection | Encryption at Rest |
| Public Exposure | Disabled for Storage and Key Vault |

# Appendix B – Acronyms

| Acronym | Meaning |
|----------|---------|
| RBAC | Role-Based Access Control |
| NSG | Network Security Group |
| VNet | Virtual Network |
| DNS | Domain Name System |
| PaaS | Platform as a Service |
| IAM | Identity and Access Management |
| PE | Private Endpoint |
| ARM | Azure Resource Manager |

