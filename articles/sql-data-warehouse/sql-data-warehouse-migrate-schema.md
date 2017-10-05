---
title: "SQL Data Warehouse로 스키마 마이그레이션| Microsoft Docs"
description: "솔루션 개발을 위한 Azure SQL 데이터 웨어하우스로 스키마를 마이그레이션하기 위한 팁"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="056be-103">SQL Data Warehouse로 스키마 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="056be-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="056be-104">SQL Data Warehouse에 SQL 스키마를 마이그레이션하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="056be-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="056be-105">스키마 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="056be-105">Plan your schema migration</span></span>

<span data-ttu-id="056be-106">마이그레이션을 계획할 경우 [테이블 개요][table overview]를 참조하여 통계, 배포, 분할 및 인덱싱과 같은 테이블 설계 고려 사항에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="056be-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="056be-107">또한 몇 가지 [지원되지 않는 테이블 기능][unsupported table features] 및 해당 해결 방법을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="056be-108">사용자 정의 스키마를 사용하여 데이터베이스 통합</span><span class="sxs-lookup"><span data-stu-id="056be-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="056be-109">기존 워크로드에는 둘 이상의 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="056be-110">예를 들어 SQL Server 데이터 웨어하우스는 스테이징 데이터베이스, 데이터 웨어하우스 데이터베이스 및 일부 데이터 마트 데이터베이스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="056be-111">이 토폴로지에서 각 데이터베이스는 별도 보안 정책을 사용하여 별도 워크로드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="056be-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="056be-112">반면, SQL 데이터 웨어하우스는 하나의 데이터베이스 내에서 전체 데이터 웨어하우스 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="056be-113">데이터베이스 간 조인은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="056be-114">따라서 SQL Data Warehouse는 데이터 웨어하우스에서 사용된 모든 테이블을 하나의 데이터베이스 내에 저장할 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="056be-115">사용자 정의 스키마를 사용하여 하나의 데이터베이스에 기존 워크로드를 통합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="056be-116">예를 들어 [사용자 정의 스키마](sql-data-warehouse-develop-user-defined-schemas.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="056be-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="056be-117">호환되는 데이터 형식 사용</span><span class="sxs-lookup"><span data-stu-id="056be-117">Use compatible data types</span></span>
<span data-ttu-id="056be-118">SQL Data Warehouse와 호환되도록 데이터 형식을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="056be-119">지원되는 데이터 형식 및 지원되지 않는 데이터 형식의 목록은 [데이터 형식][data types]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="056be-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="056be-120">해당 항목은 지원되지 않는 형식에 대한 해결 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="056be-121">또한SQL Data Warehouse에서 지원되지 않는 기존 형식을 식별하는 쿼리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="056be-122">행 크기 최소화</span><span class="sxs-lookup"><span data-stu-id="056be-122">Minimize row size</span></span>
<span data-ttu-id="056be-123">최상의 성능을 위해 테이블의 행 길이를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="056be-124">행 길이가 짧으면 성능을 향상시키기 때문에 데이터에 작동하는 가장 작은 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="056be-125">PolyBase는 테이블 행 너비를 1MB로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="056be-126">PolyBase를 사용하여 SQL Data Warehouse로 데이터를 로드하려는 경우 최대 행 너비가 1MB 미만이 되도록 테이블을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="056be-127">배포 옵션 지정</span><span class="sxs-lookup"><span data-stu-id="056be-127">Specify the distribution option</span></span>
<span data-ttu-id="056be-128">SQL Data Warehouse는 배포된 데이터베이스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="056be-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="056be-129">각 테이블은 계산 노드에 배포되거나 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="056be-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="056be-130">데이터를 배포하는 방법을 지정할 수 있는 테이블 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="056be-131">라운드 로빈, 복제 또는 해시 배포를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="056be-132">각각에 장점 및 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-132">Each has pros and cons.</span></span> <span data-ttu-id="056be-133">배포 옵션을 지정하지 않은 경우 SQL Data Warehouse는 기본적으로 라운드 로빈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="056be-134">라운드 로빈이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="056be-134">Round-robin is the default.</span></span> <span data-ttu-id="056be-135">사용하기 간단하고 데이터를 빠르게 로드하지만 조인에는 쿼리 성능을 저하시키는 데이터 이동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="056be-136">복제는 각 계산 노드에 테이블의 복사본을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="056be-137">복제된 테이블은 조인 및 집계에 데이터 이동을 필요로 하지 않기 때문에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="056be-138">추가 저장소가 필요하므로 작은 테이블에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="056be-139">배포된 해시는 해시 함수를 통해 모든 노드에 행을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="056be-140">배포된 해시 테이블은 큰 테이블에서 높은 쿼리 성능을 제공하도록 설계되었기 때문에 SQL Data Warehouse의 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="056be-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="056be-141">이 옵션을 사용하려면 데이터를 배포하는 경우 가장 적합한 열을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="056be-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="056be-142">그러나 처음으로 가장 적합한 열을 선택하지 않더라도 다른 열에 데이터를 다시 쉽게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="056be-143">각 테이블에 가장 적합한 배포 옵션을 선택하려면 [배포된 테이블](sql-data-warehouse-tables-distribute.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="056be-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="056be-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="056be-144">Next steps</span></span>
<span data-ttu-id="056be-145">SQL 데이터 웨어하우스로 데이터베이스 스키마를 성공적으로 마이그레이션한 후에 다음 문서 중 하나를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="056be-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="056be-146">[데이터 마이그레이션][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="056be-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="056be-147">[코드 마이그레이션][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="056be-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="056be-148">SQL Data Warehouse 모범 사례에 대한 자세한 내용은 [모범 사례][best practices] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="056be-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
