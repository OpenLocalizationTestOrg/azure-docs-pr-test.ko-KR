---
title: "논리 앱의 지연 aaaAdd | Microsoft Docs"
description: "Hello 간략하게 지연 시간 및 지연을-동작, 방법과 toouse Azure 논리 앱을 사용 하 여 합니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="2adcc-103">Hello로 시작 지연 시간 및 지연을-동작</span><span class="sxs-lookup"><span data-stu-id="2adcc-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="2adcc-104">Hello 지연을 사용 하 여 및 "지연-될 때까지" 작업을 워크플로 시나리오를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="2adcc-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-105">For example, you can:</span></span>

* <span data-ttu-id="2adcc-106">전자 메일을 통해 평일 toosend 상태가 업데이트 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="2adcc-107">HTTP 호출 될 때까지 지연 hello 워크플로 다시 시작 하 고 hello 결과 검색 하기 전에 시간 toofinish에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="2adcc-108">tooget hello 지연 작업을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="2adcc-109">Hello 지연 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2adcc-109">Use hello delay actions</span></span>
<span data-ttu-id="2adcc-110">동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="2adcc-111">[작업에 대해 자세히 알아봅니다.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2adcc-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="2adcc-112">시퀀스 toouse 지연 단계 논리 앱 방법의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="2adcc-113">트리거를 추가한 후 클릭 **새 단계** tooadd 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="2adcc-114">검색할 **지연** toobring hello 지연 동작을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="2adcc-115">이 예제에서는 **지연**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-115">In this example, we will select **Delay**.</span></span>
   
    ![지연 작업](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="2adcc-117">Hello 동작 속성 tooconfigure hello 지연 중 하나를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![지연 구성](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="2adcc-119">클릭 **저장** toopublish hello 논리 앱을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="2adcc-120">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2adcc-120">Action details</span></span>
<span data-ttu-id="2adcc-121">hello 되풀이 트리거 hello 다음과 같은 구성 될 수 있는 속성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="2adcc-122">지연 동작</span><span class="sxs-lookup"><span data-stu-id="2adcc-122">Delay action</span></span>
<span data-ttu-id="2adcc-123">이 작업 시간 지연 hello 특정 시간 간격에 대 한 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="2adcc-124">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="2adcc-125">표시 이름</span><span class="sxs-lookup"><span data-stu-id="2adcc-125">Display name</span></span> | <span data-ttu-id="2adcc-126">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2adcc-126">Property name</span></span> | <span data-ttu-id="2adcc-127">설명</span><span class="sxs-lookup"><span data-stu-id="2adcc-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2adcc-128">Count*</span><span class="sxs-lookup"><span data-stu-id="2adcc-128">Count*</span></span> |<span data-ttu-id="2adcc-129">count</span><span class="sxs-lookup"><span data-stu-id="2adcc-129">count</span></span> |<span data-ttu-id="2adcc-130">시간 단위 toodelay hello 수</span><span class="sxs-lookup"><span data-stu-id="2adcc-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="2adcc-131">Unit*</span><span class="sxs-lookup"><span data-stu-id="2adcc-131">Unit*</span></span> |<span data-ttu-id="2adcc-132">단위</span><span class="sxs-lookup"><span data-stu-id="2adcc-132">unit</span></span> |<span data-ttu-id="2adcc-133">시간 단위 hello: `Second`, `Minute`, `Hour`, 또는`Day`</span><span class="sxs-lookup"><span data-stu-id="2adcc-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="2adcc-134">다음 기간까지 지연 동작</span><span class="sxs-lookup"><span data-stu-id="2adcc-134">Delay-until action</span></span>
<span data-ttu-id="2adcc-135">이 작업에 지정된 된 날짜/시간까지 실행 하는 hello를 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="2adcc-136">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="2adcc-137">표시 이름</span><span class="sxs-lookup"><span data-stu-id="2adcc-137">Display name</span></span> | <span data-ttu-id="2adcc-138">속성 이름</span><span class="sxs-lookup"><span data-stu-id="2adcc-138">Property name</span></span> | <span data-ttu-id="2adcc-139">설명</span><span class="sxs-lookup"><span data-stu-id="2adcc-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2adcc-140">Year*</span><span class="sxs-lookup"><span data-stu-id="2adcc-140">Year*</span></span> |<span data-ttu-id="2adcc-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="2adcc-141">timestamp</span></span> |<span data-ttu-id="2adcc-142">hello 연도 toodelay (GMT)까지</span><span class="sxs-lookup"><span data-stu-id="2adcc-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="2adcc-143">Month*</span><span class="sxs-lookup"><span data-stu-id="2adcc-143">Month*</span></span> |<span data-ttu-id="2adcc-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="2adcc-144">timestamp</span></span> |<span data-ttu-id="2adcc-145">hello 월 toodelay (GMT)까지</span><span class="sxs-lookup"><span data-stu-id="2adcc-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="2adcc-146">Day*</span><span class="sxs-lookup"><span data-stu-id="2adcc-146">Day*</span></span> |<span data-ttu-id="2adcc-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="2adcc-147">timestamp</span></span> |<span data-ttu-id="2adcc-148">hello 일 toodelay (GMT)까지</span><span class="sxs-lookup"><span data-stu-id="2adcc-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="2adcc-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2adcc-149">Next steps</span></span>
<span data-ttu-id="2adcc-150">이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="2adcc-151">탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2adcc-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

