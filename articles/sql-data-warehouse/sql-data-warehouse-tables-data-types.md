---
title: "aaaData 형식을 지침-Azure SQL 데이터 웨어하우스 | Microsoft Docs"
description: "권장 사항 toodefine 데이터 형식에 SQL 데이터 웨어하우스와 호환 됩니다."
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
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="8e332-103">SQL Data Warehouse의 테이블에 대한 데이터 형식을 정의하기 위한 지침</span><span class="sxs-lookup"><span data-stu-id="8e332-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="8e332-104">SQL 데이터 웨어하우스와 호환 되는 이러한 권장 사항을 toodefine 테이블 데이터 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-104">Use these recommendations toodefine table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="8e332-105">또한 데이터 형식의 hello 크기를 최소화 toocompatibility 쿼리 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-105">In addition toocompatibility, minimizing hello size of data types improves query performance.</span></span>

<span data-ttu-id="8e332-106">SQL 데이터 웨어하우스는 hello 가장 일반적으로 사용 되는 데이터 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-106">SQL Data Warehouse supports hello most commonly used data types.</span></span> <span data-ttu-id="8e332-107">목록이 hello 지원 데이터 형식에 대 한 참조 [데이터 형식](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) CREATE TABLE 문 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-107">For a list of hello supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in hello CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="8e332-108">행 길이 최소화</span><span class="sxs-lookup"><span data-stu-id="8e332-108">Minimize row length</span></span>
<span data-ttu-id="8e332-109">데이터 형식의 hello 크기를 최소화 hello 행 길이 toobetter 쿼리 성능이 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-109">Minimizing hello size of data types shortens hello row length, which leads toobetter query performance.</span></span> <span data-ttu-id="8e332-110">데이터에 대해 작동 하는 hello 가장 작은 데이터 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-110">Use hello smallest data type that works for your data.</span></span> 

- <span data-ttu-id="8e332-111">문자 열을 큰 기본 길이로 정의하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8e332-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="8e332-112">예를 들어 25 자 hello 가장 긴 값을 사용 하는 경우 프로그램 열 VARCHAR(25)로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-112">For example, if hello longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="8e332-113">VARCHAR만 필요한 경우 [NVARCHAR][NVARCHAR]를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="8e332-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="8e332-114">가능한 경우 NVARCHAR(MAX) 또는 VARCHAR(MAX) 대신 NVARCHAR(4000) 또는 VARCHAR(8000)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="8e332-115">Polybase tooload 테이블 사용 중인 경우 hello 테이블 행의 정의 된 hello 길이 1MB를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-115">If you are using Polybase tooload your tables, hello defined length of hello table row cannot exceed 1 MB.</span></span> <span data-ttu-id="8e332-116">가변 길이 데이터를 사용 하 여 행 1 MB를 초과 하면 hello 행 PolyBase 있지만 with BCP를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-116">When a row with variable-length data exceeds 1 MB, you can load hello row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="8e332-117">지원되지 않는 데이터 형식 식별</span><span class="sxs-lookup"><span data-stu-id="8e332-117">Identify unsupported data types</span></span>
<span data-ttu-id="8e332-118">다른 SQL 데이터베이스에서 데이터베이스를 마이그레이션하려는 경우 SQL Data Warehouse에서 지원되지 않는 데이터 형식이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="8e332-119">기존 SQL 스키마에서이 쿼리 toodiscover 지원 되지 않는 데이터 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-119">Use this query toodiscover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="8e332-120"><a name="unsupported-data-types"></a>지원되지 않는 데이터 형식에 대한 해결 방법 사용</span><span class="sxs-lookup"><span data-stu-id="8e332-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="8e332-121">hello 다음 목록 hello SQL 데이터 웨어하우스를 지원 하지 않는 데이터 형식을 나타내고 제공 대안 hello 대신 사용할 수 있는 데이터 형식이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-121">hello following list shows hello data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of hello unsupported data types.</span></span>

| <span data-ttu-id="8e332-122">지원되지 않는 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="8e332-122">Unsupported data type</span></span> | <span data-ttu-id="8e332-123">해결 방법</span><span class="sxs-lookup"><span data-stu-id="8e332-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="8e332-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="8e332-124">[geometry][geometry]</span></span> |<span data-ttu-id="8e332-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="8e332-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="8e332-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="8e332-126">[geography][geography]</span></span> |<span data-ttu-id="8e332-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="8e332-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="8e332-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="8e332-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="8e332-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="8e332-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="8e332-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="8e332-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="8e332-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="8e332-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="8e332-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="8e332-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="8e332-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="8e332-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="8e332-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="8e332-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="8e332-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="8e332-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="8e332-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="8e332-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="8e332-137">열을 강력한 형식의 열로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="8e332-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="8e332-138">[table][table]</span></span> |<span data-ttu-id="8e332-139">Tootemporary 테이블을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-139">Convert tootemporary tables.</span></span> |
| <span data-ttu-id="8e332-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="8e332-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="8e332-141">코드 toouse 재작업 [datetime2] [ datetime2] 및 `CURRENT_TIMESTAMP` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-141">Rework code toouse [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="8e332-142">상수만 기본값으로 지원됩니다. 따라서 current_timestamp는 기본 제약 조건으로 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="8e332-143">형식화 된 타임 스탬프 열에서 toomigrate 행 버전 값을 필요한 경우 사용 하 여 [이진][BINARY](8) 또는 [VARBINARY][BINARY](8)에 NOT NULL 또는 행 버전 값이 NULL입니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-143">If you need toomigrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="8e332-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="8e332-144">[xml][xml]</span></span> |<span data-ttu-id="8e332-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="8e332-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="8e332-146">[사용자 정의 형식][user defined types]</span><span class="sxs-lookup"><span data-stu-id="8e332-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="8e332-147">가능 하면 뒤로 toohello 네이티브 데이터 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-147">Convert back toohello native data type when possible.</span></span> |
| <span data-ttu-id="8e332-148">기본값</span><span class="sxs-lookup"><span data-stu-id="8e332-148">default values</span></span> | <span data-ttu-id="8e332-149">기본값은 리터럴 및 상수만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="8e332-150">`GETDATE()` 또는 `CURRENT_TIMESTAMP`와 같은 명확하지 않은 식 또는 함수는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e332-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8e332-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e332-151">Next steps</span></span>
<span data-ttu-id="8e332-152">toolearn 더 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8e332-152">toolearn more, see:</span></span>

- <span data-ttu-id="8e332-153">[SQL Data Warehouse 모범 사례][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="8e332-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="8e332-154">[테이블 개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="8e332-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="8e332-155">[테이블 배포][Distribute]</span><span class="sxs-lookup"><span data-stu-id="8e332-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="8e332-156">[테이블 인덱싱][Index]</span><span class="sxs-lookup"><span data-stu-id="8e332-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="8e332-157">[테이블 분할][Partition]</span><span class="sxs-lookup"><span data-stu-id="8e332-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="8e332-158">[테이블 통계 유지 관리][Statistics]</span><span class="sxs-lookup"><span data-stu-id="8e332-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="8e332-159">[임시 테이블][Temporary]</span><span class="sxs-lookup"><span data-stu-id="8e332-159">[Temporary Tables][Temporary]</span></span>

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
