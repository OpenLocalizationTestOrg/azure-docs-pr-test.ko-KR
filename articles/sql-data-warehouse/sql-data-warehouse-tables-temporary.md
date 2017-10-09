---
title: "SQL 데이터 웨어하우스에 aaaTemporary 테이블 | Microsoft Docs"
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
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="5a55b-103">SQL 데이터 웨어하우스의 임시 테이블</span><span class="sxs-lookup"><span data-stu-id="5a55b-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="5a55b-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="5a55b-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="5a55b-105">[데이터 형식][Data Types]</span><span class="sxs-lookup"><span data-stu-id="5a55b-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="5a55b-106">[배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="5a55b-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="5a55b-107">[인덱스][Index]</span><span class="sxs-lookup"><span data-stu-id="5a55b-107">[Index][Index]</span></span>
> * <span data-ttu-id="5a55b-108">[파티션][Partition]</span><span class="sxs-lookup"><span data-stu-id="5a55b-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="5a55b-109">[통계][Statistics]</span><span class="sxs-lookup"><span data-stu-id="5a55b-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="5a55b-110">[임시][Temporary]</span><span class="sxs-lookup"><span data-stu-id="5a55b-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="5a55b-111">데이터 요금-hello 중간 결과 일시적인 변환 중 특히 처리할 때 임시 테이블은 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="5a55b-112">SQL 데이터 웨어하우스 hello 세션 수준에서 임시 테이블 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="5a55b-113">이들은 표시 toohello 세션에만 생성 된 하 고 하 던 해당 세션을 로그 오프할 때 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="5a55b-114">임시 테이블의 결과 원격 저장소 보다는 toolocal 기록 되기 때문에 성능 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="5a55b-115">임시 테이블은으로 액세스할 수에서 아무 곳 이나 hello 세션을 내부와 외부 저장된 프로시저를 포함 하 여 Azure SQL 데이터베이스 보다 Azure SQL 데이터 웨어하우스에 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="5a55b-116">이 문서는 임시 테이블 사용을 위한 필수 지침을 포함 하 고 세션 수준 임시 테이블의 hello 원칙을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="5a55b-117">이 문서의 hello 정보를 사용 하 여 코드를 재사용 및 코드의 유지 관리의 편의성을 둘 다 향상 모듈화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="5a55b-118">임시 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="5a55b-118">Create a temporary table</span></span>
<span data-ttu-id="5a55b-119">임시 테이블은 간단히 테이블 이름 앞에 `#`을 붙여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="5a55b-120">예:</span><span class="sxs-lookup"><span data-stu-id="5a55b-120">For example:</span></span>

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

<span data-ttu-id="5a55b-121">된 임시 테이블을 만들 수도 있습니다는 `CTAS` 같은 방법을 hello 정확 하 게 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5a55b-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="5a55b-122">`CTAS`매우 강력한 명령이 며이 hello 추가 되 고 트랜잭션 로그 공간 사용에 매우 효율적으로 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="5a55b-123">임시 테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="5a55b-123">Dropping temporary tables</span></span>
<span data-ttu-id="5a55b-124">새 세션이 만들어지면 임시 테이블이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="5a55b-125">하지만 호출 하는 경우 hello 동일한 저장 프로시저를 임시 hello를 사용 하 여 만듭니다 동일한 이름, tooensure 하 여 `CREATE TABLE` 문이 성공적으로 수행 되와 함께 간단한 사전 존재 여부 확인은 `DROP` hello 아래 예제에서와 같이 사용할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="5a55b-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="5a55b-126">일관성을 코딩, 테이블 및 임시 테이블 모두에 대해이 패턴을 좋은 toouse 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="5a55b-127">좋습니다 toouse 이기도 `DROP TABLE` tooremove 임시 테이블을 코드에서 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="5a55b-128">저장된 프로시저 개발 것이 매우 일반적 toosee hello drop 명령이 프로시저 tooensure의 hello 끝에 번들로 묶으면 이러한 개체가 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="5a55b-129">코드 모듈화</span><span class="sxs-lookup"><span data-stu-id="5a55b-129">Modularizing code</span></span>
<span data-ttu-id="5a55b-130">임시 테이블은 사용자 세션에서 아무 곳 이나 볼 수 있습니다, 때문이 응용 프로그램 코드 모듈화 악용 된 toohelp 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="5a55b-131">예를 들어 hello 저장된 프로시저 아래 모여 통계 이름으로 권장 되는 사례 toogenerate DDL hello 데이터베이스의 모든 통계를 업데이트 하면 위쪽부터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="5a55b-132">이 단계에서 hello만 수행 된 동작은 hello 생성 한 저장된 프로시저는 단순히 #stats_ddl DDL 문에서 임시 테이블을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="5a55b-133">이 저장된 프로시저 세션 내에서 두 번 이상 실행 되는 경우 실패 하지 않는 tooensure 이미 있는 경우 # stats_ddl을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="5a55b-134">그러나 없으므로 없습니다 `DROP TABLE` hello 저장 프로시저의 hello 끝 hello 저장된 프로시저가 완료 되 면 둡니다 hello 만든 테이블 hello 저장 프로시저 외부에서 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="5a55b-135">SQL 데이터 웨어하우스, 다른 SQL Server 데이터베이스와 달리 것이 가능한 toouse hello 임시 테이블을 만든 hello 프로시저 외부의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="5a55b-136">SQL 데이터 웨어하우스 임시 테이블을 사용할 수 있습니다 **아무 곳 이나** hello 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="5a55b-137">아래 예제는 hello 처럼 toomore 하 고 관리할 수 있는 모듈식 코드를 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="5a55b-138">임시 테이블 제한 사항</span><span class="sxs-lookup"><span data-stu-id="5a55b-138">Temporary table limitations</span></span>
<span data-ttu-id="5a55b-139">임시 테이블을 구현하는 경우 SQL 데이터 웨어하우스는 두 가지 제한 사항을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="5a55b-140">현재 세션 범위의 임시 테이블만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="5a55b-141">전역 임시 테이블은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="5a55b-142">또한 임시 테이블에서 뷰를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a55b-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a55b-143">Next steps</span></span>
<span data-ttu-id="5a55b-144">toolearn에 hello 문서를 더 참조 [테이블 개요][Overview], [테이블 데이터 형식][Data Types], [테이블배포] [ Distribute], [테이블 인덱스를 만들][Index], [테이블 분할] [ Partition] 및 [ 테이블 통계를 유지 관리][Statistics]합니다.</span><span class="sxs-lookup"><span data-stu-id="5a55b-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="5a55b-145">모범 사례에 대한 자세한 내용은 [SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a55b-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
