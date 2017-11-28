---
title: "SQL 데이터베이스-메모리 내 기술 aaaAzure | Microsoft Docs"
description: "Azure SQL 데이터베이스-메모리 내 기술 hello 성능을 트랜잭션 및 분석 워크 로드에 크게 향상 시킬 합니다. 자세한 내용은 방법 tootake 이러한 기술 활용 합니다."
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
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="cce1e-104">SQL Database에서 메모리 내 기술을 사용하여 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="cce1e-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="cce1e-105">Azure SQL Database의 메모리 내 기술을 사용하여 트랜잭션(OLTP(온라인 트랜잭션 처리)), 분석(OLAP(온라인 분석 처리)), 혼합(HTAP(하이브리드 트랜잭션/분석 처리))과 같은 다양한 워크로드의 성능을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="cce1e-106">때문에 더 효율적인 쿼리 및 트랜잭션 처리 hello, 메모리 내 기술 수 있도록 도와 드릴 tooreduce 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="cce1e-107">일반적으로 가격 책정 계층 hello 데이터베이스 tooachieve 성능 향상의 tooupgrade hello가 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="cce1e-108">일부 경우에도 수 있습니다 hello 그래도 메모리 내 기술을 통한 성능 향상을 표시 하는 동안 가격 책정 계층을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="cce1e-109">다음은 메모리 내 OLTP toosignificantly 성능 향상을 작업 하는 방법의 두 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="cce1e-110">메모리 내 OLTP를 사용 하 여 [쿼럼 비즈니스 솔루션 70 %Dtu 개선 하는 동안 수 toodouble 프로그램 작업 했습니다](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="cce1e-111">여기서 DTU는 *데이터베이스 처리량 단위*를 의미하며 리소스 소비량의 측정값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="cce1e-112">hello 다음 비디오에서 보여 주는 샘플 작업과 리소스 소비량에서 향상: [Azure SQL 데이터베이스 비디오에서 메모리 내 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="cce1e-113">자세한 내용은 hello 블로그 게시물을 참조 하십시오.: [Azure SQL 데이터베이스 블로그 게시물에서 메모리 내 OLTP](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="cce1e-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="cce1e-114">메모리 내 기술 hello 프리미엄 계층에서는 프리미엄 탄력적 풀에서 데이터베이스를 비롯 한 모든 데이터베이스에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="cce1e-115">hello 다음 비디오에서는 설명 잠재적인 성능 향상 이점을 얻으려면 Azure SQL 데이터베이스의 메모리 내 기술 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="cce1e-116">항상 볼 수 있는 hello 성능 향상 hello 작업 부하 및 데이터를 hello 데이터베이스의 액세스 패턴의 hello 특성 등의 많은 요인에 따라 집니다 등에입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="cce1e-117">Azure SQL 데이터베이스의 메모리 내 기술 다음 hello 사용:</span><span class="sxs-lookup"><span data-stu-id="cce1e-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="cce1e-118">*메모리 내 OLTP*은 처리량을 증가시키고 트랜잭션 처리에 대한 대기 시간을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="cce1e-119">메모리 내 OLTP를 활용하는 시나리오는 거래와 게임, 이벤트 또는 IoT 장치의 데이터 수집, 캐싱, 데이터 부하 및 임시 테이블과 테이블 변수 시나리오와 같은 처리량 많은 트랜잭션을 처리하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="cce1e-120">*클러스터형 columnstore 인덱스* (too10 시간)을 사용 하면 저장소 공간을 줄이는 및 보고 및 분석 쿼리의 성능을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="cce1e-121">팩트 테이블을 데이터 마트 toofit에 더 많은 데이터에서에서 사용할 데이터베이스 수 있으며 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="cce1e-122">또한 운영 데이터베이스 tooarchive에서 기록 데이터와 사용할 수 있으며 too10 시간 수 tooquery 더 많은 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="cce1e-123">*비클러스터형 columnstore 인덱스* HTAP 도움말에 대 한 비용이 많이 드는 추출, 변환 및 로드 (ETL) 프로세스 hello 필요 toorun 하지 않고 직접 데이터베이스 있습니다 toogain 실시간으로 파악할 hello 작동 쿼리를 통해 비즈니스 및이 대기 에 대 한 데이터 웨어하우스 toobe hello 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="cce1e-124">비클러스터형 columnstore 인덱스는 hello 운영 워크 로드에 hello 미치는 영향을 줄이면서 hello OLTP 데이터베이스에서 분석 쿼리 실행 속도가 매우 빠르지만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="cce1e-125">Columnstore 인덱스가 있는 메모리 액세스에 최적화 된 테이블의 hello 조합을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="cce1e-126">이 조합 tooperform 매우 빠른 트랜잭션 처리, 수 및 너무*동시에* 실행된 분석 쿼리를 매우 신속 하 게 hello에 동일 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="cce1e-127">Columnstore 인덱스와 메모리 내 OLTP 일부일 hello SQL Server 제품의 2012 및 2014 년 이후 각각.</span><span class="sxs-lookup"><span data-stu-id="cce1e-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="cce1e-128">Azure SQL 데이터베이스 및 SQL Server 공유 hello 동일한 메모리 내 기술 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="cce1e-129">앞으로 이러한 기술에 대한 새로운 기능을 SQL Server에 배포하기 전에 Azure SQL Database에서 먼저 릴리스합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="cce1e-130">이 항목에 메모리 내 OLTP와 columnstore 인덱스를 특정 tooAzure SQL 데이터베이스의 측면에 설명 하 고 예제도 포함 되어:</span><span class="sxs-lookup"><span data-stu-id="cce1e-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="cce1e-131">저장소 및 데이터 크기 제한에 이러한 기술의 hello 영향을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="cce1e-132">Toomanage hello 다른 가격대 간의 이러한 기술을 사용 하는 데이터베이스의 이동을 hello 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="cce1e-133">메모리 내 OLTP와 Azure SQL 데이터베이스에서 columnstore 인덱스의 hello 사용을 보여 주는 두 개의 샘플이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="cce1e-134">Hello 리소스에 대 한 자세한 내용은 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1e-134">See hello following resources for more information.</span></span>

