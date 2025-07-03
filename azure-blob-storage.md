# 📦 Azure Storage Account Sub-Services

Azure Storage Account offers **four main types of storage services**:

## 🔹 1. Blob Storage (Binary Large Object)
- **Purpose**: Stores unstructured data (e.g., images, videos, backups)
- **Access Type**: Object-level
- **Types**:
  - Block Blobs – for large files like media
  - Append Blobs – optimized for log files
  - Page Blobs – used for virtual machine disks

### ✅ Use Cases:
- Media streaming
- Data lakes (Azure Data Lake Gen2)
- Backup and restore

---

## 🔹 2. File Storage (Azure Files)
- **Purpose**: Fully managed file shares accessible via SMB or NFS
- **Access Type**: File-level
- **Mountable**: Can be mounted as a drive on Windows, Linux, macOS

### ✅ Use Cases:
- Lift-and-shift file shares
- Shared application configurations

---

## 🔹 3. Table Storage
- **Purpose**: Stores structured NoSQL key-value data
- **Access Type**: Entity-level
- **Schema-less**: Allows different properties per row

### ✅ Use Cases:
- User metadata
- Device data (IoT)
- Fast lookups and audit logs

---

## 🔹 4. Queue Storage
- **Purpose**: Messaging between distributed app components
- **Access Type**: FIFO (first-in-first-out)
- **Message Size**: Up to 64 KB per message

### ✅ Use Cases:
- Decoupling microservices
- Task scheduling
- Asynchronous job processing

---

## 📊 Summary Table

| Service       | Type        | Access     | Best For                          |
|---------------|-------------|------------|-----------------------------------|
| Blob          | Unstructured| Object     | Media, backups, logs              |
| File          | Semi-structured| File   | File shares, configs              |
| Table         | Structured  | Entity     | NoSQL storage, metadata           |
| Queue         | Structured  | Message    | Messaging, decoupling apps        |

---

# 🧮 Data Formats: Structured vs Unstructured

## 🔷 Structured Data
- **Has Schema**: Yes (fixed format: rows & columns)
- **Storage**: Relational databases (RDBMS)
- **Searchability**: High (using SQL)

### ✅ Examples:
- SQL databases
- Excel sheets
- Customer records

## 🔶 Unstructured Data
- **Has Schema**: No (freeform format)
- **Storage**: Blobs, object storage, NoSQL
- **Searchability**: Low, requires metadata, indexing or ML

### ✅ Examples:
- Images, videos, audio
- PDFs, Word docs
- IoT sensor data, logs
- Social media posts

---

## 🧾 Summary Table

| Feature            | Structured Data        | Unstructured Data      |
|--------------------|------------------------|------------------------|
| Schema             | Yes                    | No                     |
| Format             | Rows & columns         | Files, blobs, media    |
| Searchable via     | SQL                    | AI, tags, indexing     |
| Use Cases          | ERP, finance, CRM      | Media, ML, IoT         |

---

# 🗄️ NAS vs SAN Storage

## 🔹 NAS (Network Attached Storage)
- **Type**: File-level storage
- **Access**: Over LAN using protocols like SMB, NFS
- **Use Cases**: File sharing, backups, home media servers

## 🔸 SAN (Storage Area Network)
- **Type**: Block-level storage
- **Access**: Over high-speed network (Fibre Channel, iSCSI)
- **Use Cases**: Databases, virtualization, enterprise storage

---

## 📊 Comparison Table

| Feature           | NAS                            | SAN                             |
|-------------------|----------------------------------|----------------------------------|
| Access Type       | File-level                      | Block-level                     |
| Protocols         | SMB, NFS                        | iSCSI, Fibre Channel            |
| Speed             | Moderate                        | Very high                       |
| Cost              | Low to Medium                   | High                            |
| Setup Complexity  | Simple                          | Complex                         |
| Ideal Use Case    | Media sharing, file backups     | Mission-critical workloads      |

---

## 🧪 Real-World Use Cases

| Service   | Example Use Case                                   |
|-----------|----------------------------------------------------|
| NAS       | A small design firm uses a Synology NAS for shared access to project files. |
| SAN       | A bank uses a SAN to host high-speed databases for its core financial systems. |

# 🧱 How Azure Blob Storage Handles Unstructured Data

When you upload unstructured data (e.g., a video, image, PDF) to Azure Blob Storage, especially using **Block Blobs**, Azure follows an internal process to store and retrieve the data efficiently.

---

## 📤 1. Uploading Unstructured Data

- Large files are **split into smaller "blocks"**.
- Each block is usually **4MB to 100MB** in size.
- Azure assigns a **unique Block ID** to each block.

---

