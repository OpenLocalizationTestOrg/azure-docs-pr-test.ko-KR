---
title: "aaaAzure 표준 메시징 및 서비스 버스 프리미엄 가격 책정 계층 개요 | Microsoft Docs"
description: "Service Bus 프리미엄 및 표준 메시징 계층"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="acbe4-103">Service Bus 프리미엄 및 표준 메시징 계층</span><span class="sxs-lookup"><span data-stu-id="acbe4-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="acbe4-104">큐 및 토픽과 같은 엔터티를 포함하는 Service Bus 메시징은 클라우드 규모로 엔터프라이즈 메시징 기능을 풍부한 게시-구독 의미 체계와 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="acbe4-105">서비스 버스 메시징 hello 통신 백본으로 많은 복잡 한 클라우드 솔루션 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-105">Service Bus Messaging is used as hello communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="acbe4-106">hello *프리미엄* 서비스 버스 메시징 계층 확장성, 성능 및 중요 응용 프로그램에 대 한 가용성 주위 일반적인 고객 요청을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-106">hello *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="acbe4-107">Hello 기능 집합은 거의 동일 하지만 서비스 버스 메시징이 두 계층은 설계 된 tooserve 다른 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-107">Although hello feature sets are nearly identical, these two tiers of Service Bus Messaging are designed tooserve different use cases.</span></span>

<span data-ttu-id="acbe4-108">높은 수준의 몇 가지 차이점은 다음 표에 hello에 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-108">Some high-level differences are highlighted in hello following table.</span></span>

| <span data-ttu-id="acbe4-109">Premium</span><span class="sxs-lookup"><span data-stu-id="acbe4-109">Premium</span></span> | <span data-ttu-id="acbe4-110">Standard</span><span class="sxs-lookup"><span data-stu-id="acbe4-110">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="acbe4-111">높은 처리량</span><span class="sxs-lookup"><span data-stu-id="acbe4-111">High throughput</span></span> |<span data-ttu-id="acbe4-112">가변 처리량</span><span class="sxs-lookup"><span data-stu-id="acbe4-112">Variable throughput</span></span> |
| <span data-ttu-id="acbe4-113">예측 가능한 성능</span><span class="sxs-lookup"><span data-stu-id="acbe4-113">Predictable performance</span></span> |<span data-ttu-id="acbe4-114">가변 대기 시간</span><span class="sxs-lookup"><span data-stu-id="acbe4-114">Variable latency</span></span> |
| <span data-ttu-id="acbe4-115">고정된 가격 책정</span><span class="sxs-lookup"><span data-stu-id="acbe4-115">Fixed pricing</span></span> |<span data-ttu-id="acbe4-116">종량제 가변 가격</span><span class="sxs-lookup"><span data-stu-id="acbe4-116">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="acbe4-117">기능 tooscale 작업 부하 및 축소</span><span class="sxs-lookup"><span data-stu-id="acbe4-117">Ability tooscale workload up and down</span></span> |<span data-ttu-id="acbe4-118">해당 없음</span><span class="sxs-lookup"><span data-stu-id="acbe4-118">N/A</span></span> |
| <span data-ttu-id="acbe4-119">Too1 MB 메시지 크기</span><span class="sxs-lookup"><span data-stu-id="acbe4-119">Message size up too1 MB</span></span> |<span data-ttu-id="acbe4-120">Too256 KB 메시지 크기</span><span class="sxs-lookup"><span data-stu-id="acbe4-120">Message size up too256 KB</span></span> |

<span data-ttu-id="acbe4-121">**서비스 버스 프리미엄 메시징** 각 고객 작업 격리 상태에서 실행 되도록 hello CPU 및 메모리 수준에서 리소스 격리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-121">**Service Bus Premium Messaging** provides resource isolation at hello CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="acbe4-122">이 리소스 컨테이너를 *메시징 단위*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-122">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="acbe4-123">각 프리미엄 네임스페이스에는 하나 이상의 메시징 단위가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-123">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="acbe4-124">각 서비스 버스 프리미엄 네임스페이스에 대해 1, 2 또는 4 메시징 단위를 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="acbe4-125">단일 작업 또는 엔터티 여러 메시징 단위에 걸쳐 있는 및 24 시간 또는 일별로 속도 요금이 청구는가 hello 메시징 단위 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-125">A single workload or entity can span multiple messaging units and hello number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="acbe4-126">hello 결과 서비스 버스 기반 솔루션에 대 한 예측 가능 하 고 반복 가능한 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-126">hello result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="acbe4-127">이로 인해 예측 가능성 및 가용성도 높아질 뿐 아니라 속도도 더 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-127">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="acbe4-128">에 도입 된 hello 저장소 엔진을 기반으로 서비스 버스 프리미엄 메시징 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-128">Service Bus Premium Messaging builds on hello storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="acbe4-129">프리미엄 메시징와 최고 성능 보다 훨씬 빠릅니다 hello 표준 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-129">With Premium Messaging, peak performance is much faster than with hello Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="acbe4-130">프리미엄 메시징 기술 차이</span><span class="sxs-lookup"><span data-stu-id="acbe4-130">Premium Messaging technical differences</span></span>

