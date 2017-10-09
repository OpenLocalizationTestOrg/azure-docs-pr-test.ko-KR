---
title: "Azure SQL 데이터베이스에 대 한 aaaQuery performance insight | Microsoft Docs"
description: "쿼리 성능 모니터링 hello 대부분 CPU 사용 Azure SQL 데이터베이스에 대 한 쿼리를 식별 합니다."
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
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="6008b-103">Azure SQL 데이터베이스 Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="6008b-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="6008b-104">관리 하 고 관계형 데이터베이스의 hello 성능 조정 상당한 기술력과 시간 투자를 필요로 하는 어려운 과제가 되 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="6008b-105">Query Performance Insight 있습니다 toospend를 hello 다음을 제공 하 여 데이터베이스 성능 문제 해결 시간이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="6008b-106">데이터베이스 리소스(DTU) 사용에 대한 보다 자세한 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="6008b-107">hello 잠재적으로 향상 된 성능을 위해 튜닝할 수 있는 CPU/기간/실행 수 별 상위 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="6008b-108">쿼리의 hello 세부 정보로 다운 기능 toodrill hello, 해당 텍스트 및 리소스 사용률의 기록 보기.</span><span class="sxs-lookup"><span data-stu-id="6008b-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="6008b-109">[SQL Azure 데이터베이스 관리자](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="6008b-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="6008b-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6008b-110">Prerequisites</span></span>
* <span data-ttu-id="6008b-111">Query Performance Insight를 위해서는 데이터베이스에서 [쿼리 저장소](https://msdn.microsoft.com/library/dn817826.aspx) 가 활성 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="6008b-112">Hello 포털 tooturn 쿼리 저장소를 실행 하지 않는 경우 묻는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="6008b-113">권한</span><span class="sxs-lookup"><span data-stu-id="6008b-113">Permissions</span></span>
<span data-ttu-id="6008b-114">hello 다음 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md) 필요한 toouse Query Performance Insight 사용 권한은:</span><span class="sxs-lookup"><span data-stu-id="6008b-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="6008b-115">**판독기**, **소유자**, **참가자**, **SQL DB 참가자**, 또는 **SQL Server 참가자** 사용 권한은 tooview hello 리소스를 소비한 상위 쿼리 및 차트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="6008b-116">**소유자**, **참가자**, **SQL DB 참가자**, 또는 **SQL Server 참가자** 권한은 필요한 tooview 쿼리 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="6008b-117">Query Performance Insight 사용</span><span class="sxs-lookup"><span data-stu-id="6008b-117">Using Query Performance Insight</span></span>
<span data-ttu-id="6008b-118">Query Performance Insight은 쉽게 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="6008b-119">열기 [Azure 포털](https://portal.azure.com/) 및 tooexamine 찾기 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="6008b-120">왼쪽 메뉴의 지원 및 문제 해결에서 "Query Performance Insight"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="6008b-121">Hello 첫 번째 탭에서 상위 리소스 소비 쿼리의 hello 목록을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="6008b-122">개별 쿼리 tooview 세부 정보를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="6008b-123">[SQL Azure 데이터베이스 관리자](sql-database-advisor.md) 를 열고 권장 사항을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="6008b-124">슬라이더를 사용 하 여 또는 관찰 간격 아이콘 toochange 확대/축소 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![성능 대시보드](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="6008b-126">몇 시간 데이터는 SQL 데이터베이스 tooprovide query performance insight에 쿼리 저장소에서 캡처하지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="6008b-127">특정 기간 중 쿼리 저장소 활성화 되지 않았습니다 hello 데이터베이스에는 활동이 없는 경우 해당 기간을 표시할 때 hello 차트 비어 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="6008b-128">실행하지 않는 경우 언제든지 쿼리 저장소를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="6008b-129">최상위 CPU 소비 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="6008b-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="6008b-130">Hello에 [포털](http://portal.azure.com) 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="6008b-131">Tooa SQL 데이터베이스를 검색 하 고 클릭 **모든 설정을** > **지원 + 문제 해결** > **쿼리 성능 통찰력**합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query Performance Insight][1]
   
    <span data-ttu-id="6008b-133">hello 상위 쿼리 보기 열리고 hello 상위 CPU 소비 쿼리 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="6008b-134">자세한 내용은 hello 차트 주위를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-134">Click around hello chart for details.</span></span><br><span data-ttu-id="6008b-135">hello 윗줄 표시 hello 데이터베이스에 대 한 전체 DTU %hello 바 표시 CPU (%) hello 선택한 간격 동안 선택한 hello 쿼리에서 사용 하는 동안 (경우에 예를 들어 **지난 주** 선택 되어 각 막대 1 일을 나타냅니다).</span><span class="sxs-lookup"><span data-stu-id="6008b-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![최상위 쿼리][2]
   
    <span data-ttu-id="6008b-137">hello 아래쪽 표에 표시 쿼리 hello에 대 한 집계 된 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="6008b-138">쿼리 ID – 데이터베이스 내 쿼리의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="6008b-139">예측 가능한 간격 동안 쿼리당 CPU입니다(집계 함수에 따라 다름).</span><span class="sxs-lookup"><span data-stu-id="6008b-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="6008b-140">쿼리당 기간입니다(집계 함수에 따라 다름).</span><span class="sxs-lookup"><span data-stu-id="6008b-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="6008b-141">특정 쿼리에 대한 총 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="6008b-142">선택 하거나 개별 쿼리에 tooinclude의 선택을 취소 하거나 확인란을 사용 하 여 hello 차트에서 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="6008b-143">데이터 만료 되 면 클릭 hello **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="6008b-144">슬라이더 및 확대/축소 단추 toochange 관찰 간격을 사용 하 고 스파이크를 조사할 수 있습니다: ![설정](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="6008b-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="6008b-145">필요에 따라 다른 보기를 원할 경우 **사용자 지정** 탭을 선택하고 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="6008b-146">메트릭(CPU, 기간, 실행 횟수)</span><span class="sxs-lookup"><span data-stu-id="6008b-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="6008b-147">시간 간격(지난 24시간, 지난주, 지난달)</span><span class="sxs-lookup"><span data-stu-id="6008b-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="6008b-148">쿼리 수</span><span class="sxs-lookup"><span data-stu-id="6008b-148">Number of queries.</span></span>
   * <span data-ttu-id="6008b-149">집계 함수</span><span class="sxs-lookup"><span data-stu-id="6008b-149">Aggregation function.</span></span>
     
     ![설정](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="6008b-151">개별 쿼리 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="6008b-151">Viewing individual query details</span></span>
<span data-ttu-id="6008b-152">tooview 쿼리 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="6008b-152">tooview query details:</span></span>

1. <span data-ttu-id="6008b-153">상위 쿼리의 hello 목록에서 쿼리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-153">Click any query in hello list of top queries.</span></span>
   
    ![세부 정보](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="6008b-155">hello 자세히 보기 열리고 hello 쿼리의 CPU 소비/기간/실행 수 시간에 따라 분리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="6008b-156">자세한 내용은 hello 차트 주위를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="6008b-157">Hello 막대는 hello 선택한 쿼리에 사용 된 CPU % 및 상위 차트에 전체 데이터베이스 DTU % 있는 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="6008b-158">두 번째 차트 hello 선택한 쿼리에 의해 총 기간을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="6008b-159">아래쪽 차트 hello 선택한 쿼리에 의해 실행의 총 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![쿼리 세부 정보][3]
4. <span data-ttu-id="6008b-161">필요에 따라 슬라이더를 사용 하 여, 확대/축소 단추 또는 클릭 **설정을** toocustomize 쿼리 데이터 표시 방법을 또는 다른 기간 toopick 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="6008b-162">기간당 최상위 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="6008b-162">Review top queries per duration</span></span>
<span data-ttu-id="6008b-163">최근 업데이트 Query Performance Insight의 hello, 잠재적인 병목 상태를 식별 하는 데 도움이 되는 두 개의 새 메트릭으로 소개: 기간 및 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="6008b-164">장기 실행 쿼리 긴 리소스 잠금, 다른 사용자를 차단 및 확장성 제한에 대 한 hello 가장 가능성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="6008b-165">또한 hello 적합 한 최적화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="6008b-166">장기 실행 쿼리 tooidentify:</span><span class="sxs-lookup"><span data-stu-id="6008b-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="6008b-167">선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기</span><span class="sxs-lookup"><span data-stu-id="6008b-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="6008b-168">메트릭 toobe 변경 **기간**</span><span class="sxs-lookup"><span data-stu-id="6008b-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="6008b-169">쿼리 수 및 관찰 간격 선택</span><span class="sxs-lookup"><span data-stu-id="6008b-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="6008b-170">집계 함수 선택</span><span class="sxs-lookup"><span data-stu-id="6008b-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="6008b-171">**Sum** 은 전체 관찰 간격 동안 모든 쿼리 실행 시간을 합합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="6008b-172">**Max** 는 전체 관찰 간격에는 실행 시간이 최대였던 쿼리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="6008b-173">**Avg** 찾습니다 모든 평균 실행 시간 쿼리 실행 하 고 보여 hello 이러한 평균은에서 위쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![쿼리 기간][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="6008b-175">실행 횟수당 최상위 쿼리 검토</span><span class="sxs-lookup"><span data-stu-id="6008b-175">Review top queries per execution count</span></span>
<span data-ttu-id="6008b-176">실행 횟수가 높을 경우 데이터베이스 자체에는 영향을 주지 않고 리소스 사용량이 적어질 수 있지만 전체 응용 프로그램이 느려질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="6008b-177">경우에 따라 매우 높은 실행 횟수 않을 tooincrease 네트워크의 라운드트립 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="6008b-178">왕복은 성능에 지대한 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="6008b-179">서로 주체 toonetwork 대기 시간 및 toodownstream 서버 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="6008b-180">예를 들어 여러 데이터 기반 웹 사이트 과도 하 게 모든 사용자 요청에 대해 hello 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="6008b-181">연결 풀링을 사용 하면, hello 증가 하는 동안 네트워크 트래픽 및 hello 데이터베이스 서버의 처리 부하 성능이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="6008b-182">일반 조언을 라운드 트립 tooan 꼭 필요한 tookeep입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="6008b-183">tooidentify 쿼리 ("수 다 스러운") 쿼리를 자주 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="6008b-184">선택한 데이터베이스에 대한 Query Performance Insight에서 **사용자 지정** 탭 열기</span><span class="sxs-lookup"><span data-stu-id="6008b-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="6008b-185">메트릭 toobe 변경 **실행 수**</span><span class="sxs-lookup"><span data-stu-id="6008b-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="6008b-186">쿼리 수 및 관찰 간격 선택</span><span class="sxs-lookup"><span data-stu-id="6008b-186">Select number of queries and observation interval</span></span>
   
    ![쿼리 실행 횟수][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="6008b-188">성능 튜닝 주석 이해</span><span class="sxs-lookup"><span data-stu-id="6008b-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="6008b-189">Query Performance Insight에서 작업 부하를 탐색 하는 동안 hello 차트 위에 세로 선이 있는 아이콘이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="6008b-190">이러한 아이콘은 주석으로, [SQL Azure 데이터베이스 관리자](sql-database-advisor.md)가 수행한 작업에 영향을 미치는 성능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="6008b-191">가리키기 주석으로 hello 동작에 대 한 기본 정보를 얻을 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="6008b-191">By hovering annotation, you get basic information about hello action:</span></span>

![쿼리 주석][6]

<span data-ttu-id="6008b-193">더 많은 tooknow 이나 관리자의 권장 구성 적용, hello 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="6008b-194">작업의 세부 정보가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-194">It will open details of action.</span></span> <span data-ttu-id="6008b-195">활성 권장 사항은 명령을 사용하여 바로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![쿼리 주석 세부 정보][7]

### <a name="multiple-annotations"></a><span data-ttu-id="6008b-197">여러 주석.</span><span class="sxs-lookup"><span data-stu-id="6008b-197">Multiple annotations.</span></span>
<span data-ttu-id="6008b-198">이기는 확대/축소 수준 때문에 다른 닫기 tooeach 되는 주석 됩니다 get으로 축소 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="6008b-199">이러한 경우 특수 아이콘이 표시됩니다. 이 아이콘을 클릭하면 그룹화된 주석 목록이 표시되는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="6008b-200">쿼리 및 성능 튜닝 작업의 상관 관계 지정 toobetter 작업을 파악 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="6008b-201">Query Performance Insight에 대 한 쿼리 저장소 구성을 hello 최적화</span><span class="sxs-lookup"><span data-stu-id="6008b-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="6008b-202">Query Performance Insight를 사용 하는 동안 다음 쿼리 저장소 메시지 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="6008b-203">"이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="6008b-204">여기를 클릭 toolearn 자세한. "</span><span class="sxs-lookup"><span data-stu-id="6008b-204">Click here toolearn more."</span></span>
* <span data-ttu-id="6008b-205">"이 데이터베이스의 쿼리 저장소가 적절하게 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="6008b-206">여기 toochange 설정 클릭 합니다. "</span><span class="sxs-lookup"><span data-stu-id="6008b-206">Click here toochange settings."</span></span> 

<span data-ttu-id="6008b-207">이러한 메시지는 일반적으로 쿼리 저장소 수 toocollect 새 데이터가 없는 경우에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="6008b-208">첫 번째 경우는 쿼리 저장소가 읽기 전용 상태이고 매개 변수가 최적으로 설정되었을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="6008b-209">쿼리 저장소의 크기를 늘리거나 쿼리 저장소를 지워서 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![qds 단추][8]

<span data-ttu-id="6008b-211">두 번째 경우는 쿼리 저장소가 꺼져 있거나 매개 변수가 최적 상태로 설정되어 있지 않을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="6008b-212">아래 명령을 실행 하 여 또는 포털에서 직접 hello 보존 및 캡처 정책 및 사용 쿼리 저장소를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![qds 단추][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="6008b-214">권장된 보존 및 캡처 정책</span><span class="sxs-lookup"><span data-stu-id="6008b-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="6008b-215">보존 정책에는 다음과 같은 두 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="6008b-216">크기 기반-에 도달 하면 집합 tooAUTO 최대 크기 근처 자동으로 데이터를 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="6008b-217">시간 기반-기본적으로 설정 됩니다 म too30 일, 즉, 쿼리 저장소, 공간 부족을 삭제 하는 30 일 보다 오래 된 정보를 쿼리할</span><span class="sxs-lookup"><span data-stu-id="6008b-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="6008b-218">캡처 정책은 다음과 같이 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="6008b-219">**모두** – 모든 쿼리를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="6008b-220">**자동** – 컴파일 및 실행 기간이 중요하지 않고 사용 빈도가 적은 쿼리가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="6008b-221">실행 횟수, 컴파일 및 런타임 기간에 대한 임계값을 내부적으로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="6008b-222">Hello 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-222">This is hello default option.</span></span>
* <span data-ttu-id="6008b-223">**없음** – 쿼리 저장소에서 새 쿼리의 캡처를 중지하지만 이미 캡처된 쿼리에 대한 런타임 통계는 계속 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="6008b-224">모든 정책 tooAUTO 및 정리 정책 too30 (일)을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="6008b-225">쿼리 저장소의 크기를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-225">Increase size of Query Store.</span></span> <span data-ttu-id="6008b-226">연결 tooa 데이터베이스에서 수행 하 고 쿼리 다음 발급 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="6008b-227">하지만 쿼리 저장소를 지울 수 toowait 않도록 이러한 설정을 적용 하는 새 쿼리를 수집 하는 쿼리 저장소 결국 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="6008b-228">다음 쿼리를 실행 하는 hello 쿼리 저장소에에서 현재 정보를 모두 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="6008b-229">요약</span><span class="sxs-lookup"><span data-stu-id="6008b-229">Summary</span></span>
<span data-ttu-id="6008b-230">Query Performance Insight의 쿼리 작업이 hello 영향 및 toodatabase 리소스 사용의 관계를 이해 하도록 도와 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="6008b-231">이 기능을 hello 가장 쿼리를 많이 사용 되는 방법을 알아봅니다 쿼리하고 문제가 해지기 전에 hello 것 toofix 쉽게 식별할 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6008b-232">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6008b-232">Next steps</span></span>
<span data-ttu-id="6008b-233">SQL 데이터베이스의 hello 성능 향상에 대 한 자세한 내용은 클릭 [권장 사항을](sql-database-advisor.md) hello에 **Query Performance Insight** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="6008b-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

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

