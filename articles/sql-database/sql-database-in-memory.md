---
title: "Azure SQL Database 메모리 내 기술 | Microsoft Docs"
description: "Azure SQL Database 메모리 내 기술은 트랜잭션 및 분석 작업의 성능을 크게 향상시킵니다. 이러한 기술을 활용하는 방법을 알아봅니다."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="060cb-104">SQL Database에서 메모리 내 기술을 사용하여 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="060cb-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="060cb-105">Azure SQL Database의 메모리 내 기술을 사용하여 트랜잭션(OLTP(온라인 트랜잭션 처리)), 분석(OLAP(온라인 분석 처리)), 혼합(HTAP(하이브리드 트랜잭션/분석 처리))과 같은 다양한 워크로드의 성능을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="060cb-106">메모리 내 기술을 사용하면 보다 효율적인 쿼리 및 트랜잭션 처리로 인해 비용을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="060cb-107">일반적으로는 성능 향상을 위해 데이터베이스의 가격 책정 계층을 업그레이드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="060cb-108">일부 경우에 가격 책정 계층을 줄이는 동시에 메모리 내 기술의 성능이 향상된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="060cb-109">메모리 내 OLTP가 성능을 크게 향상시키는 방법의 두 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="060cb-110">메모리 내 OLTP를 사용하여 [Quorum Business Solutions은 DTU를 70%까지 개선하면서 작업량을 두 배로 늘릴 수 있었습니다](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="060cb-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="060cb-111">여기서 DTU는 *데이터베이스 처리량 단위*를 의미하며 리소스 소비량의 측정값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="060cb-112">다음 [Azure SQL Database의 메모리 내 OLTP 동영상](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)은 샘플 워크로드에서 리소스 소비가 크게 향상되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="060cb-113">자세한 내용은 [Azure SQL Database의 메모리 내 OLTP 블로그 게시물](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="060cb-114">메모리 내 기술은 프리미엄 탄력적 풀의 데이터베이스를 비롯한 프리미엄 계층의 모든 데이터베이스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="060cb-115">다음 비디오에서는 Azure SQL Database에서 메모리 내 기술을 포함한 잠재적인 성능 향상에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="060cb-116">향상된 성능은 워크로드 및 데이터의 특성, 데이터베이스 등의 액세스 패턴을 포함한 많은 요인에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="060cb-117">Azure SQL Database에는 다음과 같은 메모리 내 기술이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="060cb-118">*메모리 내 OLTP*은 처리량을 증가시키고 트랜잭션 처리에 대한 대기 시간을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="060cb-119">메모리 내 OLTP를 활용하는 시나리오는 거래와 게임, 이벤트 또는 IoT 장치의 데이터 수집, 캐싱, 데이터 부하 및 임시 테이블과 테이블 변수 시나리오와 같은 처리량 많은 트랜잭션을 처리하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="060cb-120">*클러스터형 Columnstore 인덱스*는 저장소 공간을 최대 10배로 감소시키고 보고 및 분석 쿼리에 대한 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="060cb-121">데이터베이스에 있는 더 많은 데이터에 적합한 데이터 마트에서 팩트 테이블과 함께 이 기능을 사용하여 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="060cb-122">운영 데이터베이스에 있는 기록 데이터와 함께 이 기능을 사용하여 최대 10배 더 많은 데이터를 보관하고 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="060cb-123">HTAP에 대한 *비클러스터형 Columnstore 인덱스*를 통해 비용이 많이 드는 ETL(추출, 변형 및 로드) 프로세스를 실행하거나 데이터 웨어하우스를 채울 때까지 기다릴 필요 없이 운영 데이터베이스를 직접 쿼리하여 비즈니스에 대한 실시간 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="060cb-124">비클러스터형 Columnstore 인덱스를 사용하면 운영 워크로드에 미치는 영향을 줄이는 동시에 OLTP 데이터베이스에 대한 분석 쿼리를 매우 빠르게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="060cb-125">columnstore 인덱스가 있는 메모리 최적화 테이블 조합도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="060cb-126">이러한 조합을 사용하면 트랜잭션 처리를 매우 빠르게 수행하고 동일한 데이터에서 분석 쿼리를 매우 신속하게 *동시* 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="060cb-127">columnstore 인덱스 및 메모리 내 OLTP는 각각 SQL Server 제품 2012 및 2014 이상에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="060cb-128">Azure SQL Database 및 SQL Server는 메모리 내 기술의 동일한 구현을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="060cb-129">앞으로 이러한 기술에 대한 새로운 기능을 SQL Server에 배포하기 전에 Azure SQL Database에서 먼저 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="060cb-130">이 항목에서는 Azure SQL Database와 관련된 메모리 내 OLTP 및 columnstore 인덱스의 측면을 설명하며 다음과 같은 샘플도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="060cb-131">여기서는 데이터 크기 제한과 저장소에 대한 이와 같은 기술의 영향에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="060cb-132">그리고 이러한 기술을 사용하는 데이터베이스를 여러 가격 책정 계층 간에 이동하는 작업을 관리하는 방법도 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="060cb-133">또한 Azure SQL Database의 columnstore 인덱스뿐만 아니라 메모리 내 OLTP의 사용을 보여 주는 두 개의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="060cb-134">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-134">See the following resources for more information.</span></span>

<span data-ttu-id="060cb-135">기술에 대한 자세한 정보는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="060cb-136">[메모리 내 OLTP 개요 및 사용 시나리오](https://msdn.microsoft.com/library/mt774593.aspx)(고객 사례 연구 및 시작 정보에 대한 참조 포함)</span><span class="sxs-lookup"><span data-stu-id="060cb-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="060cb-137">메모리 내 OLTP에 대한 설명서</span><span class="sxs-lookup"><span data-stu-id="060cb-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="060cb-138">Columnstore 인덱스 가이드</span><span class="sxs-lookup"><span data-stu-id="060cb-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="060cb-139">HTAP(하이브리드 트랜잭션/분석 처리) 즉, [실시간 운영 분석](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="060cb-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="060cb-140">메모리 내 OLTP에 대한 빠른 입문서: [빠른 시작 1: 더 빠른 T-SQL 성능에 대한 메모리 내 OLTP 기술](http://msdn.microsoft.com/library/mt694156.aspx)(시작하는 데 유용한 다른 문서)</span><span class="sxs-lookup"><span data-stu-id="060cb-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="060cb-141">기술에 대한 자세한 비디오:</span><span class="sxs-lookup"><span data-stu-id="060cb-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="060cb-142">[Azure SQL Database의 메모리 내 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)(성능 이점에 대한 데모 및 이 결과를 사용자 스스로 재현하는 단계 포함)</span><span class="sxs-lookup"><span data-stu-id="060cb-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="060cb-143">메모리 내 OLTP 비디오: 기능 정의 및 사용 시기/방법</span><span class="sxs-lookup"><span data-stu-id="060cb-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="060cb-144">Columnstore 인덱스: Ignite 2016의 메모리 내 분석 비디오</span><span class="sxs-lookup"><span data-stu-id="060cb-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="060cb-145">저장소 및 데이터 크기</span><span class="sxs-lookup"><span data-stu-id="060cb-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="060cb-146">메모리 내 OLTP의 데이터 크기 및 저장 제한</span><span class="sxs-lookup"><span data-stu-id="060cb-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="060cb-147">메모리 내 OLTP는 사용자 데이터를 저장하는 데 사용되는 메모리에 최적화된 테이블을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="060cb-148">이러한 테이블은 메모리에 적합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="060cb-149">SQL Database 서비스에 직접 메모리를 관리하기 때문에 사용자 데이터에 대한 할당량의 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="060cb-150">이 개념은 *메모리 내 OLTP 저장소*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="060cb-151">지원되는 독립 실행형 데이터베이스 가격 책정 계층 및 탄력적 풀 가격 책정 계층은 각각 일정량의 메모리 내 OLTP 저장소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="060cb-152">작성할 때 모든 125개의 DTU(데이터베이스 트랜잭션 단위) 또는 eDTU(Elastic Database 트랜잭션 단위)에 대해 기가바이트 단위의 저장소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="060cb-153">[SQL Database 서비스 계층](sql-database-service-tiers.md) 문서에는 지원되는 독립 실행형 데이터베이스 및 탄력적 풀 가격 책정 계층 각각에 사용 가능한 메모리 내 OLTP 저장소의 공식 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="060cb-154">메모리 내 OLTP 저장소 제한 계산 시 포함되는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="060cb-155">메모리 최적화된 테이블 및 테이블 변수의 활성 사용자 데이터 행입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="060cb-156">예전 행 버전은 제한에 고려되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="060cb-157">메모리 최적화된 테이블에 대한 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="060cb-158">ALTER TABLE 작업의 작업 오버헤드입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="060cb-159">제한에 도달한 경우 할당량 초과 오류가 표시되고 더 이상 데이터를 삽입하거나 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="060cb-160">이 오류를 완화하려면 데이터를 삭제하거나 데이터베이스 또는 풀의 가격 책정 계층을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="060cb-161">제한에 도달한 경우 메모리 내 OLTP 저장소 사용률을 모니터링하고 경고를 구성하는 방법에 대한 자세한 내용은 [메모리 내 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="060cb-162">탄력적 풀에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="060cb-162">About elastic pools</span></span>

<span data-ttu-id="060cb-163">탄력적 풀을 사용하여 메모리 내 OLTP 저장소는 풀에 있는 모든 데이터베이스에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="060cb-164">따라서 한 데이터베이스의 사용량은 다른 데이터베이스에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="060cb-165">두 가지 해결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="060cb-166">데이터베이스의 최대 eDTU를 전체 풀의 eDTU 수보다 낮게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="060cb-167">이 최대값은 풀에 있는 모든 데이터베이스에서 메모리 내 OLTP 저장소 사용률을 eDTU 수에 해당하는 크기로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="060cb-168">최소 eDTU를 0보다 크게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="060cb-169">이 최소값은 풀에 있는 각 데이터베이스가 구성된 최소 eDTU에 해당하는 사용 가능한 메모리 내 OLTP 저장소의 양을 사용할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="060cb-170">columnstore 인덱스의 데이터 크기 및 저장소</span><span class="sxs-lookup"><span data-stu-id="060cb-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="060cb-171">columnstore 인덱스는 메모리에 적합할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="060cb-172">따라서 인덱스의 크기에 대한 유일한 제한은 전체 최대 데이터베이스 크기이며 [SQL Database 서비스 계층](sql-database-service-tiers.md) 문서에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="060cb-173">클러스터형 columnstore 인덱스를 사용하는 경우 기본 Table Storage에 칼럼 형식 압축을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="060cb-174">이러한 압축을 사용하면 사용자 데이터의 저장소 공간을 크게 줄일 수 있습니다. 즉, 데이터베이스에 더 많은 데이터를 담을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="060cb-175">또한 [칼럼 형식 보관 압축](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)을 사용하여 압축량을 더욱 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="060cb-176">수행할 수 있는 압축량은 데이터의 특성에 따라 달라지지만 10배 압축은 일반적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="060cb-177">예를 들어, 최대 크기 1TB(테라바이트)인 데이터베이스가 있고 columnstore 인덱스를 사용하여 10배 압축을 달성한 경우 데이터베이스에 총 10TB의 사용자 데이터를 담을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="060cb-178">비클러스터형 columnstore 인덱스를 사용하는 경우 기본 테이블은 여전히 기존의 rowstore 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="060cb-179">따라서 절약된 저장소는 클러스터형 columnstore 인덱스만큼 크지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="060cb-180">그러나 많은 기존의 비클러스터형 인덱스를 단일 columnstore 인덱스로 바꾸는 경우 테이블에 대한 저장소 공간에서 절약된 전체 공간을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="060cb-181">가격 책정 계층 간의 메모리 내 기술을 사용하여 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="060cb-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="060cb-182">표준에서 프리미엄으로 업그레이드하는 등 상위 가격 책정 계층으로 업그레이드할 때는 비호환성이나 기타 문제가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="060cb-183">사용할 수 있는 기능 및 리소스만 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="060cb-184">하지만 가격 책정 계층을 다운그레이드하면 데이터베이스 성능이 저하될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="060cb-185">데이터베이스에 메모리 내 OLTP 개체가 포함되어 있을 때 프리미엄에서 표준이나 기본으로 다운그레이드하면 성능 저하 현상이 특히 뚜렷하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="060cb-186">메모리 최적화 테이블 및 columnstore 인덱스는 계속 표시되더라도 다운그레이드 후에 사용할 수 없는 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="060cb-187">탄력적 풀의 가격 책정 계층을 낮추거나 메모리 내 기술을 포함한 데이터베이스를 표준 또는 기본 탄력적 풀로 이동하는 경우에도 동일한 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="060cb-188">메모리 내 OLTP</span><span class="sxs-lookup"><span data-stu-id="060cb-188">In-Memory OLTP</span></span>

<span data-ttu-id="060cb-189">*기본/표준으로 다운그레이드*: 메모리 내 OLTP는 표준 또는 기본 계층에 있는 데이터베이스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="060cb-190">또한 메모리 내 OLTP 개체가 있는 데이터베이스를 표준 또는 기본 계층에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="060cb-191">데이터베이스를 표준/기본으로 다운그레이드하기 전에 모든 메모리 최적화된 테이블 및 테이블 형식뿐만 아니라 고유하게 컴파일된 모든 T-SQL 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="060cb-192">지정된 데이터베이스가 메모리 내 OLTP를 지원하는지 여부를 프로그래밍 방식으로 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="060cb-193">다음 Transact-SQL 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="060cb-194">쿼리가 **1**을 반환하는 경우 메모리 내 OLTP는 이 데이터베이스에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="060cb-195">*하위 프리미엄 계층으로 다운그레이드*: 메모리 최적화된 테이블의 데이터는 데이터베이스의 가격 책정 계층과 연결되거나 탄력적 풀에서 사용할 수 있는 메모리 내 OLTP 저장소 내에 담겨야 합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="060cb-196">가격 책정 계층을 줄이려고 하거나 충분히 사용 가능한 메모리 내 OLTP 저장소가 없는 풀로 데이터베이스를 이동하려는 경우 작업은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="060cb-197">Columnstore 인덱스</span><span class="sxs-lookup"><span data-stu-id="060cb-197">Columnstore indexes</span></span>

<span data-ttu-id="060cb-198">*기본 또는 표준으로 다운그레이드*: columnstore 인덱스는 프리미엄 가격 책정 계층에서만 지원되며 표준 또는 기본 계층에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="060cb-199">데이터베이스를 표준 또는 기본으로 다운그레이드하면 columnstore 인덱스를 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="060cb-200">시스템에서 columnstore 인덱스가 유지는 되지만 사용되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="060cb-201">나중에 다시 프리미엄으로 업그레이드하는 경우 columnstore 인덱스는 즉시 다시 사용 가능한 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="060cb-202">**클러스터형** columnstore 인덱스가 있는 경우에는 계층 다운그레이드 후에 전체 테이블을 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="060cb-203">그러므로 프리미엄 계층보다 하위 계층으로 데이터베이스를 다운그레이드하기 전에 *클러스터형* columnstore 인덱스를 모두 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="060cb-204">*하위 프리미엄 계층으로 다운그레이드*: 대상 가격 책정 계층의 최대 데이터베이스 크기 또는 탄력적 풀의 사용 가능한 저장소 내에 전체 데이터베이스를 포함할 수 있으면 이 다운그레이드는 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="060cb-205">columnstore 인덱스로부터 특별한 영향은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="060cb-206">1. 메모리 내 OLTP 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="060cb-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="060cb-207">[Azure Portal](https://portal.azure.com/)에서 몇 번만 클릭하면 AdventureWorksLT 샘플 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="060cb-208">그런 다음 이 섹션의 단계에서는 메모리 내 OLTP 개체를 사용하여 AdventureWorksLT 데이터베이스를 보강할 수 있는 방법 및 성능 이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="060cb-209">메모리 내 OLTP의 경우 더 간단하지만 시각적으로 뛰어난 성능 데모는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="060cb-210">릴리스: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="060cb-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="060cb-211">소스 코드: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="060cb-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="060cb-212">설치 단계</span><span class="sxs-lookup"><span data-stu-id="060cb-212">Installation steps</span></span>

1. <span data-ttu-id="060cb-213">[Azure Portal](https://portal.azure.com/)에서 서버에 Premium 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="060cb-214">AdventureWorksLT 샘플 데이터베이스에 **소스**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="060cb-215">자세한 지침은 [첫 번째 Azure SQL Database 만들기](sql-database-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="060cb-216">SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)를 사용하여 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="060cb-217">[메모리 내 OLTP Transact-SQL 스크립트](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) 를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="060cb-218">T-SQL 스크립트는 1단계에서 만든 AdventureWorksLT 샘플 데이터베이스에서 필요한 메모리 내 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="060cb-219">SSMS에 T-SQL 스크립트를 붙여 넣고 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="060cb-220">`MEMORY_OPTIMIZED = ON` 절 CREATE TABLE 문이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="060cb-221">예:</span><span class="sxs-lookup"><span data-stu-id="060cb-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="060cb-222">오류 40536</span><span class="sxs-lookup"><span data-stu-id="060cb-222">Error 40536</span></span>


<span data-ttu-id="060cb-223">T-SQL 스크립트를 실행할 때 오류 40536을 받게 되면 다음 T-SQL 스크립트를 실행하여 데이터베이스에서 메모리를 지원하는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="060cb-224">**0**이라는 결과는 메모리 내가 지원되지 않음을 나타내고 **1**은 지원됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="060cb-225">문제를 진단하려면 데이터베이스가 프리미엄 서비스 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="060cb-226">생성된 메모리 최적화된 항목에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="060cb-226">About the created memory-optimized items</span></span>

<span data-ttu-id="060cb-227">**테이블**: 샘플은 다음과 같은 메모리 액세스에 최적화된 테이블을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="060cb-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="060cb-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="060cb-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="060cb-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="060cb-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="060cb-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="060cb-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="060cb-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="060cb-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="060cb-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="060cb-233">SSMS의 **개체 탐색기** 를 통해 메모리 액세스에 최적화된 테이블을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="060cb-234">**테이블** > **필터** > **필터 설정** > **메모리 액세스에 최적화됨**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="060cb-235">값은 1과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-235">The value equals 1.</span></span>


<span data-ttu-id="060cb-236">또는 다음과 같은 카탈로그 뷰를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="060cb-237">**고유하게 컴파일된 저장 프로시저**: 카탈로그 뷰 쿼리를 통해 SalesLT.usp_InsertSalesOrder_inmem을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="060cb-238">샘플 OLTP 워크로드 실행</span><span class="sxs-lookup"><span data-stu-id="060cb-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="060cb-239">다음 두 *저장 프로시저* 간의 유일한 차이점은 첫 번째 절차는 메모리 액세스에 최적화된 테이블 버전을 사용하는 반면 두 번째 절차에서는 일반 디스크상의 테이블을 사용한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="060cb-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="060cb-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="060cb-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="060cb-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="060cb-242">이 섹션에는 편리한 **ostress.exe** 유틸리티를 사용하여 스트레스 수준에서 두 저장된 프로시저를 실행하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="060cb-243">두 스트레스가 실행을 마치는 데 걸리는 시간을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="060cb-244">ostress.exe를 실행하는 경우 다음 모두에 대해 설계된 매개 변수 값을 전달하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="060cb-245">-n100을 사용하여 많은 수의 동시 연결을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="060cb-246">-r500을 사용하여 각 연결 루프를 수백 번 가집니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="060cb-247">그러나 모든 것이 작동하도록 -n10 및 -r50과 같은 훨씬 작은 값으로 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="060cb-248">ostress.exe에 대한 스크립트</span><span class="sxs-lookup"><span data-stu-id="060cb-248">Script for ostress.exe</span></span>


<span data-ttu-id="060cb-249">이 섹션에서는 ostress.exe 명령줄에 포함된 T-SQL 스크립트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="060cb-250">스크립트는 이전에 설치한 T-SQL 스크립트에 의해 생성된 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="060cb-251">다음 스크립트는 다음과 같은 메모리 액세스에 최적화된 *테이블*에 다섯 줄 항목의 샘플 판매 주문을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="060cb-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="060cb-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="060cb-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="060cb-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="060cb-254">ostress.exe용 이전 T-SQL 스크립트의 *_ondisk* 버전을 만들려면 *_inmem* 하위 문자열의 두 항목을 *_ondisk*로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="060cb-255">이렇게 대체하면 테이블의 이름 및 저장된 프로시저에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="060cb-256">RML 유틸리티 및 ostress 설치</span><span class="sxs-lookup"><span data-stu-id="060cb-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="060cb-257">이상적으로 Azure VM(가상 컴퓨터)에 ostress.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="060cb-258">AdventureWorksLT 데이터베이스가 있는 곳과 동일한 Azure 지리적 지역에 [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="060cb-259">하지만 대신 노트북에서 ostress.exe를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="060cb-260">VM 또는 선택한 호스트에서 RML(Replay Markup Language) 유틸리티를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="060cb-261">유틸리티는 ostress.exe를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="060cb-262">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-262">For more information, see:</span></span>
- <span data-ttu-id="060cb-263">[메모리 내 OLTP에 대한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)의 ostress.exe 설명</span><span class="sxs-lookup"><span data-stu-id="060cb-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="060cb-264">[메모리 내 OLTP에 대한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)</span><span class="sxs-lookup"><span data-stu-id="060cb-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="060cb-265">[ostress.exe 설치에 대한 블로그](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="060cb-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="060cb-266">먼저 *_inmem* 스트레스 워크로드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="060cb-267">*RML Cmd Prompt* 창을 사용하여 ostress.exe 명령줄을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="060cb-268">명령줄 매개 변수는 ostress에게 다음을 명령합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="060cb-269">동시에 100개의 연결(-n100)을 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="060cb-270">각 연결이 T-SQL 스크립트를 50회(-r50) 실행하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="060cb-271">위의 ostress.exe 명령줄을 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="060cb-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="060cb-272">이전 실행으로 삽입된 모든 데이터를 삭제하도록 SSMS에서 다음 명령을 실행하여 데이터베이스 데이터 콘텐츠를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="060cb-273">이전 ostress.exe 명령줄의 텍스트를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="060cb-274">매개 변수-S -U -P -d에 대한 `<placeholders>` 을(를) 올바른 실제 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="060cb-275">편집한 명령줄을 RML Cmd 창에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="060cb-276">결과는 기간입니다</span><span class="sxs-lookup"><span data-stu-id="060cb-276">Result is a duration</span></span>


<span data-ttu-id="060cb-277">ostress.exe가 완료되면 출력의 마지막 줄로 실행 기간을 RML Cmd 창에 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="060cb-278">예를 들어 짧은 테스트 실행은 약 1.5분 동안 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="060cb-279">*_ondisk*에 대해 다시 설정하고 편집한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="060cb-280">*_inmem* 실행에서 결과를 얻은 후 *_ondisk* 실행에 대해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="060cb-281">이전 실행으로 삽입된 모든 데이터를 삭제하도록 SSMS에서 다음 명령을 실행하여 데이터베이스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="060cb-282">ostress.exe 명령줄을 편집하여 모든 *_inmem*을 *_ondisk*로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="060cb-283">ostress.exe를 두 번째로 실행하고 기간 결과를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="060cb-284">많은 양의 테스트 데이터를 확실히 제거하기 위해 데이터베이스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="060cb-285">예상된 비교 결과</span><span class="sxs-lookup"><span data-stu-id="060cb-285">Expected comparison results</span></span>

<span data-ttu-id="060cb-286">데이터베이스와 동일한 Azure 지역의 Azure VM에서 ostress를 실행하여 이렇게 간단한 워크로드에 대한 메모리 내 테스트의 성능이 **9배**까지 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="060cb-287">2. 메모리 내 분석 샘플 설치</span><span class="sxs-lookup"><span data-stu-id="060cb-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="060cb-288">이 섹션에서는 columnstore 인덱스 및 전형적인 b-트리 인덱스를 사용하는 경우의 IO 및 통계 결과를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="060cb-289">OLTP 워크로드의 실시간 분석의 경우 비클러스터형 columnstore 인덱스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="060cb-290">자세한 내용은 [설명한 Columnstore 인덱스](http://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="060cb-291">columnstore 분석 테스트 준비</span><span class="sxs-lookup"><span data-stu-id="060cb-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="060cb-292">Azure Portal을 사용하여 샘플에서 새로운 AdventureWorksLT 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="060cb-293">정확한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-293">Use that exact name.</span></span>
 - <span data-ttu-id="060cb-294">Premium 서비스 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="060cb-295">[sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql)을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="060cb-296">T-SQL 스크립트는 1단계에서 만든 AdventureWorksLT 샘플 데이터베이스에서 필요한 메모리 내 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="060cb-297">스크립트는 차원 테이블과 두 개의 팩트 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="060cb-298">팩트 테이블은 각각 350만 개의 행으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="060cb-299">스크립트는 완료하는 데 15분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="060cb-300">SSMS에 T-SQL 스크립트를 붙여 넣고 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="060cb-301">다음과 같이 **CREATE INDEX** 문의 **COLUMNSTORE** 키워드가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="060cb-302">AdventureWorksLT를 호환성 수준 130으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="060cb-303">수준 130은 메모리 내 기능과 직접적으로 연관되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="060cb-304">하지만 수준 130은 일반적으로 120이 제공하는 것보다 빠른 쿼리 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="060cb-305">핵심 테이블 및 columnstore 인덱스</span><span class="sxs-lookup"><span data-stu-id="060cb-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="060cb-306">dbo.FactResellerSalesXL_CCI는 클러스터형 columnstore 인덱스를 포함하는 테이블이고, 여기에는 *데이터* 수준의 고급 압축이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="060cb-307">dbo.FactResellerSalesXL_PageCompressed는 동등한 일반 클러스터형 인덱스를 가지며 *페이지* 수준에서만 압축된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="060cb-308">columnstore 인덱스를 비교하는 핵심 쿼리</span><span class="sxs-lookup"><span data-stu-id="060cb-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="060cb-309">성능 향상을 확인하도록 [실행할 수 있는 여러 유형의 T-SQL 쿼리](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="060cb-310">T-SQL 스크립트의 2단계에서 이 쿼리 쌍에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="060cb-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="060cb-311">두 쿼리는 한 줄만 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="060cb-312">클러스터형 columnstore 인덱스는 FactResellerSalesXL\_CCI 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="060cb-313">다음 T-SQL 스크립트 발췌는 각 테이블의 쿼리에 대한 IO 및 TIME에 대한 통계를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="060cb-314">P2 가격 책정 계층의 데이터베이스에서 클러스터형 columnstore 인덱스를 사용하면 기존 인덱스와 비교하여 이 쿼리에 대해 약 9배의 성능 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="060cb-315">P15에서는 columnstore 인덱스를 사용하여 약 57배의 성능 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="060cb-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="060cb-316">Next steps</span></span>

- [<span data-ttu-id="060cb-317">빠른 시작 1: 더 빠른 T-SQL 성능을 위한 메모리 내 OLTP 기술</span><span class="sxs-lookup"><span data-stu-id="060cb-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="060cb-318">기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용</span><span class="sxs-lookup"><span data-stu-id="060cb-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="060cb-319">메모리 내 OLTP에 대한 [메모리 내 OLTP 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="060cb-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="060cb-320">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="060cb-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="060cb-321">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="060cb-321">Deeper information</span></span>

- [<span data-ttu-id="060cb-322">쿼럼이 SQL Database의 메모리 내 OLTP을 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="060cb-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="060cb-323">Azure SQL Database의 메모리 내 OLTP 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="060cb-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="060cb-324">메모리 내 OLTP에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="060cb-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="060cb-325">columnstore 인덱스에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="060cb-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="060cb-326">실시간 운영 성과 분석에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="060cb-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="060cb-327">[일반적인 워크로드 패턴 및 마이그레이션 고려 사항에 대한 백서](http://msdn.microsoft.com/library/dn673538.aspx)를 참조하세요. 여기에서 메모리 내 OLTP가 일반적으로 상당한 성능 향상을 제공하는 워크로드 패턴을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="060cb-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="060cb-328">응용 프로그램 설계</span><span class="sxs-lookup"><span data-stu-id="060cb-328">Application design</span></span>

- [<span data-ttu-id="060cb-329">메모리 내 OLTP(메모리 내 최적화)</span><span class="sxs-lookup"><span data-stu-id="060cb-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="060cb-330">기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용</span><span class="sxs-lookup"><span data-stu-id="060cb-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="060cb-331">도구</span><span class="sxs-lookup"><span data-stu-id="060cb-331">Tools</span></span>

- [<span data-ttu-id="060cb-332">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="060cb-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="060cb-333">SSMS(SQL Server Management Studio)</span><span class="sxs-lookup"><span data-stu-id="060cb-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="060cb-334">SSDT(SQL Server Data Tools)</span><span class="sxs-lookup"><span data-stu-id="060cb-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
