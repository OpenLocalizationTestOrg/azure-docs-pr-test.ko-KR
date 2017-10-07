---
title: "Azure Application Insights에서 검색을 aaaSmart | Microsoft Docs"
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
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="8652e-103">Application Insights의 스마트 감지</span><span class="sxs-lookup"><span data-stu-id="8652e-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="8652e-104">스마트 감지는 웹 응용 프로그램에서 잠재적인 성능 문제를 자동으로 경고해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="8652e-105">사전 분석할 때 너무 응용 프로그램에서 전송 하는 hello 원격 분석을 수행[Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8652e-106">실패율이나 클라이언트 또는 서버 성능의 비정상적인 패턴이 갑자기 증가하는 경우 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="8652e-107">이 기능에는 구성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-107">This feature needs no configuration.</span></span> <span data-ttu-id="8652e-108">응용 프로그램에서 충분한 원격 분석을 보내는 경우 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="8652e-109">스마트 감지 경고와 hello 스마트 검색 블레이드 모두 hello 전자 메일을 받으면에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="8652e-110">스마트 감지 검토</span><span class="sxs-lookup"><span data-stu-id="8652e-110">Review your Smart Detections</span></span>
<span data-ttu-id="8652e-111">두 가지 방법으로 자동 관리 검색을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="8652e-112">**전자 메일을 받습니다** .</span><span class="sxs-lookup"><span data-stu-id="8652e-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="8652e-113">일반적인 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-113">Here's a typical example:</span></span>
  
    ![전자 메일 경고](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="8652e-115">Hello 큰 단추가 tooopen hello 포털에서 자세히를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="8652e-116">**hello 스마트 검색 타일** 블레이드 응용 프로그램의 개요에 최근 경고의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="8652e-117">Hello 타일 toosee 목록이 최신 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-117">Click hello tile toosee a list of recent alerts.</span></span>

![최근 검색 보기](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="8652e-119">경고 toosee 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="8652e-120">어떤 문제가 검색되나요?</span><span class="sxs-lookup"><span data-stu-id="8652e-120">What problems are detected?</span></span>
<span data-ttu-id="8652e-121">세 가지 종류가 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="8652e-122">[스마트 감지 - 실패](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8652e-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="8652e-123">기계 학습 사용 하 여 tooset hello 예상 비율 앱 부하 및 기타 요소와의 상관 관계에 대 한 실패 한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="8652e-124">Hello 실패율 hello 예상된 봉투 (envelope) 외부 되 면 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="8652e-125">[스마트 감지 - 성능 이상](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8652e-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="8652e-126">작업 또는 종속성 기간의 응답 시간은 비교 toohistorical 기준의 속도가 느려지지 또는 응답 시간이 나 페이지 로드 시간 비정상 패턴을 식별 했습니다 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="8652e-127">[스마트 감지 - Azure 클라우드 서비스 문제](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="8652e-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="8652e-128">앱이 Azure 클라우드 서비스에서 호스트되고 역할 인스턴스에 시작 실패, 빈번한 재활용 또는 런타임 충돌이 있는 경우 경고가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="8652e-129">(각 알림에 hello 도움말 링크 이동 toohello 관련 문서.)</span><span class="sxs-lookup"><span data-stu-id="8652e-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="8652e-130">비디오</span><span class="sxs-lookup"><span data-stu-id="8652e-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="8652e-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8652e-131">Next steps</span></span>
<span data-ttu-id="8652e-132">이러한 진단 도구를 사용 하면 응용 프로그램에서 hello 원격 분석을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="8652e-133">메트릭 탐색기</span><span class="sxs-lookup"><span data-stu-id="8652e-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="8652e-134">검색 탐색기</span><span class="sxs-lookup"><span data-stu-id="8652e-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="8652e-135">분석 - 강력한 쿼리 언어</span><span class="sxs-lookup"><span data-stu-id="8652e-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="8652e-136">스마트 감지는 완전 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="8652e-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="8652e-137">하지만 미정 원하는 몇 가지 더 많은 경고를 tooset?</span><span class="sxs-lookup"><span data-stu-id="8652e-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="8652e-138">수동으로 구성된 메트릭 경고</span><span class="sxs-lookup"><span data-stu-id="8652e-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="8652e-139">가용성 웹 테스트</span><span class="sxs-lookup"><span data-stu-id="8652e-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

