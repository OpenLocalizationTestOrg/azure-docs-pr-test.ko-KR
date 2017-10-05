---
title: "논리 앱에서 되풀이 트리거 추가 | Microsoft Docs"
description: "되풀이 트리거 개요 및 Azure 논리 앱으로 사용하는 방법"
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="1054d-103">되풀이 트리거 시작</span><span class="sxs-lookup"><span data-stu-id="1054d-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="1054d-104">되풀이 트리거를 사용하여 클라우드에서 강력한 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="1054d-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-105">For example, you can:</span></span>

* <span data-ttu-id="1054d-106">SQL 저장 프로시저를 매일 실행하도록 워크플로 예약</span><span class="sxs-lookup"><span data-stu-id="1054d-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="1054d-107">특정 해시 태그에 대한 지난 주의 모든 트윗 요약을 전자 메일로 전송</span><span class="sxs-lookup"><span data-stu-id="1054d-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="1054d-108">논리 앱에서 되풀이 트리거 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1054d-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="1054d-109">되풀이 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="1054d-109">Use a recurrence trigger</span></span>
<span data-ttu-id="1054d-110">트리거는 논리 앱에서 정의된 워크플로를 시작하는 데 사용할 수 있는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="1054d-111">[트리거에 대해 자세히 알아보세요](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1054d-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="1054d-112">논리 앱에서 되풀이 트리거를 설정하는 방법의 예제 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="1054d-113">**되풀이** 트리거를 논리 앱의 첫 번째 단계로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="1054d-114">되풀이 간격에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="1054d-115">논리 앱은 각 시간 간격 후에 실행되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-115">The logic app now starts a run after each interval of time.</span></span>

![HTTP 트리거](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="1054d-117">트리거 세부 정보</span><span class="sxs-lookup"><span data-stu-id="1054d-117">Trigger details</span></span>
<span data-ttu-id="1054d-118">되풀이 트리거에는 구성할 수 있는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="1054d-119">지정된 시간 간격 후 논리 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="1054d-120">A*는 필수 필드 임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="1054d-121">표시 이름</span><span class="sxs-lookup"><span data-stu-id="1054d-121">Display name</span></span> | <span data-ttu-id="1054d-122">속성 이름</span><span class="sxs-lookup"><span data-stu-id="1054d-122">Property name</span></span> | <span data-ttu-id="1054d-123">설명</span><span class="sxs-lookup"><span data-stu-id="1054d-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1054d-124">빈도*</span><span class="sxs-lookup"><span data-stu-id="1054d-124">Frequency*</span></span> |<span data-ttu-id="1054d-125">frequency</span><span class="sxs-lookup"><span data-stu-id="1054d-125">frequency</span></span> |<span data-ttu-id="1054d-126">시간 단위: `Second`, `Minute`, `Hour`, `Day` 또는 `Year`</span><span class="sxs-lookup"><span data-stu-id="1054d-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="1054d-127">간격*</span><span class="sxs-lookup"><span data-stu-id="1054d-127">Interval*</span></span> |<span data-ttu-id="1054d-128">interval</span><span class="sxs-lookup"><span data-stu-id="1054d-128">interval</span></span> |<span data-ttu-id="1054d-129">되풀이에 대해 지정된 빈도 간격</span><span class="sxs-lookup"><span data-stu-id="1054d-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="1054d-130">표준 시간대</span><span class="sxs-lookup"><span data-stu-id="1054d-130">Time Zone</span></span> |<span data-ttu-id="1054d-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="1054d-131">timeZone</span></span> |<span data-ttu-id="1054d-132">UTC 오프셋 없이 시작 시간이 제공될 경우 이 시간대가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="1054d-133">시작 시간</span><span class="sxs-lookup"><span data-stu-id="1054d-133">Start time</span></span> |<span data-ttu-id="1054d-134">startTime</span><span class="sxs-lookup"><span data-stu-id="1054d-134">startTime</span></span> |<span data-ttu-id="1054d-135">[ISO 8601 형식](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations)의 시작 시간</span><span class="sxs-lookup"><span data-stu-id="1054d-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="1054d-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1054d-136">Next steps</span></span>
<span data-ttu-id="1054d-137">이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1054d-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="1054d-138">[API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1054d-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

