---
title: "hello Azure CDN 규칙 엔진을 사용 하 여 HTTP aaaOverride 동작 | Microsoft Docs"
description: "hello 규칙 엔진 toocustomize를 캐싱 정책을 정의 하 고 HTTP 헤더를 수정 하는 특정 유형의 콘텐츠를 차단 hello 배달와 같은 HTTP 요청 Azure CDN에서 처리 하는 방법이 있습니다."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="5a00b-103">Hello Azure CDN 규칙 엔진을 사용 하 여 HTTP 동작을 재정의</span><span class="sxs-lookup"><span data-stu-id="5a00b-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="5a00b-104">개요</span><span class="sxs-lookup"><span data-stu-id="5a00b-104">Overview</span></span>
<span data-ttu-id="5a00b-105">hello 규칙 엔진에서는 특정 유형의 콘텐츠를 배달 hello 차단 캐싱 정책을 정의 HTTP 헤더를 수정 등으로 HTTP 요청 처리 되는 방법을 toocustomize가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="5a00b-106">이 자습서에서는 캐싱 동작 CDN 자산 hello는 규칙을 만들 바뀝니다 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="5a00b-107">Hello에서 사용할 수 있는 비디오 콘텐츠도는 "[참조](#see-also)" 섹션.</span><span class="sxs-lookup"><span data-stu-id="5a00b-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="5a00b-108">자세히 참조 toohello 구문에 대 한 참조 [규칙 엔진 참조](cdn-rules-engine-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="5a00b-109">자습서</span><span class="sxs-lookup"><span data-stu-id="5a00b-109">Tutorial</span></span>
1. <span data-ttu-id="5a00b-110">Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="5a00b-112">hello CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="5a00b-113">Hello 클릭 **HTTP 큰** 탭, **규칙 엔진**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="5a00b-114">새 규칙에 대한 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-114">Options for a new rule are displayed.</span></span>
   
    ![CDN 새 규칙 옵션](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="5a00b-116">hello 나열 된 여러 규칙의 영향을 줍니다 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="5a00b-117">후속 규칙 이전 규칙에 지정 된 hello 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="5a00b-118">Hello에 이름을 입력 **이름 / 설명** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="5a00b-119">Hello 규칙을 적용할 요청 hello 유형을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="5a00b-120">기본적으로 hello **항상** 일치 조건을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="5a00b-121">이 자습서에서는 **항상** 을 사용하므로 선택된 상태 그대로 두면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN 일치 조건](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="5a00b-123">Hello 드롭다운에서 사용할 수 있는 조건은 다양 한 유형의 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="5a00b-124">왼쪽의 일치 조건 hello hello 파란색 정보 아이콘 toohello 클릭 하면 자세히 hello 현재 선택 된 조건을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="5a00b-125">자세히 조건 식의 전체 목록을 hello에 대 한 참조 [규칙 엔진 조건식](cdn-rules-engine-reference-match-conditions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="5a00b-126">일치 조건 자세히의 전체 목록을 hello에 대 한 참조 [규칙 엔진의 일치 조건을](cdn-rules-engine-reference-match-conditions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5a00b-127">Hello 클릭  **+**  너무 단추 옆**기능** tooadd 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="5a00b-128">Hello 왼쪽에 hello 드롭다운에서 선택 **Force 내부 Max-age**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="5a00b-129">나타나는 hello 텍스트 상자에 입력 **300**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="5a00b-130">Hello 나머지 기본값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-130">Leave hello remaining default values.</span></span>
   
   ![CDN 기능](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="5a00b-132">으로 일치 조건으로 hello 파란색 정보 아이콘 toohello 클릭 하면 남아 hello의 새 기능에는이 기능에 대 한 세부 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="5a00b-133">경우 hello **Force 내부 Max-age**, hello 자산을 재정의 하는 것 **캐시 제어** 및 **Expires** 헤더 toocontrol hello CDN 가장자리 노드 hello 새로 됩니다 hello 원점에서 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="5a00b-134">300 초의 예제는 hello CDN 가장자리 노드는 hello 자산 hello 자산 원본을 새로 고치기 전에 5 분 동안 캐시를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="5a00b-135">기능을 자세히 설명의 전체 목록을 hello에 대 한 참조 [규칙 엔진 기능 정보](cdn-rules-engine-reference-features.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="5a00b-136">Hello 클릭 **추가** 단추 toosave hello에 대 한 새 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="5a00b-137">이제 hello 새 규칙에는 승인 대기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="5a00b-138">Hello 상태에서 변경 됩니다. 승인 되 면 **보류 중인 XML** 너무**활성 XML**합니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="5a00b-139">규칙 변경 내용을 hello CDN 통해 too90 분 toopropagate를 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a00b-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="5a00b-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5a00b-140">See also</span></span>
* [<span data-ttu-id="5a00b-141">Azure CDN 개요</span><span class="sxs-lookup"><span data-stu-id="5a00b-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="5a00b-142">규칙 엔진 참조</span><span class="sxs-lookup"><span data-stu-id="5a00b-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="5a00b-143">규칙 엔진 일치 조건</span><span class="sxs-lookup"><span data-stu-id="5a00b-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="5a00b-144">규칙 엔진 조건식</span><span class="sxs-lookup"><span data-stu-id="5a00b-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="5a00b-145">규칙 엔진 기능</span><span class="sxs-lookup"><span data-stu-id="5a00b-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="5a00b-146">Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="5a00b-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="5a00b-147">[Azure Fridays: Azure CDN의 강력하고 새로운 프리미엄 기능](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (동영상)</span><span class="sxs-lookup"><span data-stu-id="5a00b-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>