## Azure File Storage – Quick Summary

### ✅ What is it?
Azure File Storage is a fully managed file share service under the Azure Storage Account.

---

### 🧱 Requirements
- Must create a **Storage Account** first.
- Azure File Storage is a **sub-service** within that account.

---

### 📂 Purpose
- Provides **file sharing** and **file synchronization** across multiple Virtual Machines (VMs).
- Used when **multiple VMs host the same application** and need **simultaneous access to shared files**.

---

### ⚙️ Key Features
- Supports **SMB** and **NFS** protocols.
- Can be mounted on **Windows, Linux, macOS**, and **on-prem systems**.
- Ideal for **lift-and-shift** apps needing shared storage.
- Supports **Azure File Sync** for hybrid cloud setups.

---

### 🔐 Security
- Data encrypted **at rest and in transit**.
- Supports **Azure AD** and **NTFS ACLs**.

---

### ✅ Use Case Recap
> "You need a storage account to create Azure File Storage (a sub-core service). This is used for file shares and file sync among multiple VMs hosting the same app, so they can access shared files simultaneously with ease."

## 📦 Azure File Storage – Use Cases

### 1. ✅ File Sharing Between VMs
- Share files across multiple Azure VMs running the same application.
- Centralize logs, configs, media, or static data.

### 2. 🔁 Application Lift-and-Shift (Migration)
- Migrate legacy on-prem apps to Azure **without changing the file system dependencies**.
- Apps that rely on **file shares (SMB/NFS)** can continue to work with minimal or no code changes.

### 3. 🌐 Hybrid Cloud with Azure File Sync
- Sync Azure File shares with on-prem file servers.
- Keeps frequently accessed files local; uses cloud as central storage.
- Great for **branch offices** and **distributed teams**.

### 4. 🧪 Dev/Test Environments
- Multiple test VMs accessing the same data sets.
- Temporary, sharable file storage for staging environments.

### 5. 📂 Centralized Configuration & Assets
- Share application configuration files, static web assets, libraries, etc.
- Common in web farms or microservices accessing shared read/write files.

### 6. 🧩 Container Storage
- Mount file shares into containers (e.g., in **Azure Kubernetes Service**) when persistent, shared storage is needed.

## 📁 File Sharing Protocols in Azure File Storage

### ✅ SMB (Server Message Block)
- **Full Form**: Server Message Block
- **OS Compatibility**: Primarily used with **Windows OS**
- **Purpose**: File sharing over a network (files, printers, etc.)
- **Azure Support**: Azure File Storage supports SMB (v2.x & v3.x)
- **Typical Use Case**: Windows-based applications that need shared file access

---

### ✅ NFS (Network File System)
- **Full Form**: Network File System
- **OS Compatibility**: Primarily used with **Linux/Unix OS**
- **Protocol Version**: Azure supports **NFS v4.1**
- **Purpose**: File sharing over a network in Linux environments
- **Azure Support**: Azure File Storage supports NFS (Premium tier required)
- **Typical Use Case**: Linux-based applications or HPC workloads

---

### 🧠 Summary
> **SMB is the standard file sharing protocol for Windows**, while **NFSv4 is commonly used in Linux systems**. Azure File Storage supports both, allowing seamless file sharing across different OS environments.

## 🆚 EFS vs Azure File Storage – Do You Need a VM?

### 📌 AWS EFS
- Uses **NFSv4.1** protocol.
- No VM needed — fully managed by AWS.
- Mount directly to EC2 instances.

### 📌 Azure File Storage
- Supports **SMB** and **NFSv4.1** (Premium only).
- **No dedicated VM needed**.
- File shares are created inside a **Storage Account**.
- Mountable from Azure VMs, on-prem servers, or containers.

---

### ✅ Conclusion
> In both AWS and Azure, you don’t need to create a dedicated VM to act as the file server. The file share is a **fully managed service** created at the cloud platform level (EFS or Storage Account).

## 📂 Azure File Storage – Access Tiers

After creating a **Storage Account**, when creating a new **File Share**, you must choose an **Access Tier** based on your performance and cost needs.

---

### 🧱 1. Premium (SSD-backed)
- Backed by **solid-state drives (SSD)**
- **High throughput**, **low latency**
- Best for:
  - IOPS-intensive workloads
  - Databases, VMs requiring fast access
- 💰 Higher cost, higher performance

---

### 🔄 2. Transaction Optimized (HDD-backed)
- Designed for **frequent access** with **optimized costs**
- Balances **reasonable performance** with **cost-efficiency**
- Best for:
  - General-purpose file shares
  - Workloads with frequent small transactions
- 💡 *"Best of both worlds"* — decent performance with lower cost

---

### 🔥 3. Hot Tier
- Optimized for **frequent access**
- Lower latency than cool, but not as fast as Premium
- Best for:
  - Active datasets accessed regularly
