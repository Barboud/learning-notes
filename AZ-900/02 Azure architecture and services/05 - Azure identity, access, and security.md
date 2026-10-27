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