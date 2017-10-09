---
title: "Windows VM을 암호화 하는 PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="4470b-103">Azure PowerShell을 사용하여 Windows 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="4470b-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="4470b-104">이 스크립트는 보안 Azure Key Vault, 암호화 키, Azure Active Directory 서비스 주체 및 Windows VM(가상 컴퓨터)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="4470b-105">그런 다음 VM hello 암호화 키를 키 자격 증명 모음 및 서비스 사용자 자격 증명 제공 hello를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4470b-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="4470b-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4470b-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="4470b-107">Clean up deployment</span></span> 

<span data-ttu-id="4470b-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4470b-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="4470b-109">Script explanation</span></span>

<span data-ttu-id="4470b-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="4470b-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4470b-112">명령</span><span class="sxs-lookup"><span data-stu-id="4470b-112">Command</span></span> | <span data-ttu-id="4470b-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4470b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4470b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4470b-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4470b-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4470b-116">New-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="4470b-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="4470b-117">암호화 키와 같은 Azure 키 자격 증명 모음 toostore 보안 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="4470b-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="4470b-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="4470b-119">Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="4470b-120">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="4470b-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="4470b-121">Azure Active Directory 서비스를 인증 하 고 tooencryption 키 액세스를 제어 하는 주 toosecurely 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="4470b-122">Set-AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="4470b-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="4470b-123">Hello 서비스 보안 주체 액세스 tooencryption 키 hello 키 자격 증명 모음 toogrant에 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="4470b-124">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4470b-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4470b-125">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-125">Creates a subnet configuration.</span></span> <span data-ttu-id="4470b-126">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="4470b-127">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4470b-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4470b-128">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="4470b-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4470b-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4470b-130">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="4470b-131">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4470b-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4470b-132">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="4470b-133">이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="4470b-134">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4470b-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="4470b-135">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="4470b-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4470b-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4470b-137">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-137">Gets subnet information.</span></span> <span data-ttu-id="4470b-138">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="4470b-139">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4470b-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4470b-140">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="4470b-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4470b-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4470b-142">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-142">Creates a VM configuration.</span></span> <span data-ttu-id="4470b-143">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4470b-144">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4470b-145">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4470b-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4470b-146">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="4470b-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="4470b-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="4470b-148">Hello 키 자격 증명 모음에 필요한 정보를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="4470b-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="4470b-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="4470b-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="4470b-150">Hello 서비스 사용자 자격 증명 및 암호화 키를 사용 하는 VM에서 암호화를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="4470b-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="4470b-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="4470b-152">Hello hello VM 암호화 프로세스 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="4470b-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4470b-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4470b-154">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4470b-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4470b-155">Next steps</span></span>

<span data-ttu-id="4470b-156">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4470b-157">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4470b-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
