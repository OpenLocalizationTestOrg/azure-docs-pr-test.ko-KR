---
title: "aaaWhat Azure 이벤트 허브는 및 사용 하는 이유 | Microsoft Docs"
description: "개요 및 도입 tooAzure 이벤트 허브-웹 사이트, 앱 및 장치에서 클라우드 규모 원격 분석 수집"
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
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="3938b-103">Event Hubs란?</span><span class="sxs-lookup"><span data-stu-id="3938b-103">What is Event Hubs?</span></span>

<span data-ttu-id="3938b-104">Azure Event Hubs는 초당 수백만 개의 이벤트를 수신하고 처리할 수 있는 확장성이 뛰어난 데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="3938b-105">Event Hubs는 분산된 소프트웨어와 장치에서 생성된 이벤트, 데이터 또는 원격 분석을 처리하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="3938b-106">데이터 전송 tooan 이벤트 허브 전환 하 여 모든 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용 하 여 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="3938b-107">Hello 기능 tooprovide와 [게시-구독 기능과](https://msdn.microsoft.com/library/aa560414.aspx) 빅 데이터에 대 한 이벤트 허브 역할 진입점"에" hello을 짧은 대기 시간으로 및 대규모 합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="3938b-108">Event Hubs를 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="3938b-108">Why use Event Hubs?</span></span>

<span data-ttu-id="3938b-109">Event Hubs 이벤트 및 원격 분석 처리 기능은 다음과 같은 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="3938b-110">응용 프로그램 계측</span><span class="sxs-lookup"><span data-stu-id="3938b-110">Application instrumentation</span></span>
* <span data-ttu-id="3938b-111">사용자 환경 또는 워크플로 처리</span><span class="sxs-lookup"><span data-stu-id="3938b-111">User experience or workflow processing</span></span>
* <span data-ttu-id="3938b-112">IoT(사물 인터넷) 시나리오</span><span class="sxs-lookup"><span data-stu-id="3938b-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="3938b-113">예를 들어 Event Hubs를 사용하면 모바일 앱의 동작 추적, 웹 팜의 트래픽 정보, 콘솔 게임의 게임 내 이벤트 캡처 또는 산업용 컴퓨터, 연결된 차량 또는 다른 장치에서 수집한 원격 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="3938b-114">Azure Event Hubs 개요</span><span class="sxs-lookup"><span data-stu-id="3938b-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="3938b-115">hello 일반적인 역할 이벤트 허브에 솔루션 아키텍처는 hello "프런트 도어" 이벤트 파이프라인의 라고도 *생산과 이벤트 사용*합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="3938b-116">이벤트 수집기 구성 요소 또는 이벤트 게시자 및 해당 이벤트의 hello 소비에서 이벤트 스트림의 이벤트 소비자 toodecouple hello 프로덕션 사이 있는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="3938b-117">hello 다음 그림은 나타냅니다이 아키텍처를.</span><span class="sxs-lookup"><span data-stu-id="3938b-117">hello following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="3938b-119">Event Hubs는 메시지 스트림 처리 기능을 제공하지만 기존 엔터프라이즈 메시지와 다른 특징을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="3938b-120">Event Hubs 기능은 높은 처리량 및 이벤트 처리 시나리오를 중심으로 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="3938b-121">따라서 이벤트 허브와 다르면 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/) 메시징과에 사용할 수 있는 hello 기능 중 일부를 구현 하지 않는 [서비스 버스 메시징](/azure/service-bus-messaging/) 항목 등의 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3938b-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="3938b-122">Event Hubs 기능</span><span class="sxs-lookup"><span data-stu-id="3938b-122">Event Hubs features</span></span>

<span data-ttu-id="3938b-123">이벤트 허브는 다음 주요 요소는 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="3938b-124">[**이벤트 생산자/게시자**](event-hubs-features.md#event-publishers): tooan 이벤트 허브 데이터를 전송 하는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="3938b-125">이벤트는 AMQP 1.0 또는 HTTPS를 통해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="3938b-126">[**캡처**](event-hubs-features.md#capture): 스트리밍 데이터 toocapture 이벤트 허브를 사용 하면를 Azure Blob 저장소 계정에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="3938b-127">[**파티션**](event-hubs-features.md#partitions): 각 소비자 tooonly의 특정 하위 집합 또는 파티션, 읽을 수 있도록 hello 이벤트 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="3938b-128">[**SAS 토큰**](event-hubs-features.md#sas-tokens): 식별 하 고 hello 이벤트 게시자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="3938b-129">[**이벤트 소비자**](event-hubs-features.md#event-consumers): 이벤트 허브에서 이벤트 데이터를 읽는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="3938b-130">이벤트 소비자는 AMQP 1.0을 통해 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="3938b-131">[**소비자 그룹**](event-hubs-features.md#consumer-groups): 각 여러 hello 이벤트 스트림에 대 한 별도 보기를 응용 프로그램 사용, 해당 소비자 tooact를 독립적으로 활성화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="3938b-132">[**처리량 단위**](event-hubs-features.md#capacity): 미리 구입한 용량의 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="3938b-133">단일 파티션에는 처리량 단위 하나의 최대 크기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="3938b-134">이러한 오류 코드 및 기타 이벤트 허브 기능에 대 한 기술 세부 정보에 대 한 참조 hello [이벤트 허브 기능 개요](event-hubs-features.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3938b-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3938b-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3938b-135">Next steps</span></span>

<span data-ttu-id="3938b-136">Event Hubs 가격에 대한 자세한 내용은 [Event Hubs 가격](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3938b-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="3938b-137">이벤트 허브에 대 한 자세한 내용은 다음 링크는 hello 방문.</span><span class="sxs-lookup"><span data-stu-id="3938b-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="3938b-138">[Event Hubs 자습서](event-hubs-dotnet-standard-getstarted-send.md) 시작</span><span class="sxs-lookup"><span data-stu-id="3938b-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="3938b-139">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="3938b-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="3938b-140">Event Hubs를 사용하는 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3938b-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

