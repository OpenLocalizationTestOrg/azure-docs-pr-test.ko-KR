---
title: "Visual Studio CodeLens에서 Application Insights 원격 분석 | Microsoft Docs"
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
ms.openlocfilehash: 20933afab55043ccc5ce908c04c6e4a7a28e3538
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a><span data-ttu-id="0a20b-103">Visual Studio CodeLens에서 Application Insights 원격 분석</span><span class="sxs-lookup"><span data-stu-id="0a20b-103">Application Insights telemetry in Visual Studio CodeLens</span></span>
<span data-ttu-id="0a20b-104">웹앱의 코드에 있는 메서드는 런타임 예외 및 요청 응답 시간에 대한 원격 분석을 사용하여 주석이 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-104">Methods in the code of your web app can be annotated with telemetry about run-time exceptions and request response times.</span></span> <span data-ttu-id="0a20b-105">응용 프로그램에 [Azure Application Insights](app-insights-overview.md)를 설치하는 경우 원격 분석은 Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx)에 표시됩니다. 즉, 각 함수의 상단에 있는 메모에서 해당 함수가 참조된 횟수 또는 마지막으로 편집한 사용자 등 유용한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-105">If you install [Azure Application Insights](app-insights-overview.md) in your application, the telemetry appears in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) - the notes at the top of each function where you're used to seeing useful information such as the number of places the function is referenced or the last person who edited it.</span></span>

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> <span data-ttu-id="0a20b-107">CodeLens에서 Application Insights는 Visual Studio 2015 업데이트 3 이상에서 또는 최신 버전의 [개발자 분석 도구 확장](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a)과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-107">Application Insights in CodeLens is available in Visual Studio 2015 Update 3 and later, or with the latest version of [Developer Analytics Tools extension](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a).</span></span> <span data-ttu-id="0a20b-108">CodeLens는 Visual Studio의 Enterprise 및 Professional edition에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-108">CodeLens is available in the Enterprise and Professional editions of Visual Studio.</span></span>
> 
> 

## <a name="where-to-find-application-insights-data"></a><span data-ttu-id="0a20b-109">Application Insights 데이터의 위치</span><span class="sxs-lookup"><span data-stu-id="0a20b-109">Where to find Application Insights data</span></span>
<span data-ttu-id="0a20b-110">웹 응용 프로그램의 공용 요청 메서드의 CodeLens 지표에서 Application Insights 원격 분석을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-110">Look for Application Insights telemetry in the CodeLens indicators of the public request methods of your web application.</span></span> <span data-ttu-id="0a20b-111">CodeLens 지표는 C# 및 Visual Basic 코드로 위의 메서드 및 다른 선언을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-111">CodeLens indicators are shown above method and other declarations in C# and Visual Basic code.</span></span> <span data-ttu-id="0a20b-112">Application Insights 데이터를 메서드에 사용할 수 있는 경우 "100개의 요청, 1% 실패함" 또는 "10개의 예외"와 같은 요청 및 예외에 대한 표시를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-112">If Application Insights data is available for a method, you'll see indicators for requests and exceptions such as "100 requests, 1% failed" or "10 exceptions."</span></span> <span data-ttu-id="0a20b-113">자세한 내용은 CodeLens 지표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-113">Click a CodeLens indicator for more details.</span></span> 

> [!TIP]
> <span data-ttu-id="0a20b-114">Application Insights 요청 및 예외 지표를 로드하려면 다른 CodeLens 지표가 표시된 후에 몇 초가 더 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-114">Application Insights request and exception indicators may take a few extra seconds to load after other CodeLens indicators appear.</span></span>
> 
> 

## <a name="exceptions-in-codelens"></a><span data-ttu-id="0a20b-115">CodeLens의 예외</span><span class="sxs-lookup"><span data-stu-id="0a20b-115">Exceptions in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

