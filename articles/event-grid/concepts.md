---
title: "Azure Event Grid 개념"
description: "Azure Event Grid 및 해당 개념을 설명합니다. Event Grid의 몇 가지 주요 구성 요소를 정의합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: 83b9b2c7bb4134e1d9bdf857449bfb85884333d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="concepts-in-azure-event-grid"></a><span data-ttu-id="d8811-104">Azure Event Grid의 개념</span><span class="sxs-lookup"><span data-stu-id="d8811-104">Concepts in Azure Event Grid</span></span>

<span data-ttu-id="d8811-105">Azure Event Grid의 주요 개념은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-105">The main concepts in Azure Event Grid are:</span></span>

## <a name="events"></a><span data-ttu-id="d8811-106">이벤트</span><span class="sxs-lookup"><span data-stu-id="d8811-106">Events</span></span>

<span data-ttu-id="d8811-107">이벤트는 시스템에서 발생하는 무언가를 완벽히 설명하는 가장 작은 크기의 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-107">An event is the smallest amount of information that fully describes something that happened in the system.</span></span>  <span data-ttu-id="d8811-108">모든 이벤트에는 이벤트의 원본, 이벤트가 발생한 시간 및 고유 식별자와 같은 일반적인 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-108">Every event has common information like: source of the event, time the event took place, and unique identifier.</span></span>  <span data-ttu-id="d8811-109">또한 모든 이벤트에는 특정 이벤트에만 관련된 특정 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-109">Every event also has specific information that is only relevant to the specific event.</span></span> <span data-ttu-id="d8811-110">예를 들어 Azure Storage에서 만들어지는 새 파일에 대한 이벤트에는 lastTimeModified 값과 같이 파일에 대한 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-110">For example, an event about a new file being created in Azure Storage contains details about the file, such as the lastTimeModified value.</span></span> <span data-ttu-id="d8811-111">또는 가상 컴퓨터 다시 부팅에 대한 이벤트에는 가상 컴퓨터의 이름 및 다시 부팅에 대한 이유가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-111">Or, an event about a virtual machine rebooting contains the name of the virtual machine, and the reason for reboot.</span></span>

## <a name="event-sourcespublishers"></a><span data-ttu-id="d8811-112">이벤트 원본/게시자</span><span class="sxs-lookup"><span data-stu-id="d8811-112">Event sources/publishers</span></span>

<span data-ttu-id="d8811-113">이벤트 원본은 이벤트가 발생하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-113">An event source is where the event happens.</span></span> <span data-ttu-id="d8811-114">예를 들어 Azure Storage는 이벤트가 생성된 Blob에 대한 이벤트 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-114">For example, Azure Storage is the event source for blob created events.</span></span> <span data-ttu-id="d8811-115">Azure VM 패브릭은 가상 컴퓨터 이벤트에 대한 이벤트 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-115">Azure VM Fabric is the event source for virtual machine events.</span></span> <span data-ttu-id="d8811-116">이벤트 원본은 이벤트를 Event Grid에 게시하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-116">Event sources are responsible for publishing events to Event Grid.</span></span>

## <a name="topics"></a><span data-ttu-id="d8811-117">토픽</span><span class="sxs-lookup"><span data-stu-id="d8811-117">Topics</span></span>

<span data-ttu-id="d8811-118">게시자는 이벤트를 토픽으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-118">Publishers categorize events into topics.</span></span> <span data-ttu-id="d8811-119">토픽에는 게시자가 이벤트를 보내는 끝점이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-119">The topic includes an endpoint where the publisher sends events.</span></span> <span data-ttu-id="d8811-120">특정 이벤트 형식에 응답하려면 구독자가 구독할 토픽을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-120">To respond to certain types of events, subscribers decide which topics to subscribe to.</span></span> <span data-ttu-id="d8811-121">또한 토픽은 구독자가 이벤트를 적절하게 사용하는 방법을 검색할 수 있도록 이벤트 스키마를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-121">Topics also provide an event schema so that subscribers can discover how to consume the events appropriately.</span></span>

<span data-ttu-id="d8811-122">시스템 토픽은 Azure 서비스에서 제공하는 기본 제공 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-122">System topics are built-in topics provided by Azure services.</span></span> <span data-ttu-id="d8811-123">사용자 지정 토픽은 응용 프로그램 및 타사 토픽입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-123">Custom topics are application and third-party topics.</span></span>

## <a name="event-subscriptions"></a><span data-ttu-id="d8811-124">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="d8811-124">Event subscriptions</span></span>

