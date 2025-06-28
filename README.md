# Azure-cloud-journey
A comprehensive documentation of my learning journey and hands-on experience with Microsoft Azure Cloud. This repository includes step-by-step guides, configurations, best practices, mini-projects, troubleshooting notes, and key concepts explored while building cloud-native solutions on Azure.

# Azure Cloud – Key Infrastructure Terms (Beginner Guide)

- **Geo**: A large geographical area (e.g., US, Europe) used to meet data residency and compliance needs.

- **Region**: A specific location within a Geo where Azure offers cloud services (e.g., Central India).

- **Availability Zone**: A group of separate datacenters within a region, designed for high availability and fault tolerance (minimum of 3 per supported region).

- **Data Center**: A physical facility that houses Azure’s computing infrastructure like servers and networking equipment.

- **Rack**: A storage unit inside a datacenter that holds servers and hardware in an organized setup.

- **Server**: A physical or virtual machine that provides computing resources for Azure services.

# Azure Core Concepts – Logical Structure and Governance

## 🧾 Tenant
A **tenant** is a container inside **Azure Active Directory** that stores:
- Identities (users, groups)
- Access policies
- Authentication settings
- App registrations

---

## 🧱 Management Group
To better manage multiple teams (Dev, Test, Prod), each with its own subscription, you use a **management group** to apply **policies and permissions** across all subscriptions **consistently and centrally**.

---

## 📦 Subscription
A **subscription** in Azure acts like a:
- **Workspace**: Where all Azure resources are deployed and managed
- **Billing boundary**: Tracks cost and usage per project or team

---

## 🗂 Resource Group
- **Resource groups** are **logical containers** used to organize and house Azure resources.
- A **resource can belong to only one resource group at a time**.

---

## ⚙️ Resource
A **resource** in Azure is **any service or component** you create and manage in the Azure environment, such as:
- Virtual Machines
- Storage Accounts
- Databases
- App Services
- Networking components

## 🧠 Azure Virtual Machines – Series vs. Size

When configuring a Virtual Machine (VM) in Azure, it's important to understand the difference between **series** and **size**:

### ✅ Size
**Size** refers to the **computational power and specifications** of the virtual machine. This includes:
- Number of **vCPUs**
- Amount of **RAM**
- **Storage throughput**
- **Network bandwidth**

The **size** determines the performance capabilities of the VM.

---

### ✅ Series
**Series** refers to the **category or family** of the VM, based on the **underlying physical hardware** and what the VM is **optimized for**. Each series is tailored for specific use cases:

- **D-series**: General-purpose workloads  
- **E-series**: Memory-intensive applications  
- **F-series**: Compute-optimized workloads  
- **N-series**: GPU-based workloads (e.g., AI, rendering)  
- **B-series**: Burstable workloads for cost savings

---

### 📌 Summary
- **Size = How powerful the VM is**
- **Series = What the VM is designed and optimized for**

## 🧱 Azure Resource Hierarchy

To manage and organize resources effectively, Azure follows a structured hierarchy:

1. **Azure Tenant**
   - The top-level identity boundary.
   - Created automatically when you sign up for Azure.
   - Manages users, groups, and access through Azure Active Directory.

2. **Management Groups**
   - Optional layer used to group multiple subscriptions.
   - Ideal for applying governance (policies, RBAC) across subscriptions at scale.

3. **Subscriptions**
   - Containers for deploying Azure resources.
   - Defines billing, quotas, and access control boundaries.

4. **Resource Groups**
   - Logical containers within a subscription.
   - Used to organize and manage related Azure resources.

5. **Azure Resources**
   - The actual services and components you create and use (e.g., VMs, storage accounts, databases).

---

### 📌 Visual Summary:

Tenant
└── Management Group
└── Subscription
└── Resource Group
└── Azure Resources

Note: An Azure image is a template that contains a pre-installed operating system

## Azure Cloud Shell: Bash vs PowerShell

When you click on **Azure Cloud Shell**, you're given two options:
- **Bash** (Azure CLI)
- **PowerShell** (Azure PowerShell)

### 💭 Which Should You Choose?

It depends on your **background** and **use case**. Here's a breakdown:

---

### ⚙️ Azure PowerShell

- **Preferred by**: Windows users, those comfortable with PowerShell scripting.
- **Cmdlets**: Uses `Az` module (e.g., `New-AzResourceGroup`).
- **Best for**: Complex scripting, especially if you're automating across Windows environments or integrating with PowerShell-based tooling.
- **Syntax style**: Verb-Noun (`Get-AzVM`, `Set-AzContext`)

