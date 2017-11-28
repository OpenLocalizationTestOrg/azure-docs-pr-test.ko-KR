---
title: "Azure SQL Database에서 데이터베이스 성능 모니터링 | Microsoft Docs"
description: "Azure 도구 및 동적 관리 뷰를 사용하여 데이터베이스를 모니터링하기 위한 옵션에 대해 알아봅니다."
keywords: "데이터베이스 모니터링, 클라우드 데이터베이스 성능"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: e11ed3275413b428523eef78a5a89b537f6a4afc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a><span data-ttu-id="64e1e-104">Azure SQL 데이터베이스에서 데이터베이스 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="64e1e-104">Monitoring database performance in Azure SQL Database</span></span>
<span data-ttu-id="64e1e-105">Azure에서 SQL 데이터베이스의 성능 모니터링은 데이터베이스에 대해 선택한 데이터베이스 성능 수준을 기준으로 리소스 사용률을 모니터링하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-105">Monitoring the performance of a SQL database in Azure starts with monitoring the resource utilization relative to the level of database performance you choose.</span></span> <span data-ttu-id="64e1e-106">모니터링을 통해 데이터베이스에 과도한 용량이 있는지, 리소스가 최대값에 도달하는 문제가 있는지 확인한 후 데이터베이스의 성능 수준 및 [서비스 계층](sql-database-service-tiers.md)을 조정할 시기인지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-106">Monitoring helps you  determine whether your database has excess capacity or is having trouble because resources are maxed out, and then decide whether it's time to adjust the performance level and [service tier](sql-database-service-tiers.md) of your database.</span></span> <span data-ttu-id="64e1e-107">[Azure 포털](https://portal.azure.com)에서 그래픽 도구를 사용하거나 SQL [동적 관리 뷰](https://msdn.microsoft.com/library/ms188754.aspx)를 사용하여 데이터베이스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-107">You can monitor your database using graphical tools in the [Azure portal](https://portal.azure.com) or using SQL [dynamic management views](https://msdn.microsoft.com/library/ms188754.aspx).</span></span>

