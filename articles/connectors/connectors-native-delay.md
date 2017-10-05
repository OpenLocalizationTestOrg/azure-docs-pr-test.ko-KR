---
title: "논리 앱에 지연 추가 | Microsoft Docs"
description: "지연 및 다음 기간까지 지연 동작에 대한 개요와 Azure 논리 앱에서 이를 사용하는 방법을 설명합니다."
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="064a0-103">지연 및 다음 기간까지 지연 동작 시작</span><span class="sxs-lookup"><span data-stu-id="064a0-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="064a0-104">지연 및 다음 기간까지 지연 동작을 사용하여 워크플로 시나리오를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="064a0-105">예를 들어 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-105">For example, you can:</span></span>

* <span data-ttu-id="064a0-106">평일까지 기다렸다가 전자 메일로 상태 업데이트 전송</span><span class="sxs-lookup"><span data-stu-id="064a0-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="064a0-107">다시 시작하고 결과를 검색하기 전에 HTTP 호출이 완료될 때까지 워크플로 지연</span><span class="sxs-lookup"><span data-stu-id="064a0-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="064a0-108">논리 앱에서 지연 동작 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="064a0-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="064a0-109">지연 작업 사용</span><span class="sxs-lookup"><span data-stu-id="064a0-109">Use the delay actions</span></span>
<span data-ttu-id="064a0-110">동작은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="064a0-111">[작업에 대해 자세히 알아봅니다](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="064a0-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="064a0-112">논리 앱에서 지연 단계는 사용하는 방법의 예제 시퀀스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="064a0-113">트리거를 추가한 후 **새 단계** 를 클릭하여 동작을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="064a0-114">**delay** 를 검색하여 지연 동작을 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="064a0-115">이 예제에서는 **지연**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-115">In this example, we will select **Delay**.</span></span>
   
    ![지연 작업](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="064a0-117">동작 속성을 완료하여 지연을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![지연 구성](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="064a0-119">**저장** 을 클릭하여 논리 앱을 게시하고 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="064a0-120">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="064a0-120">Action details</span></span>
<span data-ttu-id="064a0-121">되풀이 트리거에는 구성할 수 있는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="064a0-122">지연 동작</span><span class="sxs-lookup"><span data-stu-id="064a0-122">Delay action</span></span>
<span data-ttu-id="064a0-123">이 동작은 특정 시간 간격 동안 실행을 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="064a0-124">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="064a0-125">표시 이름</span><span class="sxs-lookup"><span data-stu-id="064a0-125">Display name</span></span> | <span data-ttu-id="064a0-126">속성 이름</span><span class="sxs-lookup"><span data-stu-id="064a0-126">Property name</span></span> | <span data-ttu-id="064a0-127">설명</span><span class="sxs-lookup"><span data-stu-id="064a0-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="064a0-128">Count*</span><span class="sxs-lookup"><span data-stu-id="064a0-128">Count*</span></span> |<span data-ttu-id="064a0-129">count</span><span class="sxs-lookup"><span data-stu-id="064a0-129">count</span></span> |<span data-ttu-id="064a0-130">지연할 시간 단위 수</span><span class="sxs-lookup"><span data-stu-id="064a0-130">The number of time units to delay</span></span> |
| <span data-ttu-id="064a0-131">Unit*</span><span class="sxs-lookup"><span data-stu-id="064a0-131">Unit*</span></span> |<span data-ttu-id="064a0-132">단위</span><span class="sxs-lookup"><span data-stu-id="064a0-132">unit</span></span> |<span data-ttu-id="064a0-133">시간 단위: `Second`, `Minute`, `Hour` 또는 `Day`</span><span class="sxs-lookup"><span data-stu-id="064a0-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="064a0-134">다음 기간까지 지연 동작</span><span class="sxs-lookup"><span data-stu-id="064a0-134">Delay-until action</span></span>
<span data-ttu-id="064a0-135">이 동작은 지정된 날짜/시간까지 실행을 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="064a0-136">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="064a0-137">표시 이름</span><span class="sxs-lookup"><span data-stu-id="064a0-137">Display name</span></span> | <span data-ttu-id="064a0-138">속성 이름</span><span class="sxs-lookup"><span data-stu-id="064a0-138">Property name</span></span> | <span data-ttu-id="064a0-139">설명</span><span class="sxs-lookup"><span data-stu-id="064a0-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="064a0-140">Year*</span><span class="sxs-lookup"><span data-stu-id="064a0-140">Year*</span></span> |<span data-ttu-id="064a0-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="064a0-141">timestamp</span></span> |<span data-ttu-id="064a0-142">다음까지 지연 연도(GMT)</span><span class="sxs-lookup"><span data-stu-id="064a0-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="064a0-143">Month*</span><span class="sxs-lookup"><span data-stu-id="064a0-143">Month*</span></span> |<span data-ttu-id="064a0-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="064a0-144">timestamp</span></span> |<span data-ttu-id="064a0-145">다음가지 지연 월(GMT)</span><span class="sxs-lookup"><span data-stu-id="064a0-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="064a0-146">Day*</span><span class="sxs-lookup"><span data-stu-id="064a0-146">Day*</span></span> |<span data-ttu-id="064a0-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="064a0-147">timestamp</span></span> |<span data-ttu-id="064a0-148">다음까지 지연 일(GMT)</span><span class="sxs-lookup"><span data-stu-id="064a0-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="064a0-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="064a0-149">Next steps</span></span>
<span data-ttu-id="064a0-150">이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="064a0-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="064a0-151">[API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064a0-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

