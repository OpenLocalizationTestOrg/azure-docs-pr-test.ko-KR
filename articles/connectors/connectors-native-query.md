---
title: "논리 앱에서 aaaAdd hello 쿼리 작업 | Microsoft Docs"
description: "필터 배열 처럼 동작을 수행 하는 것에 대 한 hello 쿼리 작업의 개요입니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="318cb-103">Hello 쿼리 작업 시작</span><span class="sxs-lookup"><span data-stu-id="318cb-103">Get started with hello query action</span></span>
<span data-ttu-id="318cb-104">Hello 쿼리 작업을 사용 하 여 일괄 처리 및 배열 tooaccomplish 워크플로를 사용 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="318cb-105">데이터베이스에서 모든 높은 우선순위 레코드에 대한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="318cb-106">전자 메일에 대한 모든 PDF 첨부 파일을 Azure Blob에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="318cb-107">tooget hello 쿼리 동작을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="318cb-108">Hello 쿼리 동작을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="318cb-108">Use hello query action</span></span>
<span data-ttu-id="318cb-109">동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="318cb-110">[작업에 대해 자세히 알아봅니다.](connectors-overview.md)</span><span class="sxs-lookup"><span data-stu-id="318cb-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="318cb-111">hello 쿼리 작업에는 현재 hello 디자이너에서 제공 되는 hello 필터 배열 이라는 한 번의 작업을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="318cb-112">이 배열 tooquery 있으며 필터링 된 결과 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="318cb-113">논리 앱에서 이를 추가하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="318cb-114">선택 hello **새 단계** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="318cb-115">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="318cb-116">Hello 동작 검색 상자에 입력 **필터** toolist hello **필터 배열** 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Hello 쿼리 작업을 선택](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="318cb-118">배열 toofilter를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-118">Select an array toofilter.</span></span> <span data-ttu-id="318cb-119">(hello 다음 스크린샷은 Twitter 검색에서 결과의 hello 배열입니다.)</span><span class="sxs-lookup"><span data-stu-id="318cb-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="318cb-120">각 항목에 조건이 tooevaluate를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="318cb-121">(다음 스크린샷 hello 100 개가 넘는 후속 작업이 사용자 로부터 트 윗을 필터링 합니다.)</span><span class="sxs-lookup"><span data-stu-id="318cb-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![전체 hello 쿼리 작업](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="318cb-123">hello 작업 hello 필터 요구 사항을 충족 하는 결과만 포함 하는 새 배열을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="318cb-124">Hello 도구 모음 toosave와 여 논리 앱에서 모두 저장 hello 왼쪽 위 모퉁이 클릭 하 고 게시 (활성화).</span><span class="sxs-lookup"><span data-stu-id="318cb-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="318cb-125">쿼리 작업</span><span class="sxs-lookup"><span data-stu-id="318cb-125">Query action</span></span>
<span data-ttu-id="318cb-126">이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="318cb-127">hello 커넥터에 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="318cb-128">동작</span><span class="sxs-lookup"><span data-stu-id="318cb-128">Action</span></span> | <span data-ttu-id="318cb-129">설명</span><span class="sxs-lookup"><span data-stu-id="318cb-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="318cb-130">배열 필터링</span><span class="sxs-lookup"><span data-stu-id="318cb-130">Filter array</span></span> |<span data-ttu-id="318cb-131">배열에 있는 각 항목에 대 한 조건을 평가 하 고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="318cb-132">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="318cb-132">Action details</span></span>
<span data-ttu-id="318cb-133">hello 쿼리 작업은 작업을 사용할 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="318cb-134">hello 다음 표에서 필요한 hello 및 hello 작업과 hello 동작을 사용 하 여 연관 된 hello 해당 하는 출력 정보에 대 한 선택적 입력된 필드.</span><span class="sxs-lookup"><span data-stu-id="318cb-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="318cb-135">배열 필터링</span><span class="sxs-lookup"><span data-stu-id="318cb-135">Filter array</span></span>
<span data-ttu-id="318cb-136">hello 다음은 아웃 바운드 HTTP 요청을 낮추는 hello 동작에 대 한 입력된 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="318cb-137">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="318cb-138">표시 이름</span><span class="sxs-lookup"><span data-stu-id="318cb-138">Display name</span></span> | <span data-ttu-id="318cb-139">속성 이름</span><span class="sxs-lookup"><span data-stu-id="318cb-139">Property name</span></span> | <span data-ttu-id="318cb-140">설명</span><span class="sxs-lookup"><span data-stu-id="318cb-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="318cb-141">원본*</span><span class="sxs-lookup"><span data-stu-id="318cb-141">From*</span></span> |<span data-ttu-id="318cb-142">from</span><span class="sxs-lookup"><span data-stu-id="318cb-142">from</span></span> |<span data-ttu-id="318cb-143">hello 배열 toofilter</span><span class="sxs-lookup"><span data-stu-id="318cb-143">hello array toofilter</span></span> |
| <span data-ttu-id="318cb-144">조건*</span><span class="sxs-lookup"><span data-stu-id="318cb-144">Condition*</span></span> |<span data-ttu-id="318cb-145">여기서,</span><span class="sxs-lookup"><span data-stu-id="318cb-145">where</span></span> |<span data-ttu-id="318cb-146">각 항목에 대 한 hello 조건 tooevaluate</span><span class="sxs-lookup"><span data-stu-id="318cb-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="318cb-147">출력 세부 정보</span><span class="sxs-lookup"><span data-stu-id="318cb-147">Output details</span></span>
<span data-ttu-id="318cb-148">hello 다음은 hello HTTP 응답에 대 한 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="318cb-149">속성 이름</span><span class="sxs-lookup"><span data-stu-id="318cb-149">Property name</span></span> | <span data-ttu-id="318cb-150">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="318cb-150">Data type</span></span> | <span data-ttu-id="318cb-151">설명</span><span class="sxs-lookup"><span data-stu-id="318cb-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="318cb-152">필터링된 배열</span><span class="sxs-lookup"><span data-stu-id="318cb-152">Filtered array</span></span> |<span data-ttu-id="318cb-153">array</span><span class="sxs-lookup"><span data-stu-id="318cb-153">array</span></span> |<span data-ttu-id="318cb-154">각 필터링된 결과에 대한 개체를 포함하는 배열</span><span class="sxs-lookup"><span data-stu-id="318cb-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="318cb-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="318cb-155">Next steps</span></span>
<span data-ttu-id="318cb-156">이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="318cb-157">탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="318cb-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

