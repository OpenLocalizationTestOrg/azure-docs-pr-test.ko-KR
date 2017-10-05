---
title: "Log Analytics의 Azure SQL Analytics 솔루션 | Microsoft Docs"
description: "Azure SQL Analytics 솔루션을 통해 Azure SQL Database를 관리할 수 있습니다."
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
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="99931-103">Log Analytics에 Azure SQL Analytics(미리 보기)를 사용하여 Azure SQL Database 모니터링</span><span class="sxs-lookup"><span data-stu-id="99931-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL 분석 기호](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="99931-105">Azure Log Analytics의 Azure SQL 분석 솔루션은 중요한 SQL Azure 성능 메트릭을 수집하여 시각화합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="99931-106">솔루션으로 수집한 메트릭을 사용하여 사용자 지정 모니터링 규칙 및 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="99931-107">그리고 여러 Azure 구독 및 탄력적 풀 간에 Azure SQL Database 및 탄력적 풀 메트릭을 모니터링하고 이를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="99931-108">또한 솔루션은 응용 프로그램 스택의 각 계층에서 문제를 식별할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="99931-109">[Azure 진단 메트릭](log-analytics-azure-storage.md)과 Log Analytics 뷰를 함께 사용하여 모든 Azure SQL Databases 및 탄력적 풀에 대한 데이터를 단일 Log Analytics 작업 영역에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="99931-110">현재, 이 미리 보기 솔루션은 작업 영역당 최대 150,000개의 Azure SQL Database 및 5,000개의 SQL 탄력적 풀을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="99931-111">Log Analytics에 대해 제공되는 다른 도구처럼 Azure SQL 분석 솔루션은 Azure 리소스의 상태에 대한 알림(이 경우, Azure SQL Database)을 모니터링하고 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="99931-112">Microsoft Azure SQL Database는 Azure 클라우드에서 실행되는 응용 프로그램에 친숙한 SQL Server와 유사한 기능을 제공하는 확장성 있는 관계형 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="99931-113">Log Analytics를 통해 구조적 및 비구조적 데이터를 수집하고, 상관 관계를 지정하며 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="99931-114">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="99931-114">Connected sources</span></span>

<span data-ttu-id="99931-115">Azure SQL 분석 솔루션은 Log Analytics 서비스에 연결하는 데 에이전트를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="99931-116">다음 표는 이 솔루션이 지원하는 연결된 소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="99931-117">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="99931-117">Connected Source</span></span> | <span data-ttu-id="99931-118">지원</span><span class="sxs-lookup"><span data-stu-id="99931-118">Support</span></span> | <span data-ttu-id="99931-119">설명</span><span class="sxs-lookup"><span data-stu-id="99931-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="99931-120">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="99931-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="99931-121">아니요</span><span class="sxs-lookup"><span data-stu-id="99931-121">No</span></span> | <span data-ttu-id="99931-122">직접 Windows 에이전트는 솔루션에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="99931-123">Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="99931-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="99931-124">아니요</span><span class="sxs-lookup"><span data-stu-id="99931-124">No</span></span> | <span data-ttu-id="99931-125">직접 Linux 에이전트는 솔루션에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="99931-126">SCOM 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="99931-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="99931-127">아니요</span><span class="sxs-lookup"><span data-stu-id="99931-127">No</span></span> | <span data-ttu-id="99931-128">SCOM 에이전트에서 Log Analytics로 직접 연결은 솔루션에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="99931-129">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="99931-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="99931-130">아니요</span><span class="sxs-lookup"><span data-stu-id="99931-130">No</span></span> | <span data-ttu-id="99931-131">Log Analytics는 저장소 계정의 데이터를 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="99931-132">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="99931-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="99931-133">예</span><span class="sxs-lookup"><span data-stu-id="99931-133">Yes</span></span> | <span data-ttu-id="99931-134">Azure 메트릭 데이터는 Azure에 의해 직접 Log Analytics에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="99931-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="99931-135">필수 조건</span><span class="sxs-lookup"><span data-stu-id="99931-135">Prerequisites</span></span>

