---
title: "Machine Learning 권장 사항: JavaScript 통합 | Microsoft Docs"
description: "Azure Machine Learning 권장 사항 - JavaScript 통합 - 설명서"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="7e6c1-103">Azure 기계 학습 권장 사항 - JavaScript 통합</span><span class="sxs-lookup"><span data-stu-id="7e6c1-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="7e6c1-104">이 버전 대신 hello 권장 API Cognitive 서비스를 사용 하 여 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="7e6c1-105">hello 권장 Cognitive 서비스를 입력 해야 하므로이 서비스 및 hello 새로운 기능을 모두 있는 개발 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="7e6c1-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="7e6c1-107">에 대 한 자세한 내용은 [toohello 마이그레이션 새 Cognitive 서비스](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="7e6c1-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="7e6c1-108">이 문서를 보여 주는 방법을 toointegrate JavaScript를 사용 하 여 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="7e6c1-109">hello JavaScript를 사용 하면 toosend 데이터 취득 이벤트 및 tooconsume 권장 사항 추천 모델을 작성 한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="7e6c1-110">JS를 통해 수행하는 모든 작업은 서버 쪽에서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="7e6c1-111">1. 일반 개요</span><span class="sxs-lookup"><span data-stu-id="7e6c1-111">1. General Overview</span></span>
<span data-ttu-id="7e6c1-112">Azure ML 권장 사항과 사이트를 통합하는 과정은 다음 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="7e6c1-113">Azure ML 권장 사항으로 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="7e6c1-114">이렇게 하면 toobuild 추천 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="7e6c1-115">Hello 권장 사항을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-115">Consume hello recommendations.</span></span> <span data-ttu-id="7e6c1-116">Hello 모델의 빌드 후 hello 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="7e6c1-117">(이 문서의 설명 하지 않습니다 방법을 toobuild 모델을 읽을 hello 퀵 스타트 가이드 tooget 방법은).</span><span class="sxs-lookup"><span data-stu-id="7e6c1-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="7e6c1-118"><ins>I단계</ins></span><span class="sxs-lookup"><span data-stu-id="7e6c1-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="7e6c1-119">Hello 수 있도록 하는 작은 JavaScript 라이브러리를 html 페이지에 삽입 하는 첫 번째 단계 (데이터 마켓)를 통해 Azure ML 권장 사항을 서버에 hello html 페이지에 나타나는 순서 대로 페이지 toosend 이벤트를 hello:</span><span class="sxs-lookup"><span data-stu-id="7e6c1-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="7e6c1-121"><ins>II단계</ins></span><span class="sxs-lookup"><span data-stu-id="7e6c1-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="7e6c1-122">Hello에 hello 페이지 tooshow hello 권장 구성 하려는 경우 두 번째 단계 중 하나를 선택 hello 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="7e6c1-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="7e6c1-123">1. (페이지 렌더링의 hello 단계)의 서버 (데이터 마켓)를 통해 Azure ML 권장 사항을 서버 tooget 권장 사항을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="7e6c1-124">hello 결과 항목 id 목록이 포함 됩니다. 서버는 hello 항목 메타 데이터 (예: 이미지, 설명)를 사용 하 여 tooenrich hello 결과 되어야 하며 보낼 hello toohello 브라우저 페이지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="7e6c1-126">2. hello 다른 옵션은 toouse hello 작은 JavaScript 파일 단계 하나의 tooget 추천된 항목의 단순 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="7e6c1-127">여기에 수신 hello 데이터는 hello 첫 번째 옵션에 hello 하나 보다 보다 간결 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="7e6c1-129">2. 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7e6c1-129">2. Prerequisites</span></span>
1. <span data-ttu-id="7e6c1-130">Hello Api를 사용 하 여 새 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="7e6c1-131">방법에 hello 빠른 시작 가이드를 참조 하십시오. toodo 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="7e6c1-132">&lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;를 base64로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="7e6c1-133">(이 사용 hello 기본 인증 tooenable hello JS 코드 toocall hello Api에 대 한).</span><span class="sxs-lookup"><span data-stu-id="7e6c1-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="7e6c1-134">3. JavaScript를 사용하여 데이터 취득 이벤트 전송</span><span class="sxs-lookup"><span data-stu-id="7e6c1-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="7e6c1-135">이벤트 전송을 원활 하는 단계를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="7e6c1-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="7e6c1-136">JQuery 라이브러리를 코드에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-136">Include JQuery library in your code.</span></span> <span data-ttu-id="7e6c1-137">Hello url에 nuget에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="7e6c1-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="7e6c1-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="7e6c1-139">Hello url에서 hello 권장 사항을 자바 스크립트 라이브러리를 포함: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="7e6c1-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="7e6c1-140">Hello 적절 한 매개 변수를 사용 하 여 Azure ML 권장 라이브러리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="7e6c1-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. 송신 hello에 대 한 적절 한 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="7e6c1-142">이벤트의 모든 형식에 대해 아래 세부 섹션을 참조하세요(클릭 이벤트의 예) <script> if (typeof AzureMLRecommendationsEvent==“undefined”) {</span><span class="sxs-lookup"><span data-stu-id="7e6c1-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="7e6c1-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="7e6c1-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="7e6c1-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-144">3.1.</span></span>    <span data-ttu-id="7e6c1-145">제한 사항 및 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="7e6c1-145">Limitations and Browser Support</span></span>
<span data-ttu-id="7e6c1-146">참조 구현이며, 있는 그대로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="7e6c1-147">모든 주요 브라우저를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="7e6c1-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-148">3.2.</span></span>    <span data-ttu-id="7e6c1-149">이벤트 형식</span><span class="sxs-lookup"><span data-stu-id="7e6c1-149">Type of Events</span></span>
<span data-ttu-id="7e6c1-150">형식은 5 개 이벤트 라이브러리 지원 hello: 쇼핑 카트 및 구매에서 클릭, 권장 사항을 클릭 제거 tooShop 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="7e6c1-151">컨텍스트가 사용 되는 tooset hello 사용자 로그인을 호출 하는 추가 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="7e6c1-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-152">3.2.1.</span></span> <span data-ttu-id="7e6c1-153">Click 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-153">Click Event</span></span>
<span data-ttu-id="7e6c1-154">이 이벤트는 사용자가 항목을 클릭할 때마다 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="7e6c1-155">Hello 항목 세부 정보;로 새 페이지를 연 사용자가 항목을 클릭할 때 일반적으로 이 페이지에이 이벤트가 트리거되어 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7e6c1-156">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-156">Parameters:</span></span>

* <span data-ttu-id="7e6c1-157">event(문자열, 필수) - "click"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="7e6c1-158">항목 (문자열, 필수)-hello 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="7e6c1-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7e6c1-159">항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="7e6c1-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7e6c1-160">itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명</span><span class="sxs-lookup"><span data-stu-id="7e6c1-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7e6c1-161">itemCategory (문자열, 선택 사항)-hello hello 항목 범주</span><span class="sxs-lookup"><span data-stu-id="7e6c1-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="7e6c1-162">또는 선택적 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="7e6c1-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-163">3.2.2.</span></span> <span data-ttu-id="7e6c1-164">Recommendation Click 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-164">Recommendation Click Event</span></span>
<span data-ttu-id="7e6c1-165">이 이벤트는 사용자가 Azure ML 권장 사항에서 권장 항목으로 받은 항목을 클릭할 때마다 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="7e6c1-166">Hello 항목 세부 정보;로 새 페이지를 연 사용자가 항목을 클릭할 때 일반적으로 이 페이지에이 이벤트가 트리거되어 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7e6c1-167">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-167">Parameters:</span></span>

* <span data-ttu-id="7e6c1-168">event(문자열, 필수) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="7e6c1-169">항목 (문자열, 필수)-hello 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="7e6c1-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7e6c1-170">항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="7e6c1-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7e6c1-171">itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명</span><span class="sxs-lookup"><span data-stu-id="7e6c1-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7e6c1-172">itemCategory (문자열, 선택 사항)-hello hello 항목 범주</span><span class="sxs-lookup"><span data-stu-id="7e6c1-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="7e6c1-173">초기값 (문자열 배열, 선택 사항)-hello 초기값 hello 권장 사항 쿼리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="7e6c1-174">(문자열 배열, 선택 사항)-recoList hello hello 클릭 된 항목을 생성 하는 hello 권장 요청의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="7e6c1-175">또는 선택적 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="7e6c1-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-176">3.2.3.</span></span> <span data-ttu-id="7e6c1-177">Add Shopping Cart 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="7e6c1-178">이 이벤트를 사용 해야 hello 사용자 쇼핑 카트는 항목 toohello를 추가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="7e6c1-179">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-179">Parameters:</span></span>

* <span data-ttu-id="7e6c1-180">event(문자열, 필수) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="7e6c1-181">항목 (문자열, 필수)-hello 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="7e6c1-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7e6c1-182">항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="7e6c1-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7e6c1-183">itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명</span><span class="sxs-lookup"><span data-stu-id="7e6c1-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7e6c1-184">itemCategory (문자열, 선택 사항)-hello hello 항목 범주</span><span class="sxs-lookup"><span data-stu-id="7e6c1-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="7e6c1-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-185">3.2.4.</span></span> <span data-ttu-id="7e6c1-186">Remove Shopping Cart 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="7e6c1-187">Hello 사용자 toohello 쇼핑 카트에 항목을 제거 하는 경우이 이벤트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="7e6c1-188">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-188">Parameters:</span></span>

* <span data-ttu-id="7e6c1-189">event(문자열, 필수) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="7e6c1-190">항목 (문자열, 필수)-hello 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="7e6c1-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7e6c1-191">항목 이름 (문자열, 선택 사항)-hello 항목의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="7e6c1-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7e6c1-192">itemDescription (문자열, 선택 사항)-hello 항목에 대 한 hello 설명</span><span class="sxs-lookup"><span data-stu-id="7e6c1-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7e6c1-193">itemCategory (문자열, 선택 사항)-hello hello 항목 범주</span><span class="sxs-lookup"><span data-stu-id="7e6c1-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="7e6c1-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-194">3.2.5.</span></span> <span data-ttu-id="7e6c1-195">Purchase 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-195">Purchase Event</span></span>
<span data-ttu-id="7e6c1-196">Hello 사용자의 쇼핑 카트를 구매할 때이 이벤트를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="7e6c1-197">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-197">Parameters:</span></span>

* <span data-ttu-id="7e6c1-198">event(문자열) – "purchase"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="7e6c1-199">items(Purchased) – 구매한 각 항목에 대한 항목이 저장되는 배열</span><span class="sxs-lookup"><span data-stu-id="7e6c1-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="7e6c1-200">Purchased 형식:</span><span class="sxs-lookup"><span data-stu-id="7e6c1-200">Purchased format:</span></span>
  * <span data-ttu-id="7e6c1-201">항목 (string)-hello 항목의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="7e6c1-202">count(정수 또는 문자열) – 구매한 항목 수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="7e6c1-203">가격 (float 또는 문자열)-선택적 필드-hello 가격 hello 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="7e6c1-204">3 구매 되는 hello 코드 항목 (33, 34, 35) 2 대와 모든 필드가 채워집니다 (항목, count, 가격)과 (항목 34) 없는 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="7e6c1-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-205">3.2.6.</span></span> <span data-ttu-id="7e6c1-206">User Login 이벤트</span><span class="sxs-lookup"><span data-stu-id="7e6c1-206">User Login Event</span></span>
<span data-ttu-id="7e6c1-207">Azure ML 권장 사항을 이벤트 라이브러리를 만듭니다 및에서 제공 된 순서 tooidentify 이벤트에서 쿠키를 사용 하 여 같은 브라우저를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="7e6c1-208">순서 tooimprove hello 모델의 결과 Azure ML 권장 사항을 tooset을 hello 쿠키 사용을 재정의 하는 사용자 고유 id를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="7e6c1-209">Hello 사용자 로그인 tooyour 사이트 후이 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="7e6c1-210">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-210">Parameters:</span></span>

* <span data-ttu-id="7e6c1-211">event(문자열) – "userlogin"</span><span class="sxs-lookup"><span data-stu-id="7e6c1-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="7e6c1-212">사용자 (string)-hello 사용자의 고유 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="7e6c1-213">4. JavaScript 통해 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="7e6c1-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="7e6c1-214">hello 추천을 사용 하는 hello 코드 hello 클라이언트의 웹 페이지에서 일부 JavaScript 이벤트에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="7e6c1-215">hello 권장 응답에는 권장 항목 Id, 이름 및 해당 등급 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="7e6c1-216">것이 가장 좋은 toouse hello 서버 쪽 통합에서 hello 추천 항목 보다 복잡 한 처리 (예: hello 항목의 메타 데이터 추가)의 목록 표시 하는 데에이 옵션을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="7e6c1-217">4.1 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="7e6c1-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="7e6c1-218">tooconsume 권장 사항을 tooinclude hello 필요 페이지 및 toocall AzureMLRecommendationsStart JavaScript 라이브러리를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="7e6c1-219">섹션 2를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-219">See section 2.</span></span>

<span data-ttu-id="7e6c1-220">메서드를 호출 하는 toocall 필요 하나 이상의 항목에 대 한 권장 사항을 tooconsume: AzureMLRecommendationsGetI2IRecommendation 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="7e6c1-221">매개 변수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-221">Parameters:</span></span>

* <span data-ttu-id="7e6c1-222">(문자열의 배열)-에 대 한 하나 이상의 항목 tooget 권장 항목합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="7e6c1-223">Fbt 빌드를 사용하는 경우 하나의 항목만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="7e6c1-224">numberOfResults(int) – 필요한 결과 수</span><span class="sxs-lookup"><span data-stu-id="7e6c1-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="7e6c1-225">(부울, 선택 사항)-includeMetadata 경우 too'true 설정 ' hello 결과에 해당 hello 메타 데이터 필드를 채워야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="7e6c1-226">처리 기능-hello 권장 사항을 처리 하는 함수 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="7e6c1-227">hello 데이터의 배열로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="7e6c1-228">Item - 항목의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="7e6c1-228">Item - item unique id</span></span>
  * <span data-ttu-id="7e6c1-229">name – 항목 이름(카탈로그에 있는 경우)</span><span class="sxs-lookup"><span data-stu-id="7e6c1-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="7e6c1-230">rating - 권장 사항 등급</span><span class="sxs-lookup"><span data-stu-id="7e6c1-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="7e6c1-231">메타 데이터-hello 항목의 hello 메타 데이터를 나타내는 문자열</span><span class="sxs-lookup"><span data-stu-id="7e6c1-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="7e6c1-232">예: 코드 다음 hello 요청 "64f6eb0d-947a-4c18-a16c-888da9e228ba" 항목에 대 한 8 권장 사항 (및 지정 하 여 includeMetadata-암시적으로 표시 메타 데이터가 필요 하다), 다음 버퍼에 hello 결과 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7e6c1-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
