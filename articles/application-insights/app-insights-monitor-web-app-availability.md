---
title: "aaaMonitor 가용성 및 응답성 모든 웹 사이트 | Microsoft Docs"
description: "Application Insights에서 웹 테스트를 설정합니다. 웹 사이트가 사용할 수 없게 되거나 느리게 응답하는 경우 알림이 제공됩니다."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="8ce8b-104">웹 사이트의 가용성 및 응답성 모니터링</span><span class="sxs-lookup"><span data-stu-id="8ce8b-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="8ce8b-105">웹 앱 또는 웹 사이트 tooany 서버 배포 후의 가용성 및 응답성 테스트 toomonitor를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-105">After you've deployed your web app or web site tooany server, you can set up tests toomonitor its availability and responsiveness.</span></span> <span data-ttu-id="8ce8b-106">[Azure Application Insights](app-insights-overview.md) 웹 요청 tooyour 응용 프로그램 일정 한 간격에서 전송 하는 hello world 중심으로 점을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-106">[Azure Application Insights](app-insights-overview.md) sends web requests tooyour application at regular intervals from points around hello world.</span></span> <span data-ttu-id="8ce8b-107">응용 프로그램이 응답하지 않거나 느리게 응답하는 경우 사용자에게 경고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="8ce8b-108">모든 HTTP에 대 한 가용성 테스트를 설정할 수 있습니다 또는 HTTPS 끝점에서 액세스할 수 있는 공용 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from hello public internet.</span></span> <span data-ttu-id="8ce8b-109">없는 tooadd 어느 것에 toohello 웹 사이트를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-109">You don't have tooadd anything toohello web site you're testing.</span></span> <span data-ttu-id="8ce8b-110">도 없는 toobe 사이트: 하면 종속 된 REST API 서비스를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-110">It doesn't even have toobe your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="8ce8b-111">가용성 테스트는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="8ce8b-112">[URL ping 테스트](#create): hello Azure 포털에서에서 만들 수 있는 간단 하 게 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-112">[URL ping test](#create): a simple test that you can create in hello Azure portal.</span></span>
* <span data-ttu-id="8ce8b-113">[Multi-step 웹 테스트](#multi-step-web-tests): Visual Studio Enterprise 및 업로드 toohello 포털에서 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload toohello portal.</span></span>

<span data-ttu-id="8ce8b-114">응용 프로그램 리소스 당 too25 가용성 테스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-114">You can create up too25 availability tests per application resource.</span></span>

## <span data-ttu-id="8ce8b-115"><a name="create"></a>1. 가용성 테스트 보고서에 대한 리소스 열기</span><span class="sxs-lookup"><span data-stu-id="8ce8b-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="8ce8b-116">**Application Insights를 이미 구성한 경우** 웹 앱에 대 한 hello에 Application Insights 리소스를 열고 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8ce8b-117">**또는 toosee 새 리소스에서 보고서를 원하는 경우** 너무 등록[Microsoft Azure](http://azure.com), toohello 이동 [Azure 포털](https://portal.azure.com), Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-117">**Or, if you want toosee your reports in a new resource,** sign up too[Microsoft Azure](http://azure.com), go toohello [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![새로 만들기 > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="8ce8b-119">클릭 **모든 리소스** tooopen hello 개요 블레이드에 hello 새 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-119">Click **All resources** tooopen hello Overview blade for hello new resource.</span></span>

## <span data-ttu-id="8ce8b-120"><a name="setup"></a>2. URL ping 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="8ce8b-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="8ce8b-121">Hello 가용성 블레이드를 열고 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-121">Open hello Availability blade and add a test.</span></span>

![채우기 이상 웹 사이트의 URL을 hello](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="8ce8b-123">**hello URL** 모든 웹 페이지 수, tootest 싶지만에서 표시 되어야 합니다 공용 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-123">**hello URL** can be any web page you want tootest, but it must be visible from hello public internet.</span></span> <span data-ttu-id="8ce8b-124">hello URL 쿼리 문자열을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-124">hello URL can include a query string.</span></span> <span data-ttu-id="8ce8b-125">따라서 데이터베이스 사용 등을 연습해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="8ce8b-126">Hello URL tooa 리디렉션 확인 되 면 too10 리디렉션을 추가 작업 했습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-126">If hello URL resolves tooa redirect, we follow it up too10 redirects.</span></span>
* <span data-ttu-id="8ce8b-127">**종속 요청을 구문 분석**:이 옵션을 선택 하는 경우 이미지, 스크립트, 스타일의 파일 및 기타 파일을 테스트 중인 hello 웹 페이지의 일부 hello 테스트를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-127">**Parse dependent requests**: If this option is checked, hello test requests images, scripts, style files, and other files that are part of hello web page under test.</span></span> <span data-ttu-id="8ce8b-128">hello 기록 된 응답 시간 hello에 걸린 시간 tooget 이러한 파일 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-128">hello recorded response time includes hello time taken tooget these files.</span></span> <span data-ttu-id="8ce8b-129">hello 테스트가 hello 전체 테스트에 대 한 hello 시간 제한 내에서 이러한 모든 리소스를 성공적으로 다운로드할 수 없는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-129">hello test fails if all these resources cannot be successfully downloaded within hello timeout for hello whole test.</span></span> 

    <span data-ttu-id="8ce8b-130">Hello 옵션을 선택 하지 않으면 hello 테스트 hello 파일에서 지정한 hello URL만 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-130">If hello option is not checked, hello test only requests hello file at hello URL you specified.</span></span>
* <span data-ttu-id="8ce8b-131">**다시 시도 횟수를 사용 하도록 설정**: 짧은 간격 후에 다시 시도 됩니다 hello 테스트가 실패 하는 경우이 옵션을 선택 하면, 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-131">**Enable retries**:  If this option is checked, when hello test fails, it is retried after a short interval.</span></span> <span data-ttu-id="8ce8b-132">연속 된 세 번의 시도가 실패하는 경우에 실패가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="8ce8b-133">그런 다음 후속 테스트 hello 일반적인 테스트 빈도로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-133">Subsequent tests are then performed at hello usual test frequency.</span></span> <span data-ttu-id="8ce8b-134">다시 시도 hello 다음 성공할 때까지 일시적으로 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-134">Retry is temporarily suspended until hello next success.</span></span> <span data-ttu-id="8ce8b-135">이 규칙은 각 테스트 위치에서 독립적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="8ce8b-136">이 옵션을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-136">We recommend this option.</span></span> <span data-ttu-id="8ce8b-137">평균 실패의 약 80%는 다시 시도에서 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="8ce8b-138">**테스트 빈도**: 얼마나 자주 hello 테스트를 실행 각 테스트 위치에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-138">**Test frequency**: Sets how often hello test is run from each test location.</span></span> <span data-ttu-id="8ce8b-139">5분에 5번의 테스트를 하는 빈도로 사이트를 평균 1분마다 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="8ce8b-140">**테스트 위치** hello 웹 요청 tooyour URL 보낼 하는 서버에서 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-140">**Test locations** are hello places from where our servers send web requests tooyour URL.</span></span> <span data-ttu-id="8ce8b-141">웹 사이트의 문제와 네트워크 문제를 구분할 수 있도록 한 가지 이상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="8ce8b-142">Too16 위치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-142">You can select up too16 locations.</span></span>
* <span data-ttu-id="8ce8b-143">**성공 조건**:</span><span class="sxs-lookup"><span data-stu-id="8ce8b-143">**Success criteria**:</span></span>

    <span data-ttu-id="8ce8b-144">**테스트 시간 제한**: 느린 응답에 대 한 경고를 발생 시킬 값 toobe이 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-144">**Test timeout**: Decrease this value toobe alerted about slow responses.</span></span> <span data-ttu-id="8ce8b-145">이 기간 내 사이트의 hello 응답을 받지 못했습니다 경우 hello 테스트를 실패로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-145">hello test is counted as a failure if hello responses from your site have not been received within this period.</span></span> <span data-ttu-id="8ce8b-146">선택한 경우 **종속 요청을 구문 분석**, 이미지, 스타일의 파일, 스크립트, 모든 hello 다음 및 다른 종속 된 리소스도이 기간 내에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-146">If you selected **Parse dependent requests**, then all hello images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="8ce8b-147">**HTTP 응답**: hello를 성공으로 계산 하는 상태 코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-147">**HTTP response**: hello returned status code that is counted as a success.</span></span> <span data-ttu-id="8ce8b-148">200은 일반적인 웹 페이지 반환 되었습니다. 나타내는 hello 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-148">200 is hello code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="8ce8b-149">"Welcome!"과 같은 **콘텐츠 일치** 문자열.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="8ce8b-150">정확한 대/소문자 구분 일치가 모든 응답에서 발생하는지 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="8ce8b-151">와일드카드 없는 일반 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="8ce8b-152">Tooupdate 해야할 페이지 콘텐츠 변경 내용이 되는 경우 반드시 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-152">Don't forget that if your page content changes you might have tooupdate it.</span></span>
* <span data-ttu-id="8ce8b-153">**경고** 인 기본적으로 tooyou 경우 전송 오류가 발생 하는 세 위치 (5 분)입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-153">**Alerts** are, by default, sent tooyou if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="8ce8b-154">실패 한 위치에서 네트워크 문제일 가능성이 toobe 이며 사이트와 문제가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-154">A failure in one location is likely toobe a network problem, and not a problem with your site.</span></span> <span data-ttu-id="8ce8b-155">하지만 더 많은 hello 임계값 toobe 변경할 수 있습니다 또는 중요 하 고 덜 수 hello 전자 메일 사용자를 변경 해야 보낼 수를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-155">But you can change hello threshold toobe more or less sensitive, and you can also change who hello emails should be sent to.</span></span>

    <span data-ttu-id="8ce8b-156">경고가 발생하면 호출되는 [웹후크](../monitoring-and-diagnostics/insights-webhooks-alerts.md)를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="8ce8b-157">그러나 현재 쿼리 매개 변수는 속성으로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="8ce8b-158">더 많은 URL 테스트</span><span class="sxs-lookup"><span data-stu-id="8ce8b-158">Test more URLs</span></span>
<span data-ttu-id="8ce8b-159">테스트를 더 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-159">Add more tests.</span></span> <span data-ttu-id="8ce8b-160">예를 들어 더하기 tootesting 홈 페이지에 있습니다 되었는지 확인할 수 검색에 대 한 hello URL을 테스트 하 여 데이터베이스를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-160">For example, In addition tootesting your home page, you can make sure your database is running by testing hello URL for a search.</span></span>


## <span data-ttu-id="8ce8b-161"><a name="monitor"></a>3. 가용성 테스트 결과 참조</span><span class="sxs-lookup"><span data-stu-id="8ce8b-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="8ce8b-162">몇 분 후 클릭 **새로 고침** toosee 테스트 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-162">After a few minutes, click **Refresh** toosee test results.</span></span> 

![Hello 홈 블레이드의 요약 결과](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="8ce8b-164">hello scatterplot hello의 샘플 진단 테스트 단계 세부 개 테스트 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-164">hello scatterplot shows samples of hello test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="8ce8b-165">hello 테스트 엔진 오류가 발생 한 테스트에 대 한 진단 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-165">hello test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="8ce8b-166">성공적인 테스트에 대 한 hello 실행의 하위 집합에 대 한 진단 세부 정보가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-166">For successful tests, diagnostic details are stored for a subset of hello executions.</span></span> <span data-ttu-id="8ce8b-167">Hello 녹색/빨간색 점 toosee hello 테스트 타임 스탬프, 테스트 지속 시간, 위치 및 테스트 이름 위로 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-167">Hover over any of hello green/red dots toosee hello test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="8ce8b-168">Hello 산 점도 toosee hello 결과의 세부 정보 hello 테스트에서에서 모든 점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-168">Click through any dot in hello scatter plot toosee hello details of hello test result.</span></span>  

<span data-ttu-id="8ce8b-169">특정 테스트, 위치를 선택 하거나 hello 시간 기간 toosee 더 결과 hello 주위 관심 있는 기간을 단축 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-169">Select a particular test, location, or reduce hello time period toosee more results around hello time period of interest.</span></span> <span data-ttu-id="8ce8b-170">탐색기 검색 toosee 결과 모든 실행에서 사용 하거나이 데이터에 분석 쿼리 toorun 사용자 지정 보고서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-170">Use Search Explorer toosee results from all executions, or use Analytics queries toorun custom reports on this data.</span></span>

<span data-ttu-id="8ce8b-171">또한 toohello 원시 결과에 두 가지 가용성 메트릭이 있습니다 메트릭 탐색기에서:</span><span class="sxs-lookup"><span data-stu-id="8ce8b-171">In addition toohello raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="8ce8b-172">모든 테스트 실행에서 성공 했 hello 테스트의 사용 가능성: 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-172">Availability: Percentage of hello tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="8ce8b-173">테스트 지속 시간: 모든 테스트 실행에서의 평균 테스트 지속 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="8ce8b-174">Hello 테스트 이름, 위치 tooanalyze 추세는 특정 테스트 및/또는 위치에 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-174">You can apply filters on hello test name, location tooanalyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="8ce8b-175"><a name="edit"></a>테스트 검사 및 편집</span><span class="sxs-lookup"><span data-stu-id="8ce8b-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="8ce8b-176">Hello 요약 페이지에서 특정 테스트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-176">From hello summary page, select a specific test.</span></span> <span data-ttu-id="8ce8b-177">거기에서 해당 특정 결과를 확인하고 편집하거나 일시적으로 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![웹 테스트 편집 또는 사용 안 함](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="8ce8b-179">서비스에서 유지 관리를 수행 하는 동안 규칙 관련 된 hello 경고 또는 toodisable 가용성 테스트를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-179">You might want toodisable availability tests or hello alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="8ce8b-180"><a name="failures"></a>오류가 표시되는 경우</span><span class="sxs-lookup"><span data-stu-id="8ce8b-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="8ce8b-181">빨간 점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-181">Click a red dot.</span></span>

![빨간 점을 클릭 합니다.](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="8ce8b-183">가용성 테스트 결과에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="8ce8b-184">서버에서 받은 hello 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-184">Inspect hello response received from your server.</span></span>
* <span data-ttu-id="8ce8b-185">Hello 실패 한 요청 인스턴스를 처리 하는 동안 서버 응용 프로그램에서 보낸 hello 원격 분석을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-185">Open hello telemetry sent by your server app while processing hello failed request instance.</span></span>
* <span data-ttu-id="8ce8b-186">Git 또는 VSTS tootrack hello 문제에서 작업 항목 하거나 문제를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-186">Log an issue or work item in Git or VSTS tootrack hello problem.</span></span> <span data-ttu-id="8ce8b-187">hello 버그 링크 toothis 이벤트를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-187">hello bug will contain a link toothis event.</span></span>
* <span data-ttu-id="8ce8b-188">Visual Studio에서 hello 웹 테스트 결과를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-188">Open hello web test result in Visual Studio.</span></span>


<span data-ttu-id="8ce8b-189">*정상으로 보이지만 실패로 보고되었습니까?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="8ce8b-190">모든 hello 이미지, 스크립트, 스타일 시트 및 hello 페이지에 의해 로드 하는 다른 모든 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-190">Check all hello images, scripts, style sheets, and any other files loaded by hello page.</span></span> <span data-ttu-id="8ce8b-191">그 중 하나라도 실패 하면 hello 테스트 보고 되며 실패 한 hello 기본 html 페이지 확인을 로드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-191">If any of them fails, hello test is reported as failed, even if hello main html page loads OK.</span></span>

<span data-ttu-id="8ce8b-192">*관련 항목이 없나요?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-192">*No related items?*</span></span> <span data-ttu-id="8ce8b-193">서버 쪽 응용 프로그램에 대해 Application Insights를 설정한 경우, [샘플링](app-insights-sampling.md)이 작동 중이기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="8ce8b-194">다중 단계 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="8ce8b-194">Multi-step web tests</span></span>
<span data-ttu-id="8ce8b-195">URL 시퀀스를 포함하는 시나리오를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="8ce8b-196">예를 들어 판매 웹 사이트를 모니터링 하는 경우 추가 항목 toohello 쇼핑 카트 제대로 작동 하는지 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-196">For example, if you are monitoring a sales website, you can test that adding items toohello shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ce8b-197">다단계 웹 테스트에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="8ce8b-198">[가격 체계](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="8ce8b-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="8ce8b-199">toocreate multi-step 테스트를 Visual Studio Enterprise를 사용 하 여 hello 시나리오 기록 한 다음 업로드할 있습니다 hello tooApplication 통찰력을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-199">toocreate a multi-step test, you record hello scenario by using Visual Studio Enterprise, and then upload hello recording tooApplication Insights.</span></span> <span data-ttu-id="8ce8b-200">Application Insights 간격 hello 시나리오를 재생 하 고 hello 응답을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-200">Application Insights replays hello scenario at intervals and verifies hello responses.</span></span>

> [!NOTE]
> <span data-ttu-id="8ce8b-201">테스트에서 코딩된 함수 또는 루프를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="8ce8b-202">hello 테스트 hello.webtest 스크립트에 완전히 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-202">hello test must be contained completely in hello .webtest script.</span></span> <span data-ttu-id="8ce8b-203">그러나 표준 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="8ce8b-204">1. 시나리오 기록</span><span class="sxs-lookup"><span data-stu-id="8ce8b-204">1. Record a scenario</span></span>
<span data-ttu-id="8ce8b-205">Visual Studio Enterprise를 사용 하 여 웹 세션 toorecord 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-205">Use Visual Studio Enterprise toorecord a web session.</span></span>

1. <span data-ttu-id="8ce8b-206">웹 성능 테스트 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-206">Create a Web performance test project.</span></span>

    ![Visual Studio Enterprise edition에서 hello 웹 성능 및 부하 테스트 템플릿에서 프로젝트를 만듭니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="8ce8b-208">*Hello 웹 성능 및 부하 테스트 템플릿이 보이지 않으세요?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-208">*Don't see hello Web Performance and Load Test template?*</span></span> <span data-ttu-id="8ce8b-209">- Visual Studio Enterprise를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="8ce8b-210">열기 **Visual Studio 설치 관리자** toomodify Visual Studio Enterprise 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-210">Open **Visual Studio Installer** toomodify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="8ce8b-211">**개별 구성 요소** 아래에서 **웹 성능 및 부하 테스트 도구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="8ce8b-212">Hello.webtest 파일을 열고 기록을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-212">Open hello .webtest file and start recording.</span></span>

    ![Hello.webtest 파일을 열고 레코드를 클릭 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="8ce8b-214">사용자 작업 toosimulate 테스트에서 원하는 hello지 않습니다: 웹 사이트를 열고, 추가 제품 toohello 카트 등입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-214">Do hello user actions you want toosimulate in your test: open your website, add a product toohello cart, and so on.</span></span> <span data-ttu-id="8ce8b-215">테스트를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-215">Then stop your test.</span></span>

    ![hello 웹 테스트 레코더 실행 Internet Explorer에서 사용 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="8ce8b-217">시나리오를 길게 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-217">Don't make a long scenario.</span></span> <span data-ttu-id="8ce8b-218">100개 단계와 2 분으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="8ce8b-219">Hello 테스트를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-219">Edit hello test to:</span></span>

   * <span data-ttu-id="8ce8b-220">유효성 검사 toocheck 받은 hello 텍스트 및 응답 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-220">Add validations toocheck hello received text and response codes.</span></span>
   * <span data-ttu-id="8ce8b-221">불필요한 상호 작용을 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="8ce8b-222">또한 그림 또는 tooad 또는 사이트를 추적에 대 한 종속 요청을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-222">You could also remove dependent requests for pictures or tooad or tracking sites.</span></span>

     <span data-ttu-id="8ce8b-223">Hello 테스트 스크립트 편집할 수 있습니다-사용자 지정 코드를 추가 하거나 다른 웹 테스트를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-223">Remember that you can only edit hello test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="8ce8b-224">Hello 테스트에 루프를 삽입 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-224">Don't insert loops in hello test.</span></span> <span data-ttu-id="8ce8b-225">표준 웹 테스트 플러그 인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="8ce8b-226">Visual Studio toomake 작동의 hello 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-226">Run hello test in Visual Studio toomake sure it works.</span></span>

    <span data-ttu-id="8ce8b-227">hello 웹 테스트 러너 웹 브라우저를 열고 반복 hello 기록한 작업.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-227">hello web test runner opens a web browser and repeats hello actions you recorded.</span></span> <span data-ttu-id="8ce8b-228">예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-228">Make sure it works as you expect.</span></span>

    ![Visual Studio에서 hello.webtest 파일을 열고 실행을 클릭 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a><span data-ttu-id="8ce8b-230">2. Hello 웹 테스트 tooApplication Insights 업로드</span><span class="sxs-lookup"><span data-stu-id="8ce8b-230">2. Upload hello web test tooApplication Insights</span></span>
1. <span data-ttu-id="8ce8b-231">Hello Application Insights 포털에서 웹 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-231">In hello Application Insights portal, create a web test.</span></span>

    ![Hello 웹 테스트 블레이드에서 추가 선택 합니다.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="8ce8b-233">여러 단계의 테스트를 선택 하 고 hello.webtest 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-233">Select multi-step test, and upload hello .webtest file.</span></span>

    ![다단계 웹 테스트를 선택합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="8ce8b-235">Hello 테스트 위치 설정, 빈도 및 경고 매개 변수 hello에 ping 용 방식으로 동일한 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-235">Set hello test locations, frequency, and alert parameters in hello same way as for ping tests.</span></span>

#### <a name="3-see-hello-results"></a><span data-ttu-id="8ce8b-236">3. Hello 결과 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-236">3. See hello results</span></span>

<span data-ttu-id="8ce8b-237">보고 테스트 결과 및 오류 hello 동일한 방식으로 단일 url 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-237">View your test results and any failures in hello same way as single-url tests.</span></span>

<span data-ttu-id="8ce8b-238">테스트 결과 tooview hello를 다운로드할 수는 또한 Visual Studio에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-238">In addition, you can download hello test results tooview them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="8ce8b-239">오류가 너무 많나요?</span><span class="sxs-lookup"><span data-stu-id="8ce8b-239">Too many failures?</span></span>

* <span data-ttu-id="8ce8b-240">실패에 대 한 일반적인 이유는 해당 hello 테스트 너무 오래 실행 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-240">A common reason for failure is that hello test runs too long.</span></span> <span data-ttu-id="8ce8b-241">2분 이내로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="8ce8b-242">반드시 hello 테스트 toosucceed, 스크립트, 스타일 시트, 이미지 등을 포함 하 여에 대 한 페이지의 모든 hello 리소스 올바르게 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-242">Don't forget that all hello resources of a page must load correctly for hello test toosucceed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="8ce8b-243">hello 웹 테스트 완전히에 포함 되어야 합니다 hello.webtest 스크립트: hello 테스트에 코딩 된 함수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-243">hello web test must be entirely contained in hello .webtest script: you can't use coded functions in hello test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="8ce8b-244">다단계 테스트에 시간 및 난수 연결</span><span class="sxs-lookup"><span data-stu-id="8ce8b-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="8ce8b-245">외부 피드에서 주식과 같이 시간에 따라 변하는 데이터를 가져오는 도구를 테스트한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="8ce8b-246">웹 테스트를 기록할 때 toouse 특정 시간 있지만 StartTime과 EndTime의 hello 매개 변수 테스트 설정.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-246">When you record your web test, you have toouse specific times, but you set them as parameters of hello test, StartTime and EndTime.</span></span>

![매개 변수를 가진 웹 테스트입니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="8ce8b-248">EndTime toobe hello 시간을 표시 하는 항상 원하는 StartTime 15 분 이어야 합니다 hello 테스트를 실행할 때 이전에 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-248">When you run hello test, you'd like EndTime always toobe hello present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="8ce8b-249">웹 테스트 플러그 인에 toodo 시간 매개 변수화 하는 hello 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-249">Web Test Plug-ins provide hello way toodo parameterize times.</span></span>

1. <span data-ttu-id="8ce8b-250">원하는 각 가변 매개 변수 값에 대한 웹 테스트 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="8ce8b-251">Hello 웹 테스트 도구 모음에서 선택 **웹 테스트 플러그 인 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-251">In hello web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![웹 테스트 플러그인 추가를 선택하고 형식을 선택합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="8ce8b-253">이 예에서는 날짜 시간 Plug-in hello의 두 인스턴스가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-253">In this example, we use two instances of hello Date Time Plug-in.</span></span> <span data-ttu-id="8ce8b-254">한 인스턴스는 "15분 전"이고 다른 하나는 "지금"입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="8ce8b-255">각 플러그 인의 hello 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-255">Open hello properties of each plug-in.</span></span> <span data-ttu-id="8ce8b-256">이름을 지정 하 고 현재 시간 toouse hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-256">Give it a name and set it toouse hello current time.</span></span> <span data-ttu-id="8ce8b-257">둘 중 하나에 대해 Add Minutes = -15를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-257">For one of them, set Add Minutes = -15.</span></span>

    ![이름을 설정하고, 현재 시간을 사용하며 시간을 추가합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="8ce8b-259">Hello 웹 테스트 매개 변수에서 {{name} 플러그 인} tooreference 플러그 인 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-259">In hello web test parameters, use {{plug-in name}} tooreference a plug-in name.</span></span>

    ![Hello 테스트 매개 변수, {{name} 플러그 인을 (를) 사용 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="8ce8b-261">이제 테스트 toohello 포털을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-261">Now, upload your test toohello portal.</span></span> <span data-ttu-id="8ce8b-262">Hello 테스트의 모든 실행에서 동적 값 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-262">It uses hello dynamic values on every run of hello test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="8ce8b-263">로그인 처리</span><span class="sxs-lookup"><span data-stu-id="8ce8b-263">Dealing with sign-in</span></span>
<span data-ttu-id="8ce8b-264">사용자가 tooyour 앱에 로그인 하는 경우 뒤에 hello 로그인 페이지를 테스트할 수 있도록 로그인 시뮬레이션 하는 데는 다양 한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-264">If your users sign in tooyour app, you have various options for simulating sign-in so that you can test pages behind hello sign-in.</span></span> <span data-ttu-id="8ce8b-265">사용 하는 hello 방법 hello 유형의 hello 응용 프로그램에서 제공 하는 보안에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-265">hello approach you use depends on hello type of security provided by hello app.</span></span>

<span data-ttu-id="8ce8b-266">모든 경우에만 테스트 목적 hello에 대 한 응용 프로그램에서 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-266">In all cases, you should create an account in your application just for hello purpose of testing.</span></span> <span data-ttu-id="8ce8b-267">가능 하면 두는 실제 사용자에 게 영향을 주는 hello 웹 테스트 가능성이 hello 계정의 권한으로이 테스트를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-267">If possible, restrict hello permissions of this test account so that there's no possibility of hello web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="8ce8b-268">간단한 사용자 이름 및 암호</span><span class="sxs-lookup"><span data-stu-id="8ce8b-268">Simple username and password</span></span>
<span data-ttu-id="8ce8b-269">Hello에서 웹 테스트를 기록 일반적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-269">Record a web test in hello usual way.</span></span> <span data-ttu-id="8ce8b-270">우선 쿠키를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="8ce8b-271">SAML 인정</span><span class="sxs-lookup"><span data-stu-id="8ce8b-271">SAML authentication</span></span>
<span data-ttu-id="8ce8b-272">웹 테스트에 사용할 수 있는 hello SAML 플러그 인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-272">Use hello SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="8ce8b-273">클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="8ce8b-273">Client secret</span></span>
<span data-ttu-id="8ce8b-274">앱에 클라이언트 암호를 포함하는 로그인 경로가 있는 경우 해당 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="8ce8b-275">AAD(Azure Active Directory)는 클라이언트 암호 로그인을 제공하는 서비스의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="8ce8b-276">AAD에서 hello 클라이언트 암호는 hello 앱 키입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-276">In AAD, hello client secret is hello App Key.</span></span>

<span data-ttu-id="8ce8b-277">앱 키를 사용하는 Azure 웹앱의 샘플 웹 테스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![클라이언트 암호 샘플](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="8ce8b-279">클라이언트 암호(AppKey)를 사용하여 AAD에서 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="8ce8b-280">응답에서 전달자 토큰을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="8ce8b-281">전달자 토큰을 사용 하 여 hello 인증 헤더에 API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-281">Call API using bearer token in hello authorization header.</span></span>

<span data-ttu-id="8ce8b-282">Hello 웹 테스트는 실제 클라이언트--AAD에서 자체 응용 프로그램 즉,에 있는지 확인 하 고 해당 clientId + appkey를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-282">Make sure that hello web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="8ce8b-283">테스트 대상 서비스에서 AAD 자체 응용 프로그램을 갖도록: hello appID이 응용이 프로그램의 URI는 hello "resource" 필드에 hello 웹 테스트에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-283">Your service under test also has its own app in AAD: hello appID URI of this app is reflected in hello web test in hello “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="8ce8b-284">공개 인증</span><span class="sxs-lookup"><span data-stu-id="8ce8b-284">Open Authentication</span></span>
<span data-ttu-id="8ce8b-285">공개 인증의 예는 Microsoft 또는 Google 계정으로 로그인하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="8ce8b-286">많은 응용 프로그램을 사용 하 여 OAuth 제공 hello 클라이언트 비밀 대신에 첫 번째 방법은 tooinvestigate 이어야 합니다.이 가능성입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-286">Many apps that use OAuth provide hello client secret alternative, so your first tactic should be tooinvestigate that possibility.</span></span>

<span data-ttu-id="8ce8b-287">테스트 해야 OAuth를 사용 하 여 로그인 하는 경우 hello 일반적인 방법이입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-287">If your test must sign in using OAuth, hello general approach is:</span></span>

* <span data-ttu-id="8ce8b-288">Fiddler tooexamine hello 트래픽 앱, 웹 브라우저 및 hello 인증 사이트와 같은 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-288">Use a tool such as Fiddler tooexamine hello traffic between your web browser, hello authentication site, and your app.</span></span>
* <span data-ttu-id="8ce8b-289">두 개 이상의 로그인 서로 다른 컴퓨터 또는 브라우저를 사용 하 여 수행 하거나 (tooallow 토큰 tooexpire) 긴 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (tooallow tokens tooexpire).</span></span>
* <span data-ttu-id="8ce8b-290">서로 다른 세션을 비교 하 여 로그인 한 후 응용 프로그램 서버 tooyour 전달 되는 사이트를 인증 하는 hello에서 다시 전달 하는 hello 토큰을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-290">By comparing different sessions, identify hello token passed back from hello authenticating site, that is then passed tooyour app server after sign-in.</span></span>
* <span data-ttu-id="8ce8b-291">Visual Studio Online을 사용하여 웹 테스트 기록</span><span class="sxs-lookup"><span data-stu-id="8ce8b-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="8ce8b-292">Hello 토큰 hello 인증자에서 반환 되 면 hello 매개 변수를 설정 하 고 hello 쿼리 toohello 사이트에서 사용 하 여 hello 토큰 매개 변수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-292">Parameterize hello tokens, setting hello parameter when hello token is returned from hello authenticator, and using it in hello query toohello site.</span></span>
  <span data-ttu-id="8ce8b-293">(Visual Studio tooparameterize hello 테스트 하려고 하지만 hello 토큰 올바르게 매개 변수화 되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="8ce8b-293">(Visual Studio attempts tooparameterize hello test, but does not correctly parameterize hello tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="8ce8b-294">성능 테스트</span><span class="sxs-lookup"><span data-stu-id="8ce8b-294">Performance tests</span></span>
<span data-ttu-id="8ce8b-295">웹 사이트에 부하 테스트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-295">You can run a load test on your website.</span></span> <span data-ttu-id="8ce8b-296">Hello 가용성 테스트와 같은 hello 전 세계이 지점에서 간단한 요청 또는 multi-step 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-296">Like hello availability test, you can send either simple requests or multi-step requests from our points around hello world.</span></span> <span data-ttu-id="8ce8b-297">가용성 테스트와는 달리 많은 요청이 전송되어 여러 동시 사용자를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="8ce8b-298">Hello 개요 블레이드에서 엽니다 **설정**, **성능 테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-298">From hello Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="8ce8b-299">초대는 테스트를 만들 때 tooconnect tooor Visual Studio Team Services 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-299">When you create a test, you are invited tooconnect tooor create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="8ce8b-300">Hello 테스트 완료 되 면 응답 시간과 성공률 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-300">When hello test is complete, you are shown response times and success rates.</span></span>


![성능 테스트](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="8ce8b-302">성능 테스트의 tooobserve hello 효과 사용 하 여 [라이브 스트림을](app-insights-live-stream.md) 및 [프로파일러](app-insights-profiler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-302">tooobserve hello effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="8ce8b-303">Automation</span><span class="sxs-lookup"><span data-stu-id="8ce8b-303">Automation</span></span>
* <span data-ttu-id="8ce8b-304">[PowerShell 스크립트 tooset 가용성 테스트를 사용 하 여](app-insights-powershell.md#add-an-availability-test) 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-304">[Use PowerShell scripts tooset up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="8ce8b-305">경고가 발생하면 호출되는 [웹후크](../monitoring-and-diagnostics/insights-webhooks-alerts.md)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="8ce8b-306"><a name="qna"></a>질문이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8ce8b-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="8ce8b-307">문제가 있습니까?</span><span class="sxs-lookup"><span data-stu-id="8ce8b-307">Problems?</span></span>
* <span data-ttu-id="8ce8b-308">*웹 테스트에서 코드를 호출할 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="8ce8b-309">아니요.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-309">No.</span></span> <span data-ttu-id="8ce8b-310">hello hello 테스트 단계 hello.webtest 파일에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-310">hello steps of hello test must be in hello .webtest file.</span></span> <span data-ttu-id="8ce8b-311">또한 다른 웹 테스트를 호출하거나 루프를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="8ce8b-312">그러나 몇 가지 유용한 플러그 인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="8ce8b-313">*HTTPS가 지원됩니까?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="8ce8b-314">TLS 1.1 및 TLS 1.2를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="8ce8b-315">*"웹 테스트" 및 "가용성 테스트" 간의 차이가 있나요?*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="8ce8b-316">hello 두 용어 참조 될 수 있습니다 같은 의미로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-316">hello two terms may be referenced interchangeably.</span></span> <span data-ttu-id="8ce8b-317">가용성 테스트 hello 단일 URL ping을 포함 하는 보다 일반적인 용어 테스트 또한 toohello multi-step 웹 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-317">Availability tests is a more generic term that includes hello single URL ping tests in addition toohello multi-step web tests.</span></span>
* <span data-ttu-id="8ce8b-318">*방화벽 뒤에서 실행 되는 내부 서버에서 toouse 가용성 테스트를 하겠습니다.*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-318">*I'd like toouse availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="8ce8b-319">가능한 해결 방법으로 다음 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="8ce8b-320">방화벽 toopermit 들어오는 요청에서 hello 구성 [웹의 IP 주소 테스트 에이전트](app-insights-ip-addresses.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-320">Configure your firewall toopermit incoming requests from hello [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="8ce8b-321">내부 서버 tooperiodically 테스트 사용자 고유의 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-321">Write your own code tooperiodically test your internal server.</span></span> <span data-ttu-id="8ce8b-322">방화벽 뒤에 있는 테스트 서버에서 백그라운드 프로세스로 hello 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-322">Run hello code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="8ce8b-323">테스트 프로세스 결과 보낼 수는 tooApplication Insights를 사용 하 여 [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello 핵심 SDK 패키지에서 API입니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-323">Your test process can send its results tooApplication Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in hello core SDK package.</span></span> <span data-ttu-id="8ce8b-324">이 위해서는 테스트 서버 toohave 나가는 액세스 toohello Application Insights 수집 끝점에 있지만 hello의 들어오는 요청을 허용 하는 대체 항목 보다 훨씬 더 작은 보안 위험.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-324">This requires your test server toohave outgoing access toohello Application Insights ingestion endpoint, but that is a much smaller security risk than hello alternative of permitting incoming requests.</span></span> <span data-ttu-id="8ce8b-325">hello 결과가 hello 가용성 웹 테스트 블레이드에 표시 되지 않습니다 되지만 분석, 검색 및 메트릭 탐색기에서 가용성 결과으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-325">hello results will not appear in hello availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="8ce8b-326">*다중 단계 웹 테스트 업로드 실패*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="8ce8b-327">300K의 크기 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="8ce8b-328">루프는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-328">Loops aren't supported.</span></span>

    <span data-ttu-id="8ce8b-329">참조 tooother 웹 테스트가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-329">References tooother web tests aren't supported.</span></span>

    <span data-ttu-id="8ce8b-330">데이터 원본은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="8ce8b-331">*다중 단계 테스트가 완료되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="8ce8b-332">테스트당 100개 요청의 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="8ce8b-333">hello 테스트 2 분 이상 실행 하는 경우 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-333">hello test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="8ce8b-334">*클라이언트 인증서로 테스트를 실행하는 방법*</span><span class="sxs-lookup"><span data-stu-id="8ce8b-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="8ce8b-335">죄송합니다만, 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ce8b-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="8ce8b-336"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ce8b-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="8ce8b-337">[진단 로그 검색][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="8ce8b-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="8ce8b-338">[문제 해결][qna]</span><span class="sxs-lookup"><span data-stu-id="8ce8b-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="8ce8b-339">웹 테스트 에이전트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="8ce8b-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
