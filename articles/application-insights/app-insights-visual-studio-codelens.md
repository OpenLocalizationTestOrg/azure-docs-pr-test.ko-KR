---
title: "Visual Studio CodeLens의 Insights 원격 분석 aaaApplication | Microsoft Docs"
description: "Visual Studio에서 CodeLens를 사용하여 Application Insights 요청 및 예외 원격 분석에 빠르게 액세스합니다."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a><span data-ttu-id="de9d3-103">Visual Studio CodeLens에서 Application Insights 원격 분석</span><span class="sxs-lookup"><span data-stu-id="de9d3-103">Application Insights telemetry in Visual Studio CodeLens</span></span>
<span data-ttu-id="de9d3-104">웹 응용 프로그램의 hello 코드의 메서드에 런타임 예외에 대 한 원격 분석으로 주석을 달아야 하 고 응답 시간을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-104">Methods in hello code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span></span> <span data-ttu-id="de9d3-105">설치 하는 경우 [Azure Application Insights](app-insights-overview.md) 응용 프로그램에서 Visual Studio에 hello 원격 분석 표시 [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello 위쪽 각 함수를 사용 하는 위치에 참고 사항 hello tooseeing 유용 위치 hello 함수 hello 수 같은 정보 또는 참조 되는 마지막으로 편집한 사용자 것 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, hello telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - hello notes at hello top of each function where you're used tooseeing useful information such as hello number of places hello function is referenced or hello last person who edited it.</span></span>

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> <span data-ttu-id="de9d3-107">CodeLens에서 application Insights는 Visual Studio 2015 업데이트 3에서 사용할 수 있는 및 이상 또는 최신 버전의 hello [개발자 분석 도구 확장](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with hello latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span></span> <span data-ttu-id="de9d3-108">CodeLens는 hello Enterprise 및 Visual studio Professional 버전에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-108">CodeLens is available in hello Enterprise and Professional editions of Visual Studio.</span></span>
> 
> 

## <a name="where-toofind-application-insights-data"></a><span data-ttu-id="de9d3-109">여기서 toofind Application Insights 데이터</span><span class="sxs-lookup"><span data-stu-id="de9d3-109">Where toofind Application Insights data</span></span>
<span data-ttu-id="de9d3-110">웹 응용 프로그램의 hello 공용 요청 메서드의 hello CodeLens 표시기의 Application Insights 원격 분석을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-110">Look for Application Insights telemetry in hello CodeLens indicators of hello public request methods of your web application.</span></span> <span data-ttu-id="de9d3-111">CodeLens 지표는 C# 및 Visual Basic 코드로 위의 메서드 및 다른 선언을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span></span> <span data-ttu-id="de9d3-112">Application Insights 데이터를 메서드에 사용할 수 있는 경우 "100개의 요청, 1% 실패함" 또는 "10개의 예외"와 같은 요청 및 예외에 대한 표시를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span></span> <span data-ttu-id="de9d3-113">자세한 내용은 CodeLens 지표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-113">Click a CodeLens indicator for more details.</span></span> 

> [!TIP]
> <span data-ttu-id="de9d3-114">Application Insights 요청 하 고 예외 표시기에는 몇 가지 추가 초 정도 걸릴 수 tooload 후 다른 CodeLens 표시기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-114">Application Insights request and exception indicators may take a few extra seconds tooload after other CodeLens indicators appear.</span></span>
> 
> 

## <a name="exceptions-in-codelens"></a><span data-ttu-id="de9d3-115">CodeLens의 예외</span><span class="sxs-lookup"><span data-stu-id="de9d3-115">Exceptions in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

<span data-ttu-id="de9d3-117">hello 예외 CodeLens 표시기에서에서 발생 한 hello 지난 24 시간 동안 15 hello 메서드에서 hello 요청을 처리 하는 동안 해당 기간 동안의 응용 프로그램에서 자주 나타나는 대부분의 예외 처리 hello에서 예외 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-117">hello exception CodeLens indicator shows hello number of exceptions that have occurred in hello past 24 hours from hello 15 most frequently occurring exceptions in your application during that period, while processing hello request served by hello method.</span></span>

<span data-ttu-id="de9d3-118">toosee 자세한 내용 hello 예외 CodeLens 표시기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-118">toosee more details, click hello exceptions CodeLens indicator:</span></span>

* <span data-ttu-id="de9d3-119">24 시간 동안 한 hello 가장 최근 24 시간 동안 상대 toohello 이전에서 예외 hello 비율 변경</span><span class="sxs-lookup"><span data-stu-id="de9d3-119">hello percentage change in number of exceptions from hello most recent 24 hours relative toohello prior 24 hours</span></span>
* <span data-ttu-id="de9d3-120">선택 **toocode 이동** hello 예외를 throw 하는 hello 함수에 대 한 toonavigate toohello 소스 코드</span><span class="sxs-lookup"><span data-stu-id="de9d3-120">Choose **Go toocode** toonavigate toohello source code for hello function throwing hello exception</span></span>
* <span data-ttu-id="de9d3-121">선택 **검색** tooquery이이 예외에서 발생 한 함수의 모든 인스턴스의 hello 지난 24 시간</span><span class="sxs-lookup"><span data-stu-id="de9d3-121">Choose **Search** tooquery all instances of this exception that have occurred in hello past 24 hours</span></span>
* <span data-ttu-id="de9d3-122">선택 **추세** tooview hello에서 지난 24 시간 동안이이 예외를 발생에 대 한 추세 시각화</span><span class="sxs-lookup"><span data-stu-id="de9d3-122">Choose **Trend** tooview a trend visualization for occurrences of this exception in hello past 24 hours</span></span>
* <span data-ttu-id="de9d3-123">선택 **이 응용 프로그램에서 모든 예외 보기** tooquery에서 발생 한 모든 예외 hello 지난 24 시간</span><span class="sxs-lookup"><span data-stu-id="de9d3-123">Choose **View all exceptions in this app** tooquery all exceptions that have occurred in hello past 24 hours</span></span>
* <span data-ttu-id="de9d3-124">선택 **예외 추세를 탐색** tooview 지난 24 시간 동안 hello에서 발생 한 모든 예외에 대 한 추세 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-124">Choose **Explore exception trends** tooview a trend visualization for all exceptions that have occurred in hello past 24 hours.</span></span> 

> [!TIP]
> <span data-ttu-id="de9d3-125">CodeLens의 "예외 0"를 참조 하는 경우 예외 있을 것을 알고 있는 toomake CodeLens hello 오른쪽 Application Insights 리소스 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check toomake sure hello right Application Insights resource is selected in CodeLens.</span></span> <span data-ttu-id="de9d3-126">tooselect 다른 리소스에서 hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Application Insights > 원격 분석 소스 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-126">tooselect another resource, right-click on your project in hello Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span></span> <span data-ttu-id="de9d3-127">CodeLens만 표시 15 hello에 대 한 대부분의 자주 나타나는 예외 hello의 응용 프로그램에 예외가 16 대부분을 자주 hello는 경우 또는 지난 24 시간, ""0 예외입니다. 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-127">CodeLens is only shown for hello 15 most frequently occurring exceptions in your application in hello past 24 hours, so if an exception is hello 16th most frequently or less, you'll see "0 exceptions."</span></span> <span data-ttu-id="de9d3-128">이러한 뷰를 생성 하는 hello 컨트롤러 메서드에서 ASP.NET 뷰에서 예외가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-128">Exceptions from ASP.NET views may not appear on hello controller methods that generated those views.</span></span>
> 
> [!TIP]
> <span data-ttu-id="de9d3-129">”가 표시되면?</span><span class="sxs-lookup"><span data-stu-id="de9d3-129">If you see "?</span></span> <span data-ttu-id="de9d3-130">예외"CodeLens의 tooassociate Visual Studio 또는 Azure 계정 자격 증명을 사용 하 여 Azure 계정 만료 된 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-130">exceptions" in CodeLens, you need tooassociate your Azure account with Visual Studio or your Azure account credential may have expired.</span></span> <span data-ttu-id="de9d3-131">두 경우 모두 "?</span><span class="sxs-lookup"><span data-stu-id="de9d3-131">In either case, click "?</span></span> <span data-ttu-id="de9d3-132">예외 "를 선택 하 고 **계정 추가...**  tooenter 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-132">exceptions" and choose **Add an account...** tooenter your credentials.</span></span>
> 
> 

## <a name="requests-in-codelens"></a><span data-ttu-id="de9d3-133">CodeLens에서 요청</span><span class="sxs-lookup"><span data-stu-id="de9d3-133">Requests in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

<span data-ttu-id="de9d3-135">hello CodeLens 표시기 표시 hello 수가 HTTP 요청을 요청 하는 된 hello 지난 24 시간 및 이러한 요청에 실패 한 클라이언트 hello 백분율의에서 방법으로 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-135">hello request CodeLens indicator shows hello number of HTTP requests that been serviced by a method in hello past 24 hours, plus hello percentage of those requests that failed.</span></span>

<span data-ttu-id="de9d3-136">toosee 자세한 내용을 보려면 클릭 하십시오 hello CodeLens 표시기를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-136">toosee more details, click hello requests CodeLens indicator:</span></span>

* <span data-ttu-id="de9d3-137">24 시간 동안 이전 24 시간 동안 비해 toohello 지난 hello를 통해 요청, 실패 한 요청 및 응답 시간 수의 절대 경로 백분율 변경 hello</span><span class="sxs-lookup"><span data-stu-id="de9d3-137">hello absolute and percentage changes in number of requests, failed requests, and average response times over hello past 24 hours compared toohello prior 24 hours</span></span>
* <span data-ttu-id="de9d3-138">실패 하지 않았지만 hello에 지난 24 시간 동안 요청 hello 백분율로 계산 hello 메서드의 hello 안정성</span><span class="sxs-lookup"><span data-stu-id="de9d3-138">hello reliability of hello method, calculated as hello percentage of requests that did not fail in hello past 24 hours</span></span>
* <span data-ttu-id="de9d3-139">선택 **검색** 요청 또는 실패 한 요청 tooquery 모든 hello 지난 24 시간 동안 발생 한 hello (실패 한) 요청에 대 한</span><span class="sxs-lookup"><span data-stu-id="de9d3-139">Choose **Search** for requests or failed requests tooquery all hello (failed) requests that occurred in hello past 24 hours</span></span>
* <span data-ttu-id="de9d3-140">선택 **추세** tooview 추세 시각화를 요청, 실패 한 요청 또는 평균 응답 시간을 hello 지난 24 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-140">Choose **Trend** tooview a trend visualization for requests, failed requests, or average response times in hello past 24 hours.</span></span>
* <span data-ttu-id="de9d3-141">Hello의 왼쪽된 위 모서리 hello CodeLens 세부 정보 보기 toochange 리소스 hello CodeLens 데이터 원본인에서 hello 이름을 hello Application Insights 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-141">Choose hello name of hello Application Insights resource in hello upper left corner of hello CodeLens details view toochange which resource is hello source for CodeLens data.</span></span>

## <span data-ttu-id="de9d3-142"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="de9d3-142"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="de9d3-143">**[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="de9d3-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="de9d3-144">원격 분석을 검색하고, CodeLens에서 데이터를 확인하며, Application Insights를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="de9d3-145">Visual Studio 내에서 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-145">All within Visual Studio.</span></span> |![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights 선택 검색](./media/app-insights-visual-studio-codelens/34.png) |
| <span data-ttu-id="de9d3-147">**[더 많은 데이터 추가](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="de9d3-147">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="de9d3-148">사용량, 가용성, 종속성, 예외를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-148">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="de9d3-149">로깅 프레임 워크의 추적을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-149">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="de9d3-150">사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-150">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio-codelens/64.png) |
| <span data-ttu-id="de9d3-152">**[Hello Application Insights 포털 작업](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="de9d3-152">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="de9d3-153">대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기입니다.</span><span class="sxs-lookup"><span data-stu-id="de9d3-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](./media/app-insights-visual-studio-codelens/62.png) |