<span data-ttu-id="d8811-125">구독은 구독자가 받고자 하는 토픽의 이벤트를 Event Grid에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-125">A subscription instructs Event Grid on which events on a topic a subscriber is interested in receiving.</span></span>  <span data-ttu-id="d8811-126">또한 구독에는 이벤트가 구독자에게 어떻게 배달되는지에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-126">A subscription also holds information on how events should be delivered to the subscriber.</span></span>

## <a name="event-handlers"></a><span data-ttu-id="d8811-127">이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="d8811-127">Event handlers</span></span>

<span data-ttu-id="d8811-128">Event Grid 측면에서 볼 때 이벤트 처리기는 이벤트가 전송된 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-128">From an Event Grid perspective, an event handler is the place where the event is sent.</span></span> <span data-ttu-id="d8811-129">처리기는 이벤트를 처리하기 위한 추가 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-129">The handler takes some further action to process the event.</span></span>  <span data-ttu-id="d8811-130">Event Grid는 여러 구독자 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-130">Event Grid supports multiple subscriber types.</span></span> <span data-ttu-id="d8811-131">구독자의 형식에 따라 Event Grid는 이벤트의 배달을 보장하는 다양한 메커니즘을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-131">Depending on the type of subscriber, Event Grid follows different mechanisms to guarantee the delivery of the event.</span></span>  <span data-ttu-id="d8811-132">HTTP 웹후크 이벤트 처리기의 경우 처리기가 `200 – OK`의 상태 코드를 반환할 때까지 이벤트를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-132">For HTTP webhook event handlers, the event is retried until the handler returns a status code of `200 – OK`.</span></span> <span data-ttu-id="d8811-133">Azure Storage Queue의 경우 큐 서비스가 성공적으로 큐에 메시지 푸시를 처리할 수 있을 때까지 이벤트를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-133">For Azure Storage Queue, the events are retried until the Queue service is able to successfully process the message push into the queue.</span></span>

## <a name="filters"></a><span data-ttu-id="d8811-134">필터</span><span class="sxs-lookup"><span data-stu-id="d8811-134">Filters</span></span>

<span data-ttu-id="d8811-135">토픽을 구독하면 끝점에 전송된 이벤트를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-135">When subscribing to a topic, you can filter the events that are sent to the endpoint.</span></span> <span data-ttu-id="d8811-136">이벤트 형식 또는 제목 패턴으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-136">You can filter by event type, or subject pattern.</span></span> <span data-ttu-id="d8811-137">자세한 내용은 [Event Grid 구독 스키마](subscription-creation-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8811-137">For more information, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>

## <a name="security"></a><span data-ttu-id="d8811-138">보안</span><span class="sxs-lookup"><span data-stu-id="d8811-138">Security</span></span>

<span data-ttu-id="d8811-139">이벤트는 토픽 구독 및 토픽 게시에 대한 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-139">Event provides security for subscribing to topics, and publishing topics.</span></span> <span data-ttu-id="d8811-140">구독할 때 리소스 또는 토픽에 대해 적절한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-140">When subscribing, you must have adequate permissions on the resource or topic.</span></span> <span data-ttu-id="d8811-141">게시할 때 토픽에 대한 SAS 토큰 또는 키 인증이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-141">When publishing, you must have a SAS token or key authentication for the topic.</span></span> <span data-ttu-id="d8811-142">자세한 내용은 [Event Grid 보안 및 인증](security-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8811-142">For more information, see [Event Grid security and authentication](security-authentication.md).</span></span>

## <a name="failed-delivery"></a><span data-ttu-id="d8811-143">배달 실패</span><span class="sxs-lookup"><span data-stu-id="d8811-143">Failed delivery</span></span>

<span data-ttu-id="d8811-144">Event Grid에서 이벤트가 구독자의 끝점에서 수신되었는지 확인할 수 없는 경우 이벤트를 다시 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="d8811-144">When Event Grid cannot confirm that an event has been received by the subscriber's endpoint, it redelivers the event.</span></span> <span data-ttu-id="d8811-145">자세한 내용은 [Event Grid 메시지 배달 및 재시도](delivery-and-retry.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8811-145">For more information, see [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8811-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8811-146">Next steps</span></span>

* <span data-ttu-id="d8811-147">Event Grid에 대한 소개는 [Event Grid 정보](overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8811-147">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="d8811-148">Event Grid를 빠르게 시작하려면 [Azure Event Grid를 사용하여 사용자 지정 이벤트 만들기 및 라우팅](custom-event-quickstart.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8811-148">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>