<span data-ttu-id="0a20b-117">예외 CodeLens 지표는 해당 기간 동안 응용 프로그램에서 가장 자주 발생한 15개의 예외 지난 24시간 동안 발생한 예외의 수를 보여 주고 메서드에서 제공한 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-117">The exception CodeLens indicator shows the number of exceptions that have occurred in the past 24 hours from the 15 most frequently occurring exceptions in your application during that period, while processing the request served by the method.</span></span>

<span data-ttu-id="0a20b-118">자세한 세부 정보를 보려면 예외 CodeLens 지표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-118">To see more details, click the exceptions CodeLens indicator:</span></span>

* <span data-ttu-id="0a20b-119">가장 최근 24시간 동안 발생한 예외의 수에서 발생한 비율 변화는 전기 24시간에 비해 상대적입니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-119">The percentage change in number of exceptions from the most recent 24 hours relative to the prior 24 hours</span></span>
* <span data-ttu-id="0a20b-120">**코드로 이동** 을 선택하여 예외를 throw하는 함수에 대한 소스 코드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-120">Choose **Go to code** to navigate to the source code for the function throwing the exception</span></span>
* <span data-ttu-id="0a20b-121">**검색** 을 선택하여 지난 24시간 동안 발생한 이러한 예외의 모든 인스턴스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-121">Choose **Search** to query all instances of this exception that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="0a20b-122">**추세** 를 선택하여 지난 24시간 동안 발생한 이러한 예외의 추세 시각화를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-122">Choose **Trend** to view a trend visualization for occurrences of this exception in the past 24 hours</span></span>
* <span data-ttu-id="0a20b-123">**이 앱에서 모든 예외 보기** 를 선택하여 지난 24시간 동안 발생한 모든 예외를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-123">Choose **View all exceptions in this app** to query all exceptions that have occurred in the past 24 hours</span></span>
* <span data-ttu-id="0a20b-124">**예외 추세 탐색** 을 선택하여 지난 24시간 동안 발생한 모든 예외의 추세 시각화를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-124">Choose **Explore exception trends** to view a trend visualization for all exceptions that have occurred in the past 24 hours.</span></span> 

> [!TIP]
> <span data-ttu-id="0a20b-125">CodeLens에서 "0개의 예외"가 표시되지만 예외가 있다는 점을 아는 경우 CodeLens에서 올바른 Application Insights 리소스가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-125">If you see "0 exceptions" in CodeLens but you know there should be exceptions, check to make sure the right Application Insights resource is selected in CodeLens.</span></span> <span data-ttu-id="0a20b-126">다른 리소스를 선택하려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights > 원격 분석 원본 선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-126">To select another resource, right-click on your project in the Solution Explorer and choose **Application Insights > Choose Telemetry Source**.</span></span> <span data-ttu-id="0a20b-127">CodeLens는 지난 24시간 동안 응용 프로그램에서 가장 자주 발생한 15개의 예외에 대해서만 표시되므로, 가장 자주 발생하는 16번째 이후의 예외인 경우 "0 exceptions(0개의 예외)"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-127">CodeLens is only shown for the 15 most frequently occurring exceptions in your application in the past 24 hours, so if an exception is the 16th most frequently or less, you'll see "0 exceptions."</span></span> <span data-ttu-id="0a20b-128">ASP.NET 보기에서 예외는 해당 보기를 생성하는 컨트롤러 메서드에 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-128">Exceptions from ASP.NET views may not appear on the controller methods that generated those views.</span></span>
> 
> [!TIP]
> <span data-ttu-id="0a20b-129">”가 표시되면?</span><span class="sxs-lookup"><span data-stu-id="0a20b-129">If you see "?</span></span> <span data-ttu-id="0a20b-130">CodeLens에 "?개의 예외"가 표시되면 Azure 계정을 Visual Studio에 연결해야 합니다. 또는 Azure 계정 자격 증명이 만료되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-130">exceptions" in CodeLens, you need to associate your Azure account with Visual Studio or your Azure account credential may have expired.</span></span> <span data-ttu-id="0a20b-131">두 경우 모두 "?</span><span class="sxs-lookup"><span data-stu-id="0a20b-131">In either case, click "?</span></span> <span data-ttu-id="0a20b-132">예외"를 클릭하고 **계정 추가...**를 선택하여 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-132">exceptions" and choose **Add an account...** to enter your credentials.</span></span>
> 
> 

