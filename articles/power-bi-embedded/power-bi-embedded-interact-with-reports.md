---
title: "hello JavaScript API를 사용 하 여 보고서와 aaaInteract | Microsoft Docs"
description: "Power BI 포함, hello JavaScript API를 사용 하 여 보고서와 상호 작용"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="a76bf-103">Hello JavaScript API를 사용 하 여 Power BI 보고서와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="a76bf-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="a76bf-104">hello Power BI JavaScript API를 사용 하면 tooeasily 응용 프로그램에 Power BI 보고서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="a76bf-105">API hello로 응용 프로그램 페이지 및 필터와 같은 다른 보고서 요소 프로그래밍 방식으로 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="a76bf-106">이러한 상호 작용은 Power BI 보고서가 응용 프로그램에 더욱 통합되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="a76bf-107">Hello 응용 프로그램의 일부로 호스팅되는 iframe을 사용 하 여 응용 프로그램에서 Power BI 보고서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="a76bf-108">hello iframe 한 경계 역할을 응용 프로그램 및 hello 보고서 간에 hello 다음 이미지에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Javascript API가 포함되지 않은 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="a76bf-110">hello JavaScript API hello 없이 보고서 및 응용 프로그램 없습니다 서로 상호 작용 낮지만 hello iframe 훨씬 쉽게 프로세스를 포함 하는 hello를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="a76bf-111">이 처럼 상호 작용의 hello 보고서는 실제로 hello 응용 프로그램의 일부와 같은 모습 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="a76bf-112">hello 보고서 및 응용 프로그램 hello 다음 이미지와 같이 실제로 toocommunicate 주고받는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Javascript API가 포함된 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="a76bf-114">Power BI JavaScript API hello toowrite 코드를 hello iframe 경계를 통해 안전 하 게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="a76bf-115">이 사용 하면 응용 프로그램 tooprogrammatically, 보고서 및 toolisten hello 보고서 내에서 사용자가 구성 하는 작업에서 이벤트에 대 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="a76bf-116">Power BI JavaScript API hello로 합니까?</span><span class="sxs-lookup"><span data-stu-id="a76bf-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="a76bf-117">Hello JavaScript API로 보고서를 관리, 보고서에서 toopages 탐색, 보고서를 필터링를 처리할 수 있습니다 이벤트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="a76bf-118">hello 다음 다이어그램에서는 hello API의 hello 구조</span><span class="sxs-lookup"><span data-stu-id="a76bf-118">hello following diagram shows hello structure of hello API.</span></span>

