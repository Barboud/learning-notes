# Azure directory services

# 1. Azure Identity & Access Security — Directory Services

## 1. Active Directory Domain Services (AD DS)
- Traditional directory service, usually running on Windows Server.
- Manages users, computers, groups, and domains.
- Supports LDAP, Kerberos, NTLM, and Group Policy.
- Requires managing Domain Controllers.
    

## 2. Domain Controller (DC)
- A server running AD DS.
- Authenticates users and manages domain resources.
    

## 3. Microsoft Entra ID
- Microsoft's cloud-based identity and access management service.
- Manages access to Azure, Microsoft 365, and other applications.
- Supports MFA, SSO, and Conditional Access.
- Formerly called Azure Active Directory (Azure AD).
    

## 4. Microsoft Entra Connect
- Synchronizes identities between on-premises AD DS and Microsoft Entra ID.
- Used in hybrid environments.
    

## 5. Microsoft Entra Domain Services
- Provides managed traditional domain services in Azure.
- Microsoft manages the Domain Controllers.
- Supports LDAP, Kerberos, NTLM, domain join, and Group Policy.
- Useful for legacy applications that require traditional domain functionality.
- Synchronization flows from Entra ID to Domain Services (one-way).
    

## Key Terms

- **Authentication:** Verifies who you are.
- **Authorization:** Determines what you can access.
- **MFA:** Requires multiple authentication factors.
- **SSO:** One sign-in provides access to multiple applications.
- **Conditional Access:** Applies access rules based on conditions.
- **LDAP:** Protocol for accessing directory information.
- **Kerberos:** Authentication protocol.
    

## Exam — Remember These
- Cloud identities → **Microsoft Entra ID**
- Traditional Windows domain → **AD DS**
- Server running AD DS → **Domain Controller**
- Synchronize on-premises AD DS with Entra ID → **Entra Connect**
- Managed domain services in Azure → **Entra Domain Services**
- Legacy application requiring LDAP/Kerberos → **Entra Domain Services**
- One sign-in for multiple apps → **SSO**
- Extra authentication factors → **MFA**


# 2. Azure authentication methods


## 1. Authentication
Verifies who you are.
## 2. Single Sign-On (SSO)
## 3. Multifactor Authentication (MFA)
**Remember:** MFA protects accounts even if the password is compromised.

## 4. Passwordless Authentication
Sign in without a password.
Microsoft Entra ID supports:
- **Windows Hello for Business:** PIN or biometrics on a trusted device.
- **Microsoft Authenticator:** Phone-based approval.
- **FIDO2 security keys:** Hardware security keys.
    

## Exam — Remember
- Sign in once for multiple apps → **SSO**
- Extra authentication factors → **MFA**
- No password required → **Passwordless authentication**
- Fingerprint or face → **Something you are**
- Phone or security key → **Something you have**
- Password or PIN → **Something you know**


# 3. Azure external identities

Main idea: External Identities allow people outside your organization to access your apps and resources securely.

### What to remember

- Microsoft Entra External ID: Manages identities for external users.
    
- B2B collaboration: Invite external users, such as business partners or guests, to access your organization's resources using their own identities.
    
- B2C / customer identity: Lets customers sign in to your applications. Microsoft’s current terminology and product offerings distinguish customer identity scenarios from workforce B2B collaboration.
    

Memory trick: B2B = business guests. Customer identity = people using your app.

### Three types to memorize

|Type|Purpose|
|---|---|
|B2B collaboration|Guest users access your organization's apps and resources.|
|B2B direct connect|External users collaborate through Teams shared channels without guest accounts in your directory.|
|External ID for customers|Customers sign in to your applications.|

Also remember: Access reviews help verify whether guests still need access and remove access when it's no longer required.


# 4. Azure conditional access

## What is it?
Conditional Access is a Microsoft Entra ID feature that allows or blocks access based on signals such as user, location, device, and application.

## How it works

**Signals → Decision → Enforcement**
- **Signals:** User, location, device, application.
- **Decision:** Evaluate security requirements.
- **Enforcement:** Allow access, require MFA, or block access.
    

## Exam Examples

|Scenario|Action|
|---|---|
|Admin signs in|Require MFA|
|Sign-in from an unusual location|Require MFA or block|
|Unmanaged device accesses a sensitive app|Block or restrict access|

## Remember

- Part of **Microsoft Entra ID**.
- Uses signals to make access decisions.
- Can allow access, require MFA, or block access.
    

**Memory trick:** Conditional Access = Check conditions, then allow, challenge, or block.

# 5. Azure role-based access control (RBAC)

## What is it?
Azure RBAC manages **who can access Azure resources and what they can do**.

## Key Concepts
- **Principle of Least Privilege:** Grant only the permissions needed to do a task.
- **Role:** Defines permissions (e.g., Owner, Contributor, Reader).
- **Scope:** Where the permissions apply.
    

## Built-in Roles
|Role|Permissions|
|---|---|
|**Owner**|Full access + can assign roles|
|**Contributor**|Create and manage resources, but cannot assign roles|
|**Reader**|View resources only|

## Scope Hierarchy
From broadest to narrowest:
1. Management Group
2. Subscription
3. Resource Group
4. Resource
    
**Important:** Permissions assigned at a parent scope are inherited by child scopes.

## Remember for the Exam
- Azure RBAC follows the **least privilege** principle.
- RBAC uses an **allow model**: permissions from multiple role assignments combine.
- Azure RBAC controls actions on Azure resources through **Azure Resource Manager**.
Azure Resource Manager (ARM) manages Azure resources, while Azure RBAC checks whether a user has permission to perform an action on those resources.
- RBAC does not control access inside an application's own data; the application handles that.
    

**Memory trick:** RBAC = Who + What permissions + Where (scope).

# 6. Zero Trust model
Zero Trust is a security model based on **"Never trust, always verify."**

## Three Principles
1. **Verify explicitly:** Always verify identity and access using available signals.
2. **Use least privilege access:** Give users only the minimum permissions they need. 
3. **Assume breach:** Assume attackers may already be inside the network and minimize potential damage.
    

## Remember for the Exam
- Never automatically trust users or devices, even inside the corporate network.
- Verify every access request.
- Use **MFA**, Conditional Access, and **RBAC** to help enforce Zero Trust.
- Zero Trust is a **security strategy**, not a single product.


**Memory trick:** Verify explicitly + Least privilege + Assume breach.

# 7. Defense-in-depth
Defense-in-depth is a security strategy that uses **multiple layers of protection** to protect resources. If one layer fails, other layers can still help prevent an attack.

## Security Layers
- **Physical security:** Protect datacenters and hardware.
- **Identity and access:** MFA, RBAC.
- **Perimeter:** Firewalls and network protection.
- **Network:** Network segmentation.
- **Compute:** Secure virtual machines and servers.
- **Application:** Secure applications.
- **Data:** Encryption and access controls.
    

## Remember for the Exam
- Uses **multiple layers of security**.
- Protects against attacks by avoiding reliance on a single security control.
- Layers help protect **data, applications, networks, compute, identity, and physical infrastructure**.
    
**Memory trick:** Defense-in-depth = Multiple security layers; if one fails, others help protect you.

# 8. Encryption and key management in Azure