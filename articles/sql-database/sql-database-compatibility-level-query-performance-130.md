---
title: "데이터베이스 호환성 수준 130 - Azure SQL Database | Microsoft Docs"
description: "이 문서에서는 Azure SQL Database를 호환성 수준 130으로 실행하고 새로운 쿼리 최적화 프로그램과 쿼리 프로세서 기능의 이점을 활용하여 얻을 수 있는 이점에 대해 살펴봅니다. 또한 기존 SQL 응용 프로그램의 쿼리 성능에 발생할 수 있는 잠재적인 부작용도 해결합니다."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="269b5-104">Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능</span><span class="sxs-lookup"><span data-stu-id="269b5-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="269b5-105">Azure SQL 데이터베이스는 다양한 호환성 수준에서 수십만 개의 데이터베이스를 투명하게 실행하고 있으며, Microsoft SQL Server 해당 버전의 모든 고객을 위해 이전 버전과의 호환성을 유지 및 보장하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="269b5-106">이 문서에서는 Azure SQL Databse를 호환성 수준 130으로 실행하고 새로운 쿼리 최적화 프로그램과 쿼리 프로세서 기능의 이점을 활용하여 얻을 수 있는 이점에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="269b5-107">또한 기존 SQL 응용 프로그램의 쿼리 성능에 발생할 수 있는 잠재적인 부작용도 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="269b5-108">지난 기록을 확인하자면, 기본 호환성 수준 대비 SQL 버전 내역은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="269b5-109">100: SQL Server 2008 및 Azure SQL 데이터베이스 V11.</span><span class="sxs-lookup"><span data-stu-id="269b5-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="269b5-110">110: SQL Server 2012 및 Azure SQL 데이터베이스 V11.</span><span class="sxs-lookup"><span data-stu-id="269b5-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="269b5-111">120: SQL Server 2014 및 Azure SQL 데이터베이스 V12.</span><span class="sxs-lookup"><span data-stu-id="269b5-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="269b5-112">130: SQL Server 2016 및 Azure SQL 데이터베이스 V12.</span><span class="sxs-lookup"><span data-stu-id="269b5-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="269b5-113">**2016년 6월 중순**을 시작으로, Azure SQL Database에서 **새로 만든** 데이터베이스에 대한 기본 호환성 수준은 120이 아니라 130이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="269b5-114">2016년 6월 중순 전에 만든 데이터베이스는 영향을 받지 *않고* , 현재 호환성 수준(100, 110, 또는 120)을 유지하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="269b5-115">Azure SQL Database 버전 V11에서 V12로 마이그레이션 된 데이터베이스의 호환성 수준은 100 또는 110입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="269b5-116">호환성 수준 130에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="269b5-116">About compatibility level 130</span></span>
<span data-ttu-id="269b5-117">먼저, 데이터베이스의 현재 호환성 수준을 알아보려면, 다음 Transact-SQL 문을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="269b5-118">**새로** 생성되는 데이터베이스에 수준 130이 적용되는 상황이 벌어지기 전에, 매우 기본적인 쿼리 예제를 통해 무엇이 변하는 것인지, 그것을 통해 어떻게 이익을 얻을 수 있을지에 대해 검토하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="269b5-119">관계형 데이터베이스에서의 쿼리 처리는 매우 복잡하며 본질적인 디자인에 대한 선택과 동작을 이해하려면 수많은 컴퓨터 공학과 수학으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="269b5-120">이 문서에서는, 최소의 기술적 지식이 있다면 누구나 호환성 수준의 변경이 미치는 영향을 이해하고 응용 프로그램에 어떠한 이점을 줄 수 있는지 판단할 수 있도록 하기 위하여 콘텐츠를 의도적으로 간소화하였습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="269b5-121">호환성 수준 130이 가져다 주는 것이 무엇인지 테이블에서 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="269b5-122">[ALTER DATABASE 호환성 수준(Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)에서 자세한 내용을 볼 수 있지만, 여기에 간략한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="269b5-123">Insert-select 문의 삽입 작업이, 이전에는 단일 스레드였지만, 다중 스레드로 만들어 지거나 병렬 계획을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="269b5-124">메모리 액세스에 최적화된 테이블 및 테이블 변수 쿼리가, 이전에는 단일 스레드 작업이었지만, 이제 병렬 계획을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="269b5-125">메모리 액세스에 최적화된 테이블에 대한 통계를 이제 샘플링하고 자동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="269b5-126">자세한 내용은 [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) (데이터베이스 엔진의 새로운 기능: 메모리 내 OLTP)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="269b5-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="269b5-127">배치 모드 및 행 모드가 열 저장소 인덱스와 함께 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="269b5-128">열 저장소 인덱스를 통한 테이블 정렬이 이제 배치 모드로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="269b5-129">기간 이동 집계가 이제 배치 모드(예: TSQL LAG/LEAD 문)로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="269b5-130">여러 개의 다른 절을 포함하는 열 저장소 테이블에 대한 쿼리가 배치 모드에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="269b5-131">직렬 계획 또는 DOP=1 하에서 실행되는 쿼리도 배치 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="269b5-132">마지막으로 카디널리티 예측 향상이 호환성 수준 120에 실제 포함되지만, 이 보다 낮은 호환성 수준(예: 100 또는 110)에서 실행하는 경우, 호환성 수준 130으로 이동하면 이러한 향상이 동반되며, 응용 프로그램의 쿼리 성능에도 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="269b5-133">호환성 수준 130 연습</span><span class="sxs-lookup"><span data-stu-id="269b5-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="269b5-134">우선, 일부 새로운 기능을 연습하기 위해 테이블, 인덱스 및 난수 데이터를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="269b5-135">TSQL 스크립트 예제는 SQL Server 2016, 또는 Azure SQL 데이터베이스에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="269b5-136">하지만, Azure SQL 데이터베이스를 만드는 경우, 다중 스레딩을 허용하여 이러한 기능으로부터 이익을 얻기 위해 코어가 적어도 두 개 필요하기 때문에 최소 P2 데이터베이스를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="269b5-137">이제, 호환성 수준 130과 함께 제공되는 일부 쿼리 처리 기능을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="269b5-138">병렬 삽입</span><span class="sxs-lookup"><span data-stu-id="269b5-138">Parallel INSERT</span></span>
<span data-ttu-id="269b5-139">아래 TSQL 문을 실행하면 호환성 수준 120 및 130에서 INSERT 작업이 실행되며, 이것은 단일 스레드 모델(120) 및 다중 스레드 모델(130)에서 각각 작업을 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-140">실제 쿼리 계획을 요청하고, 그에 대한 그래픽 표현 또는 XML 콘텐츠를 살펴보면, 실행 중인 Cardinality Estimation 함수를 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="269b5-141">그림 1의 계획을 나란히 살펴보면, Column Store INSERT 실행이 120의 경우 직렬에서 130의 경우 병렬로 이동한 것을 명확하게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="269b5-142">또한, 130 계획의 반복기 아이콘이, 이제 반복기 실행도 실제로 병렬이라는 사실을 나타내는, 두 개의 병렬 화살표를 나타내도록 변경된 것이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="269b5-143">대규모 INSERT 작업을 완료해야 하는 경우, 병렬 실행이, 데이터베이스에 대해 원하는 대로 사용할 수 있는 수의 코어에 연결되어 있으면, 상황에 따라서 최대 100배 빠른 성능을 낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="269b5-144">*그림 1: 호환성 수준 130에서 INSERT 작업은 직렬에서 병렬로 변경됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![그림 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="269b5-146">직렬 배치 모드</span><span class="sxs-lookup"><span data-stu-id="269b5-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="269b5-147">마찬가지로, 데이터 행을 처리할 때 호환성 수준 130으로 이동하면 배치 모드 처리가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="269b5-148">첫째, 배치 모드 작업은 열 저장소 인덱스가 있어야만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="269b5-149">둘째, 하나의 배치는 일반적으로 900행을 나타내고, 멀티 코어 CPU, 높은 메모리 처리량에 최적화된 코드 논리를 사용하며, 가능하면 열 저장소의 압축 데이터를 직접 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="269b5-150">이러한 조건 하에서, SQL Server 2016은 한 번에 최대 900개의 행을 처리할 수 있고(한 번에 1개의 행이 아닌), 그 결과, 작업의 전반적인 오버헤드 비용이 전체 배치에 의해 공유되기 때문에, 행별 전체 비용이 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="269b5-151">이렇게 공유되는 작업 양이 열 저장소 압축과 결합되면 SELECT 배치 모드 작업에 관련된 대기 시간이 근본적으로 감소됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="269b5-152">열 저장소 및 배치 모드에 대한 자세한 내용은 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="269b5-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-153">아래에서 볼 수 있듯이, 그림 2의 쿼리 계획을 나란히 살펴보면, 처리 모드가 호환성 수준과 함께 변경된 것을 볼 수 있으며, 그 결과, 두 가지 호환성 모드에서 모두 함께 쿼리를 실행하면, 두 개의 배치가 처리된 시간에, 대부분의 처리 시간이 배치 모드(14%)와 비교하면 행 모드(86%)에 소요된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="269b5-154">데이터 집합을 증가시키면 이점이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="269b5-155">*그림 2: 호환성 수준 130에서 SELECT 작업은 직렬에서 배치 모드로 변경됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![그림 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="269b5-157">배치 모드에서 정렬 실행</span><span class="sxs-lookup"><span data-stu-id="269b5-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="269b5-158">위와 마찬가지로 정렬 작업을, 행 모드(호환성 수준 120)에서 배치 모드(호환성 수준 130)로 전환하면 SORT 작업의 성능이 같은 이유로 인해 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-159">그림 3에 나란히 보이는 것처럼, 행 모드의 정렬 작업은 비용의 81%를 나타내는 반면, 배치 모드는 비용의 19%만을 나타냅니다(각각 정렬의 81% 및 56%).</span><span class="sxs-lookup"><span data-stu-id="269b5-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="269b5-160">*그림 3: 호환성 수준 130에서 SORT 작업은 행에서 배치 모드로 변경됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![그림 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="269b5-162">물론, 여기의 샘플은 행을 수만 개만 포함하며, 이것은 요즘 대부분의 SQL Server에서 사용할 수 있는 데이터를 살펴볼 때 매우 미미한 양입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="269b5-163">대신, 이것을 수백만 개의 행에 투영하면, 워크로드의 특성에 따라 매일 몇 분 동안의 실행을 절약하는 것으로 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="269b5-164">카디널리티 예측(CE) 향상</span><span class="sxs-lookup"><span data-stu-id="269b5-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="269b5-165">SQL Server 2014에 도입된, 호환성 수준 120 이상에서 실행되는 모든 데이터베이스는 새로운 카디널리티 예측 기능을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="269b5-166">본질적으로, 카디널리티 예측은 SQL Server에서 예상 비용을 기반으로 쿼리를 실행하는 방식을 결정하는 데 사용되는 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="269b5-167">예측은 쿼리와 관련된 개체와 연결된 통계로부터의 입력을 사용하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="269b5-168">사실상, 대략적으로, Cardinality Estimation 함수는 값의 분포, 별도의 값의 개수, 쿼리에 의해 참조되는 개체 및 테이블에 포함된 중복 개수에 대한 정보에 따른 행 개수에 대한 예측입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="269b5-169">이러한 예측이 잘못되는 경우에 대한 몇 가지 예를 들자면, 불필요한 메모리 허용(예: TempDB 유출)으로 인해 불필요한 디스크 I/O가 발생하거나, 병렬 계획 실행 대신 직렬 계획 실행이 선택될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="269b5-170">요컨대, 잘못된 예측은 전반적인 쿼리 실행 성능을 저하시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="269b5-171">반면에, 우수한 예측, 보다 정확한 예측은 쿼리 실행 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="269b5-172">앞서 언급했듯이, 쿼리 최적화와 예측은 복잡한 사안이지만, 쿼리 계획 및 카디널리티 평가기에 대해 자세히 알아보려면, [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) (SQL Server 2014 카디널리티 평가기를 사용하여 쿼리 계획 최적화)에서 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="269b5-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="269b5-173">현재 어떤 카디널리티 예측을 사용하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="269b5-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="269b5-174">어떤 카디널리티 예측 하에서 쿼리가 실행되고 있는지를 알아보기 위해서 아래 쿼리 샘플을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="269b5-175">첫째 예제는 호환성 수준 110에서 실행되며, 이것은 오래된 Cardinality Estimation 함수를 사용한다는 의미를 내포합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-176">실행이 완료되면, XML 링크를 클릭하고, 아래와 같이 첫째 반복기의 속성을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="269b5-177">CardinalityEstimationModelVersion이라는 속성 이름은 현재 70으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="269b5-178">이것은 데이터베이스 호환성 수준이 SQL Server 7.0 버전(위의 TSQL 문에서 볼 수 있듯이 110으로 설정되어 있음)으로 설정되어 있다는 것을 의미하는 것은 아니며, 70이라는 값은 단지 SQL Server 7.0 이상에서 사용할 수 있는 레거시 카디널리티 예측 기능을 나타내고, SQL Server 7.0 이상은 SQL Server 2014(호환성 수준 120이 제공되는)까지 중요한 수정 내용이 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="269b5-179">*그림 4: 호환성 수준을 110 이하로 사용할 때 CardinalityEstimationModelVersion은 70으로 설정됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![그림 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="269b5-181">아니면, 호환성 수준을 130으로 변경하고, ON으로 설정된 LEGACY_CARDINALITY_ESTIMATION 설정과 [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)을 사용하여 새 Cardinality Estimation 함수의 사용을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="269b5-182">이렇게 하면 Cardinality Estimation 함수의 측면에서 110을 사용하는 것과 똑같지만, 최신 쿼리 처리 호환성 수준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="269b5-183">이렇게 하면, 최신 호환성 수준(예: 배치 모드)에 제공되는 새로운 쿼리 처리 기능의 이점을 얻을 수 있지만, 필요한 경우 이전 카디널리티 예측 기능에 여전히 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-184">호환성 수준을 120 또는 130으로 이동만 하면, 새로운 카디널리티 예측 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="269b5-185">이런 경우, 기본 CardinalityEstimationModelVersion은 그에 맞춰 120 또는 130으로 아래와 같이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-186">*그림 5: 호환성 수준 130을 사용하면 CardinalityEstimationModelVersion이 130으로 설정됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![그림 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="269b5-188">카디널리티 예측 차이 살펴보기</span><span class="sxs-lookup"><span data-stu-id="269b5-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="269b5-189">이제, 조건자와 INNER JOIN과 WHERE 절이 포함된 약간 더 복잡한 쿼리를 실행하고 이전 Cardinality Estimation 함수의 행 개수 예측을 우선 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-190">이 쿼리를 효과적으로 실행하면 200,704개의 행이 반환되는 반면에, 이전 카디널리티 예측 기능은 194,284개의 행을 예측합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="269b5-191">물론, 앞서 언급했듯이, 이러한 행 개수 결과는 이전 샘플을 얼마나 자주 실행하느냐에 달려 있으며, 샘플을 실행할 때마다 샘플 테이블이 계속해서 다시 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="269b5-192">물론, 쿼리의 조건자도 테이블 모양, 데이터 콘텐츠, 데이터가 서로 상관 관계를 맺는 실제 방식과 별개로 실제 예측에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="269b5-193">*그림 6: 행 개수 예측은 194,284개 이거나 예측된 200,704개 행에서 6,000개 행이 해제됩니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![그림 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="269b5-195">같은 방식으로, 이제 카디널리티 예측 기능을 사용하여 동일한 쿼리를 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="269b5-196">아래를 살펴보면, 행 예측이 202,877이거나, 이전 카디널리티 예측보다 훨씬 더 가깝고 큰 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="269b5-197">*그림 7: 행 개수 예측이 이제 194,284가 아니라 202,877입니다.*</span><span class="sxs-lookup"><span data-stu-id="269b5-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![그림 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="269b5-199">실제로, 결과 집합은 200,704행입니다.(하지만 모든 것은 이전 샘플의 쿼리를 얼마나 자주 실행했는가에 달려 있고, 그 보다 더 중요한 것은, TSQL이 RAND() 문을 사용하기 때문에, 실제 반환되는 값이 실행할 때마다 다를 수 있다는 점입니다.)</span><span class="sxs-lookup"><span data-stu-id="269b5-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="269b5-200">따라서, 이 예제에서는 202,877이 194,284보다 200,704에 훨씬 더 가깝기 때문에, 새 카디널리티 예측이 행의 개수를 더 잘 측정했습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="269b5-201">마지막으로 WHERE 절 조건자를 같음(예를 들면 “>” 대신)으로 변경하면, 일치하는 수가 얼마나 되느냐에 따라서, 이전 카디널리티 함수와 새로운 카디널리티 함수의 예측이 한층 더 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="269b5-202">물론, 이 경우, 실제 카운트에서 최대 6000개의 행이 해제되면 상황에 따라서 많은 데이터를 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="269b5-203">이제, 이것을 더 복잡한 쿼리와 여러 개의 테이블에 걸친 수백만 개의 행으로 이동하면, 때때로 예측이 수백만 개의 행에 의해 해제될 수 있으며, 따라서, 잘못된 실행 계획을 선택하거나 부족한 메모리를 요청할 위험으로 인해 TempDB 유출이 발생하고, I/O가 훨씬 더 많아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="269b5-204">기화가 된다면, 가장 일반적인 쿼리와 데이터 집합을 사용하여 이러한 비교를 연습하고, 이전 예측과 새로운 예측에 얼마나 영향을 미치는지 직접 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="269b5-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="269b5-205">경우에 따라 실제보다 더 밑돌 수도 있고, 결과 집합에 실제로 반환되는 실제 행 카운트에 더 가까울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="269b5-206">이 모든 것은 쿼리의 모양, Azure SQL 데이터베이스의 특성, 데이터베이스의 본질 및 크기, 그리고 이들 항목에 대해 사용할 수 있는 통계에 달려 있습니다 Azure SQL 데이터베이스 인스턴스를 만들었다면, 쿼리 최적화 프로그램은 이전 쿼리 실행에서 생성된 통계를 다시 사용하는 대신 정보를 처음부터 다시 구축해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="269b5-207">따라서, 예측은 모든 서버 및 응용 프로그램 각각의 상황에 따라 매우 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="269b5-208">이런 중요한 측면을 염두에 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="269b5-209">고려해야 할 몇 가지 사항</span><span class="sxs-lookup"><span data-stu-id="269b5-209">Some considerations to take into account</span></span>
<span data-ttu-id="269b5-210">대부분의 워크로드는 호환성 수준 130을 통해 이점을 갖게 되지만, 프로덕션 환경에 대한 호환성 수준을 채택하기 전에, 기본적으로 3가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="269b5-211">호환성 수준 130이로 이동하고, 성능 추이를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="269b5-212">성능이 떨어지는 경우에는, 호환성 수준을 이전 수준으로 되돌리거나, 130을 유지하고 카디널리티 예측만 레거시 모드로 되돌립니다.(앞서 설명했듯이, 이것만으로 문제를 해결할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="269b5-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="269b5-213">비슷한 프로덕션 부하에서 기존 응용 프로그램을 철저히 테스트하여, 미세 조정하고, 프로덕션에 적용하기 전에 성능의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="269b5-214">문제가 발생하는 경우, 위와 마찬가지로, 언제나 이전 호환성 수준으로 되돌릴 수 있고 아니면 카디널리티 예측만 레거시 모드로 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="269b5-215">마지막 옵션이면서, 이러한 질문을 해결하는 최신의 방법은 쿼리 저장소를 활용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="269b5-216">이것이 현재 권장되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-216">That’s today’s recommended option!</span></span> <span data-ttu-id="269b5-217">호환성 수준 130대비 120이하의 쿼리 분석을 지원하기 위해, 쿼리 저장소를 사용하는 것은 매우 바람직합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="269b5-218">쿼리 저장소는 Azure SQL 데이터베이스 V12 최신 버전에 제공되며, 쿼리 성능 문제 해결을 지원하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="269b5-219">쿼리 저장소는 모든 쿼리에 대한 자세한 기록 정보를 수집하고 제공하는 데이터베이스에 대한 블랙박스라고 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="269b5-220">이것은 문제를 진단하고 해결하는 시간을 줄여서 성능에 대한 기술적 조사를 크게 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="269b5-221">자세한 내용은 [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(쿼리 저장소: 데이터베이스에 대한 블랙박스)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="269b5-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="269b5-222">대략적으로, 호환성 수준 120 이하에서 실행 중인 데이터베이스 집합이 있고 그 중 일부를 130으로 이동할 계획이거나, 워크로드가 새 데이터베이스를 자동으로 프로비전하기 때문에 곧 130으로 기본 설정될 예정인 경우에는, 다음 사항을 고려하십시오.</span><span class="sxs-lookup"><span data-stu-id="269b5-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="269b5-223">프로덕션을 새 호환성 수준으로 변경하기 전에, 쿼리 저장소를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="269b5-224">자세한 내용은 [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) (데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="269b5-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="269b5-225">다음으로, 프로덕션과 유사한 환경의 대표적인 데이터와 쿼리를 사용하여 모든 중요한 워크로드를 테스트하여, 체감 성능과 쿼리 저장소에 의해 보고되는 성능을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="269b5-226">성능 저하를 체감한다면, 쿼리 저장소에서 회귀된 쿼리를 파악하여 쿼리 저장소의 옵션을 강제 적용하는 계획을(즉, 계획 고정) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="269b5-227">이런 경우, 호환성 수준 130을 반드시 유지하고, 쿼리 저장소의 제시에 따라 이전 쿼리 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="269b5-228">Azure SQL 데이터베이스의(SQL Server 2016을 실행하는) 새로운 기능과 성능을 활용하고 싶지만, 호환성 수준 130이 가져오는 변화에 신경이 쓰이는 경우에는, 최후의 수단으로, ALTER DATABASE 문을 사용하여 사용자의 워크로드에 적합한 수준으로 호환성 수준을 되돌리는 것을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="269b5-229">하지만 먼저, 130을 사용하지 않는다면 근본적으로 이전 SQL Server 버전의 성능 수준을 유지하는 것이므로, 쿼리 저장소 계획 고정 옵션이 최고의 옵션이라는 점을 인지하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="269b5-230">다수의 데이터베이스에 걸쳐있는 다중 테넌트 응용 프로그램이 있다면, 이전에 프로비전한 데이터베이스와 새로 프로비전한 데이터베이스를 비롯한 모든 데이터베이스에 대해 일관적인 호환성 수준을 보장하기 위해, 데이터베이스의 프로비전 논리를 업데이트하는 것이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="269b5-231">응용 프로그램 워크로드 성능은 일부 데이터베이스가 다른 호환성 수준에서 실행되는 경우에 민감하게 영향을 받을 수 있기 때문에, 모든 사용자에게 전반적으로 동일한 환경을 제공하려면, 모든 데이터베이스에 대해 일관적인 호환성 수준을 적용할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="269b5-232">필수 사항은 아니며, 응용 프로그램이 호환성 수준에 의해 어떻게 영향을 받는가에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="269b5-233">마지막으로, 카디널리티 예측과 관련하여, 호환성 수준 변경과 마찬가지로, 프로덕션에 적용하기 전에, 새로운 조건 하에서 프로덕션 워크로드를 테스트하고 카디널리티 예측 향상을 통해 응용 프로그램에 이로운 점이 있는지를 측정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="269b5-234">결론</span><span class="sxs-lookup"><span data-stu-id="269b5-234">Conclusion</span></span>
<span data-ttu-id="269b5-235">Azure SQL 데이터베이스를 사용하여 SQL Server 2016의 모든 개선 사항을 활용하면 쿼리 실행이 분명히 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="269b5-236">얘기한 그대로 입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-236">Just as-is!</span></span> <span data-ttu-id="269b5-237">물론, 다른 새로운 기능과 마찬가지로, 데이터베이스 워크로드가 최고로 작동되는 정확한 조건을 측정하기 위해 적절한 평가가 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="269b5-238">경험에 의하면, 대부분의 워크로드는 호환성 수준 130 하에서, 새로운 쿼리 처리 기능 및 새 카디널리티 예측을 처리하면서, 최소한 투명하게 실행될 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="269b5-239">그렇긴 하지만, 현실적으로, 언제나 예외는 있으며 적절하고 부단하게 주의를 기울이는 것이 이러한 개선 사항의 이점을 얼마나 활용할 수 있는지를 결정하는 중요한 척도가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="269b5-240">다시 말하지만, 쿼리 저장소는 이러한 작업을 수행하는데 큰 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="269b5-241">SQL Azure 개발이 계속되고 있으니, 장차 호환성 수준 140을 기대해도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="269b5-242">적절한 시기가 되면, 현재 호환성 수준 130을 통해 가능해 지는 것들을 여기에서 간략하게 설명했듯이, 미래의 호환성 수준 140을 통해 가능해지는 것들에 관해 간략하게 설명할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="269b5-243">일단은, 2016년 6월부터 Azure SQL 데이터베이스가 새로 생성되는 데이터베이스에 대한 기본 호환성 수준을 120에서 130으로 변경한다는 점을 기억하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="269b5-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="269b5-244">잊지 마세요!</span><span class="sxs-lookup"><span data-stu-id="269b5-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="269b5-245">참조</span><span class="sxs-lookup"><span data-stu-id="269b5-245">References</span></span>
* [<span data-ttu-id="269b5-246">데이터베이스 엔진의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="269b5-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="269b5-247">블로그: 쿼리 저장소: 데이터베이스에 대한 블랙박스, 작성자: Borko Novakovic, 2016년 6월 8일</span><span class="sxs-lookup"><span data-stu-id="269b5-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="269b5-248">ALTER DATABASE 호환성 수준(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="269b5-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="269b5-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="269b5-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="269b5-250">Azure SQL 데이터베이스 V12에 대한 호환성 수준 130</span><span class="sxs-lookup"><span data-stu-id="269b5-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="269b5-251">SQL Server 2014 카디널리티 평가기를 사용하여 쿼리 계획 최적화</span><span class="sxs-lookup"><span data-stu-id="269b5-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="269b5-252">Columnstore 인덱스 가이드</span><span class="sxs-lookup"><span data-stu-id="269b5-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="269b5-253">블로그: Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능, 작성자: Alain Lissoir, 2016년 5월 6일</span><span class="sxs-lookup"><span data-stu-id="269b5-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
