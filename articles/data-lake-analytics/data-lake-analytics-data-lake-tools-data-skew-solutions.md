---
title: "Azure Data Lake Tools for Visual Studio를 사용하여 데이터 기울이기 문제 해결 | Microsoft Docs"
description: "Azure Data Lake Tools for Visual Studio를 사용하여 데이터 기울이기 문제에 대한 잠재적인 해결 방법을 마련합니다."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 9b284ef33be4b935569fc368d81ddf040b2c2b7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="49b29-103">Azure Data Lake Tools for Visual Studio를 사용하여 데이터 기울이기 문제 해결</span><span class="sxs-lookup"><span data-stu-id="49b29-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="49b29-104">데이터 기울이기란?</span><span class="sxs-lookup"><span data-stu-id="49b29-104">What is data skew?</span></span>

<span data-ttu-id="49b29-105">간단히 말해 데이터 기울이기는 지나치게 많은 값입니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="49b29-106">세금 환급 감사를 위해 미국의 각 주당 세금 조사관을 한 명씩 총 50명을 지명했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-106">Imagine that you have assigned 50 tax examiners to audit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="49b29-107">와이오밍 주는 인구가 적기 때문에 이 지역을 맡은 조사관은 별로 할 일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-107">The Wyoming examiner, because the population there is small, has little to do.</span></span> <span data-ttu-id="49b29-108">하지만 캘리포니아 주는 인구가 많이 때문에 이 지역을 맡은 조사관은 매우 바쁠 것입니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-108">In California, however, the examiner is kept very busy because of the state's large population.</span></span>
    <span data-ttu-id="49b29-109">![데이터 기울이기 문제 예](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="49b29-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="49b29-110">이 시나리오에서는 전체 세금 조사관에게 데이터가 고르지 않게 분산되어 일부 조사관은 다른 조사관보다 많은 일을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-110">In our scenario, the data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="49b29-111">실제로 작업을 수행할 때 여기에 나온 세금 조사관 예와 같은 상황을 자주 경험할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-111">In your own job, you frequently experience situations like the tax-examiner example here.</span></span> <span data-ttu-id="49b29-112">좀 더 기술적인 용어로 말하자면 하나의 꼭짓점이 동료보다 훨씬 더 많은 데이터를 가져와서 다른 사람보다 더 많은 일을 하고 결과적으로 전체 작업 속도를 늦추는 상황을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes the vertex work more than the others and that eventually slows down an entire job.</span></span> <span data-ttu-id="49b29-113">더욱 문제가 되는 것은 꼭짓점은 5시간의 런타임 제한과 6GB의 메모리 제한과 같은 제한을 가질 수 있기 때문에 작업이 실패할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-113">What's worse, the job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="49b29-114">데이터 기울이기 문제 해결</span><span class="sxs-lookup"><span data-stu-id="49b29-114">Resolving data-skew problems</span></span>

<span data-ttu-id="49b29-115">Azure Data Lake Tools for Visual Studio는 작업에 데이터 기울이기 문제가 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="49b29-116">문제가 있을 경우 이 섹션의 해결 방법을 시도하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-116">If a problem exists, you can resolve it by trying the solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="49b29-117">해결 방법 1: 테이블 분할 향상</span><span class="sxs-lookup"><span data-stu-id="49b29-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-the-skewed-key-value-in-advance"></a><span data-ttu-id="49b29-118">옵션 1: 불균형된 키 값을 미리 필터링</span><span class="sxs-lookup"><span data-stu-id="49b29-118">Option 1: Filter the skewed key value in advance</span></span>

<span data-ttu-id="49b29-119">비즈니스 논리에 영향을 주지 않으면 사전에 높은 빈도 값을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-119">If it does not affect your business logic, you can filter the higher-frequency values in advance.</span></span> <span data-ttu-id="49b29-120">예를 들어, GUID 열에 000-000-000이 많은 경우 해당 값을 집계하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want to aggregate that value.</span></span> <span data-ttu-id="49b29-121">집계하기 전에 “WHERE GUID != “000-000-000””을 작성하면 높은 빈도 값을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” to filter the high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="49b29-122">옵션 2: 다른 파티션 또는 배포 키 선택</span><span class="sxs-lookup"><span data-stu-id="49b29-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="49b29-123">앞의 예제에서 해당 국가 전역의 세금 감사 워크로드만 확인하려면 ID 번호를 키로 선택하여 데이터 배포를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-123">In the preceding example, if you want only to check the tax-audit workload all over the country, you can improve the data distribution by selecting the ID number as your key.</span></span> <span data-ttu-id="49b29-124">다른 파티션/배포 키를 선택하면 때때로 데이터를 보다 고르게 배포할 수 있지만 이로 인해 비즈니스 논리에 영향을 주지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-124">Picking a different partition or distribution key can sometimes distribute the data more evenly, but you need to make sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="49b29-125">예를 들어, 각 주의 세금 합계를 계산하려면 _주_를 파티션 키로 지정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-125">For instance, to calculate the tax sum for each state, you might want to designate _State_ as the partition key.</span></span> <span data-ttu-id="49b29-126">이러한 문제가 계속되면 옵션 3을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="49b29-126">If you continue to experience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="49b29-127">옵션 3: 더 많은 파티션 또는 배포 키 추가</span><span class="sxs-lookup"><span data-stu-id="49b29-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="49b29-128">_주_만 파티션 키로 사용하는 대신 두 개 이상의 키를 분할에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="49b29-129">예를 들어, 데이터 파티션 크기를 줄이고 데이터를 더 고르게 배포하려면 _우편 번호_를 추가 파티션 키로 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-129">For example, consider adding _ZIP Code_ as an additional partition key to reduce data-partition sizes and distribute the data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="49b29-130">옵션 4: 라운드 로빈 배포 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="49b29-131">파티션 및 배포에 적합한 키가 없는 경우 라운드 로빈 배포를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-131">If you cannot find an appropriate key for partition and distribution, you can try to use round-robin distribution.</span></span> <span data-ttu-id="49b29-132">라운드 로빈 배포는 모든 행을 동등하게 처리하고 임의로 해당 버킷에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="49b29-133">데이터는 고르게 배포되지만 지역(구/군/시) 정보를 잃어 버리고 일부 작업에 대한 작업 성능도 저하될 수 있다는 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-133">The data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="49b29-134">또한 어떻게 해서라도 기울어진 키에 대한 집계를 수행할 경우 데이터 기울이기 문제가 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-134">Additionally, if you are doing aggregation for the skewed key anyway, the data-skew problem will persist.</span></span> <span data-ttu-id="49b29-135">라운드 로빈 배포에 대해 자세히 알아보려면 [REATE TABLE(U-SQL): 스키마로 테이블 만들기](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch)에서 U-SQL 테이블 배포 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b29-135">To learn more about round-robin distribution, see the U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-the-query-plan"></a><span data-ttu-id="49b29-136">해결 방법 2: 쿼리 계획 향상</span><span class="sxs-lookup"><span data-stu-id="49b29-136">Solution 2: Improve the query plan</span></span>

### <a name="option-1-use-the-create-statistics-statement"></a><span data-ttu-id="49b29-137">옵션 1: CREATE STATISTICS 문 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-137">Option 1: Use the CREATE STATISTICS statement</span></span>

<span data-ttu-id="49b29-138">U-SQL은 테이블에 CREATE STATISTICS 문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-138">U-SQL provides the CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="49b29-139">이 문은 쿼리 최적화 프로그램에 데이터 특성에 대한 자세한 정보(예: 테이블에 저장된 값 분포)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-139">This statement gives more information to the query optimizer about the data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="49b29-140">대부분의 쿼리에서 쿼리 최적화 프로그램은 고품질 쿼리 계획을 위해 필요한 통계를 이미 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-140">For most queries, the query optimizer already generates the necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="49b29-141">경우에 따라 CREATE STATISTICS로 추가 통계를 만들거나 쿼리 디자인을 수정하여 쿼리 성능을 개선해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-141">Occasionally, you might need to improve query performance by creating additional statistics with CREATE STATISTICS or by modifying the query design.</span></span> <span data-ttu-id="49b29-142">자세한 내용은 [CREATE STATISTICS(U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49b29-142">For more information, see the [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="49b29-143">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="49b29-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="49b29-144">통계 정보는 자동으로 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="49b29-145">통계를 다시 만들지 않고 테이블의 데이터를 업데이트할 경우 쿼리 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-145">If you update the data in a table without re-creating the statistics, the query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="49b29-146">옵션 2: SKEWFACTOR 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="49b29-147">각 주의 세금 합계를 계산하려는 경우 데이터 기울이기 문제를 방지하는 접근 방식인 GROUP BY 문을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-147">If you want to sum the tax for each state, you must use GROUP BY state, an approach that doesn't avoid the data-skew problem.</span></span> <span data-ttu-id="49b29-148">그러나 최적화 프로그램에서 실행 계획을 준비할 수 있도록 쿼리에 데이터 힌트를 제공하여 키의 데이터 기울이기를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-148">However, you can provide a data hint in your query to identify data skew in keys so that the optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="49b29-149">일반적으로 매개 변수를 0.5와 1로 설정할 수 있습니다. 여기서 0.5는 심각하지 않은 기울이기를 의미하고 1은 심각한 기울이기를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-149">Usually, you can set the parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="49b29-150">힌트는 현재 문 및 모든 다운스트림 문에 대한 실행 계획 최적화에 영향을 미치므로 잠재적으로 기울어진 키 인식 집계 전에 힌트를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-150">Because the hint affects execution-plan optimization for the current statement and all downstream statements, be sure to add the hint before the potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that the given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="49b29-151">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="49b29-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="49b29-152">옵션 3: ROWCOUNT 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="49b29-153">SKEWFACTOR 외에도 특정한 기울어진 키 조인 사례에서 다른 조인된 행 집합이 작다는 것을 알고 있는 경우 U-SQL 문에서 JOIN 앞에 ROWCOUNT 힌트를 추가하여 최적화 프로그램에 이 사실을 알려줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-153">In addition to SKEWFACTOR, for specific skewed-key join cases, if you know that the other joined row set is small, you can tell the optimizer by adding a ROWCOUNT hint in the U-SQL statement before JOIN.</span></span> <span data-ttu-id="49b29-154">그러면 최적화 프로그램에서 성능 향상에 도움이 될 수 있는 브로드캐스트 조인 전략을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-154">This way, optimizer can choose a broadcast join strategy to help improve performance.</span></span> <span data-ttu-id="49b29-155">ROWCOUNT는 데이터 기울이기 문제를 해결하지 않지만 몇 가지 추가 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-155">Be aware that ROWCOUNT does not resolve the data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="49b29-156">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="49b29-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information to determine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-the-user-defined-reducer-and-combiner"></a><span data-ttu-id="49b29-157">해결 방법 3: 사용자 정의 리듀서 및 결합자 향상</span><span class="sxs-lookup"><span data-stu-id="49b29-157">Solution 3: Improve the user-defined reducer and combiner</span></span>

<span data-ttu-id="49b29-158">때로는 사용자 정의 연산자를 작성하여 복잡한 프로세스 논리를 처리할 수 있으며 잘 작성된 리듀서와 결합자는 경우에 따라 데이터 기울이기 문제를 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-158">You can sometimes write a user-defined operator to deal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="49b29-159">옵션 1: 가능한 경우 재귀적(recursive) 리듀서 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="49b29-160">기본적으로 사용자 정의 리듀서는 비재귀 모드로 실행됩니다. 즉, 키에 대한 작업을 줄이면 단일 꼭짓점으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="49b29-161">그러나 기울어진 데이터인 경우 대량 데이터 집합이 단일 꼭짓점에서 처리되어 오랫동안 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-161">But if your data is skewed, the huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="49b29-162">성능 향상을 위해 코드에 재귀 모드에서 실행되도록 리듀서를 정의하는 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-162">To improve performance, you can add an attribute in your code to define reducer to run in recursive mode.</span></span> <span data-ttu-id="49b29-163">그런 다음 대량 데이터 집합을 여러 꼭짓점에 배포하고 병렬로 실행하여 작업 속도를 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-163">Then, the huge data sets can be distributed to multiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="49b29-164">비재귀적 리듀서를 재귀적 리듀서로 변경하려면 associativity(연결성) 알고리즘인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-164">To change a non-recursive reducer to recursive, you need to make sure that your algorithm is associative.</span></span> <span data-ttu-id="49b29-165">예를 들어 합계(sum)는 연결성이고 중앙값(median)은 연결성이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-165">For example, the sum is associative, and the median is not.</span></span> <span data-ttu-id="49b29-166">또한 리듀서의 입력 및 출력이 동일한 스키마를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-166">You also need to make sure that the input and output for reducer keep the same schema.</span></span>

<span data-ttu-id="49b29-167">재귀적 리듀서의 특성:</span><span class="sxs-lookup"><span data-stu-id="49b29-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="49b29-168">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="49b29-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="49b29-169">옵션 2: 가능한 경우 행 수준 결합자 모드 사용</span><span class="sxs-lookup"><span data-stu-id="49b29-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="49b29-170">특정 기울어진 키 조인의 경우 ROWCOUNT 힌트와 마찬가지로 결합자 모드는 여러 꼭짓점에 설정된 기울어진 대량 키 값을 배포하여 작업을 동시에 실행할 수 있도록 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-170">Similar to the ROWCOUNT hint for specific skewed-key join cases, combiner mode tries to distribute huge skewed-key value sets to multiple vertices so that the work can be executed concurrently.</span></span> <span data-ttu-id="49b29-171">결합자 모드는 데이터 기울이기 문제를 해결할 수는 없지만 기울어진 대량 키 값 집합에 추가적인 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="49b29-172">기본적으로 결합자 모드는 왼쪽 행 집합과 오른쪽 행 집합을 분리할 수 없음을 의미하는 Full입니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-172">By default, the combiner mode is Full, which means that the left row set and right row set cannot be separated.</span></span> <span data-ttu-id="49b29-173">Left/Right/Inner 모드로 설정하면 행 수준 조인이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-173">Setting the mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="49b29-174">시스템은 해당 행 집합을 분리하고 병렬로 실행되는 여러 꼭짓점에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-174">The system separates the corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="49b29-175">그러나 결합자 모드를 구성하기 전에 해당 행 집합을 분리할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-175">However, before you configure the combiner mode, be careful to ensure that the corresponding row sets can be separated.</span></span>

<span data-ttu-id="49b29-176">다음 예제는 분리된 왼쪽 행 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-176">The example that follows shows a separated left row set.</span></span> <span data-ttu-id="49b29-177">각 출력 행은 왼쪽의 단일 입력 행에 따라 달라지며, 잠재적으로 동일한 키 값을 갖는 오른쪽의 모든 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-177">Each output row depends on a single input row from the left, and it potentially depends on all rows from the right with the same key value.</span></span> <span data-ttu-id="49b29-178">결합자 모드를 왼쪽으로 설정하면 시스템에서 왼쪽의 대량 행 집합을 작은 집합으로 분리하여 여러 개의 꼭짓점에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-178">If you set the combiner mode as left, the system separates the huge left-row set into small ones and assigns them to multiple vertices.</span></span>

![결합자 모드 그림](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="49b29-180">잘못된 결합자 모드를 설정하면 결합 효율이 떨어지고 결과가 잘못될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-180">If you set the wrong combiner mode, the combination is less efficient, and the results might be wrong.</span></span>

<span data-ttu-id="49b29-181">결합자 모드의 특성:</span><span class="sxs-lookup"><span data-stu-id="49b29-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all the input rows from left and right with the same key value.

- <span data-ttu-id="49b29-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): 모든 출력 행은 왼쪽의 단일 입력 행에 따라 달라지며, 잠재적으로 동일한 키 값을 갖는 오른쪽의 모든 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from the left (and potentially all rows from the right with the same key value).</span></span>

- <span data-ttu-id="49b29-183">SqlUserDefinedCombiner(Mode=CombinerMode.Right): 모든 출력 행은 오른쪽의 단일 입력 행에 따라 달라지며, 잠재적으로 동일한 키 값을 갖는 왼쪽의 모든 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from the right (and potentially all rows from the left with the same key value).</span></span>

- <span data-ttu-id="49b29-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): 모든 출력 행은 동일한 값을 갖는 왼쪽과 오른쪽의 단일 입력 행에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="49b29-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from the left and the right with the same value.</span></span>

<span data-ttu-id="49b29-185">코드 예제:</span><span class="sxs-lookup"><span data-stu-id="49b29-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
