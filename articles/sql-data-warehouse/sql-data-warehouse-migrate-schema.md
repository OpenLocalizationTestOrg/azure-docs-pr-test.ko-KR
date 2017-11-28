---
title: "aaaMigrate 프로그램 스키마 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "솔루션 개발을 위한 프로그램 스키마 tooAzure SQL 데이터 웨어하우스를 마이그레이션하기 위한 팁입니다."
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
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="a4650-103">사용자 스키마 tooSQL 데이터 웨어하우스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="a4650-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="a4650-104">SQL 스키마 tooSQL 데이터 웨어하우스를 마이그레이션하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="a4650-105">스키마 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="a4650-105">Plan your schema migration</span></span>

<span data-ttu-id="a4650-106">마이그레이션을 계획할 때는 hello 참조 [테이블 개요] [ table overview] toobecome 통계, 배포, 분할 및 인덱싱과 같은 테이블 디자인 고려 사항에 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="a4650-107">또한 몇 가지 [지원되지 않는 테이블 기능][unsupported table features] 및 해당 해결 방법을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="a4650-108">사용자 정의 스키마 tooconsolidate 데이터베이스 사용</span><span class="sxs-lookup"><span data-stu-id="a4650-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="a4650-109">기존 워크로드에는 둘 이상의 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="a4650-110">예를 들어 SQL Server 데이터 웨어하우스는 스테이징 데이터베이스, 데이터 웨어하우스 데이터베이스 및 일부 데이터 마트 데이터베이스를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="a4650-111">이 토폴로지에서 각 데이터베이스는 별도 보안 정책을 사용하여 별도 워크로드로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="a4650-112">반면, SQL 데이터 웨어하우스 데이터베이스 내에 hello 전체 데이터 웨어하우스 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="a4650-113">데이터베이스 간 조인은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="a4650-114">따라서 SQL 데이터 웨어하우스는 hello 데이터 웨어하우스 toobe hello 한 데이터베이스에 저장 된 사용 되는 모든 테이블을 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="a4650-115">사용자 정의 스키마 tooconsolidate를 사용 하 여 하나의 데이터베이스에 기존 작업을 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="a4650-116">예를 들어 [사용자 정의 스키마](sql-data-warehouse-develop-user-defined-schemas.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4650-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="a4650-117">호환되는 데이터 형식 사용</span><span class="sxs-lookup"><span data-stu-id="a4650-117">Use compatible data types</span></span>
<span data-ttu-id="a4650-118">SQL 데이터 웨어하우스 호환 데이터 형식 toobe 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="a4650-119">지원되는 데이터 형식 및 지원되지 않는 데이터 형식의 목록은 [데이터 형식][data types]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4650-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="a4650-120">해당 항목 hello 지원 되지 않는 형식에 대 한 해결 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="a4650-121">쿼리 SQL 데이터 웨어하우스에서 지원 되지 않는 tooidentify 기존 형식도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="a4650-122">행 크기 최소화</span><span class="sxs-lookup"><span data-stu-id="a4650-122">Minimize row size</span></span>
<span data-ttu-id="a4650-123">최상의 성능을 위해 테이블의 행 길이가 hello를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="a4650-124">더 짧은 행 길이 toobetter 성능 lead, 이후 데이터에 대해 작동 하는 hello 가장 작은 하는 데이터 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="a4650-125">PolyBase는 테이블 행 너비를 1MB로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="a4650-126">PolyBase 사용 하 여 SQL 데이터 웨어하우스로 tooload 데이터를 계획 하는 경우 1 m B의 사용자 테이블 toohave 최대 행 너비를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="a4650-127">Hello 배포 옵션 지정</span><span class="sxs-lookup"><span data-stu-id="a4650-127">Specify hello distribution option</span></span>
<span data-ttu-id="a4650-128">SQL Data Warehouse는 배포된 데이터베이스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="a4650-129">각 테이블 또는 배포 hello 계산 노드에 복제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="a4650-130">Toodistribute 데이터 hello 하는 방법을 지정할 수 있는 테이블 옵션은.</span><span class="sxs-lookup"><span data-stu-id="a4650-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="a4650-131">hello 선택 항목은 라운드 로빈, 복제 또는 해시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="a4650-132">각각에 장점 및 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-132">Each has pros and cons.</span></span> <span data-ttu-id="a4650-133">Hello 배포 옵션을 지정 하지 않으면 SQL 데이터 웨어하우스 라운드 로빈 hello 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="a4650-134">라운드 로빈 hello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-134">Round-robin is hello default.</span></span> <span data-ttu-id="a4650-135">Hello 가장 간단한 toouse 되 고, 가능한 한 빠르게 hello 데이터를 로드 하지만 조인 하면 쿼리 성능이 저하는 데이터 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="a4650-136">복제 된 각 계산 노드에 대해 hello 테이블의 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="a4650-137">복제된 테이블은 조인 및 집계에 데이터 이동을 필요로 하지 않기 때문에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="a4650-138">추가 저장소가 필요하므로 작은 테이블에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="a4650-139">Distributed 해시는 해시 함수를 통해 모든 hello 노드에서 hello 행을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="a4650-140">배포 하는 해시 테이블 SQL 데이터 웨어하우스의 hello 핵심 되므로 대형 테이블에 쿼리 성능이 디자인 된 tooprovide는입니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="a4650-141">이 옵션에는 몇 가지 계획 tooselect hello 적합 한 열 toodistribute hello 데이터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="a4650-142">그러나 경우을 선택 하지 않으면 hello 최상의 열 hello 처음으로 배포할 수 있습니다 쉽게 다시 hello 데이터는 다른 열.</span><span class="sxs-lookup"><span data-stu-id="a4650-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="a4650-143">각 테이블에 대해 toochoose hello 최상의 배포 옵션 참조 [테이블 Distributed](sql-data-warehouse-tables-distribute.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4650-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4650-144">Next steps</span></span>
<span data-ttu-id="a4650-145">데이터베이스 스키마 tooSQL 데이터 웨어하우스를 성공적으로 마이그레이션한 후 tooone의 hello 다음 문서를 계속 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4650-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="a4650-146">[데이터 마이그레이션][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="a4650-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="a4650-147">[코드 마이그레이션][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="a4650-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="a4650-148">SQL 데이터 웨어하우스 모범 사례에 대 한 자세한 참조 hello [모범 사례] [ best practices] 문서.</span><span class="sxs-lookup"><span data-stu-id="a4650-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

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