- 💰 Cost: Medium

---

### ❄️ 4. Cool Tier
- Optimized for **infrequently accessed** data
- Higher latency, lower performance
- Best for:
  - Backup, archive scenarios
- 💰 Lowest cost, highest latency

---

### ✅ Summary
> **Transaction Optimized** is the ideal middle ground — offering decent performance for apps that access files frequently but don’t require ultra-low latency.

## ♻️ Azure File Share – Soft Delete

### ✅ What is Soft Delete?
Soft Delete is a **data protection feature** that allows you to **recover accidentally deleted files or shares** within a retention period.

---

### 🛡️ Key Points:
- When enabled, **deleted file shares are not permanently removed** immediately.
- Instead, they are **retained in a hidden recovery state** for a **configurable retention period** (1 to 365 days).
- Users can **recover** deleted shares during this time.
- After the retention period, data is **permanently deleted**.

---

### 🧭 Where is it configured?
- Go to your **Storage Account** → **Data Protection** blade.
- Enable **Soft Delete for File Shares**.
- Set the **retention period** (e.g., 7, 30, or 90 days).

---

### 🧠 Why Use It?
> Prevents **accidental loss** of critical file data and gives admins the ability to **restore deleted shares** quickly without backup dependencies.

## 🚫 SMB Connection Blocked by ISP – Why Azure File Share Won’t Work

### ❗ Problem:
- **SMB (Server Message Block)** protocol uses **TCP port 445**
- Many **ISPs block outbound port 445** to prevent malware attacks (like WannaCry)
- As a result, your **Windows machine can't connect to Azure File Shares over the public internet**

---

### 🔍 How to Confirm:
Run the following in PowerShell:

Test-NetConnection <storage-account-name>.file.core.windows.net -Port 445

## 🔢 SMB Default Port

### 📦 Protocol: SMB (Server Message Block)

- **Default Port**: `TCP 445`
- **Purpose**: Used for **file sharing**, **printer sharing**, and **network communication** on Windows networks
- **Azure Usage**: Required to **mount Azure File Shares** using SMB

---

### ⚠️ Note:
- **Port 445 must be open** on outbound connections to access Azure File Storage via SMB.
- Many **ISPs block port 445** for security reasons (especially on residential networks).

---

### ✅ Tip:
To test if your system can access SMB over port 445:

Test-NetConnection <storage-account-name>.file.core.windows.net -Port 445

## 🛠️ Edit Quota – Azure File Share

### 📌 What does it mean?
**Editing quota** allows you to **change the storage capacity limit** of an individual Azure File Share.

---

### 📂 Quota Details:
- Defined in **GiB (Gibibytes)**
- Represents the **maximum size** the file share can grow to
- Helps in **cost control** and **storage allocation management**

---

### 🧭 How to Edit:
1. Go to your **Storage Account**
2. Click on **File Shares**
3. Select a file share → Click **"Edit Quota"**
4. Enter the new size in GiB → Save

---

### 🔒 Note:
- The **quota doesn’t affect performance**, only **limits the maximum storage** used.
- Applicable to **standard** and **premium** file shares.

---

### ✅ Example:
> If you set a quota of **200 GiB**, the file share can hold up to 200 GiB of data. If more is written, writes will fail until space is freed or quota is increased.

## 📦 Azure Storage Account – Multiple Sub-Core Services Support

### ✅ Statement:
> A **single Azure Storage Account** supports **multiple sub-core storage services** simultaneously.

---

### 🧱 Sub-Core Services Supported:

1. **Blob Storage** – For storing unstructured object data (images, videos, logs, etc.)
2. **File Storage** – For file shares via SMB/NFS
3. **Queue Storage** – For decoupled messaging between services
4. **Table Storage** – For NoSQL key-value data
5. **Data Lake Gen2** – Hierarchical namespace over Blob (if enabled)

---

### 🧠 Summary:
> You **do not need separate storage accounts** for Blob, File, Queue, or Table.  
> **One storage account** can handle them all under a unified namespace and billing unit.

## 🔁 Azure File Sync – What Is It?

### ✅ Definition:
**Azure File Sync** is a **cloud service** that allows you to **synchronize** file data between:

- Your **on-premises Windows Server** (or Azure VM acting as a file server)  
**and**  
- An **Azure File Share** (in a Storage Account)

---

### 🔧 Key Features:
- Keeps files **in sync** across on-prem servers and Azure
- Supports **cloud tiering** (hot files on-prem, cold files in cloud)
- Enables **multi-site sync** (multiple branch servers sync to the same file share)
- Allows **centralized backup & disaster recovery** through Azure

---

### 🧠 Summary:
> **Azure File Sync is a cloud service**, not software you buy —  
> You install its **agent** on a Windows Server, but the **sync intelligence and control lives in Azure**.

















