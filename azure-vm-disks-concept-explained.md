## 🧱 Types of Disks in Azure Virtual Machines

1. **Operating System Disk**  
   → Contains the **OS installation** (e.g., Windows Server or Linux). It's a **managed disk**, persistent, and created from the selected image when the VM is deployed.

2. **Data Disk**  
   → Additional **persistent storage** used to store application data, databases, logs, or files. You can attach multiple data disks to a VM as needed.

3. **Temporary Disk**  
   → A **non-persistent disk** (usually D:\ on Windows VMs) used for temporary storage (e.g., page files or cache). Data on this disk is **lost when the VM is stopped/deallocated** or moved.

## 🧩 Disk Usage Summary in Azure Virtual Machines

- **Operating System Disk**  
  → Contains the OS files and system configurations. This disk is managed by Azure, and you typically **don’t modify it directly** beyond installing software or updates.

- **Data Disk**  
  → Ideal for storing **personal data, databases, logs, or any sensitive information**. It is **persistent**, safely stored in Azure Storage, and remains intact even if the VM is stopped or restarted.

- **Temporary Disk**  
  → Used for **ephemeral storage** like swap files or caches. This disk is **not safe for critical data**, as contents are **erased if the VM is stopped, deallocated, or moved to another host**.

## 🚀 Azure Disk Performance Tiers

1. **Standard HDD**  
   → Cost-effective and suitable for **low-performance workloads** like dev/test or infrequent access.  
   - **Use case**: Backup servers, rarely accessed data  
   - **Performance**: Lower IOPS and throughput

2. **Standard SSD**  
   → Balances cost and performance for **general-purpose workloads** with consistent latency.  
   - **Use case**: Web servers, lightly used apps  
   - **Performance**: Better than HDD, but not ideal for high I/O

3. **Premium SSD**  
   → High-performance SSDs designed for **IO-intensive, production-grade workloads**.  
   - **Use case**: Databases, large-scale apps, transaction-heavy systems  
   - **Performance**: High IOPS, low latency, suitable for critical workloads

## 🖼️ What Happens When You Use an Azure Image?

An image is essentially a **VHD (Virtual Hard Disk)** containing a **pre-installed operating system** and optional **configurations or software**.

When you deploy a VM using that image:

- Azure creates a **managed OS disk** from the image (VHD).
- This OS disk is then **attached to the virtual machine** as its system/boot disk.

> ⚠️ **Note:**  
> Anything stored in the **temporary disk** is **ephemeral** — it will be **lost** when the virtual machine is **stopped**, **deallocated**, or **moved**.  
> The temporary disk is intended only for **non-critical data** like cache files or page files.

> ⚠️ **Important:**  
> Simply **stopping** the virtual machine from within the OS (e.g., shutting down from Windows/Linux) is **not enough** to clear the temporary disk.  
> The temporary disk is only **cleared** when the VM is **stopped and deallocated** from the Azure portal or using Azure CLI/PowerShell.  
>  
> 🔁 **Deallocation** means the VM is no longer consuming compute resources — and it may be moved to a different host, which resets the temporary disk.

## 💾 Azure Managed Disk Size Ranges

| Disk Type       | Minimum Size | Maximum Size |
|------------------|--------------|---------------|
| Standard HDD     | 32 GB        | 32 TB         |
| Standard SSD     | 4 GB         | 32 TB         |
| Premium SSD      | 4 GB         | 32 TB         |

---

### 📘 Notes:

- **Standard HDD** is limited to sizes starting from 32 GB.
- **Standard SSD** and **Premium SSD** offer **smaller sizes** (starting at 4 GB), making them more flexible.
- All disk types are **resizable**, but you can only **increase** size — not reduce it once created.
