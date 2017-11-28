---
title: "데이터 형식 지침 - Azure SQL Data Warehouse | Microsoft Docs"
description: "SQL Data Warehouse와 호환되는 데이터 형식을 정의하는 권장 사항입니다."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="b4db0-103">SQL Data Warehouse의 테이블에 대한 데이터 형식을 정의하기 위한 지침</span><span class="sxs-lookup"><span data-stu-id="b4db0-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="b4db0-104">이러한 권장 사항을 사용하여 SQL Data Warehouse와 호환되는 테이블 데이터 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="b4db0-105">호환성 외에도 데이터 형식의 크기를 최소화하면 쿼리 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="b4db0-106">SQL 데이터 웨어하우스는 가장 일반적으로 사용되는 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="b4db0-107">지원되는 데이터 형식의 목록은 CREATE TABLE 문에서 [데이터 형식](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4db0-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="b4db0-108">행 길이 최소화</span><span class="sxs-lookup"><span data-stu-id="b4db0-108">Minimize row length</span></span>
<span data-ttu-id="b4db0-109">데이터 형식의 크기를 최소화하면 쿼리 성능을 향상시키는 행 길이를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="b4db0-110">데이터에 대해 작동하는 가장 작은 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="b4db0-111">문자 열을 큰 기본 길이로 정의하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b4db0-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="b4db0-112">예를 들어 가장 긴 값이 25자인 경우 열을 VARCHAR(25)로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="b4db0-113">VARCHAR만 필요한 경우 [NVARCHAR][NVARCHAR]를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b4db0-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="b4db0-114">가능한 경우 NVARCHAR(MAX) 또는 VARCHAR(MAX) 대신 NVARCHAR(4000) 또는 VARCHAR(8000)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="b4db0-115">Polybase를 사용하여 테이블을 로드하는 경우 정의된 데이터 행의 길이는 1MB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="b4db0-116">가변 길이 데이터가 있는 행이 1MB를 초과하는 경우 행을 PolyBase가 아닌 BCP로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="b4db0-117">지원되지 않는 데이터 형식 식별</span><span class="sxs-lookup"><span data-stu-id="b4db0-117">Identify unsupported data types</span></span>
<span data-ttu-id="b4db0-118">다른 SQL 데이터베이스에서 데이터베이스를 마이그레이션하려는 경우 SQL Data Warehouse에서 지원되지 않는 데이터 형식이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="b4db0-119">이 쿼리를 사용하여 기존 SQL 스키마에서 지원되지 않는 데이터 형식을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="b4db0-120"><a name="unsupported-data-types"></a>지원되지 않는 데이터 형식에 대한 해결 방법 사용</span><span class="sxs-lookup"><span data-stu-id="b4db0-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="b4db0-121">다음 목록은 SQL Data Warehouse에서 지원하지 않는 데이터 형식을 보여 주고 지원되지 않는 데이터 형식 대신 사용할 수 있는 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="b4db0-122">지원되지 않는 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="b4db0-122">Unsupported data type</span></span> | <span data-ttu-id="b4db0-123">해결 방법</span><span class="sxs-lookup"><span data-stu-id="b4db0-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="b4db0-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="b4db0-124">[geometry][geometry]</span></span> |<span data-ttu-id="b4db0-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="b4db0-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="b4db0-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="b4db0-126">[geography][geography]</span></span> |<span data-ttu-id="b4db0-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="b4db0-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="b4db0-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="b4db0-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="b4db0-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="b4db0-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="b4db0-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="b4db0-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="b4db0-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="b4db0-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="b4db0-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="b4db0-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="b4db0-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="b4db0-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="b4db0-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="b4db0-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="b4db0-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="b4db0-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="b4db0-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="b4db0-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="b4db0-137">열을 강력한 형식의 열로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="b4db0-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="b4db0-138">[table][table]</span></span> |<span data-ttu-id="b4db0-139">임시 테이블로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="b4db0-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="b4db0-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="b4db0-141">[datetime2][datetime2] 및 `CURRENT_TIMESTAMP` 함수를 사용하도록 코드 재작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="b4db0-142">상수만 기본값으로 지원됩니다. 따라서 current_timestamp는 기본 제약 조건으로 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="b4db0-143">rowversion 값을 타임스탬프 형식의 열에서 마이그레이션해야 하는 경우, NOT NULL 또는 NULL 행 버전 값으로 [BINARY][BINARY](8) 또는 [VARBINARY][BINARY](8)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="b4db0-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="b4db0-144">[xml][xml]</span></span> |<span data-ttu-id="b4db0-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="b4db0-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="b4db0-146">[사용자 정의 형식][user defined types]</span><span class="sxs-lookup"><span data-stu-id="b4db0-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="b4db0-147">가능하면 네이티브 데이터 형식으로 다시 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="b4db0-148">기본값</span><span class="sxs-lookup"><span data-stu-id="b4db0-148">default values</span></span> | <span data-ttu-id="b4db0-149">기본값은 리터럴 및 상수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="b4db0-150">`GETDATE()` 또는 `CURRENT_TIMESTAMP`와 같은 명확하지 않은 식 또는 함수는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4db0-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="b4db0-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4db0-151">Next steps</span></span>
<span data-ttu-id="b4db0-152">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4db0-152">To learn more, see:</span></span>

- <span data-ttu-id="b4db0-153">[SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="b4db0-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="b4db0-154">[테이블 개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="b4db0-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="b4db0-155">[테이블 배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="b4db0-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="b4db0-156">[테이블 인덱싱][Index]</span><span class="sxs-lookup"><span data-stu-id="b4db0-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="b4db0-157">[테이블 분할][Partition]</span><span class="sxs-lookup"><span data-stu-id="b4db0-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="b4db0-158">[테이블 통계 유지 관리][Statistics]</span><span class="sxs-lookup"><span data-stu-id="b4db0-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="b4db0-159">[임시 테이블][Temporary]</span><span class="sxs-lookup"><span data-stu-id="b4db0-159">[Temporary Tables][Temporary]</span></span>

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
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
