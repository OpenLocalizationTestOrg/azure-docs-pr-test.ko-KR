---
title: "Azure 검색의 aaaHow tooimplement 패싯 탐색 | Microsoft Docs"
description: "Azure 검색에서는 Microsoft Azure에서 호스팅되는 클라우드 검색 서비스와 통합 되는 패싯 탐색 tooapplications를 추가 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a><span data-ttu-id="51ba5-103">어떻게 Azure 검색의 tooimplement 패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="51ba5-103">How tooimplement faceted navigation in Azure Search</span></span>
<span data-ttu-id="51ba5-104">패싯 탐색은 검색 응용 프로그램에서 자기 주도형 드릴다운 탐색을 제공하는 필터링 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span></span> <span data-ttu-id="51ba5-105">hello 용어 '패싯 탐색' 친숙 하 고 있지만 아마도 사용 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="51ba5-105">hello term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span></span> <span data-ttu-id="51ba5-106">다음 예제와 hello, 패싯 탐색은 hello 4 가지 범주가 사용 toofilter 결과 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-106">As hello following example shows, faceted navigation is nothing more than hello categories used toofilter results.</span></span>

 ![Azure Search 작업 포털 데모][1]

<span data-ttu-id="51ba5-108">패싯 탐색은 대체 항목 지점 toosearch입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-108">Faceted navigation is an alternative entry point toosearch.</span></span> <span data-ttu-id="51ba5-109">제공 편리한 대체 tootyping 복잡 한 검색 식 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-109">It offers a convenient alternative tootyping complex search expressions by hand.</span></span> <span data-ttu-id="51ba5-110">패싯을 사용하면 원하는 항목을 쉽게 찾을 수 있으며 항상 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span></span> <span data-ttu-id="51ba5-111">개발자는 패싯 검색 모음을 탐색 하기 위한 가장 유용한 검색 조건을 hello를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-111">As a developer, facets let you expose hello most useful search criteria for navigating your search corpus.</span></span> <span data-ttu-id="51ba5-112">온라인 소매 응용 프로그램에서는 종종 브랜드, 부서(어린이 신발), 크기, 가격, 인기도 및 등급에 대한 패싯 탐색이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span></span> 

<span data-ttu-id="51ba5-113">패싯 탐색의 구현은 검색 기술에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-113">Implementing faceted navigation differs across search technologies.</span></span> <span data-ttu-id="51ba5-114">Azure Search에서는 이전에 스키마에서 특성을 지정한 필드를 사용하여 쿼리 시 패싯 탐색이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span></span>

-   <span data-ttu-id="51ba5-115">응용 프로그램 빌드, 쿼리를 보내야 하는 hello 쿼리에서 *패싯 쿼리 매개 변수* tooget hello 사용할 수 있는 패싯 필터 값 해당 문서에 대 한 결과 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-115">In hello queries that your application builds, a query must send *facet query parameters* tooget hello available facet filter values for that document result set.</span></span>

-   <span data-ttu-id="51ba5-116">tooactually 자르기 hello 문서 결과 집합, hello 응용 프로그램에도 적용 해야는 `$filter` 식입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-116">tooactually trim hello document result set, hello application must also apply a `$filter` expression.</span></span>

<span data-ttu-id="51ba5-117">응용 프로그램 개발에서 쿼리를 생성 하는 코드 작성 hello 대량의 hello 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-117">In your application development, writing code that constructs queries constitutes hello bulk of hello work.</span></span> <span data-ttu-id="51ba5-118">대부분 패싯 탐색에서 예상 하는 hello 응용 프로그램 동작의 범위를 정의 하 고 패싯 결과 대 한 개수를 가져오는 대 한 기본 제공 지원을 비롯 하 여 hello 서비스에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-118">Many of hello application behaviors that you would expect from faceted navigation are provided by hello service, including built-in support for defining ranges and getting counts for facet results.</span></span> <span data-ttu-id="51ba5-119">hello 서비스도 수행할 수 있는 실제 기본값 다루기 탐색 구조를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-119">hello service also includes sensible defaults that help you avoid unwieldy navigation structures.</span></span> 

## <a name="sample-code-and-demo"></a><span data-ttu-id="51ba5-120">샘플 코드 및 데모</span><span class="sxs-lookup"><span data-stu-id="51ba5-120">Sample code and demo</span></span>
<span data-ttu-id="51ba5-121">이 문서에서는 구직 검색 포털을 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-121">This article uses a job search portal as an example.</span></span> <span data-ttu-id="51ba5-122">hello 예제는 ASP.NET MVC 응용 프로그램으로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-122">hello example is implemented as an ASP.NET MVC application.</span></span>

