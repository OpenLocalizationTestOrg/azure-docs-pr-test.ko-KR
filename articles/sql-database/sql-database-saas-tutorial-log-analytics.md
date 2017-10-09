---
title: "SQL 데이터베이스는 다중 테 넌 트 앱으로 로그 분석 aaaUse | Microsoft Docs"
description: "설정 하 고 hello Azure SQL 데이터베이스 샘플 Wingtip SaaS 응용 프로그램으로 로그 분석 (OMS) 사용"
keywords: "SQL Database 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a><span data-ttu-id="59c2e-104">설정 하 고 로그 분석 (OMS) hello Wingtip SaaS 앱과 함께 사용</span><span class="sxs-lookup"><span data-stu-id="59c2e-104">Setup and use Log Analytics (OMS) with hello Wingtip SaaS app</span></span>

<span data-ttu-id="59c2e-105">이 자습서에서는 탄력적 풀 및 데이터베이스 모니터링을 위해 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*를 설정 및 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="59c2e-106">Hello에 기반 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md), 표시 방법을 toouse *로그 분석* tooaugment hello 모니터링 및 경고 hello Azure 포털에에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-106">It builds on hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how toouse *Log Analytics* tooaugment hello monitoring and alerting provided in hello Azure portal.</span></span> <span data-ttu-id="59c2e-107">Log Analytics는 수백 개의 풀과 무수히 많은 데이터베이스를 지원하므로 특히 일정 규모의 모니터링 및 경고에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="59c2e-108">또한 여러 Azure 구독에서 다양한 응용 프로그램과 Azure 서비스의 모니터링을 통합할 수 있는 단일 모니터링 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="59c2e-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59c2e-110">Log Analytics(OMS) 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="59c2e-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="59c2e-111">로그 분석 toomonitor 풀 및 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59c2e-111">Use Log Analytics toomonitor pools and databases</span></span>

