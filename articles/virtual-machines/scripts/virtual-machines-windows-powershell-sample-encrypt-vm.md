---
title: "Azure PowerShell 스크립트 샘플 - Windows VM 암호화 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Windows VM 암호화"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="5e938-103">Azure PowerShell을 사용하여 Windows 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="5e938-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="5e938-104">이 스크립트는 보안 Azure Key Vault, 암호화 키, Azure Active Directory 서비스 주체 및 Windows VM(가상 컴퓨터)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="5e938-105">그런 다음 Key Vault의 암호화 키 및 서비스 주체 자격 증명을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5e938-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="5e938-106">Sample script</span></span>

<span data-ttu-id="5e938-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "VM 디스크 암호화")]</span><span class="sxs-lookup"><span data-stu-id="5e938-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5e938-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="5e938-108">Clean up deployment</span></span> 

<span data-ttu-id="5e938-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5e938-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="5e938-110">Script explanation</span></span>

<span data-ttu-id="5e938-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5e938-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5e938-113">명령</span><span class="sxs-lookup"><span data-stu-id="5e938-113">Command</span></span> | <span data-ttu-id="5e938-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5e938-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e938-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e938-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5e938-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e938-117">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="5e938-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="5e938-118">암호화 키와 같은 보안 데이터를 저장하기 위한 Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="5e938-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="5e938-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="5e938-120">Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="5e938-121">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="5e938-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="5e938-122">암호화 키를 안전하게 인증하고 암호화 키에 대한 액세스를 제어하기 위한 Azure Active Directory 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="5e938-123">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="5e938-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="5e938-124">서비스 주체에 암호화 키에 대한 액세스 권한을 부여하기 위해 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="5e938-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e938-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e938-126">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-126">Creates a subnet configuration.</span></span> <span data-ttu-id="5e938-127">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="5e938-128">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5e938-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5e938-129">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5e938-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5e938-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5e938-131">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5e938-132">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5e938-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5e938-133">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5e938-134">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="5e938-135">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5e938-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5e938-136">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="5e938-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5e938-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5e938-138">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-138">Gets subnet information.</span></span> <span data-ttu-id="5e938-139">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5e938-140">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5e938-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5e938-141">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="5e938-142">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5e938-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5e938-143">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-143">Creates a VM configuration.</span></span> <span data-ttu-id="5e938-144">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5e938-145">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5e938-146">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5e938-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5e938-147">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5e938-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="5e938-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="5e938-149">Key Vault에 대한 필수 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="5e938-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="5e938-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="5e938-151">서비스 주체 자격 증명 및 암호화 키를 사용하여 VM에 대해 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="5e938-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="5e938-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="5e938-153">VM 암호화 프로세스의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="5e938-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5e938-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5e938-155">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e938-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e938-156">Next steps</span></span>

<span data-ttu-id="5e938-157">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e938-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5e938-158">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e938-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
