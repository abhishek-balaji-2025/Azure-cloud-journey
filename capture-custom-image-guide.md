# 📸 Capturing a Custom Azure VM Image (Step-by-Step)

Creating a custom image in Azure involves preparing a "parent" VM, configuring it as needed, and then capturing it for reuse. Below is the recommended workflow:

---

## 🧩 1. **Start from a Parent Azure VM**
- Deploy a new VM using a base image (e.g., Windows Server, Ubuntu).
- This VM will act as your **source machine** for customization.

---

## 🔄 2. **Install Updates**
- Apply all **operating system updates** and **security patches**.
- Ensure the VM is running the **latest and most secure version** of its OS.
- Restart if necessary to apply changes.

---

## 🛡️ 3. **Harden the Server**
- Follow industry best practices to **secure** the VM:
  - Close unnecessary ports and services
  - Disable unused accounts and default credentials
  - Configure firewall rules
  - Set secure password policies
  - Remove unused software
  - Disable insecure protocols (e.g., Telnet, SMBv1)
- Use tools like:
  - Microsoft Defender for Cloud (formerly Azure Security Center)
  - CIS Benchmarks
  - Lynis (Linux) or Security Compliance Toolkit (Windows)

---

## ⚙️ 4. **Configure Options**
- Install **project-specific tools and applications**.
- Set environment variables, install agents, or configure logging and monitoring solutions.
- Customize settings to match your **deployment environment needs**.

---

## 📦 5. **Deprovision the VM (Important Step)**
- Use the Azure VM Agent to **deprovision** the VM before capturing:
  - For Linux:
    ```bash
    sudo waagent -deprovision+user
    ```
  - For Windows:
    ```powershell
    sysprep /oobe /generalize /shutdown
    ```
- This step **removes user-specific data** and prepares the image for general use.

---

## 📸 6. **Capture the Image**
- Use the Azure portal, CLI, or PowerShell to **capture the image**:
  - Mark the VM as **generalized**.
  - Capture it into a **Managed Image** or a **Shared Image Gallery**.

---

## 📤 7. **Share Image to Azure Shared Image Gallery**
- Upload the image to **Azure Shared Image Gallery** (SIG) for:
  - Versioning
  - Global replication
  - Scalable distribution across multiple regions and subscriptions

---

### ✅ Summary of Steps

| Step | Description                                      |
|------|--------------------------------------------------|
| 1    | Start from a parent Azure VM                     |
| 2    | Install OS updates and security patches          |
| 3    | Harden the VM (secure configurations)            |
| 4    | Install project-specific tools & settings        |
| 5    | Deprovision the VM for generalization            |
| 6    | Capture the image                                |
| 7    | Share via Azure Shared Image Gallery             |

---

> 🔐 Following these steps ensures your image is **secure**, **scalable**, and **production-ready** for consistent deployments.