-   <span data-ttu-id="51ba5-123">참조 및 hello 작업 데모 온라인에서 테스트 [Azure 검색 작업 포털 데모](http://azjobsdemo.azurewebsites.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-123">See and test hello working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="51ba5-124">Hello에서 hello 코드 다운로드 [GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-124">Download hello code from hello [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

## <a name="get-started"></a><span data-ttu-id="51ba5-125">시작</span><span class="sxs-lookup"><span data-stu-id="51ba5-125">Get started</span></span>
<span data-ttu-id="51ba5-126">을 사용 하는 새로운 toosearch 개발 hello 가장 좋은 방법은 toothink 패싯 탐색의 경우 자체 방향이 지정 된 검색에 대 한 hello 가능성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-126">If you're new toosearch development, hello best way toothink of faceted navigation is that it shows hello possibilities for self-directed search.</span></span> <span data-ttu-id="51ba5-127">패싯 탐색은 포인트 클릭 동작을 통해 검색 결과의 범위를 신속하게 좁히는 데 사용되는 미리 정의된 필터를 기반으로 하는 드릴다운 검색 환경에 일종입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span></span> 

### <a name="interaction-model"></a><span data-ttu-id="51ba5-128">상호 작용 모델</span><span class="sxs-lookup"><span data-stu-id="51ba5-128">Interaction model</span></span>

<span data-ttu-id="51ba5-129">hello 검색 패싯 탐색의 경우 반복적으로 하겠습니다를 일련의 쿼리 응답 toouser 작업에 펼치려면를 이해 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-129">hello search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response toouser actions.</span></span>

<span data-ttu-id="51ba5-130">hello 시작 지점에는 일반적으로 hello 주변에 배치 하는 패싯 탐색을 제공 하는 응용 프로그램 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-130">hello starting point is an application page that provides faceted navigation, typically placed on hello periphery.</span></span> <span data-ttu-id="51ba5-131">패싯 탐색은 각 값에 대한 확인란 또는 클릭할 수 있는 텍스트가 포함된 트리 구조인 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span></span> 

1. <span data-ttu-id="51ba5-132">전송 tooAzure 검색 쿼리는 하나 이상의 패싯 쿼리 매개 변수를 통해 hello 패싯 탐색 구조를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-132">A query sent tooAzure Search specifies hello faceted navigation structure via one or more facet query parameters.</span></span> <span data-ttu-id="51ba5-133">예를 들어 hello 쿼리 포함 될 수 있습니다 `facet=Rating`, 등을 사용는 `:values` 또는 `:sort` 옵션 toofurther hello 프레젠테이션 구체화 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-133">For instance, hello query might include `facet=Rating`, perhaps with a `:values` or `:sort` option toofurther refine hello presentation.</span></span>
2. <span data-ttu-id="51ba5-134">hello 프레젠테이션 계층 hello 요청에 지정 된 hello 패싯을 사용 하 여 패싯 탐색을 제공 하는 검색 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-134">hello presentation layer renders a search page that provides faceted navigation, using hello facets specified on hello request.</span></span>
3. <span data-ttu-id="51ba5-135">등급이 4 이상이 인 제품만 표시 해야 하는 "4" tooindicate 클릭 등급을 포함 하는 패싯 탐색 구조를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-135">Given a faceted navigation structure that includes Rating, you click "4" tooindicate that only products with a rating of 4 or higher should be shown.</span></span> 
4. <span data-ttu-id="51ba5-136">응답으로 hello 응용 프로그램 포함 하는 쿼리를 보냅니다.`$filter=Rating ge 4`</span><span class="sxs-lookup"><span data-stu-id="51ba5-136">In response, hello application sends a query that includes `$filter=Rating ge 4`</span></span> 
5. <span data-ttu-id="51ba5-137">hello 프레젠테이션 계층 업데이트 hello 페이지 hello 새 조건을 충족 하는 해당 항목을 포함 하는 축소 된 결과 집합을 보여 주는 (이 경우 제품 등급 4 이상).</span><span class="sxs-lookup"><span data-stu-id="51ba5-137">hello presentation layer updates hello page, showing a reduced result set, containing just those items that satisfy hello new criteria (in this case, products rated 4 and up).</span></span>

<span data-ttu-id="51ba5-138">패싯은 쿼리 매개 변수이지만 쿼리 입력과 혼동해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-138">A facet is a query parameter, but do not confuse it with query input.</span></span> <span data-ttu-id="51ba5-139">쿼리의 선택 조건으로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-139">It is never used as selection criteria in a query.</span></span> <span data-ttu-id="51ba5-140">대신, 이라고 패싯 쿼리 매개 변수 다시 hello 응답에 제공 된 입력 toohello 탐색 구조.</span><span class="sxs-lookup"><span data-stu-id="51ba5-140">Instead, think of facet query parameters as inputs toohello navigation structure that comes back in hello response.</span></span> <span data-ttu-id="51ba5-141">각 패싯 쿼리 매개 변수에 제공한 Azure 검색 문서는 각 패싯 값에 대 한 hello 부분 결과에 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in hello partial results for each facet value.</span></span>

<span data-ttu-id="51ba5-142">공지 hello `$filter` 4 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-142">Notice hello `$filter` in step 4.</span></span> <span data-ttu-id="51ba5-143">hello 필터는 패싯 탐색의 중요 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-143">hello filter is an important aspect of faceted navigation.</span></span> <span data-ttu-id="51ba5-144">패싯 및 필터는 hello API에서에서 관련이, 하려는 두 toodeliver hello 경험을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-144">Although facets and filters are independent in hello API, you need both toodeliver hello experience you intend.</span></span> 

### <a name="app-design-pattern"></a><span data-ttu-id="51ba5-145">앱 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="51ba5-145">App design pattern</span></span>

<span data-ttu-id="51ba5-146">응용 프로그램 코드에서 hello 방법은 toouse 패싯 쿼리 매개 변수 tooreturn hello 패싯 탐색 구조와 함께 패싯 결과 $filter 식입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-146">In application code, hello pattern is toouse facet query parameters tooreturn hello faceted navigation structure along with facet results, plus a $filter expression.</span></span>  <span data-ttu-id="51ba5-147">hello 필터 식 핸들 hello는 hello 패싯 값에는 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-147">hello filter expression handles hello click event on hello facet value.</span></span> <span data-ttu-id="51ba5-148">Hello 간주할 `$filter` hello 코드 숨김 hello 실제 트리밍으로 검색 결과의 식 toohello 프레젠테이션 계층을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-148">Think of hello `$filter` expression as hello code behind hello actual trimming of search results returned toohello presentation layer.</span></span> <span data-ttu-id="51ba5-149">색 패싯을 매개 변수로 받아을 통해 구현 됩니다 빨간색 hello 색을 클릭 하는 `$filter` 선택 항목에는 빨간색의 색만 식입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-149">Given a Colors facet, clicking hello color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span></span> 

### <a name="query-basics"></a><span data-ttu-id="51ba5-150">쿼리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="51ba5-150">Query basics</span></span>

<span data-ttu-id="51ba5-151">Azure 검색에서는 하나 이상의 쿼리 매개 변수를 통해 요청이 지정됩니다(각 매개 변수에 대한 설명은 [문서 검색](http://msdn.microsoft.com/library/azure/dn798927.aspx) 참조).</span><span class="sxs-lookup"><span data-stu-id="51ba5-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span></span> <span data-ttu-id="51ba5-152">Hello 쿼리 매개 변수 모두가 필요 하지만 쿼리 toobe 유효 하려면에서 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-152">None of hello query parameters are required, but you must have at least one in order for a query toobe valid.</span></span>

<span data-ttu-id="51ba5-153">전체 자릿수, 이해 하는 hello 관련이 없는 적중 아웃 toofilter 기능을 통해 얻습니다 이러한 식 중 하나 이상이:</span><span class="sxs-lookup"><span data-stu-id="51ba5-153">Precision, understood as hello ability toofilter out irrelevant hits, is achieved through one or both of these expressions:</span></span>

-   <span data-ttu-id="51ba5-154">**search=**</span><span class="sxs-lookup"><span data-stu-id="51ba5-154">**search=**</span></span>  
    <span data-ttu-id="51ba5-155">이 매개 변수 값 hello hello 검색 식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-155">hello value of this parameter constitutes hello search expression.</span></span> <span data-ttu-id="51ba5-156">단일 텍스트 조각 또는 여러 항 및 연산자를 포함하는 복잡한 검색 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span></span> <span data-ttu-id="51ba5-157">Hello 서버에서 검색 식 결과에 반환 용어 일치에 대 한 hello 인덱스의 검색 가능 필드를 쿼리 하는 전체 텍스트 검색에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-157">On hello server, a search expression is used for full-text search, querying searchable fields in hello index for matching terms, returning results in rank order.</span></span> <span data-ttu-id="51ba5-158">설정한 경우 `search` hello 전체 인덱스 toonull, 쿼리 실행 됩니다 (즉, `search=*`).</span><span class="sxs-lookup"><span data-stu-id="51ba5-158">If you set `search` toonull, query execution is over hello entire index (that is, `search=*`).</span></span> <span data-ttu-id="51ba5-159">Hello의 다른 요소와 같은 쿼리 되는,이 `$filter` hello 반환 되는 문서에 영향을 주는 주요 요소는 점수 매기기 프로필, 또는 `($filter`) 어떤 순서로 (`scoringProfile` 또는 `$orderby`).</span><span class="sxs-lookup"><span data-stu-id="51ba5-159">In this case, other elements of hello query, such as a `$filter` or scoring profile, are hello primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span></span>

-   <span data-ttu-id="51ba5-160">**$filter=**</span><span class="sxs-lookup"><span data-stu-id="51ba5-160">**$filter=**</span></span>  
    <span data-ttu-id="51ba5-161">필터는 특정 문서 특성의 hello 값을 기반으로 하는 검색 결과의 hello 크기 제한에 대 한 강력한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-161">A filter is a powerful mechanism for limiting hello size of search results based on hello values of specific document attributes.</span></span> <span data-ttu-id="51ba5-162">A `$filter` 를 먼저 평가 hello 사용 가능한 값과 각 값에 대 한 해당 수를 생성 하는 패싯 논리 이어서</span><span class="sxs-lookup"><span data-stu-id="51ba5-162">A `$filter` is evaluated first, followed by faceting logic that generates hello available values and corresponding counts for each value</span></span>

<span data-ttu-id="51ba5-163">복잡 한 검색 식에는 hello 쿼리의 hello 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-163">Complex search expressions decrease hello performance of hello query.</span></span> <span data-ttu-id="51ba5-164">가능한 경우 제대로 생성 된 필터 식을 tooincrease 정밀도 사용 및 쿼리 성능을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-164">Where possible, use well-constructed filter expressions tooincrease precision and improve query performance.</span></span>

<span data-ttu-id="51ba5-165">toobetter 보다 정밀 하 게 필터를 추가 하는 방법을 이해, 필터 식을 포함 하는 복잡 한 검색 식 tooone 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-165">toobetter understand how a filter adds more precision, compare a complex search expression tooone that includes a filter expression:</span></span>

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

<span data-ttu-id="51ba5-166">두 쿼리는 유효 하지만 hello 둘째 더 우수 비-적합 하지 않습니다 시애틀에 주차 된 찾고 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="51ba5-166">Both queries are valid, but hello second is superior if you’re looking for non-motels with parking in Seattle.</span></span>
-   <span data-ttu-id="51ba5-167">hello 첫 번째 쿼리는 이름, 설명 및 검색 가능한 데이터가 포함 된 다른 모든 필드와 같은 문자열 필드에 언급 되지 않은 되거나 언급 되 해당 특정 단어에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-167">hello first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span></span>
-   <span data-ttu-id="51ba5-168">hello 두 번째 쿼리는 구조화 된 데이터에서 일치 하는 정확한 찾은 가능성이 toobe 더욱 정확 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-168">hello second query looks for precise matches on structured data and is likely toobe much more accurate.</span></span>

<span data-ttu-id="51ba5-169">패싯 탐색이 포함된 응용 프로그램에서는 패싯 탐색 구조에 대한 각 사용자 작업이 수행된 후 검색 결과 범위를 좁혀야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span></span> <span data-ttu-id="51ba5-170">toonarrow 결과 필터 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-170">toonarrow results, use a filter expression.</span></span>

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a><span data-ttu-id="51ba5-171">패싯 탐색 앱 구축</span><span class="sxs-lookup"><span data-stu-id="51ba5-171">Build a faceted navigation app</span></span>
<span data-ttu-id="51ba5-172">Hello 검색 요청을 작성 하는 응용 프로그램 코드에서 Azure 검색을 사용 하 여 패싯 탐색을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-172">You implement faceted navigation with Azure Search in your application code that builds hello search request.</span></span> <span data-ttu-id="51ba5-173">이전에 정의 된 스키마의 요소를 의존 하는 hello 패싯 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-173">hello faceted navigation relies on elements in your schema that you defined previously.</span></span>

<span data-ttu-id="51ba5-174">검색 인덱스에 미리 정의 된 hello `Facetable [true|false]` 특성을 인덱싱하거나 tooenable 선택한 필드에 설정, 패싯 탐색 구조에서 사용 되는 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-174">Predefined in your search index is hello `Facetable [true|false]` index attribute, set on selected fields tooenable or disable their use in a faceted navigation structure.</span></span> <span data-ttu-id="51ba5-175">`"Facetable" = true`가 아니면 패싯 탐색에서 필드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span></span>

<span data-ttu-id="51ba5-176">코드에서 프레젠테이션 계층 hello hello 사용자 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-176">hello presentation layer in your code provides hello user experience.</span></span> <span data-ttu-id="51ba5-177">상자 hello hello 패싯 탐색 hello 레이블, 값, 확인란, hello count 등의 구성 요소를 나열 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-177">It should list hello constituent parts of hello faceted navigation, such as hello label, values, check boxes, and hello count.</span></span> <span data-ttu-id="51ba5-178">hello Azure 검색 REST API는 플랫폼과 별 관계가, 모든 언어 및 플랫폼을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-178">hello Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span></span> <span data-ttu-id="51ba5-179">hello 중요 한 점은 tooinclude UI 요소를 지 원하는 증분 새로 고침, 업데이트 된 UI 상태와 각 추가 패싯을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-179">hello important thing is tooinclude UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span></span> 

<span data-ttu-id="51ba5-180">쿼리 시간에 응용 프로그램 코드를 포함 하는 요청 만듭니다 `facet=[string]`, hello 필드 toofacet에서 제공 하는 요청 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides hello field toofacet by.</span></span> <span data-ttu-id="51ba5-181">`&facet=color&facet=category&facet=rating`과 같이 각 패싯을 앰퍼샌드(&) 문자로 구분하여 여러 패싯을 쿼리에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span></span>

<span data-ttu-id="51ba5-182">응용 프로그램 코드 구성도 해야는 `$filter` 식 toohandle hello 패싯 탐색 창에서 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-182">Application code must also construct a `$filter` expression toohandle hello click events in faceted navigation.</span></span> <span data-ttu-id="51ba5-183">A `$filter` hello 검색 결과 hello 패싯 값을 사용 하 여 필터 조건으로 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-183">A `$filter` reduces hello search results, using hello facet value as filter criteria.</span></span>

<span data-ttu-id="51ba5-184">Azure 검색 업데이트 toohello 패싯 탐색 구조와 함께 입력 하는 하나 이상의 조건에 따른 hello 검색 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-184">Azure Search returns hello search results, based on one or more terms that you enter, along with updates toohello faceted navigation structure.</span></span> <span data-ttu-id="51ba5-185">Azure 검색에서 패싯 탐색은 패싯 값과 각 값에 대해 발견된 결과 수로 이루어진 단일 수준 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span></span>

<span data-ttu-id="51ba5-186">Hello 다음 섹션, 방법 자세히 보기 걸릴 toobuild 각 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-186">In hello following sections, we take a closer look at how toobuild each part.</span></span>

<a name="buildindex"></a>

## <a name="build-hello-index"></a><span data-ttu-id="51ba5-187">Hello 인덱스를 작성</span><span class="sxs-lookup"><span data-stu-id="51ba5-187">Build hello index</span></span>
<span data-ttu-id="51ba5-188">이 인덱스 특성을 통해 hello 인덱스에서 필드 별로으로 패싯 사용 됨: `"Facetable": true`합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-188">Faceting is enabled on a field-by-field basis in hello index, via this index attribute: `"Facetable": true`.</span></span>  
<span data-ttu-id="51ba5-189">패싯 탐색에 사용할 수 있는 모든 필드 형식은 기본적으로 `Facetable` 입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span></span> <span data-ttu-id="51ba5-190">이러한 필드 형식에는 `Edm.String`, `Edm.DateTimeOffset`, 모든 hello 숫자 필드 형식 및 (기본적으로, 모든 필드 유형에 제외 하 고 facetable `Edm.GeographyPoint`, 패싯 탐색에 사용할 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="51ba5-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all hello numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span></span> 

<span data-ttu-id="51ba5-191">인덱스를 작성할 때 패싯 탐색에 대 한 가장 좋은 방법은 꺼져 tooexplicitly turn 패싯 패싯으로 사용 하면 안 되는 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-191">When building an index, a best practice for faceted navigation is tooexplicitly turn faceting off for fields that should never be used as a facet.</span></span>  <span data-ttu-id="51ba5-192">특히, ID 또는 제품 이름, 같은 단일 항목 값에 대 한 문자열 필드 설정할지 너무`"Facetable": false` tooprevent 패싯 탐색에 사용 하 여 자신의 실수로 (및 비효율적인).</span><span class="sxs-lookup"><span data-stu-id="51ba5-192">In particular, string fields for singleton values, such as an ID or product name, should be set too`"Facetable": false` tooprevent their accidental (and ineffective) use in faceted navigation.</span></span> <span data-ttu-id="51ba5-193">패싯 접속이 필요 없는 해제 하면 hello 인덱스의 hello 크기를 작게 유지 하는 데 도움이 되 고 일반적으로 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-193">Turning faceting off where you don’t need it helps keep hello size of hello index small, and typically improves performance.</span></span>

<span data-ttu-id="51ba5-194">다음은 몇 가지 특성 tooreduce hello 크기로 잘린 hello 작업 포털 데모 샘플 앱에 대 한 hello 스키마의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-194">Following is part of hello schema for hello Job Portal Demo sample app, trimmed of some attributes tooreduce hello size:</span></span>

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

<span data-ttu-id="51ba5-195">Hello 샘플 스키마에서 볼 수 있듯이 `Facetable` ID 값과 같은 패싯으로 사용 하면 안 되는 문자열 필드에 꺼져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-195">As you can see in hello sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span></span> <span data-ttu-id="51ba5-196">패싯 접속이 필요 없는 해제 하면 hello 인덱스의 hello 크기를 작게 유지 하는 데 도움이 되 고 일반적으로 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-196">Turning faceting off where you don’t need it helps keep hello size of hello index small, and typically improves performance.</span></span>

> [!TIP]
> <span data-ttu-id="51ba5-197">모범 사례로, 각 필드에 대 한 인덱스 특성의 hello 전체 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-197">As a best practice, include hello full set of index attributes for each field.</span></span> <span data-ttu-id="51ba5-198">하지만 `Facetable` 각 특성 얻을 수 있습니다 각 스키마 의사 결정의 hello 의미를 통해 의도적으로 설정 하는 거의 모든 필드에는 기본적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through hello implications of each schema decision.</span></span> 

<a name="checkdata"></a>

## <a name="check-hello-data"></a><span data-ttu-id="51ba5-199">Hello 데이터 검사</span><span class="sxs-lookup"><span data-stu-id="51ba5-199">Check hello data</span></span>
<span data-ttu-id="51ba5-200">데이터의 품질 hello 하 되는 대로 hello 패싯 탐색 구조를 구체화 여부에 직접적인 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-200">hello quality of your data has a direct effect on whether hello faceted navigation structure materializes as you expect it to.</span></span> <span data-ttu-id="51ba5-201">Hello 쉽게를 생성할 수 있다는 필터 tooreduce hello 결과 집합에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-201">It also affects hello ease of constructing filters tooreduce hello result set.</span></span>

<span data-ttu-id="51ba5-202">각 문서에 대 한 값을 포함 해야 toofacet 브랜드 또는 가격을 하려는 경우 *BrandName* 및 *ProductPrice* 유효 하 고 생산성 필터 옵션을 일관 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-202">If you want toofacet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span></span>

<span data-ttu-id="51ba5-203">에 대 한 어떤 tooscrub의 몇 가지 미리 알림은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-203">Here are a few reminders of what tooscrub for:</span></span>

* <span data-ttu-id="51ba5-204">Toofacet 하 여 원하는 모든 필드에 대 한 자문해 값 자체 방향이 지정 된 검색의 필터와 적합 한을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-204">For every field that you want toofacet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span></span> <span data-ttu-id="51ba5-205">hello 값 짧고 설명적 충분히 고유한 toooffer 경쟁 옵션 중 하나를 지우기 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-205">hello values should be short, descriptive, and sufficiently distinctive toooffer a clear choice between competing options.</span></span>
* <span data-ttu-id="51ba5-206">맞춤법 오류 또는 거의 일치하는 값.</span><span class="sxs-lookup"><span data-stu-id="51ba5-206">Misspellings or nearly matching values.</span></span> <span data-ttu-id="51ba5-207">경우 hello 색 필드에 따라 패싯 모두를 선택 하는, 색 및 필드 값에서 패싯을 포함 주황색 및 Ornage (맞춤법 오류).</span><span class="sxs-lookup"><span data-stu-id="51ba5-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on hello Color field would pick up both.</span></span>
* <span data-ttu-id="51ba5-208">대/소문자가 혼합된 텍스트도 패싯 탐색에서 나타날 수 있습니다. 예를 들어 orange와 Orange가 두 가지 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span></span> 
* <span data-ttu-id="51ba5-209">단일 및 복수 버전의 hello 동일한 값 각각에 대해 별도 패싯에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-209">Single and plural versions of hello same value can result in a separate facet for each.</span></span>

<span data-ttu-id="51ba5-210">상상할 수 있듯이 성실 hello 데이터 준비는 효과적인 패싯 탐색의 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-210">As you can imagine, diligence in preparing hello data is an essential aspect of effective faceted navigation.</span></span>

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a><span data-ttu-id="51ba5-211">Hello UI 빌드</span><span class="sxs-lookup"><span data-stu-id="51ba5-211">Build hello UI</span></span>
<span data-ttu-id="51ba5-212">Hello 프레젠테이션 계층에서 다시 작업할 수 그렇지 않은 경우 누락 될 수 있습니다 하 고 어떤 기능에 필수적인 toohello을 이해 하는 요구 사항을 클릭 하면 도움말 검색 환경을 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-212">Working back from hello presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential toohello search experience.</span></span>

<span data-ttu-id="51ba5-213">패싯 탐색 측면에서 웹 또는 응용 프로그램 페이지 hello 패싯 탐색 구조를 표시, hello 페이지에서 사용자 입력을 검색 및 변경 하는 hello 요소를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-213">In terms of faceted navigation, your web or application page displays hello faceted navigation structure, detects user input on hello page, and inserts hello changed elements.</span></span> 

<span data-ttu-id="51ba5-214">AJAX 웹 응용 프로그램에서는 일반적으로 증분 변경 내용을 toorefresh 수 있기 때문에 hello 프레젠테이션 계층에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-214">For web applications, AJAX is commonly used in hello presentation layer because it allows you toorefresh incremental changes.</span></span> <span data-ttu-id="51ba5-215">ASP.NET MVC 또는 HTTP를 통해 tooan Azure 검색 서비스에 연결할 수 있는 다른 시각화 플랫폼을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-215">You could also use ASP.NET MVC or any other visualization platform that can connect tooan Azure Search service over HTTP.</span></span> <span data-ttu-id="51ba5-216">hello 샘플 응용 프로그램에서 참조 된이 문서 hello **Azure 검색 작업 포털 데모** – toobe ASP.NET MVC 응용 프로그램에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-216">hello sample application referenced throughout this article -- hello **Azure Search Job Portal Demo** – happens toobe an ASP.NET MVC application.</span></span>

<span data-ttu-id="51ba5-217">Hello 샘플에서 패싯 탐색 hello 검색 결과 페이지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-217">In hello sample, faceted navigation is built into hello search results page.</span></span> <span data-ttu-id="51ba5-218">다음 예제에서는 hello에서 가져온 hello `index.cshtml` 패싯 탐색 hello 검색에 표시 하기 위한 표시 hello 정적 HTML 구조 hello 샘플 응용 프로그램의 파일 결과 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-218">hello following example, taken from hello `index.cshtml` file of hello sample application, shows hello static HTML structure for displaying faceted navigation on hello search results page.</span></span> <span data-ttu-id="51ba5-219">패싯 목록이 hello 작성 하거나 검색 용어를 제출 또는 선택 하거나 패싯의 선택을 취소 하면 동적으로 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-219">hello list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span></span>

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

<span data-ttu-id="51ba5-220">다음 코드 조각에서 hello hello `index.cshtml` 페이지 hello HTML toodisplay hello 첫 번째 패싯, 직함을 동적으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-220">hello following code snippet from hello `index.cshtml` page dynamically builds hello HTML toodisplay hello first facet, Business Title.</span></span> <span data-ttu-id="51ba5-221">유사한 기능을 동적으로 hello에 대 한 HTML hello 패싯 지정할 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-221">Similar functions dynamically build hello HTML for hello other facets.</span></span> <span data-ttu-id="51ba5-222">각 패싯 레이블과 hello 해당 패싯 결과 대 한 항목 수를 표시 하는 개수에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-222">Each facet has a label and a count, which displays hello number of items found for that facet result.</span></span>

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> <span data-ttu-id="51ba5-223">Hello 검색 결과 페이지를 디자인할 때 tooadd 패싯을 지우기 위한 메커니즘을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-223">When you design hello search results page, remember tooadd a mechanism for clearing facets.</span></span> <span data-ttu-id="51ba5-224">확인란을 추가 하는 경우 tooclear hello 필터링 하는 방법을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-224">If you add check boxes, you can easily see how tooclear hello filters.</span></span> <span data-ttu-id="51ba5-225">다른 레이아웃에는 이동 경로 탐색 패턴 또는 다른 창의적인 방법이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span></span> <span data-ttu-id="51ba5-226">예를 들어 hello 작업 검색 포털 샘플 응용 프로그램에서에서 클릭할 수 있는 hello `[X]` 선택한 패싯 tooclear hello 패싯 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-226">For example, in hello Job Search Portal sample application, you can click hello `[X]` after a selected facet tooclear hello facet.</span></span>

<a name="buildquery"></a>

## <a name="build-hello-query"></a><span data-ttu-id="51ba5-227">Hello 쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="51ba5-227">Build hello query</span></span>
<span data-ttu-id="51ba5-228">쿼리 작성을 위한 작성 하는 hello 코드 tooformulate 요청을 사용 하는 모든 부분의 검색 식, 패싯, 필터, 점수 매기기 프로필 – 모든 항목을 포함 하 여 올바른 쿼리를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-228">hello code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used tooformulate a request.</span></span> <span data-ttu-id="51ba5-229">이 섹션에서는 패싯 필요한 경우 쿼리 및 패싯 toodeliver와 필터는 사용 하는 방법에 축소 된 탐색 결과 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-229">In this section, we explore where facets fit into a query, and how filters are used with facets toodeliver a reduced result set.</span></span>

<span data-ttu-id="51ba5-230">패싯은 이 샘플 응용 프로그램의 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-230">Notice that facets are integral in this sample application.</span></span> <span data-ttu-id="51ba5-231">hello 포털 데모 작업에서에서 hello 검색 환경 패싯 탐색 및 필터 기반으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-231">hello search experience in hello Job Portal Demo is designed around faceted navigation and filters.</span></span> <span data-ttu-id="51ba5-232">패싯 탐색 hello 페이지의 hello 두드러진 배치의 중요성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-232">hello prominent placement of faceted navigation on hello page demonstrates its importance.</span></span> 

<span data-ttu-id="51ba5-233">예로 것이 좋습니다 toobegin 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-233">An example is often a good place toobegin.</span></span> <span data-ttu-id="51ba5-234">다음 예제에서는 hello에서 가져온 hello `JobsSearch.cs` 파일을 빌드 비즈니스 제목, 위치, 게시 유형 및 최소 급여에 따라 만드는 패싯 탐색 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-234">hello following example, taken from hello `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span></span> 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

<span data-ttu-id="51ba5-235">패싯 쿼리 매개 변수가 설정 되어 tooa 필드 고 hello 데이터 형식에 따라 추가로 매개 변수화 할 수를 포함 하는 쉼표로 구분 된 목록으로 `count:<integer>`, `sort:<>`, `interval:<integer>`, 및 `values:<list>`합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-235">A facet query parameter is set tooa field and depending on hello data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span></span> <span data-ttu-id="51ba5-236">값 목록은 범위를 설정할 때 숫자 데이터에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-236">A values list is supported for numeric data when setting up ranges.</span></span> <span data-ttu-id="51ba5-237">자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ba5-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span></span>

<span data-ttu-id="51ba5-238">응용 프로그램에 의해 공식화 hello 요청, 면 함께 필터 toonarrow hello 문서 집합을 후보 패싯 값 선택 항목을 아래로 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-238">Along with facets, hello request formulated by your application should also build filters toonarrow down hello set of candidate documents based on a facet value selection.</span></span> <span data-ttu-id="51ba5-239">패싯 탐색 자전거 저장소에 대 한 단서 tooquestions와 같은 제공 *사용할 수 있는 어떤 색, 제조업체 및 자전거 유형의?*합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-239">For a bike store, faceted navigation provides clues tooquestions like *What colors, manufacturers, and types of bikes are available?*.</span></span> <span data-ttu-id="51ba5-240">필터링은 *이 가격대의 빨간색 산악용 자전거는 무엇입니까?*와 같은 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span></span> <span data-ttu-id="51ba5-241">만 빨간색 제품 표시할지, "Red" tooindicate를 클릭할 때 hello 다음 쿼리 hello 응용 프로그램이 포함 되어 보낼 `$filter=Color eq ‘Red’`합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-241">When you click "Red" tooindicate that only Red products should be shown, hello next query hello application sends includes `$filter=Color eq ‘Red’`.</span></span>

<span data-ttu-id="51ba5-242">다음 코드 조각에서 hello hello `JobsSearch.cs` 페이지 hello 비즈니스 제목 패싯의 값을 선택할 경우 선택한 hello 비즈니스 제목 toohello 필터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-242">hello following code snippet from hello `JobsSearch.cs` page adds hello selected Business Title toohello filter if you select a value from hello Business Title facet.</span></span>

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a><span data-ttu-id="51ba5-243">팁 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="51ba5-243">Tips and best practices</span></span>

### <a name="indexing-tips"></a><span data-ttu-id="51ba5-244">인덱싱 팁</span><span class="sxs-lookup"><span data-stu-id="51ba5-244">Indexing tips</span></span>
<span data-ttu-id="51ba5-245">**검색 상자를 사용하지 않을 경우 인덱스 효율성 향상**</span><span class="sxs-lookup"><span data-stu-id="51ba5-245">**Improve index efficiency if you don't use a Search box**</span></span>

<span data-ttu-id="51ba5-246">응용 프로그램 패싯 탐색에 독점적으로 사용 하는 경우 (즉, 없음 검색 상자)로 hello 필드를 표시할 수 있습니다 `searchable=false`, `facetable=true` tooproduce 인덱스를 더욱 간결 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark hello field as `searchable=false`, `facetable=true` tooproduce a more compact index.</span></span> <span data-ttu-id="51ba5-247">또한 인덱싱 전체 패싯 값이 없는 단어 잘림 또는 다중 단어 값의 hello 구성 요소 부분의 인덱싱에 대해서만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of hello component parts of a multi-word value.</span></span>

<span data-ttu-id="51ba5-248">**패싯으로 사용할 수 있는 필드 지정**</span><span class="sxs-lookup"><span data-stu-id="51ba5-248">**Specify which fields can be used as facets**</span></span>

<span data-ttu-id="51ba5-249">해당 hello 회수 hello 인덱스의 스키마는 패싯으로 사용할 수 있는 toouse 있는 필드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-249">Recall that hello schema of hello index determines which fields are available toouse as a facet.</span></span> <span data-ttu-id="51ba5-250">Hello 쿼리 필드 facetable로 가정 하 고 여는 필드 toofacet를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-250">Assuming a field is facetable, hello query specifies which fields toofacet by.</span></span> <span data-ttu-id="51ba5-251">패싯이 hello 필드 hello 레이블 아래에 표시 되는 hello 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-251">hello field by which you are faceting provides hello values that appear below hello label.</span></span> 

<span data-ttu-id="51ba5-252">각 레이블에 아래에 표시 되는 hello 값 hello 인덱스에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-252">hello values that appear under each label are retrieved from hello index.</span></span> <span data-ttu-id="51ba5-253">예를 들어 hello 패싯 필드는 *색*, hello 추가 필터링에 사용할 수 있는 값이 됩니다 hello-해당 필드에 대 한 빨간색, 검정, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-253">For example, if hello facet field is *Color*, hello values available for additional filtering are hello values for that field - Red, Black, and so forth.</span></span>

<span data-ttu-id="51ba5-254">숫자 및 날짜/시간 값에만, 명시적으로 값을 설정할 수 hello 패싯 필드 (예를 들어 `facet=Rating,values:1|2|3|4|5`).</span><span class="sxs-lookup"><span data-stu-id="51ba5-254">For Numeric and DateTime values only, you can explicitly set values on hello facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span></span> <span data-ttu-id="51ba5-255">이러한 필드 형식 toosimplify hello 분리 패싯 결과의 연속 범위 (숫자 값 이나 전체 기간에 따라 범위 중 하나)에 값 목록을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-255">A values list is allowed for these field types toosimplify hello separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span></span> 

<span data-ttu-id="51ba5-256">**기본적으로 한 수준의 패싯 탐색만 유지 가능**</span><span class="sxs-lookup"><span data-stu-id="51ba5-256">**By default you can only have one level of faceted navigation**</span></span> 

<span data-ttu-id="51ba5-257">계층 구조에서 패싯 중첩은 직접 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-257">As noted, there is no direct support for nesting facets in a hierarchy.</span></span> <span data-ttu-id="51ba5-258">기본적으로 Azure Search의 패싯 탐색은 하나의 필터 수준만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-258">By default, faceted navigation in Azure Search only supports one level of filters.</span></span> <span data-ttu-id="51ba5-259">그러나 해결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-259">However, workarounds do exist.</span></span> <span data-ttu-id="51ba5-260">`Collection(Edm.String)` 의 계층적 패싯 구조를 계층당 하나의 항목으로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span></span> <span data-ttu-id="51ba5-261">이 해결 방법을 구현 하는 것은이 문서의 hello 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-261">Implementing this workaround is beyond hello scope of this article.</span></span> 

### <a name="querying-tips"></a><span data-ttu-id="51ba5-262">쿼리 팁</span><span class="sxs-lookup"><span data-stu-id="51ba5-262">Querying tips</span></span>
<span data-ttu-id="51ba5-263">**필드의 유효성 검사**</span><span class="sxs-lookup"><span data-stu-id="51ba5-263">**Validate fields**</span></span>

<span data-ttu-id="51ba5-264">신뢰할 수 없는 사용자 입력에 따라 동적으로 패싯의 hello 목록을 작성 하는 경우 hello hello 패싯 필드 이름이 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-264">If you build hello list of facets dynamically based on untrusted user input, validate that hello names of hello faceted fields are valid.</span></span> <span data-ttu-id="51ba5-265">또는 중 하나를 사용 하 여 Url 작성 시 hello 이름을 이스케이프 `Uri.EscapeDataString()` .NET 또는 선택한 플랫폼에서 동일한 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-265">Or, escape hello names when building URLs by using either `Uri.EscapeDataString()` in .NET, or hello equivalent in your platform of choice.</span></span>

### <a name="filtering-tips"></a><span data-ttu-id="51ba5-266">필터링 팁</span><span class="sxs-lookup"><span data-stu-id="51ba5-266">Filtering tips</span></span>
<span data-ttu-id="51ba5-267">**필터로 검색 정확도 향상**</span><span class="sxs-lookup"><span data-stu-id="51ba5-267">**Increase search precision with filters**</span></span>

<span data-ttu-id="51ba5-268">필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-268">Use filters.</span></span> <span data-ttu-id="51ba5-269">에 의존 하는 경우 검색 식만 단독으로 형태소 분석 문서 toobe 공격자는 hello 정확한 패싯 값이 해당 필드 중 하나에 없는 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-269">If you rely on just search expressions alone, stemming could cause a document toobe returned that doesn’t have hello precise facet value in any of its fields.</span></span>

<span data-ttu-id="51ba5-270">**필터로 검색 성능 향상**</span><span class="sxs-lookup"><span data-stu-id="51ba5-270">**Increase search performance with filters**</span></span>

<span data-ttu-id="51ba5-271">필터는 hello 문서 집합을 후보 검색에 대 한 범위를 좁힐 하 고 순위에서 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-271">Filters narrow down hello set of candidate documents for search and exclude them from ranking.</span></span> <span data-ttu-id="51ba5-272">대량의 문서 집합이 있는 경우 엄선된 패싯 드릴다운을 사용하면 때로는 성능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span></span>
  
<span data-ttu-id="51ba5-273">**패싯 필드에 hello만 필터링**</span><span class="sxs-lookup"><span data-stu-id="51ba5-273">**Filter only hello faceted fields**</span></span>

<span data-ttu-id="51ba5-274">패싯 드릴 다운에 일반적으로 원하는 tooonly 모든 검색 가능한 필드에서 아무 곳 이나 하지 hello 패싯 값이 특정 (패싯) 필드에 포함 된 문서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-274">In faceted drill-down, you typically want tooonly include documents that have hello facet value in a specific (faceted) field, not anywhere across all searchable fields.</span></span> <span data-ttu-id="51ba5-275">필터를 추가 하 여 일치 하는 값에 대 한 hello 패싯 필드에만 서비스 toosearch hello hello 대상 필드에 도움이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-275">Adding a filter reinforces hello target field by directing hello service toosearch only in hello faceted field for a matching value.</span></span>

<span data-ttu-id="51ba5-276">**추가 필터로 패싯 결과 자르기**</span><span class="sxs-lookup"><span data-stu-id="51ba5-276">**Trim facet results with more filters**</span></span>

<span data-ttu-id="51ba5-277">패싯 결과 패싯 용어와 일치 하는 hello 검색 결과는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-277">Facet results are documents found in hello search results that match a facet term.</span></span> <span data-ttu-id="51ba5-278">다음 예제에 대 한 검색 결과에서 hello에 *클라우드 컴퓨팅*, 254 항목 있습니다 *내부 사양* 콘텐츠 형식으로.</span><span class="sxs-lookup"><span data-stu-id="51ba5-278">In hello following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span></span> <span data-ttu-id="51ba5-279">항목은 상호 배타적이지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-279">Items are not necessarily mutually exclusive.</span></span> <span data-ttu-id="51ba5-280">항목 필터 둘 모두의 hello 조건에 부합 하는 경우에 각각에서 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-280">If an item meets hello criteria of both filters, it is counted in each one.</span></span> <span data-ttu-id="51ba5-281">이러한 중복이 가능에 패싯 `Collection(Edm.String)` 필드는 종종 tooimplement 문서 태그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used tooimplement document tagging.</span></span>

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

<span data-ttu-id="51ba5-282">일반적으로 패싯 결과는 너무 큰 일관 되 게, 더 추가 하는 것이 좋습니다 찾을 필터링 toogive 사용자 hello 검색을 축소 하는 옵션이 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters toogive users more options for narrowing hello search.</span></span>

### <a name="tips-about-result-count"></a><span data-ttu-id="51ba5-283">결과 개수에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="51ba5-283">Tips about result count</span></span>

<span data-ttu-id="51ba5-284">**Hello 패싯 탐색 창에서 항목 hello 수 제한**</span><span class="sxs-lookup"><span data-stu-id="51ba5-284">**Limit hello number of items in hello facet navigation**</span></span>

<span data-ttu-id="51ba5-285">Hello 탐색 트리의 각 패싯 필드에 대 한 기본 제한이 10 개의 값을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-285">For each faceted field in hello navigation tree, there is a default limit of 10 values.</span></span> <span data-ttu-id="51ba5-286">이 기본 탐색 구조에 대 한 때문에 합리적 hello 값 목록 tooa 관리 하기 쉬운 크기로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-286">This default makes sense for navigation structures because it keeps hello values list tooa manageable size.</span></span> <span data-ttu-id="51ba5-287">값 toocount 할당 하 여 hello 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-287">You can override hello default by assigning a value toocount.</span></span>

* <span data-ttu-id="51ba5-288">`&facet=city,count:5`패싯 결과적으로 hello 처음 5 개 도시만 hello 최상위 결과 반환 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-288">`&facet=city,count:5` specifies that only hello first five cities found in hello top ranked results are returned as a facet result.</span></span> <span data-ttu-id="51ba5-289">검색 용어가 "공항"이고 일치 항목이 32개인 샘플 쿼리를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="51ba5-289">Consider a sample query with a search term of “airport” and 32 matches.</span></span> <span data-ttu-id="51ba5-290">Hello 쿼리를 지정 하는 경우 `&facet=city,count:5`hello 검색 결과에서 대부분의 문서에 포함 된 hello로 처음 다섯 개의 고유한 도시의 hello hello 패싯 결과 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-290">If hello query specifies `&facet=city,count:5`, only hello first five unique cities with hello most documents in hello search results are included in hello facet results.</span></span>

<span data-ttu-id="51ba5-291">공지 hello 패싯 결과 구별 검색 결과.</span><span class="sxs-lookup"><span data-stu-id="51ba5-291">Notice hello distinction between facet results and search results.</span></span> <span data-ttu-id="51ba5-292">검색 결과 hello 쿼리와 일치 하는 모든 hello 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-292">Search results are all hello documents that match hello query.</span></span> <span data-ttu-id="51ba5-293">패싯 결과 각 패싯 값에 일치 하는 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-293">Facet results are hello matches for each facet value.</span></span> <span data-ttu-id="51ba5-294">Hello 예제 검색 결과는 hello 패싯 분류 목록 (예에서 5)에 없는 도시 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-294">In hello example, search results include City names that are not in hello facet classification list (5 in our example).</span></span> <span data-ttu-id="51ba5-295">패싯 탐색을 통해 필터링된 결과는 사용자가 패싯을 지우거나 City 이외의 다른 패싯을 선택한 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span></span> 

> [!NOTE]
> <span data-ttu-id="51ba5-296">두 가지 이상의 형식이 있을 때 `count`를 설명하면 혼동을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-296">Discussing `count` when there is more than one type can be confusing.</span></span> <span data-ttu-id="51ba5-297">hello 다음 표에서 제공 Azure 검색 API, 예제 코드 및 설명서 hello 용어 사용 방법에 대 한 간단한 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-297">hello following table offers a brief summary of how hello term is used in Azure Search API, sample code, and documentation.</span></span> 

* `@colorFacet.count`<br/>
  <span data-ttu-id="51ba5-298">프레젠테이션 코드 hello 패싯을 사용 하는 toodisplay hello 수가 패싯 결과에서 count 매개 변수를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-298">In presentation code, you should see a count parameter on hello facet, used toodisplay hello number of facet results.</span></span> <span data-ttu-id="51ba5-299">패싯 결과 개수 hello hello 패싯 용어 또는 범위에서 일치 하는 문서 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-299">In facet results, count indicates hello number of documents that match on hello facet term or range.</span></span>
* `&facet=City,count:12`<br/>
  <span data-ttu-id="51ba5-300">패싯 쿼리에서 count tooa 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-300">In a facet query, you can set count tooa value.</span></span>  <span data-ttu-id="51ba5-301">hello 기본값은 10, 하지만 위쪽 또는 아래쪽에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-301">hello default is 10, but you can set it higher or lower.</span></span> <span data-ttu-id="51ba5-302">설정 `count:12` 가져옵니다 문서 수에 따라 패싯 결과에서 상위 12 일치 하는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-302">Setting `count:12` gets hello top 12 matches in facet results by document count.</span></span>
* <span data-ttu-id="51ba5-303">"`@odata.count`"</span><span class="sxs-lookup"><span data-stu-id="51ba5-303">"`@odata.count`"</span></span><br/>
  <span data-ttu-id="51ba5-304">Hello 쿼리 응답에이 값 hello hello 검색 결과에 일치 하는 항목 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-304">In hello query response, this value indicates hello number of matching items in hello search results.</span></span> <span data-ttu-id="51ba5-305">평균적으로 인해 hello 검색 단어와 일치 하는 항목의 toohello 존재 결합 하는 모든 패싯 결과의 hello 합계 보다 큽니다. 되었지만 패싯 값 일치 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-305">On average, it’s larger than hello sum of all facet results combined, due toohello presence of items that match hello search term, but have no facet value matches.</span></span>

<span data-ttu-id="51ba5-306">**패싯 결과의 개수 가져오기**</span><span class="sxs-lookup"><span data-stu-id="51ba5-306">**Get counts in facet results**</span></span>

<span data-ttu-id="51ba5-307">필터 tooa 패싯 쿼리를 추가 하면 tooretain hello 패싯 문 할 수 있습니다 (예를 들어 `facet=Rating&$filter=Rating ge 4`).</span><span class="sxs-lookup"><span data-stu-id="51ba5-307">When you add a filter tooa faceted query, you might want tooretain hello facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span></span> <span data-ttu-id="51ba5-308">기술적으로 패싯 = 등급 필요 하지 않습니다 되지만 4 이상에 hello 등급에 대 한 패싯 값 수를 반환 지속적으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-308">Technically, facet=Rating isn’t needed, but keeping it returns hello counts of facet values for ratings 4 and higher.</span></span> <span data-ttu-id="51ba5-309">예를 들어, "4"을 클릭 하 고 hello 쿼리에 포함 된 필터 크거나 너무 "4", 개수 반환 됩니다에 대 한 각 등급을 4 이상.</span><span class="sxs-lookup"><span data-stu-id="51ba5-309">For example, if you click "4" and hello query includes a filter for greater or equal too"4", counts are returned for each rating that is 4 and higher.</span></span>  

<span data-ttu-id="51ba5-310">**정확한 수의 패싯을 가져오는지 확인**</span><span class="sxs-lookup"><span data-stu-id="51ba5-310">**Make sure you get accurate facet counts**</span></span>

<span data-ttu-id="51ba5-311">특정 상황에서는 경우가 패싯 수가 hello 결과 집합을 일치 하지 않으므로 (참조 [Azure 검색 (포럼 게시물)의 패싯 탐색](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span><span class="sxs-lookup"><span data-stu-id="51ba5-311">Under certain circumstances, you might find that facet counts do not match hello result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span></span>

<span data-ttu-id="51ba5-312">패싯 개수 toohello 분할 아키텍처 인해 정확 하 게 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-312">Facet counts can be inaccurate due toohello sharding architecture.</span></span> <span data-ttu-id="51ba5-313">모든 검색 인덱스에 여러 분할 영역이 하 고 각 분할 결과 단일 구조로 결합 되는 문서 수에 따라 상위 n 개 면 hello를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-313">Every search index has multiple shards, and each shard reports hello top N facets by document count, which is then combined into a single result.</span></span> <span data-ttu-id="51ba5-314">분할 된 데이터베이스 일부가 여러 개의 일치 하는 값을 다른 사용자가 보다 적은 반면 일부 패싯 값이 누락 되었습니다 또는 아래 횟수가 계산 hello 결과에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in hello results.</span></span>

<span data-ttu-id="51ba5-315">Hello 수를 인위적으로 않아서 여 주위 사용할 수 있지만이 문제는 현재이 문제를 발생 하는 경우 언제 든 지 변경할 수 없습니다,:<number> 큰 숫자 tooenforce tooa 전체 각 분할에서 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating hello count:<number> tooa large number tooenforce full reporting from each shard.</span></span> <span data-ttu-id="51ba5-316">경우 수의 값을 hello: 보다 크거나 같은 toohello 숫자인 hello 필드의 고유 값의 정확한 결과 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-316">If hello value of count: is greater than or equal toohello number of unique values in hello field, you are guaranteed accurate results.</span></span> <span data-ttu-id="51ba5-317">그러나 문서 수가 많은 경우에는 성능이 저하되므로 이 옵션을 신중하게 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span></span>

### <a name="user-interface-tips"></a><span data-ttu-id="51ba5-318">사용자 인터페이스 팁</span><span class="sxs-lookup"><span data-stu-id="51ba5-318">User interface tips</span></span>
<span data-ttu-id="51ba5-319">**패싯 탐색의 각 필드에 대한 레이블 추가**</span><span class="sxs-lookup"><span data-stu-id="51ba5-319">**Add labels for each field in facet navigation**</span></span>

<span data-ttu-id="51ba5-320">레이블이 hello HTML 또는 폼에 일반적으로 정의 됩니다 (`index.cshtml` hello 예제 응용 프로그램에서).</span><span class="sxs-lookup"><span data-stu-id="51ba5-320">Labels are typically defined in hello HTML or form (`index.cshtml` in hello sample application).</span></span> <span data-ttu-id="51ba5-321">Azure Search에는 패싯 탐색 레이블 또는 다른 메타데이터에 사용할 수 있는 API가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span></span>

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a><span data-ttu-id="51ba5-322">범위를 기준으로 필터링</span><span class="sxs-lookup"><span data-stu-id="51ba5-322">Filter based on a range</span></span>
<span data-ttu-id="51ba5-323">값 범위에 대한 패싯은 일반적인 검색 응용 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-323">Faceting over ranges of values is a common search application requirement.</span></span> <span data-ttu-id="51ba5-324">범위는 숫자 데이터 및 DateTime 값에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-324">Ranges are supported for numeric data and DateTime values.</span></span> <span data-ttu-id="51ba5-325">각 접근 방법에 대한 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51ba5-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span></span>

<span data-ttu-id="51ba5-326">Azure 검색에서는 범위를 계산하는 두 가지 방법을 제공하여 범위 생성을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span></span> <span data-ttu-id="51ba5-327">두 방법에 대 한 Azure 검색 hello 제공 된 hello 입력이 주어진 적절 한 범위를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-327">For both approaches, Azure Search creates hello appropriate ranges given hello inputs you’ve provided.</span></span> <span data-ttu-id="51ba5-328">예를 들어 10|20|30 범위 값을 지정한 경우 0-10, 10-20, 20-30 범위가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span></span> <span data-ttu-id="51ba5-329">비어 있는 간격을 응용 프로그램에서 선택적으로 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-329">Your application can optionally remove any intervals that are empty.</span></span> 

<span data-ttu-id="51ba5-330">**Hello 간격 매개 변수를 사용 하는 접근 방식 1:**</span><span class="sxs-lookup"><span data-stu-id="51ba5-330">**Approach 1: Use hello interval parameter**</span></span>  
<span data-ttu-id="51ba5-331">$10 단위로, tooset 가격 면을 지정 합니다.`&facet=price,interval:10`</span><span class="sxs-lookup"><span data-stu-id="51ba5-331">tooset price facets in $10 increments, you would specify: `&facet=price,interval:10`</span></span>

<span data-ttu-id="51ba5-332">**방법 2: 값 목록 사용**</span><span class="sxs-lookup"><span data-stu-id="51ba5-332">**Approach 2: Use a values list**</span></span>  
<span data-ttu-id="51ba5-333">숫자 데이터의 경우 값 목록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-333">For numeric data, you can use a values list.</span></span>  <span data-ttu-id="51ba5-334">에 대 한 hello 패싯 범위를 고려는 `listPrice` 필드를 다음과 같이 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-334">Consider hello facet range for a `listPrice` field, rendered as follows:</span></span>

  ![샘플 값 목록][5]

<span data-ttu-id="51ba5-336">패싯 범위 hello hello 스크린 샷 앞에서 같은 toospecify 값 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-336">toospecify a facet range like hello one in hello preceding screen shot, use a values list:</span></span>

    facet=listPrice,values:10|25|100|500|1000|2500

<span data-ttu-id="51ba5-337">각 범위는 시작점, 끝점으로 hello 목록에서 값으로 0을 사용 하 고 hello 이전 범위 toocreate 불연속 간격 잘린 후에 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-337">Each range is built using 0 as a starting point, a value from hello list as an endpoint, and then trimmed of hello previous range toocreate discrete intervals.</span></span> <span data-ttu-id="51ba5-338">Azure Search는 이러한 작업을 패싯 탐색의 일부로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-338">Azure Search does these things as part of faceted navigation.</span></span> <span data-ttu-id="51ba5-339">각 간격의 구조를 지정 toowrite 코드가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-339">You do not have toowrite code for structuring each interval.</span></span>

### <a name="build-a-filter-for-a-range"></a><span data-ttu-id="51ba5-340">범위에 대한 필터 작성</span><span class="sxs-lookup"><span data-stu-id="51ba5-340">Build a filter for a range</span></span>
<span data-ttu-id="51ba5-341">선택한 범위에 따라 toofilter 문서 hello를 사용할 수 있습니다 `"ge"` 및 `"lt"` hello 범위의 hello 끝점을 정의 하는 두 부분으로 구성 식에서 연산자를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-341">toofilter documents based on a range you select, you can use hello `"ge"` and `"lt"` filter operators in a two-part expression that defines hello endpoints of hello range.</span></span> <span data-ttu-id="51ba5-342">예를 들어 선택한 경우 hello에 대 한 범위 10-25는 `listPrice` 필드가, hello 필터 잘립니다 `$filter=listPrice ge 10 and listPrice lt 25`합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-342">For example, if you choose hello range 10-25 for a `listPrice` field, hello filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span></span> <span data-ttu-id="51ba5-343">Hello 필터 식을 사용 하 여 hello 샘플 코드에서 **priceFrom** 및 **priceTo** tooset hello 끝점 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-343">In hello sample code, hello filter expression uses **priceFrom** and **priceTo** parameters tooset hello endpoints.</span></span> 

  ![값 범위 쿼리][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a><span data-ttu-id="51ba5-345">거리를 기준으로 필터링</span><span class="sxs-lookup"><span data-stu-id="51ba5-345">Filter based on distance</span></span>
<span data-ttu-id="51ba5-346">일반적인 toosee 저장소나 restaurant, 근접 tooyour 현재 위치에 따라 대상을 선택 하는 데 도움이 되도록 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-346">It’s common toosee filters that help you choose a store, restaurant, or destination based on its proximity tooyour current location.</span></span> <span data-ttu-id="51ba5-347">이 유형의 필터는 패싯 탐색처럼 보일 수 있지만 단순한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-347">While this type of filter might look like faceted navigation, it’s just a filter.</span></span> <span data-ttu-id="51ba5-348">특별히 이와 같은 특정 디자인 문제에 대한 구현 조언을 구하는 경우 이 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span></span>

<span data-ttu-id="51ba5-349">Azure Search에는 **geo.distance** 및 **geo.intersects**라는 두 개의 지리 공간 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span></span>

* <span data-ttu-id="51ba5-350">hello **geo.distance** 함수 두 점 사이의 hello 거리 킬로미터 단위로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-350">hello **geo.distance** function returns hello distance in kilometers between two points.</span></span> <span data-ttu-id="51ba5-351">1 포인트 필드 이며 다른 하나는 hello 필터의 일부분으로 전달 되는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-351">One point is a field and other is a constant passed as part of hello filter.</span></span> 
* <span data-ttu-id="51ba5-352">hello **geo.intersects** 함수 해당된 지점이 특정된 다각형 내에 있으면 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-352">hello **geo.intersects** function returns true if a given point is within a given polygon.</span></span> <span data-ttu-id="51ba5-353">hello 포인트 필드 이며 hello 다각형 hello 필터의 일부분으로 전달 하는 좌표 상수 목록으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-353">hello point is a field and hello polygon is specified as a constant list of coordinates passed as part of hello filter.</span></span>

<span data-ttu-id="51ba5-354">필터 예제는 [OData 식 구문(Azure 검색)](http://msdn.microsoft.com/library/azure/dn798921.aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span></span>

<a name="tryitout"></a>

## <a name="try-hello-demo"></a><span data-ttu-id="51ba5-355">Hello 데모를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="51ba5-355">Try hello demo</span></span>
<span data-ttu-id="51ba5-356">hello Azure 검색 작업 포털 데모가이 문서에서 참조 하는 hello 예제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-356">hello Azure Search Job Portal Demo contains hello examples referenced in this article.</span></span>

-   <span data-ttu-id="51ba5-357">참조 및 hello 작업 데모 온라인에서 테스트 [Azure 검색 작업 포털 데모](http://azjobsdemo.azurewebsites.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-357">See and test hello working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="51ba5-358">Hello에서 hello 코드 다운로드 [GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-358">Download hello code from hello [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

<span data-ttu-id="51ba5-359">검색 결과 사용할 때는 변경 쿼리 생성에 대 한 hello URL 살펴보십시오.</span><span class="sxs-lookup"><span data-stu-id="51ba5-359">As you work with search results, watch hello URL for changes in query construction.</span></span> <span data-ttu-id="51ba5-360">각 항목을 선택할 때이 응용 프로그램 tooappend 패싯 toohello URI에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-360">This application happens tooappend facets toohello URI as you select each one.</span></span>

1. <span data-ttu-id="51ba5-361">hello 데모 응용 프로그램의 toouse hello 매핑 기능 hello에서 Bing 지도 키 가져오기 [Bing Maps 개발자 센터](https://www.bingmapsportal.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-361">toouse hello mapping functionality of hello demo app, get a Bing Maps key from hello [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="51ba5-362">Hello에 기존 키 hello에 붙여넣습니다 `index.cshtml` 페이지.</span><span class="sxs-lookup"><span data-stu-id="51ba5-362">Paste it over hello existing key in hello `index.cshtml` page.</span></span> <span data-ttu-id="51ba5-363">hello `BingApiKey` hello에서 설정 `Web.config` 파일 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-363">hello `BingApiKey` setting in hello `Web.config` file is not used.</span></span> 

2. <span data-ttu-id="51ba5-364">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-364">Run hello application.</span></span> <span data-ttu-id="51ba5-365">Hello 선택적 둘러보기 걸리거나 hello 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-365">Take hello optional tour, or dismiss hello dialog box.</span></span>
   
3. <span data-ttu-id="51ba5-366">"분석가"와 같은 검색 용어를 입력 하 고 hello 검색 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-366">Enter a search term, such as "analyst", and click hello Search icon.</span></span> <span data-ttu-id="51ba5-367">hello 쿼리가 신속 하 게 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-367">hello query executes quickly.</span></span>
   
   <span data-ttu-id="51ba5-368">패싯 탐색 구조 hello 검색 결과 함께 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-368">A faceted navigation structure is also returned with hello search results.</span></span> <span data-ttu-id="51ba5-369">Hello 검색 결과 페이지 hello 패싯 탐색 구조에 대 한 각 패싯 결과 수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-369">In hello search result page, hello faceted navigation structure includes counts for each facet result.</span></span> <span data-ttu-id="51ba5-370">패싯을 선택하지 않았으므로 일치하는 모든 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-370">No facets are selected, so all matching results are returned.</span></span>
   
   ![패싯을 선택하기 전의 검색 결과][11]

4. <span data-ttu-id="51ba5-372">직함, 위치 또는 최소 급여를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-372">Click a Business Title, Location, or Minimum Salary.</span></span> <span data-ttu-id="51ba5-373">패싯 hello 초기 검색 시 null 되었지만 더 이상 일치 하는 항목의 hello 검색 결과 값을 사용 하는 대로 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-373">Facets were null on hello initial search, but as they take on values, hello search results are trimmed of items that no longer match.</span></span>
   
   ![패싯을 선택한 후의 검색 결과][12]

5. <span data-ttu-id="51ba5-375">tooclear hello 패싯 쿼리 다른 쿼리 동작을 시도할 수 있도록 클릭 hello `[X]` hello 패싯 tooclear hello 패싯을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-375">tooclear hello faceted query so that you can try different query behaviors, click hello `[X]` after hello selected facets tooclear hello facets.</span></span>
   
<a name="nextstep"></a>

## <a name="learn-more"></a><span data-ttu-id="51ba5-376">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="51ba5-376">Learn more</span></span>
<span data-ttu-id="51ba5-377">[Azure Search 심층 정보](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="51ba5-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span></span> <span data-ttu-id="51ba5-378">에 45:25는 데모는 방법에 tooimplement 패싯 합니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-378">At 45:25, there is a demo on how tooimplement facets.</span></span>

<span data-ttu-id="51ba5-379">패싯 탐색에 대 한 디자인 원칙에 더 많은 정보에 대 한 링크를 따라 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="51ba5-379">For more insights on design principles for faceted navigation, we recommend hello following links:</span></span>

* [<span data-ttu-id="51ba5-380">패싯 검색을 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="51ba5-380">Designing for Faceted Search</span></span>](http://www.uie.com/articles/faceted_search/)
* [<span data-ttu-id="51ba5-381">디자인 패턴: 패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="51ba5-381">Design Patterns: Faceted Navigation</span></span>](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

