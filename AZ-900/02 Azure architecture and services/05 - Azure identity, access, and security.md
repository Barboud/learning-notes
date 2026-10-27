# Azure directory services

# Azure Identity & Access Security — Directory Services

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


# Azure authentication methods


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


# Azure external identities

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