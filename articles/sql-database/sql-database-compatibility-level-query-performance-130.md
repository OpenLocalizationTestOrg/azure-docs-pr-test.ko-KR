---
title: "aaaDatabase 호환성 수준 130-Azure SQL 데이터베이스 | Microsoft Docs"
description: "이 문서에서는 호환성 수준 130에서 Azure SQL 데이터베이스를 실행 하 고 hello 새 쿼리 최적화 프로그램의 hello 혜택을 활용 하 여 hello 이점을 탐색 하 고 쿼리 프로세서 기능. Hello 가능한 부작용 hello 기존 SQL 응용 프로그램에 대 한 hello 쿼리 성능에 해결합니다."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="da1b0-104">Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능</span><span class="sxs-lookup"><span data-stu-id="da1b0-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="da1b0-105">Azure SQL 데이터베이스 실행 투명 하 게 수백, 수천 데이터베이스의 여러 다른 호환성 수준에서 유지 하 고 모든 고객에 대 한 hello 이전 버전과 호환성 toohello Microsoft SQL Server의 해당 버전을 보장 하기!</span><span class="sxs-lookup"><span data-stu-id="da1b0-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="da1b0-106">이 문서에서는 호환성 수준 130에서 Azure SQL 데이터베이스를 실행 하 고 hello 새 쿼리 최적화 프로그램의 hello 혜택을 활용 하 여 hello 이점을 탐색 하 고 쿼리 프로세서 기능.</span><span class="sxs-lookup"><span data-stu-id="da1b0-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="da1b0-107">Hello 가능한 부작용 hello 기존 SQL 응용 프로그램에 대 한 hello 쿼리 성능에 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="da1b0-108">기록의 알림으로 SQL 버전 toodefault 호환성 수준의 hello 맞춤은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="da1b0-109">100: SQL Server 2008 및 Azure SQL 데이터베이스 V11.</span><span class="sxs-lookup"><span data-stu-id="da1b0-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="da1b0-110">110: SQL Server 2012 및 Azure SQL 데이터베이스 V11.</span><span class="sxs-lookup"><span data-stu-id="da1b0-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="da1b0-111">120: SQL Server 2014 및 Azure SQL 데이터베이스 V12.</span><span class="sxs-lookup"><span data-stu-id="da1b0-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="da1b0-112">130: SQL Server 2016 및 Azure SQL 데이터베이스 V12.</span><span class="sxs-lookup"><span data-stu-id="da1b0-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da1b0-113">부터는 **mid-2016 년 6 월**, Azure SQL 데이터베이스 hello 기본 호환성 수준 130에 대 한 120 대신 됩니다 **새로 만든** 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="da1b0-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="da1b0-114">2016년 6월 중순 전에 만든 데이터베이스는 영향을 받지 *않고* , 현재 호환성 수준(100, 110, 또는 120)을 유지하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="da1b0-115">Azure SQL 데이터베이스 버전 V11 tooV12에서에서 마이그레이션된 데이터베이스 호환성 수준이 100 또는 110 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="da1b0-116">호환성 수준 130에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="da1b0-116">About compatibility level 130</span></span>
<span data-ttu-id="da1b0-117">첫째, 데이터베이스의 tooknow hello 현재 호환성 수준을 원한다 면 hello Transact SQL 문 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="da1b0-118">이러한 변경 전에 toolevel 130에 대 한 발생 **새로** 보겠습니다이 변경은 란 모두에 대 한 몇 가지 기본적인 쿼리 예를 통해 검토 하 고 여기에서 얻을 수 누구나 어떻게 참조 데이터베이스를 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="da1b0-119">관계형 데이터베이스에서 쿼리 처리 매우 복잡할 수 있으며 toolots 컴퓨터 과학, 수학 toounderstand hello 고유 설계 선택 및 동작을 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="da1b0-120">이 문서에서는 hello 콘텐츠 의도적으로 단순화 된 tooensure는 최소 기술 배경 지식이 있는 모든 사용자 수 hello 호환성 수준 변경이 미치는 hello 영향을 이해 하 고 응용 프로그램에 이점을 얻을 수 있습니다 어떻게 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="da1b0-121">Hello 호환성 수준을 130 hello 테이블에는 개요 죠.</span><span class="sxs-lookup"><span data-stu-id="da1b0-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="da1b0-122">[ALTER DATABASE 호환성 수준(Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)에서 자세한 내용을 볼 수 있지만, 여기에 간략한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="da1b0-123">hello Insert select 문의 삽입 작업 다중 스레드 수 또는 병렬 계획을 가질 수 있습니다 하지만 전에이 작업이 단일 스레드입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="da1b0-124">메모리 액세스에 최적화된 테이블 및 테이블 변수 쿼리가, 이전에는 단일 스레드 작업이었지만, 이제 병렬 계획을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="da1b0-125">메모리 액세스에 최적화된 테이블에 대한 통계를 이제 샘플링하고 자동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="da1b0-126">자세한 내용은 [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) (데이터베이스 엔진의 새로운 기능: 메모리 내 OLTP)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da1b0-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="da1b0-127">배치 모드 및 행 모드가 열 저장소 인덱스와 함께 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="da1b0-128">열 저장소 인덱스를 통한 테이블 정렬이 이제 배치 모드로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="da1b0-129">기간 이동 집계가 이제 배치 모드(예: TSQL LAG/LEAD 문)로 진행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="da1b0-130">여러 개의 다른 절을 포함하는 열 저장소 테이블에 대한 쿼리가 배치 모드에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="da1b0-131">직렬 계획 또는 DOP=1 하에서 실행되는 쿼리도 배치 모드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="da1b0-132">마지막으로, 호환성 수준이 120 되지만 그룹 정책 실행에 낮은 호환성 수준 (100 또는 110)에 대 한 카디널리티 추정 개선 실제로 들어오는, hello 이동 toocompatibility 수준 130 또한 나타납니다 이러한 향상 된이 기능 및 이러한 수도 있습니다. 응용 프로그램의 hello 쿼리 성능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="da1b0-133">호환성 수준 130 연습</span><span class="sxs-lookup"><span data-stu-id="da1b0-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="da1b0-134">첫 번째 살펴보겠습니다 일부 테이블, 인덱스 및 생성 된 난수 데이터 toopractice 이러한 새로운 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="da1b0-135">Azure SQL 데이터베이스 또는 SQL Server 2016 hello TSQL 스크립트 예제를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="da1b0-136">그러나 Azure SQL 데이터베이스를 만들 때 최소한 두 가지 다중 스레드 코어 tooallow hello 최소 P2 필요 하기 때문에 데이터베이스에서 선택 하 고 따라서 이러한 기능을 활용 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="da1b0-137">이제 호환성 수준 130으로 들어오는 hello 쿼리 처리 기능 모양 toosome 죠.</span><span class="sxs-lookup"><span data-stu-id="da1b0-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="da1b0-138">병렬 삽입</span><span class="sxs-lookup"><span data-stu-id="da1b0-138">Parallel INSERT</span></span>
<span data-ttu-id="da1b0-139">Hello 호환성 수준 120 및 130, 다중 스레드 모델 (130) 및 단일 스레드 모델 (120)에서 각각 hello 삽입 작업을 실행 하는 삽입 작업을 실행 아래 hello TSQL 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="da1b0-140">Hello hello 실제 쿼리 계획을 그래픽 표현 또는 해당 XML 콘텐츠를 요청 하 여 재생에 함수는 어떤 카디널리티 추정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="da1b0-141">그림 1에 hello 계획-side-by-side를 살펴보면 130에서 120 tooparallel에서 직렬에서 전환 되는 열 저장소 삽입 실행 해당 hello를 명확 하 게 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="da1b0-142">실제로 병렬은 이제 반복기 실행 hello hello 팩트를 보여 주기 위해 두 개의 병렬 화살표를 표시 하는 hello 130 계획에 hello 반복기 아이콘의 hello 변경을 note 또한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="da1b0-143">연결 된 toohello hello 데이터베이스에 있는 코어 수가 hello 병렬 실행 성능이 향상; INSERT 작업 toocomplete 큰 경우 100 배 이상 빠릅니다 tooa를 상황에 따라!</span><span class="sxs-lookup"><span data-stu-id="da1b0-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="da1b0-144">*그림 1: 호환성 수준이 130 직렬 tooparallel에서 변경 작업을 삽입 합니다.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![그림 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="da1b0-146">직렬 배치 모드</span><span class="sxs-lookup"><span data-stu-id="da1b0-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="da1b0-147">마찬가지로 데이터의 행을 처리할 때 toocompatibility 수준 130 이동 일괄 처리 모드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="da1b0-148">첫째, 배치 모드 작업은 열 저장소 인덱스가 있어야만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="da1b0-149">둘째, 일괄 처리 일반적으로 ~ 900 행을 나타내는 멀티 코어 CPU, 메모리 처리량에 대 한 액세스에 최적화 된 코드 논리를 사용 하 고 직접 활용 하 여 hello hello 가능 하면 Columnstore의 압축 된 데이터.</span><span class="sxs-lookup"><span data-stu-id="da1b0-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="da1b0-150">이러한 상황에서는 SQL Server 2016 처리할 수 ~ 900 행 한 번에 hello 시 1 개 행 대신 있으며이 인해 hello hello 작업의 전체적인 오버 헤드 비용 이제 공유 hello 전체 일괄 처리에 의해, hello 전체 행으로 비용을 감소.</span><span class="sxs-lookup"><span data-stu-id="da1b0-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="da1b0-151">이 공유 작업과 기본적으로 hello 열 저장소 압축 결합 양을 hello 대기 작업과 관련된 된 선택 일괄 처리 모드를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="da1b0-152">모드에서 일괄 처리와 hello 열 저장소에 대 한 자세한 정보를 찾을 수 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="da1b0-153">아래 표시로 hello 쿼리 계획--함께 숫자 2 관찰 하 여 볼 수 있습니다 hello 처리 모드가 hello 호환성 수준으로 변경 하 고이 인해 두 호환성 수준에서 hello 쿼리 실행을 완전히 때 수 있다는 것을 알합니다 행 비교 모드 (86%) toohello 일괄 처리 모드 (14%)이 2 일괄 처리 된 대부분의 hello 처리 시간이 소비 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="da1b0-154">Hello 데이터 집합을 증가 hello 혜택 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="da1b0-155">*그림 2: 호환성 수준 130 사용 하 여 직렬 toobatch 모드에서 변경 작업을 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![그림 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="da1b0-157">배치 모드에서 정렬 실행</span><span class="sxs-lookup"><span data-stu-id="da1b0-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="da1b0-158">행 모드 (호환성 수준 120) toobatch 모드 (호환성 수준 130)에서 위의 비슷한 toohello 수 있지만, 적용 된 tooa 정렬 작업 hello 전환을 속도가 빨라집니다 hello hello hello에 대 한 정렬 작업의 몇 가지 이유로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="da1b0-159">표시-side-by-side 그림 3에, hello 정렬 작업이 행 모드에서의 비용, hello 일괄 처리 모드에만 hello 비용 (각각 81% 및 hello 정렬 자체에 56%)의 %19 나타냅니다 hello 81%를 나타내는 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="da1b0-160">*그림 3: 정렬 작업에서 행 toobatch 모드 호환성 수준 130으로 변경합니다.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![그림 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="da1b0-162">물론, 이러한 샘플만 포함 수만 개의 행을 되 고이 nothing 요즘 대부분의 SQL 서버에서 사용할 수 있는 hello 데이터를 볼 때.</span><span class="sxs-lookup"><span data-stu-id="da1b0-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="da1b0-163">방금 대신 수백만 행에 대해 이러한 프로젝트를 마우스 용 hello 특성 워크 로드의 보류 중인 매일 실행의 몇 분 정도에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="da1b0-164">카디널리티 예측(CE) 향상</span><span class="sxs-lookup"><span data-stu-id="da1b0-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="da1b0-165">SQL Server 2014에 도입 된, 모든 데이터베이스 호환성 수준 120 이상에서 실행 하면 새 카디널리티 추정 기능 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="da1b0-166">기본적으로, 카디널리티 추정 hello 논리가 사용 toodetermine SQL server는 예상된 비용을 기반으로 쿼리를 실행 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="da1b0-167">hello 추정 해당 쿼리에 관련 된 개체와 관련 된 통계의 입력을 사용 하 여 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="da1b0-168">실제로, 상위 수준에서 카디널리티 추정 기능은 hello 값, 고유 값 수의 분포 hello에 대 한 정보와 함께 행 수가 예상치와 중복 된 개수에 포함 된 hello 테이블과 hello 쿼리에서 참조 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="da1b0-169">이러한 예상치를 잘못 된, 나타났다 toounnecessary 디스크 I/O tooinsufficient 메모리 부여 (예:: TempDB spill) 인해 발생할 수 있습니다 또는 tooa 선택 직렬 계획의 실행을 통해 병렬 계획 실행, tooname 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="da1b0-170">결론을 잘못 된 예측 tooan 편이성 hello 쿼리 실행의 전반적인 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="da1b0-171">Hello에 다른 쪽 보다 잘 예측 더 정확 하 게 예측, 잠재 고객 toobetter 쿼리 실행!</span><span class="sxs-lookup"><span data-stu-id="da1b0-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="da1b0-172">앞서 언급 했 듯이 쿼리 최적화와 예상치는 복잡 한 것 이지만 쿼리 계획 및 카디널리티 평가기에 대 한 자세한 toolearn 하려는 경우 toohello 문서에서 참조할 수 있습니다 [hello SQL Server 2014로 Your 쿼리 계획을 최적화 카디널리티 평가기](https://msdn.microsoft.com/library/dn673537.aspx) 심층 분석에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="da1b0-173">현재 어떤 카디널리티 예측을 사용하고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="da1b0-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="da1b0-174">쿼리를 사용 중인 카디널리티 예측 해 보겠습니다 방금 hello 쿼리 사용 샘플 아래 toodetermine 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="da1b0-175">호환성 수준 110에서 암시 hello 이전 카디널리티 예측 함수의 hello 사용이 첫 번째 예제를 실행 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="da1b0-176">실행이 완료 되 면 hello XML 링크를 클릭 하 고 아래와 같이 hello 첫 번째 반복기의 hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="da1b0-177">Hello 메모 속성 이름인 호출 CardinalityEstimationModelVersion 현재 70에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="da1b0-178">데이터베이스 호환성 수준이 hello toohello SQL Server 7.0 버전 (설정 110으로 위의 hello TSQL 문을에 표시)을 설정 하지만 hello 값 70 단순히 hello 레거시 카디널리티 추정 기능 나타내는 SQL부터 사용할 수 있음 의미 하지 않습니다. 서버 7.0, SQL Server 2014 (와 함께 제공 되는 호환성 수준 120) 될 때까지 어느 주요 수정 버전이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="da1b0-179">*그림 4: hello CardinalityEstimationModelVersion too70은 설정 하는 호환성 수준이 110 이하로 사용 하는 경우.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![그림 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="da1b0-181">Hello 호환성 수준 too130 변경 하 고 LEGACY_CARDINALITY_ESTIMATION 설정으로 tooON hello를 사용 하 여 hello 새 카디널리티 예측 함수의 hello 사용을 비활성화할 수 또는 [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="da1b0-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="da1b0-182">이 수 정확 하 게 hello 카디널리티 추정 함수의 관점에서 110을 사용 하 여 호환성 수준을 처리 하는 hello 최신 쿼리를 사용 하는 동안과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="da1b0-183">이렇게 hello 새 쿼리 처리 hello 최신 호환성 수준 (즉, 일괄 처리 모드)가 기능을 활용 하지만 필요한 경우 이전 카디널리티 추정 기능 hello 하면서 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="da1b0-184">Toohello 호환성 수준 120 또는 130을 이동 하기만 하면 hello 새 카디널리티 예측 기능을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="da1b0-185">이 경우 CardinalityEstimationModelVersion hello 기본 설정 됩니다 적절 하 게 too120 또는 아래 보이지 130입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="da1b0-186">*그림 5: hello CardinalityEstimationModelVersion too130은 설정 하는 호환성 수준이 130 사용 하는 경우.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![그림 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="da1b0-188">Witnessing hello 카디널리티 추정 차이점</span><span class="sxs-lookup"><span data-stu-id="da1b0-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="da1b0-189">이제 확인해 보겠습니다 약간 더 복잡 일부 조건자를 사용 하는 WHERE 절로 INNER JOIN 관련 된 쿼리를 살펴 보겠습니다 hello 행 개수 예측이 hello 이전 카디널리티 추정 함수에서 먼저.</span><span class="sxs-lookup"><span data-stu-id="da1b0-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="da1b0-190">이 쿼리를 효과적으로 실행 hello 이전 카디널리티 예측 기능을 사용 하 여 hello 행 예상 194,284 행을 주장 하는 동안 200,704 행 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="da1b0-191">물론, 전에 언급 한 것 처럼 이러한 행 개수 결과 다릅니다 얼마나 자주 실행 hello 이전 샘플 각 실행에서 반복 해 서 다시 hello 예제 테이블을 채우는.</span><span class="sxs-lookup"><span data-stu-id="da1b0-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="da1b0-192">물론, 쿼리에서 hello 조건자 hello 실제 추정 hello 테이블 모양, 데이터 콘텐츠 및 어떻게이 데이터 실제로 서로 상호 연결 하는 것 외에 영향이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="da1b0-193">*그림 6: hello 행 개수 예측이 꺼져 194,284 또는 6000 행에서 예상 되는 hello 200,704 행 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![그림 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="da1b0-195">Hello에 동일한 방식으로 보겠습니다 이제 hello 같은 hello 새 카디널리티 추정 기능으로 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="da1b0-196">Hello 아래를 살펴보면 이제 보면 해당 hello 행 예상 값 이며 202,877, 또는 훨씬 더 가깝기 때문 이전 카디널리티 추정 hello 보다 더 높은 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="da1b0-197">*그림 7: hello 행 개수 예측이 이제 202,877 194,284 대신.*</span><span class="sxs-lookup"><span data-stu-id="da1b0-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![그림 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="da1b0-199">실제로 hello 결과 집합은 200,704 행 (하지만 얼마나 자주 않은 쿼리를 실행할 hello hello의 이전 예제를 따라 해당 내용을 모두 않지만 무엇 보다도 TSQL hello hello rand () 문을 사용 하 여, 때문에 반환 하는 hello 실제 값 달라질 수 있습니다 하나 실행된 toohello에서 옆).</span><span class="sxs-lookup"><span data-stu-id="da1b0-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="da1b0-200">따라서이 특정 예제의 hello 새 카디널리티 추정 않으면 202,877 더 가깝습니다 too200, 704, 194,284 보다 이므로 hello 행 수를 예측에 더 효율적으로!</span><span class="sxs-lookup"><span data-stu-id="da1b0-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="da1b0-201">Last, WHERE 절 조건자 tooequality hello를 변경 하는 경우 (보다는 ">" 예를 들어), hello 이전 및 새 카디널리티 함수 간의 hello 예측을 훨씬 더 서로 다르게 만들 수이 하, 일치 항목의 수에 따라 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="da1b0-202">물론, 이 경우, 실제 카운트에서 최대 6000개의 행이 해제되면 상황에 따라서 많은 데이터를 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="da1b0-203">이제이 toomillions 행의 여러 테이블 및 더 복잡 한 쿼리를 통해 행과 열 및 hello 예상 시간에 수백만 개의 행을 날 수 있고 따라서 실행 계획 또는 메모리가 부족 하 여 요청 권한을 부여 앞에 오는 잘못 선택 하는 데 접속 hello의 위험을 hello tooTempDB spill 및 하므로 더 많은 I/O는 훨씬 더 높은입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="da1b0-204">Hello 기회를 설정한 경우이 비교 가장 일반적인 쿼리 및 데이터 집합, 연습 및 얼마나 hello 이전 및 새 예측 중 일부에 영향을 일부만 될 수 오프 hello 현실에서 수를 늘리거나 일부는 다른 하는 것 동안 자신에 대 한 참조 자세히 toohello 실제 행 hello 결과 집합에 실제로 반환 된를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="da1b0-205">해당 내용을 모두 쿼리, hello Azure SQL 데이터베이스 특징, hello 특성 및 데이터 집합 및 hello 통계에 대 한 사용 가능한의 hello 크기의 hello 셰이프의 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="da1b0-206">Azure SQL 데이터베이스 인스턴스, hello 쿼리 최적화 프로그램은 toobuild 방금 만든 지식을 다시 사용 통계 hello 이전 쿼리는 구성 대신 처음부터 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="da1b0-207">따라서 hello 예측은 매우 컨텍스트 및 거의 특정 tooevery 서버 및 응용 프로그램 상황 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="da1b0-208">에 중요 한 측면 tookeep입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="da1b0-209">계정에 몇 가지 고려 사항 tootake</span><span class="sxs-lookup"><span data-stu-id="da1b0-209">Some considerations tootake into account</span></span>
<span data-ttu-id="da1b0-210">대부분의 작업은 프로덕션 환경에 대 한 호환성 수준을 hello를 채택 하기 전에 hello 호환성 수준 130에서에서 이익을 얻을, 3 옵션은 기본적으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="da1b0-211">Toocompatibility 수준 130을 이동한 항목 성능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="da1b0-212">일부 재발을 확인 하는 경우 하는 것 설정 hello 호환성 수준 뒤로 tooits 원래 수준 또는 130을 유지 하 고만 hello 카디널리티 추정 백 toohello 레거시 모드를 역방향 (위에서 설명한 대로이 단독 수 hello 문제 해결).</span><span class="sxs-lookup"><span data-stu-id="da1b0-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="da1b0-213">미세 조정을 진행 중인 tooproduction 하기 전에 hello 성능 평가 비슷한 프로덕션 부하에서 기존 응용 프로그램을 철저히 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="da1b0-214">문제가 발생 하면 위와 동일한 항상 toohello 원래 호환성 수준으로 다시 이동 하거나 hello 카디널리티 추정 백 toohello 레거시 모드를 반대로 생각해 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="da1b0-215">마지막 옵션 및 hello 가장 최근의 방식으로 tooaddress tooleverage hello 쿼리 저장소는 질문 이러한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="da1b0-216">이것이 현재 권장되는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-216">That’s today’s recommended option!</span></span> <span data-ttu-id="da1b0-217">tooassist hello 분석 쿼리의 호환성 수준 120 또는 아래 130, 대 수 없습니다 좋습니다 toouse 쿼리 저장소 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="da1b0-218">쿼리 저장소는 hello Azure SQL 데이터베이스 v 12의 최신 버전으로 사용할 수 있으며 기능은 toohelp 쿼리 성능 문제 해결을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="da1b0-219">Hello 쿼리 저장소를 수집 하 고 모든 쿼리에 대 한 기록 세부 정보를 나타내는 데이터베이스에 대 한 항공 데이터 레코더 라고 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="da1b0-220">이 크게 hello 시간 toodiagnose를 줄임으로써 성능 법정 단순화 및 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="da1b0-221">자세한 내용은 [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)(쿼리 저장소: 데이터베이스에 대한 블랙박스)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da1b0-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="da1b0-222">Hello 이미 호환성 수준 120 이하로 실행 되는 데이터베이스 집합이 있고 toomove 계획 하는 경우 상위 수준에서 그 중 일부를 too130, 워크 로드 될 새 데이터베이스를 자동으로 프로 비전 곧 될 기본 too130 설정한, 하십시오 다음과 같이 hello:</span><span class="sxs-lookup"><span data-stu-id="da1b0-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="da1b0-223">프로덕션 환경에서 새로운 호환성 수준 toohello를 변경 하기 전에 쿼리 저장소를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="da1b0-224">너무 참조할 수[hello 데이터베이스 호환성 모드와 사용 하 여 hello 쿼리 저장소를 변경](https://msdn.microsoft.com/library/bb895281.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="da1b0-225">다음으로 대표 데이터 및 쿼리 프로덕션 환경과 유사한 환경 및 발생 하는 hello 성능을 비교 하 고 쿼리 저장소에서 보고를 사용 하 여 모든 중요 한 워크 로드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="da1b0-226">일부 회귀가 발생 하는 경우를 식별할 수 있습니다 쿼리 저장소 hello로 회귀 된 쿼리를 hello 및 hello 계획 쿼리 저장소에서 옵션을 사용 하 여 (고정 계획 aka).</span><span class="sxs-lookup"><span data-stu-id="da1b0-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="da1b0-227">이 경우 명확 hello 호환성 수준 130 그대로 적용 했으며 hello 쿼리 저장소에서 제시한 대로 hello 이전 쿼리 계획을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="da1b0-228">만으로도 마지막 수단으로 hello 호환성 수준 130에서 중요 한 toochanges 않는 tooleverage 새로운 기능 및 Azure SQL 데이터베이스 (SQL Server 2016을 실행 중임)의 기능을 사용할 경우 고려할 수 강제 다시 hello 호환성 수준 ALTER DATABASE 문을 사용 하 여 워크 로드에 맞는 toohello 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="da1b0-229">먼저, 수 있지만 130을 사용 하지 않는 기본적으로 남아 있는 경우 이전 SQL Server 버전의 hello 기능 수준에서 때문에 옵션 고정 hello 쿼리 저장소 계획은 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="da1b0-230">여러 데이터베이스를 확장 하는 다중 테 넌 트 응용 프로그램의 경우 필요한 tooupdate hello; 모든 데이터베이스에서 사용자 데이터베이스 tooensure 일관 된 호환성 수준이의 논리를 프로 비전 수 있습니다. 이전 구문과 새로 프로 비전 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="da1b0-231">응용 프로그램 워크 로드 성능에는 일부 데이터베이스는 서로 다른 호환성 수준에서 실행 되는 중요 한 toohello 팩트 될 수 있으며 따라서 모든 데이터베이스에서 호환성 수준 일관성 필요할 수 tooprovide hello 동일한 순서 tooyour 고객 hello 보드에서 모두 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="da1b0-232">Note는 필수적, 실제로 hello 호환성 수준에 따라 응용 프로그램의 적용 하는 방법에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="da1b0-233">마지막으로, hello 카디널리티 추정에 대 한 프로덕션 환경에서 계속 진행 하기 전에 hello 호환성 수준 변경이 마찬가지로 응용 프로그램에서 활용 하는 경우 tootest hello 새 조건 toodetermine에서 프로덕션 작업에 권장 hello 카디널리티 추정 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="da1b0-234">결론</span><span class="sxs-lookup"><span data-stu-id="da1b0-234">Conclusion</span></span>
<span data-ttu-id="da1b0-235">Azure SQL 데이터베이스를 사용 하 여 모든 SQL Server 2016 향상 기능에서 toobenefit 명확 하 게 향상 시킬 수 있습니다 쿼리 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="da1b0-236">얘기한 그대로 입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-236">Just as-is!</span></span> <span data-ttu-id="da1b0-237">물론, 새 기능과 마찬가지로 적절 한 평가 해야 toodetermine hello 조건은 정확 하 게 데이터베이스 작업 중인 hello 가장 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="da1b0-238">경험 대부분 작업 부하 예상된 tooat 이상 투명 하 게 실행 호환성 수준 130, 함수 및 새 카디널리티 예측을 처리 하는 새 쿼리를 활용 하면서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="da1b0-239">적절 한 기한을 진행 하 고 다시 말하면 실제적으로, 몇 가지 예외는 항상 성실은 중요 한 평가 toodetermine 얼마나 이러한 향상 기능에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="da1b0-240">이며이 작업을 수행 하에 큰 도움이 hello 쿼리 저장소를 다시 지정할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="da1b0-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="da1b0-241">SQL Azure 진화 함에 따라 hello에 호환성 수준이 140 이후 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="da1b0-242">적절한 시기가 되면, 현재 호환성 수준 130을 통해 가능해 지는 것들을 여기에서 간략하게 설명했듯이, 미래의 호환성 수준 140을 통해 가능해지는 것들에 관해 간략하게 설명할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="da1b0-243">지금은 콘텐트가, 2016 년 6 월부터 Azure SQL 데이터베이스에서에서 변경 됩니다. hello 기본 호환성 수준 120 too130 새로 만든된 데이터베이스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="da1b0-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="da1b0-244">잊지 마세요!</span><span class="sxs-lookup"><span data-stu-id="da1b0-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="da1b0-245">참조</span><span class="sxs-lookup"><span data-stu-id="da1b0-245">References</span></span>
* [<span data-ttu-id="da1b0-246">데이터베이스 엔진의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="da1b0-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="da1b0-247">블로그: 쿼리 저장소: 데이터베이스에 대한 블랙박스, 작성자: Borko Novakovic, 2016년 6월 8일</span><span class="sxs-lookup"><span data-stu-id="da1b0-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="da1b0-248">ALTER DATABASE 호환성 수준(Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="da1b0-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="da1b0-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="da1b0-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="da1b0-250">Azure SQL 데이터베이스 V12에 대한 호환성 수준 130</span><span class="sxs-lookup"><span data-stu-id="da1b0-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="da1b0-251">쿼리 계획을 여를 최적화 하 여 hello SQL Server 2014 카디널리티 평가기</span><span class="sxs-lookup"><span data-stu-id="da1b0-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="da1b0-252">Columnstore 인덱스 가이드</span><span class="sxs-lookup"><span data-stu-id="da1b0-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="da1b0-253">블로그: Azure SQL 데이터베이스의 호환성 수준 130을 통해 개선된 쿼리 성능, 작성자: Alain Lissoir, 2016년 5월 6일</span><span class="sxs-lookup"><span data-stu-id="da1b0-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
