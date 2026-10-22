# Microsoft Purview

### Easy way to remember it

- **Purview = “Where is my data, what is it, and is it safe and compliant?”**
- **Risk & compliance** = protect data and follow the rules.
- **Data governance** = map, understand and control all your data.

### Likely exam angles

- Purview works across **on-premises, multicloud, and SaaS**, not just Azure.
- Know the **two areas**: risk and compliance, and unified data governance.
- Know the **three capabilities**: discovery, classification, lineage.
- Don’t confuse it with **Microsoft Defender for Cloud** (security posture and threat protection for your resources) or **Azure Policy** (rules for resource configuration). Purview is about **data**, not resources.


# Azure Policy

### What it is

- Azure Policy is a service for creating, assigning and managing rules that control or audit your Azure resources.
- It keeps resource **configurations** compliant with your standards. It helps with governance, security, compliance and cost control.
- It can **audit** (flag non-compliant resources) and **prevent** (block non-compliant resources from being created).

### Policy vs RBAC (a favourite exam trap)
**RBAC** stands for **Role-Based Access Control**.

||Azure Policy|RBAC|
|---|---|---|
|Focus|**Resource properties** (“what is allowed to exist”)|**User actions** (“who can do what”)|
|Example|“VMs may only be in West Europe”|“Salem can create VMs”|

A user can have permission to create a VM (RBAC) and still be blocked by a policy (for example, a forbidden VM size).

### Building blocks

1. **Policy definition** says what should happen. It has a **condition** (if) and an **effect** (then).
    - Effects include: deny, audit, append, modify.
    - Typical examples: allowed locations, allowed resource types, allowed SKUs/VM sizes, required or inherited tags.
    - Both **built-in** and **custom** definitions are supported.
2. **Initiative** is a **group of related policy definitions** for one bigger goal.
    - Example: “Enable Monitoring in Azure Security Center” contains over 100 policies, such as unencrypted SQL, OS vulnerabilities, and missing endpoint protection.
3. **Assignment** applies a policy or initiative to a **scope**.
    - Scopes: **management group → subscription → resource group → resource**.

**Memory trick:** Definition = the rule. Initiative = a bundle of rules. Assignment = where the rule applies.

### Inheritance and exclusions

- Policies are **inherited downward**. A policy set on a resource group applies to everything inside it, including new resources.
- You can **exclude** certain scopes or mark resources as exceptions, so you keep full control.

### When it is checked

- When a resource is **created** or **updated**.
- When you **resize** (for example, a VM).
- For **existing resources**, which are evaluated and flagged even if they were created before the policy existed.
- **Remediation** can fix some non-compliant resources automatically. For example, a policy can add a missing `AppName` tag.

### Extras worth knowing

- Built-in definitions cover Storage, Networking, Compute, Security Center and Monitoring.
- It integrates with **Azure DevOps** CI/CD pipelines (pre- and post-deployment).
- It enforces your standards even for changes proposed by Copilot or automation, such as allowed locations, required tags and approved SKUs.

### Quick exam checklist

- Policy controls **resource configuration**. RBAC controls **user permissions**.
- Initiative = **group of policies**.
- Policies can be assigned at **management group, subscription, resource group, or resource** level, and they **inherit downward**.
- It evaluates **existing** resources too, not just new ones.
- It can **deny, audit, append, modify**, and **remediate**.
- Don’t confuse it with **Purview** (data governance), **Defender for Cloud** (security posture and threats), or **resource locks** (prevent deletion or modification).


# Resource locks

- Designed to **prevent accidental deletion** and/or **modification**
- Used in conjunction with RBAC
- Two types of locks
    - **Read-only** (**ReadOnly**) – only read actions are allowed
    - **Delete** (**CanNotDelete**) – all actions except delete are allowed
- Scopes are **hierarchical** (**inherited**)
    - Subscriptions > Resource Groups > Resources
- **Management Groups** can’t be locked
- Only **Owner** and **User Access Administrator** roles can manage locks (**built-in** roles)


# Service Trust portal
It’s Microsoft’s public library of proof that its cloud is secure, private and compliant. If your company or an auditor asks “how do you know Azure is safe and follows the rules?”, this is where you look.


**Memory trick:** _Purview and Policy manage YOUR stuff. Service Trust Portal shows MICROSOFT’s proof._