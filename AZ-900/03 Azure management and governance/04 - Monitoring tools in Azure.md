# Azure Advisor

- **What:** Free tool in the Azure portal that checks your resources and gives **recommendations** (act, postpone, or dismiss).
- **Doesn't auto-fix**, it only advises.

## 5 categories
1. **Reliability**: keep apps running
2. **Security**: threats and vulnerabilities
3. **Performance**: speed up apps
4. **Operational Excellence**: workflows and deployment
5. **Cost**: reduce spending

## Exam tip
Recommendations to cut cost, improve security or performance → **Azure Advisor**.


# Azure Service Health

- **What:** Tells you about the health of Azure itself and of the resources you run.
- Has **3 views**, from broad to narrow:

| View | Scope |
|---|---|
| **Azure Status** | **Global**: all services and regions |
| **Service Health** | **Your** services and regions: outages, planned maintenance, advisories (alerts can be set up) |
| **Resource Health** | **One resource** (e.g. a VM): is it healthy, and is the problem on Azure's side or yours |

## Exam tips
- Azure outage affecting **my** services/regions → **Service Health**
- Is **this VM** having a problem? → **Resource Health**
- Global Azure status page → **Azure Status**
- Gives links to support and keeps historical alerts.


# Azure Monitor

- **What:** Platform to **collect, analyze and act on** data (logs and metrics) from Azure, on-premises and multicloud.
- Data is stored centrally and shown through **dashboards, queries and alerts**.

## 3 key parts

| Part | What it does |
|---|---|
| **Log Analytics** | Portal tool to **write queries** on collected data (e.g. errors in the last hour) |
| **Alerts** | Notify you when a **condition** is met. Made of an **alert rule** (condition) + **action group** (who is notified / what happens) |
| **Application Insights** | Monitors **web app** performance and usage (Azure, on-prem or other cloud) |

## Details
- Alerts can be **metric-based** (e.g. VM CPU > 80%) or **log-based** (error patterns).
- **Action groups** are reusable across Azure Monitor, Service Health and Advisor.
- Application Insights is set up with an **SDK** in code or an **agent** (no code changes).
- It tracks request/response/failure rates, dependencies, page loads, users, and server CPU/memory.
- **Availability tests** send synthetic requests to check the app is responding.

## Exam tips
- Query logs → **Log Analytics**
- Notify when CPU is high → **Alerts**
- Monitor a web app's performance → **Application Insights**
- Collect and analyze metrics and logs → **Azure Monitor**