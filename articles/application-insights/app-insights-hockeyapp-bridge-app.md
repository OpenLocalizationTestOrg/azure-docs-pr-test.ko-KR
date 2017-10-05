---
title: "Azure Application Insights에서 HockeyApp 데이터 탐색 | Microsoft Docs"
description: "Application Insights를 사용하여 Azure 앱의 사용 현황 및 성능을 분석합니다."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: 450ca10613d137393090578619f3766734d1d493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="5d848-103">Application Insights에서 HockeyApp 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="5d848-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="5d848-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) 는 데스크톱 및 Mobile Apps를 실시간으로 모니터링하는 권장된 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is the recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="5d848-105">HockeyApp에서 사용자 지정 및 추적 원격 분석을 전송하여(충돌 데이터를 가져오는 것 외에도) 사용량을 모니터링하고 진단에 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-105">From HockeyApp, you can send custom and trace telemetry to monitor usage and assist in diagnosis (in addition to getting crash data).</span></span> <span data-ttu-id="5d848-106">원격 분석의 이 스트림은 [Azure Application Insights](app-insights-analytics.md)의 강력한 [분석](app-insights-overview.md) 기능을 사용하여 쿼리될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-106">This stream of telemetry can be queried using the powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5d848-107">또한 [사용자 지정 및 추적 원격 분석을 내보낼](app-insights-export-telemetry.md)수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-107">In addition, you can [export the custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="5d848-108">이러한 기능을 활성화하기 위해 Application Insights에 HockeyApp 사용자 지정 데이터를 릴레이하는 브리지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-108">To enable these features, you set up a bridge that relays HockeyApp custom data to Application Insights.</span></span>

## <a name="the-hockeyapp-bridge-app"></a><span data-ttu-id="5d848-109">HockeyApp 브리지 앱</span><span class="sxs-lookup"><span data-stu-id="5d848-109">The HockeyApp Bridge app</span></span>
<span data-ttu-id="5d848-110">HockeyApp 브리지 앱은 분석 및 연속 내보내기 기능을 통해 Application Insights에서 HockeyApp 사용자 지정 및 추적 원격 분석에 액세스할 수 있는 핵심 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-110">The HockeyApp Bridge App is the core feature that enables you to access your HockeyApp custom and trace telemetry in Application Insights through the Analytics and Continuous Export features.</span></span> <span data-ttu-id="5d848-111">HockeyApp 브리지 앱을 만든 후에 HockeyApp에서 수집한 사용자 지정 및 추적 이벤트를 이러한 기능에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-111">Custom and trace events collected by HockeyApp after the creation of the HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="5d848-112">이러한 브리지 앱 중 하나를 설정하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-112">Let’s see how to set up one of these Bridge Apps.</span></span>

<span data-ttu-id="5d848-113">HockeyApp에서 계정 설정, [API 토큰](https://rink.hockeyapp.net/manage/auth_tokens)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="5d848-114">새 토큰을 만들거나 기존 토큰을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="5d848-115">필요한 최소 권한은 "읽기 전용"입니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-115">The minimum rights required are "read only".</span></span> <span data-ttu-id="5d848-116">API 토큰의 복사본을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-116">Take a copy of the API token.</span></span>

![HockeyApp API 토큰 가져오기](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="5d848-118">Microsoft Azure Portal을 열고 [Application Insights 리소스를 만듭니다](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="5d848-118">Open the Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="5d848-119">응용 프로그램 유형을 "HockeyApp 브리지 응용 프로그램"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-119">Set Application Type to “HockeyApp bridge application”:</span></span>

![새 Application Insights 리소스](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="5d848-121">이름을 설정하지 않아도 됩니다. - HockeyApp 이름에서 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-121">You don't need to set a name - this will automatically be set from the HockeyApp name.</span></span>

<span data-ttu-id="5d848-122">HockeyApp 브리지 필드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-122">The HockeyApp bridge fields appear.</span></span> 

![브리지 필드 입력](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="5d848-124">앞에서 설명한 HockeyApp 토큰을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-124">Enter the HockeyApp token you noted earlier.</span></span> <span data-ttu-id="5d848-125">이 작업에서는 모든 HockeyApp 응용 프로그램으로 "HockeyApp 응용 프로그램" 드롭다운 메뉴를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-125">This action populates the “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="5d848-126">사용하려는 필드를 선택하고 필드의 나머지 부분을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-126">Select the one you want to use, and complete the remainder of the fields.</span></span> 

<span data-ttu-id="5d848-127">새 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-127">Open the new resource.</span></span> 

<span data-ttu-id="5d848-128">데이터가 흐르기 시작하는 데 약간의 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-128">Note that the data takes a while to start flowing.</span></span>

![데이터를 기다리는 Application Insights 리소스](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="5d848-130">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-130">That’s it!</span></span> <span data-ttu-id="5d848-131">지금부터 HockeyApp 계측 앱에서 수집된 사용자 지정 및 추적 데이터는 이제 Application Insights의 분석 및 연속 내보내기 기능에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available to you in the Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="5d848-132">이제 사용할 수 있는 이러한 기능을 각각 간단히 검토하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-132">Let’s briefly review each of these features now available to you.</span></span>

## <a name="analytics"></a><span data-ttu-id="5d848-133">분석</span><span class="sxs-lookup"><span data-stu-id="5d848-133">Analytics</span></span>
<span data-ttu-id="5d848-134">분석은 데이터를 임시 쿼리하는 강력한 도구이며 이를 통해 원격 분석을 진단하고 분석하며 근본 원인 및 패턴을 신속하게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you to diagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![분석](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="5d848-136">분석에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5d848-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="5d848-137">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="5d848-137">Continuous export</span></span>
<span data-ttu-id="5d848-138">연속 내보내기를 사용하면 Azure Blob Storage 컨테이너에 데이터를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-138">Continuous Export allows you to export your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="5d848-139">현재 Application Insights에서 제공하는 보존 기간보다 오래 데이터를 유지해야 하는 경우 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-139">This is very useful if you need to keep your data for longer than the retention period currently offered by Application Insights.</span></span> <span data-ttu-id="5d848-140">Blob Storage에 데이터를 유지하고 SQL Database 또는 기본 데이터 웨어하우스 솔루션으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d848-140">You can keep the data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="5d848-141">연속 내보내기에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5d848-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="5d848-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d848-142">Next steps</span></span>
* [<span data-ttu-id="5d848-143">데이터에 분석 적용</span><span class="sxs-lookup"><span data-stu-id="5d848-143">Apply Analytics to your data</span></span>](app-insights-analytics-tour.md)

