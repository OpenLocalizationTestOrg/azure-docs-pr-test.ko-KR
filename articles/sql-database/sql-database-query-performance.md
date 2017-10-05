---
title: "Azure SQL Database에 대한 쿼리 성능 Insight | Microsoft Docs"
description: "쿼리 성능 모니터링은 Azure SQL 데이터베이스에 대한 대부분의 CPU 사용 쿼리를 식별합니다."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="170cc-103">Azure SQL 데이터베이스 Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="170cc-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="170cc-104">관련 데이터베이스의 성능을 관리하고 튜닝하는 것은 많은 전문 지식과 시간 투자를 필요로 하는 어려운 일입니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="170cc-105">Query Performance Insight를 통해 다음을 제공하여 데이터베이스 성능 문제 해결 시간을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="170cc-106">데이터베이스 리소스(DTU) 사용에 대한 보다 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="170cc-107">CPU/기간/실행 횟수별 최상위 쿼리는 향상된 성능을 위해 잠재적으로 조정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="170cc-108">쿼리에 대한 세부 정보로 드릴다운하는 기능으로, 리소스 사용률에 대한 텍스트 및 기록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="170cc-109">[SQL Azure 데이터베이스 관리자](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="170cc-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="170cc-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="170cc-110">Prerequisites</span></span>
* <span data-ttu-id="170cc-111">Query Performance Insight를 위해서는 데이터베이스에서 [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx) 가 활성 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="170cc-112">쿼리 저장소가 실행되지 않는 경우 저장소를 켜라는 포털 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="170cc-113">권한</span><span class="sxs-lookup"><span data-stu-id="170cc-113">Permissions</span></span>
<span data-ttu-id="170cc-114">Query Performance Insight를 사용하려면 다음 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="170cc-115">최상위 리소스 사용 쿼리 및 차트를 보려면 **판독기**, **소유자**, **참여자**, **SQL DB 참여자** 또는 **SQL Server 참여자** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="170cc-116">쿼리 텍스트를 보려면 **소유자**, **참여자**, **SQL DB 참여자** 또는 **SQL Server 참여자** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="170cc-117">Query Performance Insight 사용</span><span class="sxs-lookup"><span data-stu-id="170cc-117">Using Query Performance Insight</span></span>
<span data-ttu-id="170cc-118">Query Performance Insight는 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="170cc-119">[Azure 포털](https://portal.azure.com/) 을 열고 검사하려는 데이터베이스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="170cc-120">왼쪽 메뉴의 지원 및 문제 해결에서 "Query Performance Insight"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="170cc-121">첫 번째 탭에서 최상위 리소스 사용 쿼리의 목록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="170cc-122">해당하는 세부 정보를 보려면 개별 쿼리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="170cc-123">[SQL Azure 데이터베이스 관리자](sql-database-advisor.md) 를 열고 권장 사항을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="170cc-124">슬라이더를 또는 확대/축소 아이콘을 사용하여 관찰 간격을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![성능 대시보드](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="170cc-126">Query Performance Insight를 제공하는 SQL 데이터베이스용 쿼리 저장소로 데이터를 캡처하는 데 몇 시간이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="170cc-127">데이터베이스에 아무런 작업이 없거나 쿼리 저장소가 특정 기간 동안 비활성 상태였던 경우 해당 기간을 표시할 때 차트가 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="170cc-128">실행하지 않는 경우 언제든지 쿼리 저장소를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="170cc-129">최상위 CPU 소비 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="170cc-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="170cc-130">[포털](http://portal.azure.com) 에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="170cc-131">SQL 데이터베이스로 이동한 후 **모든 설정** > **지원 + 문제 해결** > **Query Performance Insight**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query Performance Insight][1]
   
    <span data-ttu-id="170cc-133">최상위 쿼리 뷰가 열리고 최상위 CPU 사용 쿼리가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="170cc-134">자세한 내용은 차트 주위를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-134">Click around the chart for details.</span></span><br><span data-ttu-id="170cc-135">위쪽 줄에는 데이터베이스에 대한 전체 DTU%가 표시되고 막대에는 선택한 기간 중에 선택한 쿼리에서 사용된 CPU%가 표시됩니다. 예를 들어 **지난주**를 선택하면 각 막대는 1일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![최상위 쿼리][2]
   
    <span data-ttu-id="170cc-137">아래 그리드는 표시되는 쿼리에 대해 집계된 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="170cc-138">쿼리 ID – 데이터베이스 내 쿼리의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="170cc-139">예측 가능한 간격 동안 쿼리당 CPU입니다(집계 함수에 따라 다름).</span><span class="sxs-lookup"><span data-stu-id="170cc-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="170cc-140">쿼리당 기간입니다(집계 함수에 따라 다름).</span><span class="sxs-lookup"><span data-stu-id="170cc-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="170cc-141">특정 쿼리에 대한 총 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="170cc-142">확인란을 사용하여 개별 쿼리를 선택하거나 지워 차트에서 포함하거나 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="170cc-143">데이터가 최신 상태가 아닌 경우 **새로 고침** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="170cc-144">슬라이더 및 확대/축소 단추를 사용하여 관찰 간격을 변경하고 스파이크를 조사할 수 있습니다. ![설정](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="170cc-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="170cc-145">필요에 따라 다른 보기를 원할 경우 **사용자 지정** 탭을 선택하고 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="170cc-146">메트릭(CPU, 기간, 실행 횟수)</span><span class="sxs-lookup"><span data-stu-id="170cc-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="170cc-147">시간 간격(지난 24시간, 지난주, 지난달)</span><span class="sxs-lookup"><span data-stu-id="170cc-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="170cc-148">쿼리 수</span><span class="sxs-lookup"><span data-stu-id="170cc-148">Number of queries.</span></span>
   * <span data-ttu-id="170cc-149">집계 함수</span><span class="sxs-lookup"><span data-stu-id="170cc-149">Aggregation function.</span></span>
     
     ![설정](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="170cc-151">개별 쿼리 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="170cc-151">Viewing individual query details</span></span>
<span data-ttu-id="170cc-152">쿼리 세부 정보를 보려면:</span><span class="sxs-lookup"><span data-stu-id="170cc-152">To view query details:</span></span>

1. <span data-ttu-id="170cc-153">맨 위 쿼리 목록에서 쿼리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-153">Click any query in the list of top queries.</span></span>
   
    ![세부 정보](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="170cc-155">세부 정보 보기가 열리고 쿼리 CPU 사용/기간/실행 횟수가 시간에 따라 분석됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="170cc-156">자세한 내용은 차트 주위를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="170cc-157">맨 위 차트에는 전체 데이터베이스 DTU %가 선으로 표시되고, 선택한 쿼리에서 사용되는 CPU %가 막대로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="170cc-158">두 번째 차트에는 선택한 쿼리의 전체 기간이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="170cc-159">맨 아래 차트에는 선택한 쿼리의 전체 실행 횟수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![쿼리 세부 정보][3]
4. <span data-ttu-id="170cc-161">필요에 따라 슬라이더, 확대/축소 단추를 사용하거나 **설정** 을 클릭하여 쿼리 데이터 표시 방법을 사용자 지정하거나 다른 기간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="170cc-162">기간당 최상위 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="170cc-162">Review top queries per duration</span></span>
<span data-ttu-id="170cc-163">Query Performance Insight의 최신 업데이트에는 잠재적인 병목 상태를 식별하는 데 도움이 되는 두 가지 새로운 메트릭인 기간과 실행 횟수가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="170cc-164">장기 실행 쿼리는 리소스를 더 오래 잠그고, 다른 사용자를 차단하고, 확장성을 제한할 가능성이 가장 높습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="170cc-165">또한 최적화에 가장 적합한 후보이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="170cc-166">장기 실행 쿼리를 식별하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-166">To identify long running queries:</span></span>

1. <span data-ttu-id="170cc-167">선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기</span><span class="sxs-lookup"><span data-stu-id="170cc-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="170cc-168">메트릭을 **기간**</span><span class="sxs-lookup"><span data-stu-id="170cc-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="170cc-169">쿼리 수 및 관찰 간격 선택</span><span class="sxs-lookup"><span data-stu-id="170cc-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="170cc-170">집계 함수 선택</span><span class="sxs-lookup"><span data-stu-id="170cc-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="170cc-171">**Sum** 은 전체 관찰 간격 동안 모든 쿼리 실행 시간을 합합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="170cc-172">**Max** 는 전체 관찰 간격에는 실행 시간이 최대였던 쿼리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="170cc-173">**Avg** 는 모든 쿼리 실행의 평균 실행 시간을 찾은 후 이러한 평균을 초과하는 항목을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![쿼리 기간][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="170cc-175">실행 횟수당 최상위 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="170cc-175">Review top queries per execution count</span></span>
<span data-ttu-id="170cc-176">실행 횟수가 높을 경우 데이터베이스 자체에는 영향을 주지 않고 리소스 사용량이 적어질 수 있지만 전체 응용 프로그램이 느려질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="170cc-177">일부 경우에 실행 횟수가 매우 높을 경우 네트워크 왕복이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="170cc-178">왕복은 성능에 지대한 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="170cc-179">네트워크 대기 시간 및 다운스트림 서버 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="170cc-180">예를 들어, 많은 데이터 기반 웹 사이트는 사용자 요청이 있을 때마다 데이터베이스에 과도하게 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="170cc-181">연결 풀링이 도움이 되지만, 데이터베이스 서버에서 네트워크 트래픽 및 처리 부하가 높아져 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="170cc-182">일반적으로는 왕복을 최소로 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="170cc-183">자주 실행되는 쿼리("번잡한") 쿼리를 식별하려면</span><span class="sxs-lookup"><span data-stu-id="170cc-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="170cc-184">선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기</span><span class="sxs-lookup"><span data-stu-id="170cc-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="170cc-185">메트릭을 **실행 횟수**</span><span class="sxs-lookup"><span data-stu-id="170cc-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="170cc-186">쿼리 수 및 관찰 간격 선택</span><span class="sxs-lookup"><span data-stu-id="170cc-186">Select number of queries and observation interval</span></span>
   
    ![쿼리 실행 횟수][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="170cc-188">성능 튜닝 주석 이해</span><span class="sxs-lookup"><span data-stu-id="170cc-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="170cc-189">Query Performance Insight에서 워크로드를 살펴보는 동안 차트 맨 위에 세로줄이 있는 아이콘이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="170cc-190">이러한 아이콘은 주석으로, [SQL Azure 데이터베이스 관리자](sql-database-advisor.md)가 수행한 작업에 영향을 미치는 성능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="170cc-191">주석에 마우스를 가져가면 해당 작업에 대한 기본 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-191">By hovering annotation, you get basic information about the action:</span></span>

![쿼리 주석][6]

<span data-ttu-id="170cc-193">더 자세히 알고 싶거나 관리자 권장 구성을 적용하려는 경우 이 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="170cc-194">작업의 세부 정보가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-194">It will open details of action.</span></span> <span data-ttu-id="170cc-195">활성 권장 사항은 명령을 사용하여 바로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![쿼리 주석 세부 정보][7]

### <a name="multiple-annotations"></a><span data-ttu-id="170cc-197">여러 주석.</span><span class="sxs-lookup"><span data-stu-id="170cc-197">Multiple annotations.</span></span>
<span data-ttu-id="170cc-198">확대/축소 수준으로 인해 서로 가까이 있는 주석은 하나로 축소되어 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="170cc-199">이러한 경우 특수 아이콘이 표시됩니다. 이 아이콘을 클릭하면 그룹화된 주석 목록이 표시되는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="170cc-200">쿼리 및 성능 조정 작업의 상관 관계를 파악하면 워크로드를 파악하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="170cc-201">Query Performance Insight에 대한 쿼리 저장소 구성 최적화</span><span class="sxs-lookup"><span data-stu-id="170cc-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="170cc-202">Query Performance Insight를 사용하는 동안 다음 쿼리 저장소 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="170cc-203">"이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="170cc-204">자세한 내용은 여기를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="170cc-204">Click here to learn more."</span></span>
* <span data-ttu-id="170cc-205">"이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="170cc-206">여기를 클릭하여 설정을 변경하세요."</span><span class="sxs-lookup"><span data-stu-id="170cc-206">Click here to change settings."</span></span> 

<span data-ttu-id="170cc-207">이러한 메시지는 일반적으로 쿼리 저장소가 새 데이터를 수집할 수 없을 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="170cc-208">첫 번째 경우는 쿼리 저장소가 읽기 전용 상태이고 매개 변수가 최적으로 설정되었을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="170cc-209">쿼리 저장소의 크기를 늘리거나 쿼리 저장소를 지워서 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds 단추][8]

<span data-ttu-id="170cc-211">두 번째 경우는 쿼리 저장소가 꺼져 있거나 매개 변수가 최적 상태로 설정되어 있지 않을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="170cc-212">아래 명령을 실행하거나 포털에서 직접 보존 및 캡처 정책을 변경하고 쿼리 저장소를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds 단추][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="170cc-214">권장된 보존 및 캡처 정책</span><span class="sxs-lookup"><span data-stu-id="170cc-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="170cc-215">보존 정책에는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="170cc-216">크기 기반 - AUTO로 설정된 경우 최대 크기에 가까워지면 데이터를 자동으로 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="170cc-217">시간 기반 - 기본적으로 30일로 설정됩니다. 즉, 쿼리 저장소의 공간이 부족해지면 30일이 지난 쿼리 정보를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="170cc-218">캡처 정책은 다음과 같이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="170cc-219">**모두** – 모든 쿼리를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="170cc-220">**자동** – 컴파일 및 실행 기간이 중요하지 않고 사용 빈도가 적은 쿼리가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="170cc-221">실행 횟수, 컴파일 및 런타임 기간에 대한 임계값을 내부적으로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="170cc-222">기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-222">This is the default option.</span></span>
* <span data-ttu-id="170cc-223">**없음** – 쿼리 저장소에서 새 쿼리의 캡처를 중지하지만 이미 캡처된 쿼리에 대한 런타임 통계는 계속 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="170cc-224">모든 정책을 AUTO로 설정하고 클린 정책을 30일로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="170cc-225">쿼리 저장소의 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-225">Increase size of Query Store.</span></span> <span data-ttu-id="170cc-226">이는 데이터베이스에 연결하고 다음 쿼리를 실행하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="170cc-227">하지만 이러한 설정을 적용하면 결과적으로 쿼리 저장소가 새 쿼리를 수집하게 되지만, 기다리는 것을 원치 않을 경우 쿼리 저장소를 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="170cc-228">다음 쿼리를 실행하면 쿼리 저장소의 모든 현재 정보가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="170cc-229">요약</span><span class="sxs-lookup"><span data-stu-id="170cc-229">Summary</span></span>
<span data-ttu-id="170cc-230">쿼리 성능 Insight를 통해 쿼리 작업의 영향 및 데이터베이스 리소스 사용의 관계를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="170cc-231">이 기능을 사용하여 최상위 사용 쿼리를 확인하고 문제가 되기 전에 해결할 쿼리를 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="170cc-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="170cc-232">Next steps</span></span>
<span data-ttu-id="170cc-233">SQL 데이터베이스의 성능 향상에 관한 추가 권장 사항은 [Query Performance Insight](sql-database-advisor.md) 블레이드의 **권장 사항** 을 클릭하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="170cc-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

![성능 관리자](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

