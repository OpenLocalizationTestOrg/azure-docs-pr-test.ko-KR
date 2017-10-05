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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="f788b-103">Azure 기계 학습 권장 사항 - JavaScript 통합</span><span class="sxs-lookup"><span data-stu-id="f788b-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="f788b-104">이 버전 대신 Recommendations API Cognitive 서비스를 사용하기 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="f788b-105">Recommendations Cognitive 서비스가 이 서비스를 대체하게 되며, 모든 새로운 기능이 여기에서 개발됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="f788b-106">일괄 처리 지원, 개선된 API 탐색기, 보다 깔끔한 API 노출 영역, 보다 일관적인 등록/청구 경험 등의 새로운 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="f788b-107">[새로운 Cognitive 서비스로 마이그레이션](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="f788b-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="f788b-108">이 문서에는 JavaScript를 사용하여 사이트를 통합하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="f788b-109">JavaScript를 통해 데이터 취득 이벤트를 전송하고, 권장 모델을 작성한 후 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="f788b-110">JS를 통해 수행하는 모든 작업은 서버 쪽에서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="f788b-111">1. 일반 개요</span><span class="sxs-lookup"><span data-stu-id="f788b-111">1. General Overview</span></span>
<span data-ttu-id="f788b-112">Azure ML 권장 사항과 사이트를 통합하는 과정은 다음 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="f788b-113">Azure ML 권장 사항으로 이벤트를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="f788b-114">그러면 권장 모델을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="f788b-115">권장 사항을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-115">Consume the recommendations.</span></span> <span data-ttu-id="f788b-116">모델이 작성되고 나면 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="f788b-117">이 문서에서는 모델을 작성하는 방법을 설명하지 않습니다. 방법에 대한 자세한 내용은 빠른 시작 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f788b-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="f788b-118"><ins>I단계</ins></span><span class="sxs-lookup"><span data-stu-id="f788b-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="f788b-119">첫 번째 단계에서는 페이지가 데이터 마켓을 통해 html 페이지에서 발생하는 이벤트를 Azure ML 권장 사항 서버로 전송할 수 있게 해주는 작은 JavaScript 라이브러리를 html 페이지에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="f788b-121"><ins>II단계</ins></span><span class="sxs-lookup"><span data-stu-id="f788b-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="f788b-122">권장 사항을 페이지에 표시하려는 두 번째 단계에서는 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="f788b-123">1. 서버(페이지 렌더링 단계)가 데이터 마켓을 통해 Azure ML 권장 사항 서버를 호출하여 권장 사항을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="f788b-124">결과는 항목 ID 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-124">The results include a list of items id.</span></span> <span data-ttu-id="f788b-125">서버는 항목 메타데이터(예: 이미지, 설명)로 결과를 보완하고 만든 페이지를 브라우저로 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="f788b-127">2. 다른 옵션은 1단계의 작은 JavaScript 파일을 사용하여 권장 항목의 단순 목록을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="f788b-128">여기서 받은 데이터는 첫 번째 옵션에서 받은 데이터보다 간결합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-128">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="f788b-130">2. 필수 조건</span><span class="sxs-lookup"><span data-stu-id="f788b-130">2. Prerequisites</span></span>
1. <span data-ttu-id="f788b-131">API를 사용하여 새 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-131">Create a new model using the APIs.</span></span> <span data-ttu-id="f788b-132">수행 방법에 대한 빠른 시작 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f788b-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="f788b-133">&lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;를 base64로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="f788b-134">이 코드는 JS 코드가 API를 호출할 수 있게 하는 기본 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="f788b-135">3. JavaScript를 사용하여 데이터 취득 이벤트 전송</span><span class="sxs-lookup"><span data-stu-id="f788b-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="f788b-136">다음 단계는 이벤트 전송에 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="f788b-137">JQuery 라이브러리를 코드에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-137">Include JQuery library in your code.</span></span> <span data-ttu-id="f788b-138">다음 URL의 nuget에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="f788b-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="f788b-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="f788b-140">다음 URL의 권장 사항 JavaScript 라이브러리를 포함합니다. http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="f788b-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="f788b-141">적절한 매개 변수를 사용하여 Azure ML 권장 사항 라이브러리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="f788b-142"><script>AzureMLRecommendationsStart (“<base64encoding of username:key>”, “<model_id>”); </script>
4. 적절한 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="f788b-143">이벤트의 모든 형식에 대해 아래 세부 섹션을 참조하세요(클릭 이벤트의 예) <script> if (typeof AzureMLRecommendationsEvent==“undefined”) {</span><span class="sxs-lookup"><span data-stu-id="f788b-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="f788b-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="f788b-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="f788b-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="f788b-145">3.1.</span></span>    <span data-ttu-id="f788b-146">제한 사항 및 브라우저 지원</span><span class="sxs-lookup"><span data-stu-id="f788b-146">Limitations and Browser Support</span></span>
<span data-ttu-id="f788b-147">참조 구현이며, 있는 그대로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="f788b-148">모든 주요 브라우저를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="f788b-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="f788b-149">3.2.</span></span>    <span data-ttu-id="f788b-150">이벤트 형식</span><span class="sxs-lookup"><span data-stu-id="f788b-150">Type of Events</span></span>
<span data-ttu-id="f788b-151">라이브러리에서 지원하는 5가지 이벤트 형식은 Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart 및 Purchase입니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="f788b-152">사용자 컨텍스트를 설정하는 데 사용되는 Login이라는 추가 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="f788b-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="f788b-153">3.2.1.</span></span> <span data-ttu-id="f788b-154">Click 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-154">Click Event</span></span>
<span data-ttu-id="f788b-155">이 이벤트는 사용자가 항목을 클릭할 때마다 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="f788b-156">일반적으로 사용자가 항목을 클릭하면 항목 세부 정보가 포함된 새 페이지가 열립니다. 이 페이지에서 이 이벤트가 트리거되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="f788b-157">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-157">Parameters:</span></span>

* <span data-ttu-id="f788b-158">event(문자열, 필수) - "click"</span><span class="sxs-lookup"><span data-stu-id="f788b-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="f788b-159">item(문자열, 필수) - 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="f788b-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="f788b-160">itemName(문자열, 선택) - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="f788b-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="f788b-161">itemDescription(문자열, 선택) - 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="f788b-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="f788b-162">itemCategory(문자열, 선택) - 항목의 범주</span><span class="sxs-lookup"><span data-stu-id="f788b-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="f788b-163">또는 선택적 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="f788b-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="f788b-164">3.2.2.</span></span> <span data-ttu-id="f788b-165">Recommendation Click 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-165">Recommendation Click Event</span></span>
<span data-ttu-id="f788b-166">이 이벤트는 사용자가 Azure ML 권장 사항에서 권장 항목으로 받은 항목을 클릭할 때마다 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="f788b-167">일반적으로 사용자가 항목을 클릭하면 항목 세부 정보가 포함된 새 페이지가 열립니다. 이 페이지에서 이 이벤트가 트리거되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="f788b-168">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-168">Parameters:</span></span>

* <span data-ttu-id="f788b-169">event(문자열, 필수) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="f788b-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="f788b-170">item(문자열, 필수) - 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="f788b-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="f788b-171">itemName(문자열, 선택) - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="f788b-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="f788b-172">itemDescription(문자열, 선택) - 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="f788b-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="f788b-173">itemCategory(문자열, 선택) - 항목의 범주</span><span class="sxs-lookup"><span data-stu-id="f788b-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="f788b-174">seeds(문자열 배열, 선택) - 권장 사항 쿼리를 생성한 시드</span><span class="sxs-lookup"><span data-stu-id="f788b-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="f788b-175">recoList(문자열 배열, 선택) - 클릭한 항목을 생성한 권장 사항 요청의 결과</span><span class="sxs-lookup"><span data-stu-id="f788b-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="f788b-176">또는 선택적 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="f788b-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="f788b-177">3.2.3.</span></span> <span data-ttu-id="f788b-178">Add Shopping Cart 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="f788b-179">이 이벤트는 사용자가 장바구니에 항목을 추가할 때 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="f788b-180">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-180">Parameters:</span></span>

* <span data-ttu-id="f788b-181">event(문자열, 필수) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="f788b-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="f788b-182">item(문자열, 필수) - 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="f788b-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="f788b-183">itemName(문자열, 선택) - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="f788b-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="f788b-184">itemDescription(문자열, 선택) - 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="f788b-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="f788b-185">itemCategory(문자열, 선택) - 항목의 범주</span><span class="sxs-lookup"><span data-stu-id="f788b-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="f788b-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="f788b-186">3.2.4.</span></span> <span data-ttu-id="f788b-187">Remove Shopping Cart 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="f788b-188">이 이벤트는 사용자가 장바구니에서 항목을 제거할 때 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="f788b-189">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-189">Parameters:</span></span>

* <span data-ttu-id="f788b-190">event(문자열, 필수) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="f788b-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="f788b-191">item(문자열, 필수) - 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="f788b-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="f788b-192">itemName(문자열, 선택) - 항목의 이름</span><span class="sxs-lookup"><span data-stu-id="f788b-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="f788b-193">itemDescription(문자열, 선택) - 항목에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="f788b-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="f788b-194">itemCategory(문자열, 선택) - 항목의 범주</span><span class="sxs-lookup"><span data-stu-id="f788b-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="f788b-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="f788b-195">3.2.5.</span></span> <span data-ttu-id="f788b-196">Purchase 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-196">Purchase Event</span></span>
<span data-ttu-id="f788b-197">이 이벤트는 사용자가 장바구니를 구매했을 때 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="f788b-198">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-198">Parameters:</span></span>

* <span data-ttu-id="f788b-199">event(문자열) – "purchase"</span><span class="sxs-lookup"><span data-stu-id="f788b-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="f788b-200">items(Purchased) – 구매한 각 항목에 대한 항목이 저장되는 배열</span><span class="sxs-lookup"><span data-stu-id="f788b-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="f788b-201">Purchased 형식:</span><span class="sxs-lookup"><span data-stu-id="f788b-201">Purchased format:</span></span>
  * <span data-ttu-id="f788b-202">item(문자열) - 항목의 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="f788b-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="f788b-203">count(정수 또는 문자열) – 구매한 항목 수</span><span class="sxs-lookup"><span data-stu-id="f788b-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="f788b-204">price(부동 소수점 수 또는 문자열) – 선택적 필드 - 항목의 가격</span><span class="sxs-lookup"><span data-stu-id="f788b-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="f788b-205">아래 예제에서는 3개 항목(33, 34, 35)의 구매를 보여 줍니다. 두 항목은 모든 필드가 채워져 있고(항목, 개수, 가격), 한 항목(항목 34)은 가격이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="f788b-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="f788b-206">3.2.6.</span></span> <span data-ttu-id="f788b-207">User Login 이벤트</span><span class="sxs-lookup"><span data-stu-id="f788b-207">User Login Event</span></span>
<span data-ttu-id="f788b-208">Azure ML 권장 사항 이벤트 라이브러리는 동일한 브라우저에서 제공된 이벤트를 식별하기 위해 쿠키를 만들고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="f788b-209">모델 결과를 개선하기 위해 Azure ML 권장 사항에서 쿠키 사용을 재정의하는 사용자 고유 ID를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="f788b-210">이 이벤트는 사용자가 사이트에 로그인한 후에 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="f788b-211">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-211">Parameters:</span></span>

* <span data-ttu-id="f788b-212">event(문자열) – "userlogin"</span><span class="sxs-lookup"><span data-stu-id="f788b-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="f788b-213">user(문자열) – 사용자의 공유 ID.</span><span class="sxs-lookup"><span data-stu-id="f788b-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="f788b-214">4. JavaScript 통해 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="f788b-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="f788b-215">권장 사항을 사용하는 코드는 클라이언트 웹 페이지의 일부 JavaScript 이벤트에 의해 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="f788b-216">권장 사항 응답에는 권장 항목 ID, 이름 및 해당 등급이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="f788b-217">권장 항목의 목록 표시에만 이 옵션을 사용하는 것이 좋습니다. 더 복잡한 처리(예: 항목의 메타데이터 추가)는 서버 쪽 통합에서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="f788b-218">4.1 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="f788b-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="f788b-219">권장 사항을 사용하려면 필요한 JavaScript 라이브러리를 페이지에 포함하고 AzureMLRecommendationsStart를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="f788b-220">섹션 2를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f788b-220">See section 2.</span></span>

<span data-ttu-id="f788b-221">하나 이상의 항목에 대해 권장 사항을 사용하려면 AzureMLRecommendationsGetI2IRecommendation이라는 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="f788b-222">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f788b-222">Parameters:</span></span>

* <span data-ttu-id="f788b-223">items(문자열 배열) - 권장 사항을 가져올 하나 이상의 항목.</span><span class="sxs-lookup"><span data-stu-id="f788b-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="f788b-224">Fbt 빌드를 사용하는 경우 하나의 항목만 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="f788b-225">numberOfResults(int) – 필요한 결과 수</span><span class="sxs-lookup"><span data-stu-id="f788b-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="f788b-226">includeMetadata(부울, 선택) - ‘true’로 설정된 경우 결과에서 메타데이터 필드를 채워야 함을 나타냄</span><span class="sxs-lookup"><span data-stu-id="f788b-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="f788b-227">처리 함수 - 반환된 권장 사항을 처리할 함수.</span><span class="sxs-lookup"><span data-stu-id="f788b-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="f788b-228">반환되는 데이터의 배열:</span><span class="sxs-lookup"><span data-stu-id="f788b-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="f788b-229">Item - 항목의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="f788b-229">Item - item unique id</span></span>
  * <span data-ttu-id="f788b-230">name – 항목 이름(카탈로그에 있는 경우)</span><span class="sxs-lookup"><span data-stu-id="f788b-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="f788b-231">rating - 권장 사항 등급</span><span class="sxs-lookup"><span data-stu-id="f788b-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="f788b-232">metadata - 항목의 메타데이터를 나타내는 문자열</span><span class="sxs-lookup"><span data-stu-id="f788b-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="f788b-233">예제: 다음 코드는 "64f6eb0d-947a-4c18-a16c-888da9e228ba" 항목에 대한 8개 권장 사항을 요청하고(includeMetadata를 지정하지 않아 메타데이터가 필요 없음을 암시적으로 나타냄) 그 결과를 버퍼에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f788b-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

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
