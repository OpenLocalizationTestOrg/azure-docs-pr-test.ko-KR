---
title: "Azure 네트워크 감시자 다음 홉-Azure 포털 aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 어떤 hello 다음 홉 형식 및 ip 주소를 사용 하 여 다음 홉을 사용 하 여 hello Azure 포털을 찾을 수 있습니다."
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="59a0a-103">어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하 여 Azure 네트워크 감시자 hello 포털을 사용 하는 확인</span><span class="sxs-lookup"><span data-stu-id="59a0a-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="59a0a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="59a0a-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="59a0a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59a0a-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="59a0a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="59a0a-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="59a0a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="59a0a-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="59a0a-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="59a0a-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="59a0a-109">다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="59a0a-110">이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59a0a-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="59a0a-111">Before you begin</span></span>

<span data-ttu-id="59a0a-112">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="59a0a-113">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="59a0a-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="59a0a-114">Scenario</span></span>

<span data-ttu-id="59a0a-115">이 문서에서 설명 하는 hello 시나리오는 리소스에 대 한 다음 홉 toofind hello 다음 홉 형식이 및 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="59a0a-116">다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="59a0a-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-117">In this scenario, you will:</span></span>

* <span data-ttu-id="59a0a-118">가상 컴퓨터에서 다음 홉 hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="59a0a-119">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="59a0a-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="59a0a-120">1단계</span><span class="sxs-lookup"><span data-stu-id="59a0a-120">Step 1</span></span>

<span data-ttu-id="59a0a-121">Hello Azure 포털에서에서 tooyour 네트워크 감시자 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="59a0a-122">2단계</span><span class="sxs-lookup"><span data-stu-id="59a0a-122">Step 2</span></span>

<span data-ttu-id="59a0a-123">클릭 **다음 홉** hello 원본 및 대상 IP hello 탐색 창, 선택 hello 가상 컴퓨터 및 네트워크 인터페이스를 작성 하 고 hello 클릭 **다음 홉** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="59a0a-124">다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![다음 홉 가져오기 개요][1]

### <a name="step-3"></a><span data-ttu-id="59a0a-126">3단계</span><span class="sxs-lookup"><span data-stu-id="59a0a-126">Step 3</span></span>

<span data-ttu-id="59a0a-127">Hello 작업 완료 되 면 hello 결과가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="59a0a-128">IP 주소와 장치 hello 다음 홉 유형을 hello가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="59a0a-129">hello 다음 표에 hello 사용할 수 있는 반환된 값 hello 포털에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="59a0a-130">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="59a0a-130">**Next Hop Type**</span></span>

* <span data-ttu-id="59a0a-131">인터넷</span><span class="sxs-lookup"><span data-stu-id="59a0a-131">Internet</span></span>
* <span data-ttu-id="59a0a-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="59a0a-132">VirtualAppliance</span></span>
* <span data-ttu-id="59a0a-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="59a0a-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="59a0a-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="59a0a-134">VnetLocal</span></span>
* <span data-ttu-id="59a0a-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="59a0a-135">HyperNetGateway</span></span>
* <span data-ttu-id="59a0a-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="59a0a-136">VnetPeering</span></span>
* <span data-ttu-id="59a0a-137">없음</span><span class="sxs-lookup"><span data-stu-id="59a0a-137">None</span></span>

<span data-ttu-id="59a0a-138">사용자 지정 경로 사용 하는 tooroute hello 결과 함께이 트래픽은 hello 사용자 정의 경로 (UDR)도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59a0a-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![다음 홉 결과 가져오기][2]

## <a name="next-steps"></a><span data-ttu-id="59a0a-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59a0a-140">Next steps</span></span>

<span data-ttu-id="59a0a-141">자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="59a0a-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














