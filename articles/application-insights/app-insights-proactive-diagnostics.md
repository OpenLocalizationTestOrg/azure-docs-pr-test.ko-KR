---
title: "Azure Application Insights의 스마트 감지 | Microsoft Docs"
description: "Application Insights는 앱 원격 분석의 자동 심층 분석을 수행하여 잠재적 성능 문제에 대해 경고합니다."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="b8dd2-103">Application Insights의 스마트 감지</span><span class="sxs-lookup"><span data-stu-id="b8dd2-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="b8dd2-104">스마트 감지는 웹 응용 프로그램에서 잠재적인 성능 문제를 자동으로 경고해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="b8dd2-105">앱에서 [Application Insights](app-insights-overview.md)로 보내는 원격 분석의 사전 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b8dd2-106">실패율이나 클라이언트 또는 서버 성능의 비정상적인 패턴이 갑자기 증가하는 경우 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="b8dd2-107">이 기능에는 구성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-107">This feature needs no configuration.</span></span> <span data-ttu-id="b8dd2-108">응용 프로그램에서 충분한 원격 분석을 보내는 경우 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="b8dd2-109">사용자가 받은 전자 메일 또는 스마트 감지 블레이드에서 스마트 감지 경고에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="b8dd2-110">스마트 감지 검토</span><span class="sxs-lookup"><span data-stu-id="b8dd2-110">Review your Smart Detections</span></span>
<span data-ttu-id="b8dd2-111">두 가지 방법으로 자동 관리 검색을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="b8dd2-112">**전자 메일을 받습니다** .</span><span class="sxs-lookup"><span data-stu-id="b8dd2-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="b8dd2-113">일반적인 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-113">Here's a typical example:</span></span>
  
    ![전자 메일 경고](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="b8dd2-115">포털에서 자세한 정보를 열려면 큰 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="b8dd2-116">앱 개요 블레이드의 **스마트 감지 타일**에 최근 경고 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="b8dd2-117">최근 경고 목록을 보려면 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-117">Click the tile to see a list of recent alerts.</span></span>

![최근 검색 보기](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="b8dd2-119">경고를 클릭하여 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="b8dd2-120">어떤 문제가 검색되나요?</span><span class="sxs-lookup"><span data-stu-id="b8dd2-120">What problems are detected?</span></span>
<span data-ttu-id="b8dd2-121">세 가지 종류가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="b8dd2-122">[스마트 감지 - 실패](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b8dd2-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="b8dd2-123">기계 학습을 사용하여 앱에 대해 실패한 요청의 예상 비율을 설정하고 로드 및 다른 요소와 상관 관계를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="b8dd2-124">실패율이 예상된 범위를 벗어나는 경우 경고를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="b8dd2-125">[스마트 감지 - 성능 이상](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b8dd2-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="b8dd2-126">작업 또는 종속성 지속 시간의 응답 시간이 기록 기준과 비교하여 느려지거나 응답 시간 또는 페이지 로드 시간에서 비정상적인 패턴을 식별하는 경우 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="b8dd2-127">[스마트 감지 - Azure 클라우드 서비스 문제](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="b8dd2-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="b8dd2-128">앱이 Azure 클라우드 서비스에서 호스트되고 역할 인스턴스에 시작 실패, 빈번한 재활용 또는 런타임 충돌이 있는 경우 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="b8dd2-129">(각 알림에서 도움말 링크를 통해 관련 문서로 이동할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b8dd2-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="b8dd2-130">비디오</span><span class="sxs-lookup"><span data-stu-id="b8dd2-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b8dd2-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8dd2-131">Next steps</span></span>
<span data-ttu-id="b8dd2-132">이러한 진단 도구를 사용하면 앱에서 원격 분석을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="b8dd2-133">메트릭 탐색기</span><span class="sxs-lookup"><span data-stu-id="b8dd2-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="b8dd2-134">검색 탐색기</span><span class="sxs-lookup"><span data-stu-id="b8dd2-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b8dd2-135">분석 - 강력한 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="b8dd2-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="b8dd2-136">스마트 감지는 완전 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="b8dd2-137">하지만 보다 많은 경고를 설정하고 싶을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8dd2-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="b8dd2-138">수동으로 구성된 메트릭 경고</span><span class="sxs-lookup"><span data-stu-id="b8dd2-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="b8dd2-139">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="b8dd2-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

