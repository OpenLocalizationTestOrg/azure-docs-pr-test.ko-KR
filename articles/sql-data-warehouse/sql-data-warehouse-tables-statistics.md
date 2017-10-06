---
title: "SQL 데이터 웨어하우스에 테이블에 대 한 aaaManaging 통계 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 테이블에 대한 통계 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="eb899-103">SQL 데이터 웨어하우스의 테이블에 대한 통계 관리</span><span class="sxs-lookup"><span data-stu-id="eb899-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="eb899-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="eb899-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="eb899-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="eb899-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="eb899-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="eb899-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="eb899-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="eb899-107">[Index][Index]</span></span>
> * <span data-ttu-id="eb899-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="eb899-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="eb899-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="eb899-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="eb899-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="eb899-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="eb899-111">hello 자세한 SQL 데이터 웨어하우스 알고 있는 데이터에 대 한 hello 더 빠르게 해당 쿼리를 실행할 수 데이터에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="eb899-112">데이터에 대 한 SQL 데이터 웨어하우스를 지시 하는 hello 방법은 데이터에 대 한 통계를 수집 하 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="eb899-113">하나는 데이터에 대해 통계가 있는 hello 가장 중요 한 작업 중 할 수 있는 toooptimize 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="eb899-114">통계는 SQL 데이터 웨어하우스 쿼리에 대 한 hello 최적의 계획을 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="eb899-115">Hello SQL 데이터 웨어하우스 쿼리 최적화 프로그램은 비용 기반 최적화 프로그램 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="eb899-116">즉, 다양 한 쿼리 계획의 hello 비용을 비교 하 고도 가장 빠른 hello를 실행 하는 hello 계획에 있어야 하 고 hello 최저 비용으로 hello 계획을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="eb899-117">단일 열, 여러 열 또는 테이블의 인덱스에 대해 통계를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="eb899-118">통계는 hello 범위 및 값의 선택도 캡처하는 히스토그램에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="eb899-119">이 특히 경우 hello 최적화 프로그램에서 필요한 tooevaluate 조인, GROUP BY, HAVING 및 쿼리의 WHERE 절.</span><span class="sxs-lookup"><span data-stu-id="eb899-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="eb899-120">예를 들어 hello 최적화 프로그램의 계산 결과 쿼리에서 필터링 할 hello 날짜는 1 개 행을 반환 합니다, 선택할 수 있지만 매우 다른 경우 보다 게 계획 하면 날짜은 예상 선택한 됩니다 1 백만 행을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="eb899-121">중요 통계를 작성 하는 것은 매우 중요 한를 해당 통계 *정확 하 게* hello hello 테이블의 현재 상태를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="eb899-122">최신 통계가 있는 hello 최적화 프로그램에서 올바른 계획 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="eb899-123">hello 최적화 프로그램에서 만든 hello 계획은 데이터에 대 한 hello 통계 우수한 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="eb899-124">hello 프로세스 통계 생성 및 업데이트의 수동 프로세스는 현재 있지만 매우 간단한 toodo 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="eb899-125">이러한 방식은 단일 열 및 인덱스에 대한 통계를 자동으로 만들고 업데이트하는 SQL Server와는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="eb899-126">아래 정보를 hello를 사용 하 여 데이터에 대해 크게 hello 통계의 hello 관리를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="eb899-127">통계 시작</span><span class="sxs-lookup"><span data-stu-id="eb899-127">Getting started with statistics</span></span>
 <span data-ttu-id="eb899-128">모든 열에 샘플링 된 통계를 만드는 쉽게 tooget으로 시작 됩니다 통계.</span><span class="sxs-lookup"><span data-stu-id="eb899-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="eb899-129">최신 중요 tookeep 통계 동일 하 게 되므로 보수적인 접근 방법 수 tooupdate 통계 매일 또는 될 각 로드 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="eb899-130">성능 및 비용 toocreate 및 update statistics hello 간의 장단점은 항상입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="eb899-131">걸리는 너무 길어 toomaintain 모든 통계를 찾을 경우 통계가 있는 열 또는 열에 대 한 좀 더 선택적 tootry toobe 자주 업데이트 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="eb899-132">예를 들어 좋습니다 tooupdate 날짜 열 로드할 때마다 이후가 보다 매일, 새 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="eb899-133">다시, 하면 얻게 됩니다 hello 것이 가장 좋습니다 조인, GROUP BY, HAVING에 포함 된 열에 통계가 있는 및 WHERE 절.</span><span class="sxs-lookup"><span data-stu-id="eb899-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="eb899-134">많이 포함 된 테이블이 있는 경우 열 hello에만 사용 되는 SELECT 절, 이러한 열에 대 한 통계 도움이 되지 않을 수 및 약간 더 많은 노력이 tooidentify 지출 여기서 통계는 도움이 되지만, hello 열만 줄일 수 hello 시간 toomaintain 통계 .</span><span class="sxs-lookup"><span data-stu-id="eb899-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="eb899-135">여러 열 통계</span><span class="sxs-lookup"><span data-stu-id="eb899-135">Multi-column statistics</span></span>
