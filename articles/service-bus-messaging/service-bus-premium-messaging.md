---
title: "Azure Service Bus 프리미엄 및 표준 메시지 가격 책정 계층 개요 | Microsoft Docs"
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
ms.openlocfilehash: 3fe666da149085d14c3839a64b50765eea483e05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a><span data-ttu-id="c0e1f-103">Service Bus 프리미엄 및 표준 메시징 계층</span><span class="sxs-lookup"><span data-stu-id="c0e1f-103">Service Bus Premium and Standard messaging tiers</span></span>

<span data-ttu-id="c0e1f-104">큐 및 토픽과 같은 엔터티를 포함하는 Service Bus 메시징은 클라우드 규모로 엔터프라이즈 메시징 기능을 풍부한 게시-구독 의미 체계와 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-104">Service Bus Messaging, which includes entities such as queues and topics, combines enterprise messaging capabilities with rich publish-subscribe semantics at cloud scale.</span></span> <span data-ttu-id="c0e1f-105">Service Bus 메시징은 정교한 여러 클라우드 솔루션의 통신 백본으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-105">Service Bus Messaging is used as the communication backbone for many sophisticated cloud solutions.</span></span>

<span data-ttu-id="c0e1f-106">Service Bus 메시징의 *프리미엄* 계층은 중요 업무용 응용 프로그램에 대한 확장성, 성능 및 가용성에 관한 일반적인 고객의 요청을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-106">The *Premium* tier of Service Bus Messaging addresses common customer requests around scale, performance, and availability for mission-critical applications.</span></span> <span data-ttu-id="c0e1f-107">기능 집합은 거의 동일하지만 이러한 Service Bus 메시징의 두 계층은 다른 용도로 사용하도록 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-107">Although the feature sets are nearly identical, these two tiers of Service Bus Messaging are designed to serve different use cases.</span></span>

<span data-ttu-id="c0e1f-108">다음 테이블에는 차이가 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-108">Some high-level differences are highlighted in the following table.</span></span>

| <span data-ttu-id="c0e1f-109">Premium</span><span class="sxs-lookup"><span data-stu-id="c0e1f-109">Premium</span></span> | <span data-ttu-id="c0e1f-110">Standard</span><span class="sxs-lookup"><span data-stu-id="c0e1f-110">Standard</span></span> |
| --- | --- |
| <span data-ttu-id="c0e1f-111">높은 처리량</span><span class="sxs-lookup"><span data-stu-id="c0e1f-111">High throughput</span></span> |<span data-ttu-id="c0e1f-112">가변 처리량</span><span class="sxs-lookup"><span data-stu-id="c0e1f-112">Variable throughput</span></span> |
| <span data-ttu-id="c0e1f-113">예측 가능한 성능</span><span class="sxs-lookup"><span data-stu-id="c0e1f-113">Predictable performance</span></span> |<span data-ttu-id="c0e1f-114">가변 대기 시간</span><span class="sxs-lookup"><span data-stu-id="c0e1f-114">Variable latency</span></span> |
| <span data-ttu-id="c0e1f-115">고정된 가격 책정</span><span class="sxs-lookup"><span data-stu-id="c0e1f-115">Fixed pricing</span></span> |<span data-ttu-id="c0e1f-116">종량제 가변 가격</span><span class="sxs-lookup"><span data-stu-id="c0e1f-116">Pay as you go variable pricing</span></span> |
| <span data-ttu-id="c0e1f-117">작업을 확장 및 축소하는 기능</span><span class="sxs-lookup"><span data-stu-id="c0e1f-117">Ability to scale workload up and down</span></span> |<span data-ttu-id="c0e1f-118">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0e1f-118">N/A</span></span> |
| <span data-ttu-id="c0e1f-119">최대 1MB의 메시지 크기</span><span class="sxs-lookup"><span data-stu-id="c0e1f-119">Message size up to 1 MB</span></span> |<span data-ttu-id="c0e1f-120">최대 256KB의 메시지 크기</span><span class="sxs-lookup"><span data-stu-id="c0e1f-120">Message size up to 256 KB</span></span> |

