---
title: "SQL Database 다중 테넌트 앱과 함께 Log Analytics 사용 | Microsoft Docs"
description: "Azure SQL Database 샘플 Wingtip SaaS 앱을 사용하여 Log Analytics(OMS) 설정 및 사용"
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
ms.openlocfilehash: 26f6f519ecb3abf6343dc2776aa141dff99ced15
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="setup-and-use-log-analytics-oms-with-the-wingtip-saas-app"></a><span data-ttu-id="78096-104">Wingtip SaaS 앱을 사용하여 Log Analytics(OMS) 설정 및 사용</span><span class="sxs-lookup"><span data-stu-id="78096-104">Setup and use Log Analytics (OMS) with the Wingtip SaaS app</span></span>

<span data-ttu-id="78096-105">이 자습서에서는 탄력적 풀 및 데이터베이스 모니터링을 위해 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*를 설정 및 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78096-105">In this tutorial, you set up and use *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))* for monitoring elastic pools and databases.</span></span> <span data-ttu-id="78096-106">이 자습서는 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md)를 기반으로 구성되었으며 *Log Analytics*을 사용하여 Azure Portal에서 제공하는 모니터링 및 경고를 강화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="78096-106">It builds on the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md), and shows how to use *Log Analytics* to augment the monitoring and alerting provided in the Azure portal.</span></span> <span data-ttu-id="78096-107">Log Analytics는 수백 개의 풀과 무수히 많은 데이터베이스를 지원하므로 특히 일정 규모의 모니터링 및 경고에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-107">Log Analytics is particularly suitable for monitoring and alerting at scale because it supports hundreds of pools and hundreds of thousands of databases.</span></span> <span data-ttu-id="78096-108">또한 여러 Azure 구독에서 다양한 응용 프로그램과 Azure 서비스의 모니터링을 통합할 수 있는 단일 모니터링 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-108">It also provides a single monitoring solution, which can integrate monitoring of different applications and Azure services, across multiple Azure subscriptions.</span></span>

<span data-ttu-id="78096-109">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="78096-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="78096-110">Log Analytics(OMS) 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="78096-110">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="78096-111">Log Analytics를 사용하여 풀 및 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="78096-111">Use Log Analytics to monitor pools and databases</span></span>

