---
title: "Azure PowerShell 스크립트 샘플 - Windows VM NLB 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Windows VM NLB 만들기"
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
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="ab1f8-103">항상 사용 가능한 가상 컴퓨터 간에 트래픽 부하 분산</span><span class="sxs-lookup"><span data-stu-id="ab1f8-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="ab1f8-104">이 스크립트 샘플에서는 항상 사용 가능하고 부하 분산된 구성에서 구성된 여러 Windows Server 2016 가상 컴퓨터를 실행하는 데 필요한 모든 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="ab1f8-105">스크립트를 실행하면 3개의 가상 컴퓨터가 Azure 가용성 집합에 조인되고 Azure Load Balancer를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ab1f8-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ab1f8-106">Sample script</span></span>

<span data-ttu-id="ab1f8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "VM NLB 만들기")]</span><span class="sxs-lookup"><span data-stu-id="ab1f8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ab1f8-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ab1f8-108">Clean up deployment</span></span> 

<span data-ttu-id="ab1f8-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ab1f8-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ab1f8-110">Script explanation</span></span>

<span data-ttu-id="ab1f8-111">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ab1f8-112">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ab1f8-113">명령</span><span class="sxs-lookup"><span data-stu-id="ab1f8-113">Command</span></span> | <span data-ttu-id="ab1f8-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ab1f8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab1f8-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ab1f8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ab1f8-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ab1f8-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ab1f8-118">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-118">Creates a subnet configuration.</span></span> <span data-ttu-id="ab1f8-119">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="ab1f8-120">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ab1f8-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ab1f8-121">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ab1f8-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ab1f8-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ab1f8-123">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ab1f8-124">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="ab1f8-125">부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="ab1f8-127">부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-128">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="ab1f8-129">부하 분산 장치에 대한 프로브 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="ab1f8-131">부하 분산 장치에 대한 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="ab1f8-133">부하 분산 장치에 대한 인바운드 NAT 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-134">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ab1f8-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="ab1f8-135">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="ab1f8-136">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ab1f8-137">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ab1f8-138">이 구성은 NSG가 만들어질 때 NSG 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="ab1f8-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ab1f8-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ab1f8-140">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="ab1f8-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ab1f8-142">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-142">Gets subnet information.</span></span> <span data-ttu-id="ab1f8-143">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ab1f8-144">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ab1f8-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ab1f8-145">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="ab1f8-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ab1f8-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ab1f8-147">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-147">Creates a VM configuration.</span></span> <span data-ttu-id="ab1f8-148">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ab1f8-149">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ab1f8-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ab1f8-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ab1f8-151">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ab1f8-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ab1f8-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ab1f8-153">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab1f8-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab1f8-154">Next steps</span></span>

<span data-ttu-id="ab1f8-155">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ab1f8-156">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab1f8-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
