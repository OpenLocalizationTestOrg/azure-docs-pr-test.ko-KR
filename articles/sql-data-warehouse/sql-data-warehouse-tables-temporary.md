---
title: "SQL Data Warehouse의 임시 테이블 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스에서 임시 테이블로 시작"
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="75bc4-103">SQL 데이터 웨어하우스의 임시 테이블</span><span class="sxs-lookup"><span data-stu-id="75bc4-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="75bc4-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="75bc4-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="75bc4-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="75bc4-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="75bc4-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="75bc4-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="75bc4-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="75bc4-107">[Index][Index]</span></span>
> * <span data-ttu-id="75bc4-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="75bc4-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="75bc4-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="75bc4-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="75bc4-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="75bc4-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="75bc4-111">특히 중간 결과가 일시적인 변환 중 데이터를 처리할 때 임시 테이블은 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="75bc4-112">임시 테이블은 SQL 데이터 웨어하우스의 세션 수준에서 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="75bc4-113">이러한 임시 테이블은 생성된 세션에서만 보이고, 해당 세션이 로그오프되면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="75bc4-114">임시 테이블은 결과가 원격 저장소 대신 로컬로 기록되기 때문에 성능상의 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="75bc4-115">Azure SQL 데이터 웨어하우스의 임시 테이블은 저장 프로시저의 내부 및 외부를 비롯하여 세션 내의 어디에서나 액세스할 수 있으므로 Azure SQL 데이터베이스의 임시 테이블과 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="75bc4-116">이 문서에서는 임시 테이블을 사용하기 위한 필수 지침을 제공하고 세션 수준 임시 테이블의 원리를 강조해서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="75bc4-117">이 문서의 정보를 사용하여 코드를 모듈화할 수 있으므로 코드의 재사용 가능성 및 유지 관리 용이성이 개선됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="75bc4-118">임시 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="75bc4-118">Create a temporary table</span></span>
<span data-ttu-id="75bc4-119">임시 테이블은 간단히 테이블 이름 앞에 `#`을 붙여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="75bc4-120">예:</span><span class="sxs-lookup"><span data-stu-id="75bc4-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="75bc4-121">정확히 동일한 접근 방식을 사용하여 `CTAS` 를 통해 임시 테이블을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="75bc4-122">`CTAS` 는 매우 강력한 명령이며 트랜잭션 로그 공간을 사용한다는 점에서 매우 효율적이라는 추가적인 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="75bc4-123">임시 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="75bc4-123">Dropping temporary tables</span></span>
<span data-ttu-id="75bc4-124">새 세션이 만들어지면 임시 테이블이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="75bc4-125">그러나 동일한 이름의 임시 테이블을 만드는 동일한 저장 프로시저를 호출하는 경우 `CREATE TABLE` 문이 정상적으로 수행되도록 하려면 아래 예제와 같이 `DROP`을 사용해서 단순한 사전 존재 여부 확인을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="75bc4-126">코딩 일관성을 유지하려면 테이블 및 임시 테이블 모두에 대해 이 패턴을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="75bc4-127">또한 코드에서 사용을 완료한 경우 `DROP TABLE` 을 사용하여 임시 테이블을 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="75bc4-128">저장 프로시저 개발에서는 프로시저 끝에 삭제 명령이 번들로 포함되어 있는지 확인하여 이러한 개체가 정리되는지 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="75bc4-129">코드 모듈화</span><span class="sxs-lookup"><span data-stu-id="75bc4-129">Modularizing code</span></span>
<span data-ttu-id="75bc4-130">임시 테이블을 사용자 세션의 어디에서나 볼 수 있으므로 응용 프로그램 코드를 모듈화하는 데 이용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="75bc4-131">예를 들어 위의 권장 방법과 아래의 저장 프로시저를 함께 사용하여 데이터베이스의 모든 통계를 통계 이름으로 업데이트하는 DDL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="75bc4-132">이 단계에서 발생하는 유일한 작업은 DDL 문으로 임시 테이블인 #stats_ddl을 생성하는 저장 프로시저를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="75bc4-133">이 저장 프로시저는 세션 내에서 두 번 이상 실행하는 경우 실패하지 않도록 #stats_ddl(이미 있는 경우)을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="75bc4-134">그러나 저장 프로시저 끝에는 `DROP TABLE` 이 없으므로 저장 프로시저가 완료되면 저장 프로시저 외부에서 읽을 수 있도록 만든 테이블이 그대로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="75bc4-135">다른 SQL Server 데이터베이스와 달리, SQL 데이터 웨어하우스에서 임시 테이블을 만든 프로시저의 외부에서 임시 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="75bc4-136">세션 내의 **어디에서나** SQL 데이터 웨어하우스 임시 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="75bc4-137">아래 예제와 같이 모듈식 및 관리 가능 코드가 더 많아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-137">This can lead to more modular and manageable code as in the below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="75bc4-138">임시 테이블 제한 사항</span><span class="sxs-lookup"><span data-stu-id="75bc4-138">Temporary table limitations</span></span>
<span data-ttu-id="75bc4-139">임시 테이블을 구현하는 경우 SQL 데이터 웨어하우스는 두 가지 제한 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="75bc4-140">현재 세션 범위의 임시 테이블만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="75bc4-141">전역 임시 테이블은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="75bc4-142">또한 임시 테이블에서 뷰를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75bc4-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75bc4-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75bc4-143">Next steps</span></span>
<span data-ttu-id="75bc4-144">자세히 알아보려면 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블 배포][Distribute],  [테이블 인덱싱][Index], [테이블 분할][Partition] 및 [테이블 통계 유지 관리][Statistics]에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75bc4-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="75bc4-145">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75bc4-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

<!--Other Web references-->
