---
title: "응용 프로그램 Insights 원격 분석 데이터 모델-aaaAzure 요청 원격 분석 | Microsoft Docs"
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
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a><span data-ttu-id="c3cfe-103">요청 원격 분석: Application Insights 데이터 모델</span><span class="sxs-lookup"><span data-stu-id="c3cfe-103">Request telemetry: Application Insights data model</span></span>

<span data-ttu-id="c3cfe-104">요청 원격 분석 항목 (에서 [Application Insights](app-insights-overview.md)) 외부 요청 tooyour 응용 프로그램에 의해 트리거되는 실행의 논리적 시퀀스를 hello 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-104">A request telemetry item (in [Application Insights](app-insights-overview.md)) represents hello logical sequence of execution triggered by an external request tooyour application.</span></span> <span data-ttu-id="c3cfe-105">모든 요청을 실행 고유으로 식별 되 `ID` 및 `url` 모든 hello 실행 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-105">Every request execution is identified by unique `ID` and `url` containing all hello execution parameters.</span></span> <span data-ttu-id="c3cfe-106">요청을 논리적으로 그룹화 수 `name` hello를 정의 하 고 `source` 이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-106">You can group requests by logical `name` and define hello `source` of this request.</span></span> <span data-ttu-id="c3cfe-107">코드 실행으로 `success` 또는 `fail`이 발생할 수 있으며 특정 `duration` 동안 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-107">Code execution can result in `success` or `fail` and has a certain `duration`.</span></span> <span data-ttu-id="c3cfe-108">success(성공) 및 failure(실패) 실행은 모두 `resultCode`별로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-108">Both success and failure executions may be grouped further by `resultCode`.</span></span> <span data-ttu-id="c3cfe-109">Hello 봉투 수준에 정의 된 hello 요청 원격 분석에 대 한 시간을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-109">Start time for hello request telemetry defined on hello envelope level.</span></span>

<span data-ttu-id="c3cfe-110">원격 분석을 사용자 지정을 사용 하 여 hello 표준 확장성 모델 지원 요청 `properties` 및 `measurements`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-110">Request telemetry supports hello standard extensibility model using custom `properties` and `measurements`.</span></span>

## <a name="name"></a><span data-ttu-id="c3cfe-111">이름</span><span class="sxs-lookup"><span data-stu-id="c3cfe-111">Name</span></span>

<span data-ttu-id="c3cfe-112">Hello 요청의 이름 코드 경로 tooprocess hello 요청을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-112">Name of hello request represents code path taken tooprocess hello request.</span></span> <span data-ttu-id="c3cfe-113">낮은 카디널리티 값 tooallow 더 잘 요청을 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-113">Low cardinality value tooallow better grouping of requests.</span></span> <span data-ttu-id="c3cfe-114">HTTP 메서드 및 URL 경로 템플릿을 나타내는 hello HTTP의 요청에 대 한 `GET /values/{id}` hello 실제 없이 `id` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-114">For HTTP requests it represents hello HTTP method and URL path template like `GET /values/{id}` without hello actual `id` value.</span></span>

