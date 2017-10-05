---
title: "Azure PowerShell 스크립트 샘플 - OMS | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - OMS"
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="838f2-103">PowerShell로 Operations Management Suite 모니터링 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="838f2-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="838f2-104">이 스크립트는 Azure Virtual Machine을 만들고 OMS(Operations Management Suite) 에이전트를 설치하고 OMS 작업 영역을 사용하여 시스템을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="838f2-105">스크립트를 실행하면 가상 컴퓨터가 OMS 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="838f2-106">또한 OMS 작업 영역 ID와 작업 영역 키를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="838f2-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="838f2-107">Sample script</span></span>

<span data-ttu-id="838f2-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "VM OMS 만들기")]</span><span class="sxs-lookup"><span data-stu-id="838f2-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="838f2-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="838f2-109">Clean up deployment</span></span> 

<span data-ttu-id="838f2-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="838f2-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="838f2-111">Script explanation</span></span>

<span data-ttu-id="838f2-112">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="838f2-113">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="838f2-114">명령</span><span class="sxs-lookup"><span data-stu-id="838f2-114">Command</span></span> | <span data-ttu-id="838f2-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="838f2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="838f2-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="838f2-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="838f2-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="838f2-118">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="838f2-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="838f2-119">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-119">Creates a subnet configuration.</span></span> <span data-ttu-id="838f2-120">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="838f2-121">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="838f2-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="838f2-122">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="838f2-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="838f2-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="838f2-124">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="838f2-125">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="838f2-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="838f2-126">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="838f2-127">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="838f2-128">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="838f2-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="838f2-129">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="838f2-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="838f2-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="838f2-131">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-131">Gets subnet information.</span></span> <span data-ttu-id="838f2-132">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="838f2-133">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="838f2-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="838f2-134">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="838f2-135">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="838f2-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="838f2-136">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-136">Creates a VM configuration.</span></span> <span data-ttu-id="838f2-137">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="838f2-138">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="838f2-139">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="838f2-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="838f2-140">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="838f2-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="838f2-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="838f2-142">가상 컴퓨터에 VM 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="838f2-143">이 경우에 Operations Management Suite 에이전트 확장은 OMS 에이전트를 설치하고 OMS 작업 영역에서 VM을 등록하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="838f2-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="838f2-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="838f2-145">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="838f2-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="838f2-146">Next steps</span></span>

<span data-ttu-id="838f2-147">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="838f2-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="838f2-148">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="838f2-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