<span data-ttu-id="c0e1f-121">**Service Bus 프리미엄 메시지**는 각 고객의 워크로드가 따로 실행되도록 CPU 및 메모리 수준에서 리소스 격리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-121">**Service Bus Premium Messaging** provides resource isolation at the CPU and memory level so that each customer workload runs in isolation.</span></span> <span data-ttu-id="c0e1f-122">이 리소스 컨테이너를 *메시징 단위*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-122">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="c0e1f-123">각 프리미엄 네임스페이스에는 하나 이상의 메시징 단위가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-123">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="c0e1f-124">각 서비스 버스 프리미엄 네임스페이스에 대해 1, 2 또는 4 메시징 단위를 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-124">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="c0e1f-125">요금은 24시간 단위 또는 일별 요금으로 부과되더라도 단일 워크로드 또는 엔터티가 여러 메시징 단위에 걸쳐 있을 수 있고 메시징 단위 수를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-125">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="c0e1f-126">그 결과, 서비스 버스 기반 솔루션에 대해 예측 가능하고 반복 가능한 성능이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-126">The result is predictable and repeatable performance for your Service Bus-based solution.</span></span>

<span data-ttu-id="c0e1f-127">이로 인해 예측 가능성 및 가용성도 높아질 뿐 아니라 속도도 더 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-127">Not only is this performance more predictable and available, but it is also faster.</span></span> <span data-ttu-id="c0e1f-128">Service Bus 프리미엄 메시징은 [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/)에 도입된 저장소 엔진에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-128">Service Bus Premium Messaging builds on the storage engine introduced in [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span> <span data-ttu-id="c0e1f-129">프리미엄 메시징을 사용할 경우 표준 계층을 사용하는 것보다 최고 성능이 훨씬 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-129">With Premium Messaging, peak performance is much faster than with the Standard tier.</span></span>

## <a name="premium-messaging-technical-differences"></a><span data-ttu-id="c0e1f-130">프리미엄 메시징 기술 차이</span><span class="sxs-lookup"><span data-stu-id="c0e1f-130">Premium Messaging technical differences</span></span>

<span data-ttu-id="c0e1f-131">다음 섹션에서는 프리미엄 및 표준 메시지 계층 간의 몇 가지 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-131">The following sections discuss a few differences between Premium and Standard messaging tiers.</span></span>

### <a name="partitioned-queues-and-topics"></a><span data-ttu-id="c0e1f-132">분할 큐 및 항목</span><span class="sxs-lookup"><span data-stu-id="c0e1f-132">Partitioned queues and topics</span></span>

<span data-ttu-id="c0e1f-133">분할된 큐 및 항목은 프리미엄 메시지에서 지원됩니다. 사실 이러한 엔터티는 항상 분할됩니다(또한 비활성화될 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="c0e1f-133">Partitioned queues and topics are supported in Premium Messaging; in fact these entities are always partitioned (and cannot be disabled).</span></span> <span data-ttu-id="c0e1f-134">그러나 프리미엄 분할된 큐 및 토픽은 Service Bus 메시지의 표준 및 기본 계층의 경우와 동일하게 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-134">However, Premium partitioned queues and topics do not function the same way as in the Standard and Basic tiers of Service Bus messaging.</span></span> <span data-ttu-id="c0e1f-135">프리미엄 메시징은 SQL을 데이터 저장소로 사용하지 않으며 공유 플랫폼과 관련된 리소스 경합이 더 이상 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-135">Premium messaging does not use SQL as a data store and no longer has the possible resource competition associated with a shared platform.</span></span> <span data-ttu-id="c0e1f-136">따라서 성능을 개선하기 위해 분할이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-136">As a result, partitioning is not necessary to improve performance.</span></span> <span data-ttu-id="c0e1f-137">또한 파티션 수가 표준 메시징의 16개 파티션에서 프리미엄 메시징의 2개 파티션으로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-137">Additionally, the partition count has been changed from 16 partitions in Standard Messaging to 2 partitions in Premium.</span></span> <span data-ttu-id="c0e1f-138">2개의 파티션은 가용성을 보장하며, 프리미엄 런타임 환경에 좀 더 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-138">Having two partitions ensures availability and is a more appropriate number for the Premium runtime environment.</span></span> 

<span data-ttu-id="c0e1f-139">프리미엄 메시지를 사용하면 [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes)로 엔터티의 크기를 지정할 때 총 크기가 지정된 크기의 16배인 [표준 분할 엔터티](service-bus-partitioning.md#standard)와는 달리, 크기가 두 파티션으로 고르게 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-139">With Premium messaging, when you specify the size of an entity with [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), that size is split equally across the 2 partitions, unlike [Standard partitioned entities](service-bus-partitioning.md#standard) in which the total size is 16 times the specified size.</span></span> 

<span data-ttu-id="c0e1f-140">분할에 대한 자세한 내용은 [분할 큐 및 항목](service-bus-partitioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-140">For more information about partitioning, see [Partitioned queues and topics](service-bus-partitioning.md).</span></span>

### <a name="express-entities"></a><span data-ttu-id="c0e1f-141">Express 엔터티</span><span class="sxs-lookup"><span data-stu-id="c0e1f-141">Express entities</span></span>

<span data-ttu-id="c0e1f-142">프리미엄 메시지가 완전히 격리된 런타임 환경에서 실행되므로 프리미엄 메시지는 Express 엔터티가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-142">Because Premium messaging runs in a completely isolated run-time environment, express entities are not supported in Premium namespaces.</span></span> <span data-ttu-id="c0e1f-143">Express 기능에 대한 자세한 내용은 [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 속성을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-143">For more information about the express feature, see the [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property.</span></span>

<span data-ttu-id="c0e1f-144">표준 메시지에서 실행되는 코드가 있고 프리미엄 계층으로 이식하려는 경우 [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) 속성이 **false**(기본값)로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-144">If you have code running under Standard messaging and want to port it to the Premium tier, make sure the [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) property is set to **false** (the default value).</span></span>

## <a name="get-started-with-premium-messaging"></a><span data-ttu-id="c0e1f-145">프리미엄 메시징 시작</span><span class="sxs-lookup"><span data-stu-id="c0e1f-145">Get started with Premium Messaging</span></span>

<span data-ttu-id="c0e1f-146">프리미엄 메시징 시작은 간단하며 프로세스는 표준 메시징의 프로세스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-146">Getting started with Premium Messaging is straightforward and the process is similar to that of Standard Messaging.</span></span> <span data-ttu-id="c0e1f-147">먼저 [네임스페이스를 만듭니다](service-bus-create-namespace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c0e1f-147">Begin by [creating a namespace](service-bus-create-namespace-portal.md).</span></span> <span data-ttu-id="c0e1f-148">**가격 책정 계층**에서 **프리미엄**을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-148">Make sure you select **Premium** under **Pricing tier**.</span></span>

![create-premium-namespace][create-premium-namespace]

<span data-ttu-id="c0e1f-150">[Azure Resource Manager 템플릿을 사용하여 프리미엄 네임스페이스](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/)를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-150">You can also create [Premium namespaces using Azure Resource Manager templates](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c0e1f-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c0e1f-151">Next steps</span></span>

<span data-ttu-id="c0e1f-152">Service Bus 메시징에 대해 자세히 알아보려면 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0e1f-152">To learn more about Service Bus Messaging, see the following topics.</span></span>

* [<span data-ttu-id="c0e1f-153">Azure Service Bus 프리미엄 메시징 소개(블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="c0e1f-153">Introducing Azure Service Bus Premium Messaging (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="c0e1f-154">Azure Service Bus 프리미엄 메시징 소개(Channel9)</span><span class="sxs-lookup"><span data-stu-id="c0e1f-154">Introducing Azure Service Bus Premium Messaging (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="c0e1f-155">Service Bus 메시징 개요</span><span class="sxs-lookup"><span data-stu-id="c0e1f-155">Service Bus Messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="c0e1f-156">Service Bus 큐를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="c0e1f-156">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
