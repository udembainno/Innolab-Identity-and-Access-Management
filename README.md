Overview

This project demonstrates the design, configuration, and validation of a cloud-based identity and access management (IAM) environment using Microsoft Entra ID (Azure AD) and Azure Role-Based Access Control (RBAC). The lab enforces strong authentication, least-privilege authorization, and modern security controls using Conditional Access policies, MFA, group-based administration, and subscription-level RBAC.

Lab Environment

Tenant Name: InnoLab

Tenant Domain: innolab455.onmicrosoft.com

Identity Platform: Microsoft Entra ID (Azure AD)

Subscription: Subscription 1

License: Microsoft Entra ID P2

Users: HR, IT, IAM Admin, Global Admin (break-glass)

Security Model: Zero Trust (MFA + Conditional Access + RBAC)

## 1. Microsoft Entra ID Tenant Setup

- Created and validated the InnoLab Entra ID tenant.

- Verified tenant ID, primary domain, licensing, and identity objects.

- Confirmed centralized identity management for users, groups, and applications.

# Screenshot:  
- 01-entra-overview.png


## 2. User Account Provisioning

- Created multiple cloud-only users to represent enterprise roles:

- Alex IT (Lab)

- IAM Admin (Lab)

- Sam HR (Lab)

- Innocent Udemba (Global Admin / Break-glass)

- Verified account status, object IDs, and sign-in readiness.

# Screenshots:

- 02-users-list.png

- 03-user-details-samhr.png


## 3. Security Group Design

- Created role-based security groups to support scalable access control:

- HR-Users

- IT-Users

- Privileged-Admins

- Assigned users to groups based on job function rather than direct permissions.

# Screenshot:

- 04-groups-list.png


## 4. Privileged Access Group Management

- Added IAM Admin (Lab) to the Privileged-Admins security group.

- Used group-based administration to simplify enforcement of elevated security policies.

# Screenshot:

- 05-privileged-admins-members.png


## 5. Authentication Methods Configuration

- Enabled secure authentication methods aligned with modern security standards:

- Microsoft Authenticator

- Software OATH tokens

- Temporary Access Pass (TAP)

- Email OTP

- Disabled weak or legacy methods such as SMS and voice calls.

# Screenshot:

- 06-authentication-methods.png


## 6. Conditional Access – MFA for All Users

- Created Conditional Access policy CA – Require MFA – All Users.

- Scope:

  - Include: All users

  - Exclude: Break-glass admin account

- Grant control:

   - Require multi-factor authentication

- Policy deployed in Report-only mode for validation.

# Screenshot:

- 07a-ca-mfa-policy-users-include.png

- 07b-ca-mfa-policy-users-exclude.png

- 07c-ca-mfa-policy-grant.png

- 07d-ca-mfa-policy-report-only.png


## 7. MFA Registration Enforcement Validation

- Signed in as a standard user (Sam HR).

- Verified Microsoft Entra ID prompted for Microsoft Authenticator enrollment.

- Confirmed MFA enforcement was triggered by Conditional Access evaluation.

# Screenshot:

- 09-mfa-registration-prompt.png


## 8. Conditional Access – Admin MFA Enforcement

- Created Conditional Access policy CA – Admins – MFA Always.

- Scope:

  - Applied to Privileged-Admins group only

- Enforced MFA for all admin sign-ins regardless of application.

# Screenshot:

- 10-ca-admins-mfa.png
  

## 9. Conditional Access – Block Legacy Authentication

- Created Conditional Access policy CA – Block Legacy Authentication.

- Blocked legacy protocols vulnerable to credential-based attacks (POP, IMAP, SMTP AUTH).

- Applied to all users and all cloud apps.

# Screenshot:

- 11-ca-block-legacy-auth.png


## 10. Entra ID Administrative Role Assignment

- Assigned User Administrator directory role to Alex IT (Lab).

- Enabled delegated identity management without granting full tenant control.

# Screenshot:

- 12-entra-role-user-admin.png


## 11. Azure RBAC – Subscription-Level Authorization

- Configured Azure RBAC roles at the subscription scope:

- Innocent Udemba → Owner

- Alex IT (Lab) → Reader

- Ensured separation between identity administration and resource management.

# Screenshot:

- 13-azure-rbac-reader.png


## 12. Authorization Enforcement Validation (Least Privilege)

- Attempted to create a resource group as Alex IT (Lab).

- Operation failed due to insufficient permissions.

- Confirmed Azure RBAC correctly enforced least-privilege access.

# Screenshot:

- 14-rbac-access-denied.png