![Power BI JavaScript API 다이어그램](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="a76bf-120">보고서 관리</span><span class="sxs-lookup"><span data-stu-id="a76bf-120">Manage reports</span></span>
<span data-ttu-id="a76bf-121">hello Javascript API hello 보고서 및 페이지 수준에서 toomanage 동작을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="a76bf-122">응용 프로그램에서 특정 Power BI 보고서를 안전 하 게 포함-hello 테스트 [데모 응용 프로그램 포함](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="a76bf-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="a76bf-123">액세스 토큰 설정</span><span class="sxs-lookup"><span data-stu-id="a76bf-123">Set access token</span></span>
* <span data-ttu-id="a76bf-124">Hello 보고서 구성</span><span class="sxs-lookup"><span data-stu-id="a76bf-124">Configure hello report</span></span>
  * <span data-ttu-id="a76bf-125">사용 및 hello 필터 창 및 페이지 탐색 창 사용 안 함-hello 시도 [설정 데모 응용 프로그램 업데이트](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="a76bf-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="a76bf-126">페이지 및 필터에 대 한 기본값 설정-hello 테스트 [집합 기본값 데모](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="a76bf-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="a76bf-127">전체 화면 모드 시작 및 종료</span><span class="sxs-lookup"><span data-stu-id="a76bf-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="a76bf-128">포함 보고서에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a76bf-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="a76bf-129">보고서에서 toopages 이동</span><span class="sxs-lookup"><span data-stu-id="a76bf-129">Navigate toopages in a report</span></span>
<span data-ttu-id="a76bf-130">hello JavaScript API enbales 있습니다 toodiscover 모든 보고서 및 tooset hello 현재 페이지에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="a76bf-131">Hello 시도 [탐색 데모 응용 프로그램](http://azure-samples.github.io/powerbi-angular-client/#/scenario3)합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="a76bf-132">페이지 탐색에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a76bf-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="a76bf-133">보고서 필터링</span><span class="sxs-lookup"><span data-stu-id="a76bf-133">Filter a report</span></span>
<span data-ttu-id="a76bf-134">기본 및 고급 기능이 포함 된 보고서 및 보고서 페이지에 대 한 필터링 hello JavaScript API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="a76bf-135">Hello 시도 [데모 응용 프로그램을 필터링](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), 여기에 소개 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="a76bf-136">기본 필터</span><span class="sxs-lookup"><span data-stu-id="a76bf-136">Basic filters</span></span>
<span data-ttu-id="a76bf-137">기본 필터는 열 또는 계층 수준에 배치 되며 값 tooinclude 또는 제외 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="a76bf-138">고급 필터</span><span class="sxs-lookup"><span data-stu-id="a76bf-138">Advanced filters</span></span>
<span data-ttu-id="a76bf-139">Hello 논리 연산자를 사용 하 여 고급 필터 및 또는 OR, 자신의 연산자 및 값 반반씩 하나 또는 두 개의 조건을 적용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="a76bf-140">지원되는 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a76bf-140">Supported conditions are:</span></span>

* <span data-ttu-id="a76bf-141">없음</span><span class="sxs-lookup"><span data-stu-id="a76bf-141">None</span></span>
* <span data-ttu-id="a76bf-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="a76bf-142">LessThan</span></span>
* <span data-ttu-id="a76bf-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="a76bf-143">LessThanOrEqual</span></span>
* <span data-ttu-id="a76bf-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="a76bf-144">GreaterThan</span></span>
* <span data-ttu-id="a76bf-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="a76bf-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="a76bf-146">포함</span><span class="sxs-lookup"><span data-stu-id="a76bf-146">Contains</span></span>
* <span data-ttu-id="a76bf-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="a76bf-147">DoesNotContain</span></span>
* <span data-ttu-id="a76bf-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="a76bf-148">StartsWith</span></span>
* <span data-ttu-id="a76bf-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="a76bf-149">DoesNotStartWith</span></span>
* <span data-ttu-id="a76bf-150">Is</span><span class="sxs-lookup"><span data-stu-id="a76bf-150">Is</span></span>
* <span data-ttu-id="a76bf-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="a76bf-151">IsNot</span></span>
* <span data-ttu-id="a76bf-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="a76bf-152">IsBlank</span></span>
* <span data-ttu-id="a76bf-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="a76bf-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="a76bf-154">필터링에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a76bf-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="a76bf-155">이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="a76bf-155">Handling events</span></span>
<span data-ttu-id="a76bf-156">또한 hello iframe에 toosending 정보, 응용 프로그램도 정보를 받을 수 hello hello iframe에서 오는 이벤트 뒤에:</span><span class="sxs-lookup"><span data-stu-id="a76bf-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="a76bf-157">Embed</span><span class="sxs-lookup"><span data-stu-id="a76bf-157">Embed</span></span>
  * <span data-ttu-id="a76bf-158">loaded</span><span class="sxs-lookup"><span data-stu-id="a76bf-158">loaded</span></span>
  * <span data-ttu-id="a76bf-159">error</span><span class="sxs-lookup"><span data-stu-id="a76bf-159">error</span></span>
* <span data-ttu-id="a76bf-160">보고서</span><span class="sxs-lookup"><span data-stu-id="a76bf-160">Reports</span></span>
  * <span data-ttu-id="a76bf-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="a76bf-161">pageChanged</span></span>
  * <span data-ttu-id="a76bf-162">dataSelected(출시 예정)</span><span class="sxs-lookup"><span data-stu-id="a76bf-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="a76bf-163">이벤트를 처리하는 방법에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="a76bf-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="a76bf-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a76bf-164">Next steps</span></span>
<span data-ttu-id="a76bf-165">Hello Power BI JavaScript API에 대 한 자세한 내용은 다음 링크는 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a76bf-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="a76bf-166">JavaScript API Wiki</span><span class="sxs-lookup"><span data-stu-id="a76bf-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="a76bf-167">개체 모델 참조</span><span class="sxs-lookup"><span data-stu-id="a76bf-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="a76bf-168">샘플</span><span class="sxs-lookup"><span data-stu-id="a76bf-168">Samples</span></span>
  * [<span data-ttu-id="a76bf-169">Angular</span><span class="sxs-lookup"><span data-stu-id="a76bf-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="a76bf-170">Ember</span><span class="sxs-lookup"><span data-stu-id="a76bf-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="a76bf-171">라이브 데모</span><span class="sxs-lookup"><span data-stu-id="a76bf-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

