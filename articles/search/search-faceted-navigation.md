---
title: "Azure Search에서 패싯 탐색을 구현하는 방법 | Microsoft Docs"
description: "Microsoft Azure에서 클라우드 호스팅되는 검색 서비스인 Azure 검색과 통합되는 응용 프로그램에 패싯 탐색을 추가합니다."
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
ms.openlocfilehash: 413f498eeb0bbc9a971c7a65200ed2fd8caa9aaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-implement-faceted-navigation-in-azure-search"></a><span data-ttu-id="d2a88-103">Azure 검색에서 패싯 탐색을 구현하는 방법</span><span class="sxs-lookup"><span data-stu-id="d2a88-103">How to implement faceted navigation in Azure Search</span></span>
<span data-ttu-id="d2a88-104">패싯 탐색은 검색 응용 프로그램에서 자기 주도형 드릴다운 탐색을 제공하는 필터링 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-104">Faceted navigation is a filtering mechanism that provides self-directed drilldown navigation in search applications.</span></span> <span data-ttu-id="d2a88-105">'패싯 탐색'이라는 용어가 낯설 수도 있지만 아마도 이전에 사용해 보셨을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-105">The term 'faceted navigation' may be unfamiliar, but you've probably used it before.</span></span> <span data-ttu-id="d2a88-106">다음 예제와 같이 패싯 탐색은 결과를 필터링하는 데 사용되는 범주일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-106">As the following example shows, faceted navigation is nothing more than the categories used to filter results.</span></span>

 ![Azure Search 작업 포털 데모][1]

<span data-ttu-id="d2a88-108">패싯 탐색은 검색의 대체 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-108">Faceted navigation is an alternative entry point to search.</span></span> <span data-ttu-id="d2a88-109">복잡한 검색 식을 직접 입력할 수 있는 편리한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-109">It offers a convenient alternative to typing complex search expressions by hand.</span></span> <span data-ttu-id="d2a88-110">패싯을 사용하면 원하는 항목을 쉽게 찾을 수 있으며 항상 결과를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-110">Facets can help you find what you're looking for, while ensuring that you don’t get zero results.</span></span> <span data-ttu-id="d2a88-111">개발자는 패싯을 통해 검색 모음을 탐색하는 데 가장 유용한 검색 조건을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-111">As a developer, facets let you expose the most useful search criteria for navigating your search corpus.</span></span> <span data-ttu-id="d2a88-112">온라인 소매 응용 프로그램에서는 종종 브랜드, 부서(어린이 신발), 크기, 가격, 인기도 및 등급에 대한 패싯 탐색이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-112">In online retail applications, faceted navigation is often built over brands, departments (kid’s shoes), size, price, popularity, and ratings.</span></span> 

<span data-ttu-id="d2a88-113">패싯 탐색의 구현은 검색 기술에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-113">Implementing faceted navigation differs across search technologies.</span></span> <span data-ttu-id="d2a88-114">Azure Search에서는 이전에 스키마에서 특성을 지정한 필드를 사용하여 쿼리 시 패싯 탐색이 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-114">In Azure Search, faceted navigation is built at query time, using fields that you previously attributed in your schema.</span></span>

-   <span data-ttu-id="d2a88-115">응용 프로그램에서 작성한 쿼리는 해당 문서 결과 집합에서 사용 가능한 패싯 필터 값을 받기 위해 *패싯 쿼리 매개 변수*를 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-115">In the queries that your application builds, a query must send *facet query parameters* to get the available facet filter values for that document result set.</span></span>

-   <span data-ttu-id="d2a88-116">실제로 문서 결과 집합을 자르려면 응용 프로그램에서 `$filter` 식도 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-116">To actually trim the document result set, the application must also apply a `$filter` expression.</span></span>

<span data-ttu-id="d2a88-117">응용 프로그램 개발 측면에서 쿼리를 생성하는 코드 작성은 대량 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-117">In your application development, writing code that constructs queries constitutes the bulk of the work.</span></span> <span data-ttu-id="d2a88-118">범위 정의 및 패싯 결과 수 가져오기에 대한 기본 제공 지원을 포함하여 패싯 탐색에서 예상하는 응용 프로그램 동작의 대부분은 서비스에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-118">Many of the application behaviors that you would expect from faceted navigation are provided by the service, including built-in support for defining ranges and getting counts for facet results.</span></span> <span data-ttu-id="d2a88-119">서비스에는 다루기 힘든 탐색 구조를 방지하는 데 도움이 되는 적절한 기본값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-119">The service also includes sensible defaults that help you avoid unwieldy navigation structures.</span></span> 

## <a name="sample-code-and-demo"></a><span data-ttu-id="d2a88-120">샘플 코드 및 데모</span><span class="sxs-lookup"><span data-stu-id="d2a88-120">Sample code and demo</span></span>
<span data-ttu-id="d2a88-121">이 문서에서는 구직 검색 포털을 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-121">This article uses a job search portal as an example.</span></span> <span data-ttu-id="d2a88-122">이 예제는 ASP.NET MVC 응용 프로그램으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-122">The example is implemented as an ASP.NET MVC application.</span></span>

