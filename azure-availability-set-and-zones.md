### Concept: Microsoft Azure availability set and availability zone

What is downtime?

**Downtime** in Microsoft Azure refers to a period when a cloud service or resource becomes unavailable or unresponsive, preventing users from accessing or using it.

There are two types of downtime:

1. **Unexpected Downtime** – Caused by unforeseen events such as hardware failure, software crashes, or natural disasters.
2. **Maintenance Downtime** – Planned interruptions for tasks like software patching, updates, or hardware upgrades.

## 🧠 What I Learned: Azure Availability Set

An **Availability Set** is a logical grouping of two or more Virtual Machines (VMs) that helps distribute them across multiple **Fault Domains (FDs)** and **Update Domains (UDs)** to improve high availability and reduce downtime risk.

- **Fault Domains (FD)**: Represent separate physical server racks. Protects against hardware failures.
- **Update Domains (UD)**: Represent groups of VMs that get updated/rebooted together during maintenance. Prevents simultaneous reboots.

### Example Configuration:
- **VM1** → FD0, UD0  
- **VM2** → FD1, UD1  

This ensures:
- If one **rack** fails (FD failure), only one VM is affected.
- If Azure performs a **maintenance update**, only one VM restarts at a time.

**Result**: Your application stays available even during hardware failures or planned maintenance.

## Note on Load Balancers and Public IPs

When using **Azure Load Balancers**, you can **dissociate the Public IP** from individual Virtual Machines.

- The Load Balancer handles all external traffic using its **own Public IP**.
- Individual VMs behind the Load Balancer do **not require their own public IPs**.
- This enhances **security** and **centralizes traffic management**.

🔒 Best Practice: Let the Load Balancer expose only one public entry point while keeping backend VMs private.

## What is a Load Balancer?

A **Load Balancer** is a networking component used to **distribute incoming traffic evenly and uniformly** across a pool of **healthy virtual machines (VMs)**.

- Ensures **high availability** and **scalability**.
- Routes traffic only to **responsive (healthy)** instances.
- Can be used for **inbound (internet-facing)** or **internal (private)** traffic.

## Goal: Prevent overloading a single VM and ensure seamless application performance.

## 🧱 What is a Fault Domain?

A **Fault Domain** in Azure represents a group of **physical hardware** (like **server racks**) that share:

- A **common power source**
- **Network switches**
- **Physical infrastructure**

### Example:
- **Fault Domain 0 (FD0)** → Rack A  
- **Fault Domain 1 (FD1)** → Rack B

By placing VMs in different fault domains, Azure ensures that if one rack fails (e.g., due to power or network issues), the other VMs on a separate rack stay operational.

✅ This reduces the risk of **simultaneous hardware failure** affecting all your resources.




