---
title: "PowerShell 스크립트 샘플-aaaAzure Windows VM NLB 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="9f70f-103">항상 사용 가능한 가상 컴퓨터 간에 트래픽 부하 분산</span><span class="sxs-lookup"><span data-stu-id="9f70f-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="9f70f-104">이 스크립트 예제에서는 필요한 모든 것을 만듭니다 toorun 몇 가지 Windows Server 2016 가상 컴퓨터에서 항상 사용 가능한 구성 및 부하 분산 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="9f70f-105">Hello 스크립트를 실행 한 후 3 개의 가상 컴퓨터가 Azure 가용성 집합에 가입된 tooan 될 것 이며는 Azure 부하 분산 장치를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9f70f-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="9f70f-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9f70f-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="9f70f-107">Clean up deployment</span></span> 

<span data-ttu-id="9f70f-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9f70f-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="9f70f-109">Script explanation</span></span>

<span data-ttu-id="9f70f-110">이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9f70f-111">Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9f70f-112">명령</span><span class="sxs-lookup"><span data-stu-id="9f70f-112">Command</span></span> | <span data-ttu-id="9f70f-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9f70f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f70f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f70f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9f70f-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9f70f-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f70f-117">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9f70f-118">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9f70f-119">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9f70f-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9f70f-120">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9f70f-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9f70f-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9f70f-122">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9f70f-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="9f70f-124">부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="9f70f-126">부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="9f70f-128">부하 분산 장치에 대한 프로브 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="9f70f-130">부하 분산 장치에 대한 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="9f70f-132">부하 분산 장치에 대한 인바운드 NAT 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="9f70f-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="9f70f-134">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="9f70f-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9f70f-136">네트워크 보안 그룹 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9f70f-137">이 구성은 hello NSG를 만들 때 사용 되는 toocreate NSG 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9f70f-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9f70f-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9f70f-139">네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="9f70f-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f70f-141">서브넷 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-141">Gets subnet information.</span></span> <span data-ttu-id="9f70f-142">이 정보는 네트워크 인터페이스를 만들 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9f70f-143">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9f70f-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9f70f-144">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="9f70f-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9f70f-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9f70f-146">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-146">Creates a VM configuration.</span></span> <span data-ttu-id="9f70f-147">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9f70f-148">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9f70f-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9f70f-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9f70f-150">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="9f70f-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f70f-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9f70f-152">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f70f-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f70f-153">Next steps</span></span>

<span data-ttu-id="9f70f-154">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9f70f-155">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f70f-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
