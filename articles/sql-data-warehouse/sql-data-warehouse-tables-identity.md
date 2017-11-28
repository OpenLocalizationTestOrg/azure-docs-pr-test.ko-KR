---
title: "IDENTITY를 사용하여 서로게이트 키 만들기 | Microsoft Docs"
description: "IDENTITY를 사용하여 테이블에 서로게이트 키를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="a9fd4-103">IDENTITY를 사용하여 서로게이트 키 만들기</span><span class="sxs-lookup"><span data-stu-id="a9fd4-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a9fd4-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a9fd4-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="a9fd4-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="a9fd4-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-107">[Index][Index]</span></span>
> * <span data-ttu-id="a9fd4-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="a9fd4-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="a9fd4-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="a9fd4-111">[ID][Identity]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="a9fd4-112">데이터 웨어하우스 모델을 설계하는 경우 많은 데이터 모델러는 해당 테이블에 서로게이트 키를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="a9fd4-113">로드 성능에 영향을 주지 않고 간단하고 효과적으로 이 목표를 달성하기 위해 IDENTITY 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="a9fd4-114">IDENTITY 시작</span><span class="sxs-lookup"><span data-stu-id="a9fd4-114">Get started with IDENTITY</span></span>
<span data-ttu-id="a9fd4-115">다음 문과 유사한 구문을 사용하여 테이블을 처음 만드는 경우 테이블이 IDENTITY 속성을 가졌다고 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

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

<span data-ttu-id="a9fd4-116">테이블을 채우는 데 `INSERT..SELECT`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="a9fd4-117">동작</span><span class="sxs-lookup"><span data-stu-id="a9fd4-117">Behavior</span></span>
<span data-ttu-id="a9fd4-118">IDENTITY 속성은 로드 성능에 영향을 주지 않고 데이터 웨어하우스의 모든 배포에 확장하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="a9fd4-119">따라서 IDENTITY를 구현하여 이러한 목표를 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="a9fd4-120">이 섹션에는 보다 완전하게 이해할 수 있도록 구현의 미묘한 차이를 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="a9fd4-121">값 할당</span><span class="sxs-lookup"><span data-stu-id="a9fd4-121">Allocation of values</span></span>
<span data-ttu-id="a9fd4-122">IDENTITY 속성은 서로게이트 값을 할당한 순서를 보장하지 않습니다. 해당 순서는 SQL Server 및 Azure SQL Database의 동작을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="a9fd4-123">그러나 Azure SQL Data Warehouse에서 보장되지 않는다는 점이 더욱 분명합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="a9fd4-124">다음 예제는 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-124">The following example is an illustration:</span></span>

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

<span data-ttu-id="a9fd4-125">앞의 예제에서 두 개의 행이 배포 1에서 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="a9fd4-126">첫 번째 행에는 열 `C1`의 서로게이트 값 1이 있고 두 번째 행에는 서로게이트 값 61이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="a9fd4-127">이 값은 모두 IDENTITY 속성에 의해 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="a9fd4-128">그러나 값은 인접하게 할당되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="a9fd4-129">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="a9fd4-130">불균형 데이터</span><span class="sxs-lookup"><span data-stu-id="a9fd4-130">Skewed data</span></span> 
<span data-ttu-id="a9fd4-131">데이터 형식 값의 범위는 배포에 균등하게 분산되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="a9fd4-132">배포된 테이블에 불균형 데이터가 발생한 경우 데이터 형식으로 사용할 수 있는 값의 범위는 중간에 소진될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="a9fd4-133">예를 들어 모든 데이터가 단일 분포에서 끝난 경우 테이블은 데이터 형식 값의 1/6에만 효율적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="a9fd4-134">이러한 이유로 IDENTITY 속성은 `INT` 및 `BIGINT` 데이터 형식으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="a9fd4-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="a9fd4-135">SELECT..INTO</span></span>
<span data-ttu-id="a9fd4-136">다음 조건 중 하나가 true가 아닌 경우 새 테이블에서 기존 IDENTITY 열을 선택하면 새 열은 IDENTITY 속성을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="a9fd4-137">SELECT 문이 조인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="a9fd4-138">UNION을 사용하여 여러 SELECT 문이 조인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="a9fd4-139">IDENTITY 열이 SELECT 목록에 한 번 이상 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="a9fd4-140">IDENTITY 열이 식의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="a9fd4-141">이러한 조건 중 하나라도 true인 경우 열은 IDENTITY 속성을 상속하지 않고 NOT NULL로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="a9fd4-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="a9fd4-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="a9fd4-143">CTAS(CREATE TABLE AS SELECT)의 경우 SELECT..INTO에서 설명한 동일한 SQL Server 동작을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="a9fd4-144">그러나 문의 `CREATE TABLE` 부분에 있는 열 정의에서 IDENTITY 속성을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="a9fd4-145">CTAS의 `SELECT` 부분에서 IDENTITY 함수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="a9fd4-146">테이블을 채우려면 `CREATE TABLE`를 사용하여 `INSERT..SELECT` 다음의 테이블을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="a9fd4-147">IDENTITY 열에 값을 명시적으로 삽입</span><span class="sxs-lookup"><span data-stu-id="a9fd4-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="a9fd4-148">SQL Data Warehouse는 `SET IDENTITY_INSERT <your table> ON|OFF` 구문을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="a9fd4-149">이 구문을 사용하여 명시적으로 값을 IDENTITY 열에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="a9fd4-150">많은 데이터 모델러는 해당 차원에 있는 특정 행에 미리 정의된 음수 값을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="a9fd4-151">예를 들어 -1 또는 "알 수 없는 멤버" 행입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="a9fd4-152">다음 스크립트에서는 SET IDENTITY_INSERT를 사용하여 이 행을 명시적으로 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="a9fd4-153">IDENTITY가 있는 테이블에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a9fd4-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="a9fd4-154">IDENTITY 속성이 존재한다는 것은 데이터 로딩 코드와 몇 가지 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="a9fd4-155">이 섹션에서는 IDENTITY를 사용하여 테이블로 데이터를 로드하는 몇 가지 기본 패턴을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="a9fd4-156">PolyBase를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a9fd4-156">Load data with PolyBase</span></span>
<span data-ttu-id="a9fd4-157">IDENTITY를 사용하여 테이블에 데이터를 로드하고 서로게이트 키를 생성하려면 테이블을 만든 다음 INSERT..SELECT 또는 INSERT..VALUES를 사용하여 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="a9fd4-158">다음 예제에서는 기본 패턴을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-158">The following example highlights the basic pattern:</span></span>
 
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