<span data-ttu-id="acbe4-131">hello 다음 섹션에서는 설명 고급 도메인 및 표준 메시징 계층 간의 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-131">hello following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="acbe4-132">분할 큐 및 항목</span><span class="sxs-lookup"><span data-stu-id="acbe4-132">Partitioned queues and topics</span></span>

<span data-ttu-id="acbe4-133">분할된 큐 및 항목은 프리미엄 메시지에서 지원됩니다. 사실 이러한 엔터티는 항상 분할됩니다(또한 비활성화될 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="acbe4-133">Partitioned queues and topics are supported in Premium Messaging; in fact these entities are always partitioned (and cannot be disabled).</span></span> <span data-ttu-id="acbe4-134">그러나 Premium 분할 큐 및 항목 hello 작동 하지 않습니다에서 동일한 방법으로 서비스 버스 메시징 표준 및 기본 계층 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-134">However, Premium partitioned queues and topics do not function hello same way as in hello Standard and Basic tiers of Service Bus messaging.</span></span> <span data-ttu-id="acbe4-135">프리미엄 메시징 않습니다에 SQL 데이터 저장소로 이동 하 고 더 이상 사용 하지 않으므로 공유 플랫폼에 연결 된 가능한 리소스 경쟁을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-135">Premium messaging does not use SQL as a data store and no longer has hello possible resource competition associated with a shared platform.</span></span> <span data-ttu-id="acbe4-136">따라서 분할은 하지 필요한 tooimprove 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-136">As a result, partitioning is not necessary tooimprove performance.</span></span> <span data-ttu-id="acbe4-137">또한 Premium too2 파티션에 표준 메시징 16 파티션에서 hello 파티션 수 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-137">Additionally, hello partition count has been changed from 16 partitions in Standard Messaging too2 partitions in Premium.</span></span> <span data-ttu-id="acbe4-138">두 개의 파티션이 있으면 가용성을 보장 하 고 hello 프리미엄 런타임 환경에 대 한 보다 적절 한 수입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-138">Having two partitions ensures availability and is a more appropriate number for hello Premium runtime environment.</span></span> 

<span data-ttu-id="acbe4-139">프리미엄 메시징 엔터티의 hello 크기를 지정 하는 경우와 [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes)는 크기는 동일 하 게 여러 분할 2 hello 파티션을 달리 [표준 분할 엔터티](service-bus-partitioning.md#standard) 는 hello에 총 크기는 16 회 hello 지정 된 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-139">With Premium messaging, when you specify hello size of an entity with [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), that size is split equally across hello 2 partitions, unlike [Standard partitioned entities](service-bus-partitioning.md#standard) in which hello total size is 16 times hello specified size.</span></span> 

<span data-ttu-id="acbe4-140">분할에 대한 자세한 내용은 [분할 큐 및 항목](service-bus-partitioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acbe4-140">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="acbe4-141">Express 엔터티</span><span class="sxs-lookup"><span data-stu-id="acbe4-141">Express entities</span></span>

<span data-ttu-id="acbe4-142">프리미엄 메시지가 완전히 격리된 런타임 환경에서 실행되므로 프리미엄 메시지는 Express 엔터티가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-142">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="acbe4-143">Hello express 기능에 대 한 자세한 내용은 참조 hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-143">For more information about hello express feature, see hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

<span data-ttu-id="acbe4-144">실행에서 표준 메시징 및 원하는 tooport toohello Premium 계층 코드가 있는 경우 확인 있는지 hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 너무 속성이**false** (기본값 hello).</span><span class="sxs-lookup"><span data-stu-id="acbe4-144">If you have code running under Standard messaging and want tooport it toohello Premium tier, make sure hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set too**false** (hello default value).</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="acbe4-145">프리미엄 메시징 시작</span><span class="sxs-lookup"><span data-stu-id="acbe4-145">Get started with Premium Messaging</span></span>

<span data-ttu-id="acbe4-146">프리미엄 메시징 시작 하는 것은 간단 하며 hello 프로세스는 표준 메시징 비슷한 toothat 합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-146">Getting started with Premium Messaging is straightforward and hello process is similar toothat of Standard Messaging.</span></span> <span data-ttu-id="acbe4-147">먼저 [네임스페이스를 만듭니다](service-bus-create-namespace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="acbe4-147">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="acbe4-148">**가격 책정 계층**에서 **프리미엄**을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-148">Make sure you select **Premium** under **Pricing tier**.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="acbe4-150">[Azure Resource Manager 템플릿을 사용하여 프리미엄 네임스페이스](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/)를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acbe4-150">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="acbe4-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="acbe4-151">Next steps</span></span>

<span data-ttu-id="acbe4-152">서비스 버스 메시징에 대 한 더 toolearn hello 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="acbe4-152">toolearn more about Service Bus Messaging, see hello following topics.</span></span>

* [<span data-ttu-id="acbe4-153">Azure Service Bus 프리미엄 메시징 소개(블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="acbe4-153">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="acbe4-154">Azure Service Bus 프리미엄 메시징 소개(Channel9)</span><span class="sxs-lookup"><span data-stu-id="acbe4-154">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="acbe4-155">Service Bus 메시징 개요</span><span class="sxs-lookup"><span data-stu-id="acbe4-155">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="acbe4-156">어떻게 toouse 서비스 버스 큐</span><span class="sxs-lookup"><span data-stu-id="acbe4-156">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