## 🗃️ 2. Storage & Indexing

- These blocks are **stored independently** in Azure’s storage system.
- Azure **indexes the blocks** by maintaining a list of their Block IDs in the correct order.
- This allows Azure to know how to reconstruct the blob later.

---

## ✅ 3. Committing the Blob

- After uploading all blocks, a **"commit" operation** is done.
- This tells Azure to **finalize the blob** using the sequence of Block IDs.
- Until committed, blocks can be replaced, reordered, or removed.

---

## 📥 4. Downloading/Retrieving the Blob

- When a user requests the blob (e.g., streaming a video), Azure:
  - Uses the indexed block list,
  - **Pieces them together in the correct order** (like Lego bricks),
  - Reconstructs the original file seamlessly.

---

## 🧾 Example Workflow

| Step               | Description                                       |
|--------------------|---------------------------------------------------|
| Upload             | 300MB video split into 75 blocks (4MB each)       |
| Block Storage      | Each block gets a unique Block ID                 |
| Block Indexing     | Azure stores the sequence of Block IDs            |
| Commit             | Finalizes blob using the ordered Block IDs        |
| Retrieve/Download  | Reassembles blocks to form the original file      |

---

## 🚀 Benefits of This Architecture

- **Parallel Uploads**: Blocks can be uploaded simultaneously.
- **Resumable Uploads**: Only failed blocks need to be re-sent.
- **Efficient Retrieval**: Azure streams the file block by block.
- **Flexibility**: Developers can update or append data easily.

---

> ✅ In short: Blob storage treats unstructured data as a series of blocks. These are stored, indexed, and then reassembled on-demand — just like building and rebuilding with Lego blocks!

# 📛 Azure Storage Account Naming Rules

When creating a storage account in Azure, you must follow these strict naming conventions:

---

## ✅ Allowed Naming Rules

- **Lowercase letters only**
- **Numbers allowed**
- Must be **between 3 and 24 characters** long
- Must **start and end with a letter or number**
- No special characters (e.g., no underscores `_`, hyphens `-`, or uppercase letters)

---

## 🚫 Invalid Naming Examples

| Name              | Why It's Invalid                              |
|-------------------|-----------------------------------------------|
| `MyStorage123`     | Contains uppercase letters                   |
| `storage_account` | Contains underscore                          |
| `st`              | Too short (less than 3 characters)           |
| `storage-123`     | Contains a hyphen                           |
| `1234567890123456789012345` | Too long (25 characters)             |

---

## 🌐 Why So Strict?

- The storage account name becomes part of the public **endpoint URL**:

# 📄 What is a Page Blob?

A **Page Blob** is a special type of Azure blob optimized for **random read/write** operations and is mainly used to store **virtual hard disks (VHDs)** for Azure virtual machines.

---

## 🔹 Key Features

- Used for Azure **OS and data disks**
- Supports **random I/O** (read/write) in **512-byte pages**
- Can go up to **8 TB** in size
- Ideal for use cases that require **frequent partial updates**
- Stored as **.vhd files** under the hood

---

## 🧱 Structure

- Each page is **512 bytes**
- You can write or read from **specific byte ranges**
- Pages can be **cleared or overwritten individually**

---

## 🧾 Common Use Cases

- Azure Virtual Machine disks
- High-performance databases
- Custom VHD hosting

---

## 🔁 Comparison with Other Blob Types

| Type         | Optimized For     | Max Size | Use Case                    |
|--------------|-------------------|----------|-----------------------------|
| Block Blob   | Sequential Access | ~4.75 TB | Images, backups, videos     |
| **Page Blob**| **Random Access** | **8 TB** | **Azure Disks, Databases**  |
| Append Blob  | Append-only       | 195 GB   | Logs, telemetry, streaming  |

---

> ✅ In summary: A **Page Blob** is like a smart binary file inside Azure that acts as the virtual disk for your VMs. It's fast, random-access, and can grow up to 8 TB.

# 🧱 Azure VM Disk Storage Architecture (From Logical to Physical)

## 🧾 Complete Storage Hierarchy

```text
Managed Disk (VHD)
   ↓
Page Blob
   ↓
Storage Account
   ↓
Storage Cluster
   ↓
Storage Infrastructure (SAN / SSD / HDD)
   ↓
Azure Data Center (Region)

# 🧱 Azure Blob Storage: Structure & Access Levels

## 📦 Blob Storage Hierarchy

```text
Storage Account
   └── Blob Storage
         └── Container (Logical folder)
               └── Blobs (files: images, videos, docs, etc.)

A Container is a logical folder for storing blobs in Azure Blob Storage.
You can control who can access it using access levels:
Private, Blob, or Container.