--Use INSERT..SELECT to populate the table from an external table
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
> <span data-ttu-id="a9fd4-159">현재 IDENTITY 열이 있는 테이블에 데이터를 로드 하는 경우 `CREATE TABLE AS SELECT`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="a9fd4-160">BCP(대량 복사 프로그램) 도구를 사용하여 데이터를 로드하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="a9fd4-161">[PolyBase로 로드하기][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="a9fd4-162">[PolyBase 모범 사례][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="a9fd4-163">BCP를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a9fd4-163">Load data with BCP</span></span>
<span data-ttu-id="a9fd4-164">BCP는 SQL Data Warehouse로 데이터를 로드하는 데 사용할 수 있는 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="a9fd4-165">해당 매개 변수(-E) 중 하나는 IDENTITY 열이 있는 테이블에 데이터를 로드할 때 BCP의 동작을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="a9fd4-166">-E를 지정하는 경우 IDENTITY를 포함한 열의 입력 파일에 보관된 값이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="a9fd4-167">-E를 지정하지 *않는* 경우 이 열의 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="a9fd4-168">ID 열이 포함되지 않는 경우 데이터가 정상적으로 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="a9fd4-169">속성의 증분 및 초기값 정책에 따라 값이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="a9fd4-170">BCP를 사용하여 데이터를 로드하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="a9fd4-171">[BCP로 로드하기][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-171">[Load with BCP][]</span></span>
- <span data-ttu-id="a9fd4-172">[MSDN의 BCP][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="a9fd4-173">카탈로그 뷰</span><span class="sxs-lookup"><span data-stu-id="a9fd4-173">Catalog views</span></span>
<span data-ttu-id="a9fd4-174">SQL Data Warehouse는 `sys.identity_columns` 카탈로그 뷰를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="a9fd4-175">IDENTITY 속성이 있는 열을 식별하는 데 이 뷰를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="a9fd4-176">이 예제에서는 데이터베이스 스키마를 보다 잘 이해할 수 있도록 다른 시스템 카탈로그 뷰와 `sys.identity_columns`를 통합하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="a9fd4-177">제한 사항</span><span class="sxs-lookup"><span data-stu-id="a9fd4-177">Limitations</span></span>
<span data-ttu-id="a9fd4-178">IDENTITY 속성은 다음과 같은 시나리오에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="a9fd4-179">열 데이터 형식이 INT 또는 BIGINT가 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="a9fd4-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="a9fd4-180">열이 배포 키인 경우</span><span class="sxs-lookup"><span data-stu-id="a9fd4-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="a9fd4-181">테이블이 외부 테이블인 경우</span><span class="sxs-lookup"><span data-stu-id="a9fd4-181">Where the table is an external table</span></span> 

<span data-ttu-id="a9fd4-182">SQL Data Warehouse에서 다음과 같은 관련 함수가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="a9fd4-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="a9fd4-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="a9fd4-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="a9fd4-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="a9fd4-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="a9fd4-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="a9fd4-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="a9fd4-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="a9fd4-190">작업</span><span class="sxs-lookup"><span data-stu-id="a9fd4-190">Tasks</span></span>

<span data-ttu-id="a9fd4-191">이 섹션에서는 IDENTITY 열을 사용하여 작업할 때 일반적인 작업을 수행하는 데 사용할 수 있는 몇 가지 샘플 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="a9fd4-192">열 C1은 다음과 같은 모든 작업의 IDENTITY입니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="a9fd4-193">테이블에 가장 높게 할당된 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="a9fd4-194">`MAX()` 함수를 사용하여 배포된 테이블에 할당된 가장 높은 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="a9fd4-195">IDENTITY 속성에 대한 초기값 및 증분을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="a9fd4-196">다음 쿼리를 사용하여 테이블에 대한 ID 증분 및 초기 구성 값을 검색하기 위해 카탈로그 뷰를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="a9fd4-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9fd4-197">Next steps</span></span>

* <span data-ttu-id="a9fd4-198">테이블 개발에 대해 자세히 알아보려면 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블 배포][Distribute], [테이블 인덱싱][Index], [테이블 분할][Partition] 및 [임시 테이블][Temporary]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="a9fd4-199">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9fd4-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

<span data-ttu-id="a9fd4-200">[BCP로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="a9fd4-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="a9fd4-201">[PolyBase로 로드하기]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="a9fd4-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="a9fd4-202">[PolyBase 모범 사례]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="a9fd4-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="a9fd4-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="a9fd4-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="a9fd4-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="a9fd4-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="a9fd4-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="a9fd4-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="a9fd4-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="a9fd4-210">[MSDN의 BCP]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="a9fd4-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
