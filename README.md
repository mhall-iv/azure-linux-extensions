# Linux extensions for Microsoft Azure IaaS

This project provides the source code of Linux extensions for Microsoft Azure IaaS.

VM Extensions are injected components authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation.

You can read the document [about virtual machine extensions and features](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-extensions-features/).

# Extension List

| Name | Lastest Version | Description |
|:---|:---|:---|
| [Custom Script](./CustomScript) | 1.5 | Allow the owner of the Azure Virtual Machines to run customized scripts in the VM |
| [DSC](./DSC) | 2.0 | Allow the owner of the Azure Virtual Machines to configure the VM using Windows PowerShell Desired State Configuration (DSC) for Linux |
| [OS Patching](./OSPatching) | 2.0 | Allow the owner of the Azure VM to configure the Linux VM patching schedule cycle |
| [VM Access](./VMAccess) | 1.3 | Provide several ways to allow owner of the VM to get the SSH access back |
| [OMS Agent](./OmsAgent) | 1.0 | Allow the owner of the Azure VM to install the omsagent and attach it to an OMS workspace |
| [Diagnostic](./Diagnostic) | 2.3 | Allow the owner of the Azure Virtual Machines to obtain diagnostic data for a Linux virtual machine |

# Contributing Guide

Please refer to [**HERE**](./docs/contribution-guide.md).

# Known Issues
1. When you run the PowerShell command "Set-AzureVMExtension" on Linux VM, you may hit following error: "Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension". 

  * Root Cause: When you create the Linux VM via portal, the value of provision guest agent on the VM is not always set to "True". If your VM is created using PowerShell or using the Azure new portal, you will not see this issue.

  * Resolution: Add the following PowerShell command to set the ProvisionGuestAgent to "True".
  ```powershell
  $vm = Get-AzureVM -ServiceName 'MyServiceName' -Name 'MyVMName'
  $vm.GetInstance().ProvisionGuestAgent = $true
  ```
