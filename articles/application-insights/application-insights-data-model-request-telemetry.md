---
title: "Azure Application Insights 원격 분석 데이터 모델 - 요청 원격 분석 | Microsoft Docs"
description: "요청 원격 분석을 위한 Azure Application Insights 데이터 모델"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 8e782e45b706cadec66e7404dd9abc2e01dea917
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="request-telemetry-application-insights-data-model"></a><span data-ttu-id="ad00f-103">요청 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="ad00f-103">Request telemetry: Application Insights data model</span></span>

<span data-ttu-id="ad00f-104">[Application Insights](app-insights-overview.md)에서 요청 원격 분석 항목은 응용 프로그램에 대한 외부 요청으로 트리거되는 실행의 논리적 순서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents the logical sequence of execution triggered by an external request to your application.</span></span> <span data-ttu-id="ad00f-105">모든 요청 실행은 모든 실행 매개 변수를 포함하는 고유한 `ID` 및 `url`로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-105">Every request execution is identified by unique `ID` and `url` containing all the execution parameters.</span></span> <span data-ttu-id="ad00f-106">논리적 `name`으로 요청을 그룹화하고 이 요청의 `source`를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-106">You can group requests by logical `name` and define the `source` of this request.</span></span> <span data-ttu-id="ad00f-107">코드 실행으로 `success` 또는 `fail`이 발생할 수 있으며 특정 `duration` 동안 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span></span> <span data-ttu-id="ad00f-108">success(성공) 및 failure(실패) 실행은 모두 `resultCode`별로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-108">Both success and failure executions may be grouped further by `resultCode`.</span></span> <span data-ttu-id="ad00f-109">봉투 (envelope) 수준에 정의된 요청 원격 분석의 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-109">Start time for the request telemetry defined on the envelope level.</span></span>

<span data-ttu-id="ad00f-110">요청 원격 분석은 사용자 지정 `properties` 및 `measurements`를 사용하여 표준 확장성 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-110">Request telemetry supports the standard extensibility model using custom `properties` and `measurements`.</span></span>

## <a name="name"></a><span data-ttu-id="ad00f-111">이름</span><span class="sxs-lookup"><span data-stu-id="ad00f-111">Name</span></span>

<span data-ttu-id="ad00f-112">요청의 이름은 요청을 처리하기 위해 진행된 코드 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-112">Name of the request represents code path taken to process the request.</span></span> <span data-ttu-id="ad00f-113">더 나은 요청 그룹화를 허용하는 낮은 카디널리티 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-113">Low cardinality value to allow better grouping of requests.</span></span> <span data-ttu-id="ad00f-114">HTTP 요청의 경우 HTTP 메서드 및 실제 `id` 값이 없는 `GET /values/{id}`와 같은 URL 경로 템플릿을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-114">For HTTP requests it represents the HTTP method and URL path template like `GET /values/{id}` without the actual `id` value.</span></span>

