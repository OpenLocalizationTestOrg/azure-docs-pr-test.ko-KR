---
title: "SQL Data Warehouse에 솔루션 마이그레이션| Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 플랫폼에 솔루션을 가져오기 위한 마이그레이션 지침"
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
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="d60bc-103">Azure SQL Data Warehouse에 솔루션 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d60bc-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d60bc-104">Azure SQL Data Warehouse로 기존 데이터베이스 솔루션을 마이그레이션하는 데 관련된 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d60bc-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="d60bc-105">워크로드 프로파일링</span><span class="sxs-lookup"><span data-stu-id="d60bc-105">Profile your workload</span></span>
<span data-ttu-id="d60bc-106">마이그레이션하기 전에 워크로드에 적합한 솔루션인 특정 SQL Data Warehouse를 선택하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="d60bc-107">SQL Data Warehouse는 대규모 데이터 분석을 수행하도록 설계되고 배포된 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="d60bc-108">SQL Data Warehouse로 마이그레이션하려면 이해하기 어렵지 않지만 구현하는 데 시간이 걸릴 수 있는 몇 가지 설계를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="d60bc-109">비즈니스에 엔터프라이즈 수준의 데이터 웨어하우스가 필요한 경우 충분한 혜택을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="d60bc-110">그러나 SQL Data Warehouse의 기능이 필요하지 않은 경우 SQL Server 또는 Azure SQL Database를 사용하는 것이 더 비용 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="d60bc-111">다음과 같은 경우 SQL Data Warehouse를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="d60bc-112">하나 이상의 테라바이트의 데이터가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="d60bc-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="d60bc-113">많은 양의 데이터에 대한 분석을 실행하려는 경우</span><span class="sxs-lookup"><span data-stu-id="d60bc-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="d60bc-114">계산 및 저장소의 크기를 조정하는 기능이 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="d60bc-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="d60bc-115">필요하지 않을 때 계산 리소스를 일시 중지하여 비용을 절감하는 경우</span><span class="sxs-lookup"><span data-stu-id="d60bc-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="d60bc-116">다음과 같은 작업(OLTP) 워크로드에 SQL Data Warehouse를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="d60bc-117">높은 빈도의 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="d60bc-117">High frequency reads and writes</span></span>
- <span data-ttu-id="d60bc-118">많은 수의 단일 항목 선택</span><span class="sxs-lookup"><span data-stu-id="d60bc-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="d60bc-119">많은 양의 단일 행 삽입</span><span class="sxs-lookup"><span data-stu-id="d60bc-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="d60bc-120">행 단위 처리 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d60bc-120">Row by row processing needs</span></span>
- <span data-ttu-id="d60bc-121">호환되지 않는 형식(JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="d60bc-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="d60bc-122">마이그레이션 계획</span><span class="sxs-lookup"><span data-stu-id="d60bc-122">Plan the migration</span></span>

<span data-ttu-id="d60bc-123">SQL Data Warehouse에 기존 솔루션을 마이그레이션하기로 결정했다면 시작하기 전에 마이그레이션을 계획해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="d60bc-124">데이터, 테이블 스키마 및 코드가 SQL Data Warehouse와 호환되는지 확인하는 것이 계획의 중요한 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="d60bc-125">현재 시스템 및 SQL Data Warehouse 간에 호환성 차이점을 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="d60bc-126">또한 많은 양의 데이터를 Azure로 마이그레이션하는 데 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="d60bc-127">신중하게 계획하면 신속하게 Azure에 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="d60bc-128">계획의 또 다른 목표는 솔루션에서 SQL Data Warehouse가 제공하도록 설계된 높은 쿼리 성능을 활용하도록 설계를 조정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="d60bc-129">확장을 위한 데이터 웨어하우스의 디자인은 다양한 디자인 패턴을 도입하므로 일반적인 접근 방식이 항상 최선은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="d60bc-130">마이그레이션 후에 일부 설계를 조정할 수 있지만 프로세스를 더 빨리 변경하면 나중에 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="d60bc-131">성공적인 마이그레이션을 수행하려면 테이블 스키마, 코드 및 데이터를 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="d60bc-132">이러한 마이그레이션 항목에 대한 지침은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d60bc-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="d60bc-133">스키마 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d60bc-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="d60bc-134">코드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="d60bc-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="d60bc-135">[데이터 마이그레이션](sql-data-warehouse-migrate-data.md)</span><span class="sxs-lookup"><span data-stu-id="d60bc-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="d60bc-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d60bc-136">Next steps</span></span>
<span data-ttu-id="d60bc-137">CAT(고객 자문 팀)에서 블로그를 통해 게시하는 몇 가지 유용한 SQL Data Warehouse 관련 지침도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d60bc-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="d60bc-138">[Azure SQL Data Warehouse로의 데이터 마이그레이션 실습][Migrating data to Azure SQL Data Warehouse in practice] 문서에서 마이그레이션 관련 추가 지침을 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d60bc-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
