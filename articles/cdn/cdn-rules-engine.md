---
title: "Azure CDN 규칙 엔진을 사용하여 HTTP 동작 재정의 | Microsoft Docs"
description: "규칙 엔진을 사용하면 특정 유형의 콘텐츠 전달 차단과 같이 Azure CDN에서 HTTP 요청을 처리하는 방식을 사용자 지정하여 캐싱 정책을 정의하고 HTTP 헤더를 수정할 수 있습니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="194b6-103">Azure CDN 규칙 엔진을 사용하여 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="194b6-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="194b6-104">개요</span><span class="sxs-lookup"><span data-stu-id="194b6-104">Overview</span></span>
<span data-ttu-id="194b6-105">규칙 엔진을 사용하면 특정 유형의 콘텐츠 전달 차단과 같이 HTTP 요청이 처리되는 방식을 사용자 지정하여 캐싱 정책을 정의하고 HTTP 헤더를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="194b6-106">이 자습서에서는 CDN 자산의 캐싱 동작을 변경하는 규칙을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="194b6-107">"[참고 항목](#see-also)" 섹션에는 동영상 콘텐츠도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="194b6-108">구문에 대한 자세한 정보는 [규칙 엔진 참조](cdn-rules-engine-reference.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="194b6-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="194b6-109">자습서</span><span class="sxs-lookup"><span data-stu-id="194b6-109">Tutorial</span></span>
1. <span data-ttu-id="194b6-110">CDN 프로필 블레이드에서 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="194b6-112">CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="194b6-113">**HTTP Large** 탭, **규칙 엔진**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="194b6-114">새 규칙에 대한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-114">Options for a new rule are displayed.</span></span>
   
    ![CDN 새 규칙 옵션](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="194b6-116">여러 규칙이 나열된 순서는 규칙이 처리되는 방식에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="194b6-117">후속 규칙은 이전 규칙에서 지정된 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="194b6-118">**이름/설명** 텍스트 상자에 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="194b6-119">규칙이 적용되는 요청의 유형을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="194b6-120">기본적으로 **항상** 일치 조건이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="194b6-121">이 자습서에서는 **항상** 을 사용하므로 선택된 상태 그대로 두면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN 일치 조건](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="194b6-123">드롭다운 목록에서 사용할 수 있는 다양한 유형의 일치 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="194b6-124">일치 조건의 왼쪽에 있는 파란색 정보 아이콘을 클릭하면 현재 선택한 조건을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="194b6-125">조건식의 전체 목록에 대한 자세한 정보는 [규칙 엔진 조건식](cdn-rules-engine-reference-match-conditions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="194b6-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="194b6-126">일치 조건의 전체 목록을 자세하게 보려면 [규칙 엔진 일치 조건 및 기능](cdn-rules-engine-reference-match-conditions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="194b6-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="194b6-127">**기능** 옆에 있는 **+** 단추를 클릭하여 새 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="194b6-128">왼쪽의 드롭다운 목록에서 **Force Internal Max-Age**(내부 Max-Age 강제)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="194b6-129">표시되는 텍스트 상자에 **300**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="194b6-130">나머지 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-130">Leave the remaining default values.</span></span>
   
   ![CDN 기능](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="194b6-132">일치 조건처럼 새 기능의 왼쪽에 있는 파란색 정보 아이콘을 클릭하면 이 기능에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="194b6-133">**Force Internal Max-Age**의 경우 자산의 **Cache-Control** 및 **Expires** 헤더를 재정의하여 CDN 에지 노드가 원본에서 자산을 새로 고치는 시기를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="194b6-134">300초의 경우 원본에서 자산을 새로 고치기 전에 CDN 에지 노드가 자산을 5분 동안 캐시한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="194b6-135">기능의 전체 목록을 자세하게 보려면 [규칙 엔진 기능 세부 정보](cdn-rules-engine-reference-features.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="194b6-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="194b6-136">**추가** 단추를 클릭하여 새 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="194b6-137">이제 새 규칙이 승인 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="194b6-138">승인되면 상태가 **보류 중인 XML**에서 **활성 XML**로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="194b6-139">규칙 변경이 CDN을 통해 전파되기까지 최대 90분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="194b6-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="194b6-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="194b6-140">See also</span></span>
* [<span data-ttu-id="194b6-141">Azure CDN 개요</span><span class="sxs-lookup"><span data-stu-id="194b6-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="194b6-142">규칙 엔진 참조</span><span class="sxs-lookup"><span data-stu-id="194b6-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="194b6-143">규칙 엔진 일치 조건</span><span class="sxs-lookup"><span data-stu-id="194b6-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="194b6-144">규칙 엔진 조건식</span><span class="sxs-lookup"><span data-stu-id="194b6-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="194b6-145">규칙 엔진 기능</span><span class="sxs-lookup"><span data-stu-id="194b6-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="194b6-146">규칙 엔진을 사용하여 기본 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="194b6-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="194b6-147">[Azure Fridays: Azure CDN의 강력하고 새로운 프리미엄 기능](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (동영상)</span><span class="sxs-lookup"><span data-stu-id="194b6-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>