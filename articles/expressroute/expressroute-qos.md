---
title: "ExpressRoute에 대한 QoS 요구 사항 | Microsoft Docs"
description: "이 페이지는 Express 경로 회로에 QoS를 구성하고 관리하는 자세한 요구 사항을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="5ba62-103">Express 경로 QoS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5ba62-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="5ba62-104">비즈니스용 Skype에는 차별화된 QoS 처리를 필요로 하는 다양한 워크로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="5ba62-105">Express 경로를 통해 음성 서비스를 사용하려면 아래에 설명한 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="5ba62-106">QoS 요구 사항은 Microsoft 피어링에만 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="5ba62-107">Azure 공용 피어링 및 Azure 개인 피어링에서 수신하는 네트워크 트래픽의 DSCP 값은 0으로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="5ba62-108">다음 테이블에서는 비즈니스용 Skype에서 사용하는 DSCP 표시의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="5ba62-109">자세한 내용은 [비즈니스용 Skype에 대한 QoS 관리](https://technet.microsoft.com/library/gg405409.aspx) 를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="5ba62-110">**트래픽 클래스**</span><span class="sxs-lookup"><span data-stu-id="5ba62-110">**Traffic Class**</span></span> | <span data-ttu-id="5ba62-111">**처리(DSCP 표시)**</span><span class="sxs-lookup"><span data-stu-id="5ba62-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="5ba62-112">**비즈니스 워크로드용 Skype**</span><span class="sxs-lookup"><span data-stu-id="5ba62-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ba62-113">**음성**</span><span class="sxs-lookup"><span data-stu-id="5ba62-113">**Voice**</span></span> |<span data-ttu-id="5ba62-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="5ba62-114">EF (46)</span></span> |<span data-ttu-id="5ba62-115">Skype/Lync 음성</span><span class="sxs-lookup"><span data-stu-id="5ba62-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="5ba62-116">**대화형**</span><span class="sxs-lookup"><span data-stu-id="5ba62-116">**Interactive**</span></span> |<span data-ttu-id="5ba62-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="5ba62-117">AF41 (34)</span></span> |<span data-ttu-id="5ba62-118">비디오, VBSS</span><span class="sxs-lookup"><span data-stu-id="5ba62-118">Video, VBSS</span></span> |
| <span data-ttu-id="5ba62-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="5ba62-119">AF21 (18)</span></span> |<span data-ttu-id="5ba62-120">앱 공유</span><span class="sxs-lookup"><span data-stu-id="5ba62-120">App sharing</span></span> | |
| <span data-ttu-id="5ba62-121">**기본값**</span><span class="sxs-lookup"><span data-stu-id="5ba62-121">**Default**</span></span> |<span data-ttu-id="5ba62-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="5ba62-122">AF11 (10)</span></span> |<span data-ttu-id="5ba62-123">파일 전송</span><span class="sxs-lookup"><span data-stu-id="5ba62-123">File transfer</span></span> |
| <span data-ttu-id="5ba62-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="5ba62-124">CS0 (0)</span></span> |<span data-ttu-id="5ba62-125">다른 항목</span><span class="sxs-lookup"><span data-stu-id="5ba62-125">Anything else</span></span> | |

* <span data-ttu-id="5ba62-126">워크로드를 분류하고 올바른 DSCP 값을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="5ba62-127">네트워크에서 DSCP 표시를 설정하는 방법은 [여기](https://technet.microsoft.com/library/gg405409.aspx) 에 제공된 가이드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="5ba62-128">네트워크 내에서 여러 QoS 큐를 구성하고 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="5ba62-129">음성은 독립 실행형 클래스이고 RFC 3246에 지정된 EF 처리를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="5ba62-130">큐 메커니즘, 정체 감지 정책 및 트래픽 클래스 당 대역폭 할당을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="5ba62-131">하지만 비즈니스 워크로드용 Skype에 대한 DSCP 표시를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="5ba62-132">AF31 (26)와 같이 위에 나열되지 않은 DSCP 표시를 사용하면 패킷을 Microsoft에 보내기 전에 이 DSCP 값을 0으로 다시 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="5ba62-133">Microsoft는 위의 테이블에 나와 있는 DSCP 값으로 표시되는 패킷을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5ba62-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ba62-134">Next steps</span></span>
* <span data-ttu-id="5ba62-135">[라우팅](expressroute-routing.md) 및 [NAT](expressroute-nat.md)에 대한 요구 사항을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5ba62-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="5ba62-136">Express 경로 연결을 구성하려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ba62-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="5ba62-137">Express 경로 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="5ba62-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="5ba62-138">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="5ba62-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="5ba62-139">VNet을 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="5ba62-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

