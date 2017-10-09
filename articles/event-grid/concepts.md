---
title: "aaaAzure 이벤트 표 형태 개념"
description: "Azure Event Grid 및 해당 개념을 설명합니다. Event Grid의 몇 가지 주요 구성 요소를 정의합니다."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a><span data-ttu-id="ef853-104">Azure Event Grid의 개념</span><span class="sxs-lookup"><span data-stu-id="ef853-104">Concepts in Azure Event Grid</span></span>

<span data-ttu-id="ef853-105">hello Azure 이벤트 표 형태에서 주요 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-105">hello main concepts in Azure Event Grid are:</span></span>

## <a name="events"></a><span data-ttu-id="ef853-106">이벤트</span><span class="sxs-lookup"><span data-stu-id="ef853-106">Events</span></span>

<span data-ttu-id="ef853-107">이벤트는 hello 가장 작은 크기 hello 시스템에서 발생 하는 완벽 하 게 무언가 설명 하는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-107">An event is hello smallest amount of information that fully describes something that happened in hello system.</span></span>  <span data-ttu-id="ef853-108">모든 이벤트에 같은 일반적인 정보: hello 이벤트, 시간 hello 이벤트의 소스 걸린 및 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-108">Every event has common information like: source of hello event, time hello event took place, and unique identifier.</span></span>  <span data-ttu-id="ef853-109">모든 이벤트는 특정 정보는 관련 toohello만 특정 이벤트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-109">Every event also has specific information that is only relevant toohello specific event.</span></span> <span data-ttu-id="ef853-110">예를 들어 Azure 저장소에서 만들어지는 새 파일에 대 한 이벤트 hello lastTimeModified 값과 같은 hello 파일에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-110">For example, an event about a new file being created in Azure Storage contains details about hello file, such as hello lastTimeModified value.</span></span> <span data-ttu-id="ef853-111">또는 가상 컴퓨터가 다시 부팅 하는 방법에 대 한 이벤트 hello 이름 hello 가상 컴퓨터 및 다시 부팅에 대 한 hello 이유를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-111">Or, an event about a virtual machine rebooting contains hello name of hello virtual machine, and hello reason for reboot.</span></span>

## <a name="event-sourcespublishers"></a><span data-ttu-id="ef853-112">이벤트 원본/게시자</span><span class="sxs-lookup"><span data-stu-id="ef853-112">Event sources/publishers</span></span>

<span data-ttu-id="ef853-113">이벤트 소스는 hello 이벤트 상황이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-113">An event source is where hello event happens.</span></span> <span data-ttu-id="ef853-114">예를 들어 Azure 저장소는 이벤트를 생성 하는 blob에 대 한 hello 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-114">For example, Azure Storage is hello event source for blob created events.</span></span> <span data-ttu-id="ef853-115">Azure VM 패브릭은 가상 컴퓨터 이벤트에 대 한 hello 이벤트 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-115">Azure VM Fabric is hello event source for virtual machine events.</span></span> <span data-ttu-id="ef853-116">이벤트 소스는 이벤트 tooEvent 그리드를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-116">Event sources are responsible for publishing events tooEvent Grid.</span></span>

## <a name="topics"></a><span data-ttu-id="ef853-117">토픽</span><span class="sxs-lookup"><span data-stu-id="ef853-117">Topics</span></span>

<span data-ttu-id="ef853-118">게시자는 이벤트를 토픽으로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-118">Publishers categorize events into topics.</span></span> <span data-ttu-id="ef853-119">hello 항목 hello 게시자가 이벤트를 보내는 끝점을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-119">hello topic includes an endpoint where hello publisher sends events.</span></span> <span data-ttu-id="ef853-120">toorespond toocertain 유형의 이벤트를 구독자에 있는 항목 toosubscribe를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-120">toorespond toocertain types of events, subscribers decide which topics toosubscribe to.</span></span> <span data-ttu-id="ef853-121">또한 항목 구독자 어떻게 tooconsume hello 이벤트 적절 하 게 검색할 수 있도록 이벤트 스키마를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-121">Topics also provide an event schema so that subscribers can discover how tooconsume hello events appropriately.</span></span>

<span data-ttu-id="ef853-122">시스템 토픽은 Azure 서비스에서 제공하는 기본 제공 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-122">System topics are built-in topics provided by Azure services.</span></span> <span data-ttu-id="ef853-123">사용자 지정 토픽은 응용 프로그램 및 타사 토픽입니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-123">Custom topics are application and third-party topics.</span></span>

## <a name="event-subscriptions"></a><span data-ttu-id="ef853-124">이벤트 구독</span><span class="sxs-lookup"><span data-stu-id="ef853-124">Event subscriptions</span></span>

