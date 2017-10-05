---
title: "Azure Event Hubs 정의 및 사용하는 이유 | Microsoft Docs"
description: "Azure Event Hubs 개요 및 소개 - 웹 사이트, 앱 및 장치에서 클라우드 규모 원격 분석 수집"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: 1a6bf0a0352e6d9e3a22586ac825558d12e1307a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="d7fb4-103">Event Hubs란?</span><span class="sxs-lookup"><span data-stu-id="d7fb4-103">What is Event Hubs?</span></span>

<span data-ttu-id="d7fb4-104">Azure Event Hubs는 초당 수백만 개의 이벤트를 수신하고 처리할 수 있는 확장성이 뛰어난 데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="d7fb4-105">Event Hubs는 분산된 소프트웨어와 장치에서 생성된 이벤트, 데이터 또는 원격 분석을 처리하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="d7fb4-106">Event Hub로 전송된 데이터는 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용하여 변환하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-106">Data sent to an event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="d7fb4-107">Event Hubs는 짧은 대기 시간과 엄청난 규모의 [게시-가입 기능](https://msdn.microsoft.com/library/aa560414.aspx)을 제공함으로써 빅 데이터를 위한 "램프" 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-107">With the ability to provide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as the "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="d7fb4-108">Event Hubs를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="d7fb4-108">Why use Event Hubs?</span></span>

<span data-ttu-id="d7fb4-109">Event Hubs 이벤트 및 원격 분석 처리 기능은 다음과 같은 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="d7fb4-110">응용 프로그램 계측</span><span class="sxs-lookup"><span data-stu-id="d7fb4-110">Application instrumentation</span></span>
* <span data-ttu-id="d7fb4-111">사용자 환경 또는 워크플로 처리</span><span class="sxs-lookup"><span data-stu-id="d7fb4-111">User experience or workflow processing</span></span>
* <span data-ttu-id="d7fb4-112">IoT(사물 인터넷) 시나리오</span><span class="sxs-lookup"><span data-stu-id="d7fb4-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="d7fb4-113">예를 들어 Event Hubs를 사용하면 모바일 앱의 동작 추적, 웹 팜의 트래픽 정보, 콘솔 게임의 게임 내 이벤트 캡처 또는 산업용 컴퓨터, 연결된 차량 또는 다른 장치에서 수집한 원격 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="d7fb4-114">Azure Event Hubs 개요</span><span class="sxs-lookup"><span data-stu-id="d7fb4-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="d7fb4-115">Event Hubs가 솔루션 아키텍처에서 수행하는 일반적인 역할은 *이벤트 수집기*라고 하는 이벤트 파이프라인에 대한 "현관"으로서의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-115">The common role that Event Hubs plays in solution architectures is the "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="d7fb4-116">이벤트 ingestor는 이러한 이벤트에서 이벤트 스트림의 프로덕션을 분리하는 이벤트 게시자와 이벤트 소비자 간에 작용하는 구성 요소 또는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-116">An event ingestor is a component or service that sits between event publishers and event consumers to decouple the production of an event stream from the consumption of those events.</span></span> <span data-ttu-id="d7fb4-117">다음 그림은 이 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-117">The following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="d7fb4-119">Event Hubs는 메시지 스트림 처리 기능을 제공하지만 기존 엔터프라이즈 메시지와 다른 특징을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="d7fb4-120">Event Hubs 기능은 높은 처리량 및 이벤트 처리 시나리오를 중심으로 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="d7fb4-121">따라서 Event Hubs는 [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) 메시지와 다르며, 토픽과 같은 [Service Bus 메시지](/azure/service-bus-messaging/) 엔터티에 사용할 수 있는 기능 일부를 구현하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of the capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="d7fb4-122">Event Hubs 기능</span><span class="sxs-lookup"><span data-stu-id="d7fb4-122">Event Hubs features</span></span>

<span data-ttu-id="d7fb4-123">Event Hubs에는 다음과 같은 주요 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-123">Event Hubs contains the following key elements:</span></span>

- <span data-ttu-id="d7fb4-124">[**이벤트 생산자/게시자**](event-hubs-features.md#event-publishers): 이벤트 허브에 데이터를 보내는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data to an event hub.</span></span> <span data-ttu-id="d7fb4-125">이벤트는 AMQP 1.0 또는 HTTPS를 통해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="d7fb4-126">[**캡처**](event-hubs-features.md#capture): Event Hubs 스트리밍 데이터를 캡처하고 Azure Blob Storage 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-126">[**Capture**](event-hubs-features.md#capture): Enables you to capture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="d7fb4-127">[**파티션**](event-hubs-features.md#partitions): 각 소비자에서 이벤트 스트림의 특정 하위 집합 또는 파티션만 읽을 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer to only read a specific subset, or partition, of the event stream.</span></span>
- <span data-ttu-id="d7fb4-128">[**SAS 토큰**](event-hubs-features.md#sas-tokens): 이벤트 게시자를 식별하고 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates the event publisher.</span></span>
- <span data-ttu-id="d7fb4-129">[**이벤트 소비자**](event-hubs-features.md#event-consumers): 이벤트 허브에서 이벤트 데이터를 읽는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="d7fb4-130">이벤트 소비자는 AMQP 1.0을 통해 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="d7fb4-131">[**소비자 그룹**](event-hubs-features.md#consumer-groups): 각 이벤트 스트림을 개별적으로 볼 수 있는 다중 소비 응용 프로그램을 제공하여 소비자가 독립적으로 작동할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of the event stream, enabling those consumers to act independently.</span></span>
- <span data-ttu-id="d7fb4-132">[**처리량 단위**](event-hubs-features.md#capacity): 미리 구입한 용량의 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="d7fb4-133">단일 파티션에는 처리량 단위 하나의 최대 크기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="d7fb4-134">이러한 요소와 다른 Event Hubs 기능에 대한 자세한 기술적 내용은 [Event Hubs 기능 개요](event-hubs-features.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-134">For technical details about these and other Event Hubs features, see the [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d7fb4-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7fb4-135">Next steps</span></span>

<span data-ttu-id="d7fb4-136">Event Hubs 가격에 대한 자세한 내용은 [Event Hubs 가격](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="d7fb4-137">Event Hubs에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="d7fb4-137">For more information about Event Hubs, visit the following links:</span></span>

* <span data-ttu-id="d7fb4-138">[Event Hubs 자습서](event-hubs-dotnet-standard-getstarted-send.md) 시작</span><span class="sxs-lookup"><span data-stu-id="d7fb4-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="d7fb4-139">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="d7fb4-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="d7fb4-140">Event Hubs를 사용하는 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d7fb4-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

