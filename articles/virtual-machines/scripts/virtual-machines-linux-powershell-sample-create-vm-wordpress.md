---
title: "Azure PowerShell 스크립트 샘플 - WordPress | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 778a6d5cfc63f80aa66654d682fedb178cfd67a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="d8d42-103">PowerShell로 WordPress VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d8d42-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="d8d42-104">이 스크립트는 가상 컴퓨터를 만들고 Azure Virtual Machine 사용자 지정 스크립트 확장을 사용하여 WordPress를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="d8d42-105">스크립트를 실행하면 `http://<public IP of VM>/wordpress`에서 WordPress 구성 사이트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d8d42-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="d8d42-106">Sample script</span></span>

<span data-ttu-id="d8d42-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "VM WordPress 만들기")]</span><span class="sxs-lookup"><span data-stu-id="d8d42-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d8d42-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="d8d42-108">Clean up deployment</span></span> 

<span data-ttu-id="d8d42-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d8d42-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="d8d42-110">Script explanation</span></span>

<span data-ttu-id="d8d42-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="d8d42-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d8d42-113">명령</span><span class="sxs-lookup"><span data-stu-id="d8d42-113">Command</span></span> | <span data-ttu-id="d8d42-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d8d42-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d8d42-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d8d42-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d8d42-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d8d42-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d8d42-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d8d42-118">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-118">Creates a subnet configuration.</span></span> <span data-ttu-id="d8d42-119">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="d8d42-120">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d8d42-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="d8d42-121">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="d8d42-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d8d42-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="d8d42-123">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="d8d42-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d8d42-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="d8d42-125">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d8d42-126">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="d8d42-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d8d42-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="d8d42-128">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="d8d42-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d8d42-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d8d42-130">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-130">Gets subnet information.</span></span> <span data-ttu-id="d8d42-131">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="d8d42-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d8d42-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="d8d42-133">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="d8d42-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d8d42-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="d8d42-135">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-135">Creates a VM configuration.</span></span> <span data-ttu-id="d8d42-136">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d8d42-137">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d8d42-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d8d42-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="d8d42-139">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="d8d42-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="d8d42-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="d8d42-141">가상 컴퓨터에 WordPress를 설치하는 스크립트를 호출하는 사용자 지정 스크립트 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-141">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="d8d42-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d8d42-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d8d42-143">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d8d42-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8d42-144">Next steps</span></span>

<span data-ttu-id="d8d42-145">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8d42-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d8d42-146">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Linux VM 설명서](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8d42-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
