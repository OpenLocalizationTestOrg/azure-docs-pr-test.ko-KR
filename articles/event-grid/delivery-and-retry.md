---
title: "aaaAzure 이벤트 표 형태 배달 및 다시 시도"
description: "Azure Event Grid에서 이벤트를 배달하는 방법 및 배달되지 않은 메시지를 처리하는 방법을 설명합니다."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="fba29-103">Event Grid 메시지 배달 및 다시 시도</span><span class="sxs-lookup"><span data-stu-id="fba29-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="fba29-104">이 문서에서는 Azure Event Grid에서 배달이 승인되지 않는 경우 이벤트를 처리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="fba29-105">Event Grid는 지속성이 있는 배달을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="fba29-106">각 메시지를 각 구독에 대해 최소 한 번 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="fba29-107">이벤트 등록 toohello webhook 각 구독을 즉시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="fba29-108">webhook 이벤트 수신을 확인 하지 않습니다 hello 첫 번째 배달의 60 초 이내 시도, 이벤트 표 형태 hello 이벤트의 배달을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="fba29-109">메시지 배달 상태</span><span class="sxs-lookup"><span data-stu-id="fba29-109">Message delivery status</span></span>

<span data-ttu-id="fba29-110">이벤트 표 형태는 HTTP 응답 코드 tooacknowledge 수신 이벤트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="fba29-111">성공 코드</span><span class="sxs-lookup"><span data-stu-id="fba29-111">Success codes</span></span>

<span data-ttu-id="fba29-112">hello HTTP 응답 코드를 다음 표시 하는 이벤트에 성공적으로 배달 되었습니다 tooyour webhook 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="fba29-113">Event Grid는 배달이 완료되었다고 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="fba29-114">200 정상</span><span class="sxs-lookup"><span data-stu-id="fba29-114">200 OK</span></span>
- <span data-ttu-id="fba29-115">202 수락됨</span><span class="sxs-lookup"><span data-stu-id="fba29-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="fba29-116">실패 코드</span><span class="sxs-lookup"><span data-stu-id="fba29-116">Failure codes</span></span>

<span data-ttu-id="fba29-117">HTTP 응답 코드를 다음 hello 이벤트 배달 시도가 실패 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="fba29-118">이벤트 표 형태 toosend hello 이벤트를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="fba29-119">400 잘못된 요청</span><span class="sxs-lookup"><span data-stu-id="fba29-119">400 Bad Request</span></span>
- <span data-ttu-id="fba29-120">401 권한 없음</span><span class="sxs-lookup"><span data-stu-id="fba29-120">401 Unauthorized</span></span>
- <span data-ttu-id="fba29-121">404 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="fba29-121">404 Not Found</span></span>
- <span data-ttu-id="fba29-122">408 요청 시간 초과</span><span class="sxs-lookup"><span data-stu-id="fba29-122">408 Request timeout</span></span>
- <span data-ttu-id="fba29-123">414 URI가 너무 김</span><span class="sxs-lookup"><span data-stu-id="fba29-123">414 URI Too Long</span></span>
- <span data-ttu-id="fba29-124">500 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="fba29-124">500 Internal Server Error</span></span>
- <span data-ttu-id="fba29-125">503 서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="fba29-125">503 Service Unavailable</span></span>
- <span data-ttu-id="fba29-126">504 게이트웨이 시간 초과</span><span class="sxs-lookup"><span data-stu-id="fba29-126">504 Gateway Timeout</span></span>

<span data-ttu-id="fba29-127">다른 모든 응답 코드 또는 응답의 부족은 오류가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="fba29-128">Event Grid는 배달을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="fba29-129">재시도 간격</span><span class="sxs-lookup"><span data-stu-id="fba29-129">Retry intervals</span></span>

<span data-ttu-id="fba29-130">Event Grid는 이벤트 배달에 대해 지수 백오프 재시도 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="fba29-131">프로그램 webhook 응답 하지 않으면 오류 코드가 반환, 이벤트 표 형태 일정에 따라 hello에서 배달을 다시 시도:</span><span class="sxs-lookup"><span data-stu-id="fba29-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="fba29-132">10초</span><span class="sxs-lookup"><span data-stu-id="fba29-132">10 seconds</span></span>
2. <span data-ttu-id="fba29-133">30초</span><span class="sxs-lookup"><span data-stu-id="fba29-133">30 seconds</span></span>
3. <span data-ttu-id="fba29-134">1분</span><span class="sxs-lookup"><span data-stu-id="fba29-134">1 minute</span></span>
4. <span data-ttu-id="fba29-135">5분</span><span class="sxs-lookup"><span data-stu-id="fba29-135">5 minutes</span></span>
5. <span data-ttu-id="fba29-136">10분</span><span class="sxs-lookup"><span data-stu-id="fba29-136">10 minutes</span></span>
6. <span data-ttu-id="fba29-137">30분</span><span class="sxs-lookup"><span data-stu-id="fba29-137">30 minutes</span></span>
7. <span data-ttu-id="fba29-138">1시간</span><span class="sxs-lookup"><span data-stu-id="fba29-138">1 hour</span></span>

<span data-ttu-id="fba29-139">작은 임의 tooall 다시 시도 간격을 추가 하는 이벤트 표 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="fba29-140">다시 시도 기간</span><span class="sxs-lookup"><span data-stu-id="fba29-140">Retry duration</span></span>

<span data-ttu-id="fba29-141">Azure 이벤트 표 형태 hello 미리 보기 기간 동안 2 시간 이내에 배달 되지 않는 모든 이벤트에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="fba29-142">일반 공급 전에이 시간 증가 too24 시간 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fba29-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fba29-143">Next steps</span></span>

* <span data-ttu-id="fba29-144">눈금에는 소개 tooEvent 참조 [이벤트 표 형태에 대 한](overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="fba29-145">tooquickly 이벤트 표 형태를 사용 하 여 시작 하려면 다음을 참조 하십시오 [Azure 이벤트 표 형태를 사용자 지정 이벤트 만들기 및 경로](custom-event-quickstart.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fba29-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
