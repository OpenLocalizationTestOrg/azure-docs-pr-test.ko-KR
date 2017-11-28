---
title: "PowerShell 스크립트 샘플-aaaAzure 부하를 분산 Azure PowerShell을 사용한 여러 웹 사이트 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-을 부하 분산 여러 웹 사이트 toohello 동일한 가상 컴퓨터"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="ea1aa-103">여러 웹 사이트 부하 분산</span><span class="sxs-lookup"><span data-stu-id="ea1aa-103">Load balance multiple websites</span></span>

<span data-ttu-id="ea1aa-104">이 스크립트 샘플에서는 가용성 집합의 구성원인 두 개의 VM(가상 컴퓨터)과 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="ea1aa-105">부하 분산 장치에 대 한 두 개의 별도 트래픽을 전송 IP 주소 2 toohello Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="ea1aa-106">Hello 스크립트를 실행 한 후 웹 서버 소프트웨어 toohello Vm을 배포 하 고 각각 자체 IP 주소를 가진 여러 웹 사이트를 호스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="ea1aa-107">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ea1aa-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ea1aa-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ea1aa-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ea1aa-109">Clean up deployment</span></span> 

<span data-ttu-id="ea1aa-110">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ea1aa-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ea1aa-111">Script explanation</span></span>

<span data-ttu-id="ea1aa-112">이 스크립트 명령 toocreate 리소스 그룹에서 가상 네트워크 부하 분산 장치, 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-112">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="ea1aa-113">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ea1aa-114">명령</span><span class="sxs-lookup"><span data-stu-id="ea1aa-114">Command</span></span> | <span data-ttu-id="ea1aa-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ea1aa-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ea1aa-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea1aa-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ea1aa-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ea1aa-118">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="ea1aa-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="ea1aa-119">Azure 가용성 집합 tooprovide 높은 가용성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-119">Creates an Azure availability set tooprovide high availability.</span></span> |
| [<span data-ttu-id="ea1aa-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ea1aa-121">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-121">Creates a subnet configuration.</span></span> <span data-ttu-id="ea1aa-122">이 구성은 hello 가상 네트워크 만들기 프로세스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-122">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="ea1aa-123">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ea1aa-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ea1aa-124">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ea1aa-125">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ea1aa-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ea1aa-126">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ea1aa-127">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="ea1aa-128">부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="ea1aa-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="ea1aa-130">부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ea1aa-131">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="ea1aa-132">NLB 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-132">Creates an NLB probe.</span></span> <span data-ttu-id="ea1aa-133">NLB 프로브는 사용 되는 toomonitor hello NLB 집합의 각 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-133">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="ea1aa-134">모든 VM에 액세스할 수 없게 됩니다, 트래픽 라우팅된 toohello VM 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-134">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="ea1aa-135">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="ea1aa-136">NLB 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-136">Creates an NLB rule.</span></span> <span data-ttu-id="ea1aa-137">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="ea1aa-138">HTTP 트래픽을 hello NLB에 도착 하면 때 라우트된 tooport 80 hello NLB 집합의 hello Vm 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-138">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="ea1aa-139">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ea1aa-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="ea1aa-140">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="ea1aa-141">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="ea1aa-142">가상 네트워크 인터페이스에 대한 고급 기능을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="ea1aa-143">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ea1aa-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ea1aa-144">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="ea1aa-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ea1aa-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ea1aa-146">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-146">Creates a VM configuration.</span></span> <span data-ttu-id="ea1aa-147">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ea1aa-148">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ea1aa-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ea1aa-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ea1aa-150">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ea1aa-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea1aa-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ea1aa-152">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ea1aa-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea1aa-153">Next steps</span></span>

<span data-ttu-id="ea1aa-154">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-154">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ea1aa-155">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea1aa-155">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
