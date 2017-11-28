---
title: "논리 앱에서 aaaAdd hello 되풀이 트리거 | Microsoft Docs"
description: "Hello 되풀이 트리거의 개요 및 방법을 toouse Azure 논리 앱으로 합니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="639e0-103">Hello 되풀이 트리거 시작</span><span class="sxs-lookup"><span data-stu-id="639e0-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="639e0-104">Hello 되풀이 트리거를 사용 하 여 hello 클라우드에서 강력한 워크플로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="639e0-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-105">For example, you can:</span></span>

* <span data-ttu-id="639e0-106">매일 워크플로 toorun SQL 저장 프로시저를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="639e0-107">모든 트 윗 hello에 대 한 특정 hashtag 지난 주에 대 한 요약 전자 메일입니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="639e0-108">hello 되풀이 트리거를 사용 하 여 논리 앱의 시작 tooget 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="639e0-109">되풀이 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="639e0-109">Use a recurrence trigger</span></span>
<span data-ttu-id="639e0-110">트리거는 사용 되는 toostart hello 워크플로 논리 앱에 정의 된 일 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="639e0-111">[트리거에 대해 자세히 알아보세요.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="639e0-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="639e0-112">시퀀스 tooset 되풀이를 트리거할 논리 앱 방법의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="639e0-113">Hello 추가 **되풀이** 트리거 논리 앱의 첫 번째 단계로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="639e0-114">Hello 되풀이 간격에 대 한 hello 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="639e0-115">hello 논리 앱 각 시간 간격 이후에 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-115">hello logic app now starts a run after each interval of time.</span></span>

![HTTP 트리거](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="639e0-117">트리거 세부 정보</span><span class="sxs-lookup"><span data-stu-id="639e0-117">Trigger details</span></span>
<span data-ttu-id="639e0-118">hello 되풀이 트리거 hello 다음과 같은 구성할 수 있는 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="639e0-119">지정된 시간 간격 후 논리 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="639e0-120">A*는 필수 필드 임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="639e0-121">표시 이름</span><span class="sxs-lookup"><span data-stu-id="639e0-121">Display name</span></span> | <span data-ttu-id="639e0-122">속성 이름</span><span class="sxs-lookup"><span data-stu-id="639e0-122">Property name</span></span> | <span data-ttu-id="639e0-123">설명</span><span class="sxs-lookup"><span data-stu-id="639e0-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="639e0-124">빈도*</span><span class="sxs-lookup"><span data-stu-id="639e0-124">Frequency*</span></span> |<span data-ttu-id="639e0-125">frequency</span><span class="sxs-lookup"><span data-stu-id="639e0-125">frequency</span></span> |<span data-ttu-id="639e0-126">시간 단위 hello: `Second`, `Minute`, `Hour`, `Day`, 또는 `Year`합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="639e0-127">간격*</span><span class="sxs-lookup"><span data-stu-id="639e0-127">Interval*</span></span> |<span data-ttu-id="639e0-128">interval</span><span class="sxs-lookup"><span data-stu-id="639e0-128">interval</span></span> |<span data-ttu-id="639e0-129">hello 간격 hello 되풀이 빈도 지정 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="639e0-130">표준 시간대</span><span class="sxs-lookup"><span data-stu-id="639e0-130">Time Zone</span></span> |<span data-ttu-id="639e0-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="639e0-131">timeZone</span></span> |<span data-ttu-id="639e0-132">UTC 오프셋 없이 시작 시간이 제공될 경우 이 시간대가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="639e0-133">시작 시간</span><span class="sxs-lookup"><span data-stu-id="639e0-133">Start time</span></span> |<span data-ttu-id="639e0-134">startTime</span><span class="sxs-lookup"><span data-stu-id="639e0-134">startTime</span></span> |<span data-ttu-id="639e0-135">hello 시작 시간 [ISO 8601 형식](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="639e0-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="639e0-136">Next steps</span></span>
<span data-ttu-id="639e0-137">이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="639e0-138">탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="639e0-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

