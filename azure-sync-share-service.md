# Azure File Sync - Step-by-Step Setup Guide

## 📋 Pre-requisites

Ensure the following steps are completed before configuring Azure File Sync:

1. Create **two Virtual Machines (VMs)** in **two different Azure regions**.
2. **Attach and configure a data disk** on both VMs.
3. On each VM:
   - Create a **shared folder path** on the data disk.
   - Add **sample files** to this folder.
4. **Enable TLS 1.2** on both VMs.  
   *(Refer to the separately attached TLS 1.2 setup instructions.)*
5. **Install the Az PowerShell module** on both VMs.  
   *(Refer to the separately attached instructions for installation.)*
6. **Disable Internet Explorer Enhanced Security Configuration** via **Server Manager** on both VMs.
7. **Restart both VMs** after completing the above steps.
8. Ensure an **Azure Storage Account** is ready, and a **File Share** has been created within it.

---

## ⚙️ Azure File Sync Setup Steps

### Step 1: Deploy Azure Storage Sync Service
- Open the [Azure Portal](https://portal.azure.com).
- Search for **Storage Sync Services** and click **+ Create**.
- Fill in the required details:
  - **Subscription**
  - **Resource Group**
  - **Name** for the sync service
  - **Region** (must match the Storage Account’s region)
- Click **Review + Create**, then **Create**.

---

### Step 2: Create a Sync Group
- Navigate to your created **Storage Sync Service**.
- Click **+ Add Sync Group**.
- Provide:
  - **Sync Group Name**
  - **Storage Account** (select the one you already created)
  - **Azure File Share** (select the one already created as the cloud endpoint)
- Click **Create**.

---

### Step 3: Download and Install Azure File Sync Agent
- Go to the **Registered servers** section of your Storage Sync Service.
- Copy the agent download link:  
  ➤ [https://www.microsoft.com/en-us/download/details.aspx?id=57159](https://www.microsoft.com/en-us/download/details.aspx?id=57159)
- Download and install the agent on **both VMs**.

---

### Step 4: Register the Servers via PowerShell
- Open **PowerShell as Administrator** on each VM.
- Run the following commands to authenticate and register the server:

##powershell
Connect-AzAccount

Register-AzStorageSyncServer -ResourceGroupName "<your-resource-group>" `
  -StorageSyncServiceName "<your-sync-service-name>" `
  -Region "<vm-region>"

### Step 5: Confirm Registration in Azure Portal

- Navigate to:  
  `Storage Sync Service > Registered Servers`
- Verify that **both VMs appear** in the list as successfully registered.

---

### Step 6: Add Server Endpoints to the Sync Group

- Go to the **Sync Group** you created.
- Click **+ Add server endpoint**.
- Choose the **registered server**.
- Enter the **local folder path** (e.g., `E:\SharedData`) on that server.
- Optionally, **enable Cloud Tiering**.
- Click **Create**.
- Repeat this process for the **second VM**.

---

### Step 7: Validate Cloud Sync

- Navigate to:  
  `Azure Storage Account > File Share`
- Check that the **data from both VMs** is visible and syncing to the file share.

---

### Step 8: Verify Sync Across Servers

- On **both VMs**, open the synced folder path.
- Confirm that **identical data** is visible.
- **Create or delete a file** on one VM.
- Verify that the **change is reflected** on:
  - The second VM
  - The Azure File Share (via portal)

---

## ✅ Completion Checklist

- [x] Two VMs created in different regions  
- [x] Data disks configured with shared folder paths  
- [x] TLS 1.2 and Az PowerShell module installed  
- [x] IE Enhanced Security disabled and VMs restarted  
- [x] Storage Account and File Share created  
- [x] Azure Storage Sync Service deployed  
- [x] Sync Group and Server Endpoints configured  
- [x] File sync verified across cloud and both VMs  
