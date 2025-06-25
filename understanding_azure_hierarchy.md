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
