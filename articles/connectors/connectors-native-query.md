---
title: "논리 앱에서 쿼리 작업 추가 | Microsoft Docs"
description: "배열 필터링과 같은 작업을 수행하기 위한 쿼리 작업의 개요입니다."
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="79769-103">쿼리 작업 시작</span><span class="sxs-lookup"><span data-stu-id="79769-103">Get started with the query action</span></span>
<span data-ttu-id="79769-104">쿼리 작업을 사용하면 배치 및 배열을 통해 다음을 수행하는 워크플로를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="79769-105">데이터베이스에서 모든 높은 우선순위 레코드에 대한 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79769-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="79769-106">전자 메일에 대한 모든 PDF 첨부 파일을 Azure Blob에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="79769-107">논리 앱에서 쿼리 작업 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79769-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="79769-108">쿼리 작업 사용</span><span class="sxs-lookup"><span data-stu-id="79769-108">Use the query action</span></span>
<span data-ttu-id="79769-109">작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="79769-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="79769-110">[작업에 대해 자세히 알아봅니다](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="79769-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="79769-111">쿼리 작업에는 디자이너에 표시되는 배열 필터링이라는 작업 한 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="79769-112">이를 통해 배열을 쿼리하고 필터링된 결과 집합을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="79769-113">논리 앱에서 이를 추가하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="79769-114">**새 단계** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="79769-115">**작업 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="79769-116">작업 검색 상자에 **filter**를 입력하여 **배열 필터링** 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![쿼리 작업 선택](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="79769-118">필터링할 배열을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-118">Select an array to filter.</span></span> <span data-ttu-id="79769-119">(다음 스크린샷은 Twitter 검색에서 결과의 배열을 표시합니다.)</span><span class="sxs-lookup"><span data-stu-id="79769-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="79769-120">각 항목에 대해 평가할 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79769-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="79769-121">(다음 스크린샷은 폴로워가 100명 이상인 사용자로부터 오는 트윗을 필터링합니다.)</span><span class="sxs-lookup"><span data-stu-id="79769-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![쿼리 작업 완료](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="79769-123">이 작업은 필터 요구 사항을 충족하는 결과만 포함하는 새 배열을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="79769-124">도구 모음의 왼쪽 위 모서리를 클릭하여 저장하면 논리 앱이 저장하고 게시합니다(활성화).</span><span class="sxs-lookup"><span data-stu-id="79769-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="79769-125">쿼리 작업</span><span class="sxs-lookup"><span data-stu-id="79769-125">Query action</span></span>
<span data-ttu-id="79769-126">여기에는 이 커넥터가 지원하는 작업에 대한 세부 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="79769-127">커넥터에는 한 개의 가능한 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-127">The connector has one possible action.</span></span>

| <span data-ttu-id="79769-128">작업</span><span class="sxs-lookup"><span data-stu-id="79769-128">Action</span></span> | <span data-ttu-id="79769-129">설명</span><span class="sxs-lookup"><span data-stu-id="79769-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="79769-130">배열 필터링</span><span class="sxs-lookup"><span data-stu-id="79769-130">Filter array</span></span> |<span data-ttu-id="79769-131">배열에 있는 각 항목에 대한 조건을 평가하고 결과를 반환</span><span class="sxs-lookup"><span data-stu-id="79769-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="79769-132">작업 세부 정보</span><span class="sxs-lookup"><span data-stu-id="79769-132">Action details</span></span>
<span data-ttu-id="79769-133">쿼리 작업은 한 개의 가능한 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-133">The query action comes with one possible action.</span></span> <span data-ttu-id="79769-134">다음 표에서는 작업의 필수 및 선택적 입력 필드와 함께 작업 사용과 연관된 해당 출력 세부 정보를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="79769-135">배열 필터링</span><span class="sxs-lookup"><span data-stu-id="79769-135">Filter array</span></span>
<span data-ttu-id="79769-136">HTTP 아웃바운드 요청을 하는 작업에 대한 입력 필드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="79769-137">*는 필수 필드임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="79769-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="79769-138">표시 이름</span><span class="sxs-lookup"><span data-stu-id="79769-138">Display name</span></span> | <span data-ttu-id="79769-139">속성 이름</span><span class="sxs-lookup"><span data-stu-id="79769-139">Property name</span></span> | <span data-ttu-id="79769-140">설명</span><span class="sxs-lookup"><span data-stu-id="79769-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79769-141">원본*</span><span class="sxs-lookup"><span data-stu-id="79769-141">From*</span></span> |<span data-ttu-id="79769-142">from</span><span class="sxs-lookup"><span data-stu-id="79769-142">from</span></span> |<span data-ttu-id="79769-143">필터링할 배열</span><span class="sxs-lookup"><span data-stu-id="79769-143">The array to filter</span></span> |
| <span data-ttu-id="79769-144">조건*</span><span class="sxs-lookup"><span data-stu-id="79769-144">Condition*</span></span> |<span data-ttu-id="79769-145">여기서,</span><span class="sxs-lookup"><span data-stu-id="79769-145">where</span></span> |<span data-ttu-id="79769-146">각 항목에 대해 평가할 조건</span><span class="sxs-lookup"><span data-stu-id="79769-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="79769-147">출력 세부 정보</span><span class="sxs-lookup"><span data-stu-id="79769-147">Output details</span></span>
<span data-ttu-id="79769-148">HTTP 요청에 대한 출력 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="79769-149">속성 이름</span><span class="sxs-lookup"><span data-stu-id="79769-149">Property name</span></span> | <span data-ttu-id="79769-150">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="79769-150">Data type</span></span> | <span data-ttu-id="79769-151">설명</span><span class="sxs-lookup"><span data-stu-id="79769-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79769-152">필터링된 배열</span><span class="sxs-lookup"><span data-stu-id="79769-152">Filtered array</span></span> |<span data-ttu-id="79769-153">array</span><span class="sxs-lookup"><span data-stu-id="79769-153">array</span></span> |<span data-ttu-id="79769-154">각 필터링된 결과에 대한 개체를 포함하는 배열</span><span class="sxs-lookup"><span data-stu-id="79769-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="79769-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="79769-155">Next steps</span></span>
<span data-ttu-id="79769-156">이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="79769-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="79769-157">[API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79769-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