<span data-ttu-id="eb899-136">또한 단일 열에 대 한 toocreating 통계, 쿼리는 여러 열 통계에서 이점이 있는지을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="eb899-137">여러 열 통계는 열 목록에 대해 만든 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="eb899-138">Hello 목록의 hello 첫 번째 열에 대 한 단일 열 통계를 포함 및 몇 가지 열 간 상관 관계 정보 밀도 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="eb899-139">예를 들어 tooanother 두 열에 조인 하는 테이블을 사용 하는 경우 SQL 데이터 웨어하우스 두 열 간의 관계 hello 이해 하는 경우 hello 계획 최적화 더 잘 수를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="eb899-140">여러 열 통계는 복합 조인 및 그룹 기준과 같은 일부 작업에 대한 쿼리 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="eb899-141">통계 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb899-141">Updating statistics</span></span>
<span data-ttu-id="eb899-142">통계 업데이트는 사용자 데이터베이스 관리 루틴의 중요한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="eb899-143">Hello 배포 hello 데이터베이스의 데이터가 변경 되 면 통계 업데이트 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="eb899-144">오래 된 통계를 toosub 최적의 쿼리 성능을 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="eb899-145">최상의 방법 중 하나는 날짜 열에 통계 tooupdate 매일 새 날짜를 추가할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="eb899-146">각 시간 새 행은 hello 데이터 웨어하우스에 로드 되 면 새 부하 날짜나 트랜잭션 날짜가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="eb899-147">이러한 hello 데이터 분포를 변경 하 고 달라질 hello 통계.</span><span class="sxs-lookup"><span data-stu-id="eb899-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="eb899-148">반대로, customer 테이블에는 국가 열에 대 한 통계 필요 업데이트 toobe 값의 분포 hello 일반적으로 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="eb899-149">Hello 분포는 고객 간 상수 라고 가정할 경우 toochange hello 데이터 분산을 진행 되지 않습니다 새 행 toohello 테이블 변형을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="eb899-150">그러나 한 국가만 포함 하는 데이터 웨어하우스 데이터 새 국가에서 가져오는 경우 데이터에 저장 하는 여러 국가에서 확실 하 게 해야 합니다 hello 국가 열에 대 한 tooupdate 통계.</span><span class="sxs-lookup"><span data-stu-id="eb899-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="eb899-151">Hello 첫 번째 질문 tooask 되는 쿼리의 문제를 해결 하는 경우 중 하나 "최신임 hello 통계"?</span><span class="sxs-lookup"><span data-stu-id="eb899-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="eb899-152">이 질문은 하나 hello 데이터의 보존 기간 hello에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="eb899-153">위쪽 toodate 통계 개체는 내부 데이터 없는 중요 한 변화가 toohello 되었으면 아주 오래 된 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="eb899-154">Hello 행 수가 크게 변경 된 지정된 된 열에 대 한 값의 hello 분포에 중요 한 변화가 없는 시기나 *다음* 시간 tooupdate 통계는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="eb899-155">참고로 **SQL Server** (SQL 데이터 웨어하우스 아님)는 다음 상황에서 자동으로 통계를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="eb899-156">0 개, 행이 hello 테이블의 행을 추가 하는 경우 통계의 자동 업데이트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="eb899-157">500 개 미만의 행부터 시작 하는 500 개 이상의 행 tooa 테이블을 추가 하는 경우 (예: 시작 될 때 499을 한 500 행 tooa 총 999 개 행의 추가)에서 자동 업데이트를 얻을 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="eb899-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="eb899-158">500 개 행 되 면 해야 tooadd 500 개의 추가 행 + hello hello 테이블 크기의 20% 전에 hello 통계에 대해 자동 업데이트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="eb899-159">Hello 테이블 내에서 데이터는 hello 통계가 마지막으로 업데이트 된 이후 변경 된 경우에 없는 DMV toodetermine가가 통계의 hello 보존 기간을 알 수 제공 hello 그림의 일부 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="eb899-160">Hello 다음 toodetermine hello 마지막 시간 통계는 쿼리를 사용할 수 있는 각 테이블에 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="eb899-161">지정된 된 열에 대 한 값의 hello 분포에 중요 한 변화가 이면 업데이트 해야 통계 hello에 관계 없이 마지막으로 업데이트 된 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="eb899-162">예를 들어, 일반적으로 데이터 웨어하우스의 날짜 열은 자주 통계 업데이트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="eb899-163">각 시간 새 행은 hello 데이터 웨어하우스에 로드 되 면 새 부하 날짜나 트랜잭션 날짜가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="eb899-164">이러한 hello 데이터 분포를 변경 하 고 달라질 hello 통계.</span><span class="sxs-lookup"><span data-stu-id="eb899-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="eb899-165">반대로, 성별 열 고객 테이블에 대 한 통계 업데이트 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="eb899-166">Hello 분포는 고객 간 상수 라고 가정할 경우 toochange hello 데이터 분산을 진행 되지 않습니다 새 행 toohello 테이블 변형을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="eb899-167">그러나 여러 성별에서 새 요구 사항 결과 및 성별 하나에 데이터 웨어하우스 포함 하는 경우 다음 확실 하 게 해야 hello 성별 열에 대 한 tooupdate 통계.</span><span class="sxs-lookup"><span data-stu-id="eb899-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="eb899-168">자세한 설명은 MSDN에서 [통계][Statistics]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb899-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="eb899-169">통계 관리 구현</span><span class="sxs-lookup"><span data-stu-id="eb899-169">Implementing statistics management</span></span>
<span data-ttu-id="eb899-170">것이 좋습니다 tooextend 사용자 데이터에 통계는 업데이트 프로세스 tooensure 로드 hello hello 부하의 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="eb899-171">hello 데이터 로드가 테이블의 크기 및/또는 값의 분포를 가장 자주 변경 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="eb899-172">따라서이 방법은 논리적 위치 tooimplement 일부 관리 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="eb899-173">일부는 원칙은 hello 로드 프로세스 중에 통계를 업데이트 하는 것에 대 한 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="eb899-174">로드된 각 테이블에 하나 이상의 업데이트된 통계 개체가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="eb899-175">이 업데이트 hello 테이블 hello 통계 업데이트의 일부로 크기 (행 개수 및 페이지 수) 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="eb899-176">JOIN, GROUP BY, ORDER BY 및 DISTINCT 절에 참여하는 열에 집중</span><span class="sxs-lookup"><span data-stu-id="eb899-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="eb899-177">날짜를 더 자주 이러한 값 hello 통계 히스토그램에 포함 되지 것입니다 트랜잭션 등의 "키 ascending" 열을 업데이트 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eb899-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="eb899-178">정적 배포 열은 자주 업데이트하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="eb899-179">각 통계 개체가 연속으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="eb899-180">`UPDATE STATISTICS <TABLE_NAME>` 의 간단한 구현은 특히 통계 개체가 많은 너비가 넓은 테이블에는 적합하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="eb899-181">에 대 한 자세한 내용은 [키 오름차순] SQL Server 2014 toohello 카디널리티 추정 모델 백서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eb899-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="eb899-182">자세한 설명은 MSDN에서 [카디널리티 예측][Cardinality Estimation]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb899-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="eb899-183">예제: 통계 작성</span><span class="sxs-lookup"><span data-stu-id="eb899-183">Examples: Create statistics</span></span>
<span data-ttu-id="eb899-184">이러한 예와 어떻게 toouse 통계를 만들기 위한 다양 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="eb899-185">각 열에 대해 사용 하는 hello 옵션 데이터의 특성과 hello 및 쿼리에서 hello 열은 사용 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="eb899-186">A.</span><span class="sxs-lookup"><span data-stu-id="eb899-186">A.</span></span> <span data-ttu-id="eb899-187">기본 옵션으로 단일 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="eb899-188">toocreate 통계 열에는 hello 통계 개체에 대 한 이름 및 hello hello 열 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="eb899-189">이 구문은 모든 hello 기본 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="eb899-190">기본적으로 SQL 데이터 웨어하우스 통계를 만들 때 hello 테이블의 20% 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="eb899-191">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="eb899-192">B.</span><span class="sxs-lookup"><span data-stu-id="eb899-192">B.</span></span> <span data-ttu-id="eb899-193">모든 행을 검사하여 단일 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="eb899-194">hello 기본 샘플링 비율 20% 이면 대부분의 경우 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="eb899-195">그러나 hello 샘플링 비율을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="eb899-196">전체 toosample hello 테이블에서 다음이 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="eb899-197">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="eb899-198">C.</span><span class="sxs-lookup"><span data-stu-id="eb899-198">C.</span></span> <span data-ttu-id="eb899-199">Hello 샘플 크기를 지정 하 여 단일 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="eb899-200">또는 백분율로 hello 샘플 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="eb899-201">D.</span><span class="sxs-lookup"><span data-stu-id="eb899-201">D.</span></span> <span data-ttu-id="eb899-202">일부 hello 행에 대해서만 단일 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="eb899-203">다른 옵션을 테이블의 통계 hello 행의 부분에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="eb899-204">이를 필터링된 통계라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="eb899-205">예를 들어 큰 분할 된 테이블의 특정 파티션을 tooquery를 계획 하는 경우 필터링 된 통계를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="eb899-206">파티션 값만 hello에 통계를 만들어, hello 통계의 hello 정확도 향상 되 고 되므로 쿼리 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="eb899-207">이 예에서는 값의 범위에서 통계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="eb899-208">hello 값 수를 파티션으로 toomatch hello 범위의 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="eb899-209">Hello 쿼리 최적화 프로그램 tooconsider hello 분산된 쿼리 계획을 선택 하는 경우 필터링 된 통계를 사용 하 여에 대 한 hello 쿼리 hello 통계 개체의 hello 정의 내에 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="eb899-210">Hello 이전 예제에서는 hello 쿼리 절 2000101 사이의 20001231 toospecify col1 값 필요한 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="eb899-211">E.</span><span class="sxs-lookup"><span data-stu-id="eb899-211">E.</span></span> <span data-ttu-id="eb899-212">모든 hello 옵션으로 단일 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="eb899-213">물론, hello 옵션을 함께 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="eb899-214">아래 hello 예제 사용자 지정 샘플 크기와 함께 필터링 된 통계 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="eb899-215">Hello 전체 참조를 참조 하십시오. [CREATE STATISTICS] [ CREATE STATISTICS] msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="eb899-216">F.</span><span class="sxs-lookup"><span data-stu-id="eb899-216">F.</span></span> <span data-ttu-id="eb899-217">여러 열 통계 만들기</span><span class="sxs-lookup"><span data-stu-id="eb899-217">Create multi-column statistics</span></span>
<span data-ttu-id="eb899-218">단순히 toocreate 여러 열 통계는 hello 이전 예제에서 사용 하는 더 많은 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="eb899-219">사용 되는 hello 히스토그램 tooestimate hello 쿼리 결과 있는 행 수는 hello 통계 개체 정의에 나열 된 hello 첫 번째 열에 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="eb899-220">이 예에서 hello 히스토그램에는 *제품\_범주*합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="eb899-221">열 간 통계는 *product\_category* 및 *product\_sub_c\ategory*에서 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="eb899-222">간의 상관 관계 이므로 *제품\_범주* 및 *제품\_sub\_범주*, 다중 열 stat 이러한 열 액세스 되는 경우에 유용할 수 있습니다 hello에서 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="eb899-223">G.</span><span class="sxs-lookup"><span data-stu-id="eb899-223">G.</span></span> <span data-ttu-id="eb899-224">테이블의 모든 hello 열에서 통계를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="eb899-225">한 가지 방법은 toocreate 통계 hello 테이블을 만든 후 tooissues CREATE STATISTICS 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="eb899-226">H</span><span class="sxs-lookup"><span data-stu-id="eb899-226">H.</span></span> <span data-ttu-id="eb899-227">데이터베이스의 모든 열에 저장된 프로시저 toocreate 통계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="eb899-228">SQL 데이터 웨어하우스 없는 해당 하는 시스템 저장된 프로시저 너무 SQL Server에서 [sp_create_stats].</span><span class="sxs-lookup"><span data-stu-id="eb899-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="eb899-229">이 저장된 프로시저에 지문이 아직 없으면 통계 hello 데이터베이스의 모든 열에 단일 열 통계 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="eb899-230">데이터베이스 디자인으로 시작하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-230">This will help you get started with your database design.</span></span> <span data-ttu-id="eb899-231">무료 tooadapt 생각 될 것 tooyour 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-231">Feel free tooadapt it tooyour needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="eb899-232">이 절차를 hello 테이블의 모든 열에 대 한 toocreate 통계 hello 프로시저를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="eb899-233">예제: 통계 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb899-233">Examples: update statistics</span></span>
<span data-ttu-id="eb899-234">tooupdate 통계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="eb899-235">하나의 통계 개체를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-235">Update one statistics object.</span></span> <span data-ttu-id="eb899-236">Hello hello tooupdate 하려는 통계 개체 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="eb899-237">테이블에 있는 모든 통계 개체를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="eb899-238">하나의 특정 통계 개체 대신 hello 테이블의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="eb899-239">A.</span><span class="sxs-lookup"><span data-stu-id="eb899-239">A.</span></span> <span data-ttu-id="eb899-240">하나의 통계 개체 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb899-240">Update one specific statistics object</span></span>
<span data-ttu-id="eb899-241">다음 구문 tooupdate 특정 통계 개체는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="eb899-242">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="eb899-243">특정 통계 개체를 업데이트 하 여 hello 시간과 리소스가 필요 toomanage 통계를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="eb899-244">이 일부을 이라고 생각 하지만 toochoose hello 최상의 통계 개체 tooupdate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="eb899-245">B.</span><span class="sxs-lookup"><span data-stu-id="eb899-245">B.</span></span> <span data-ttu-id="eb899-246">테이블에 있는 모든 통계 업데이트</span><span class="sxs-lookup"><span data-stu-id="eb899-246">Update all statistics on a table</span></span>
<span data-ttu-id="eb899-247">이 테이블에 있는 모든 hello 통계 개체를 업데이트 하기 위한 간단한 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="eb899-248">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="eb899-249">이 문은 쉽게 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-249">This statement is easy toouse.</span></span> <span data-ttu-id="eb899-250">Hello 테이블에 대 한 모든 통계 업데이트 하 고 필요한 것 보다 더 많은 작업을 수행할 수 있습니다 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eb899-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="eb899-251">Hello 성능 문제가 없는 경우이 방법은 확실 하 게 hello 가장 쉽고 완벽 tooguarantee 통계가 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="eb899-252">테이블에 대 한 모든 통계를 업데이트할 때 SQL 데이터 웨어하우스 각 통계에 대 한 검색 toosample hello 테이블을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="eb899-253">Hello 테이블이 클 경우에 많은 열과 많은 통계, 요구에 따라 보다 효율적인 tooupdate 개별 통계 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="eb899-254">구현은 `UPDATE STATISTICS` 절차를 참조 하십시오. hello [임시 테이블] [ Temporary] 문서.</span><span class="sxs-lookup"><span data-stu-id="eb899-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="eb899-255">hello 구현 메서드는 약간 다른 toohello `CREATE STATISTICS` hello 최종 결과 제외한 위의 절차는 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="eb899-256">Hello 전체 구문에 대 한 참조 [Update Statistics] [ Update Statistics] msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="eb899-257">통계 메타데이터</span><span class="sxs-lookup"><span data-stu-id="eb899-257">Statistics metadata</span></span>
<span data-ttu-id="eb899-258">다양 한 시스템 뷰 및 함수 통계에 대 한 toofind 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="eb899-259">예를 들어 경우 통계 개체의이 아니게 통계가 생성 되거나 업데이트 된 마지막 때 통계 날짜 함수 toosee hello를 사용 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="eb899-260">통계에 대한 카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="eb899-260">Catalog views for statistics</span></span>
<span data-ttu-id="eb899-261">이 시스템 뷰는 통계에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="eb899-262">카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="eb899-262">Catalog View</span></span> | <span data-ttu-id="eb899-263">설명</span><span class="sxs-lookup"><span data-stu-id="eb899-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb899-264">[sys.columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="eb899-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="eb899-265">각 열에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-265">One row for each column.</span></span> |
| <span data-ttu-id="eb899-266">[sys.objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="eb899-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="eb899-267">Hello 데이터베이스의 각 개체에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="eb899-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="eb899-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="eb899-269">Hello 데이터베이스의 각 스키마에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="eb899-270">[sys.stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="eb899-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="eb899-271">각 통계 개체에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="eb899-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="eb899-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="eb899-273">Hello 통계 개체의 각 열에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="eb899-274">Toosys.columns를 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="eb899-275">[sys.tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="eb899-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="eb899-276">각 테이블에 대해 한 행입니다(외부 테이블 포함).</span><span class="sxs-lookup"><span data-stu-id="eb899-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="eb899-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="eb899-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="eb899-278">각 데이터 유형에 대해 한 행입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="eb899-279">통계에 대한 시스템 함수</span><span class="sxs-lookup"><span data-stu-id="eb899-279">System functions for statistics</span></span>
<span data-ttu-id="eb899-280">이 시스템 함수는 통계를 작업할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="eb899-281">시스템 함수</span><span class="sxs-lookup"><span data-stu-id="eb899-281">System Function</span></span> | <span data-ttu-id="eb899-282">설명</span><span class="sxs-lookup"><span data-stu-id="eb899-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb899-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="eb899-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="eb899-284">Date hello 통계 개체를 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="eb899-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="eb899-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="eb899-286">Hello 통계 개체에 의해 인식 hello 값 분포에 대 한 요약 수준 및 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="eb899-287">통계 열 및 함수를 하나의 보기로 결합</span><span class="sxs-lookup"><span data-stu-id="eb899-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="eb899-288">이 보기는 hello [STATS_DATE()] 함수에서 toostatistics와 결과 함께 연결 하는 열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="eb899-289">DBCC SHOW_STATISTICS() 예</span><span class="sxs-lookup"><span data-stu-id="eb899-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="eb899-290">DBCC SHOW_STATISTICS() 통계 개체 내에 유지 하는 hello 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="eb899-291">이 데이터는 세 부분으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="eb899-292">헤더</span><span class="sxs-lookup"><span data-stu-id="eb899-292">Header</span></span>
2. <span data-ttu-id="eb899-293">밀도 벡터</span><span class="sxs-lookup"><span data-stu-id="eb899-293">Density Vector</span></span>
3. <span data-ttu-id="eb899-294">히스토그램</span><span class="sxs-lookup"><span data-stu-id="eb899-294">Histogram</span></span>

<span data-ttu-id="eb899-295">hello 헤더 hello 통계에 대 한 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="eb899-296">hello 히스토그램 hello hello 통계 개체의 첫 번째 키 열에 값의 hello 분포를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="eb899-297">hello 밀도 벡터 열 간 상관 관계를 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="eb899-298">SQLDW는 hello 통계 개체에 hello 데이터를 사용 하 여 카디널리티 예상치 정확도 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="eb899-299">헤더, 밀도 및 히스토그램 표시</span><span class="sxs-lookup"><span data-stu-id="eb899-299">Show header, density, and histogram</span></span>
<span data-ttu-id="eb899-300">이 간단한 예제에서는 통계 개체의 모든 세 부분을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="eb899-301">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="eb899-302">DBCC SHOW_STATISTICS();의 하나 이상의 파트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="eb899-303">만 보려면 특정 부분을 사용 하 여 hello `WITH` 절 있는 부분을 지정 하 고 원하는 toosee:</span><span class="sxs-lookup"><span data-stu-id="eb899-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="eb899-304">예:</span><span class="sxs-lookup"><span data-stu-id="eb899-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="eb899-305">DBCC SHOW_STATISTICS() 차이점</span><span class="sxs-lookup"><span data-stu-id="eb899-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="eb899-306">SQL 데이터 웨어하우스에 비해 tooSQL 서버 DBCC SHOW_STATISTICS() 더 엄격 하 게 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="eb899-307">문서화되지 않은 기능은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="eb899-308">Stats_stream를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="eb899-309">통계 데이터의 특정 하위 집합에 대한 결과를 조인할 수는 없습니다(STAT_HEADER 조인 DENSITY_VECTOR).</span><span class="sxs-lookup"><span data-stu-id="eb899-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="eb899-310">NO_INFOMSGS는 메시지 제거에 대해 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="eb899-311">통계 이름에 대괄호를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="eb899-312">열 이름은 tooidentify 통계 개체를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="eb899-313">사용자 지정 오류 2767이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb899-314">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb899-314">Next steps</span></span>
<span data-ttu-id="eb899-315">자세한 내용은 MSDN에서 [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb899-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="eb899-316">toolearn에 hello 문서를 더 참조 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블배포] [ Distribute], [테이블 인덱스를 만들][Index], [테이블 분할] [ Partition] 및 [ 임시 테이블][Temporary]합니다.</span><span class="sxs-lookup"><span data-stu-id="eb899-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="eb899-317">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb899-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
