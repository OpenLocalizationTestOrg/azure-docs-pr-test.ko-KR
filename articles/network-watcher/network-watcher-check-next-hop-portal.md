---
title: "Azure Network Watcher Next Hop을 사용하여 다음 홉 찾기 - Azure Portal | Microsoft Docs"
description: "이 문서에서는 Azure Portal에서 Next Hop을 사용하여 다음 홉 유형 및 IP 주소를 찾을 수 있는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="6ebea-103">Azure Portal을 사용하는 Azure Network Watcher에서 Next Hop 기능을 사용하는 다음 홉이 무엇인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6ebea-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ebea-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6ebea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ebea-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6ebea-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6ebea-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6ebea-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6ebea-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6ebea-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="6ebea-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6ebea-109">Next Hop은 Network Watcher의 기능으로 지정된 가상 컴퓨터를 기반으로 하는 다음 홉 유형 및 IP 주소를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6ebea-110">이 기능은 가상 컴퓨터에서 나가는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크를 트래버스하여 대상에 도달할지 여부를 결정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6ebea-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6ebea-111">Before you begin</span></span>

<span data-ttu-id="6ebea-112">이 시나리오에서는 사용자가 Network Watcher를 만드는 [Network Watcher 만들기](network-watcher-create.md)의 단계를 이미 수행했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="6ebea-113">또한 시나리오에서는 유효한 가상 컴퓨터를 포함한 리소스 그룹을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6ebea-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="6ebea-114">Scenario</span></span>

<span data-ttu-id="6ebea-115">이 문서에서 다루는 시나리오는 리소스에 대한 다음 홉 유형 및 IP 주소를 찾는 데 Next Hop을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="6ebea-116">Next Hop에 대한 자세한 내용을 보려면 [Next Hop 개요](network-watcher-next-hop-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="6ebea-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="6ebea-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-117">In this scenario, you will:</span></span>

* <span data-ttu-id="6ebea-118">가상 컴퓨터에서 다음 홉을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="6ebea-119">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ebea-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="6ebea-120">1단계</span><span class="sxs-lookup"><span data-stu-id="6ebea-120">Step 1</span></span>

<span data-ttu-id="6ebea-121">Azure Portal에서 Network Watcher 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="6ebea-122">2단계</span><span class="sxs-lookup"><span data-stu-id="6ebea-122">Step 2</span></span>

<span data-ttu-id="6ebea-123">탐색 창에서 **다음 홉**을 클릭하고 가상 컴퓨터 및 네트워크 인터페이스를 선택한 후 원본 및 대상 IP를 입력하고 **다음 홉** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="6ebea-124">다음 홉에서는 VM 리소스가 실행되기 위해 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-124">Next hop requires that the VM resource is allocated to run.</span></span>

![다음 홉 가져오기 개요][1]

### <a name="step-3"></a><span data-ttu-id="6ebea-126">3단계</span><span class="sxs-lookup"><span data-stu-id="6ebea-126">Step 3</span></span>

<span data-ttu-id="6ebea-127">작업이 완료되면 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="6ebea-128">다음 홉에 대한 IP 주소 및 장치 유형이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="6ebea-129">다음 표에서는 포털에서 사용할 수 있는 반환된 값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="6ebea-130">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="6ebea-130">**Next Hop Type**</span></span>

* <span data-ttu-id="6ebea-131">인터넷</span><span class="sxs-lookup"><span data-stu-id="6ebea-131">Internet</span></span>
* <span data-ttu-id="6ebea-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6ebea-132">VirtualAppliance</span></span>
* <span data-ttu-id="6ebea-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6ebea-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6ebea-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6ebea-134">VnetLocal</span></span>
* <span data-ttu-id="6ebea-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6ebea-135">HyperNetGateway</span></span>
* <span data-ttu-id="6ebea-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6ebea-136">VnetPeering</span></span>
* <span data-ttu-id="6ebea-137">없음</span><span class="sxs-lookup"><span data-stu-id="6ebea-137">None</span></span>

<span data-ttu-id="6ebea-138">이 트래픽을 라우팅하는 데 사용자 지정 경로가 사용된 경우 UDR(사용자 정의 경로)도 결과와 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![다음 홉 결과 가져오기][2]

## <a name="next-steps"></a><span data-ttu-id="6ebea-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ebea-140">Next steps</span></span>

<span data-ttu-id="6ebea-141">[Network Watcher를 사용하여 NSG 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹 설정을 프로그래밍 방식으로 검토하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ebea-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














