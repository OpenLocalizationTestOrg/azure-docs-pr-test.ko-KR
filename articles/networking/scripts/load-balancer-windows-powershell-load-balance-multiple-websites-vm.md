---
title: "Azure PowerShell 스크립트 샘플 - Azure PowerShell을 통해 여러 웹 사이트 부하 분산 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 동일한 가상 컴퓨터로 여러 웹 사이트 부하 분산"
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
ms.openlocfilehash: d73cdc98ff279c3ee1b93443abe4b6c7c97786a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="df718-103">여러 웹 사이트 부하 분산</span><span class="sxs-lookup"><span data-stu-id="df718-103">Load balance multiple websites</span></span>

<span data-ttu-id="df718-104">이 스크립트 샘플에서는 가용성 집합의 구성원인 두 개의 VM(가상 컴퓨터)과 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="df718-105">부하 분산 장치는 두 VM에 두 개의 별도 IP 주소에 대한 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="df718-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="df718-106">스크립트를 실행한 후 웹 서버 소프트웨어를 VM에 배포하고 여러 웹 사이트를 각각 고유한 IP 주소로 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df718-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="df718-107">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="df718-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="df718-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="df718-108">Sample script</span></span>

<span data-ttu-id="df718-109">[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "여러 웹 사이트 부하 분산")]</span><span class="sxs-lookup"><span data-stu-id="df718-109">[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="df718-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="df718-110">Clean up deployment</span></span> 

<span data-ttu-id="df718-111">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df718-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="df718-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="df718-112">Script explanation</span></span>

<span data-ttu-id="df718-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크, 부하 분산 장치 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-113">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="df718-114">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="df718-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="df718-115">명령</span><span class="sxs-lookup"><span data-stu-id="df718-115">Command</span></span> | <span data-ttu-id="df718-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="df718-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df718-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df718-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="df718-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df718-119">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="df718-119">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="df718-120">고가용성을 제공하기 위해 Azure 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-120">Creates an Azure availability set to provide high availability.</span></span> |
| [<span data-ttu-id="df718-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="df718-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="df718-122">서브넷 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-122">Creates a subnet configuration.</span></span> <span data-ttu-id="df718-123">이 구성은 가상 네트워크 만들기 프로세스에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df718-123">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="df718-124">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="df718-124">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="df718-125">가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-125">Creates a virtual network.</span></span> |
| [<span data-ttu-id="df718-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="df718-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="df718-127">공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="df718-128">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="df718-128">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="df718-129">부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-129">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="df718-130">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="df718-130">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="df718-131">부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-131">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="df718-132">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="df718-132">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="df718-133">NLB 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-133">Creates an NLB probe.</span></span> <span data-ttu-id="df718-134">NLB 프로브는 NLB 집합에서 각 VM을 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df718-134">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="df718-135">모든 VM이 액세스할 수 없게 되면 트래픽은 VM에 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df718-135">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="df718-136">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="df718-136">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="df718-137">NLB 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-137">Creates an NLB rule.</span></span> <span data-ttu-id="df718-138">이 샘플에서는 포트 80에 대한 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-138">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="df718-139">HTTP 트래픽이 NLB에 도착하면 NLB 집합에서 VM 중 하나인 포트 80에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="df718-139">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="df718-140">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="df718-140">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="df718-141">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-141">Creates a load balancer.</span></span> |
| [<span data-ttu-id="df718-142">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="df718-142">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="df718-143">가상 네트워크 인터페이스에 대한 고급 기능을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="df718-143">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="df718-144">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="df718-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="df718-145">네트워크 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="df718-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="df718-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="df718-147">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-147">Creates a VM configuration.</span></span> <span data-ttu-id="df718-148">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="df718-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="df718-149">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df718-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="df718-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="df718-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="df718-151">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="df718-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="df718-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df718-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="df718-153">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="df718-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df718-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df718-154">Next steps</span></span>

<span data-ttu-id="df718-155">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df718-155">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="df718-156">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df718-156">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
