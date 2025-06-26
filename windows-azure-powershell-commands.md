# Windows Azure PowerShell Commands

This document contains a collection of commonly used **Azure PowerShell commands** for managing Azure resources from the command line. Azure PowerShell is a powerful scripting environment built on the `Az` module, ideal for automating tasks and managing Azure services efficiently within a Windows environment.

1. `New-AzResourceGroup -Name demo-resource-group -Location centralindia`  
   → Creates a new Azure resource group named **demo-resource-group** in the **Central India** region.

2. `New-AzVm -ResourceGroupName 'myResourceGroup' -Name 'myVM' -Location 'eastus' -Image 'MicrosoftWindowsServer:WindowsServer:2022-datacenter-azure-edition:latest' -VirtualNetworkName 'myVnet' -SubnetName 'mySubnet' -SecurityGroupName 'myNetworkSecurityGroup' -PublicIpAddressName 'myPublicIpAddress' -OpenPorts 80,3389`  
   → Creates a new **Windows Server 2022** virtual machine named **myVM** in the **East US** region with network configuration and opens **ports 80 (HTTP)** and **3389 (RDP)**.
 
3. `New-AzVm -ResourceGroupName demo-RG -Name my-vm-1 -Location centralindia -Image 'MicrosoftWindowsServer:WindowsServer:2022-datacenter-azure-edition:latest' -OpenPorts 80,3389 -Size Standard_B2ms -Credential (Get-Credential)`  
→ Creates a Windows Server 2022 VM in Central India with ports 80 (HTTP) and 3389 (RDP) open, using Standard_B2ms size and prompts for admin credentials.

