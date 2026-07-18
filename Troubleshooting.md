# Troubleshooting Guide

# Secure Azure Enterprise Environment

| Document Information | |
|----------------------|--------------------------------|
| Project | Secure Azure Enterprise Environment |
| Organization | Contoso Health Services (Fictional) |
| Cloud Platform | Microsoft Azure |
| Document Type | Troubleshooting Guide |
| Version | 1.0 |
| Status | Completed |
| Author | Manyo Sampson |
| Last Updated | July 2026 |

# 1. Purpose

This document records issues encountered during the deployment of the Secure Azure Enterprise Environment and the steps taken to resolve them.

Documenting troubleshooting activities provides a valuable reference for future deployments and demonstrates practical problem-solving during cloud infrastructure implementation.

# 2. Troubleshooting Summary

| Issue | Status |
|------|--------|
| Azure Key Vault Firewall Configuration Error | ✅ Resolved |

# 3. Issue: Azure Key Vault Firewall Configuration

## Description

While configuring Azure Key Vault networking, an error occurred when updating the firewall settings to allow client access.

## Error Message

```text
Invalid value found at properties.networkAcls.ipRules[0].value:
172.20.10.5/32 belongs to forbidden range
172.16.0.0–172.31.255.255 (private IP addresses)
```

## Root Cause

A private IPv4 address was mistakenly added to the Azure Key Vault firewall allow list.

Azure Key Vault firewall rules only accept **public IPv4 addresses**. Private IP addresses defined by RFC 1918 are not supported.

## Investigation

The following troubleshooting steps were performed:

- Reviewed Azure Activity Logs.
- Verified Azure RBAC role assignments.
- Checked Azure Resource Provider registration.
- Examined Key Vault networking settings.
- Validated firewall configuration.

## Resolution

The private IP address was removed and replaced with the administrator's public IPv4 address.

After updating the firewall configuration:

- Azure Key Vault became accessible.
- Secret creation completed successfully.
- Key Vault configuration was finalized.
- Public network access was later disabled after validating the Private Endpoint.

## Outcome

The issue was resolved successfully without requiring the Key Vault to be recreated.

The deployment continued as planned and all project objectives were achieved.

# 4. Lessons Learned

The troubleshooting process reinforced several important Azure concepts:

- Azure Activity Logs are essential for diagnosing deployment issues.
- Azure Key Vault firewall rules only support public IP addresses.
- Azure RBAC permissions should be verified before investigating service configuration.
- Testing connectivity before disabling public access helps prevent administrative lockout.
- Following a structured troubleshooting process reduces deployment time.

# 5. Conclusion

The deployment encountered one significant configuration issue, which was investigated, resolved, and documented successfully.

Recording troubleshooting activities improves future deployments and provides operational knowledge that can be applied to similar Azure environments.
