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

