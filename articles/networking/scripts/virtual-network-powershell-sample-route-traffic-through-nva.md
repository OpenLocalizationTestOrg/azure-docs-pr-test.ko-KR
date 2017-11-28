---
title: "Azure PowerShell 스크립트 샘플 - 네트워크 가상 어플라이언스를 통한 트래픽 라우팅 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 방화벽 네트워크 가상 어플라이언스를 통해 트래픽을 라우팅합니다."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="cceac-103">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="cceac-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="cceac-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="cceac-105">또한 두 서브넷 간에 트래픽을 라우팅할 수 있게 하는 IP 전달을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="cceac-106">스크립트를 실행한 후에 방화벽 응용 프로그램과 같은 네트워크 소프트웨어를 VM에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="cceac-107">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="cceac-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="cceac-108">Sample script</span></span>


<span data-ttu-id="cceac-109">[!code-powershell[주](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "네트워크 가상 어플라이언스를 통한 트래픽 라우팅")]</span><span class="sxs-lookup"><span data-stu-id="cceac-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="cceac-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="cceac-110">Clean up deployment</span></span> 

<span data-ttu-id="cceac-111">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="cceac-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="cceac-112">Script explanation</span></span>

<span data-ttu-id="cceac-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="cceac-114">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="cceac-115">명령</span><span class="sxs-lookup"><span data-stu-id="cceac-115">Command</span></span> | <span data-ttu-id="cceac-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="cceac-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cceac-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cceac-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="cceac-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cceac-119">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="cceac-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="cceac-120">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="cceac-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cceac-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="cceac-122">백 엔드 및 DMZ 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="cceac-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="cceac-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="cceac-124">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="cceac-125">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="cceac-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="cceac-126">가상 네트워크 인터페이스를 만들고 이 인터페이스를 위해 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="cceac-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="cceac-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="cceac-128">NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="cceac-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="cceac-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="cceac-130">VM에 대한 인바운드 HTTP 및 HTTPS 포트를 허용하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="cceac-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="cceac-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="cceac-132">NSG 및 경로 테이블을 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="cceac-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="cceac-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="cceac-134">모든 경로에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="cceac-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="cceac-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="cceac-136">VM을 통해 서브넷과 인터넷 간 트래픽을 라우팅하는 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="cceac-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="cceac-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="cceac-138">가상 컴퓨터를 만들고 NIC를 이 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="cceac-139">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="cceac-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cceac-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="cceac-141">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cceac-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cceac-142">Next steps</span></span>

<span data-ttu-id="cceac-143">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cceac-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="cceac-144">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cceac-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>