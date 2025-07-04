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

## Azure Scaling Concepts

Azure supports two types of scaling:

### 1. Horizontal Scaling (Scale Out / Scale In)
- **Definition**: Adjusting the number of virtual machines.
- **Scale Out**: Add more VMs to handle increased load.
- **Scale In**: Remove VMs when demand decreases.
- **Best For**: Load-balanced applications, stateless services.

### 2. Vertical Scaling (Scale Up / Scale Down)
- **Definition**: Changing the size (resources) of an existing VM.
- **Scale Up**: Move to a VM with more CPU, RAM, or disk.
- **Scale Down**: Move to a smaller VM to save costs.
- **Best For**: Apps that require more compute but can't be distributed across multiple VMs.

## Virtual Machine Scale Sets (VMSS)

**Virtual Machine Scale Sets** is an Azure service used to perform both **horizontal** and **vertical** scaling of virtual machines.

In a VMSS unit, you can define **autoscaling rules** to handle changing workloads automatically.

### How It Works:
- When traffic enters your application, a **load balancer** distributes it across existing VM instances.
- As traffic increases, **CPU utilization** rises, potentially degrading performance.
- To prevent this, a **trigger** activates based on the autoscaling rule.
- Depending on traffic, the rule may:
  - **Scale out**: Add more VM instances.
  - **Scale in**: Remove VM instances to optimize cost and performance.
- These newly created instances are automatically added to the **backend pool** of the **Standard Load Balancer**, which now distributes traffic equally across the updated group of VMs.

## VMSS and Load Balancer Integration

In Azure, **Virtual Machine Scale Sets (VMSS)** can be used:

- ✅ **With a Load Balancer**:  
  - Ideal for distributing incoming traffic evenly across VM instances.
  - Supports both **internal** and **public** load balancers.

- ✅ **Without a Load Balancer**:  
  - Suitable for background tasks, batch processing, or internal-only workloads.
  - VM instances can still be accessed directly (e.g., via private IP or custom networking).

> 💡 Using a Load Balancer with VMSS is optional and depends entirely on the application's architecture and traffic requirements.

If you're unable to connect to your Azure VM, you can use the **Redeploy** option to move the VM to a new host (physical server) in the Azure datacenter.

If your virtual machine is in a failed state, you can use the **Reapply** option to re-run the VM's configuration and restore its settings.
The **Reapply** option is used to change the VM's state from **Failed** back to **Running** by reapplying its configuration.

Redeploy is used when you're unable to connect to your virtual machine; it moves the VM to a new physical host within the same Azure datacenter to resolve underlying hardware or host-level issues.

An Azure virtual machine must have at least one **virtual Network Interface Card (vNIC)** to enable network communication.
The underlying physical server of course has real NICs, but from the VM's perspective, you're working with virtual NICs that are mapped and managed by Azure’s virtualization layer.

## Note
In AWS, you need to allocate and associate an Elastic IP for a static public IP.
In Azure, if you don't specify otherwise, the public IP is static and private IP is dynamic, though you can configure either to be static.

If a virtual machine is facing issues, you can use **Boot Diagnostics** and the **Serial Console** to troubleshoot startup and OS-level problems.
These tools help when the VM is not accessible via RDP or SSH — especially useful for debugging boot errors, OS crashes, or misconfigured startup scripts.

**Boot Diagnostics** is a troubleshooting tool that captures logs and takes a **screenshot of the VM's boot process**, helping identify issues during startup.

**Serial Console** is another way to troubleshoot a virtual machine, providing direct access to the VM's console without requiring internet connectivity.

With the help of the **Azure Guest Agent**, you can reset the username and password of a virtual machine from the Azure portal.

# 📦 Azure Blob Storage: Types of Blobs

Azure Blob Storage supports **three types of blobs**, each designed for specific data access and storage needs.

---

## 1️⃣ Block Blob

- 💡 **Mainly used for:** Storing **unstructured data** like images, videos, documents, and backups.
- 📦 Data is **divided into blocks** when uploaded.
- 🏷️ Each block is **uniquely named and indexed** for tracking.
- 🔁 During **retrieval**, Azure **reassembles the blob** block by block in correct order.
- 📈 **Ideal for:** Large files, media content, documents, backups.

---

## 2️⃣ Append Blob

- 💡 **Mainly used for:** **Appending data only**, without overwriting existing content.
- ➕ You can only **add (append)** to the end of the blob.
- ❌ You **cannot modify or delete** previous content.
- 📈 **Ideal for:** Logging, telemetry data, audit trails.

---

## 3️⃣ Page Blob

