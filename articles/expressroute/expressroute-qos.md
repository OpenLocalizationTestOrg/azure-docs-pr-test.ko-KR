---
title: "ExpressRoute에 대 한 요구 사항 aaaQoS | Microsoft Docs"
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
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="d4e7a-103">Express 경로 QoS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d4e7a-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="d4e7a-104">비즈니스용 Skype에는 차별화된 QoS 처리를 필요로 하는 다양한 워크로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="d4e7a-105">ExpressRoute 통해 tooconsume 음성 서비스 하려는 경우 아래에 설명 된 toohello 요구를 준수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="d4e7a-106">QoS 요구 toohello Microsoft 피어 링만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="d4e7a-107">hello Azure 공용 피어 링 및 Azure 개인 피어 링에 수신 하 여 네트워크 트래픽 DSCP 값 재설정 too0 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="d4e7a-108">hello 다음 표에서 비즈니스용 Skype를 사용한 DSCP 표시의 목록.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="d4e7a-109">너무 참조[비즈니스용 Skype에 대 한 QoS 관리](https://technet.microsoft.com/library/gg405409.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="d4e7a-110">**트래픽 클래스**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-110">**Traffic Class**</span></span> | <span data-ttu-id="d4e7a-111">**처리(DSCP 표시)**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="d4e7a-112">**비즈니스 워크로드용 Skype**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4e7a-113">**음성**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-113">**Voice**</span></span> |<span data-ttu-id="d4e7a-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="d4e7a-114">EF (46)</span></span> |<span data-ttu-id="d4e7a-115">Skype/Lync 음성</span><span class="sxs-lookup"><span data-stu-id="d4e7a-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="d4e7a-116">**대화형**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-116">**Interactive**</span></span> |<span data-ttu-id="d4e7a-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="d4e7a-117">AF41 (34)</span></span> |<span data-ttu-id="d4e7a-118">비디오, VBSS</span><span class="sxs-lookup"><span data-stu-id="d4e7a-118">Video, VBSS</span></span> |
| <span data-ttu-id="d4e7a-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="d4e7a-119">AF21 (18)</span></span> |<span data-ttu-id="d4e7a-120">앱 공유</span><span class="sxs-lookup"><span data-stu-id="d4e7a-120">App sharing</span></span> | |
| <span data-ttu-id="d4e7a-121">**기본값**</span><span class="sxs-lookup"><span data-stu-id="d4e7a-121">**Default**</span></span> |<span data-ttu-id="d4e7a-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="d4e7a-122">AF11 (10)</span></span> |<span data-ttu-id="d4e7a-123">파일 전송</span><span class="sxs-lookup"><span data-stu-id="d4e7a-123">File transfer</span></span> |
| <span data-ttu-id="d4e7a-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="d4e7a-124">CS0 (0)</span></span> |<span data-ttu-id="d4e7a-125">다른 항목</span><span class="sxs-lookup"><span data-stu-id="d4e7a-125">Anything else</span></span> | |

* <span data-ttu-id="d4e7a-126">Hello 워크 로드를 분류 하 고 hello 오른쪽 DSCP 값을 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="d4e7a-127">제공 된 hello 지침에 따라 [여기](https://technet.microsoft.com/library/gg405409.aspx) 방법에 네트워크의 tooset DSCP 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="d4e7a-128">네트워크 내에서 여러 QoS 큐를 구성하고 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="d4e7a-129">음성 독립 실행형 클래스와 RFC 3246에 지정 된 hello EF 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="d4e7a-130">Hello 큐 메커니즘, 정체 검색 정책 및 트래픽 클래스 마다 대역폭 할당을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="d4e7a-131">그러나 hello DSCP 비즈니스 작업에 대 한 Skype에 대 한 표시 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="d4e7a-132">위에 나열 되지 않은 DSCP 표시를 사용 하는 경우 예를 들어 AF31 (26)를 다시 작성 해야이 DSCP 값 too0 hello 패킷 tooMicrosoft 보내기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="d4e7a-133">Microsoft는만 hello DSCP 값 테이블 위에 hello에 표시 된 것으로 표시 하는 패킷을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d4e7a-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d4e7a-134">Next steps</span></span>
* <span data-ttu-id="d4e7a-135">Toohello 요구 사항에 대 한 참조 [라우팅](expressroute-routing.md) 및 [NAT](expressroute-nat.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="d4e7a-136">Hello 다음 링크 tooconfigure ExpressRoute 연결을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d4e7a-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="d4e7a-137">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="d4e7a-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="d4e7a-138">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="d4e7a-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="d4e7a-139">VNet tooan ExpressRoute 회로 연결</span><span class="sxs-lookup"><span data-stu-id="d4e7a-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