---

### 🐚 Bash (Azure CLI)

- **Preferred by**: Linux/macOS users, DevOps engineers, developers.
- **Commands**: Uses `az` command-line tool (e.g., `az group create`).
- **Best for**: Lightweight tasks, quick interactions, scripting in shell scripts.
- **Syntax style**: Unix-style (`az vm list`, `az login`, `az group create`)

---

### ✅ Recommendation

- If you're comfortable with **PowerShell**, go for **Azure PowerShell**.
- If you prefer **Linux-style scripting or use Azure across platforms**, go for **Bash (Azure CLI)**.

Note:
1. `mstsc /v:PublicIP`  
   → Opens Remote Desktop Connection to a Windows VM using its **public IP address**.

2. `Install-WindowsFeature -Name Web-Server -IncludeManagementTools`  
   → Installs the **IIS Web Server** role along with its management tools on a Windows Server using PowerShell.

## 🛡️ Hardened VM Images

**Hardened VM Images** are **securely configured** virtual machine images that are designed to **minimize vulnerabilities** and reduce the **attack surface** of the system.

These images are pre-configured to:
- **Close unnecessary ports and services**
- **Apply latest security patches**
- **Enforce strong access controls and policies**
- **Disable insecure protocols**
- **Remove default or unused software**

### 🎯 Purpose:
To ensure the deployed VM has **no loopholes, weak spots, or misconfigurations** that could allow infiltration, malware injection, or unauthorized access.

---

### ✅ Use Cases:
- Environments handling **sensitive data**
- **Defense**, **government**, or **enterprise-grade** systems
- Systems needing **compliance** with security standards (e.g., CIS Benchmarks, NIST, ISO 27001)

---

### 🔐 Example:
A Linux VM hardened to comply with **CIS Level 1** baseline might:
- Disable root login over SSH
- Enforce password complexity
- Enable firewall (ufw/iptables)
- Remove unused packages and compilers

---

### 🧰 Tips for Hardening:
- Use tools like **Azure Security Center**, **Microsoft Defender for Cloud**, or **Ansible hardening roles**
- Regularly scan with **vulnerability assessment tools**
- Base custom images on **hardened golden images**

---

> ✅ Hardened images = "Secure-by-Design" foundation for your cloud infrastructure.

## 🔄 What is Deprovisioning?

Before capturing a custom image, you must **deprovision the VM**. This process:

- **Removes user-specific data** (usernames, SSH keys, logs)
- **Cleans up machine-specific settings**
- Prepares the VM for **general-purpose reuse**

### ✅ Purpose:
To ensure **clean, secure, and reusable** deployments from the captured image.

# ☁️ Cloud Computing Overview

## 💻 Types of Cloud Services (Service Models)

| Service Model | Full Form                    | Description                                                                 | Example Services                                   |
|---------------|------------------------------|-----------------------------------------------------------------------------|----------------------------------------------------|
| **IaaS**      | Infrastructure as a Service  | Provides virtualized computing resources over the internet.                 | AWS EC2, Microsoft Azure VM, Google Compute Engine |
| **PaaS**      | Platform as a Service        | Provides a platform allowing customers to develop, run, and manage apps.    | Google App Engine, Azure App Services, Heroku      |
| **SaaS**      | Software as a Service        | Delivers software over the internet, on a subscription basis.               | Gmail, Microsoft 365, Dropbox, Salesforce          |

> 🔁 **IaaS** = You manage the most (VMs, OS, apps)  
> 🔁 **PaaS** = You manage just your code and app logic  
> 🔁 **SaaS** = You only use the software

---

## 🏗️ Cloud Deployment Models

| Deployment Model | Description                                                                 | Usage Scenario                                      |
|------------------|-----------------------------------------------------------------------------|-----------------------------------------------------|
| **Public Cloud**  | Services delivered over the public internet and shared across users.        | Hosting websites, test/dev environments             |
| **Private Cloud** | Cloud infrastructure operated solely for a single organization.             | Sensitive data, regulated industries like finance   |
| **Hybrid Cloud**  | Combines public and private clouds for flexibility and optimization.        | Disaster recovery, burst workloads, data locality   |

---

## ✅ Summary

- **Service Models** define *what* you consume: Infrastructure, Platform, or Software.
- **Deployment Models** define *where* it runs: Public, Private, or Hybrid environment.

