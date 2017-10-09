---
title: "SQL 데이터 웨어하우스에 대 한 트랜잭션을 aaaOptimizing | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 효율적인 트랜잭션 업데이트를 작성하는 모범 사례 가이드"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="cf50a-103">SQL 데이터 웨어하우스에 대해 트랜잭션 최적화</span><span class="sxs-lookup"><span data-stu-id="cf50a-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="cf50a-104">이 문서에서는 toooptimize 긴 롤백에 대 한 위험을 최소화 하면서 트랜잭션 코드의 성능을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="cf50a-105">트랜잭션 및 로깅</span><span class="sxs-lookup"><span data-stu-id="cf50a-105">Transactions and logging</span></span>
<span data-ttu-id="cf50a-106">트랜잭션은 관계형 데이터베이스 엔진의 중요한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="cf50a-107">SQL 데이터 웨어하우스는 데이터를 수정하는 동안 트랜잭션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="cf50a-108">이러한 트랜잭션은 명시적일 수도 있고 암시적일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="cf50a-109">단일 `INSERT`, `UPDATE` 및 `DELETE` 문은 모두 암시적 트랜잭션의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="cf50a-110">명시적 트랜잭션을 사용 하는 개발자가 명시적으로 작성 된 `BEGIN TRAN`, `COMMIT TRAN` 또는 `ROLLBACK TRAN` 되며 여러 수정 문을 toobe 단일 원자 단위에 연결 해야 하는 경우 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="cf50a-111">Azure SQL 데이터 웨어하우스 변경 toohello 데이터베이스를 트랜잭션 로그를 사용 하 여 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="cf50a-112">각 분산에는 고유한 트랜잭션 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="cf50a-113">트랜잭션 로그 쓰기는 자동입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="cf50a-114">구성이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-114">There is no configuration required.</span></span> <span data-ttu-id="cf50a-115">그러나이 프로세스는 hello 쓰기를 보장 하는 동안 hello 시스템에는 오버를 헤드가지 않습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="cf50a-116">트랜잭션 측면에서 효율적인 코드를 작성하면 이 영향을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="cf50a-117">트랜잭션 측면에서 효율적인 코드는 크게 두 범주로 나눌 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="cf50a-118">가능한 최소한의 로깅 구문 활용</span><span class="sxs-lookup"><span data-stu-id="cf50a-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="cf50a-119">장기 실행 트랜잭션 범위가 지정 된 일괄 처리 tooavoid 단 수를 사용 하 여 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="cf50a-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="cf50a-120">지정 된 파티션에서 큰 수정 tooa에 대 한 패턴을 전환 파티션 채택</span><span class="sxs-lookup"><span data-stu-id="cf50a-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="cf50a-121">최소 로깅 및 전체 로깅 비교</span><span class="sxs-lookup"><span data-stu-id="cf50a-121">Minimal vs. full logging</span></span>
<span data-ttu-id="cf50a-122">모든 행 변경의 트랜잭션 로그 tookeep 트랙 hello를 사용 하는 완전히 로그 작업과 달리 익스텐트 할당 및 메타 데이터 변경 내용만 동기화 최소 로그 작업의 추적을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="cf50a-123">따라서 최소 로깅을 포함는 오류 또는 명시적으로 요청할의 hello 이벤트에 필요한 toorollback hello 트랜잭션이 있는 hello 정보만 로깅 (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="cf50a-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="cf50a-124">훨씬 덜 hello 트랜잭션 로그에 정보를 추적, 최소 로그 작업에서 비슷한 크기 완전히 기록 된 작업 보다 더 잘 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="cf50a-125">또한 더 적은 쓰기 hello 트랜잭션 로그를 이동, 때문에 훨씬 적은 양의 로그 데이터 생성 되 고 하므로 더 많은 I/O 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="cf50a-126">만 hello 트랜잭션 보안 제한 toofully 기록 작업을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="cf50a-127">최소 로깅 작업은 명시적 트랜잭션에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="cf50a-128">할당 구조의 모든 변경 내용을 추적 하는 것이 가능한 tooroll 백 최소 로그 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="cf50a-129">Hello 변경 되어 "최소" toounderstand 기록 반드시 기록 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="cf50a-130">최소 로깅 작업</span><span class="sxs-lookup"><span data-stu-id="cf50a-130">Minimally logged operations</span></span>
<span data-ttu-id="cf50a-131">hello 다음 작업은 최소한으로 기록 되 고 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="cf50a-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="cf50a-132">[CTAS][CTAS](CREATE TABLE AS SELECT)</span><span class="sxs-lookup"><span data-stu-id="cf50a-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="cf50a-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="cf50a-133">INSERT..SELECT</span></span>
* <span data-ttu-id="cf50a-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="cf50a-134">CREATE INDEX</span></span>
* <span data-ttu-id="cf50a-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="cf50a-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="cf50a-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="cf50a-136">DROP INDEX</span></span>
* <span data-ttu-id="cf50a-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="cf50a-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="cf50a-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="cf50a-138">DROP TABLE</span></span>
* <span data-ttu-id="cf50a-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="cf50a-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="cf50a-140">내부 데이터 이동 작업 (예: `BROADCAST` 및 `SHUFFLE`) hello 트랜잭션 보안 제한의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="cf50a-141">대량 로드를 사용하여 최소 로깅</span><span class="sxs-lookup"><span data-stu-id="cf50a-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="cf50a-142">`CTAS` 및 `INSERT...SELECT`는 대량 로드 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="cf50a-143">그러나 hello 대상 테이블 정의 의해 영향을 받는 둘 다 고 hello 부하 시나리오에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="cf50a-144">아래는 대량 작업이 전부 로깅되는지 아니면 최소한으로 로깅되는지를 설명하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="cf50a-145">기본 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-145">Primary Index</span></span> | <span data-ttu-id="cf50a-146">부하 시나리오</span><span class="sxs-lookup"><span data-stu-id="cf50a-146">Load Scenario</span></span> | <span data-ttu-id="cf50a-147">로깅 모드</span><span class="sxs-lookup"><span data-stu-id="cf50a-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf50a-148">힙</span><span class="sxs-lookup"><span data-stu-id="cf50a-148">Heap</span></span> |<span data-ttu-id="cf50a-149">모두</span><span class="sxs-lookup"><span data-stu-id="cf50a-149">Any</span></span> |<span data-ttu-id="cf50a-150">**최소**</span><span class="sxs-lookup"><span data-stu-id="cf50a-150">**Minimal**</span></span> |
| <span data-ttu-id="cf50a-151">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-151">Clustered Index</span></span> |<span data-ttu-id="cf50a-152">빈 대상 테이블</span><span class="sxs-lookup"><span data-stu-id="cf50a-152">Empty target table</span></span> |<span data-ttu-id="cf50a-153">**최소**</span><span class="sxs-lookup"><span data-stu-id="cf50a-153">**Minimal**</span></span> |
| <span data-ttu-id="cf50a-154">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-154">Clustered Index</span></span> |<span data-ttu-id="cf50a-155">로드된 행이 대상의 기존 페이지와 겹치지 않음</span><span class="sxs-lookup"><span data-stu-id="cf50a-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="cf50a-156">**최소**</span><span class="sxs-lookup"><span data-stu-id="cf50a-156">**Minimal**</span></span> |
| <span data-ttu-id="cf50a-157">클러스터형 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-157">Clustered Index</span></span> |<span data-ttu-id="cf50a-158">로드된 행이 대상의 기존 페이지와 겹침</span><span class="sxs-lookup"><span data-stu-id="cf50a-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="cf50a-159">전체</span><span class="sxs-lookup"><span data-stu-id="cf50a-159">Full</span></span> |
| <span data-ttu-id="cf50a-160">클러스터형 Clustered 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="cf50a-161">배치 크기는 파티션 정렬 분산당 102,400 이상</span><span class="sxs-lookup"><span data-stu-id="cf50a-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="cf50a-162">**최소**</span><span class="sxs-lookup"><span data-stu-id="cf50a-162">**Minimal**</span></span> |
| <span data-ttu-id="cf50a-163">클러스터형 Clustered 인덱스</span><span class="sxs-lookup"><span data-stu-id="cf50a-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="cf50a-164">배치 크기는 파티션 정렬 분산당 102,400 미만</span><span class="sxs-lookup"><span data-stu-id="cf50a-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="cf50a-165">전체</span><span class="sxs-lookup"><span data-stu-id="cf50a-165">Full</span></span> |

<span data-ttu-id="cf50a-166">이므로 로그 작업에 한 쓰기가 tooupdate 보조 또는 비클러스터형 인덱스는 항상 완벽 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf50a-167">SQL 데이터 웨어하우스에는 60개의 분산이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="cf50a-168">Tooa 클러스터형 Columnstore 인덱스를 작성할 때 따라서 기록에서는 단일 파티션의 시작 되 고, 일괄 처리 해야 합니다 toocontain 6,144,000 행 또는 더 큰 toobe 최소 및 모든 행은 고르게 분포를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="cf50a-169">Hello 테이블이 분할 되 고 삽입 되는 hello 행 파티션 경계에 걸쳐, 다음 할 경우 6,144,000 행도 데이터 분포를 가정 하면 파티션의 경계 수입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="cf50a-170">각 배포의 각 파티션은 hello 삽입 toobe hello 배포에 최소 로깅에 대 한 hello 수가 102, 400 행 임계값 독립적으로 초과 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="cf50a-171">클러스터형 인덱스가 포함된 비어 있지 않은 테이블로 데이터를 로드하면 전체 로깅 행과 최소 로깅 행이 모두 포함되는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="cf50a-172">클러스터형 인덱스는 균형 잡힌 페이지 트리(b-트리)입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="cf50a-173">Hello 페이지에서 다른 트랜잭션이 행을 포함 하는 tooalready 쓰고, 경우 다음이 쓰기 완벽 하 게 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="cf50a-174">그러나 hello 페이지가 비어 있는 경우 다음 hello 쓰기 toothat 페이지 최소한으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="cf50a-175">삭제 최적화</span><span class="sxs-lookup"><span data-stu-id="cf50a-175">Optimizing deletes</span></span>
<span data-ttu-id="cf50a-176">`DELETE` 는 전체 로깅 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="cf50a-177">데이터 파티션 또는 테이블에 많은 양의 toodelete 해야 할 경우 대개는 것이 너무`SELECT` tookeep 최소 로그 작업으로 실행 될 수 있는 원하는 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="cf50a-178">tooaccomplish이 포함 된 새 테이블을 만들 [CTAS][CTAS]합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="cf50a-179">생성을 사용 하 여 [이름 바꾸기] [ RENAME] tooswap 여 이전 테이블을 새로 만든 hello 테이블과 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="cf50a-180">업데이트 최적화</span><span class="sxs-lookup"><span data-stu-id="cf50a-180">Optimizing updates</span></span>
<span data-ttu-id="cf50a-181">`UPDATE` 는 전체 로깅 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="cf50a-182">테이블의 행 수가 많은 tooupdate 하거나 파티션에 종종 것이 훨씬 더 효율적 toouse와 같은 작업을 최소 로깅으로 수행 [CTAS] [ CTAS] toodo 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="cf50a-183">Hello 전체 테이블 업데이트를 다음 예제에서는 변환 된 tooa 되었습니다 `CTAS` 최소 로깅은 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="cf50a-184">이 경우 소급 방식으로 discount amount toohello sales hello 테이블에 추가 하 고:</span><span class="sxs-lookup"><span data-stu-id="cf50a-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="cf50a-185">대규모 테이블을 다시 만들면 SQL 데이터 웨어하우스 워크로드 관리 기능의 이점을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="cf50a-186">자세한 내용은 hello에 toohello 작업 관리 섹션을 참조 하십시오에 대 한 [동시성] [ concurrency] 문서.</span><span class="sxs-lookup"><span data-stu-id="cf50a-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="cf50a-187">파티션 전환을 사용하여 최적화</span><span class="sxs-lookup"><span data-stu-id="cf50a-187">Optimizing with partition switching</span></span>
<span data-ttu-id="cf50a-188">[테이블 파티션][table partition] 내부에서 대규모 수정 작업에 직면하는 경우 파티션 전환 패턴을 사용하는 것이 훨씬 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="cf50a-189">경우 hello를 중요 한 데이터를 수정 하 고 hello 파티션을 단순히 반복 하는 여러 개의 파티션이 달성 범위 hello 동일한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="cf50a-190">hello 단계 tooperform 파티션 전환은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="cf50a-191">빈 외부 파티션 만들기</span><span class="sxs-lookup"><span data-stu-id="cf50a-191">Create an empty out partition</span></span>
2. <span data-ttu-id="cf50a-192">CTAS에는으로 hello '업데이트'를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="cf50a-193">테이블을 기존 데이터 toohello hello 외부 전환</span><span class="sxs-lookup"><span data-stu-id="cf50a-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="cf50a-194">Hello 새 데이터의 전환</span><span class="sxs-lookup"><span data-stu-id="cf50a-194">Switch in hello new data</span></span>
5. <span data-ttu-id="cf50a-195">Hello 데이터 정리</span><span class="sxs-lookup"><span data-stu-id="cf50a-195">Clean up hello data</span></span>

<span data-ttu-id="cf50a-196">그러나 toohelp hello 파티션을 tooswitch 먼저 필요한 toobuild 하나 hello 같은 도우미 프로시저 아래를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="cf50a-197">이 프로시저 코드 다시 사용을 최대화 하 고 hello 파티션 보다 간단한 예제를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="cf50a-198">아래의 hello 코드 루틴 전환 전체 파티션 tooachieve 위에서 언급 한 hello 5 단계를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="cf50a-199">작은 배치를 사용하여 로깅 최소화</span><span class="sxs-lookup"><span data-stu-id="cf50a-199">Minimize logging with small batches</span></span>
<span data-ttu-id="cf50a-200">큰 데이터 수정 작업에 대 한 작업의 의미 toodivide hello 작업 tooscope hello 단위로 청크 또는 일괄 처리 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="cf50a-201">아래는 작업 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-201">A working example is provided below.</span></span> <span data-ttu-id="cf50a-202">hello 일괄 처리 크기 tooa trivial 숫자 toohighlight hello 기술을 설정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="cf50a-203">실제로 hello 일괄 처리 크기는 훨씬 큰 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-203">In reality hello batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="cf50a-204">일시 중지 및 크기 조정 지침</span><span class="sxs-lookup"><span data-stu-id="cf50a-204">Pause and scaling guidance</span></span>
<span data-ttu-id="cf50a-205">Azure SQL 데이터 웨어하우스를 사용하여 필요에 따라 데이터 웨어하우스를 일시 중지하고, 다시 시작하고, 규모를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="cf50a-206">일시 중지 하거나 중요 한 toounderstand 모든 진행 중인 트랜잭션은 즉시 종료 되는 SQL 데이터 웨어하우스를 확장 합니다. 모든 열린 트랜잭션이 toobe 일으키는 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="cf50a-207">장기 실행 및 이전에 완료 되지 않은 데이터 수정 작업에 발급 하는 경우 toohello 일시 중지 또는 크기 조정 작업 후이 작업 toobe 실행 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="cf50a-208">이 toopause hello 시간에 영향을 줄 또는 Azure SQL 데이터 웨어하우스 데이터베이스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cf50a-209">`UPDATE` 및 `DELETE`는 전체 로깅 작업이므로 이러한 실행 취소/다시 실행 작업이 최소 로깅에 비해 훨씬 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="cf50a-210">최상의 시나리오 hello 비행 데이터 수정 트랜잭션이 완료 이전 toopausing 또는 크기 조정 SQL 데이터 웨어하우스 toolet입니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="cf50a-211">그러나 이 방법이 불가능할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-211">However, this may not always be practical.</span></span> <span data-ttu-id="cf50a-212">긴 rollback의 toomitigate hello 위험 hello 다음 옵션 중 하나를 고려해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="cf50a-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="cf50a-213">[CTAS][CTAS]를 사용하여 실행 시간이 긴 작업을 다시 작성</span><span class="sxs-lookup"><span data-stu-id="cf50a-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="cf50a-214">청크로; hello 작업 구분 hello 행의 하위 집합에 대 한 작동</span><span class="sxs-lookup"><span data-stu-id="cf50a-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf50a-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf50a-215">Next steps</span></span>
<span data-ttu-id="cf50a-216">참조 [SQL 데이터 웨어하우스에 트랜잭션을] [ Transactions in SQL Data Warehouse] toolearn 격리 수준과 트랜잭션 제한에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf50a-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="cf50a-217">기타 모범 사례의 개요에 대해서는 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf50a-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