## <a name="monitor-databases-using-the-azure-portal"></a><span data-ttu-id="64e1e-108">Azure 포털을 사용하여 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="64e1e-108">Monitor databases using the Azure portal</span></span>
<span data-ttu-id="64e1e-109">[Azure 포털](https://portal.azure.com/)에서 데이터베이스를 선택하고 **모니터링** 차트를 클릭하여 단일 데이터베이스의 사용률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-109">In the [Azure portal](https://portal.azure.com/), you can monitor a single database’s utilization by selecting your database and clicking the **Monitoring** chart.</span></span> <span data-ttu-id="64e1e-110">그러면 **메트릭** 창이 나타나며 **차트 편집** 단추를 클릭하면 이 창을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-110">This brings up a **Metric** window that you can change by clicking the **Edit chart** button.</span></span> <span data-ttu-id="64e1e-111">다음 메트릭을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-111">Add the following metrics:</span></span>

* <span data-ttu-id="64e1e-112">CPU 비율</span><span class="sxs-lookup"><span data-stu-id="64e1e-112">CPU percentage</span></span>
* <span data-ttu-id="64e1e-113">DTU 비율</span><span class="sxs-lookup"><span data-stu-id="64e1e-113">DTU percentage</span></span>
* <span data-ttu-id="64e1e-114">데이터 IO 비율</span><span class="sxs-lookup"><span data-stu-id="64e1e-114">Data IO percentage</span></span>
* <span data-ttu-id="64e1e-115">데이터베이스 크기 비율</span><span class="sxs-lookup"><span data-stu-id="64e1e-115">Database size percentage</span></span>

<span data-ttu-id="64e1e-116">이러한 메트릭을 추가한 후 **메트릭** 창의 세부 정보가 포함된 **모니터링** 차트에서 메트릭을 계속 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-116">Once you’ve added these metrics, you can continue to view them in the **Monitoring** chart with more details on the **Metric** window.</span></span> <span data-ttu-id="64e1e-117">네 가지 메트릭 모두 데이터베이스의 **DTU** 를 기준으로 평균 사용률 비율을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-117">All four metrics show the average utilization percentage relative to the **DTU** of your database.</span></span> <span data-ttu-id="64e1e-118">DTU에 대한 자세한 내용은 [서비스 계층](sql-database-service-tiers.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-118">See the [service tiers](sql-database-service-tiers.md) article for details about DTUs.</span></span>

![데이터베이스 성능의 서비스 계층 모니터링.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

<span data-ttu-id="64e1e-120">성능 메트릭에 대한 경고를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-120">You can also configure alerts on the performance metrics.</span></span> <span data-ttu-id="64e1e-121">**메트릭** 창에서 **경고 추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-121">Click the **Add alert** button in the **Metric** window.</span></span> <span data-ttu-id="64e1e-122">마법사를 따라 경고를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-122">Follow the wizard to configure your alert.</span></span> <span data-ttu-id="64e1e-123">메트릭이 특정 임계값을 초과하거나 메트릭이 특정 임계값보다 낮은 경우 경고하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-123">You have the option to alert if the metrics exceed a certain threshold or if the metric falls below a certain threshold.</span></span>

<span data-ttu-id="64e1e-124">예를 들어 데이터베이스에 대한 워크로드가 확장될 것으로 예상되면 데이터베이스가 성능 메트릭의 80%에 도달할 때마다 이메일 경고를 보내도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-124">For example, if you expect the workload on your database to grow, you can choose to configure an email alert whenever your database reaches 80% on any of the performance metrics.</span></span> <span data-ttu-id="64e1e-125">다음 높은 성능 수준으로 전환해야 할 수 있는 시기를 알 수 있도록 이 기능을 조기 경고로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-125">You can use this as an early warning to figure out when you might have to switch to the next higher performance level.</span></span>

<span data-ttu-id="64e1e-126">성능 메트릭이 더 낮은 성능 수준으로 다운그레이드할 수 있는지 여부를 판단하는 데 도움이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-126">The performance metrics can also help you determine if you are able to downgrade to a lower performance level.</span></span> <span data-ttu-id="64e1e-127">표준 S2 데이터베이스를 사용하고 있는데 모든 성능 메트릭에서 지정한 시기에 데이터베이스가 평균적으로 10% 이하를 사용하는 것으로 나타난다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-127">Assume you are using a Standard S2 database and all performance metrics show that the database on average does not use more than 10% at any given time.</span></span> <span data-ttu-id="64e1e-128">데이터베이스가 표준 S1에서 잘 작동할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-128">It is likely that the database will work well in Standard S1.</span></span> <span data-ttu-id="64e1e-129">그러나 더 낮은 성능 수준으로 이동하도록 결정하기 전에 갑자기 증가하거나 변동하는 워크로드에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-129">However, be aware of workloads that spike or fluctuate before making the decision to move to a lower performance level.</span></span>

## <a name="monitor-databases-using-dmvs"></a><span data-ttu-id="64e1e-130">DMV를 사용하여 데이터베이스 모니터링</span><span class="sxs-lookup"><span data-stu-id="64e1e-130">Monitor databases using DMVs</span></span>
<span data-ttu-id="64e1e-131">포털에 노출된 것과 같은 메트릭을 서버의 논리 **마스터** 데이터베이스에 있는 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx), 사용자 데이터베이스의 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) 등의 시스템 뷰를 통해 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-131">The same metrics that are exposed in the portal are also available through system views: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) in the logical **master** database of your server, and [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) in the user database.</span></span> <span data-ttu-id="64e1e-132">더 오랜 개간 동안 덜 자세한 데이터를 모니터링해야 하는 경우 **sys.resource_stats**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-132">Use **sys.resource_stats** if you need to monitor less granular data across a longer period of time.</span></span> <span data-ttu-id="64e1e-133">더 작은 시간 범위의 자세한 데이터를 모니터링해야 하는 경우 **sys.dm_db_resource_stats**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-133">Use **sys.dm_db_resource_stats** if you need to monitor more granular data within a smaller time frame.</span></span> <span data-ttu-id="64e1e-134">자세한 내용은 [Azure SQL 데이터베이스 성능 지침](sql-database-single-database-monitor.md#monitor-resource-use)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-134">For more information, see [Azure SQL Database Performance Guidance](sql-database-single-database-monitor.md#monitor-resource-use).</span></span>

> [!NOTE]
> <span data-ttu-id="64e1e-135">**sys.dm_db_resource_stats**는 Web 및 Business Edition 데이터베이스에서 사용할 때 빈 결과 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-135">**sys.dm_db_resource_stats** returns an empty result set when used in Web and Business edition databases, which are retired.</span></span>
>
>

### <a name="monitor-resource-use"></a><span data-ttu-id="64e1e-136">리소스 사용 모니터링</span><span class="sxs-lookup"><span data-stu-id="64e1e-136">Monitor resource use</span></span>

<span data-ttu-id="64e1e-137">[SQL Database Query Performance Insight](sql-database-query-performance.md) 및 [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx)를 사용하여 리소스 사용량을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-137">You can monitor resource usage using [SQL Database Query Performance Insight](sql-database-query-performance.md) and [Query Store](https://msdn.microsoft.com/library/dn817826.aspx).</span></span>

<span data-ttu-id="64e1e-138">또한 다음 두 가지 뷰를 사용하여 사용을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-138">You can also monitor usage using these two views:</span></span>

* [<span data-ttu-id="64e1e-139">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="64e1e-139">sys.dm_db_resource_stats</span></span>](https://msdn.microsoft.com/library/dn800981.aspx)
* [<span data-ttu-id="64e1e-140">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="64e1e-140">sys.resource_stats</span></span>](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a><span data-ttu-id="64e1e-141">sys.dm_db_resource_stats</span><span class="sxs-lookup"><span data-stu-id="64e1e-141">sys.dm_db_resource_stats</span></span>
<span data-ttu-id="64e1e-142">모든 SQL Database에 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) 뷰를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-142">You can use the [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) view in every SQL database.</span></span> <span data-ttu-id="64e1e-143">**sys.dm_db_resource_stats** 뷰는 서비스 계층과 관련된 최근 리소스 사용 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-143">The **sys.dm_db_resource_stats** view shows recent resource use data relative to the service tier.</span></span> <span data-ttu-id="64e1e-144">CPU, 데이터 I/O, 로그 쓰기 및 메모리의 평균 백분율을 15초마다 기록하고 1시간 동안 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-144">Average percentages for CPU, data I/O, log writes, and memory are recorded every 15 seconds and are maintained for 1 hour.</span></span>

<span data-ttu-id="64e1e-145">이 뷰는 리소스 사용률에 대한 훨씬 구체적인 정보를 제공하므로 현재 상태 분석 또는 문제 해결에 **sys.dm_db_resource_stats**를 먼저 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-145">Because this view provides a more granular look at resource use, use **sys.dm_db_resource_stats** first for any current-state analysis or troubleshooting.</span></span> <span data-ttu-id="64e1e-146">예를 들어 이 쿼리는 지난 시간 동안 현재 데이터베이스의 평균 및 최대 리소스 사용률을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-146">For example, this query shows the average and maximum resource use for the current database over the past hour:</span></span>

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

<span data-ttu-id="64e1e-147">다른 쿼리는 [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)의 예를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-147">For other queries, see the examples in [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).</span></span>

#### <a name="sysresourcestats"></a><span data-ttu-id="64e1e-148">sys.resource_stats</span><span class="sxs-lookup"><span data-stu-id="64e1e-148">sys.resource_stats</span></span>
<span data-ttu-id="64e1e-149">**마스터** 데이터베이스의 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) 뷰에는 특정 서비스 계층 및 성능 수준에서 SQL Database의 성능 수준을 모니터링할 수 있는 추가 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-149">The [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view in the **master** database has additional information that can help you monitor the performance of your SQL database at its specific service tier and performance level.</span></span> <span data-ttu-id="64e1e-150">데이터는 5분마다 수집되어 약 35일 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-150">The data is collected every 5 minutes and is maintained for approximately 35 days.</span></span> <span data-ttu-id="64e1e-151">이 뷰는 SQL Database가 리소스를 사용하는 방법에 대한 장기적인 기록 분석에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-151">This view is useful for a longer-term historical analysis of how your SQL database uses resources.</span></span>

<span data-ttu-id="64e1e-152">다음 그래프는 한 주 동안 각 시간당 P2 성능 수준의 Premium 데이터베이스에 대한 CPU 리소스 사용률을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-152">The following graph shows the CPU resource use for a Premium database with the P2 performance level for each hour in a week.</span></span> <span data-ttu-id="64e1e-153">이 그래프는 월요일부터 5근무일과 응용 프로그램 사용량이 훨씬 적은 주말까지 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-153">This graph starts on a Monday, shows 5 work days, and then shows a weekend, when much less happens on the application.</span></span>

![SQL Database 리소스 사용](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

<span data-ttu-id="64e1e-155">이 데이터베이스의 현재 최고 CPU 부하는 P2 성능 수준에 비해 약 50% 더 많습니다(화요일 낮).</span><span class="sxs-lookup"><span data-stu-id="64e1e-155">From the data, this database currently has a peak CPU load of just over 50 percent CPU use relative to the P2 performance level (midday on Tuesday).</span></span> <span data-ttu-id="64e1e-156">CPU가 응용 프로그램의 리소스 프로필에서 가장 지배적인 요인인 경우 P2가 항상 워크로드를 충족하는 데 적합한 성능 수준임을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-156">If CPU is the dominant factor in the application’s resource profile, then you might decide that P2 is the right performance level to guarantee that the workload always fits.</span></span> <span data-ttu-id="64e1e-157">응용 프로그램이 시간이 지남에 따라 성장할 것으로 예상되는 경우 응용 프로그램이 성능 수준 한도에 도달하지 않도록 추가 리소스 버퍼를 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-157">If you expect an application to grow over time, it's a good idea to have an extra resource buffer so that the application doesn't ever reach the performance-level limit.</span></span> <span data-ttu-id="64e1e-158">성능 수준을 높이면 특히 대기 시간이 중요한 환경에서 데이터베이스가 요청을 효과적으로 처리하므로 충분한 능력을 갖고 있지 않은 경우 발생할 수 있는 고객에게 보이는 오류를 방지하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-158">If you increase the performance level, you can help avoid customer-visible errors that might occur when a database doesn't have enough power to process requests effectively, especially in latency-sensitive environments.</span></span> <span data-ttu-id="64e1e-159">예를 들어 데이터베이스 호출의 결과를 기반으로 웹 페이지를 표시하는 응용 프로그램을 지원하는 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-159">An example is a database that supports an application that paints webpages based on the results of database calls.</span></span>

<span data-ttu-id="64e1e-160">다른 응용 프로그램 유형은 동일한 그래프를 다르게 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-160">Other application types might interpret the same graph differently.</span></span> <span data-ttu-id="64e1e-161">예를 들어 응용 프로그램에서 매일 급여 데이터를 처리하고 동일한 차트를 사용하는 경우와 같은 "일괄 처리 작업" 모델은 P1 성능 수준으로 충분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-161">For example, if an application tries to process payroll data each day and has the same chart, this kind of "batch job" model might do fine at a P1 performance level.</span></span> <span data-ttu-id="64e1e-162">P2 성능 수준은 200 DTU이지만 P1 성능 수준은 100 DTU입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-162">The P1 performance level has 100 DTUs compared to 200 DTUs at the P2 performance level.</span></span> <span data-ttu-id="64e1e-163">P1 성능 수준은 P2 성능 수준의 절반의 성능만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-163">The P1 performance level provides half the performance of the P2 performance level.</span></span> <span data-ttu-id="64e1e-164">따라서 P2에서 CPU 사용의 50%는 P1에서 100% CPU 사용과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-164">So, 50 percent of CPU use in P2 equals 100 percent CPU use in P1.</span></span> <span data-ttu-id="64e1e-165">응용 프로그램에 시간 제한이 없는 경우 작업이 오늘 완료되기만 한다면 2시간이 소요되든 또는 2.5시간이 소요되든 중요하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-165">If the application does not have timeouts, it might not matter if a job takes 2 hours or 2.5 hours to finish, if it gets done today.</span></span> <span data-ttu-id="64e1e-166">이 범주의 응용 프로그램은 아마 P1 성능 수준을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-166">An application in this category probably can use a P1 performance level.</span></span> <span data-ttu-id="64e1e-167">하루 중 리소스 사용량이 낮은 시간대가 있다는 사실을 활용할 수 있습니다. 즉, "최고" 시간대의 작업을 하루 중 사용량이 낮은 시간대 중 하나로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-167">You can take advantage of the fact that there are periods of time during the day when resource use is lower, so that any "big peak" might spill over into one of the troughs later in the day.</span></span> <span data-ttu-id="64e1e-168">작업을 매일 정시에 완료할 수 있는 경우 이러한 종류의 응용 프로그램에는 P1 성능 수준이 적합하며 비용도 절감할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-168">The P1 performance level might be good for that kind of application (and save money), as long as the jobs can finish on time each day.</span></span>

<span data-ttu-id="64e1e-169">Azure SQL Database는 각 서버에 있는 **마스터** 데이터베이스의 **sys.resource_stats** 뷰로 각 활성 데이터베이스에 사용된 리소스 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-169">Azure SQL Database exposes consumed resource information for each active database in the **sys.resource_stats** view of the **master** database in each server.</span></span> <span data-ttu-id="64e1e-170">표의 데이터는 5분 간격으로 집계되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-170">The data in the table is aggregated for 5-minute intervals.</span></span> <span data-ttu-id="64e1e-171">Basic, Standard, Premium 서비스 계층에서 데이터가 테이블에 표시될 때까지 5분 이상이 소요될 수 있어 이 데이터는 거의 실시간에 가까운 분석보다 기록 분석에 더 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-171">With the Basic, Standard, and Premium service tiers, the data can take more than 5 minutes to appear in the table, so this data is more useful for historical analysis rather than near-real-time analysis.</span></span> <span data-ttu-id="64e1e-172">**sys.resource_stats** 뷰에 대한 쿼리는 데이터베이스의 최근 기록을 보여주며 선택한 예약이 필요 시 원하는 성능을 제공했는지 여부를 검증합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-172">Query the **sys.resource_stats** view to see the recent history of a database and to validate whether the reservation you chose delivered the performance you want when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="64e1e-173">다음 예제에서 **sys.resource_stats**를 쿼리하려면 논리 SQL Database 서버의 **마스터** 데이터베이스에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-173">You must be connected to the **master** database of your logical SQL database server to query **sys.resource_stats** in the following examples.</span></span>
> 
> 

<span data-ttu-id="64e1e-174">이 예제에서는 이 뷰의 데이터가 표시되는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-174">This example shows you how the data in this view is exposed:</span></span>

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![sys.resource_stats 카탈로그 뷰](./media/sql-database-performance-guidance/sys_resource_stats.png)

<span data-ttu-id="64e1e-176">다음 예제에서는 **sys.resource_stats** 카탈로그 뷰를 사용하여 SQL Database에서 리소스를 사용하는 방법에 대한 정보를 얻을 수 있는 다른 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-176">The next example shows you different ways that you can use the **sys.resource_stats** catalog view to get information about how your SQL database uses resources:</span></span>

1. <span data-ttu-id="64e1e-177">데이터베이스 userdb1에서 지난 주의 리소스 사용을 확인하고자 할 때 이 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-177">To look at the past week’s resource use for the database userdb1, you can run this query:</span></span>
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. <span data-ttu-id="64e1e-178">워크로드가 성능 수준에 얼마나 적합한지 평가하려면 리소스 메트릭의 각 측면(CPU, 읽기, 쓰기, 작업자 수, 세션 수)까지 집중 분석해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-178">To evaluate how well your workload fits the performance level, you need to drill down into each aspect of the resource metrics: CPU, reads, writes, number of workers, and number of sessions.</span></span> <span data-ttu-id="64e1e-179">다음은 이러한 리소스 메트릭의 평균값 및 최대값에 대해 보고하기 위해 **sys.resource_stats**를 사용하여 수정한 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-179">Here's a revised query using **sys.resource_stats** to report the average and maximum values of these resource metrics:</span></span>
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. <span data-ttu-id="64e1e-180">각 리소스 메트릭의 평균값 및 최대값에 대한 이 정보를 사용하여 워크로드가 선택한 성능 수준에 얼마나 적합한지 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-180">With this information about the average and maximum values of each resource metric, you can assess how well your workload fits into the performance level you chose.</span></span> <span data-ttu-id="64e1e-181">일반적으로 **sys.resource_stats**의 평균값은 대상 크기에 맞게 사용하기에 적합한 기준선을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-181">Usually, average values from **sys.resource_stats** give you a good baseline to use against the target size.</span></span> <span data-ttu-id="64e1e-182">기본 측정 기준이 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-182">It should be your primary measurement stick.</span></span> <span data-ttu-id="64e1e-183">예를 들어 S2 성능 수준과 함께Standard 서비스 계층을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-183">For an example, you might be using the Standard service tier with S2 performance level.</span></span> <span data-ttu-id="64e1e-184">CPU 및 I/O 읽기와 쓰기에 대한 평균 사용 비율은 40% 미만, 평균 작업자 수는 50 미만, 평균 세션 수는 200 미만입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-184">The average use percentages for CPU and I/O reads and writes are below 40 percent, the average number of workers is below 50, and the average number of sessions is below 200.</span></span> <span data-ttu-id="64e1e-185">사용자의 워크로드는 S1 성능 수준에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-185">Your workload might fit into the S1 performance level.</span></span> <span data-ttu-id="64e1e-186">데이터베이스가 작업자 및 세션 한도 이내에서 적합한지 여부를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-186">It's easy to see whether your database fits in the worker and session limits.</span></span> <span data-ttu-id="64e1e-187">데이터베이스가 CPU, 읽기, 쓰기 기준의 낮은 성능 수준에 적합한지 확인하려면 낮은 성능 수준의 DTU 수를 현재 성능 수준의 DTU 수로 나눈 다음 결과에 100을 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-187">To see whether a database fits into a lower performance level with regards to CPU, reads, and writes, divide the DTU number of the lower performance level by the DTU number of your current performance level, and then multiply the result by 100:</span></span>
   
    <span data-ttu-id="64e1e-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span><span class="sxs-lookup"><span data-stu-id="64e1e-188">**S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**</span></span>
   
    <span data-ttu-id="64e1e-189">결과는 백분율로 표시한 두 성능 수준 간 상대적 성능 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-189">The result is the relative performance difference between the two performance levels in percentage.</span></span> <span data-ttu-id="64e1e-190">리소스 사용이 이 금액을 초과하지 않는 경우 워크로드가 낮은 성능 수준에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-190">If your resource use doesn't exceed this amount, your workload might fit into the lower performance level.</span></span> <span data-ttu-id="64e1e-191">하지만 모든 범위의 리소스 사용 값을 살펴보고 데이터베이스 워크로드가 낮은 성능 수준에 적합한 빈도를 백분율로 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-191">However, you need to look at all ranges of resource use values, and determine, by percentage, how often your database workload would fit into the lower performance level.</span></span> <span data-ttu-id="64e1e-192">다음 쿼리는 이 예에서 계산된 40%의 임계값을 기준으로 리소스 규격당 적합률을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-192">The following query outputs the fit percentage per resource dimension, based on the threshold of 40 percent that we calculated in this example:</span></span>
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="64e1e-193">데이터베이스의 SLO(서비스 수준 목표)를 기준으로 워크로드가 낮은 성능 수준에 적합한지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-193">Based on your database service level objective (SLO), you can decide whether your workload fits into the lower performance level.</span></span> <span data-ttu-id="64e1e-194">데이터베이스 워크로드 SLO가 99.9%이고 앞의 쿼리에서 세 가지 리소스 규격에 대해 99.9%보다 큰 값을 반환할 경우 워크로드가 낮은 성능 수준에 적합할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-194">If your database workload SLO is 99.9 percent and the preceding query returns values greater than 99.9 percent for all three resource dimensions, your workload likely fits into the lower performance level.</span></span>
   
    <span data-ttu-id="64e1e-195">적합률을 살펴보면 SLO를 충족하기 위해 상위 성능 수준으로 이동해야 하는지 여부를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-195">Looking at the fit percentage also gives you insight into whether you should move to the next higher performance level to meet your SLO.</span></span> <span data-ttu-id="64e1e-196">예를 들어 userdb1에서 지난 주에 대한 CPU 사용률은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-196">For example, userdb1 shows the following CPU use for the past week:</span></span>
   
   | <span data-ttu-id="64e1e-197">평균 CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="64e1e-197">Average CPU percent</span></span> | <span data-ttu-id="64e1e-198">최대 CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="64e1e-198">Maximum CPU percent</span></span> |
   | --- | --- |
   | <span data-ttu-id="64e1e-199">24.5</span><span class="sxs-lookup"><span data-stu-id="64e1e-199">24.5</span></span> |<span data-ttu-id="64e1e-200">100.00</span><span class="sxs-lookup"><span data-stu-id="64e1e-200">100.00</span></span> |
   
    <span data-ttu-id="64e1e-201">평균 CPU는 성능 수준 한도의 약 1/4이며 데이터베이스 성능 수준에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-201">The average CPU is about a quarter of the limit of the performance level, which would fit well into the performance level of the database.</span></span> <span data-ttu-id="64e1e-202">하지만 최대값은 데이터베이스가 성능 수준 한도에 도달함을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-202">But, the maximum value shows that the database reaches the limit of the performance level.</span></span> <span data-ttu-id="64e1e-203">다음 상위 성능 수준으로 이동해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="64e1e-203">Do you need to move to the next higher performance level?</span></span> <span data-ttu-id="64e1e-204">워크로드가 100%에 도달하는 횟수를 살펴보고 데이터베이스 워크로드 SLO와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-204">Look at how many times your workload reaches 100 percent, and then compare it to your database workload SLO.</span></span>
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    <span data-ttu-id="64e1e-205">이 쿼리에서 세 가지 리소스 규격에 대해 99.9% 미만의 값을 반환할 경우 다음 상위 성능 수준으로 이동하거나 응용 프로그램 튜닝 기술을 사용하여 SQL Database에서 부하를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-205">If this query returns a value less than 99.9 percent for any of the three resource dimensions, consider either moving to the next higher performance level or use application-tuning techniques to reduce the load on the SQL database.</span></span>
4. <span data-ttu-id="64e1e-206">이 연습에서는 향후 예상되는 워크로드 증가도 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-206">This exercise also considers your projected workload increase in the future.</span></span>

<span data-ttu-id="64e1e-207">탄력적 풀의 경우 이 섹션에서 설명하는 기법을 사용하여 풀의 개별 데이터베이스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-207">For elastic pools, you can monitor individual databases in the pool with the techniques described in this section.</span></span> <span data-ttu-id="64e1e-208">하지만 전체적으로 풀을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-208">But you can also monitor the pool as a whole.</span></span> <span data-ttu-id="64e1e-209">자세한 내용은 [탄력적 풀 모니터링 및 관리](sql-database-elastic-pool-manage-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-209">For information, see [Monitor and manage an elastic pool](sql-database-elastic-pool-manage-portal.md).</span></span>


### <a name="maximum-concurrent-requests"></a><span data-ttu-id="64e1e-210">동시 요청이 최대인 경우</span><span class="sxs-lookup"><span data-stu-id="64e1e-210">Maximum concurrent requests</span></span>
<span data-ttu-id="64e1e-211">동시 요청 수를 보려면 SQL Database에서 이 Transact-SQL 쿼리를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-211">To see the number of concurrent requests, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

<span data-ttu-id="64e1e-212">온-프레미스 SQL Server 데이터베이스의 워크로드를 분석하려면 이 쿼리를 수정하여 분석할 특정 데이터베이스에서 필터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-212">To analyze the workload of an on-premises SQL Server database, modify this query to filter on the specific database you want to analyze.</span></span> <span data-ttu-id="64e1e-213">예를 들어 MyDatabase라는 온-프레미스 데이터베이스가 있다면 이 Transact-SQL 쿼리는 해당 데이터베이스의 동시 요청 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-213">For example, if you have an on-premises database named MyDatabase, this Transact-SQL query returns the count of concurrent requests in that database:</span></span>

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

<span data-ttu-id="64e1e-214">이는 단일 시점의 스냅숏일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-214">This is just a snapshot at a single point in time.</span></span> <span data-ttu-id="64e1e-215">워크로드 및 동시 요청 요구 사항을 더 깊이 이해하려면 시간 변화에 따라 여러 샘플을 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-215">To get a better understanding of your workload and concurrent request requirements, you'll need to collect many samples over time.</span></span>

### <a name="maximum-concurrent-logins"></a><span data-ttu-id="64e1e-216">최대 동시 로그인 수</span><span class="sxs-lookup"><span data-stu-id="64e1e-216">Maximum concurrent logins</span></span>
<span data-ttu-id="64e1e-217">사용자 및 응용 프로그램 패턴을 분석하여 로그인 빈도를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-217">You can analyze your user and application patterns to get an idea of the frequency of logins.</span></span> <span data-ttu-id="64e1e-218">또한 테스트 환경에서 실제 부하를 실행하여 이 문서에서 설명한 이 한도 또는 기타 한도에 도달하지 않도록 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-218">You also can run real-world loads in a test environment to make sure that you're not hitting this or other limits we discuss in this article.</span></span> <span data-ttu-id="64e1e-219">동시 로그인 수 또는 기록을 표시할 수 있는 단일 쿼리 또는 동적 관리 뷰(DMV)는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-219">There isn’t a single query or dynamic management view (DMV) that can show you concurrent login counts or history.</span></span>

<span data-ttu-id="64e1e-220">여러 클라이언트에서 동일한 연결 문자열을 사용하는 경우 서비스에서는 각 로그인을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-220">If multiple clients use the same connection string, the service authenticates each login.</span></span> <span data-ttu-id="64e1e-221">10명의 사용자가 동일한 사용자 이름 및 암호를 사용하여 데이터베이스에 동시에 연결하는 경우 동시 로그인 수는 10개가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-221">If 10 users simultaneously connect to a database by using the same username and password, there would be 10 concurrent logins.</span></span> <span data-ttu-id="64e1e-222">이 한도는 로그인 및 인증 기간에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-222">This limit applies only to the duration of the login and authentication.</span></span> <span data-ttu-id="64e1e-223">따라서 동일한 10명의 사용자가 특정 데이터베이스에 순차적으로 연결하는 경우 동시 로그인 수는 절대로 1보다 높을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-223">If the same 10 users connect to the database sequentially, the number of concurrent logins would never be greater than 1.</span></span>

> [!NOTE]
> <span data-ttu-id="64e1e-224">현재 이 한도는 탄력적 풀의 데이터베이스에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-224">Currently, this limit does not apply to databases in elastic pools.</span></span>
> 
> 

### <a name="maximum-sessions"></a><span data-ttu-id="64e1e-225">최대 세션 수</span><span class="sxs-lookup"><span data-stu-id="64e1e-225">Maximum sessions</span></span>
<span data-ttu-id="64e1e-226">현재 활성 세션 수를 보려면 SQL Database에서 이 Transact-SQL 쿼리를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-226">To see the number of current active sessions, run this Transact-SQL query on your SQL database:</span></span>

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

<span data-ttu-id="64e1e-227">온-프레미스 SQL Server 워크로드를 분석하려는 경우 특정 데이터베이스에 집중하도록 쿼리를 수정하세요.</span><span class="sxs-lookup"><span data-stu-id="64e1e-227">If you're analyzing an on-premises SQL Server workload, modify the query to focus on a specific database.</span></span> <span data-ttu-id="64e1e-228">이 쿼리는 데이터베이스를 Azure SQL Database로 이동을 고려할 때 가능한 세션 요구 사항을 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-228">This query helps you determine possible session needs for the database if you are considering moving it to Azure SQL Database.</span></span>

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

<span data-ttu-id="64e1e-229">역시 이러한 쿼리도 지정 시간 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-229">Again, these queries return a point-in-time count.</span></span> <span data-ttu-id="64e1e-230">시간이 지남에 따라 여러 샘플을 수집하는 경우 자신의 세션 사용을 잘 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-230">If you collect multiple samples over time, you’ll have the best understanding of your session use.</span></span>

<span data-ttu-id="64e1e-231">SQL Database 분석의 경우 [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) 뷰를 쿼리하고 **active_session_count** 열을 검토하여 세션에 대한 통계 자료를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64e1e-231">For SQL Database analysis, you can get historical statistics on sessions by querying the [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) view and reviewing the **active_session_count** column.</span></span> 
