---
title: "로그 분석에서 SQL 분석 솔루션 aaaAzure | Microsoft Docs"
description: "Azure SQL 분석 솔루션 hello Azure SQL 데이터베이스를 관리할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="c7bab-103">Log Analytics에 Azure SQL Analytics(미리 보기)를 사용하여 Azure SQL Database 모니터링</span><span class="sxs-lookup"><span data-stu-id="c7bab-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL 분석 기호](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="c7bab-105">Azure 로그 분석에서 Azure SQL 분석 솔루션 hello 수집 하 고 중요 한 SQL Azure 성능 메트릭 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="c7bab-106">Hello 메트릭을 수집 하는 hello 솔루션과 사용 하 여 사용자 지정 모니터링 규칙 및 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="c7bab-107">그리고 여러 Azure 구독 및 탄력적 풀 간에 Azure SQL Database 및 탄력적 풀 메트릭을 모니터링하고 이를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="c7bab-108">hello 솔루션의 응용 프로그램 스택의 각 계층에서 tooidentify 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="c7bab-109">사용 하 여 [Azure 진단 메트릭은](log-analytics-azure-storage.md) 로그 분석 함께 단일 로그 분석 작업 영역에서 모든 Azure SQL 데이터베이스 및 탄력적인 풀에 대 한 toopresent 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="c7bab-110">현재,이 미리 보기 솔루션 too150, 000 Azure SQL 데이터베이스 및 작업 영역당 5, 000 SQL 탄력적 풀을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="c7bab-111">로그 분석에 사용할 수 있는 다른 처럼 Azure SQL 분석 솔루션 hello를 사용 하면 모니터링 하 고 Azure 리소스의 hello 상태에 대 한 알림을 받을-이 경우, Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="c7bab-112">Microsoft Azure SQL 데이터베이스는 Azure 클라우드 hello에서 실행 되는 친숙 한 SQL 서버 유형의 기능 tooapplications 제공 하는 확장 가능한 관계형 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="c7bab-113">로그 분석 하면 toocollect, 상관 관계를 분석 하 고 데이터 및 구조화 되지 않은 데이터를 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="c7bab-114">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="c7bab-114">Connected sources</span></span>

<span data-ttu-id="c7bab-115">Azure SQL 분석 솔루션 hello 에이전트 tooconnect toohello 로그 분석 서비스를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="c7bab-116">다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 원본에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="c7bab-117">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="c7bab-117">Connected Source</span></span> | <span data-ttu-id="c7bab-118">지원</span><span class="sxs-lookup"><span data-stu-id="c7bab-118">Support</span></span> | <span data-ttu-id="c7bab-119">설명</span><span class="sxs-lookup"><span data-stu-id="c7bab-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c7bab-120">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="c7bab-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="c7bab-121">아니요</span><span class="sxs-lookup"><span data-stu-id="c7bab-121">No</span></span> | <span data-ttu-id="c7bab-122">Windows 에이전트를 직접 hello 솔루션에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="c7bab-123">Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="c7bab-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="c7bab-124">아니요</span><span class="sxs-lookup"><span data-stu-id="c7bab-124">No</span></span> | <span data-ttu-id="c7bab-125">Linux 에이전트를 직접 hello 솔루션에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="c7bab-126">SCOM 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="c7bab-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="c7bab-127">아니요</span><span class="sxs-lookup"><span data-stu-id="c7bab-127">No</span></span> | <span data-ttu-id="c7bab-128">Hello SCOM 에이전트 tooLog 분석의에서 직접 연결 hello 솔루션에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="c7bab-129">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="c7bab-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="c7bab-130">아니요</span><span class="sxs-lookup"><span data-stu-id="c7bab-130">No</span></span> | <span data-ttu-id="c7bab-131">로그 분석 저장소 계정에서 hello 데이터를 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="c7bab-132">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="c7bab-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="c7bab-133">예</span><span class="sxs-lookup"><span data-stu-id="c7bab-133">Yes</span></span> | <span data-ttu-id="c7bab-134">Azure 메트릭 데이터는 Azure에서 직접 tooLog 분석을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="c7bab-135">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c7bab-135">Prerequisites</span></span>

- <span data-ttu-id="c7bab-136">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="c7bab-136">An Azure Subscription.</span></span> <span data-ttu-id="c7bab-137">없는 경우 [무료](https://azure.microsoft.com/free/) 구독을 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="c7bab-138">Log Analytics 작업 영역.</span><span class="sxs-lookup"><span data-stu-id="c7bab-138">A Log Analytics workspace.</span></span> <span data-ttu-id="c7bab-139">기존 항목을 사용하거나 이 솔루션 사용을 시작하기 전에 [새로 만들 수 있습니다.](log-analytics-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c7bab-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="c7bab-140">Azure SQL 데이터베이스 및 탄력적인 풀에 대 한 Azure 진단을 사용 하도록 설정 하 고 [toosend 구성 자신의 데이터 tooLog 분석](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="c7bab-141">구성</span><span class="sxs-lookup"><span data-stu-id="c7bab-141">Configuration</span></span>

<span data-ttu-id="c7bab-142">Hello 단계 tooadd hello Azure SQL 분석 솔루션 tooyour 작업 영역을 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="c7bab-143">Hello Azure SQL 분석 솔루션 tooyour 작업 영역에서 추가 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="c7bab-144">Hello Azure 포털에서에서 클릭 **새로** (hello + 기호) hello 목록에서 리소스를 선택 **모니터링 + 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="c7bab-145">![모니터링 + 관리](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="c7bab-146">Hello에 **모니터링 + 관리** 목록에서를 클릭 **스크롤하게**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="c7bab-147">Hello에 **권장** 목록에서 클릭 **자세한** , 했는데 이후에 hello 새 목록에 **Azure SQL 분석 (미리 보기)** 다음 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="c7bab-148">![Azure SQL Analytics 솔루션](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="c7bab-149">Hello에 **Azure SQL 분석 (미리 보기)** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="c7bab-150">![만들기](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="c7bab-151">Hello에 **새 솔루션 만들기** 블레이드, 선택 hello 작업 영역 tooadd hello 솔루션 tooand 원하는 다음 클릭 있습니다 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="c7bab-152">![tooworkspace 추가](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="c7bab-153">tooconfigure 여러 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="c7bab-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="c7bab-154">toosupport 여러 구독을 사용 하 여 hello PowerShell 스크립트를 [PowerShell을 사용 하 여 사용 하도록 설정 하는 Azure 리소스 메트릭 로깅](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="c7bab-155">다른 Azure 구독에 Azure 구독 하나 tooa 작업 영역에 리소스에서 hello 스크립트 toosend 진단 데이터를 실행할 때 매개 변수로 hello 작업 공간 리소스 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="c7bab-156">**예제**</span><span class="sxs-lookup"><span data-stu-id="c7bab-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="c7bab-157">Hello 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c7bab-157">Using hello solution</span></span>

<span data-ttu-id="c7bab-158">Hello 솔루션 tooyour 작업 영역에 추가 하면 Azure SQL 분석 타일 hello tooyour 작업 영역에 추가 됩니다 및 개요에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="c7bab-159">hello 타일에는 Azure SQL 데이터베이스 및 hello 솔루션에 연결 된 Azure SQL 탄력적 풀의 hello 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Azure SQL Analytics 타일](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="c7bab-161">Azure SQL 분석 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="c7bab-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="c7bab-162">Hello 클릭 **Azure SQL 분석** tooopen hello Azure SQL 분석 대시보드 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="c7bab-163">hello 대시보드에 아래에 정의 된 hello 블레이드 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="c7bab-164">각 블레이드 too15 리소스 (구독, 서버, 탄력적 풀 및 데이터베이스)를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="c7bab-165">해당 특정 리소스에 대 한 hello 리소스 tooopen hello 대시보드 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="c7bab-166">탄력적 풀 또는 데이터베이스에는 선택한 리소스에 대 한 메트릭 사용 하 여 hello 차트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="c7bab-167">차트 tooopen hello 로그 검색 대화 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="c7bab-168">블레이드</span><span class="sxs-lookup"><span data-stu-id="c7bab-168">Blade</span></span> | <span data-ttu-id="c7bab-169">설명</span><span class="sxs-lookup"><span data-stu-id="c7bab-169">Description</span></span> |
|---|---|
| <span data-ttu-id="c7bab-170">구독</span><span class="sxs-lookup"><span data-stu-id="c7bab-170">Subscriptions</span></span> | <span data-ttu-id="c7bab-171">연결된 서버, 풀 및 데이터베이스 수가 있는 구독 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="c7bab-172">서버</span><span class="sxs-lookup"><span data-stu-id="c7bab-172">Servers</span></span> | <span data-ttu-id="c7bab-173">연결된 풀 및 데이터베이스 수가 있는 서버 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="c7bab-174">탄력적 풀</span><span class="sxs-lookup"><span data-stu-id="c7bab-174">Elastic Pools</span></span> | <span data-ttu-id="c7bab-175">목록 최대 GB 인데 관찰 된 hello에 대 한 eDTU와 연결 된 탄력적 풀의 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="c7bab-176">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c7bab-176">Databases</span></span> | <span data-ttu-id="c7bab-177">Hello 관찰 된 최대 GB 인데 DTU와 연결 된 데이터베이스 목록을 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="c7bab-178">데이터 분석 및 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="c7bab-178">Analyze data and create alerts</span></span>

<span data-ttu-id="c7bab-179">Azure SQL 데이터베이스 리소스에서 들어오는 hello 데이터와 경고를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="c7bab-180">다음은 경고 생성에 사용할 수 있는 몇 가지 유용한 [로그 검색](log-analytics-log-searches.md) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="c7bab-181">*Azure SQL Database에 대한 높은 DTU*</span><span class="sxs-lookup"><span data-stu-id="c7bab-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="c7bab-182">*Azure SQL Database 탄력적 풀에 대한 높은 DTU*</span><span class="sxs-lookup"><span data-stu-id="c7bab-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="c7bab-183">Azure SQL 데이터베이스와 탄력적 풀에 대 한 이러한 경고 기반 쿼리 tooalert 특정 임계값에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="c7bab-184">OMS 작업 영역에 대 한 경고 tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="c7bab-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="c7bab-185">tooconfigure 작업 영역에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="c7bab-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="c7bab-186">Toohello 이동 [OMS 포털](http://mms.microsoft.com/) 에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="c7bab-187">Hello 솔루션에 대해 구성 된 hello 작업 영역을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="c7bab-188">Hello 개요 페이지에서 클릭 hello **Azure SQL 분석 (미리 보기)** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="c7bab-189">Hello 예제 쿼리 중 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="c7bab-190">로그 검색에서 **경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="c7bab-191">![검색에서 경고 만들기](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="c7bab-192">Hello에 **경고 규칙 추가** 페이지 hello 적절 한 속성을 구성 하 고 원하는 클릭 한 다음 특정 임계값 hello **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="c7bab-193">![경고 규칙 추가](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="c7bab-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="c7bab-194">Azure SQL 분석 데이터에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="c7bab-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="c7bab-195">예를 들어, 모든 Azure 구독에서 모든 Azure SQL 탄력적 풀에 대 한 toocompare hello DTU 사용률은 수행할 수 있는 hello 가장 유용한 쿼리 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="c7bab-196">데이터베이스 DTU (처리량 단위) 방식으로 toodescribe 제공 Basic, Standard 및 Premium 데이터베이스 및 풀의 성능 수준의 상대적 용량을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="c7bab-197">DTU는 CPU, 메모리, 읽기 및 쓰기의 혼합 측정값을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="c7bab-198">Dtu가 증가 hello 전원 hello 성능 수준 올리기는에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="c7bab-199">예를 들어 5 DTU의 성능 수준은 1 DTU 성능 수준보다 5배 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="c7bab-200">최대 DTU 할당량이 tooeach 서버 및 탄력적인 풀을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="c7bab-201">Hello 다음 로그 검색 쿼리를 실행 하 여 하거나 이상의 SQL Azure 탄력적 풀을 활용 하는 경우 쉽게 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="c7bab-202">작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="c7bab-203">다음 예제는 hello, 볼 수 있습니다 하나 탄력적 풀에는 거의 100% 사용량이 증가 DTU 거의 사용 했지만 다른 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="c7bab-204">Azure 활동 로그를 사용 하 여 사용자 환경에서 잠재적인 최근 변경 내용을 추가 tootroubleshoot를 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![로그 검색 결과 - 높은 사용률](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="c7bab-206">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c7bab-206">See also</span></span>

- <span data-ttu-id="c7bab-207">사용 하 여 [로그 검색](log-analytics-log-searches.md) 로그 분석 tooview에서 Azure SQL 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7bab-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="c7bab-208">Azure SQL 데이터를 보여 주는 [사용자 고유의 대시보드 만들기](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="c7bab-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="c7bab-209">특정 Azure SQL 이벤트가 발생하는 경우의 [경고 만들기](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="c7bab-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