## <a name="requests-in-codelens"></a><span data-ttu-id="0a20b-133">CodeLens에서 요청</span><span class="sxs-lookup"><span data-stu-id="0a20b-133">Requests in CodeLens</span></span>
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

<span data-ttu-id="0a20b-135">요청 CodeLens 지표는 지난 24시간 동안 메서드에서 제공한 HTTP 요청의 수와 실패한 해당 요청의 비율을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-135">The request CodeLens indicator shows the number of HTTP requests that been serviced by a method in the past 24 hours, plus the percentage of those requests that failed.</span></span>

<span data-ttu-id="0a20b-136">자세한 세부 정보를 보려면 요청 CodeLens 지표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-136">To see more details, click the requests CodeLens indicator:</span></span>

* <span data-ttu-id="0a20b-137">전기 24시간에 비한 지난 24시간 동안 발생한 요청, 실패한 요청의 수 및 평균 응답 시간 절대 값과 비율 변경</span><span class="sxs-lookup"><span data-stu-id="0a20b-137">The absolute and percentage changes in number of requests, failed requests, and average response times over the past 24 hours compared to the prior 24 hours</span></span>
* <span data-ttu-id="0a20b-138">지난 24시간 동안 실패하지 않은 요청의 백분율로 계산된 메서드의 안정성</span><span class="sxs-lookup"><span data-stu-id="0a20b-138">The reliability of the method, calculated as the percentage of requests that did not fail in the past 24 hours</span></span>
* <span data-ttu-id="0a20b-139">요청 또는 실패한 요청에 대한 **검색** 선택하여 지난 24시간 동안 발생한 모든(실패한) 요청을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-139">Choose **Search** for requests or failed requests to query all the (failed) requests that occurred in the past 24 hours</span></span>
* <span data-ttu-id="0a20b-140">**추세** 를 선택하여 지난 24시간 동안 발생한 요청, 실패한 요청 또는 평균 응답 시간에 대한 추세 시각화를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-140">Choose **Trend** to view a trend visualization for requests, failed requests, or average response times in the past 24 hours.</span></span>
* <span data-ttu-id="0a20b-141">CodeLens 세부 정보 보기의 왼쪽 위 모퉁이에 있는 Application Insights 리소스의 이름을 선택하여 CodeLens 데이터의 원본인 리소스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-141">Choose the name of the Application Insights resource in the upper left corner of the CodeLens details view to change which resource is the source for CodeLens data.</span></span>

## <span data-ttu-id="0a20b-142"><a name="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a20b-142"><a name="next"></a>Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="0a20b-143">**[Visual Studio Online에서 Application Insights로 작업](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="0a20b-143">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="0a20b-144">원격 분석을 검색하고, CodeLens에서 데이터를 확인하며, Application Insights를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-144">Search telemetry, see data in CodeLens, and configure Application Insights.</span></span> <span data-ttu-id="0a20b-145">Visual Studio 내에서 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-145">All within Visual Studio.</span></span> |![프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 및 검색을 선택합니다.](./media/app-insights-visual-studio-codelens/34.png) |
| <span data-ttu-id="0a20b-147">**[더 많은 데이터 추가](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="0a20b-147">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="0a20b-148">사용량, 가용성, 종속성, 예외를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-148">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="0a20b-149">로깅 프레임 워크의 추적을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-149">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="0a20b-150">사용자 지정 원격 분석을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-150">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio-codelens/64.png) |
| <span data-ttu-id="0a20b-152">**[Application Insights 포털 사용](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="0a20b-152">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="0a20b-153">대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 원격 분석 내보내기입니다.</span><span class="sxs-lookup"><span data-stu-id="0a20b-153">Dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span> |![Visual studio](./media/app-insights-visual-studio-codelens/62.png) |

