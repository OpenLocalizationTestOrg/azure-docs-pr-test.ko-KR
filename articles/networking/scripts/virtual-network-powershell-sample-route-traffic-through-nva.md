---
title: "aaaAzure PowerShell 스크립트 샘플 네트워크 가상 어플라이언스를 통해 트래픽 라우팅할 | Microsoft Docs"
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="b9f63-103">네트워크 가상 어플라이언스를 통한 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="b9f63-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="b9f63-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b9f63-105">또한 hello 두 서브넷 활성화 tooroute 트래픽을 전달 하는 ip는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="b9f63-106">Hello 스크립트를 실행 한 후 toohello VM 방화벽 응용 프로그램 등의 네트워크 소프트웨어를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="b9f63-107">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b9f63-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b9f63-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b9f63-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b9f63-109">Clean up deployment</span></span> 

<span data-ttu-id="b9f63-110">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="b9f63-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b9f63-111">Script explanation</span></span>

<span data-ttu-id="b9f63-112">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b9f63-113">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="b9f63-114">명령</span><span class="sxs-lookup"><span data-stu-id="b9f63-114">Command</span></span> | <span data-ttu-id="b9f63-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b9f63-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b9f63-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9f63-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="b9f63-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b9f63-118">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b9f63-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b9f63-119">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b9f63-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b9f63-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b9f63-121">백 엔드 및 DMZ 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="b9f63-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b9f63-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b9f63-123">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="b9f63-124">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b9f63-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b9f63-125">가상 네트워크 인터페이스를 만들고 이 인터페이스를 위해 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="b9f63-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="b9f63-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="b9f63-127">NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="b9f63-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b9f63-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="b9f63-129">HTTP 및 HTTPS 포트를 인바운드 toohello VM을 허용 하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="b9f63-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b9f63-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="b9f63-131">Associates Nsg hello 및 경로 toosubnets 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="b9f63-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="b9f63-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="b9f63-133">모든 경로에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="b9f63-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="b9f63-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="b9f63-135">서브넷 및 VM hello 통해 인터넷 hello 간의 tooroute 트래픽 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="b9f63-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b9f63-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b9f63-137">가상 컴퓨터를 만들고 hello NIC tooit 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="b9f63-138">이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="b9f63-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b9f63-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="b9f63-140">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9f63-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9f63-141">Next steps</span></span>

<span data-ttu-id="b9f63-142">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b9f63-143">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f63-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