<span data-ttu-id="ad00f-115">Application Insights 웹 SDK는 요청 이름을 대/소문자를 바꾸지 않고 “있는 그대로” 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-115">Application Insights web SDK sends request name "as is" with regards to letter case.</span></span> <span data-ttu-id="ad00f-116">UI의 그룹화는 대/소문자를 구분하므로 `GET /Home/Index`와 `GET /home/INDEX`는 동일한 컨트롤러 및 작업 실행을 발생하더라도 다른 것으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in the same controller and action execution.</span></span> <span data-ttu-id="ad00f-117">그 이유는 URL이 일반적으로 [대/소문자를 구분](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-117">The reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span></span> <span data-ttu-id="ad00f-118">대문자로 입력한 URL에 대해 `404`가 항상 발생하는지 확인하고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-118">You may want to see if all `404` happened for the urls typed in uppercase.</span></span> <span data-ttu-id="ad00f-119">[블로그 게시물](http://apmtips.com/blog/2015/02/23/request-name-and-url/)에서 ASP.Net 웹 SDK의 요청 이름 컬렉션에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-119">You can read more on request name collection by ASP.Net Web SDK in the [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span></span>

<span data-ttu-id="ad00f-120">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="ad00f-120">Max length: 1024 characters</span></span>

## <a name="id"></a><span data-ttu-id="ad00f-121">ID</span><span class="sxs-lookup"><span data-stu-id="ad00f-121">ID</span></span>

<span data-ttu-id="ad00f-122">요청 호출 인스턴스의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-122">Identifier of a request call instance.</span></span> <span data-ttu-id="ad00f-123">요청 및 기타 원격 분석 항목 간 상관 관계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-123">Used for correlation between request and other telemetry items.</span></span> <span data-ttu-id="ad00f-124">ID는 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-124">ID should be globally unique.</span></span> <span data-ttu-id="ad00f-125">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad00f-125">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="ad00f-126">최대 길이: 128자</span><span class="sxs-lookup"><span data-stu-id="ad00f-126">Max length: 128 characters</span></span>

## <a name="url"></a><span data-ttu-id="ad00f-127">Url</span><span class="sxs-lookup"><span data-stu-id="ad00f-127">Url</span></span>

<span data-ttu-id="ad00f-128">모든 쿼리 문자열 매개 변수를 사용하는 요청 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-128">Request URL with all query string parameters.</span></span>

<span data-ttu-id="ad00f-129">최대 길이: 2048자</span><span class="sxs-lookup"><span data-stu-id="ad00f-129">Max length: 2048 characters</span></span>

## <a name="source"></a><span data-ttu-id="ad00f-130">원본</span><span class="sxs-lookup"><span data-stu-id="ad00f-130">Source</span></span>

<span data-ttu-id="ad00f-131">요청의 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-131">Source of the request.</span></span> <span data-ttu-id="ad00f-132">호출자의 계측 키 또는 호출자의 IP 주소를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-132">Examples are the instrumentation key of the caller or the ip address of the caller.</span></span> <span data-ttu-id="ad00f-133">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad00f-133">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="ad00f-134">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="ad00f-134">Max length: 1024 characters</span></span>

## <a name="duration"></a><span data-ttu-id="ad00f-135">기간</span><span class="sxs-lookup"><span data-stu-id="ad00f-135">Duration</span></span>

<span data-ttu-id="ad00f-136">요청 기간은 `DD.HH:MM:SS.MMMMMM` 형식으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="ad00f-137">`1000`일보다 작은 양수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-137">Must be positive and less than `1000` days.</span></span> <span data-ttu-id="ad00f-138">요청 원격 분석은 처음과 끝이 있는 작업을 나타내므로 이 필드는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-138">This field is required as request telemetry represents the operation with the beginning and the end.</span></span>

## <a name="response-code"></a><span data-ttu-id="ad00f-139">응답 코드</span><span class="sxs-lookup"><span data-stu-id="ad00f-139">Response code</span></span>

<span data-ttu-id="ad00f-140">요청 실행의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-140">Result of a request execution.</span></span> <span data-ttu-id="ad00f-141">HTTP 요청에 대한 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-141">HTTP status code for HTTP requests.</span></span> <span data-ttu-id="ad00f-142">다른 요청 형식에 대한 `HRESULT` 값 또는 예외 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-142">It may be `HRESULT` value or exception type for other request types.</span></span>

<span data-ttu-id="ad00f-143">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="ad00f-143">Max length: 1024 characters</span></span>

## <a name="success"></a><span data-ttu-id="ad00f-144">성공</span><span class="sxs-lookup"><span data-stu-id="ad00f-144">Success</span></span>

<span data-ttu-id="ad00f-145">성공 또는 실패한 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-145">Indication of successful or unsuccessful call.</span></span> <span data-ttu-id="ad00f-146">이 필드는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-146">This field is required.</span></span> <span data-ttu-id="ad00f-147">명시적으로 `false`로 설정되지 않은 경우 - 요청이 성공으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-147">When not set explicitly to `false` - request considered to be successful.</span></span> <span data-ttu-id="ad00f-148">작업이 예외에 의해 중단되었거나 오류 결과 코드를 반환한 경우 이 값을 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-148">Set this value to `false` if operation was interrupted by exception or returned error result code.</span></span>

<span data-ttu-id="ad00f-149">웹 응용 프로그램의 경우 응답 코드가 `400`보다 작거나 `401`과 같은 경우 Application Insights는 요청을 실패한 것으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-149">For the web applications, Application Insights define request as failed when the response code is less the `400` or equal to `401`.</span></span> <span data-ttu-id="ad00f-150">그러나 기본 매핑이 응용 프로그램의 의미 체계와 일치하지 않는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-150">However there are cases when this default mapping does not match the semantic of the application.</span></span> <span data-ttu-id="ad00f-151">응답 코드 `404`는 정규 흐름의 일부일 수 있는 "기록 없음"을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-151">Response code `404` may indicate "no records", which can be part of regular flow.</span></span> <span data-ttu-id="ad00f-152">또한 끊어진 연결을 나타낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-152">It also may indicate a broken link.</span></span> <span data-ttu-id="ad00f-153">끊어진 연결의 경우 좀 더 고급 논리를 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-153">For the broken links, you can even implement more advanced logic.</span></span> <span data-ttu-id="ad00f-154">끊어진 연결이 동일한 사이트에 있는 경우에만 URL 참조를 분석하여 실패로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-154">You can mark broken links as failures only when those links are located on the same site by analyzing url referrer.</span></span> <span data-ttu-id="ad00f-155">또는 회사의 모바일 응용 프로그램에서 액세스할 때 실패로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-155">Or mark them as failures when accessed from the company's mobile application.</span></span> <span data-ttu-id="ad00f-156">마찬가지로 `301` 및 `302`는 리디렉션을 지원하지 않는 클라이언트에서 액세스될 때 실패를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-156">Similarly `301` and `302` indicates failure when accessed from the client that doesn't support redirect.</span></span>

<span data-ttu-id="ad00f-157">부분적으로 수락된 콘텐츠 `206`은 전체 요청의 실패를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-157">Partially accepted content `206` may indicate a failure of an overall request.</span></span> <span data-ttu-id="ad00f-158">예를 들어 Application Insights 끝점은 원격 분석 항목의 일괄 처리를 단일 요청으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span></span> <span data-ttu-id="ad00f-159">일괄 처리의 일부 항목이 성공적으로 처리되지 않으면 `206`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-159">It returns `206` when some items in the batch were not processed successfully.</span></span> <span data-ttu-id="ad00f-160">`206` 비율이 늘어나면 조사해야 하는 문제가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-160">Increasing rate of `206` indicates a problem that needs to be investigated.</span></span> <span data-ttu-id="ad00f-161">성공이 별도 응답 코드 측면에서는 더 나쁠 수 있는 `207` 다중 상태에도 유사한 논리가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-161">Similar logic applies to `207` Multi-Status where the success may be the worst of separate response codes.</span></span>

<span data-ttu-id="ad00f-162">[블로그 게시물](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/)에서 요청 결과 코드 및 상태 코드에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-162">You can read more on request result code and status code in the [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span></span>

## <a name="custom-properties"></a><span data-ttu-id="ad00f-163">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="ad00f-163">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="ad00f-164">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="ad00f-164">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="ad00f-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad00f-165">Next steps</span></span>

- <span data-ttu-id="ad00f-166">[사용자 지정 요청 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="ad00f-166">[Write custom request telemetry](app-insights-api-custom-events-metrics.md#trackrequest)</span></span>
- <span data-ttu-id="ad00f-167">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad00f-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="ad00f-168">자세한 방법 Application Insights를 사용하여 [ASP.NET Core 응용 프로그램을 구성](app-insights-asp-net.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-168">Learn how to [configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span></span>
- <span data-ttu-id="ad00f-169">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad00f-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