<span data-ttu-id="78096-112">이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-112">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="78096-113">Wingtip SaaS 앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-113">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="78096-114">5분 내에 배포하려면 [Wingtip SaaS 응용 프로그램 배포 및 탐색](sql-database-saas-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78096-114">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="78096-115">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="78096-116">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78096-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

<span data-ttu-id="78096-117">SaaS 시나리오 및 패턴에 대한 논의와 모니터링 솔루션의 요구 사항에 미치는 영향은 [성능 모니터링 및 관리 자습서](sql-database-saas-tutorial-performance-monitoring.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78096-117">See the [Performance Monitoring and Management tutorial](sql-database-saas-tutorial-performance-monitoring.md) for a discussion of the SaaS scenarios and patterns, and how they affect the requirements on a monitoring solution.</span></span>

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a><span data-ttu-id="78096-118">Log Analytics(OMS)를 통한 성능 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="78096-118">Monitoring and managing performance with Log Analytics (OMS)</span></span>

<span data-ttu-id="78096-119">SQL Database의 경우 데이터베이스 및 풀에 대한 모니터링 및 경고가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-119">For SQL Database, monitoring and alerting is available on databases and pools.</span></span> <span data-ttu-id="78096-120">이 기본 제공 모니터링 및 경고는 특정 리소스에 적용되며 소규모 리소스에 간편하게 사용할 수 있으나, 대규모 설치나 다양한 리소스 및 구독에 대한 통합 보기를 제공하는 데는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-120">This built-in monitoring and alerting is resource-specific and convenient for small numbers of resources, but is less well suited to monitoring large installations or for providing a unified view across different resources and subscriptions.</span></span>

<span data-ttu-id="78096-121">대규모 시나리오에서는 Log Analytics가 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-121">For high-volume scenarios Log Analytics can be used.</span></span> <span data-ttu-id="78096-122">이것은 여러 서비스에서 원격 분석을 수집하고 쿼리 및 경고 설정에 사용할 수 있는 로그 분석 작업 영역에서 수집된 원격 분석에 대한 분석을 제공하는 개별 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="78096-122">This is a separate Azure service that provides analytics over emitted diagnostic logs and telemetry gathered in a log analytics workspace, which can collect telemetry from many services and be used to query and set alerts.</span></span> <span data-ttu-id="78096-123">Log Analytics는 기본 제공 쿼리 언어와 데이터 시각화 도구를 제공하므로 운영 데이터 분석과 시각화가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-123">Log Analytics provides a built-in query language and data visualization tools allowing operational data analytics and visualization.</span></span> <span data-ttu-id="78096-124">SQL Analytics 솔루션은 미리 정의된 여러 탄력적 풀과 데이터베이스 모니터링 및 경고 뷰와 쿼리를 제공하며 사용자가 필요에 따라 자체 임시 쿼리를 추가하고 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-124">The SQL Analytics solution provides several pre-defined elastic pool and database monitoring and alerting views and queries, and lets you add your own ad-hoc queries and save these as needed.</span></span> <span data-ttu-id="78096-125">OMS도 사용자 지정 뷰 디자이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-125">OMS also provides a custom view designer.</span></span>

<span data-ttu-id="78096-126">Log Analytics 작업 영역과 분석 솔루션은 Azure Portal과 OMS에서 모두 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-126">Log Analytics workspaces and analytics solutions can be opened both in the Azure portal and in OMS.</span></span> <span data-ttu-id="78096-127">Azure Portal이 더 최신 액세스 방법이지만 일부 영역에서는 OMS 포털이 더 나을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-127">The Azure portal is the newer access point but may be behind the OMS portal in some areas.</span></span>

### <a name="start-the-load-generator-to-create-data-to-analyze"></a><span data-ttu-id="78096-128">분석할 데이터를 만들기 위해 부하 생성기 시작 </span><span class="sxs-lookup"><span data-stu-id="78096-128">Start the load generator to create data to analyze</span></span>

1. <span data-ttu-id="78096-129">**PowerShell ISE**에서 **Demo-PerformanceMonitoringAndManagement.ps1**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78096-129">Open **Demo-PerformanceMonitoringAndManagement.ps1** in the **PowerShell ISE**.</span></span> <span data-ttu-id="78096-130">이 자습서에서 몇 가지 부하 생성 시나리오를 실행할 수 있으므로 이 스크립트를 계속 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="78096-130">Keep this script open as you may want to run several of the load generation scenarios during this tutorial.</span></span>
1. <span data-ttu-id="78096-131">테넌트가 5개 미만이면 더 흥미로운 모니터링 환경을 위해 테넌트 일괄 처리를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-131">If you have less than five tenants, provision a batch of tenants to provide a more interesting monitoring context:</span></span>
   1. <span data-ttu-id="78096-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span><span class="sxs-lookup"><span data-stu-id="78096-132">Set **$DemoScenario = 1,** **Provision a batch of tenants**</span></span>
   1. <span data-ttu-id="78096-133">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-133">Press **F5** to run the script.</span></span>

1. <span data-ttu-id="78096-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**</span><span class="sxs-lookup"><span data-stu-id="78096-134">Set **$DemoScenario** = 2, **Generate normal intensity load (approx 40 DTU)**.</span></span>
1. <span data-ttu-id="78096-135">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-135">Press **F5** to run the script.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="78096-136">Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="78096-136">Get the Wingtip application scripts</span></span>

<span data-ttu-id="78096-137">Wingtip Tickets 스크립트 및 응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-137">The Wingtip Tickets scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="78096-138">스크립트 파일은 [Learning Modules 폴더](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-138">Script files are located in the [Learning Modules folder](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules).</span></span> <span data-ttu-id="78096-139">**Learning Modules** 폴더의 구조를 유지하면서 이 폴더를 로컬 컴퓨터로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-139">Download the **Learning Modules** folder to your local computer, maintaining its folder structure.</span></span>

## <a name="installing-and-configuring-log-analytics-and-the-azure-sql-analytics-solution"></a><span data-ttu-id="78096-140">Log Analytics 및 Azure SQL Analytics 솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="78096-140">Installing and configuring Log Analytics and the Azure SQL Analytics solution</span></span>

<span data-ttu-id="78096-141">Log Analytics는 구성이 필요한 별도의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="78096-141">Log Analytics is a separate service that needs to be configured.</span></span> <span data-ttu-id="78096-142">Log Analytics는 로그 분석 작업 영역에 로그 데이터 및 원격 분석과 메트릭을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-142">Log Analytics collects log data and telemetry and metrics in a log analytics workspace.</span></span> <span data-ttu-id="78096-143">작업 영역은 Azure의 다른 리소스와 마찬가지로 리소스이며 생성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-143">A workspace is a resource, just like other resources in Azure, and must be created.</span></span> <span data-ttu-id="78096-144">작업 영역을 자신이 모니터링하는 응용 프로그램과 동일한 리소스 그룹에서 만들 필요는 없지만 대부분의 경우 이렇게 하는 것이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-144">While the workspace doesn’t need to be created in the same resource group as the application(s) it is monitoring, this often makes the most sense.</span></span> <span data-ttu-id="78096-145">Wingtip SaaS 앱의 경우 리소스 그룹을 삭제하기만 하면 간단하게 작업 영역을 응용 프로그램과 함께 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-145">In the case of the Wingtip SaaS app, this enables the workspace to be easily deleted with the application by simply deleting the resource group.</span></span>

1. <span data-ttu-id="78096-146">**PowerShell ISE**에서 \\학습 모듈\\성능 모니터링 및 관리\\Log Analytics\\*Demo-LogAnalytics.ps1*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78096-146">Open ...\\Learning Modules\\Performance Monitoring and Management\\Log Analytics\\*Demo-LogAnalytics.ps1* in the **PowerShell ISE**.</span></span>
1. <span data-ttu-id="78096-147">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-147">Press **F5** to run the script.</span></span>

<span data-ttu-id="78096-148">이 시점에는 Azure Portal(또는 OMS 포털)에서 Log Analytics를 열 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-148">At this point you should be able open Log Analytics in the Azure portal (or the OMS portal).</span></span> <span data-ttu-id="78096-149">Log Analytics 작업 영역에서 원격 분석을 수집하여 표시하는 데는 몇 분 정도 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="78096-149">It will take a few minutes for telemetry to be collected in the Log Analytics workspace and to become visible.</span></span> <span data-ttu-id="78096-150">시스템의 데이터 수집 시간이 길어질수록 더 흥미로운 경험이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78096-150">The longer you leave the system gathering data the more interesting the experience will be.</span></span> <span data-ttu-id="78096-151">이제 잠시 쉬면서 부하 생성기가 계속 실행 중인지 확인해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="78096-151">Now's a good time to grab a beverage - just make sure the load generator is still running!</span></span>


## <a name="use-log-analytics-and-the-sql-analytics-solution-to-monitor-pools-and-databases"></a><span data-ttu-id="78096-152">Log Analytics 및 SQL Analytics 솔루션을 사용하여 풀 및 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="78096-152">Use Log Analytics and the SQL Analytics solution to monitor pools and databases</span></span>


<span data-ttu-id="78096-153">이 연습에서는 Log Analytics 및 OMS 포털을 열고 데이터베이스 및 풀에 대해 원격 분석이 수집되는 과정을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="78096-153">In this exercise, open Log Analytics and the OMS portal to look at the telemetry being gathered for the databases and pools.</span></span>

1. <span data-ttu-id="78096-154">[Azure Portal](https://portal.azure.com)로 이동하고 다른 서비스를 클릭하여 Log Analytics를 연 다음 Log Analytics를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-154">Browse to the [Azure portal](https://portal.azure.com) and open Log Analytics by clicking More services, then search for Log Analytics:</span></span>

   ![Log Analytics 열기](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. <span data-ttu-id="78096-156">이름이 *wtploganalytics-&lt;USER&gt;*인 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-156">Select the workspace named *wtploganalytics-&lt;USER&gt;*.</span></span>

1. <span data-ttu-id="78096-157">**개요**를 선택하여 Azure Portal에서 Log Analytics를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78096-157">Select **Overview** to open the Log Analytics solution in the Azure portal.</span></span>
   <span data-ttu-id="78096-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span><span class="sxs-lookup"><span data-stu-id="78096-158">![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)</span></span>

    <span data-ttu-id="78096-159">**중요**: 솔루션이 활성화되려면 몇 분 정도 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-159">**IMPORTANT**: It may take a couple of minutes before the solution is active.</span></span> <span data-ttu-id="78096-160">기다려 주십시오.</span><span class="sxs-lookup"><span data-stu-id="78096-160">Be patient!</span></span>

1. <span data-ttu-id="78096-161">Azure SQL Analytics 타일을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78096-161">Click on the Azure SQL Analytics tile to open it.</span></span>

    ![개요](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![분석](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. <span data-ttu-id="78096-164">솔루션 블레이드의 보기는 측면으로 스크롤되며 맨 아래에 자체 스크롤 막대가 있습니다(필요한 경우 블레이드 새로 고침).</span><span class="sxs-lookup"><span data-stu-id="78096-164">The view in the solution blade scrolls sideways, with its own scroll bar at the bottom (refresh the blade if needed).</span></span>

1. <span data-ttu-id="78096-165">왼쪽 위의 시간 슬라이더를 사용할 수 잇는 드릴다운 탐색기가 열리는 보기나 개별 리소스를 클릭하거나, 더 좁은 시간 조각에 초점을 맞추는 세로 막대를 클릭하여 다양한 보기를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="78096-165">Explore the various views by clicking on them or on individual resources to open a drill-down explorer, where you can use the time-slider in the top left or click on a vertical bar to focus in on a narrower time slice.</span></span> <span data-ttu-id="78096-166">이 보기를 통해 개별 데이터베이스나 풀을 선택하여 특정 리소스에 초점을 맞출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-166">With this view, you can select individual databases or pools to focus on specific resources:</span></span>

    ![차트](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. <span data-ttu-id="78096-168">솔루션 블레이드로 돌아가 맨 오른쪽으로 스크롤하면 몇 가지 저장된 쿼리가 표시됩니다. 이 쿼리를 클릭하여 열고 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-168">Back on the solution blade, if you scroll to the far right you will see some saved queries that you can click on to open and explore.</span></span> <span data-ttu-id="78096-169">쿼리를 수정하여 실험해 보고, 작성한 쿼리 중 흥미로운 것은 저장하여 나중에 다른 리소스에서 다시 열어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-169">You can experiment with modifying these, and save any interesting queries you produce, which you can then re-open and use with other resources.</span></span>

1. <span data-ttu-id="78096-170">Log Analytics 작업 영역 블레이드로 돌아가 OMS 포털을 선택하여 해당 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78096-170">Back on the Log Analytics workspace blade, select OMS Portal to open the solution there.</span></span>

    ![OMS](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. <span data-ttu-id="78096-172">OMS 포털에서 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-172">In the OMS portal, you can configure alerts.</span></span> <span data-ttu-id="78096-173">데이터베이스 DTU 보기에서 경고 부분을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-173">Click on the alert portion of the database DTU view.</span></span>

1. <span data-ttu-id="78096-174">표시되는 로그 검색 보기에는 표시할 메트릭의 막대 그래프가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="78096-174">In the Log Search view that appears you will see a bar graph of the metrics being represented.</span></span>

    ![로그 검색](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. <span data-ttu-id="78096-176">도구 모음에서 경고를 클릭하면 경고 구성을 확인하고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-176">If you click on Alert in the toolbar you will be able to see the alert configuration and can change it.</span></span>

    ![경고 규칙 추가 ](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

<span data-ttu-id="78096-178">Log Analytics 및 OMS의 모니터링 및 경고는 특정 리소스에 적용되는 각각의 리소스 블레이드와는 달리 작업 영역의 데이터에 관한 쿼리를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-178">The monitoring and alerting in Log Analytics and OMS is based on queries over the data in the workspace, unlike the alerting on each resource blade, which is resource-specific.</span></span> <span data-ttu-id="78096-179">따라서 데이터베이스마다 하나씩 정의하는 대신 모든 데이터베이스를 살피는 경고를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-179">Thus, you can define an alert that looks over all databases, say, rather than defining one per database.</span></span> <span data-ttu-id="78096-180">또는 여러 리소스 유형에 대한 복합 쿼리를 사용하는 경고를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="78096-180">Or write an alert that uses a composite query over multiple resource types.</span></span> <span data-ttu-id="78096-181">쿼리는 작업 영역에서 사용 가능한 데이터를 통해서만 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="78096-181">Queries are only limited by the data available in the workspace.</span></span>

<span data-ttu-id="78096-182">SQL Database용 Log Analytics는 작업 영역의 데이터 크기에 따라 과금됩니다.</span><span class="sxs-lookup"><span data-stu-id="78096-182">Log Analytics for SQL Database is charged for based on the data volume in the workspace.</span></span> <span data-ttu-id="78096-183">이 자습서에서는 무료로 일일 500MB로 제한되는 작업 영역을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-183">In this tutorial, you created a Free workspace, which is limited to 500MB per day.</span></span> <span data-ttu-id="78096-184">이 한도에 도달하면 더 이상 작업 영역에 데이터가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-184">Once that limit is reached data is no longer added to the workspace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78096-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78096-185">Next steps</span></span>

<span data-ttu-id="78096-186">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="78096-186">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="78096-187">Log Analytics(OMS) 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="78096-187">Install and configure Log Analytics (OMS)</span></span>
> * <span data-ttu-id="78096-188">Log Analytics를 사용하여 풀 및 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="78096-188">Use Log Analytics to monitor pools and databases</span></span>

[<span data-ttu-id="78096-189">테넌트 분석 자습서</span><span class="sxs-lookup"><span data-stu-id="78096-189">Tenant analytics tutorial</span></span>](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a><span data-ttu-id="78096-190">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="78096-190">Additional resources</span></span>

* [<span data-ttu-id="78096-191">초기 Wingtip SaaS 응용 프로그램 배포를 기반으로 작성된 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="78096-191">Additional tutorials that build upon the initial Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="78096-192">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="78096-192">Azure Log Analytics</span></span>](../log-analytics/log-analytics-azure-sql.md)
* [<span data-ttu-id="78096-193">OMS</span><span class="sxs-lookup"><span data-stu-id="78096-193">OMS</span></span>](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
