---
title: "aaaMigrate 사용자 솔루션 tooSQL 데이터 웨어하우스 | Microsoft Docs"
description: "마이그레이션 지침 tooAzure SQL 데이터 웨어하우스 솔루션 플랫폼으로 전환 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="43126-103">사용자 솔루션 tooAzure SQL 데이터 웨어하우스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="43126-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="43126-104">기존 데이터베이스 솔루션 tooAzure SQL 데이터 웨어하우스 마이그레이션 관련 정보를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="43126-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="43126-105">워크로드 프로파일링</span><span class="sxs-lookup"><span data-stu-id="43126-105">Profile your workload</span></span>
<span data-ttu-id="43126-106">를 마이그레이션하기 전에 toobe SQL 데이터 웨어하우스 작업에 대 한 hello 적합 한 솔루션에는 특정 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="43126-107">SQL 데이터 웨어하우스는 대규모 데이터에 대해 설계 된 분산된 시스템 tooperform 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="43126-108">데이터 웨어하우스 마이그레이션 tooSQL 어려운 toounderstand 이지만 일부 시간 tooimplement 걸리는 일부 디자인 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="43126-109">비즈니스에 필요한 엔터프라이즈 수준의 데이터 웨어하우스, hello 이점 hello 노력 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="43126-110">그러나 SQL 데이터 웨어하우스의 hello 전원 필요 없는 경우 더 많은 비용 효율적인 toouse SQL Server 또는 Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="43126-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="43126-111">다음과 같은 경우 SQL Data Warehouse를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="43126-112">하나 이상의 테라바이트의 데이터가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="43126-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="43126-113">많은 양의 데이터에 계획 toorun 분석</span><span class="sxs-lookup"><span data-stu-id="43126-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="43126-114">Hello 기능 tooscale 계산 및 저장소 필요</span><span class="sxs-lookup"><span data-stu-id="43126-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="43126-115">필요 하지 않을 때 일시 중지 하 여 toosave 비용 계산 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="43126-116">다음과 같은 작업(OLTP) 워크로드에 SQL Data Warehouse를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="43126-117">높은 빈도의 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="43126-117">High frequency reads and writes</span></span>
- <span data-ttu-id="43126-118">많은 수의 단일 항목 선택</span><span class="sxs-lookup"><span data-stu-id="43126-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="43126-119">많은 양의 단일 행 삽입</span><span class="sxs-lookup"><span data-stu-id="43126-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="43126-120">행 단위 처리 요구 사항</span><span class="sxs-lookup"><span data-stu-id="43126-120">Row by row processing needs</span></span>
- <span data-ttu-id="43126-121">호환되지 않는 형식(JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="43126-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="43126-122">Hello 마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="43126-122">Plan hello migration</span></span>

<span data-ttu-id="43126-123">기존 솔루션 tooSQL 데이터 웨어하우스 toomigrate 계획인 중요 tooplan hello 마이그레이션을 시작 하기 전에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="43126-124">계획의 단일 목표 tooensure 테이블 스키마를 데이터도 없으며 SQL 데이터 웨어하우스와 호환 되는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="43126-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="43126-125">현재 시스템 및 SQL 데이터 웨어하우스 간의 주위 호환성 차이점 toowork 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="43126-126">또한 많은 양의 데이터 tooAzure 사용 시간 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="43126-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="43126-127">데이터 tooAzure 가져오는 신속히 신중 하 게 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="43126-128">계획의 또 다른 목표는 솔루션에서는 SQL 데이터 웨어하우스는 hello 높은 쿼리 성능 활용 조정 tooensure 설계 tooprovide toomake 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="43126-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="43126-129">따라서 기존의 접근 방식에서는 없는 가장 hello 경우도 다양 한 디자인 패턴 소개 눈금에 대 한 데이터 웨어하우스를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="43126-130">마이그레이션 후 일부 디자인 조정을 진행할 수 있지만 변경 더 빨리 hello 프로세스에서 나중에 시간을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="43126-131">성공적인 마이그레이션 tooperform 해야 toomigrate 테이블 스키마, 코드 및 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="43126-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="43126-132">이러한 마이그레이션 항목에 대한 지침은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43126-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="43126-133">스키마 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="43126-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="43126-134">코드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="43126-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="43126-135">[데이터 마이그레이션](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="43126-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="43126-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43126-136">Next steps</span></span>
<span data-ttu-id="43126-137">hello CAT (고객 자문 팀)를 통해 블로그 게시 몇 가지 훌륭한 SQL 데이터 웨어하우스 지침을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43126-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="43126-138">해당 문서에 대해 살펴봅니다 [실제로 마이그레이션 데이터 tooAzure SQL 데이터 웨어하우스] [ Migrating data tooAzure SQL Data Warehouse in practice] 마이그레이션에 대 한 추가 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="43126-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