<span data-ttu-id="ef853-125">구독은 구독자가 받고자 하는 토픽의 이벤트를 Event Grid에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-125">A subscription instructs Event Grid on which events on a topic a subscriber is interested in receiving.</span></span>  <span data-ttu-id="ef853-126">구독도 어떻게 이벤트 전달 해야 toohello 구독자에 대 한 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-126">A subscription also holds information on how events should be delivered toohello subscriber.</span></span>

## <a name="event-handlers"></a><span data-ttu-id="ef853-127">이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="ef853-127">Event handlers</span></span>

<span data-ttu-id="ef853-128">이벤트 표 형태 측면에서 볼 때 이벤트 처리기는 hello 이벤트가 전송 된 hello 위치를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-128">From an Event Grid perspective, an event handler is hello place where hello event is sent.</span></span> <span data-ttu-id="ef853-129">hello 처리기는 몇 가지 추가 작업 tooprocess hello 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-129">hello handler takes some further action tooprocess hello event.</span></span>  <span data-ttu-id="ef853-130">Event Grid는 여러 구독자 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-130">Event Grid supports multiple subscriber types.</span></span> <span data-ttu-id="ef853-131">구독자의 hello 형식에 따라 이벤트 표 형태에는 hello 이벤트의 다양 한 메커니즘 tooguarantee hello 배달을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-131">Depending on hello type of subscriber, Event Grid follows different mechanisms tooguarantee hello delivery of hello event.</span></span>  <span data-ttu-id="ef853-132">Hello 이벤트 hello 처리기의 상태 코드 반환 될 때까지 HTTP webhook 이벤트 처리기에 대 한 재시도 `200 – OK`합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-132">For HTTP webhook event handlers, hello event is retried until hello handler returns a status code of `200 – OK`.</span></span> <span data-ttu-id="ef853-133">Azure 저장소 큐에 대 한 hello 이벤트 hello 큐 서비스는 hello 큐에 수 toosuccessfully 프로세스 hello 메시지 푸시 될 때까지 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-133">For Azure Storage Queue, hello events are retried until hello Queue service is able toosuccessfully process hello message push into hello queue.</span></span>

## <a name="filters"></a><span data-ttu-id="ef853-134">필터</span><span class="sxs-lookup"><span data-stu-id="ef853-134">Filters</span></span>

<span data-ttu-id="ef853-135">Tooa 항목, 구독 toohello 끝점으로 전송 되는 hello 이벤트를 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-135">When subscribing tooa topic, you can filter hello events that are sent toohello endpoint.</span></span> <span data-ttu-id="ef853-136">이벤트 형식 또는 제목 패턴으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-136">You can filter by event type, or subject pattern.</span></span> <span data-ttu-id="ef853-137">자세한 내용은 [Event Grid 구독 스키마](subscription-creation-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef853-137">For more information, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>

## <a name="security"></a><span data-ttu-id="ef853-138">보안</span><span class="sxs-lookup"><span data-stu-id="ef853-138">Security</span></span>

<span data-ttu-id="ef853-139">이벤트는 tootopics, 구독 및 항목 게시에 대 한 보안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-139">Event provides security for subscribing tootopics, and publishing topics.</span></span> <span data-ttu-id="ef853-140">를 구독 하는 경우에 hello 리소스 또는 항목에 대해 적절 한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-140">When subscribing, you must have adequate permissions on hello resource or topic.</span></span> <span data-ttu-id="ef853-141">를 게시할 때 SAS 토큰 또는 hello 항목에 대 한 키 인증 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-141">When publishing, you must have a SAS token or key authentication for hello topic.</span></span> <span data-ttu-id="ef853-142">자세한 내용은 [Event Grid 보안 및 인증](security-authentication.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef853-142">For more information, see [Event Grid security and authentication](security-authentication.md).</span></span>

## <a name="failed-delivery"></a><span data-ttu-id="ef853-143">배달 실패</span><span class="sxs-lookup"><span data-stu-id="ef853-143">Failed delivery</span></span>

<span data-ttu-id="ef853-144">이벤트 표 형태 hello 구독자의 끝점에서 이벤트를 받았습니다 확인할 수 없는 때 hello 이벤트를 redelivers 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-144">When Event Grid cannot confirm that an event has been received by hello subscriber's endpoint, it redelivers hello event.</span></span> <span data-ttu-id="ef853-145">자세한 내용은 [Event Grid 메시지 배달 및 재시도](delivery-and-retry.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef853-145">For more information, see [Event Grid message delivery and retry](delivery-and-retry.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef853-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef853-146">Next steps</span></span>

* <span data-ttu-id="ef853-147">눈금에는 소개 tooEvent 참조 [이벤트 표 형태에 대 한](overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-147">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="ef853-148">tooquickly 이벤트 표 형태를 사용 하 여 시작 하려면 다음을 참조 하십시오 [Azure 이벤트 표 형태를 사용자 지정 이벤트 만들기 및 경로](custom-event-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef853-148">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
