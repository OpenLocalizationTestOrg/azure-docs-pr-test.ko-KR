---
title: "ID를 사용 하 여 서로게이트 키 aaaCreate | Microsoft Docs"
description: "테이블에 toouse IDENTITY toocreate 서로게이트 키 하는 방법에 대해 알아봅니다."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="52ea2-103">IDENTITY를 사용하여 서로게이트 키 만들기</span><span class="sxs-lookup"><span data-stu-id="52ea2-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="52ea2-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="52ea2-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="52ea2-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="52ea2-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="52ea2-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="52ea2-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="52ea2-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="52ea2-107">[Index][Index]</span></span>
> * <span data-ttu-id="52ea2-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="52ea2-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="52ea2-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="52ea2-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="52ea2-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="52ea2-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="52ea2-111">[ID][Identity]</span><span class="sxs-lookup"><span data-stu-id="52ea2-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="52ea2-112">많은 데이터 모델러는 데이터 웨어하우스 모델을 디자인할 때 해당 테이블에 toocreate 서로게이트 키 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="52ea2-113">사용할 수 있습니다 hello IDENTITY 속성 tooachieve이이 목표 간단 하 고 효과적으로 로드 성능에 영향을 주지 않고.</span><span class="sxs-lookup"><span data-stu-id="52ea2-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="52ea2-114">IDENTITY 시작</span><span class="sxs-lookup"><span data-stu-id="52ea2-114">Get started with IDENTITY</span></span>
<span data-ttu-id="52ea2-115">테이블은 유사한 toohello 문 다음 구문을 사용 하 여 hello 테이블을 처음 만들 때 hello IDENTITY 속성이 있는 것으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="52ea2-116">사용할 수 있습니다 `INSERT..SELECT` toopopulate hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="52ea2-117">동작</span><span class="sxs-lookup"><span data-stu-id="52ea2-117">Behavior</span></span>
<span data-ttu-id="52ea2-118">hello IDENTITY 속성으로 설계 된 tooscale 로드 성능에 영향을 주지 않고 hello 데이터 웨어하우스의 모든 hello 분포 값은입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="52ea2-119">따라서 ID의 hello 구현 이러한 목표를 달성과 관련 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="52ea2-120">이 섹션에서는 hello 갖는 요약 hello 구현 toohelp의 올바르게 이해 하 보다 완전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="52ea2-121">값 할당</span><span class="sxs-lookup"><span data-stu-id="52ea2-121">Allocation of values</span></span>
<span data-ttu-id="52ea2-122">hello IDENTITY 속성에는 SQL Server 및 Azure SQL 데이터베이스의 hello 동작을 반영 하는 hello 순서는 hello 서로게이트 값에 할당 된, 가능성이 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="52ea2-123">그러나 Azure SQL 데이터 웨어하우스의 보장 hello 없을 경우 더 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="52ea2-124">다음 예제는 hello이를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-124">hello following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="52ea2-125">앞 예제는 hello에서 두 개의 행 배포 1에에서 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="52ea2-126">열에서 hello 서로게이트 값이 1에 대 한 hello 첫 번째 행은 `C1`, hello 두 번째 행에 61의 hello 서로게이트 값 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="52ea2-127">Hello IDENTITY 속성에 의해 생성 된 두이 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="52ea2-128">그러나 hello 값의 hello 할당 인접 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="52ea2-129">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="52ea2-130">불균형 데이터</span><span class="sxs-lookup"><span data-stu-id="52ea2-130">Skewed data</span></span> 
<span data-ttu-id="52ea2-131">hello 데이터 형식에 대 한 값의 hello 범위 hello 배포판을 균등 하 게 분산 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="52ea2-132">분산된 테이블이 일치 하지 않는 데이터에서 발생 하는 경우 사용할 수 있는 toohello datatype을 중간 소진 될 수 있습니다. 값의 범위를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="52ea2-133">예를 들어 모든 hello 데이터는 단일 분포에서 끝난 경우 효과적으로 hello 테이블에 한 hello hello 데이터 형식이 값 액세스 tooonly sixtieth 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="52ea2-134">이러한 이유로 hello IDENTITY 속성은 제한 된 너무`INT` 및 `BIGINT` 데이터 형식에 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="52ea2-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="52ea2-135">SELECT..INTO</span></span>
<span data-ttu-id="52ea2-136">기존 ID 열을 새 테이블로 선택 하면 hello 다음 조건 중 하나는 경우에 hello 새 열 hello IDENTITY 속성을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="52ea2-137">hello SELECT 문에 조인이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="52ea2-138">UNION을 사용하여 여러 SELECT 문이 조인됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="52ea2-139">hello ID 열에는 한 번 이상 hello 선택 목록에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="52ea2-140">hello ID 열이 식의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="52ea2-141">이러한 조건 중 하나라도 true 이면 hello 열 hello IDENTITY 속성을 상속 하는 대신 NULL이 아닌 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="52ea2-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="52ea2-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="52ea2-143">만들 테이블 AS 선택 (CTAS에는) 다음과 같은 SQL Server 동작 선택에 대 한 설명 하는 hello... 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="52ea2-144">그러나 Hello의 hello 열 정의에 IDENTITY 속성을 지정할 수 없습니다 `CREATE TABLE` hello 문의 일부로 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="52ea2-145">또한 hello에 hello IDENTITY 함수를 사용할 수 없습니다 `SELECT` hello CTAS에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="52ea2-146">테이블 toopopulate 해야 toouse `CREATE TABLE` toodefine hello 테이블 뒤 `INSERT..SELECT` toopopulate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="52ea2-147">IDENTITY 열에 값을 명시적으로 삽입</span><span class="sxs-lookup"><span data-stu-id="52ea2-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="52ea2-148">SQL Data Warehouse는 `SET IDENTITY_INSERT <your table> ON|OFF` 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="52ea2-149">Hello ID 열에 값이 구문 tooexplicitly 삽입을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="52ea2-150">많은 데이터 모델러 toouse 미리 정의 된 음수 값을 특정 해당 차원에 있는 행 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="52ea2-151">예-1 hello 또는 "알 수 없는 멤버" 행입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="52ea2-152">다음 스크립트 hello tooexplicitly SET IDENTITY_INSERT를 사용 하 여이 행을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="52ea2-153">IDENTITY가 있는 테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="52ea2-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="52ea2-154">hello IDENTITY 속성의 hello 존재 일부 영향 tooyour 데이터 로드 코드를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="52ea2-155">이 섹션에서는 IDENTITY를 사용하여 테이블로 데이터를 로드하는 몇 가지 기본 패턴을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="52ea2-156">PolyBase를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="52ea2-156">Load data with PolyBase</span></span>
<span data-ttu-id="52ea2-157">tooload 데이터를 테이블에 ID를 사용 하 여 서로게이트 키를 생성 하 고 hello 테이블 만들기 및 다음 INSERT를 사용 하 여... SELECT 또는 INSERT... 값 tooperform hello 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="52ea2-158">hello 다음 예제에서는 하이라이트 hello 기본 패턴:</span><span class="sxs-lookup"><span data-stu-id="52ea2-158">hello following example highlights hello basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="52ea2-159">가능한 toouse 없으면 `CREATE TABLE AS SELECT` 현재 ID 열이 있는 테이블에 데이터를 로드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="52ea2-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="52ea2-160">Hello 대량 복사 프로그램 (BCP) 도구를 사용 하 여 데이터 로드에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="52ea2-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="52ea2-161">[PolyBase로 로드하기][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="52ea2-162">[PolyBase 모범 사례][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="52ea2-163">BCP를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="52ea2-163">Load data with BCP</span></span>
<span data-ttu-id="52ea2-164">BCP는 명령줄 도구를 SQL 데이터 웨어하우스에 tooload 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="52ea2-165">해당 매개 변수 중 하나 (-E) ID 열이 있는 테이블에 데이터를 로드할 때 컨트롤 hello BCP의 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="52ea2-166">-E를 지정 하는 경우 ID를 가진 hello hello 열에 대 한 입력된 파일에 보관 hello 값이 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="52ea2-167">-E가 *하지* 지정 하면이 열의 hello 값은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="52ea2-168">Hello id 열을 지정 하지 않은 경우 hello 데이터가 정상적으로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="52ea2-169">hello 값 hello 속성의 toohello 증가 및 시드 정책에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="52ea2-170">BCP를 사용 하 여 데이터를 로드에 대 한 자세한 내용은 다음 문서는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="52ea2-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="52ea2-171">[BCP로 로드하기][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-171">[Load with BCP][]</span></span>
- <span data-ttu-id="52ea2-172">[MSDN의 BCP][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="52ea2-173">카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="52ea2-173">Catalog views</span></span>
<span data-ttu-id="52ea2-174">SQL 데이터 웨어하우스 지원 hello `sys.identity_columns` 카탈로그 뷰에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="52ea2-175">이 보기에 사용 되는 tooidentify hello IDENTITY 속성이 있는 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="52ea2-176">hello 데이터베이스 스키마를 더 잘 이해 toohelp,이 예제에서는 어떻게 toointegrate `sys.identity_columns` 다른 시스템 카탈로그 뷰와:</span><span class="sxs-lookup"><span data-stu-id="52ea2-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="52ea2-177">제한 사항</span><span class="sxs-lookup"><span data-stu-id="52ea2-177">Limitations</span></span>
<span data-ttu-id="52ea2-178">다음 시나리오는 hello에 hello IDENTITY 속성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="52ea2-179">Hello 열 데이터 형식이 인 하지 정수나 BIGINT</span><span class="sxs-lookup"><span data-stu-id="52ea2-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="52ea2-180">Hello 열이 hello 배포 키도</span><span class="sxs-lookup"><span data-stu-id="52ea2-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="52ea2-181">Hello 테이블은 외부 테이블</span><span class="sxs-lookup"><span data-stu-id="52ea2-181">Where hello table is an external table</span></span> 

<span data-ttu-id="52ea2-182">hello 관련된 함수를 다음 SQL 데이터 웨어하우스에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="52ea2-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="52ea2-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="52ea2-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="52ea2-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="52ea2-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="52ea2-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="52ea2-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="52ea2-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="52ea2-190">작업</span><span class="sxs-lookup"><span data-stu-id="52ea2-190">Tasks</span></span>

<span data-ttu-id="52ea2-191">이 섹션에는 몇 가지 샘플 코드에서는 ID 열을 사용 하 여 작업할 때 tooperform 일반적인 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="52ea2-192">열 C1는 작업을 수행 하는 모든 hello에 hello IDENTITY입니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="52ea2-193">테이블에 할당 된 hello 가장 높은 값을 찾을</span><span class="sxs-lookup"><span data-stu-id="52ea2-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="52ea2-194">사용 하 여 hello `MAX()` toodetermine hello 가장 높은 값 분산된 테이블에 할당 된 함수:</span><span class="sxs-lookup"><span data-stu-id="52ea2-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="52ea2-195">Hello IDENTITY 속성에 대 한 hello 초기값 및 증가값을 찾기</span><span class="sxs-lookup"><span data-stu-id="52ea2-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="52ea2-196">다음 쿼리에서 hello를 사용 하 여 테이블에 대 한 hello 카탈로그 뷰 toodiscover hello identity 초기값 및 증가값 구성 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="52ea2-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52ea2-197">Next steps</span></span>

* <span data-ttu-id="52ea2-198">참조 테이블의 경우 개발에 대 한 더 toolearn [테이블 개요][Overview], [데이터 형식이 테이블][Data Types], [테이블배포] [ Distribute], [테이블 인덱스][Index], [테이블 분할][Partition], 및 [ 임시 테이블][Temporary]합니다.</span><span class="sxs-lookup"><span data-stu-id="52ea2-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="52ea2-199">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52ea2-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[BCP로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[PolyBase로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase 모범 사례]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[MSDN의 BCP]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