<span data-ttu-id="59c2e-112">toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-112">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="59c2e-113">hello Wingtip SaaS 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-113">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="59c2e-114">5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="59c2e-114">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="59c2e-115">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="59c2e-116">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="59c2e-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="59c2e-117">Hello 참조 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md) hello SaaS 시나리오 및 패턴 및 모니터링 솔루션의 hello 요구 사항에 미치는 영향에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-117">See hello [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of hello SaaS scenarios and patterns, and how they affect hello requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="59c2e-118">Log Analytics(OMS)를 통한 성능 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="59c2e-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="59c2e-119">SQL Database의 경우 데이터베이스 및 풀에 대한 모니터링 및 경고가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="59c2e-120">이 기본 제공 모니터링 및 경고는 리소스 관련 및 적은 수의 리소스에 대 한 편리한 있지만 적합된 toomonitoring 대규모 설치를 통해 다양 한 리소스 및 구독 통합된 보기를 제공 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited toomonitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="59c2e-121">대규모 시나리오에서는 Log Analytics가 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="59c2e-122">이것은 내보낸된 진단 로그를 통해 분석을 제공 하는 별도 Azure 서비스 및 원격 분석에서 여러 원격 분석을 수집할 수 있는 한 로그 분석 작업에서 수집 된 서비스 사용된 tooquery 수 및 경고를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used tooquery and set alerts.</span></span> <span data-ttu-id="59c2e-123">Log Analytics는 기본 제공 쿼리 언어와 데이터 시각화 도구를 제공하므로 운영 데이터 분석과 시각화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="59c2e-124">SQL 분석 솔루션 hello 몇 가지 미리 정의 된 탄력적 풀 및 데이터베이스 모니터링 및 경고 보기와 쿼리를 제공 하 고 사용자가 직접 임시 쿼리를 추가 하 고 필요에 따라 이러한 저장 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-124">hello SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="59c2e-125">OMS도 사용자 지정 뷰 디자이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="59c2e-126">Azure 포털 hello와 OMS 로그 분석 작업 영역 및 분석 솔루션을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-126">Log Analytics workspaces and analytics solutions can be opened both in hello Azure portal and in OMS.</span></span> <span data-ttu-id="59c2e-127">hello Azure 포털 hello 최신 액세스 포인트 이지만 일부 지역에서는 hello OMS 포털 뒤에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-127">hello Azure portal is hello newer access point but may be behind hello OMS portal in some areas.</span></span>

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a><span data-ttu-id="59c2e-128">Hello 부하 생성기 toocreate 데이터 tooanalyze 시작</span><span class="sxs-lookup"><span data-stu-id="59c2e-128">Start hello load generator toocreate data tooanalyze</span></span>

1. <span data-ttu-id="59c2e-129">열기 **데모 PerformanceMonitoringAndManagement.ps1** hello에 **PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in hello **PowerShell ISE**.</span></span> <span data-ttu-id="59c2e-130">이 스크립트를 열어 둡니다 toorun 원하는 수 만큼 여러 가지 hello 부하 생성 시나리오가이 자습서에서.</span><span class="sxs-lookup"><span data-stu-id="59c2e-130">Keep this script open as you may want toorun several of hello load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="59c2e-131">보다 작거나 5 개 테 넌 트를 설정한 경우 테 넌 트 tooprovide 더 흥미로운 모니터링 컨텍스트의 일괄 처리를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-131">If you have less than five tenants, provision a batch of tenants tooprovide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="59c2e-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span><span class="sxs-lookup"><span data-stu-id="59c2e-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="59c2e-133">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-133">Press **F5** toorun hello script.</span></span>

1. <span data-ttu-id="59c2e-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**</span><span class="sxs-lookup"><span data-stu-id="59c2e-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="59c2e-135">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-135">Press **F5** toorun hello script.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="59c2e-136">Hello Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="59c2e-136">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="59c2e-137">hello Wingtip 티켓 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-137">hello Wingtip Tickets scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="59c2e-138">스크립트 파일은 %programfiles%\microsoft hello [학습 모듈 폴더](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-138">Script files are located in hello [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="59c2e-139">Hello 다운로드 **학습 모듈** 폴더 tooyour 로컬 컴퓨터의 폴더 구조를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-139">Download hello **Learning Modules** folder tooyour local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a><span data-ttu-id="59c2e-140">로그 분석 및 hello Azure SQL 분석 솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="59c2e-140">Installing and configuring Log Analytics and hello Azure SQL Analytics solution</span></span>

<span data-ttu-id="59c2e-141">로그 분석은 toobe 구성 해야 하는 별도 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-141">Log Analytics is a separate service that needs toobe configured.</span></span> <span data-ttu-id="59c2e-142">Log Analytics는 로그 분석 작업 영역에 로그 데이터 및 원격 분석과 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="59c2e-143">작업 영역은 Azure의 다른 리소스와 마찬가지로 리소스이며 생성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="59c2e-144">Hello 작업 영역에는 hello에서 만든 toobe 필요 하지 않은 동안 동일한 리소스 그룹으로 hello (가)는 모니터링, 이렇게 하면 hello 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-144">While hello workspace doesn’t need toobe created in hello same resource group as hello application(s) it is monitoring, this often makes hello most sense.</span></span> <span data-ttu-id="59c2e-145">Hello hello Wingtip SaaS 응용 프로그램의 경우에서이 통해 hello 작업 영역 toobe 쉽게 hello 리소스 그룹을 삭제 하 여 hello 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-145">In hello case of hello Wingtip SaaS app, this enables hello workspace toobe easily deleted with hello application by simply deleting hello resource group.</span></span>

1. <span data-ttu-id="59c2e-146">열기... \\학습 모듈\\성능 모니터링 및 관리\\로그 분석\\*데모 LogAnalytics.ps1* hello에 **PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in hello **PowerShell ISE**.</span></span>
1. <span data-ttu-id="59c2e-147">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-147">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="59c2e-148">이 시점에서 hello Azure 포털 (또는 hello OMS 포털)에 열기 로그 분석 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-148">At this point you should be able open Log Analytics in hello Azure portal (or hello OMS portal).</span></span> <span data-ttu-id="59c2e-149">Hello 로그 분석 작업 영역 및 toobecome 표시에서 수집 된 원격 분석 toobe 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-149">It will take a few minutes for telemetry toobe collected in hello Log Analytics workspace and toobecome visible.</span></span> <span data-ttu-id="59c2e-150">hello 긴 데이터 hello 더 흥미로운 hello 경험을 수집 하는 hello 시스템을 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-150">hello longer you leave hello system gathering data hello more interesting hello experience will be.</span></span> <span data-ttu-id="59c2e-151">이제는 것이 toograb 음료-정당한 hello 부하 생성기 여전히 실행 되 고 있는지 확인 하십시오!</span><span class="sxs-lookup"><span data-stu-id="59c2e-151">Now's a good time toograb a beverage - just make sure hello load generator is still running!</span></span>


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a><span data-ttu-id="59c2e-152">로그 분석을 사용 하 고 데이터베이스 및 SQL 분석 솔루션 toomonitor 풀 hello</span><span class="sxs-lookup"><span data-stu-id="59c2e-152">Use Log Analytics and hello SQL Analytics solution toomonitor pools and databases</span></span>


<span data-ttu-id="59c2e-153">이 연습에서는 로그 분석 및 hello 데이터베이스 및 풀에 대 한 수집 되 고 hello 원격 분석에 OMS 포털 toolook hello 엽니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-153">In this exercise, open Log Analytics and hello OMS portal toolook at hello telemetry being gathered for hello databases and pools.</span></span>

1. <span data-ttu-id="59c2e-154">Toohello 찾아보기 [Azure 포털](https://portal.azure.com) 및 더 많은 서비스를 클릭 하 여 로그 분석을 연 다음 로그 분석 검색:</span><span class="sxs-lookup"><span data-stu-id="59c2e-154">Browse toohello [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![Log Analytics 열기](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="59c2e-156">명명 된 hello 작업 영역 선택 *wtploganalytics-&lt;사용자&gt;*합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-156">Select hello workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="59c2e-157">선택 **개요** tooopen hello hello Azure 포털에서에서 로그 분석 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-157">Select **Overview** tooopen hello Log Analytics solution in hello Azure portal.</span></span>
   <span data-ttu-id="59c2e-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="59c2e-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="59c2e-159">**중요 한**: 몇 분 전에 hello 솔루션은 현재 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-159">**IMPORTANT**: It may take a couple of minutes before hello solution is active.</span></span> <span data-ttu-id="59c2e-160">기다려 주십시오.</span><span class="sxs-lookup"><span data-stu-id="59c2e-160">Be patient!</span></span>

1. <span data-ttu-id="59c2e-161">클릭 hello Azure SQL 분석 타일 tooopen에 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-161">Click on hello Azure SQL Analytics tile tooopen it.</span></span>

    ![개요](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![분석](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="59c2e-164">hello 아래쪽 (필요한 경우 hello 블레이드 새로 고침)에 스크롤 막대가 hello 솔루션 블레이드 스크롤 옆으로 배치에서 보기를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-164">hello view in hello solution blade scrolls sideways, with its own scroll bar at hello bottom (refresh hello blade if needed).</span></span>

1. <span data-ttu-id="59c2e-165">세로 hello hello의 시간 슬라이더가 hello에 사용할 수 있는 드릴 다운 탐색기에 또는 개별 리소스 tooopen에서을 클릭 하 여 다양 한 뷰 왼쪽 위 하거나 클릭 탐색 좁은 시간 조각에 toofocus의 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-165">Explore hello various views by clicking on them or on individual resources tooopen a drill-down explorer, where you can use hello time-slider in hello top left or click on a vertical bar toofocus in on a narrower time slice.</span></span> <span data-ttu-id="59c2e-166">이 보기에서는 특정 리소스에 개별 데이터베이스 또는 풀 toofocus을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-166">With this view, you can select individual databases or pools toofocus on specific resources:</span></span>

    ![차트](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="59c2e-168">Hello 솔루션 블레이드를 다시 맨 오른쪽 toohello 스크롤하면 나타납니다 tooopen에서을 클릭 하 고 탐색할 수 있는 몇 가지 저장 된 쿼리.</span><span class="sxs-lookup"><span data-stu-id="59c2e-168">Back on hello solution blade, if you scroll toohello far right you will see some saved queries that you can click on tooopen and explore.</span></span> <span data-ttu-id="59c2e-169">쿼리를 수정하여 실험해 보고, 작성한 쿼리 중 흥미로운 것은 저장하여 나중에 다른 리소스에서 다시 열어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="59c2e-170">Hello 로그 분석 작업 영역 블레이드에서 다시 OMS 포털 tooopen hello 솔루션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-170">Back on hello Log Analytics workspace blade, select OMS Portal tooopen hello solution there.</span></span>

    ![OMS](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="59c2e-172">Hello OMS 포털의 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-172">In hello OMS portal, you can configure alerts.</span></span> <span data-ttu-id="59c2e-173">Hello 경고 hello 데이터베이스 DTU 보기 부분을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-173">Click on hello alert portion of hello database DTU view.</span></span>

1. <span data-ttu-id="59c2e-174">Hello 로그 검색에에서 하면 표시 되는 보기 hello 메트릭 표시 되는 막대 그래프를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-174">In hello Log Search view that appears you will see a bar graph of hello metrics being represented.</span></span>

    ![로그 검색](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="59c2e-176">Hello 도구 모음에서 경고를 클릭 하면 수 toosee hello에 대 한 경고 구성 되 고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-176">If you click on Alert in hello toolbar you will be able toosee hello alert configuration and can change it.</span></span>

    ![경고 규칙 추가 ](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="59c2e-178">hello 모니터링 및 OMS 로그 분석 및의 경고는 hello 데이터 hello 리소스 별로 각 리소스 블레이드에서 경고와 달리 hello 작업 영역에 대해 쿼리를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-178">hello monitoring and alerting in Log Analytics and OMS is based on queries over hello data in hello workspace, unlike hello alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="59c2e-179">따라서 데이터베이스마다 하나씩 정의하는 대신 모든 데이터베이스를 살피는 경고를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="59c2e-180">또는 여러 리소스 유형에 대한 복합 쿼리를 사용하는 경고를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="59c2e-181">쿼리는 hello hello 작업 영역에서 사용할 수 있는 데이터에 의해서만 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-181">Queries are only limited by hello data available in hello workspace.</span></span>

<span data-ttu-id="59c2e-182">SQL 데이터베이스에 대 한 로그 분석 hello 작업 영역에서 hello 데이터 볼륨에 따라에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-182">Log Analytics for SQL Database is charged for based on hello data volume in hello workspace.</span></span> <span data-ttu-id="59c2e-183">이 자습서에서는 하루에 제한 된 too500MB은 무료 작업 영역에서 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-183">In this tutorial, you created a Free workspace, which is limited too500MB per day.</span></span> <span data-ttu-id="59c2e-184">한도 도달 하면 데이터 toohello 작업 영역을 더 이상 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-184">Once that limit is reached data is no longer added toohello workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="59c2e-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59c2e-185">Next steps</span></span>

<span data-ttu-id="59c2e-186">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="59c2e-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="59c2e-187">Log Analytics(OMS) 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="59c2e-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="59c2e-188">로그 분석 toomonitor 풀 및 데이터베이스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="59c2e-188">Use Log Analytics toomonitor pools and databases</span></span>

[<span data-ttu-id="59c2e-189">테넌트 분석 자습서</span><span class="sxs-lookup"><span data-stu-id="59c2e-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="59c2e-190">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="59c2e-190">Additional resources</span></span>

* [<span data-ttu-id="59c2e-191">Hello 초기 Wingtip SaaS 응용 프로그램 배포를 구축 하는 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="59c2e-191">Additional tutorials that build upon hello initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="59c2e-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="59c2e-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="59c2e-193">OMS</span><span class="sxs-lookup"><span data-stu-id="59c2e-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