-   <span data-ttu-id="d2a88-123">[Azure Search 구직 포털 데모](http://azjobsdemo.azurewebsites.net/)에서 온라인으로 작업 데모를 살펴보고 테스트하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-123">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="d2a88-124">[GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)에서 코드를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-124">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

## <a name="get-started"></a><span data-ttu-id="d2a88-125">시작</span><span class="sxs-lookup"><span data-stu-id="d2a88-125">Get started</span></span>
<span data-ttu-id="d2a88-126">검색 개발을 처음 접하는 경우 패싯 탐색을 자기 주도형 검색에 대한 가능성을 보여 주는 것이라고 생각하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-126">If you're new to search development, the best way to think of faceted navigation is that it shows the possibilities for self-directed search.</span></span> <span data-ttu-id="d2a88-127">패싯 탐색은 포인트 클릭 동작을 통해 검색 결과의 범위를 신속하게 좁히는 데 사용되는 미리 정의된 필터를 기반으로 하는 드릴다운 검색 환경에 일종입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-127">It’s a type of drill-down search experience, based on predefined filters, used for quickly narrowing down search results through point-and-click actions.</span></span> 

### <a name="interaction-model"></a><span data-ttu-id="d2a88-128">상호 작용 모델</span><span class="sxs-lookup"><span data-stu-id="d2a88-128">Interaction model</span></span>

<span data-ttu-id="d2a88-129">패싯 탐색의 검색 환경은 대화형이므로 먼저 사용자 동작에 대한 응답으로 펼쳐지는 쿼리의 시퀀스라는 점을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-129">The search experience for faceted navigation is iterative, so let’s start by understanding it as a sequence of queries that unfold in response to user actions.</span></span>

<span data-ttu-id="d2a88-130">시작 지점은 일반적으로 주변에서 패싯 탐색을 제공하는 응용 프로그램 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-130">The starting point is an application page that provides faceted navigation, typically placed on the periphery.</span></span> <span data-ttu-id="d2a88-131">패싯 탐색은 각 값에 대한 확인란 또는 클릭할 수 있는 텍스트가 포함된 트리 구조인 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-131">Faceted navigation is often a tree structure, with checkboxes for each value, or clickable text.</span></span> 

1. <span data-ttu-id="d2a88-132">Azure 검색으로 전송된 쿼리는 하나 이상의 패싯 쿼리 매개 변수를 통해 패싯 탐색 구조를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-132">A query sent to Azure Search specifies the faceted navigation structure via one or more facet query parameters.</span></span> <span data-ttu-id="d2a88-133">예를 들어 쿼리는 프레젠테이션을 구체화하는 `:values` 또는 `:sort` 옵션과 함께 `facet=Rating`이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-133">For instance, the query might include `facet=Rating`, perhaps with a `:values` or `:sort` option to further refine the presentation.</span></span>
2. <span data-ttu-id="d2a88-134">프레젠테이션 계층은 요청에 지정된 패싯을 사용하여 패싯 탐색을 제공하는 검색 페이지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-134">The presentation layer renders a search page that provides faceted navigation, using the facets specified on the request.</span></span>
3. <span data-ttu-id="d2a88-135">등급이 포함된 패싯 탐색 구조에서 사용자가 등급이 4 이상인 제품만 표시하기 위해 “4”를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-135">Given a faceted navigation structure that includes Rating, you click "4" to indicate that only products with a rating of 4 or higher should be shown.</span></span> 
4. <span data-ttu-id="d2a88-136">이에 대한 응답으로 응용 프로그램은 `$filter=Rating ge 4`</span><span class="sxs-lookup"><span data-stu-id="d2a88-136">In response, the application sends a query that includes `$filter=Rating ge 4`</span></span> 
5. <span data-ttu-id="d2a88-137">새 조건을 충족하는 항목(이 경우 등급이 4 이상인 제품)만 포함된 축소된 결과 집합을 표시하도록 프레젠테이션 계층에서 페이지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-137">The presentation layer updates the page, showing a reduced result set, containing just those items that satisfy the new criteria (in this case, products rated 4 and up).</span></span>

<span data-ttu-id="d2a88-138">패싯은 쿼리 매개 변수이지만 쿼리 입력과 혼동해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-138">A facet is a query parameter, but do not confuse it with query input.</span></span> <span data-ttu-id="d2a88-139">쿼리의 선택 조건으로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-139">It is never used as selection criteria in a query.</span></span> <span data-ttu-id="d2a88-140">패싯 쿼리 매개 변수는 응답에서 반환되는 탐색 구조의 입력이라고 생각해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-140">Instead, think of facet query parameters as inputs to the navigation structure that comes back in the response.</span></span> <span data-ttu-id="d2a88-141">제공한 각 패싯 쿼리 매개 변수에 대해 Azure Search는 각 패싯 값의 부분 결과에 포함된 문서 수를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-141">For each facet query parameter you provide, Azure Search evaluates how many documents are in the partial results for each facet value.</span></span>

<span data-ttu-id="d2a88-142">4단계의 `$filter` 에 주목하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-142">Notice the `$filter` in step 4.</span></span> <span data-ttu-id="d2a88-143">필터는 패싯 탐색의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-143">The filter is an important aspect of faceted navigation.</span></span> <span data-ttu-id="d2a88-144">패싯과 필터는 API에서 서로 독립적이지만 원하는 환경을 제공하려면 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-144">Although facets and filters are independent in the API, you need both to deliver the experience you intend.</span></span> 

### <a name="app-design-pattern"></a><span data-ttu-id="d2a88-145">앱 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="d2a88-145">App design pattern</span></span>

<span data-ttu-id="d2a88-146">응용 프로그램 코드에서 패턴은 패싯 쿼리 매개 변수를 사용하여 패싯 결과 및 $filter 식과 함께 패싯 탐색 구조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-146">In application code, the pattern is to use facet query parameters to return the faceted navigation structure along with facet results, plus a $filter expression.</span></span>  <span data-ttu-id="d2a88-147">필터 식은 패싯 값의 클릭 이벤트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-147">The filter expression handles the click event on the facet value.</span></span> <span data-ttu-id="d2a88-148">`$filter` 식은 프레젠테이션 계층으로 반환되는 검색 결과를 실제로 조정하는 숨은 코드라고 생각하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-148">Think of the `$filter` expression as the code behind the actual trimming of search results returned to the presentation layer.</span></span> <span data-ttu-id="d2a88-149">색상 패싯의 경우 빨간색을 클릭하는 것은 색상이 빨간색인 항목만 선택하는 `$filter` 식을 통해 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-149">Given a Colors facet, clicking the color Red is implemented through a `$filter` expression that selects only those items that have a color of red.</span></span> 

### <a name="query-basics"></a><span data-ttu-id="d2a88-150">쿼리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="d2a88-150">Query basics</span></span>

<span data-ttu-id="d2a88-151">Azure 검색에서는 하나 이상의 쿼리 매개 변수를 통해 요청이 지정됩니다(각 매개 변수에 대한 설명은 [문서 검색](http://msdn.microsoft.com/library/azure/dn798927.aspx) 참조).</span><span class="sxs-lookup"><span data-stu-id="d2a88-151">In Azure Search, a request is specified through one or more query parameters (see [Search Documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) for a description of each one).</span></span> <span data-ttu-id="d2a88-152">필수 사항인 쿼리 매개 변수는 없지만 쿼리가 유효하려면 하나 이상의 쿼리 매개 변수가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-152">None of the query parameters are required, but you must have at least one in order for a query to be valid.</span></span>

<span data-ttu-id="d2a88-153">관련 없는 적중 항목을 필터링하는 기능으로 이해되는 정밀도는 다음 두 식 중 하나 또는 둘 다를 통해 실현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-153">Precision, understood as the ability to filter out irrelevant hits, is achieved through one or both of these expressions:</span></span>

-   <span data-ttu-id="d2a88-154">**search=**</span><span class="sxs-lookup"><span data-stu-id="d2a88-154">**search=**</span></span>  
    <span data-ttu-id="d2a88-155">이 매개 변수의 값은 검색 식을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-155">The value of this parameter constitutes the search expression.</span></span> <span data-ttu-id="d2a88-156">단일 텍스트 조각 또는 여러 항 및 연산자를 포함하는 복잡한 검색 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-156">It might be a single piece of text, or a complex search expression that includes multiple terms and operators.</span></span> <span data-ttu-id="d2a88-157">서버의 경우 검색 식은 인덱스의 검색 가능한 필드에서 일치하는 용어를 쿼리하고 순위대로 결과를 반환하는 전체 텍스트 검색에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-157">On the server, a search expression is used for full-text search, querying searchable fields in the index for matching terms, returning results in rank order.</span></span> <span data-ttu-id="d2a88-158">`search`를 null로 설정한 경우 쿼리는 전체 인덱스에서 실행됩니다(즉, `search=*`).</span><span class="sxs-lookup"><span data-stu-id="d2a88-158">If you set `search` to null, query execution is over the entire index (that is, `search=*`).</span></span> <span data-ttu-id="d2a88-159">이 경우 쿼리의 다른 요소(예: `$filter` 또는 점수 매기기 프로필)는 반환되는 문서(`($filter`) 및 반환 순서(`scoringProfile` 또는 `$orderby`)에 영향을 주는 주요 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-159">In this case, other elements of the query, such as a `$filter` or scoring profile, are the primary factors affecting which documents are returned `($filter`) and in what order (`scoringProfile` or `$orderby`).</span></span>

-   <span data-ttu-id="d2a88-160">**$filter=**</span><span class="sxs-lookup"><span data-stu-id="d2a88-160">**$filter=**</span></span>  
    <span data-ttu-id="d2a88-161">필터는 특정 문서 특성 값을 기반으로 검색 결과의 크기를 제한하는 강력한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-161">A filter is a powerful mechanism for limiting the size of search results based on the values of specific document attributes.</span></span> <span data-ttu-id="d2a88-162">`$filter` 가 먼저 평가된 후 사용 가능한 값과 각 값의 해당 개수를 생성하는 패싯 논리가 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-162">A `$filter` is evaluated first, followed by faceting logic that generates the available values and corresponding counts for each value</span></span>

<span data-ttu-id="d2a88-163">복잡한 검색 식은 쿼리 성능을 저하시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-163">Complex search expressions decrease the performance of the query.</span></span> <span data-ttu-id="d2a88-164">되도록이면 효과적으로 작성된 필터 식을 사용하여 정밀도를 높이고 쿼리 성능을 향상시키세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-164">Where possible, use well-constructed filter expressions to increase precision and improve query performance.</span></span>

<span data-ttu-id="d2a88-165">필터를 통해 정밀도를 높이는 방법을 이해하려면 복잡한 검색 식을 필터 식이 포함된 식과 비교해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-165">To better understand how a filter adds more precision, compare a complex search expression to one that includes a filter expression:</span></span>

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

<span data-ttu-id="d2a88-166">두 쿼리 모두 유효하지만 Seattle에 주차장이 있는 모델이 아닌 곳을 찾으려는 경우에는 두 번째를 사용하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-166">Both queries are valid, but the second is superior if you’re looking for non-motels with parking in Seattle.</span></span>
-   <span data-ttu-id="d2a88-167">첫 번째 쿼리는 Name, Description 및 기타 검색 가능한 데이터가 포함된 모든 필드와 같은 문자열 필드에 언급되거나 언급되지 않은 특정 단어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-167">The first query relies on those specific words being mentioned or not mentioned in string fields like Name, Description, and any other field containing searchable data.</span></span>
-   <span data-ttu-id="d2a88-168">두 번째 쿼리는 구조화된 데이터에서 정확히 일치하는 항목을 찾으므로 정확도가 훨씬 높을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-168">The second query looks for precise matches on structured data and is likely to be much more accurate.</span></span>

<span data-ttu-id="d2a88-169">패싯 탐색이 포함된 응용 프로그램에서는 패싯 탐색 구조에 대한 각 사용자 작업이 수행된 후 검색 결과 범위를 좁혀야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-169">In applications that include faceted navigation, make sure that each user action over a faceted navigation structure is accompanied by a narrowing of search results.</span></span> <span data-ttu-id="d2a88-170">검색 결과 범위를 좁히려면 필터 식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-170">To narrow results, use a filter expression.</span></span>

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a><span data-ttu-id="d2a88-171">패싯 탐색 앱 구축</span><span class="sxs-lookup"><span data-stu-id="d2a88-171">Build a faceted navigation app</span></span>
<span data-ttu-id="d2a88-172">Azure Search를 사용하여 응용 프로그램 코드에서 검색 요청을 작성하는 패싯 탐색을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-172">You implement faceted navigation with Azure Search in your application code that builds the search request.</span></span> <span data-ttu-id="d2a88-173">패싯 탐색은 이전에 정의된 스키마의 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-173">The faceted navigation relies on elements in your schema that you defined previously.</span></span>

<span data-ttu-id="d2a88-174">검색 인덱스에 `Facetable [true|false]` 인덱스 특성이 미리 정의되어 있으므로 선택한 필드를 패싯 탐색 구조에서 사용하거나 사용하지 않도록 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-174">Predefined in your search index is the `Facetable [true|false]` index attribute, set on selected fields to enable or disable their use in a faceted navigation structure.</span></span> <span data-ttu-id="d2a88-175">`"Facetable" = true`가 아니면 패싯 탐색에서 필드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-175">Without `"Facetable" = true`, a field cannot be used in facet navigation.</span></span>

<span data-ttu-id="d2a88-176">코드의 프레젠테이션 계층은 사용자 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-176">The presentation layer in your code provides the user experience.</span></span> <span data-ttu-id="d2a88-177">레이블, 값, 확인란, 개수 등 패싯 탐색의 구성 부분을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-177">It should list the constituent parts of the faceted navigation, such as the label, values, check boxes, and the count.</span></span> <span data-ttu-id="d2a88-178">Azure 검색 REST API는 플랫폼에 독립적이므로 사용자가 원하는 언어와 플랫폼을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-178">The Azure Search REST API is platform agnostic, so use whatever language and platform you want.</span></span> <span data-ttu-id="d2a88-179">단, 각 추가 패싯이 선택될 때 업데이트된 UI 상태로 증분 새로 고침을 지원하는 UI 요소를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-179">The important thing is to include UI elements that support incremental refresh, with updated UI state as each additional facet is selected.</span></span> 

<span data-ttu-id="d2a88-180">쿼리 시 응용 프로그램 코드는 패싯에 필드를 제공하는 요청 매개 변수인 `facet=[string]`을 포함하는 요청을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-180">At query time, your application code creates a request that includes `facet=[string]`, a request parameter that provides the field to facet by.</span></span> <span data-ttu-id="d2a88-181">`&facet=color&facet=category&facet=rating`과 같이 각 패싯을 앰퍼샌드(&) 문자로 구분하여 여러 패싯을 쿼리에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-181">A query can have multiple facets, such as `&facet=color&facet=category&facet=rating`, each one separated by an ampersand (&) character.</span></span>

<span data-ttu-id="d2a88-182">또한 응용 프로그램 코드는 패싯 탐색에서 클릭 이벤트를 처리할 `$filter` 식을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-182">Application code must also construct a `$filter` expression to handle the click events in faceted navigation.</span></span> <span data-ttu-id="d2a88-183">`$filter` 는 패싯 값을 필터 조건으로 사용하여 검색 결과를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-183">A `$filter` reduces the search results, using the facet value as filter criteria.</span></span>

<span data-ttu-id="d2a88-184">Azure Search는 사용자가 입력한 하나 이상의 용어에 따라 검색 결과를 반환하고 패싯 탐색 구조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-184">Azure Search returns the search results, based on one or more terms that you enter, along with updates to the faceted navigation structure.</span></span> <span data-ttu-id="d2a88-185">Azure 검색에서 패싯 탐색은 패싯 값과 각 값에 대해 발견된 결과 수로 이루어진 단일 수준 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-185">In Azure Search, faceted navigation is a single-level construction, with facet values, and counts of how many results are found for each one.</span></span>

<span data-ttu-id="d2a88-186">다음 섹션에서는 각 부분을 작성하는 방법을 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-186">In the following sections, we take a closer look at how to build each part.</span></span>

<a name="buildindex"></a>

## <a name="build-the-index"></a><span data-ttu-id="d2a88-187">인덱스 작성</span><span class="sxs-lookup"><span data-stu-id="d2a88-187">Build the index</span></span>
<span data-ttu-id="d2a88-188">인덱스 특성 `"Facetable": true`를 통해 인덱스에서 패싯을 필드별로 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-188">Faceting is enabled on a field-by-field basis in the index, via this index attribute: `"Facetable": true`.</span></span>  
<span data-ttu-id="d2a88-189">패싯 탐색에 사용할 수 있는 모든 필드 형식은 기본적으로 `Facetable` 입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-189">All field types that could possibly be used in faceted navigation are `Facetable` by default.</span></span> <span data-ttu-id="d2a88-190">이러한 필드 형식에는 `Edm.String`, `Edm.DateTimeOffset` 및 모든 숫자 필드 형식(기본적으로 모든 필드 형식은 패싯 탐색에서 사용할 수 없는 `Edm.GeographyPoint`를 제외하고 패싯 가능)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-190">Such field types include `Edm.String`, `Edm.DateTimeOffset`, and all the numeric field types (essentially, all field types are facetable except `Edm.GeographyPoint`, which can’t be used in faceted navigation).</span></span> 

<span data-ttu-id="d2a88-191">인덱스를 작성할 때 패싯으로 사용해서는 안 되는 필드에 대한 패싯을 명시적으로 해제하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-191">When building an index, a best practice for faceted navigation is to explicitly turn faceting off for fields that should never be used as a facet.</span></span>  <span data-ttu-id="d2a88-192">특히 ID 또는 제품 이름과 같은 Singleton 값의 문자열 필드는 패싯 탐색에서 실수로(그리고 비효과적으로) 사용되지 않도록 `"Facetable": false`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-192">In particular, string fields for singleton values, such as an ID or product name, should be set to `"Facetable": false` to prevent their accidental (and ineffective) use in faceted navigation.</span></span> <span data-ttu-id="d2a88-193">필요 없는 패싯을 해제하면 인덱스 크기를 작게 유지하는 데 도움이 되며 일반적으로 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-193">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

<span data-ttu-id="d2a88-194">다음은 구직 포털 데모 샘플 앱의 스키마 중 일부이며 전체 크기를 줄이기 위해 일부 특성을 잘랐습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-194">Following is part of the schema for the Job Portal Demo sample app, trimmed of some attributes to reduce the size:</span></span>

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

<span data-ttu-id="d2a88-195">샘플 스키마에서 보시는 것처럼, ID 값과 같이 패싯으로 사용하면 안 되는 문자열 필드에 대해 `Facetable`이 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-195">As you can see in the sample schema, `Facetable` is turned off for string fields that shouldn’t be used as facets, such as ID values.</span></span> <span data-ttu-id="d2a88-196">필요 없는 패싯을 해제하면 인덱스 크기를 작게 유지하는 데 도움이 되며 일반적으로 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-196">Turning faceting off where you don’t need it helps keep the size of the index small, and typically improves performance.</span></span>

> [!TIP]
> <span data-ttu-id="d2a88-197">각 필드의 전체 인덱스 특성 집합을 포함하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-197">As a best practice, include the full set of index attributes for each field.</span></span> <span data-ttu-id="d2a88-198">`Facetable` 은 거의 모든 필드에 대해 기본적으로 설정되지만 각 특성을 의도적으로 설정하는 것이 각 스키마 의사 결정의 의미를 검토하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-198">Although `Facetable` is on by default for almost all fields, purposely setting each attribute can help you think through the implications of each schema decision.</span></span> 

<a name="checkdata"></a>

## <a name="check-the-data"></a><span data-ttu-id="d2a88-199">데이터 확인</span><span class="sxs-lookup"><span data-stu-id="d2a88-199">Check the data</span></span>
<span data-ttu-id="d2a88-200">데이터 품질은 패싯 탐색 구조가 예상대로 구체화되는지 여부에 직접적인 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-200">The quality of your data has a direct effect on whether the faceted navigation structure materializes as you expect it to.</span></span> <span data-ttu-id="d2a88-201">결과 집합을 줄이기 위한 필터 작성의 용이성에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-201">It also affects the ease of constructing filters to reduce the result set.</span></span>

<span data-ttu-id="d2a88-202">Brand 또는 Price별로 패싯하려는 경우에는 각 문서에 필터 옵션으로 유효하고 일관적이며 생산적인 *BrandName* 및 *ProductPrice* 값이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-202">If you want to facet by Brand or Price, each document should contain values for *BrandName* and *ProductPrice* that are valid, consistent, and productive as a filter option.</span></span>

<span data-ttu-id="d2a88-203">그 밖에도 다음과 같은 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-203">Here are a few reminders of what to scrub for:</span></span>

* <span data-ttu-id="d2a88-204">패싯하려는 모든 필드에 대해 자기 주도형 검색에서 필터로 적합한 값이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-204">For every field that you want to facet by, ask yourself whether it contains values that are suitable as filters in self-directed search.</span></span> <span data-ttu-id="d2a88-205">값은 간단하고, 설명을 포함하며, 경쟁 옵션 간에 명확한 선택을 제공할 수 있도록 구별되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-205">The values should be short, descriptive, and sufficiently distinctive to offer a clear choice between competing options.</span></span>
* <span data-ttu-id="d2a88-206">맞춤법 오류 또는 거의 일치하는 값.</span><span class="sxs-lookup"><span data-stu-id="d2a88-206">Misspellings or nearly matching values.</span></span> <span data-ttu-id="d2a88-207">Color를 패싯할 때 필드 값에 Orange와 Ornage(맞춤법 오류)가 포함되어 있는 경우 Color 필드를 기반으로 하는 패싯은 둘 값을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-207">If you facet on Color, and field values include Orange and Ornage (a misspelling), a facet based on the Color field would pick up both.</span></span>
* <span data-ttu-id="d2a88-208">대/소문자가 혼합된 텍스트도 패싯 탐색에서 나타날 수 있습니다. 예를 들어 orange와 Orange가 두 가지 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-208">Mixed case text can also wreak havoc in faceted navigation, with orange and Orange appearing as two different values.</span></span> 
* <span data-ttu-id="d2a88-209">동일한 값의 단수 및 복수 버전은 각각에 대해 별도의 패싯이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-209">Single and plural versions of the same value can result in a separate facet for each.</span></span>

<span data-ttu-id="d2a88-210">따라서 데이터를 충실히 준비하는 것은 효과적인 패싯 탐색의 기본적인 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-210">As you can imagine, diligence in preparing the data is an essential aspect of effective faceted navigation.</span></span>

<a name="presentationlayer"></a>

## <a name="build-the-ui"></a><span data-ttu-id="d2a88-211">UI 빌드</span><span class="sxs-lookup"><span data-stu-id="d2a88-211">Build the UI</span></span>
<span data-ttu-id="d2a88-212">프레젠테이션 계층에서 다시 작업하는 것은 놓쳤을 수 있는 요구 사항을 파악하고 검색 환경에 기본적으로 필요한 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-212">Working back from the presentation layer can help you uncover requirements that might be missed otherwise, and understand which capabilities are essential to the search experience.</span></span>

<span data-ttu-id="d2a88-213">패싯 탐색의 경우 웹 또는 응용 프로그램은 패싯 탐색 구조를 표시하고, 페이지에서 사용자 입력을 검색하며, 변경된 요소를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-213">In terms of faceted navigation, your web or application page displays the faceted navigation structure, detects user input on the page, and inserts the changed elements.</span></span> 

<span data-ttu-id="d2a88-214">웹 응용 프로그램의 경우 주로 AJAX가 프레젠테이션 계층에서 사용되는데, 이는 증분 변경 내용을 새로 고칠 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-214">For web applications, AJAX is commonly used in the presentation layer because it allows you to refresh incremental changes.</span></span> <span data-ttu-id="d2a88-215">ASP.NET MVC 또는 기타 HTTP를 통해 Azure 검색에 연결할 수 있는 모든 시각화 플랫폼을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-215">You could also use ASP.NET MVC or any other visualization platform that can connect to an Azure Search service over HTTP.</span></span> <span data-ttu-id="d2a88-216">이 문서 전체에 나오는 샘플 응용 프로그램 **Azure Search 구직 포털 데모**는 ASP.NET MVC 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-216">The sample application referenced throughout this article -- the **Azure Search Job Portal Demo** – happens to be an ASP.NET MVC application.</span></span>

<span data-ttu-id="d2a88-217">이 샘플에서 패싯 탐색은 검색 결과 페이지에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-217">In the sample, faceted navigation is built into the search results page.</span></span> <span data-ttu-id="d2a88-218">샘플 응용 프로그램의 `index.cshtml` 파일에서 가져온 다음 예제는 검색 결과 페이지에 패싯 탐색을 표시하는 동적 HTML 구조를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-218">The following example, taken from the `index.cshtml` file of the sample application, shows the static HTML structure for displaying faceted navigation on the search results page.</span></span> <span data-ttu-id="d2a88-219">검색 용어를 제출하거나 패킷을 선택 또는 선택 취소하면 자동으로 패싯 목록이 작성되거나 다시 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-219">The list of facets is built or rebuilt dynamically when you submit a search term, or select or clear a facet.</span></span>

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

<span data-ttu-id="d2a88-220">`index.cshtml` 페이지의 다음 코드 조각은 첫 번째 패싯인 직함을 표시하는 HTML을 동적으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-220">The following code snippet from the `index.cshtml` page dynamically builds the HTML to display the first facet, Business Title.</span></span> <span data-ttu-id="d2a88-221">그와 유사한 기능은 다른 패싯에 대한 HTML을 동적으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-221">Similar functions dynamically build the HTML for the other facets.</span></span> <span data-ttu-id="d2a88-222">각 패싯에는 해당 패싯 결과에 대해 발견된 항목 수를 표시하는 레이블과 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-222">Each facet has a label and a count, which displays the number of items found for that facet result.</span></span>

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
> <span data-ttu-id="d2a88-223">검색 결과 페이지를 디자인할 때 패싯을 지우는 메커니즘을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-223">When you design the search results page, remember to add a mechanism for clearing facets.</span></span> <span data-ttu-id="d2a88-224">확인란을 추가하는 경우 필터를 지우는 방법을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-224">If you add check boxes, you can easily see how to clear the filters.</span></span> <span data-ttu-id="d2a88-225">다른 레이아웃에는 이동 경로 탐색 패턴 또는 다른 창의적인 방법이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-225">For other layouts, you might need a breadcrumb pattern or another creative approach.</span></span> <span data-ttu-id="d2a88-226">예를 들어 구직 검색 포털 샘플 응용 프로그램에서 선택한 패싯 뒤에 있는 `[X]`를 클릭하여 패싯을 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-226">For example, in the Job Search Portal sample application, you can click the `[X]` after a selected facet to clear the facet.</span></span>

<a name="buildquery"></a>

## <a name="build-the-query"></a><span data-ttu-id="d2a88-227">쿼리 작성</span><span class="sxs-lookup"><span data-stu-id="d2a88-227">Build the query</span></span>
<span data-ttu-id="d2a88-228">쿼리를 만들기 위해 작성하는 코드는 검색 식, 패싯, 필터, 점수 매기기 프로필 등 요청을 구성하는 데 사용되는 유효한 쿼리의 모든 부분을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-228">The code that you write for building queries should specify all parts of a valid query, including search expressions, facets, filters, scoring profiles– anything used to formulate a request.</span></span> <span data-ttu-id="d2a88-229">이 섹션에서는 쿼리에 적합한 패싯의 위치 및 패싯과 함께 필터를 사용하여 결과 집합을 줄이는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-229">In this section, we explore where facets fit into a query, and how filters are used with facets to deliver a reduced result set.</span></span>

<span data-ttu-id="d2a88-230">패싯은 이 샘플 응용 프로그램의 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-230">Notice that facets are integral in this sample application.</span></span> <span data-ttu-id="d2a88-231">구직 포털 데모의 검색 환경은 패싯 탐색 및 필터를 중심으로 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-231">The search experience in the Job Portal Demo is designed around faceted navigation and filters.</span></span> <span data-ttu-id="d2a88-232">페이지에서 패싯 탐색의 주요 위치는 그 중요성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-232">The prominent placement of faceted navigation on the page demonstrates its importance.</span></span> 

<span data-ttu-id="d2a88-233">대부분 예제에서 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-233">An example is often a good place to begin.</span></span> <span data-ttu-id="d2a88-234">`JobsSearch.cs` 파일에서 가져온 다음 예제는 직함, 위치, 게시 유형, 최소 급여를 기반으로 패싯 탐색을 만드는 요청을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-234">The following example, taken from the `JobsSearch.cs` file, builds a request that creates facet navigation based on Business Title, Location, Posting Type, and Minimum Salary.</span></span> 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

<span data-ttu-id="d2a88-235">패싯 쿼리 매개 변수는 필드로 설정되어 있으며, 데이터 형식에 따라 `count:<integer>`, `sort:<>`, `interval:<integer>` 및 `values:<list>`를 포함하는 쉼표로 구분된 목록으로 추가 매개 변수화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-235">A facet query parameter is set to a field and depending on the data type, can be further parameterized by comma-delimited list that includes `count:<integer>`, `sort:<>`, `interval:<integer>`, and `values:<list>`.</span></span> <span data-ttu-id="d2a88-236">값 목록은 범위를 설정할 때 숫자 데이터에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-236">A values list is supported for numeric data when setting up ranges.</span></span> <span data-ttu-id="d2a88-237">자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-237">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for usage details.</span></span>

<span data-ttu-id="d2a88-238">패싯과 함께, 응용 프로그램에서 작성된 요청도 패싯 값 선택 항목에 따라 후보 문서 집합의 범위를 좁히는 필터를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-238">Along with facets, the request formulated by your application should also build filters to narrow down the set of candidate documents based on a facet value selection.</span></span> <span data-ttu-id="d2a88-239">자전거 매장의 경우 패싯 탐색은 *어떤 색상, 어떤 제조업체, 어떤 종류의 자전거를 판매합니까?*와 같은 질문에 대한 단서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-239">For a bike store, faceted navigation provides clues to questions like *What colors, manufacturers, and types of bikes are available?*.</span></span> <span data-ttu-id="d2a88-240">필터링은 *이 가격대의 빨간색 산악용 자전거는 무엇입니까?*와 같은 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-240">Filtering answers questions like *Which exact bikes are red, mountain bikes, in this price range?*.</span></span> <span data-ttu-id="d2a88-241">빨간색 제품만 표시되도록 사용자가 "빨간색"을 클릭하면 응용 프로그램에서 보내는 다음 쿼리에 `$filter=Color eq ‘Red’`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-241">When you click "Red" to indicate that only Red products should be shown, the next query the application sends includes `$filter=Color eq ‘Red’`.</span></span>

<span data-ttu-id="d2a88-242">사용자가 직함 패싯에서 값을 선택하는 경우 `JobsSearch.cs` 페이지의 다음 코드 조각은 선택된 직함을 필터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-242">The following code snippet from the `JobsSearch.cs` page adds the selected Business Title to the filter if you select a value from the Business Title facet.</span></span>

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a><span data-ttu-id="d2a88-243">팁 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d2a88-243">Tips and best practices</span></span>

### <a name="indexing-tips"></a><span data-ttu-id="d2a88-244">인덱싱 팁</span><span class="sxs-lookup"><span data-stu-id="d2a88-244">Indexing tips</span></span>
<span data-ttu-id="d2a88-245">**검색 상자를 사용하지 않을 경우 인덱스 효율성 향상**</span><span class="sxs-lookup"><span data-stu-id="d2a88-245">**Improve index efficiency if you don't use a Search box**</span></span>

<span data-ttu-id="d2a88-246">응용 프로그램에서 검색 상자 없이 패싯 탐색만 사용하는 경우 필드를 `searchable=false`, `facetable=true`로 표시하여 보다 압축된 인덱스를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-246">If your application uses faceted navigation exclusively (that is, no search box), you can mark the field as `searchable=false`, `facetable=true` to produce a more compact index.</span></span> <span data-ttu-id="d2a88-247">또한 인덱싱은 여러 단어로 된 값의 구성 요소 부분에 대한 인덱싱 또는 단어 분리 없이 전체 패싯 값에서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-247">In addition, indexing occurs only on whole facet values, with no word-break or indexing of the component parts of a multi-word value.</span></span>

<span data-ttu-id="d2a88-248">**패싯으로 사용할 수 있는 필드 지정**</span><span class="sxs-lookup"><span data-stu-id="d2a88-248">**Specify which fields can be used as facets**</span></span>

<span data-ttu-id="d2a88-249">인덱스의 스키마에 따라 패싯으로 사용할 수 있는 필드가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-249">Recall that the schema of the index determines which fields are available to use as a facet.</span></span> <span data-ttu-id="d2a88-250">필드가 패싯 가능한 경우 쿼리는 패싯할 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-250">Assuming a field is facetable, the query specifies which fields to facet by.</span></span> <span data-ttu-id="d2a88-251">패싯할 필드는 레이블 아래에 표시되는 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-251">The field by which you are faceting provides the values that appear below the label.</span></span> 

<span data-ttu-id="d2a88-252">각 레이블 아래에 표시되는 값은 인덱스에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-252">The values that appear under each label are retrieved from the index.</span></span> <span data-ttu-id="d2a88-253">예를 들어 패싯 필드가 *Color*인 경우 추가 필터링에 사용할 수 있는 값은 해당 필드에 대한 값(Red, Black 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-253">For example, if the facet field is *Color*, the values available for additional filtering are the values for that field - Red, Black, and so forth.</span></span>

<span data-ttu-id="d2a88-254">Numeric 및 DateTime 값에 한해, 패싯 필드에서 값을 명시적으로 설정할 수 있습니다(예: `facet=Rating,values:1|2|3|4|5`).</span><span class="sxs-lookup"><span data-stu-id="d2a88-254">For Numeric and DateTime values only, you can explicitly set values on the facet field (for example, `facet=Rating,values:1|2|3|4|5`).</span></span> <span data-ttu-id="d2a88-255">이러한 필드 형식에는 값 목록을 사용하여 패싯 결과를 연속 범위(숫자 값 또는 기간을 기반으로 하는 범위)로 구분하는 작업을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-255">A values list is allowed for these field types to simplify the separation of facet results into contiguous ranges (either ranges based on numeric values or time periods).</span></span> 

<span data-ttu-id="d2a88-256">**기본적으로 한 수준의 패싯 탐색만 유지 가능**</span><span class="sxs-lookup"><span data-stu-id="d2a88-256">**By default you can only have one level of faceted navigation**</span></span> 

<span data-ttu-id="d2a88-257">계층 구조에서 패싯 중첩은 직접 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-257">As noted, there is no direct support for nesting facets in a hierarchy.</span></span> <span data-ttu-id="d2a88-258">기본적으로 Azure Search의 패싯 탐색은 하나의 필터 수준만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-258">By default, faceted navigation in Azure Search only supports one level of filters.</span></span> <span data-ttu-id="d2a88-259">그러나 해결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-259">However, workarounds do exist.</span></span> <span data-ttu-id="d2a88-260">`Collection(Edm.String)` 의 계층적 패싯 구조를 계층당 하나의 항목으로 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-260">You can encode a hierarchical facet structure in a `Collection(Edm.String)` with one entry point per hierarchy.</span></span> <span data-ttu-id="d2a88-261">이 해결책을 구현하는 방법은 이 문서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-261">Implementing this workaround is beyond the scope of this article.</span></span> 

### <a name="querying-tips"></a><span data-ttu-id="d2a88-262">쿼리 팁</span><span class="sxs-lookup"><span data-stu-id="d2a88-262">Querying tips</span></span>
<span data-ttu-id="d2a88-263">**필드의 유효성 검사**</span><span class="sxs-lookup"><span data-stu-id="d2a88-263">**Validate fields**</span></span>

<span data-ttu-id="d2a88-264">신뢰할 수 없는 사용자 입력을 기반으로 패싯 목록을 동적으로 빌드하는 경우 패싯 필드의 이름이 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-264">If you build the list of facets dynamically based on untrusted user input, validate that the names of the faceted fields are valid.</span></span> <span data-ttu-id="d2a88-265">또는 .NET에서 `Uri.EscapeDataString()`을 사용하거나 본인이 선택한 플랫폼에서 그에 상응하는 옵션을 사용하여 URL을 빌드할 때 이름을 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-265">Or, escape the names when building URLs by using either `Uri.EscapeDataString()` in .NET, or the equivalent in your platform of choice.</span></span>

### <a name="filtering-tips"></a><span data-ttu-id="d2a88-266">필터링 팁</span><span class="sxs-lookup"><span data-stu-id="d2a88-266">Filtering tips</span></span>
<span data-ttu-id="d2a88-267">**필터로 검색 정확도 향상**</span><span class="sxs-lookup"><span data-stu-id="d2a88-267">**Increase search precision with filters**</span></span>

<span data-ttu-id="d2a88-268">필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-268">Use filters.</span></span> <span data-ttu-id="d2a88-269">검색 식에만 의존할 경우 형태소 분석으로 인해 해당 필드에 정확한 패싯 값이 없는 문서가 반환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-269">If you rely on just search expressions alone, stemming could cause a document to be returned that doesn’t have the precise facet value in any of its fields.</span></span>

<span data-ttu-id="d2a88-270">**필터로 검색 성능 향상**</span><span class="sxs-lookup"><span data-stu-id="d2a88-270">**Increase search performance with filters**</span></span>

<span data-ttu-id="d2a88-271">필터는 검색 후보 문서 집합의 범위를 좁히고 순위에서 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-271">Filters narrow down the set of candidate documents for search and exclude them from ranking.</span></span> <span data-ttu-id="d2a88-272">대량의 문서 집합이 있는 경우 엄선된 패싯 드릴다운을 사용하면 때로는 성능을 크게 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-272">If you have a large set of documents, using a selective facet drill-down often gives you better performance.</span></span>
  
<span data-ttu-id="d2a88-273">**패싯 필드만 필터링**</span><span class="sxs-lookup"><span data-stu-id="d2a88-273">**Filter only the faceted fields**</span></span>

<span data-ttu-id="d2a88-274">패싯 드릴다운에서는 일반적으로 검색 가능한 모든 필드에 걸쳐 있지 않고 특정(패싯) 필드에만 패싯 값이 있는 문서만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-274">In faceted drill-down, you typically want to only include documents that have the facet value in a specific (faceted) field, not anywhere across all searchable fields.</span></span> <span data-ttu-id="d2a88-275">필터를 추가하면 일치하는 값의 패싯 필터에서만 검색하도록 지시하여 대상 필드를 보강할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-275">Adding a filter reinforces the target field by directing the service to search only in the faceted field for a matching value.</span></span>

<span data-ttu-id="d2a88-276">**추가 필터로 패싯 결과 자르기**</span><span class="sxs-lookup"><span data-stu-id="d2a88-276">**Trim facet results with more filters**</span></span>

<span data-ttu-id="d2a88-277">패싯 결과는 패싯 용어와 일치하는 검색 결과에서 발견된 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-277">Facet results are documents found in the search results that match a facet term.</span></span> <span data-ttu-id="d2a88-278">다음 예제의 *cloud computing*에 대한 검색 결과에서 254개 항목은 콘텐츠 형식이 *internal specification*입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-278">In the following example, in search results for *cloud computing*, 254 items also have *internal specification* as a content type.</span></span> <span data-ttu-id="d2a88-279">항목은 상호 배타적이지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-279">Items are not necessarily mutually exclusive.</span></span> <span data-ttu-id="d2a88-280">하나의 항목이 두 필터 조건을 모두 충족하는 경우에는 각각 하나로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-280">If an item meets the criteria of both filters, it is counted in each one.</span></span> <span data-ttu-id="d2a88-281">이 중복은 주로 문서 태깅을 구현하는 데 사용되는 `Collection(Edm.String)` 필드를 패싯할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-281">This duplication is possible when faceting on `Collection(Edm.String)` fields, which are often used to implement document tagging.</span></span>

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

<span data-ttu-id="d2a88-282">일반적으로 패싯 결과가 지속적으로 너무 큰 경우에는 필터를 더 추가하여 사용자에게 검색 범위를 좁힐 수 있는 추가 옵션을 제공하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-282">In general, if you find that facet results are consistently too large, we recommend that you add more filters to give users more options for narrowing the search.</span></span>

### <a name="tips-about-result-count"></a><span data-ttu-id="d2a88-283">결과 개수에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="d2a88-283">Tips about result count</span></span>

<span data-ttu-id="d2a88-284">**패싯 탐색의 항목 수 제한**</span><span class="sxs-lookup"><span data-stu-id="d2a88-284">**Limit the number of items in the facet navigation**</span></span>

<span data-ttu-id="d2a88-285">탐색 트리의 각 패싯 필드는 기본적으로 10개의 값으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-285">For each faceted field in the navigation tree, there is a default limit of 10 values.</span></span> <span data-ttu-id="d2a88-286">이 기본값은 값 목록을 관리하기 쉬운 크기로 유지하므로 탐색 구조에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-286">This default makes sense for navigation structures because it keeps the values list to a manageable size.</span></span> <span data-ttu-id="d2a88-287">count에 값을 할당하여 기본값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-287">You can override the default by assigning a value to count.</span></span>

* <span data-ttu-id="d2a88-288">`&facet=city,count:5`는 상위 순위 결과에서 발견된 처음 5개 도시만 패싯 결과로 반환되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-288">`&facet=city,count:5` specifies that only the first five cities found in the top ranked results are returned as a facet result.</span></span> <span data-ttu-id="d2a88-289">검색 용어가 "공항"이고 일치 항목이 32개인 샘플 쿼리를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-289">Consider a sample query with a search term of “airport” and 32 matches.</span></span> <span data-ttu-id="d2a88-290">쿼리에서 `&facet=city,count:5`를 지정하면 검색 결과에 문서 수가 가장 많은 상위 5개의 고유한 도시만 패싯 결과에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-290">If the query specifies `&facet=city,count:5`, only the first five unique cities with the most documents in the search results are included in the facet results.</span></span>

<span data-ttu-id="d2a88-291">패싯 결과와 검색 결과의 차이에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-291">Notice the distinction between facet results and search results.</span></span> <span data-ttu-id="d2a88-292">검색 결과는 쿼리와 일치하는 모든 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-292">Search results are all the documents that match the query.</span></span> <span data-ttu-id="d2a88-293">패싯 결과는 각 패싯 값에 대한 일치 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-293">Facet results are the matches for each facet value.</span></span> <span data-ttu-id="d2a88-294">이 예제에서 검색 결과에는 패싯 분류 목록(이 예제의 경우 5)에 없는 City 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-294">In the example, search results include City names that are not in the facet classification list (5 in our example).</span></span> <span data-ttu-id="d2a88-295">패싯 탐색을 통해 필터링된 결과는 사용자가 패싯을 지우거나 City 이외의 다른 패싯을 선택한 경우에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-295">Results that are filtered out through faceted navigation become visible when you clear facets, or choose other facets besides City.</span></span> 

> [!NOTE]
> <span data-ttu-id="d2a88-296">두 가지 이상의 형식이 있을 때 `count`를 설명하면 혼동을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-296">Discussing `count` when there is more than one type can be confusing.</span></span> <span data-ttu-id="d2a88-297">다음 표에서는 Azure 검색 API, 샘플 코드 및 설명서에서 용어가 사용되는 방식에 대한 간략한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-297">The following table offers a brief summary of how the term is used in Azure Search API, sample code, and documentation.</span></span> 

* `@colorFacet.count`<br/>
  <span data-ttu-id="d2a88-298">프레젠테이션 코드에는 패싯 결과 수를 표시하는 데 사용되는 count 매개 변수가 패싯에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-298">In presentation code, you should see a count parameter on the facet, used to display the number of facet results.</span></span> <span data-ttu-id="d2a88-299">패싯 결과에서 count는 패싯 용어 또는 범위와 일치하는 문서 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-299">In facet results, count indicates the number of documents that match on the facet term or range.</span></span>
* `&facet=City,count:12`<br/>
  <span data-ttu-id="d2a88-300">패싯 쿼리에서는 count를 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-300">In a facet query, you can set count to a value.</span></span>  <span data-ttu-id="d2a88-301">기본값은 10이지만 더 높거나 낮은 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-301">The default is 10, but you can set it higher or lower.</span></span> <span data-ttu-id="d2a88-302">`count:12` 를 설정하면 문서 수에 따라 패싯 결과에서 상위 12개의 일치하는 항목을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-302">Setting `count:12` gets the top 12 matches in facet results by document count.</span></span>
* <span data-ttu-id="d2a88-303">"`@odata.count`"</span><span class="sxs-lookup"><span data-stu-id="d2a88-303">"`@odata.count`"</span></span><br/>
  <span data-ttu-id="d2a88-304">쿼리 응답에서 이 값은 검색 결과의 일치하는 항목 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-304">In the query response, this value indicates the number of matching items in the search results.</span></span> <span data-ttu-id="d2a88-305">검색 용어와 일치하지만 패싯 값이 일치하지 않는 항목이 존재하기 때문에 이는 평균적으로 모든 패싯 결과의 합계보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-305">On average, it’s larger than the sum of all facet results combined, due to the presence of items that match the search term, but have no facet value matches.</span></span>

<span data-ttu-id="d2a88-306">**패싯 결과의 개수 가져오기**</span><span class="sxs-lookup"><span data-stu-id="d2a88-306">**Get counts in facet results**</span></span>

<span data-ttu-id="d2a88-307">패싯 쿼리에 필터를 추가할 때 패싯 문(예: `facet=Rating&$filter=Rating ge 4`)을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-307">When you add a filter to a faceted query, you might want to retain the facet statement (for example, `facet=Rating&$filter=Rating ge 4`).</span></span> <span data-ttu-id="d2a88-308">기술적으로는 facet=Rating이 필요하지 않지만 이를 유지하면 등급 4 이상에 대한 패싯 값의 개수가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-308">Technically, facet=Rating isn’t needed, but keeping it returns the counts of facet values for ratings 4 and higher.</span></span> <span data-ttu-id="d2a88-309">예를 들어 사용자가 "4"를 클릭하고 쿼리에 "4" 이상에 대한 필터가 포함되어 있으면 4 이상인 각 등급의 개수가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-309">For example, if you click "4" and the query includes a filter for greater or equal to "4", counts are returned for each rating that is 4 and higher.</span></span>  

<span data-ttu-id="d2a88-310">**정확한 수의 패싯을 가져오는지 확인**</span><span class="sxs-lookup"><span data-stu-id="d2a88-310">**Make sure you get accurate facet counts**</span></span>

<span data-ttu-id="d2a88-311">경우에 따라 패싯 수가 결과 집합과 일치하지 않을 수 있습니다( [Azure 검색의 패싯 탐색(포럼 게시물)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)참조).</span><span class="sxs-lookup"><span data-stu-id="d2a88-311">Under certain circumstances, you might find that facet counts do not match the result sets (see [Faceted navigation in Azure Search (forum post)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).</span></span>

<span data-ttu-id="d2a88-312">패싯 수는 분할 아키텍처로 인해 부정확할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-312">Facet counts can be inaccurate due to the sharding architecture.</span></span> <span data-ttu-id="d2a88-313">모든 검색 인덱스에는 여러 개의 분할된 데이터베이스가 있으며, 각 분할된 데이터베이스는 문서 수에 따라 상위 N개의 패싯을 보고합니다. 이 값이 단일 결과로 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-313">Every search index has multiple shards, and each shard reports the top N facets by document count, which is then combined into a single result.</span></span> <span data-ttu-id="d2a88-314">분할된 데이터베이스 중에 일치하는 값이 많은 것과 적은 것이 있는 경우 결과에서 일부 패싯 값이 누락되거나 적은 개수로 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-314">If some shards have many matching values, while others have fewer, you may find that some facet values are missing or under-counted in the results.</span></span>

<span data-ttu-id="d2a88-315">이 동작은 언제든 변경될 수 있지만 이 동작이 발생한 경우 count:<number>를 큰 값으로 인위적으로 늘려 각 분할된 데이터베이스에서 전체 보고하도록 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-315">Although this behavior could change at any time, if you encounter this behavior today, you can work around it by artificially inflating the count:<number> to a large number to enforce full reporting from each shard.</span></span> <span data-ttu-id="d2a88-316">count: 값이 필드의 고유 값 수보다 크거나 같으면 정확한 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-316">If the value of count: is greater than or equal to the number of unique values in the field, you are guaranteed accurate results.</span></span> <span data-ttu-id="d2a88-317">그러나 문서 수가 많은 경우에는 성능이 저하되므로 이 옵션을 신중하게 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-317">However, when document counts are high, there is a performance penalty, so use this option judiciously.</span></span>

### <a name="user-interface-tips"></a><span data-ttu-id="d2a88-318">사용자 인터페이스 팁</span><span class="sxs-lookup"><span data-stu-id="d2a88-318">User interface tips</span></span>
<span data-ttu-id="d2a88-319">**패싯 탐색의 각 필드에 대한 레이블 추가**</span><span class="sxs-lookup"><span data-stu-id="d2a88-319">**Add labels for each field in facet navigation**</span></span>

<span data-ttu-id="d2a88-320">레이블은 일반적으로 HTML 양식(샘플 응용 프로그램의 `index.cshtml`)으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-320">Labels are typically defined in the HTML or form (`index.cshtml` in the sample application).</span></span> <span data-ttu-id="d2a88-321">Azure Search에는 패싯 탐색 레이블 또는 다른 메타데이터에 사용할 수 있는 API가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-321">There is no API in Azure Search for facet navigation labels or any other metadata.</span></span>

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a><span data-ttu-id="d2a88-322">범위를 기준으로 필터링</span><span class="sxs-lookup"><span data-stu-id="d2a88-322">Filter based on a range</span></span>
<span data-ttu-id="d2a88-323">값 범위에 대한 패싯은 일반적인 검색 응용 프로그램 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-323">Faceting over ranges of values is a common search application requirement.</span></span> <span data-ttu-id="d2a88-324">범위는 숫자 데이터 및 DateTime 값에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-324">Ranges are supported for numeric data and DateTime values.</span></span> <span data-ttu-id="d2a88-325">각 접근 방법에 대한 자세한 내용은 [문서 검색(Azure 검색 API)](http://msdn.microsoft.com/library/azure/dn798927.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-325">You can read more about each approach in [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).</span></span>

<span data-ttu-id="d2a88-326">Azure 검색에서는 범위를 계산하는 두 가지 방법을 제공하여 범위 생성을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-326">Azure Search simplifies range construction by providing two approaches for computing a range.</span></span> <span data-ttu-id="d2a88-327">두 방법 모두에 대해 Azure 검색에서는 사용자가 입력을 제공한 경우 적절한 범위를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-327">For both approaches, Azure Search creates the appropriate ranges given the inputs you’ve provided.</span></span> <span data-ttu-id="d2a88-328">예를 들어 10|20|30 범위 값을 지정한 경우 0-10, 10-20, 20-30 범위가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-328">For instance, if you specify range values of 10|20|30, it automatically creates ranges of 0-10, 10-20, 20-30.</span></span> <span data-ttu-id="d2a88-329">비어 있는 간격을 응용 프로그램에서 선택적으로 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-329">Your application can optionally remove any intervals that are empty.</span></span> 

<span data-ttu-id="d2a88-330">**방법 1: interval 매개 변수 사용**</span><span class="sxs-lookup"><span data-stu-id="d2a88-330">**Approach 1: Use the interval parameter**</span></span>  
<span data-ttu-id="d2a88-331">10달러 단위로 증분되는 가격 패싯을 설정하려면 다음과 같이 지정합니다. `&facet=price,interval:10`</span><span class="sxs-lookup"><span data-stu-id="d2a88-331">To set price facets in $10 increments, you would specify: `&facet=price,interval:10`</span></span>

<span data-ttu-id="d2a88-332">**방법 2: 값 목록 사용**</span><span class="sxs-lookup"><span data-stu-id="d2a88-332">**Approach 2: Use a values list**</span></span>  
<span data-ttu-id="d2a88-333">숫자 데이터의 경우 값 목록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-333">For numeric data, you can use a values list.</span></span>  <span data-ttu-id="d2a88-334">다음과 같이 렌더링된 `listPrice`의 패싯 범위를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-334">Consider the facet range for a `listPrice` field, rendered as follows:</span></span>

  ![샘플 값 목록][5]

<span data-ttu-id="d2a88-336">이전 스크린샷과 같은 패싯 범위를 지정하려면 값 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-336">To specify a facet range like the one in the preceding screen shot, use a values list:</span></span>

    facet=listPrice,values:10|25|100|500|1000|2500

<span data-ttu-id="d2a88-337">각 범위는 0부터 작성되며, 목록의 값을 끝점으로 사용하고 이전 범위를 잘라 불연속 간격을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-337">Each range is built using 0 as a starting point, a value from the list as an endpoint, and then trimmed of the previous range to create discrete intervals.</span></span> <span data-ttu-id="d2a88-338">Azure Search는 이러한 작업을 패싯 탐색의 일부로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-338">Azure Search does these things as part of faceted navigation.</span></span> <span data-ttu-id="d2a88-339">각 간격을 구성하기 위해 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-339">You do not have to write code for structuring each interval.</span></span>

### <a name="build-a-filter-for-a-range"></a><span data-ttu-id="d2a88-340">범위에 대한 필터 작성</span><span class="sxs-lookup"><span data-stu-id="d2a88-340">Build a filter for a range</span></span>
<span data-ttu-id="d2a88-341">사용자가 선택한 범위에 따라 문서를 필터링하려면 범위의 끝점을 정의하는 두 부분으로 구성된 식에서 `"ge"` 및 `"lt"` 필터 연산자를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-341">To filter documents based on a range you select, you can use the `"ge"` and `"lt"` filter operators in a two-part expression that defines the endpoints of the range.</span></span> <span data-ttu-id="d2a88-342">예를 들어 `listPrice` 필드의 범위를 10-25로 선택하면 필터는 `$filter=listPrice ge 10 and listPrice lt 25`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-342">For example, if you choose the range 10-25 for a `listPrice` field, the filter would be `$filter=listPrice ge 10 and listPrice lt 25`.</span></span> <span data-ttu-id="d2a88-343">샘플 코드의 필터 식에서는 **priceFrom** 및 **priceTo** 매개 변수를 사용하여 끝점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-343">In the sample code, the filter expression uses **priceFrom** and **priceTo** parameters to set the endpoints.</span></span> 

  ![값 범위 쿼리][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a><span data-ttu-id="d2a88-345">거리를 기준으로 필터링</span><span class="sxs-lookup"><span data-stu-id="d2a88-345">Filter based on distance</span></span>
<span data-ttu-id="d2a88-346">일반적으로 필터를 사용하면 현재 위치와의 근접성에 따라 매장, 레스토랑 또는 목적지를 쉽게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-346">It’s common to see filters that help you choose a store, restaurant, or destination based on its proximity to your current location.</span></span> <span data-ttu-id="d2a88-347">이 유형의 필터는 패싯 탐색처럼 보일 수 있지만 단순한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-347">While this type of filter might look like faceted navigation, it’s just a filter.</span></span> <span data-ttu-id="d2a88-348">특별히 이와 같은 특정 디자인 문제에 대한 구현 조언을 구하는 경우 이 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-348">We mention it here for those of you who are specifically looking for implementation advice for that particular design problem.</span></span>

<span data-ttu-id="d2a88-349">Azure Search에는 **geo.distance** 및 **geo.intersects**라는 두 개의 지리 공간 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-349">There are two Geospatial functions in Azure Search, **geo.distance** and **geo.intersects**.</span></span>

* <span data-ttu-id="d2a88-350">**geo.distance** 함수는 두 점 사이의 거리를 킬로미터 단위로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-350">The **geo.distance** function returns the distance in kilometers between two points.</span></span> <span data-ttu-id="d2a88-351">한 점은 필드이고 다른 점은 필터의 일부로 전달되는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-351">One point is a field and other is a constant passed as part of the filter.</span></span> 
* <span data-ttu-id="d2a88-352">**geo.intersects** 함수는 주어진 점이 주어진 다각형 내부에 있으면 true를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-352">The **geo.intersects** function returns true if a given point is within a given polygon.</span></span> <span data-ttu-id="d2a88-353">점은 필드이고, 다각형은 필터의 일부로 전달되는 좌표의 상수 목록으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-353">The point is a field and the polygon is specified as a constant list of coordinates passed as part of the filter.</span></span>

<span data-ttu-id="d2a88-354">필터 예제는 [OData 식 구문(Azure 검색)](http://msdn.microsoft.com/library/azure/dn798921.aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-354">You can find filter examples in [OData expression syntax (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).</span></span>

<a name="tryitout"></a>

## <a name="try-the-demo"></a><span data-ttu-id="d2a88-355">데모 사용해 보기</span><span class="sxs-lookup"><span data-stu-id="d2a88-355">Try the demo</span></span>
<span data-ttu-id="d2a88-356">Azure Search 구직 포털 데모에는 이 문서에 나와 있는 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-356">The Azure Search Job Portal Demo contains the examples referenced in this article.</span></span>

-   <span data-ttu-id="d2a88-357">[Azure Search 구직 포털 데모](http://azjobsdemo.azurewebsites.net/)에서 온라인으로 작업 데모를 살펴보고 테스트하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-357">See and test the working demo online at [Azure Search Job Portal Demo](http://azjobsdemo.azurewebsites.net/).</span></span>

-   <span data-ttu-id="d2a88-358">[GitHub의 Azure 샘플 리포지토리](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)에서 코드를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-358">Download the code from the [Azure-Samples repo on GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).</span></span>

<span data-ttu-id="d2a88-359">검색 결과로 작업할 때 쿼리 구문의 변경 내용에 대한 URL을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-359">As you work with search results, watch the URL for changes in query construction.</span></span> <span data-ttu-id="d2a88-360">이 응용 프로그램은 선택 시 URI에 패싯을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-360">This application happens to append facets to the URI as you select each one.</span></span>

1. <span data-ttu-id="d2a88-361">데모 앱의 매핑 기능을 사용하려면 [Bing Maps 개발자 센터](https://www.bingmapsportal.com/)에서 Bing Maps 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-361">To use the mapping functionality of the demo app, get a Bing Maps key from the [Bing Maps Dev Center](https://www.bingmapsportal.com/).</span></span> <span data-ttu-id="d2a88-362">가져온 키를 `index.cshtml` 페이지의 기존 키 위에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-362">Paste it over the existing key in the `index.cshtml` page.</span></span> <span data-ttu-id="d2a88-363">`Web.config` 파일의 `BingApiKey` 설정은 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-363">The `BingApiKey` setting in the `Web.config` file is not used.</span></span> 

2. <span data-ttu-id="d2a88-364">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-364">Run the application.</span></span> <span data-ttu-id="d2a88-365">원한다면 대화 상자를 둘러보고 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-365">Take the optional tour, or dismiss the dialog box.</span></span>
   
3. <span data-ttu-id="d2a88-366">"분석가" 등의 검색 용어를 입력하고 검색 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-366">Enter a search term, such as "analyst", and click the Search icon.</span></span> <span data-ttu-id="d2a88-367">쿼리가 신속하게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-367">The query executes quickly.</span></span>
   
   <span data-ttu-id="d2a88-368">검색 결과와 함께 패싯 탐색 구조도 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-368">A faceted navigation structure is also returned with the search results.</span></span> <span data-ttu-id="d2a88-369">검색 결과 페이지의 패싯 탐색 구조에 각 패싯 결과의 개수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-369">In the search result page, the faceted navigation structure includes counts for each facet result.</span></span> <span data-ttu-id="d2a88-370">패싯을 선택하지 않았으므로 일치하는 모든 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-370">No facets are selected, so all matching results are returned.</span></span>
   
   ![패싯을 선택하기 전의 검색 결과][11]

4. <span data-ttu-id="d2a88-372">직함, 위치 또는 최소 급여를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-372">Click a Business Title, Location, or Minimum Salary.</span></span> <span data-ttu-id="d2a88-373">패싯은 초기 검색 시 null이었지만 값을 취하는 순간 더 이상 일치하지 않는 항목이 검색 결과에서 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-373">Facets were null on the initial search, but as they take on values, the search results are trimmed of items that no longer match.</span></span>
   
   ![패싯을 선택한 후의 검색 결과][12]

5. <span data-ttu-id="d2a88-375">다른 쿼리 동작을 시도할 수 있도록 패싯 쿼리를 지우려면 선택한 패싯 뒤에 있는 `[X]`를 클릭하여 패싯을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-375">To clear the faceted query so that you can try different query behaviors, click the `[X]` after the selected facets to clear the facets.</span></span>
   
<a name="nextstep"></a>

## <a name="learn-more"></a><span data-ttu-id="d2a88-376">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d2a88-376">Learn more</span></span>
<span data-ttu-id="d2a88-377">[Azure Search 심층 정보](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="d2a88-377">Watch [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410).</span></span> <span data-ttu-id="d2a88-378">45분 25초 구간에 패싯을 구현하는 방법에 대한 데모가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-378">At 45:25, there is a demo on how to implement facets.</span></span>

<span data-ttu-id="d2a88-379">패싯 탐색의 디자인 원칙에 대한 자세한 내용은 다음 링크를 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2a88-379">For more insights on design principles for faceted navigation, we recommend the following links:</span></span>

* [<span data-ttu-id="d2a88-380">패싯 검색을 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="d2a88-380">Designing for Faceted Search</span></span>](http://www.uie.com/articles/faceted_search/)
* [<span data-ttu-id="d2a88-381">디자인 패턴: 패싯 탐색</span><span class="sxs-lookup"><span data-stu-id="d2a88-381">Design Patterns: Faceted Navigation</span></span>](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How to build it]: #howtobuildit
[Build the presentation layer]: #presentationlayer
[Build the index]: #buildindex
[Check for data quality]: #checkdata
[Build the query]: #buildquery
[Tips on how to control faceted navigation]: #tips
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

