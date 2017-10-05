---
title: "Azure PowerShell 스크립트 샘플 - Windows VM 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Windows VM 만들기"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a9e46aded0cf3792558a7fba6f00e5662166cc0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="cb33d-103">PowerShell로 완벽히 구성된 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="cb33d-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="cb33d-104">이 스크립트는 Windows Server 2016을 실행하는 Azure Virtual Machine을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="cb33d-105">스크립트를 실행하면 RDP를 통해 가상 컴퓨터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-105">After running the script, you can access the virtual machine over RDP.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cb33d-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="cb33d-106">Sample script</span></span>

<span data-ttu-id="cb33d-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "VM 세부 사항 만들기")]</span><span class="sxs-lookup"><span data-stu-id="cb33d-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="cb33d-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="cb33d-108">Clean up deployment</span></span> 

<span data-ttu-id="cb33d-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="cb33d-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="cb33d-110">Script explanation</span></span>

<span data-ttu-id="cb33d-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="cb33d-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cb33d-113">명령</span><span class="sxs-lookup"><span data-stu-id="cb33d-113">Command</span></span> | <span data-ttu-id="cb33d-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="cb33d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb33d-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb33d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="cb33d-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cb33d-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cb33d-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="cb33d-118">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-118">Creates a subnet configuration.</span></span> <span data-ttu-id="cb33d-119">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="cb33d-120">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="cb33d-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="cb33d-121">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="cb33d-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="cb33d-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="cb33d-123">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="cb33d-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="cb33d-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="cb33d-125">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="cb33d-126">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="cb33d-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="cb33d-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="cb33d-128">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="cb33d-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cb33d-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="cb33d-130">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-130">Gets subnet information.</span></span> <span data-ttu-id="cb33d-131">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="cb33d-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="cb33d-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="cb33d-133">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="cb33d-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="cb33d-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="cb33d-135">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-135">Creates a VM configuration.</span></span> <span data-ttu-id="cb33d-136">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="cb33d-137">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="cb33d-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cb33d-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="cb33d-139">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="cb33d-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb33d-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cb33d-141">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb33d-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb33d-142">Next steps</span></span>

<span data-ttu-id="cb33d-143">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb33d-143">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cb33d-144">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb33d-144">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
