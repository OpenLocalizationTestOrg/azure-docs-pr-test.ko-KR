---
title: "Azure Application Insights의 데이터를 HockeyApp aaaExploring | Microsoft Docs"
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
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="9c2aa-103">Application Insights에서 HockeyApp 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="9c2aa-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="9c2aa-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello 라이브 데스크톱 및 모바일 앱을 모니터링 하기 위한 플랫폼 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="9c2aa-105">HockeyApp을에서 사용자 지정 및 toomonitor 사용량 원격 분석 추적 보내고 수 (더하기 toogetting 충돌 데이터)에 대 한 진단에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="9c2aa-106">원격 분석의이 스트림은 강력한 hello를 사용 하 여 쿼리할 수 있는 [분석](app-insights-analytics.md) 의 기능 [Azure Application Insights](app-insights-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="9c2aa-107">수 또한 [hello 사용자 지정 및 추적 원격 분석 내보내기](app-insights-export-telemetry.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="9c2aa-108">tooenable 이러한 기능을 사용자 지정 데이터 tooApplication Insights HockeyApp을 릴레이 하는 브리지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="9c2aa-109">hello HockeyApp 브리지 앱</span><span class="sxs-lookup"><span data-stu-id="9c2aa-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="9c2aa-110">hello HockeyApp 브리지 응용 프로그램에는 hello 코어 사용할 수 있는 기능인 tooaccess HockeyApp 사용자 지정 및 hello 분석을 통해 Application Insights에서 추적 원격 분석 및 연속 내보내기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="9c2aa-111">Hello HockeyApp 브리지 앱 hello 만든 후 HockeyApp에서 수집 하는 사용자 지정 및 추적 이벤트는 이러한 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="9c2aa-112">살펴보겠습니다 어떻게 tooset 이러한 브리지 앱 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="9c2aa-113">HockeyApp에서 계정 설정, [API 토큰](https://rink.hockeyapp.net/manage/auth_tokens)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="9c2aa-114">새 토큰을 만들거나 기존 토큰을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="9c2aa-115">"읽기 전용" 하는 데 필요한 최소 권한을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="9c2aa-116">토큰 hello API의 복사본을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-116">Take a copy of hello API token.</span></span>

![HockeyApp API 토큰 가져오기](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="9c2aa-118">Microsoft Azure 포털 열기 hello 및 [Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="9c2aa-119">응용 프로그램 종류를 너무 설정 "HockeyApp 브리지 응용 프로그램":</span><span class="sxs-lookup"><span data-stu-id="9c2aa-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![새 Application Insights 리소스](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="9c2aa-121">이름을 tooset 필요 하지 않습니다-hello HockeyApp 이름에서 자동으로 설정 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="9c2aa-122">hello HockeyApp 브리지 필드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-122">hello HockeyApp bridge fields appear.</span></span> 

![브리지 필드 입력](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="9c2aa-124">앞에서 기록해 둔 hello HockeyApp 토큰을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="9c2aa-125">이 작업은 모든 HockeyApp 응용 프로그램과 함께 hello "HockeyApp 응용 프로그램" 드롭다운 메뉴를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="9c2aa-126">Toouse, 원하는 hello 필드의 전체 hello 나머지 hello 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="9c2aa-127">Hello 새 리소스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-127">Open hello new resource.</span></span> 

<span data-ttu-id="9c2aa-128">Hello 데이터 약간의 시간이 것에 유의 toostart 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-128">Note that hello data takes a while toostart flowing.</span></span>

![데이터를 기다리는 Application Insights 리소스](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="9c2aa-130">끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-130">That’s it!</span></span> <span data-ttu-id="9c2aa-131">이 시점 부터는 HockeyApp 계측 응용 프로그램에서 수집 된 사용자 지정 및 추적 데이터 이기도 이제 hello 분석에에서 사용할 수 있는 tooyou 및 Application Insights의 연속 내보내기가 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="9c2aa-132">잠시 검토해 보겠습니다 각각의 이러한 기능은 현재 사용할 수 있는 tooyou.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="9c2aa-133">분석</span><span class="sxs-lookup"><span data-stu-id="9c2aa-133">Analytics</span></span>
<span data-ttu-id="9c2aa-134">분석에는 임시 데이터 쿼리, toodiagnose 수 있는 강력한 도구 및 원격 분석 분석 및 신속 하 게 근본 원인 및 패턴을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![분석](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="9c2aa-136">분석에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="9c2aa-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="9c2aa-137">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="9c2aa-137">Continuous export</span></span>
<span data-ttu-id="9c2aa-138">연속 내보내기를 사용 하면 tooexport Azure Blob 저장소 컨테이너에 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="9c2aa-139">Application Insights에서 현재 제공 하는 hello 보존 기간 보다 오랫동안 tookeep 데이터를 유지할 경우 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="9c2aa-140">Hello 데이터를 blob 저장소에에서 유지, SQL 데이터베이스 또는 기본 데이터 웨어하우스 솔루션으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c2aa-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="9c2aa-141">연속 내보내기에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="9c2aa-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="9c2aa-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c2aa-142">Next steps</span></span>
* [<span data-ttu-id="9c2aa-143">분석 tooyour 데이터 적용</span><span class="sxs-lookup"><span data-stu-id="9c2aa-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

