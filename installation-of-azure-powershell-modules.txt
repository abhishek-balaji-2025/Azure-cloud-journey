# ⚙️ Installing Az PowerShell Module on Windows

The **Az PowerShell module** is a **rollup module** that includes all the generally available Azure modules. Installing it will make all its cmdlets available for managing Azure resources from PowerShell.

---

## ✅ Recommended Setup

- 📅 Install from the **PowerShell Gallery**  
- 🧰 Use with **PowerShell version 7 or higher** (recommended)  

This guide explains how to install the Az PowerShell module on **Windows**.

---

## 🔍 Prerequisites

## Check PowerShell Version

#powershell

`$PSVersionTable.PSVersion`

Ensure you're using Windows PowerShell 5.1 or PowerShell 7+

## Check for Azure module

`Get-Module -Name AzureRM -ListAvailable`

Important: If AzureRM is installed, review Az and AzureRM coexistence before proceeding.

Update to Windows PowerShell 5.1 (if needed)
Download from: Windows PowerShell 5.1 Download

Update PowerShellGet
Run in elevated PowerShell (Run as Administrator):

`Install-Module -Name PowerShellGet -Force`

## Set Execution Policy
Check current policy:

`Get-ExecutionPolicy -List`

Set execution policy to RemoteSigned:

`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`

## Install Az PowerShell Module
Run the following command to install:

`Install-Module -Name Az -Repository PSGallery -Force`

## Update Az Module
To update the module:

`Update-Module -Name Az -Force`

Note: Updating does not remove old versions. To completely uninstall, refer to Uninstall Azure PowerShell

## Sign In to Azure
Recommended (Device Code Login):

`Connect-AzAccount -DeviceCode`

This will display a login code in the terminal.

Visit https://microsoft.com/devicelogin and enter the code.

This method works well in restricted environments and supports MFA.

Standard (if supported):

`Connect-AzAccount`

You must repeat this for each new session.
To persist login between sessions, see: Azure PowerShell context objects