- 💡 **Mainly used for:** Simulating a **physical hard drive**.
- 📄 Data is stored in **512-byte pages**.
- 🧠 Optimized for **random read/write I/O**.
- 🖥️ Used internally to store **Virtual Hard Disks (VHDs)** for Azure Virtual Machines.
- 📈 **Ideal for:** OS and Data disks, custom VHDs, database workloads.

---

## 🧾 Summary Table

| Blob Type       | Use Case Description                              | Best For                            |
|------------------|---------------------------------------------------|--------------------------------------|
| **Block Blob**   | Unstructured data, split into blocks              | Images, videos, documents, backups   |
| **Append Blob**  | Append-only data model (no overwrites)            | Logs, telemetry, audit trails        |
| **Page Blob**    | 512-byte page structure for random access         | VM Disks (VHDs), databases, IOPS-heavy workloads |

---

> ✅ Choose the blob type based on your data pattern:  
> Use **Block Blobs** for general file storage, **Append Blobs** for logs, and **Page Blobs** for virtual disks!

# 🌡️ Azure Blob Storage Access Tiers

Azure Blob Storage offers multiple **access tiers** to balance **cost** and **data access frequency**.

---

## 🔥 1. Hot Tier

- 💡 **Best for**: Frequently accessed data
- 📁 Examples: Web content, databases, real-time logs
- 💰 **Higher storage cost**, but **low access/read/write cost**
- ⚡ Fastest access speed

---

## 🧊 2. Cool Tier

- 💡 **Best for**: Infrequently accessed data (but still needs fast retrieval)
- 📁 Examples: Monthly backups, older app data, long-term project files
- 💰 **Lower storage cost** than Hot, **higher access/read cost**
- 🕒 Ideal for data accessed once every 30+ days

---

## 🧊❄️ 3. Cold Tier *(newer tier in preview or region-limited)*

- 💡 **Best for**: Rarely accessed data, but cheaper than Cool and faster than Archive
- 📁 Examples: Cold backups, legal hold data, seldom-used compliance files
- 💰 **Cheaper than Cool**, retrieval latency in hours, not seconds

---

## 🧊 4. Archive Tier

- 💡 **Best for**: Archival data — data you almost never access
- 📁 Examples: Compliance records, medical data, historical logs
- 💤 **Very low storage cost**, **very high access cost**
- ⏳ Data must be **rehydrated** (unarchived) before access (can take hours)

---

## 🧾 Comparison Table

| Tier     | Access Frequency    | Storage Cost | Access Cost | Retrieval Time |
|----------|---------------------|---------------|--------------|-----------------|
| **Hot**     | Frequent              | High          | Low          | Immediate       |
| **Cool**    | Infrequent (30+ days) | Medium        | Medium       | Immediate       |
| **Cold**    | Rare (90+ days)       | Low           | High         | Minutes to hours|
| **Archive** | Rare (180+ days)      | Lowest        | Highest      | Hours (rehydration) |

---

## 📌 Key Notes

- ✅ You can **change tiers** at any time (e.g., Hot → Archive)
- 🔁 **Lifecycle Management Policies** can automatically move blobs between tiers
- 📂 All tiers are only available for **Block Blobs**

---

> 💡 Choose the **tier** based on **how often** you need the data and how long you're storing it.

# Azure Storage Replication — Core Concept

Azure Storage automatically replicates your data to ensure durability, availability, and redundancy. This forms the foundation of a robust disaster recovery strategy.

The entire concept revolves around data duplication — making multiple copies of your data and spreading them across different fault domains, such as:

- Within the same data center (LRS)
- Across availability zones (ZRS)
- Across geographically distant regions (GRS/GZRS)

---

## Why It Matters

This redundant architecture ensures:

- Your data remains safe and recoverable even in the event of:
  - Hardware failures
  - Network outages
  - Natural disasters
  - Zone or regional outages

- Enables business continuity with minimal to no data loss, depending on the replication strategy chosen.

---

## Summary

**“Azure Storage Replication is all about strategically duplicating your data and placing it in separate physical and geographical locations to guard against unforeseen failures. It's the backbone of a resilient, enterprise-grade disaster recovery setup.”**

---

## Replication Options

| Replication Type | Scope                        | Description                                              |
|------------------|------------------------------|----------------------------------------------------------|
| LRS              | Single Data Center           | Locally redundant storage (3 copies in one facility)     |
| ZRS              | Multiple Zones in One Region | Zone-redundant storage                                   |
| GRS              | Primary + Secondary Region   | Geo-redundant storage (replication to distant region)    |
| GZRS             | Zones + Geo                  | Combines zone and geo redundancy                         |
| RA-GRS / RA-GZRS | Read Access Geo              | Allows read-only access to data in the secondary region  |

---

## Conclusion

Azure Storage Replication is an essential part of any cloud-based disaster recovery strategy. It ensures your data is not a single point of failure and supports high availability and resilience across different failure scenarios.
