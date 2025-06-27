# Azure Virtual Machine Images: Marketplace vs Custom

In Azure, there are two main types of virtual machine (VM) images:

---

## ✅ 1. Azure Marketplace Images

Azure Marketplace Images are **predefined templates** provided by **Microsoft or third-party vendors**. These images are built to support **standard use cases** and are frequently updated and maintained.

### 🔹 Features:
- Provided via the **Azure Marketplace**
- Used for common workloads like:
  - Windows Server
  - Ubuntu, Red Hat
  - SQL Server, Jenkins, WordPress, etc.
- Quick to deploy
- Maintained by the image publisher

### 📌 Example:
> Creating a VM with "Ubuntu Server 22.04 LTS" from the Marketplace.

---

## ✅ 2. Custom Images

Custom Images are **user-defined VM images** captured from a **configured parent VM**. These are useful for replicating an environment with **pre-installed software**, custom settings, or specific configurations.

### 🔹 Features:
- Captured from an existing VM
- Includes:
  - Operating System
  - Installed applications
  - Configurations and settings
- Can be stored as:
  - Managed Images
  - Shared Image Gallery
- Ideal for scaling and automation

### 📌 Example:
> Setting up a VM with custom security software, then capturing it as a reusable custom image.

---

## ✳️ Summary Comparison

| Feature               | Azure Marketplace Image                | Custom Image                           |
|-----------------------|----------------------------------------|----------------------------------------|
| Source                | Microsoft / Third-party Vendors        | User-created from existing VM          |
| Use Case              | Standard workloads                     | Custom or specialized environments     |
| Maintenance           | Publisher-managed                      | User-managed                           |
| Reusability           | Fixed templates                        | High reusability for internal use      |
| Flexibility           | Less flexible                          | Fully customizable                     |

---

## 📝 Conclusion

- Use **Marketplace images** for rapid deployment of standard solutions.
- Use **Custom images** when you need consistency across deployments or custom-built environments.

