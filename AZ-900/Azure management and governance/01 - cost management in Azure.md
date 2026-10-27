# Factors That Affect Your Azure Costs

## Key Cost Drivers

1. **Resource Type**  
   Costs vary based on the specific services and instances you deploy.

2. **Consumption**  
    Azure operates on a pay-as-you-go model; usage patterns directly impact pricing.

3. **Maintenance & Provisioning**  
    Unused or idle resources still incur charges as long as they remain allocated.

4. **Geography**  
   Infrastructure costs differ across various global Azure regions.

5. **Subscription Type**  
   Certain subscriptions offer cost benefits (e.g., the Free Tier includes select resources free for 12 months).

6. **Azure Marketplace**  
   Purchasing third-party solutions through the Marketplace charges you for the third-party software as well as the underlying Azure resources consumed.

---

## Network Traffic & Bandwidth

* **Inbound (Ingress):** Data coming into Azure (e.g., uploading data from your local computer to an Azure resource) is generally **free**.
* **Outbound (Egress):** Data leaving Azure costs money. This is billed as **bandwidth**, and pricing depends on the **Billing Zone**.

> [!NOTE]
> **Billing Zone ≠ Availability Zone**  
> A **Billing Zone** is a collection of geographic regions grouped by Microsoft specifically for data-transfer pricing.
> 
> * **Zone 1:** Includes North America and Europe (e.g., West Europe in Amsterdam).

---

## Azure Pricing Options Compared

| Option | Description | Best For | Potential Savings |
| :--- | :--- | :--- | :--- |
| **Pay-As-You-Go** | No upfront commitment; standard rates. | Unpredictable or short-term workloads | Baseline |
| **Reservations** | 1-year or 3-year commitment for a specific resource type. | Stable, predictable workloads | Up to 72% off |
| **Savings Plan** | 1-year or 3-year commitment to a fixed hourly compute spend. | Steady compute needs requiring high flexibility | Up to 65% off |
| **Spot Pricing** | Purchase unused Azure capacity at significant discounts; subject to eviction if Azure needs capacity. | Fault-tolerant, flexible, or batch workloads | Deep discounts |

### Analogy Breakdown

* **Reservations:** **Locking in a Specific Resource** (like reserving a designated parking spot for a specific car).
* **Savings Plan:** **Locking in a Specific Spend Amount** (like committing to spend a set amount on parking, regardless of which spot you use). Only for compute.


# Azure Pricing Calculator:

  • Estimates cost of specific Azure services (VMs, storage, databases) before deployment.

  • Configures regions, tiers, usage hours, and discounts.



# Microsoft Cost Management

* **Purpose**: Analyze, monitor, and optimize Azure spend.

## Core Features >>>> focus here
1. **Cost Analysis**: Visual insights on spending by region, resource, subscription, or period.
2. **Cost Alerts**:
   * **Budget**: Triggers when spend crosses user-defined limits.
   * **Credit**: Auto-alerts at **90%** and **100%** of Azure Prepayment (EA).
   * **Department Quota**: Alerts when EA department spending hits set limits.
3. **Budgets**: Set spending limits + trigger automated actions (e.g., auto-shutdown idle dev VMs).


# Azure Resource Tags

- Tags are name:value pairs (metadata) used to organize resources, e.g. `Environment : Prod`
- Can be applied to resources, resource groups and subscriptions
- Resources **don't inherit** tags from subscriptions or resource groups
- Can be applied with Portal, CLI, PowerShell, Azure Resource Manager (ARM) Templates / Bicep, Terraform
- Azure Policy can enforce tagging rules (require, add or inherit tags)
- Tags don't trigger actions by themselves. Automation (Policy, Logic Apps, Functions, Automation runbooks) can use tags to select resources and act on them
- Limit: 50 tags per resource
- Don't store secrets in tags (they are visible in billing and logs)

# Azure Resource Manager (ARM) Templates

- JSON files that define Azure resources (Infrastructure as Code)
- Declarative and repeatable: same template, same result
- Sections: parameters, variables, resources, outputs
- Bicep is a simpler language that compiles to ARM