<span data-ttu-id="c3cfe-115">응용 프로그램 Insights 웹 SDK에 대 한 예정 tooletter 사례와 요청 이름을 "있는 그대로"을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-115">Application Insights web SDK sends request name "as is" with regards tooletter case.</span></span> <span data-ttu-id="c3cfe-116">UI에 대 한 그룹화는 대/소문자 구분 하므로 `GET /Home/Index` 에서 개별적으로 계산 됩니다 `GET /home/INDEX` 종종 초래할 있습니다 hello 동일한 경우에 컨트롤러 및 작업 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-116">Grouping on UI is case-sensitive so `GET /Home/Index` is counted separately from `GET /home/INDEX` even though often they result in hello same controller and action execution.</span></span> <span data-ttu-id="c3cfe-117">hello 이유는 url 일반적은 [대/소문자 구분](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-117">hello reason for that is that urls in general are [case-sensitive](http://www.w3.org/TR/WD-html40-970708/htmlweb.html).</span></span> <span data-ttu-id="c3cfe-118">모든 toosee 경우가 `404` 대문자로 입력 된 hello url에 대해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-118">You may want toosee if all `404` happened for hello urls typed in uppercase.</span></span> <span data-ttu-id="c3cfe-119">더 많은 온 요청 이름 컬렉션에서 ASP.Net 웹 SDK hello에 읽을 수 [블로그 게시물](http://apmtips.com/blog/2015/02/23/request-name-and-url/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-119">You can read more on request name collection by ASP.Net Web SDK in hello [blog post](http://apmtips.com/blog/2015/02/23/request-name-and-url/).</span></span>

<span data-ttu-id="c3cfe-120">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="c3cfe-120">Max length: 1024 characters</span></span>

## <a name="id"></a><span data-ttu-id="c3cfe-121">ID</span><span class="sxs-lookup"><span data-stu-id="c3cfe-121">ID</span></span>

<span data-ttu-id="c3cfe-122">요청 호출 인스턴스의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-122">Identifier of a request call instance.</span></span> <span data-ttu-id="c3cfe-123">요청 및 기타 원격 분석 항목 간 상관 관계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-123">Used for correlation between request and other telemetry items.</span></span> <span data-ttu-id="c3cfe-124">ID는 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-124">ID should be globally unique.</span></span> <span data-ttu-id="c3cfe-125">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-125">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="c3cfe-126">최대 길이: 128자</span><span class="sxs-lookup"><span data-stu-id="c3cfe-126">Max length: 128 characters</span></span>

## <a name="url"></a><span data-ttu-id="c3cfe-127">Url</span><span class="sxs-lookup"><span data-stu-id="c3cfe-127">Url</span></span>

<span data-ttu-id="c3cfe-128">모든 쿼리 문자열 매개 변수를 사용하는 요청 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-128">Request URL with all query string parameters.</span></span>

<span data-ttu-id="c3cfe-129">최대 길이: 2048자</span><span class="sxs-lookup"><span data-stu-id="c3cfe-129">Max length: 2048 characters</span></span>

## <a name="source"></a><span data-ttu-id="c3cfe-130">원본</span><span class="sxs-lookup"><span data-stu-id="c3cfe-130">Source</span></span>

<span data-ttu-id="c3cfe-131">Hello 요청의 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-131">Source of hello request.</span></span> <span data-ttu-id="c3cfe-132">예제는 hello 호출자의 계측 키 hello 또는 hello 호출자의 hello ip 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-132">Examples are hello instrumentation key of hello caller or hello ip address of hello caller.</span></span> <span data-ttu-id="c3cfe-133">자세한 내용은 [상관 관계](application-insights-correlation.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-133">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

<span data-ttu-id="c3cfe-134">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="c3cfe-134">Max length: 1024 characters</span></span>

## <a name="duration"></a><span data-ttu-id="c3cfe-135">기간</span><span class="sxs-lookup"><span data-stu-id="c3cfe-135">Duration</span></span>

<span data-ttu-id="c3cfe-136">요청 기간은 `DD.HH:MM:SS.MMMMMM` 형식으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-136">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="c3cfe-137">`1000`일보다 작은 양수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-137">Must be positive and less than `1000` days.</span></span> <span data-ttu-id="c3cfe-138">이 필드는 요청 원격 분석 hello 처음과 hello와 hello 작업을 나타내는 대로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-138">This field is required as request telemetry represents hello operation with hello beginning and hello end.</span></span>

## <a name="response-code"></a><span data-ttu-id="c3cfe-139">응답 코드</span><span class="sxs-lookup"><span data-stu-id="c3cfe-139">Response code</span></span>

<span data-ttu-id="c3cfe-140">요청 실행의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-140">Result of a request execution.</span></span> <span data-ttu-id="c3cfe-141">HTTP 요청에 대한 HTTP 상태 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-141">HTTP status code for HTTP requests.</span></span> <span data-ttu-id="c3cfe-142">다른 요청 형식에 대한 `HRESULT` 값 또는 예외 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-142">It may be `HRESULT` value or exception type for other request types.</span></span>

<span data-ttu-id="c3cfe-143">최대 길이: 1024자</span><span class="sxs-lookup"><span data-stu-id="c3cfe-143">Max length: 1024 characters</span></span>

## <a name="success"></a><span data-ttu-id="c3cfe-144">성공</span><span class="sxs-lookup"><span data-stu-id="c3cfe-144">Success</span></span>

<span data-ttu-id="c3cfe-145">성공 또는 실패한 호출을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-145">Indication of successful or unsuccessful call.</span></span> <span data-ttu-id="c3cfe-146">이 필드는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-146">This field is required.</span></span> <span data-ttu-id="c3cfe-147">설정 되지 않은 경우 명시적으로 너무`false` -요청 toobe 성공한 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-147">When not set explicitly too`false` - request considered toobe successful.</span></span> <span data-ttu-id="c3cfe-148">이 값을 너무 설정`false` 작업 예외에 의해 중단 되었거나 오류 결과 코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-148">Set this value too`false` if operation was interrupted by exception or returned error result code.</span></span>

<span data-ttu-id="c3cfe-149">Hello 웹 응용 프로그램에 대 한 Application Insights 요청을 정의할 때 hello 응답 코드는 작은 hello 실패로 `400` 너무 크거나`401`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-149">For hello web applications, Application Insights define request as failed when hello response code is less hello `400` or equal too`401`.</span></span> <span data-ttu-id="c3cfe-150">그러나 다음과 같은 경우 기본 매핑을 hello hello 응용 프로그램의 의미 체계와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-150">However there are cases when this default mapping does not match hello semantic of hello application.</span></span> <span data-ttu-id="c3cfe-151">응답 코드 `404`는 정규 흐름의 일부일 수 있는 "기록 없음"을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-151">Response code `404` may indicate "no records", which can be part of regular flow.</span></span> <span data-ttu-id="c3cfe-152">또한 끊어진 연결을 나타낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-152">It also may indicate a broken link.</span></span> <span data-ttu-id="c3cfe-153">중단 된 링크 hello에 대 한 더 많은 고급 논리를 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-153">For hello broken links, you can even implement more advanced logic.</span></span> <span data-ttu-id="c3cfe-154">이러한 링크 hello 동일한 url 참조 페이지를 분석 하 여 사이트에 있는 경우에 실패로 끊어진된 링크를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-154">You can mark broken links as failures only when those links are located on hello same site by analyzing url referrer.</span></span> <span data-ttu-id="c3cfe-155">못하거나 hello 회사의 모바일 응용 프로그램에서 액세스할 때 실패로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-155">Or mark them as failures when accessed from hello company's mobile application.</span></span> <span data-ttu-id="c3cfe-156">마찬가지로 `301` 및 `302` 리디렉션을 지원 하지 않는 hello 클라이언트에서 액세스할 때 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-156">Similarly `301` and `302` indicates failure when accessed from hello client that doesn't support redirect.</span></span>

<span data-ttu-id="c3cfe-157">부분적으로 수락된 콘텐츠 `206`은 전체 요청의 실패를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-157">Partially accepted content `206` may indicate a failure of an overall request.</span></span> <span data-ttu-id="c3cfe-158">예를 들어 Application Insights 끝점은 원격 분석 항목의 일괄 처리를 단일 요청으로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-158">For instance, Application Insights endpoint receives a batch of telemetry items as a single request.</span></span> <span data-ttu-id="c3cfe-159">반환 `206` hello 일괄 처리의 일부 항목에 성공적으로 처리 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-159">It returns `206` when some items in hello batch were not processed successfully.</span></span> <span data-ttu-id="c3cfe-160">증가 속도 `206` toobe 조사 해야 하는 문제를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-160">Increasing rate of `206` indicates a problem that needs toobe investigated.</span></span> <span data-ttu-id="c3cfe-161">도 비슷한 논리가 적용 너무`207` hello 성공 수 있는 여러 상태에는 별도 응답 코드의 최저 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-161">Similar logic applies too`207` Multi-Status where hello success may be hello worst of separate response codes.</span></span>

<span data-ttu-id="c3cfe-162">더 많은 온 요청 결과 읽을 수에서 코드 및 상태 코드 hello [블로그 게시물](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-162">You can read more on request result code and status code in hello [blog post](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).</span></span>

## <a name="custom-properties"></a><span data-ttu-id="c3cfe-163">사용자 지정 속성</span><span class="sxs-lookup"><span data-stu-id="c3cfe-163">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="c3cfe-164">사용자 지정 측정</span><span class="sxs-lookup"><span data-stu-id="c3cfe-164">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="c3cfe-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3cfe-165">Next steps</span></span>

- <span data-ttu-id="c3cfe-166">[사용자 지정 요청 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="c3cfe-166">[Write custom request telemetry](app-insights-api-custom-events-metrics.md#trackrequest)</span></span>
- <span data-ttu-id="c3cfe-167">Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-167">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="c3cfe-168">너무 방법에 대해 알아봅니다[ASP.NET Core 구성](app-insights-asp-net.md) Application Insights로 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-168">Learn how too[configure ASP.NET Core](app-insights-asp-net.md) application with Application Insights.</span></span>
- <span data-ttu-id="c3cfe-169">Application Insights에서 지원되는 [플랫폼](app-insights-platforms.md)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3cfe-169">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
