---
title: "Azure Network Watcher Next Hop을 사용하여 다음 홉 찾기 - Azure CLI 1.0 | Microsoft Docs"
description: "이 문서에서는 Azure CLI에서 다음 홉을 사용하여 다음 홉 유형 및 IP 주소를 찾을 수 있는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="9d734-103">Azure CLI 1.0을 사용하는 Azure Network Watcher에서 Next Hop 기능을 사용하는 다음 홉이 무엇인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9d734-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9d734-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="9d734-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d734-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="9d734-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9d734-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="9d734-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d734-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="9d734-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9d734-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="9d734-109">Next Hop은 Network Watcher의 기능으로 지정된 가상 컴퓨터를 기반으로 하는 다음 홉 유형 및 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="9d734-110">이 기능은 가상 컴퓨터에서 나가는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크를 트래버스하여 대상에 도달할지 여부를 결정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="9d734-111">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d734-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9d734-112">Before you begin</span></span>

<span data-ttu-id="9d734-113">이 시나리오에서는 Azure CLI를 사용하여 다음 홉 유형 및 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="9d734-114">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="9d734-115">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="9d734-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="9d734-116">Scenario</span></span>

<span data-ttu-id="9d734-117">이 문서에서 다루는 시나리오는 리소스에 대한 다음 홉 유형 및 IP 주소를 찾는 Network Watcher의 기능인 Next Hop을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="9d734-118">Next Hop에 대한 자세한 내용을 보려면 [Next Hop 개요](network-watcher-next-hop-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9d734-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="9d734-119">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="9d734-119">Get Next Hop</span></span>

<span data-ttu-id="9d734-120">다음 홉을 가져오려면 `azure netowrk watcher next-hop` cmdlet을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="9d734-121">cmdlet을 Network Watcher 리소스 그룹, NetworkWatcher, 가상 컴퓨터 ID, 원본 IP 주소 및 대상 IP 주소에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="9d734-122">이 예제에서 대상 IP 주소는 다른 가상 네트워크의 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="9d734-123">두 개의 가상 네트워크 간에 가상 네트워크 게이트웨이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="9d734-124">VM에 여러 NIC가 있고 NIC에 IP를 전달할 수 있는 경우 NIC 매개 변수(-i nic-id)를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="9d734-125">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="9d734-126">결과 검토</span><span class="sxs-lookup"><span data-stu-id="9d734-126">Review results</span></span>

<span data-ttu-id="9d734-127">완료되면 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-127">When complete, the results are provided.</span></span> <span data-ttu-id="9d734-128">리소스의 유형뿐만 아니라 다음 홉 IP 주소가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="9d734-129">다음 목록에서는 현재 사용할 수 있는 NextHopType 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="9d734-130">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="9d734-130">**Next Hop Type**</span></span>

* <span data-ttu-id="9d734-131">인터넷</span><span class="sxs-lookup"><span data-stu-id="9d734-131">Internet</span></span>
* <span data-ttu-id="9d734-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="9d734-132">VirtualAppliance</span></span>
* <span data-ttu-id="9d734-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="9d734-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="9d734-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="9d734-134">VnetLocal</span></span>
* <span data-ttu-id="9d734-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="9d734-135">HyperNetGateway</span></span>
* <span data-ttu-id="9d734-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="9d734-136">VnetPeering</span></span>
* <span data-ttu-id="9d734-137">없음</span><span class="sxs-lookup"><span data-stu-id="9d734-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d734-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d734-138">Next steps</span></span>

<span data-ttu-id="9d734-139">[Network Watcher를 사용하여 NSG 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹 설정을 프로그래밍 방식으로 검토하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d734-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