<span data-ttu-id="cce1e-135">Hello 기술에 대 한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="cce1e-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="cce1e-136">[메모리 내 OLTP 개요 및 사용 시나리오](https://msdn.microsoft.com/library/mt774593.aspx) (참조 toocustomer 사례 연구 및 시작 정보 tooget 포함)</span><span class="sxs-lookup"><span data-stu-id="cce1e-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="cce1e-137">메모리 내 OLTP에 대한 설명서</span><span class="sxs-lookup"><span data-stu-id="cce1e-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="cce1e-138">Columnstore 인덱스 가이드</span><span class="sxs-lookup"><span data-stu-id="cce1e-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="cce1e-139">HTAP(하이브리드 트랜잭션/분석 처리) 즉, [실시간 운영 분석](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="cce1e-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="cce1e-140">메모리 내 oltp는 빠른 입문: [빠른 시작 1: 더 빠르게 T-SQL 성능을 위한 메모리 내 OLTP 기술](http://msdn.microsoft.com/library/mt694156.aspx) (다른 문서 toohelp 시작 하는 데)</span><span class="sxs-lookup"><span data-stu-id="cce1e-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="cce1e-141">Hello 기술에 대 한 심층 분석 비디오:</span><span class="sxs-lookup"><span data-stu-id="cce1e-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="cce1e-142">[Azure SQL 데이터베이스에서 메모리 내 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (성능의 데모 포함 된 이점 및 단계 tooreproduce 이러한 결과 사용자가 직접)</span><span class="sxs-lookup"><span data-stu-id="cce1e-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="cce1e-143">메모리 내 OLTP 비디오: 무엇 인지 및/하는 경우 어떻게 toouse 것</span><span class="sxs-lookup"><span data-stu-id="cce1e-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="cce1e-144">Columnstore 인덱스: Ignite 2016의 메모리 내 분석 비디오</span><span class="sxs-lookup"><span data-stu-id="cce1e-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="cce1e-145">저장소 및 데이터 크기</span><span class="sxs-lookup"><span data-stu-id="cce1e-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="cce1e-146">메모리 내 OLTP의 데이터 크기 및 저장 제한</span><span class="sxs-lookup"><span data-stu-id="cce1e-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="cce1e-147">메모리 내 OLTP는 사용자 데이터를 저장하는 데 사용되는 메모리에 최적화된 테이블을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="cce1e-148">이러한 테이블은 메모리에 필요한 toofit입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="cce1e-149">메모리 hello SQL 데이터베이스 서비스에서 직접 관리 하기 때문에 사용자 데이터에 대 한 할당량의 hello 개념을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="cce1e-150">이 개념은 참조 tooas *메모리 내 OLTP 저장소*합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="cce1e-151">지원되는 독립 실행형 데이터베이스 가격 책정 계층 및 탄력적 풀 가격 책정 계층은 각각 일정량의 메모리 내 OLTP 저장소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="cce1e-152">작성 hello 시 얻게 저장소는 기가바이트 모든 125 개의 데이터베이스 트랜잭션 단위 (DTUs) 또는 탄력적 데이터베이스에 대해 트랜잭션 Edtu (단위).</span><span class="sxs-lookup"><span data-stu-id="cce1e-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="cce1e-153">hello [SQL 데이터베이스 서비스 계층](sql-database-service-tiers.md) 기술 자료 문서에 지원 되는 각 독립 실행형 데이터베이스 및 가격 책정 계층 탄력적 풀에 사용할 수 있는 hello 메모리 내 OLTP 저장소의 hello 공식 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="cce1e-154">메모리 내 OLTP 저장소 캡을 향해 항목 수가 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="cce1e-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="cce1e-155">메모리 최적화된 테이블 및 테이블 변수의 활성 사용자 데이터 행입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="cce1e-156">오래 된 행 버전 hello 캡을 차지 하지 않습니다는 참고 사항</span><span class="sxs-lookup"><span data-stu-id="cce1e-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="cce1e-157">메모리 최적화된 테이블에 대한 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="cce1e-158">ALTER TABLE 작업의 작업 오버헤드입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="cce1e-159">Hello cap 발생 하면 할당량 초과 오류를 표시 하 고 수 tooinsert 또는 update 데이터는 더 이상.</span><span class="sxs-lookup"><span data-stu-id="cce1e-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="cce1e-160">toomitigate이이 오류 데이터를 삭제 하거나 hello 가격 책정 계층 hello 데이터베이스 또는 풀을 늘리십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1e-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="cce1e-161">메모리 내 OLTP 저장소 사용을 모니터링 하 고 hello 단면에 거의 도달 하면 경고를 구성 하는 방법에 대 한 세부 정보를 참조 하십시오. [모니터에서 메모리 내 저장소](sql-database-in-memory-oltp-monitoring.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="cce1e-162">탄력적 풀에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="cce1e-162">About elastic pools</span></span>

<span data-ttu-id="cce1e-163">탄력적 풀과 메모리 내 OLTP 저장소 hello hello 풀의 모든 데이터베이스에서 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="cce1e-164">따라서 한 데이터베이스의 hello 사용 다른 데이터베이스에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="cce1e-165">두 가지 해결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="cce1e-166">최대-eDTU 데이터베이스에 대 한 전체 hello 풀에 대 한 hello eDTU 수 보다 낮은 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="cce1e-167">이 최대 풀 hello toohello eDTU 수입니다. 해당 하는 toohello 크기에에서 모든 데이터베이스에서 hello 메모리 내 OLTP 저장소 사용률, 대문자입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="cce1e-168">최소 eDTU를 0보다 크게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="cce1e-169">이 최소 보장 hello toohello 해당 하는 사용 가능한 메모리 내 OLTP 저장소 양을 hello 풀의 각 데이터베이스에 최소 eDTU를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="cce1e-170">columnstore 인덱스의 데이터 크기 및 저장소</span><span class="sxs-lookup"><span data-stu-id="cce1e-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="cce1e-171">Columnstore 인덱스는 메모리에 필요한 toofit 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="cce1e-172">따라서 hello 인덱스의 hello 크기는 hello에 설명 되어 있는 hello 최대 전체 데이터베이스 크기에만 hello [SQL 데이터베이스 서비스 계층](sql-database-service-tiers.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="cce1e-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="cce1e-173">클러스터형된 columnstore 인덱스를 사용할 때는 칼럼 형식 압축 hello 기본 테이블 저장소에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="cce1e-174">이러한 압축 hello 데이터베이스에 더 많은 데이터를 표시할 수 있습니다는 사용자 데이터의 hello 저장소 공간을 상당히 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="cce1e-175">Hello 압축으로 더 높아질 수 있습니다 및 [보관 칼럼 형식 압축](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="cce1e-176">hello 압축량 얻을 수 있는 hello 데이터의 hello 특성에 따라 달라 집니다 하지만 10 번 hello 압축도 드물지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="cce1e-177">예를 들어 최대 크기인 1tb (테라바이트)를 사용 하 여 데이터베이스 있고 columnstore 인덱스를 사용 하 여 10 회 hello 압축을 얻을 경우 hello 데이터베이스의 10TB의 사용자 데이터의 합계를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="cce1e-178">비클러스터형 columnstore 인덱스를 사용할 때는 hello 기본 테이블은 여전히 hello 일반적인 행 저장소 형식으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="cce1e-179">따라서 hello 저장소 분량이 절약 크기가 클러스터형된 columnstore 인덱스와 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="cce1e-180">그러나 기존의 비클러스터형 인덱스의 수를 단일 columnstore 인덱스로 대체 하는 경우에 여전히 hello 테이블에 대 한 hello 저장소 공간에는 전반적인 절감을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="cce1e-181">가격 책정 계층 간의 메모리 내 기술을 사용하여 데이터베이스 이동</span><span class="sxs-lookup"><span data-stu-id="cce1e-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="cce1e-182">존재 하지 않습니다 비 호환성 문제 또는 기타 문제 tooa 더 높은 가격 책정 계층을와 같은 표준 tooPremium에서 업그레이드 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="cce1e-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="cce1e-183">hello 사용할 수 있는 기능 및 리소스만 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="cce1e-184">하지만 가격 책정 계층으로 다운 그레이드 hello 데이터베이스 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="cce1e-185">hello 영향 때 특히 tooStandard Premium에서에서 다운 그레이드 하면 명백한 또는 기본 데이터베이스에 메모리 내 OLTP 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="cce1e-186">메모리 액세스에 최적화 된 테이블 및 columnstore 인덱스를 사용할 수 없는 hello 다운 그레이드 한 후 (경우에 계속 표시)입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="cce1e-187">hello hello 가격 책정 계층 탄력적 풀의 또는 데이터베이스 이동 In-memory 기술과 함께 사용 하는 표준 또는 기본 탄력적인 풀을 낮추면 하는 경우 동일한 고려 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="cce1e-188">메모리 내 OLTP</span><span class="sxs-lookup"><span data-stu-id="cce1e-188">In-Memory OLTP</span></span>

<span data-ttu-id="cce1e-189">*TooBasic/표준 다운 그레이드*: 메모리 내 OLTP는 hello Standard 또는 Basic 계층에 있는 데이터베이스에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="cce1e-190">또한 가능한 toomove 모든 메모리 내 OLTP 개체 toohello Standard 또는 Basic 계층에 있는 데이터베이스는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="cce1e-191">Hello 데이터베이스 tooStandard/Basic를 다운 그레이드 하기 전에 모든 메모리 액세스에 최적화 된 테이블 및 테이블 형식 뿐 아니라 모든 고유 하 게 컴파일된 T-SQL 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="cce1e-192">지정된 된 데이터베이스는 메모리 내 OLTP를 지원 하는지 여부를 프로그래밍 방식으로 toounderstand가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="cce1e-193">Hello 다음 TRANSACT-SQL 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="cce1e-194">Hello 쿼리가 반환 하는 경우 **1**은이 데이터베이스에서 메모리 내 OLTP를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="cce1e-195">*Tooa 낮은 Premium 계층을 다운 그레이드*: 가격 책정 계층 hello 데이터베이스의 hello와 관련 된 또는 hello 탄력적 풀에서 사용할 수 있는 hello 메모리 내 OLTP 저장소 안에 메모리 액세스에 최적화 된 테이블의 데이터에에서 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="cce1e-196">가격 책정 계층 toolower hello를 시도 하거나 hello 데이터베이스를 이동 하는 경우 사용할 수 있는 충분 한 메모리 내 OLTP 저장소 풀에 없는, hello 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="cce1e-197">Columnstore 인덱스</span><span class="sxs-lookup"><span data-stu-id="cce1e-197">Columnstore indexes</span></span>

<span data-ttu-id="cce1e-198">*TooBasic 또는 표준 다운 그레이드*: Standard 또는 Basic 계층을 hello Columnstore 인덱스는 고 아닌 hello 프리미엄 가격 책정 계층 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="cce1e-199">데이터베이스 tooStandard 또는 Basic를 다운 그레이드 하면 columnstore 인덱스가 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="cce1e-200">hello 시스템 columnstore 인덱스를 유지 하지만 hello 인덱스를 활용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="cce1e-201">나중에 다시 tooPremium으로 업그레이드할 경우 columnstore 인덱스는 즉시 toobe 다시 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="cce1e-202">있는 경우는 **클러스터 된** columnstore 인덱스 계층 다운 그레이드 한 후 hello 전체 테이블 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="cce1e-203">모든 삭제 권장 따라서 *클러스터형* hello Premium 계층 아래 데이터베이스를 다운 그레이드 하기 전에 columnstore 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="cce1e-204">*Tooa 낮은 Premium 계층을 다운 그레이드*: hello 전체 데이터베이스 또는 hello hello 탄력적 풀에서 사용 가능한 저장소 가격 책정 계층을 hello 대상에 대 한 hello 최대 데이터베이스 크기 내에 포함 되 면이 다운 그레이드 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="cce1e-205">Hello columnstore 인덱스에서 특정 영향은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="cce1e-206">1. Hello 메모리 내 OLTP 예제 설치</span><span class="sxs-lookup"><span data-stu-id="cce1e-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="cce1e-207">Hello에 몇 번의 클릭 hello AdventureWorksLT 샘플 데이터베이스를 만들 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="cce1e-208">그런 다음 hello이 섹션의 단계에 설명 AdventureWorksLT 데이터베이스를 메모리 내 OLTP 개체와 보강 성능 이점을 설명 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="cce1e-209">메모리 내 OLTP의 경우 더 간단하지만 시각적으로 뛰어난 성능 데모는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cce1e-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="cce1e-210">릴리스: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="cce1e-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="cce1e-211">소스 코드: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="cce1e-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="cce1e-212">설치 단계</span><span class="sxs-lookup"><span data-stu-id="cce1e-212">Installation steps</span></span>

1. <span data-ttu-id="cce1e-213">Hello에 [Azure 포털](https://portal.azure.com/)를 서버에 Premium 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="cce1e-214">집합 hello **소스** toohello AdventureWorksLT 샘플 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="cce1e-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="cce1e-215">자세한 지침은 [첫 번째 Azure SQL Database 만들기](sql-database-get-started-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cce1e-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="cce1e-216">SQL Server Management Studio를 사용 하 여 toohello 데이터베이스 연결 [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="cce1e-217">복사 hello [메모리 내 OLTP Transact SQL 스크립트](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="cce1e-218">T-SQL 스크립트 hello 1 단계에서 만든 hello AdventureWorksLT 샘플 데이터베이스의 hello 메모리에 필요한 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="cce1e-219">SSMS에 hello T-SQL 스크립트를 붙여 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="cce1e-220">hello `MEMORY_OPTIMIZED = ON` 절 CREATE TABLE 문에는 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="cce1e-221">예:</span><span class="sxs-lookup"><span data-stu-id="cce1e-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="cce1e-222">오류 40536</span><span class="sxs-lookup"><span data-stu-id="cce1e-222">Error 40536</span></span>


<span data-ttu-id="cce1e-223">Hello T-SQL 스크립트를 실행할 때 40536 오류가 발생할 경우 hello hello 데이터베이스에서 메모리를 지원 하는지 여부를 T-SQL 스크립트 tooverify 다음를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="cce1e-224">**0**이라는 결과는 메모리 내가 지원되지 않음을 나타내고 **1**은 지원됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="cce1e-225">toodiagnose hello 문제 hello Premium 서비스 계층에서 해당 hello 데이터베이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="cce1e-226">메모리 액세스에 최적화 된 항목을 만든 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="cce1e-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="cce1e-227">**테이블**: hello 샘플 hello 다음 메모리 액세스에 최적화 된 테이블에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="cce1e-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="cce1e-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="cce1e-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="cce1e-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="cce1e-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="cce1e-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="cce1e-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="cce1e-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="cce1e-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="cce1e-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="cce1e-233">Hello 통해 메모리 액세스에 최적화 된 테이블을 검사할 수 **개체 탐색기** SSMS에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="cce1e-234">**테이블** > **필터** > **필터 설정** > **메모리 액세스에 최적화됨**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="cce1e-235">hello 값 1을 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-235">hello value equals 1.</span></span>


<span data-ttu-id="cce1e-236">또는 같은 hello 카탈로그 뷰를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="cce1e-237">**고유하게 컴파일된 저장 프로시저**: 카탈로그 뷰 쿼리를 통해 SalesLT.usp_InsertSalesOrder_inmem을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="cce1e-238">Hello 샘플 OLTP 워크 로드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="cce1e-239">다음 두 개의 hello 간의 차이 hello *저장 프로시저* hello 테이블의 메모리 액세스에 최적화 된 버전을 사용 하 여 hello 첫 번째 프로시저, hello 하는 동안 두 번째 절차는 hello 일반 디스크에 테이블 사용:</span><span class="sxs-lookup"><span data-stu-id="cce1e-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="cce1e-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="cce1e-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="cce1e-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="cce1e-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="cce1e-242">이 섹션에서는 toouse hello 편리한 방법을 표시 **ostress.exe** 유틸리티 tooexecute hello 스트레스가 수준에서 두 개의 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="cce1e-243">Hello 두 스트레스 실행 toofinish에 걸리는 시간을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="cce1e-244">Ostress.exe를 실행 하면 hello 다음 둘 다에 대해 설계 된 매개 변수 값을 전달 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="cce1e-245">-n100을 사용하여 많은 수의 동시 연결을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="cce1e-246">-r500을 사용하여 각 연결 루프를 수백 번 가집니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="cce1e-247">그러나 모든 기능이 작동 하는 n10 및-r50 tooensure 같은 값이 훨씬 작은 toostart를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="cce1e-248">ostress.exe에 대한 스크립트</span><span class="sxs-lookup"><span data-stu-id="cce1e-248">Script for ostress.exe</span></span>


<span data-ttu-id="cce1e-249">이 섹션은 우리의 ostress.exe 명령줄에 포함 된 hello T-SQL 스크립트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="cce1e-250">hello 스크립트 hello 이전에 설치 하는 T-SQL 스크립트에서 생성 된 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="cce1e-251">hello 다음 스크립트는 샘플에 판매 주문을 삽입 품목이 5 개인 메모리 액세스에 최적화 된 hello 다음 *테이블*:</span><span class="sxs-lookup"><span data-stu-id="cce1e-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="cce1e-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="cce1e-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="cce1e-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="cce1e-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="cce1e-254">toomake hello *_ondisk* 버전의 hello ostress.exe에 대 한 이전 T-SQL 스크립트, hello의 두 항목 바꿨을 것 *_inmem* 와 substring *_ondisk*합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="cce1e-255">이러한 대체 hello 이름을 테이블 및 저장된 프로시저의 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="cce1e-256">RML 유틸리티 및 ostress 설치</span><span class="sxs-lookup"><span data-stu-id="cce1e-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="cce1e-257">이상적으로 Azure 가상 컴퓨터 (VM)에서 toorun ostress.exe를 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="cce1e-258">만듭니다는 [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello에 동일한 Azure 지역 AdventureWorksLT 데이터베이스가 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="cce1e-259">하지만 대신 노트북에서 ostress.exe를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="cce1e-260">Hello, VM 또는 호스트 무엇이 든 선택 hello 재생 Markup Language (RML) 유틸리티를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="cce1e-261">hello 유틸리티 ostress.exe를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="cce1e-262">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cce1e-262">For more information, see:</span></span>
- <span data-ttu-id="cce1e-263">ostress.exe 토론 hello [메모리 내 OLTP에 대 한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="cce1e-264">[메모리 내 OLTP에 대한 샘플 데이터베이스](http://msdn.microsoft.com/library/mt465764.aspx)</span><span class="sxs-lookup"><span data-stu-id="cce1e-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="cce1e-265">hello [ostress.exe를 설치 하기 위한 블로그](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="cce1e-266">Hello 실행 *_inmem* 작업 부하를 먼저 스트레스</span><span class="sxs-lookup"><span data-stu-id="cce1e-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="cce1e-267">사용할 수는 *RML Cmd Prompt* 창 toorun ostress.exe 명령줄 취급 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="cce1e-268">hello 명령줄 매개 변수를 ostress 직접:</span><span class="sxs-lookup"><span data-stu-id="cce1e-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="cce1e-269">동시에 100개의 연결(-n100)을 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="cce1e-270">50 회 hello T-SQL 스크립트를 실행 하는 각 연결 (-r50).</span><span class="sxs-lookup"><span data-stu-id="cce1e-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="cce1e-271">앞에 ostress.exe 명령줄 toorun hello:</span><span class="sxs-lookup"><span data-stu-id="cce1e-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="cce1e-272">모든 이전 실행 하 여 삽입 된 모든 hello 데이터 hello 다음 toodelete SSMS에서 명령을 실행 하 여 hello 데이터베이스 데이터 콘텐츠를 다시 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1e-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="cce1e-273">Hello ostress.exe 명령줄 tooyour 클립보드 앞의 hello 텍스트를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="cce1e-274">Hello 대체 `<placeholders>` hello 매개 변수-S-U-P-d hello로에 대 한 실제 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="cce1e-275">편집한 명령줄을 RML Cmd 창에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="cce1e-276">결과는 기간입니다</span><span class="sxs-lookup"><span data-stu-id="cce1e-276">Result is a duration</span></span>


<span data-ttu-id="cce1e-277">Ostress.exe 완료 되 면 실행 지속 시간 hello RML Cmd 창에서 출력의 마지막 줄으로 된 hello를 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="cce1e-278">예를 들어 짧은 테스트 실행은 약 1.5분 동안 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="cce1e-279">*_ondisk*에 대해 다시 설정하고 편집한 다음 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="cce1e-280">Hello hello 결과 구성한 후 *_inmem* 실행 hello hello에 대 한 단계를 수행 하십시오 *_ondisk* 실행:</span><span class="sxs-lookup"><span data-stu-id="cce1e-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="cce1e-281">Hello 이전을 실행 하 여 삽입 된 모든 hello 데이터 hello 다음 SSMS toodelete에서 명령을 실행 하 여 hello 데이터베이스를 다시 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1e-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="cce1e-282">Hello ostress.exe 명령줄 tooreplace 모든 편집 *_inmem* 와 *_ondisk*합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="cce1e-283">Hello에 대 한 ostress.exe를 두 번째로 다시 실행 하 고 hello 기간 결과 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1e-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="cce1e-284">다시 (삭제에 대 한 책임감 있게 많은 양의 테스트 데이터를 지정할 수 있는 대상) hello 데이터베이스를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="cce1e-285">예상된 비교 결과</span><span class="sxs-lookup"><span data-stu-id="cce1e-285">Expected comparison results</span></span>

<span data-ttu-id="cce1e-286">메모리에이 테스트 해당 성능 향상을 이루었습니다 **9 번** 이 단순한 작업에 대 한 ostress와의 Azure VM에서 실행 중인 hello 동일 hello 데이터베이스와 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="cce1e-287">2. Hello 메모리 내 분석 샘플을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="cce1e-288">이 섹션에서는 기존의 b-트리 인덱스와 columnstore 인덱스를 사용할 때 있습니다 hello IO 및 통계 결과 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="cce1e-289">OLTP 워크 로드에서 실시간 분석에 대 한 것이 가장 좋은 toouse 비클러스터형 columnstore 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="cce1e-290">자세한 내용은 [설명한 Columnstore 인덱스](http://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cce1e-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="cce1e-291">Hello columnstore 분석 테스트 준비</span><span class="sxs-lookup"><span data-stu-id="cce1e-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="cce1e-292">Azure 포털 toocreate hello 샘플에 포함 하 여 새 AdventureWorksLT 데이터베이스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="cce1e-293">정확한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-293">Use that exact name.</span></span>
 - <span data-ttu-id="cce1e-294">Premium 서비스 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="cce1e-295">복사 hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour 클립보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="cce1e-296">T-SQL 스크립트 hello 1 단계에서 만든 hello AdventureWorksLT 샘플 데이터베이스의 hello 메모리에 필요한 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="cce1e-297">hello 스크립트 hello 차원 테이블 두 개와 팩트 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="cce1e-298">hello 팩트 테이블은 각각 3.5 백만 행으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="cce1e-299">hello 스크립트 toocomplete 15 분 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="cce1e-300">SSMS에 hello T-SQL 스크립트를 붙여 하 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="cce1e-301">hello **COLUMNSTORE** hello 키워드 **CREATE INDEX** 문에에서 같이 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="cce1e-302">AdventureWorksLT toocompatibility 수준 130을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="cce1e-303">수준 130 직접적인 관련된은 tooIn 메모리 내 기능 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="cce1e-304">하지만 수준 130은 일반적으로 120이 제공하는 것보다 빠른 쿼리 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="cce1e-305">핵심 테이블 및 columnstore 인덱스</span><span class="sxs-lookup"><span data-stu-id="cce1e-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="cce1e-306">dbo입니다. 에서는 고급 hello에 압축 클러스터형된 columnstore 인덱스를 가진 테이블인 FactResellerSalesXL_CCI *데이터* 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="cce1e-307">dbo입니다. FactResellerSalesXL_PageCompressed는 해당 하는 일반 클러스터형된 인덱스는 hello에만 압축 된 테이블은 *페이지* 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="cce1e-308">키는 toocompare hello columnstore 인덱스를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="cce1e-309">[실행할 수 있는 여러 T-SQL 쿼리 형식이](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee 성능 향상.</span><span class="sxs-lookup"><span data-stu-id="cce1e-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="cce1e-310">Hello T-SQL 스크립트의에서 2 단계에서 주의 기울여야 toothis 쌍 쿼리 비용을 지불 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="cce1e-311">두 쿼리는 한 줄만 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="cce1e-312">클러스터형된 columnstore 인덱스는 hello FactResellerSalesXL에에서\_CCI 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="cce1e-313">hello T-SQL 스크립트 발췌 한 다음 통계에 대 한 인쇄 IO와 각 테이블의 hello 쿼리에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
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


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
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

<span data-ttu-id="cce1e-314">Hello P2 가격 책정 계층을 사용 하 여 데이터베이스를 hello 기존 인덱스와 비교 하는 hello 클러스터형된 columnstore 인덱스를 사용 하 여이 쿼리에 대 한 약 9 번 hello 성능 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="cce1e-315">P15와 hello columnstore 인덱스를 사용 하 여 57 배 정도 hello 성능 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cce1e-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cce1e-316">Next steps</span></span>

- [<span data-ttu-id="cce1e-317">빠른 시작 1: 더 빠른 T-SQL 성능을 위한 메모리 내 OLTP 기술</span><span class="sxs-lookup"><span data-stu-id="cce1e-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="cce1e-318">기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용</span><span class="sxs-lookup"><span data-stu-id="cce1e-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="cce1e-319">메모리 내 OLTP에 대한 [메모리 내 OLTP 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="cce1e-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cce1e-320">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="cce1e-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="cce1e-321">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="cce1e-321">Deeper information</span></span>

- [<span data-ttu-id="cce1e-322">쿼럼이 SQL Database의 메모리 내 OLTP을 사용하여 DTU를 70% 줄이는 동시에 키 데이터베이스의 워크로드를 두 배로 증가시키는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="cce1e-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="cce1e-323">Azure SQL Database의 메모리 내 OLTP 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="cce1e-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="cce1e-324">메모리 내 OLTP에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="cce1e-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="cce1e-325">columnstore 인덱스에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="cce1e-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="cce1e-326">실시간 운영 성과 분석에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="cce1e-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="cce1e-327">[일반적인 워크로드 패턴 및 마이그레이션 고려 사항에 대한 백서](http://msdn.microsoft.com/library/dn673538.aspx)를 참조하세요. 여기에서 메모리 내 OLTP가 일반적으로 상당한 성능 향상을 제공하는 워크로드 패턴을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1e-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="cce1e-328">응용 프로그램 설계</span><span class="sxs-lookup"><span data-stu-id="cce1e-328">Application design</span></span>

- [<span data-ttu-id="cce1e-329">메모리 내 OLTP(메모리 내 최적화)</span><span class="sxs-lookup"><span data-stu-id="cce1e-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="cce1e-330">기존 Azure SQL 응용 프로그램에서 메모리 내 OLTP 사용</span><span class="sxs-lookup"><span data-stu-id="cce1e-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="cce1e-331">도구</span><span class="sxs-lookup"><span data-stu-id="cce1e-331">Tools</span></span>

- [<span data-ttu-id="cce1e-332">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cce1e-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="cce1e-333">SSMS(SQL Server Management Studio)</span><span class="sxs-lookup"><span data-stu-id="cce1e-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="cce1e-334">SSDT(SQL Server Data Tools)</span><span class="sxs-lookup"><span data-stu-id="cce1e-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