- <span data-ttu-id="99931-136">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="99931-136">An Azure Subscription.</span></span> <span data-ttu-id="99931-137">없는 경우 [무료](https://azure.microsoft.com/free/) 구독을 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="99931-138">Log Analytics 작업 영역.</span><span class="sxs-lookup"><span data-stu-id="99931-138">A Log Analytics workspace.</span></span> <span data-ttu-id="99931-139">기존 항목을 사용하거나 이 솔루션 사용을 시작하기 전에 [새로 만들 수 있습니다.](log-analytics-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="99931-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="99931-140">Azure SQL Database 및 탄력적 풀에 대한 Azure 진단을 사용하도록 설정하고 [Log Analytics에 데이터를 보내도록 구성](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="99931-141">구성</span><span class="sxs-lookup"><span data-stu-id="99931-141">Configuration</span></span>

<span data-ttu-id="99931-142">Azure SQL 분석 솔루션을 작업 영역에 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="99931-143">[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명하는 프로세스를 사용하여 작업 영역에 Azure SQL 분석 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="99931-144">Azure Portal에서 **새로 만들기**(+ 기호)를 클릭한 후 리소스 목록에서 **모니터링 + 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="99931-145">![모니터링 + 관리](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="99931-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="99931-146">**모니터링 + 관리** 목록에서 **모두 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="99931-147">**권장** 목록에서 **자세히**를 클릭한 후 새 목록에서 **Azure SQL Analytics(미리 보기)**를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="99931-148">![Azure SQL Analytics 솔루션](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="99931-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="99931-149">**Azure SQL Analytics(미리 보기)** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="99931-150">![만들기](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="99931-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="99931-151">**새 솔루션 만들기** 블레이드에서 솔루션을 추가할 작업 영역을 선택한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="99931-152">![작업 영역에 추가](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="99931-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="99931-153">Azure 구독을 여러 개 구성하려면</span><span class="sxs-lookup"><span data-stu-id="99931-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="99931-154">여러 구독을 지원하려면 [PowerShell을 사용하여 Azure 리소스 메트릭 로깅 사용](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)에서 PowerShell 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="99931-155">하나의 Azure 구독에서 다른 Azure 구독의 작업 영역으로 진단 데이터를 전송하는 스크립트를 실행할 때 작업 영역 리소스 ID를 매개 변수로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="99931-156">**예제**</span><span class="sxs-lookup"><span data-stu-id="99931-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="99931-157">솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="99931-157">Using the solution</span></span>

<span data-ttu-id="99931-158">솔루션을 작업 영역에 추가하면 Azure SQL Analytics 타일이 작업 영역에 추가되고 개요에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="99931-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="99931-159">타일은 솔루션이 연결된 Azure SQL 데이터베이스 및 Azure SQL 탄력적 풀 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99931-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Azure SQL Analytics 타일](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="99931-161">Azure SQL 분석 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="99931-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="99931-162">**Azure SQL 분석** 타일을 클릭하여 Azure SQL 분석 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="99931-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="99931-163">대시보드에는 아래 정의된 블레이드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="99931-164">각 블레이드에 최대 15개의 리소스(구독, 서버, 탄력적 풀 및 데이터베이스)가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="99931-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="99931-165">특정 리소스에 대한 대시보드를 열려면 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="99931-166">탄력적 풀 또는 데이터베이스에는 선택한 리소스에 대한 메트릭을 포함하는 차트가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="99931-167">차트를 클릭하여 로그 검색 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="99931-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="99931-168">블레이드</span><span class="sxs-lookup"><span data-stu-id="99931-168">Blade</span></span> | <span data-ttu-id="99931-169">설명</span><span class="sxs-lookup"><span data-stu-id="99931-169">Description</span></span> |
|---|---|
| <span data-ttu-id="99931-170">구독</span><span class="sxs-lookup"><span data-stu-id="99931-170">Subscriptions</span></span> | <span data-ttu-id="99931-171">연결된 서버, 풀 및 데이터베이스 수가 있는 구독 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="99931-172">서버</span><span class="sxs-lookup"><span data-stu-id="99931-172">Servers</span></span> | <span data-ttu-id="99931-173">연결된 풀 및 데이터베이스 수가 있는 서버 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="99931-174">탄력적 풀</span><span class="sxs-lookup"><span data-stu-id="99931-174">Elastic Pools</span></span> | <span data-ttu-id="99931-175">관찰된 기간에 최대 GB 및 eDTU가 있는 연결된 탄력적 풀 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="99931-176">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="99931-176">Databases</span></span> | <span data-ttu-id="99931-177">관찰된 기간에 최대 GB 및 DTU가 있는 연결된 데이터베이스 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="99931-178">데이터 분석 및 경고 만들기</span><span class="sxs-lookup"><span data-stu-id="99931-178">Analyze data and create alerts</span></span>

<span data-ttu-id="99931-179">Azure SQL Database 리소스에서 가져온 데이터와 경고를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="99931-180">다음은 경고 생성에 사용할 수 있는 몇 가지 유용한 [로그 검색](log-analytics-log-searches.md) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="99931-181">*Azure SQL Database에 대한 높은 DTU*</span><span class="sxs-lookup"><span data-stu-id="99931-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="99931-182">*Azure SQL Database 탄력적 풀에 대한 높은 DTU*</span><span class="sxs-lookup"><span data-stu-id="99931-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="99931-183">이러한 경고 기반 쿼리를 사용하여 Azure SQL Database와 탄력적 풀에 대한 특정 임계값에 대해 경고를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="99931-184">OMS 작업 영역에 대해 경고를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="99931-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="99931-185">작업 영역에 대해 경고를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="99931-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="99931-186">[OMS 포털](http://mms.microsoft.com/)로 이동하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="99931-187">솔루션에 대해 구성된 작업 영역을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="99931-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="99931-188">개요 페이지에서 **Azure SQL Analytics(미리 보기)** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="99931-189">예제 쿼리 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="99931-190">로그 검색에서 **경고**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="99931-191">![검색에서 경고 만들기](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="99931-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="99931-192">**경고 규칙 추가** 페이지에서 원하는 적절한 속성과 특정 임계값을 구성한 후 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="99931-193">![경고 규칙 추가](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="99931-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="99931-194">Azure SQL 분석 데이터에 대한 작업</span><span class="sxs-lookup"><span data-stu-id="99931-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="99931-195">예를 들어, 수행할 수 있는 가장 유용한 쿼리 중 하나는 모든 Azure 구독에서 모든 Azure SQL 탄력적 풀에 대한 DTU 사용률을 비교하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="99931-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="99931-196">DTU(데이터베이스 처리량 단위)는 Basic, Standard 및 Premium 데이터베이스 및 풀의 성능 수준에 대한 상대적인 용량을 설명하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="99931-197">DTU는 CPU, 메모리, 읽기 및 쓰기의 혼합 측정값을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="99931-198">DTU가 늘어나면 성능 수준에서 제공하는 기능도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="99931-199">예를 들어 5 DTU의 성능 수준은 1 DTU 성능 수준보다 5배 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="99931-200">각 서버 및 탄력적 풀에는 최대 DTU 할당량이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99931-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="99931-201">다음 로그 검색 쿼리를 실행하여 SQL Azure 탄력적 풀의 사용률이 높고 낮음을 쉽게 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="99931-202">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 위 쿼리가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="99931-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="99931-203">다음 예제를 보면 1개의 탄력적 풀이 거의 100% DTU의 높은 사용량을 보이는 반면 나머지는 사용량이 매우 적습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="99931-204">Azure 활동 로그를 사용하여 사용자 환경에서 잠재적인 최근 변경 내용을 추가로 조사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99931-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![로그 검색 결과 - 높은 사용률](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="99931-206">참고 항목</span><span class="sxs-lookup"><span data-stu-id="99931-206">See also</span></span>

- <span data-ttu-id="99931-207">Log Analytics의 [로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 Azure SQL 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="99931-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="99931-208">Azure SQL 데이터를 보여 주는 [사용자 고유의 대시보드 만들기](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="99931-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="99931-209">특정 Azure SQL 이벤트가 발생하는 경우의 [경고 만들기](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="99931-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
