---
title: "aaaSync 데이터 (미리 보기) | Microsoft Docs"
description: "이 개요에서는 Azure SQL 데이터 동기화(미리 보기)를 소개합니다."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a><span data-ttu-id="185c2-103">SQL 데이터 동기화를 사용하여 여러 클라우드 및 온-프레미스 데이터베이스의 데이터 동기화</span><span class="sxs-lookup"><span data-stu-id="185c2-103">Sync data across multiple cloud and on-premises databases with SQL Data Sync</span></span>

<span data-ttu-id="185c2-104">SQL 데이터 동기화는 여러 SQL 데이터베이스 및 SQL Server 인스턴스 간에 양방향으로 선택 하는 hello 데이터를 동기화 할 수 있는 Azure SQL 데이터베이스는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-104">SQL Data Sync is a service built on Azure SQL Database that lets you synchronize hello data you select bi-directionally across multiple SQL databases and SQL Server instances.</span></span>

<span data-ttu-id="185c2-105">데이터 동기화가 기반 하 여 동기화 그룹의 hello 개념으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-105">Data Sync is based around hello concept of a Sync Group.</span></span> <span data-ttu-id="185c2-106">동기화 그룹은 toosynchronize 데이터베이스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-106">A Sync Group is a group of databases that you want toosynchronize.</span></span>

<span data-ttu-id="185c2-107">동기화 그룹에는 다음과 같은 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="185c2-107">A Sync Group has hello following properties:</span></span>

-   <span data-ttu-id="185c2-108">hello **동기화 스키마** 어떤 데이터를 동기화에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-108">hello **Sync Schema** describes which data is being synchronized.</span></span>

-   <span data-ttu-id="185c2-109">hello **동기화 방향** 양방향 수도 있고 한 방향 으로만 전달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-109">hello **Sync Direction** can be bi-directional or can flow in only one direction.</span></span> <span data-ttu-id="185c2-110">동기화 방향 수 hello 즉, *허브 tooMember* 또는 *멤버 tooHub*, 또는 둘 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-110">That is, hello Sync Direction can be *Hub tooMember* or *Member tooHub*, or both.</span></span>

-   <span data-ttu-id="185c2-111">hello **동기화 간격** 계획 하는 동기화가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-111">hello **Sync Interval** is how often synchronization occurs.</span></span>

-   <span data-ttu-id="185c2-112">hello **충돌 해결 정책** 될 수 있는 그룹 수준 정책이 *허브 wins* 또는 *멤버 wins*합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-112">hello **Conflict Resolution Policy** is a group level policy, which can be *Hub wins* or *Member wins*.</span></span>

<span data-ttu-id="185c2-113">데이터 동기화는 허브 및 스포크 토폴로지 toosynchronize 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-113">Data Sync uses a hub and spoke topology toosynchronize data.</span></span> <span data-ttu-id="185c2-114">Hello 데이터베이스 중 하나에서 정의한 hello 그룹 허브 데이터베이스 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-114">You define one of hello databases in hello group as hello Hub Database.</span></span> <span data-ttu-id="185c2-115">hello 데이터베이스 hello 나머지는 멤버 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-115">hello rest of hello databases are member databases.</span></span> <span data-ttu-id="185c2-116">동기화 허브 hello 및 개별 멤버 사이만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-116">Sync occurs only between hello Hub and individual members.</span></span>
-   <span data-ttu-id="185c2-117">hello **허브 데이터베이스** Azure SQL 데이터베이스 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-117">hello **Hub Database** must be an Azure SQL Database.</span></span>
-   <span data-ttu-id="185c2-118">hello **멤버 데이터베이스** SQL 데이터베이스, 온-프레미스 SQL Server 데이터베이스 또는 Azure 가상 컴퓨터에 SQL Server 인스턴스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-118">hello **member databases** can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances on Azure virtual machines.</span></span>
-   <span data-ttu-id="185c2-119">hello **동기화 데이터베이스** hello 메타 데이터 및 로그 포함 데이터 동기화. hello 동기화 데이터베이스에 toobe hello에 Azure SQL 데이터베이스에 대 한 hello 허브 데이터베이스와 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-119">hello **Sync Database** contains hello metadata and log for Data Sync. hello Sync Database has toobe an Azure SQL Database located in hello same region as hello Hub Database.</span></span> <span data-ttu-id="185c2-120">hello 동기화 데이터베이스 만든 고객 및 고객 소유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-120">hello Sync Database is customer created and customer owned.</span></span>

> [!NOTE]
> <span data-ttu-id="185c2-121">온-프레미스 데이터베이스를 사용 하는 경우 너무[로컬 에이전트를 구성 합니다.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span><span class="sxs-lookup"><span data-stu-id="185c2-121">If you're using an on premises database, you have too[configure a local agent.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span></span>

![데이터베이스 간 데이터 동기화](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a><span data-ttu-id="185c2-123">Toouse 데이터를 동기화 하는 경우</span><span class="sxs-lookup"><span data-stu-id="185c2-123">When toouse Data Sync</span></span>

<span data-ttu-id="185c2-124">데이터 동기화 데이터 toobe 여러 Azure SQL 데이터베이스 또는 SQL Server 데이터베이스에 걸쳐 toodate를 유지 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-124">Data Sync is useful in cases where data needs toobe kept up toodate across several Azure SQL Databases or SQL Server databases.</span></span> <span data-ttu-id="185c2-125">데이터 동기화에 대 한 hello 주요 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-125">Here are hello main use cases for Data Sync:</span></span>

-   <span data-ttu-id="185c2-126">**하이브리드 데이터 동기화:** 데이터 동기화 온-프레미스 데이터베이스와 Azure SQL 데이터베이스 tooenable 하이브리드 응용 프로그램 간에 동기화 된 데이터를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-126">**Hybrid Data Synchronization:** With Data Sync, you can keep data synchronized between your on-premises databases and Azure SQL Databases tooenable hybrid applications.</span></span> <span data-ttu-id="185c2-127">이 기능은 이동 toohello 클라우드를 고려 하는 고 tooput가 toocustomers 제기 될 수 있습니다 Azure에서 응용 프로그램의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-127">This capability may appeal toocustomers who are considering moving toohello cloud and would like tooput some of their application in Azure.</span></span>

-   <span data-ttu-id="185c2-128">**분산된 응용 프로그램:** 대부분의 경우 것이 유용한 tooseparate 다양 한 작업이 다른 데이터베이스에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-128">**Distributed Applications:** In many cases, it's beneficial tooseparate different workloads across different databases.</span></span> <span data-ttu-id="185c2-129">예를 들어 대형 프로덕션 데이터베이스 있는데 toorun 보고 또는 분석 워크 로드에이 데이터도 필요한 경우 유용한 toohave 이와 같은 추가 작업에 대 한 두 번째 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-129">For example, if you have a large production database, but you also need toorun a reporting or analytics workload on this data, it's helpful toohave a second database for this additional workload.</span></span> <span data-ttu-id="185c2-130">이 방법을 사용 하면 프로덕션 작업에 hello 성능에 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-130">This approach minimizes hello performance impact on your production workload.</span></span> <span data-ttu-id="185c2-131">데이터 동기화 tookeep이 두 데이터베이스 동기화를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-131">You can use Data Sync tookeep these two databases synchronized.</span></span>

-   <span data-ttu-id="185c2-132">**전역 분산 응용 프로그램:** 많은 비즈니스는 여러 지역 및 여러 국가 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-132">**Globally Distributed Applications:** Many businesses span several regions and even several countries.</span></span> <span data-ttu-id="185c2-133">데이터 영역에 닫습니다 최상의 toohave는 toominimize 네트워크 대기 시간, tooyou 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-133">toominimize network latency, it's best toohave your data in a region close tooyou.</span></span> <span data-ttu-id="185c2-134">데이터 동기화 동기화 hello 세계 지역에서 데이터베이스를 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-134">With Data Sync, you can easily keep databases in regions around hello world synchronized.</span></span>

<span data-ttu-id="185c2-135">다음 시나리오는 hello에 대 한 데이터 동기화 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-135">We don't recommend Data Sync for hello following scenarios:</span></span>

-   <span data-ttu-id="185c2-136">재해 복구</span><span class="sxs-lookup"><span data-stu-id="185c2-136">Disaster Recovery</span></span>

-   <span data-ttu-id="185c2-137">읽기 크기 조정</span><span class="sxs-lookup"><span data-stu-id="185c2-137">Read Scale</span></span>

-   <span data-ttu-id="185c2-138">ETL (OLTP tooOLAP)</span><span class="sxs-lookup"><span data-stu-id="185c2-138">ETL (OLTP tooOLAP)</span></span>

-   <span data-ttu-id="185c2-139">온-프레미스 SQL Server tooAzure SQL 데이터베이스에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="185c2-139">Migration from on-premises SQL Server tooAzure SQL Database</span></span>

## <a name="how-does-data-sync-work"></a><span data-ttu-id="185c2-140">데이터 동기화는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="185c2-140">How does Data Sync work?</span></span> 

-   <span data-ttu-id="185c2-141">**데이터 변경 내용 추적:** 데이터 동기화는 트리거 삽입, 업데이트 및 삭제를 사용하여 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-141">**Tracking data changes:** Data Sync tracks changes using insert, update, and delete triggers.</span></span> <span data-ttu-id="185c2-142">hello 변경 hello 사용자 데이터베이스에 추가 테이블에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-142">hello changes are recorded in a side table in hello user database.</span></span>

-   <span data-ttu-id="185c2-143">**데이터 동기화:** 데이터 동기화는 허브 및 스포크 모델에서 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-143">**Synchronizing data:** Data Sync is designed in a Hub and Spoke model.</span></span> <span data-ttu-id="185c2-144">hello 허브에서 동기화 각 멤버와 함께 개별적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-144">hello Hub syncs with each member individually.</span></span> <span data-ttu-id="185c2-145">Hello 허브에서에서 변경 내용을 다운로드 한 toohello 회원인과 다음 hello 멤버에서 변경 내용을 업로드 toohello 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-145">Changes from hello Hub are downloaded toohello member and then changes from hello member are uploaded toohello Hub.</span></span>

-   <span data-ttu-id="185c2-146">**충돌 해결:** 데이터 동기화는 충돌 해결을 위해 *허브 우선* 또는 *멤버 우선*이라는 두 가지 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-146">**Resolving conflicts:** Data Sync provides two options for conflict resolution, *Hub wins* or *Member wins*.</span></span>
    -   <span data-ttu-id="185c2-147">선택 하는 경우 *허브 wins*, hello 허브에 변경 내용을 hello hello 멤버의 변경 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-147">If you select *Hub wins*, hello changes in hello hub always overwrite changes in hello member.</span></span>
    -   <span data-ttu-id="185c2-148">선택 하는 경우 *멤버 wins*, hello hello 멤버 hello 허브에서 변경 내용 덮어쓰기 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-148">If you select *Member wins*, hello changes in hello member overwrite changes in hello hub.</span></span> <span data-ttu-id="185c2-149">둘 이상의 멤버가 경우 hello 최종 값 멤버는 먼저 동기화 파일에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-149">If there's more than one member, hello final value depends on which member syncs first.</span></span>

## <a name="limitations-and-considerations"></a><span data-ttu-id="185c2-150">제한 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="185c2-150">Limitations and considerations</span></span>

### <a name="performance-impact"></a><span data-ttu-id="185c2-151">성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="185c2-151">Performance impact</span></span>
<span data-ttu-id="185c2-152">데이터 동기화 사용 하 여 삽입, 업데이트 및 삭제 트리거 tootrack 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-152">Data Sync uses insert, update, and delete triggers tootrack changes.</span></span> <span data-ttu-id="185c2-153">변경 내용 추적에 대 한 hello 사용자 데이터베이스에 테이블 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-153">It creates side tables in hello user database for change tracking.</span></span> <span data-ttu-id="185c2-154">이러한 변경 내용 추적 작업은 데이터베이스 워크로드에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-154">These change tracking activities have an impact on your database workload.</span></span> <span data-ttu-id="185c2-155">서비스 계층을 평가하고 필요한 경우 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-155">Assess your service tier and upgrade if needed.</span></span>

### <a name="eventual-consistency"></a><span data-ttu-id="185c2-156">결과적 일관성</span><span class="sxs-lookup"><span data-stu-id="185c2-156">Eventual consistency</span></span>
<span data-ttu-id="185c2-157">데이터 동기화가 트리거 기반이기 때문에 트랜잭션 일관성이 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-157">Since Data Sync is trigger-based, transactional consistency is not guaranteed.</span></span> <span data-ttu-id="185c2-158">Microsoft는 결과적으로 모든 변경 내용을 적용하고 데이터 동기화가 데이터 손실을 발생하지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-158">Microsoft guarantees that all changes are made eventually and that Data Sync does not cause data loss.</span></span>

### <a name="unsupported-data-types"></a><span data-ttu-id="185c2-159">지원되지 않는 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="185c2-159">Unsupported data types</span></span>

-   <span data-ttu-id="185c2-160">FileStream</span><span class="sxs-lookup"><span data-stu-id="185c2-160">FileStream</span></span>

-   <span data-ttu-id="185c2-161">SQL/CLR UDT</span><span class="sxs-lookup"><span data-stu-id="185c2-161">SQL/CLR UDT</span></span>

-   <span data-ttu-id="185c2-162">XMLSchemaCollection(XML 지원)</span><span class="sxs-lookup"><span data-stu-id="185c2-162">XMLSchemaCollection (XML supported)</span></span>

-   <span data-ttu-id="185c2-163">Cursor, Timestamp, Hierarchyid</span><span class="sxs-lookup"><span data-stu-id="185c2-163">Cursor, Timestamp, Hierarchyid</span></span>

### <a name="requirements"></a><span data-ttu-id="185c2-164">요구 사항</span><span class="sxs-lookup"><span data-stu-id="185c2-164">Requirements</span></span>

-   <span data-ttu-id="185c2-165">각 표에는 기본 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-165">Each table must have a primary key.</span></span>

-   <span data-ttu-id="185c2-166">테이블 기본 키 hello 없는 id 열을 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-166">A table cannot have an identity column that is not hello primary key.</span></span>

-   <span data-ttu-id="185c2-167">개체 (데이터베이스, 테이블 및 열)의 hello 이름을 hello 인쇄 가능한 문자 마침표 (.), 왼쪽 대괄호 (), 포함 또는 오른쪽 대괄호 (]) 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-167">hello names of objects (databases, tables, and columns) cannot contain hello printable characters period (.), left square bracket ([), or right square bracket (]).</span></span>

### <a name="limitations-on-service-and-database-dimensions"></a><span data-ttu-id="185c2-168">서비스 및 데이터베이스 차원에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="185c2-168">Limitations on service and database dimensions</span></span>

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| <span data-ttu-id="185c2-169">**차원**</span><span class="sxs-lookup"><span data-stu-id="185c2-169">**Dimensions**</span></span>                                                      | <span data-ttu-id="185c2-170">**제한**</span><span class="sxs-lookup"><span data-stu-id="185c2-170">**Limit**</span></span>              | <span data-ttu-id="185c2-171">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="185c2-171">**Workaround**</span></span>              |
| <span data-ttu-id="185c2-172">데이터베이스가 속할 수 있는 동기화 그룹의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-172">Maximum number of sync groups any database can belong to.</span></span>       | <span data-ttu-id="185c2-173">5</span><span class="sxs-lookup"><span data-stu-id="185c2-173">5</span></span>                      |                             |
| <span data-ttu-id="185c2-174">단일 동기화 그룹에서 끝점의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-174">Maximum number of endpoints in a single sync group</span></span>              | <span data-ttu-id="185c2-175">30</span><span class="sxs-lookup"><span data-stu-id="185c2-175">30</span></span>                     | <span data-ttu-id="185c2-176">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="185c2-176">Create multiple sync groups</span></span> |
| <span data-ttu-id="185c2-177">단일 동기화 그룹에서 온-프레미스 끝점의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-177">Maximum number of on-premises endpoints in a single sync group.</span></span> | <span data-ttu-id="185c2-178">5</span><span class="sxs-lookup"><span data-stu-id="185c2-178">5</span></span>                      | <span data-ttu-id="185c2-179">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="185c2-179">Create multiple sync groups</span></span> |
| <span data-ttu-id="185c2-180">데이터베이스, 테이블, 스키마 및 열 이름</span><span class="sxs-lookup"><span data-stu-id="185c2-180">Database, table, schema, and column names</span></span>                       | <span data-ttu-id="185c2-181">이름당 50자</span><span class="sxs-lookup"><span data-stu-id="185c2-181">50 characters per name</span></span> |                             |
| <span data-ttu-id="185c2-182">동기화 그룹의 표</span><span class="sxs-lookup"><span data-stu-id="185c2-182">Tables in a sync group</span></span>                                          | <span data-ttu-id="185c2-183">500</span><span class="sxs-lookup"><span data-stu-id="185c2-183">500</span></span>                    | <span data-ttu-id="185c2-184">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="185c2-184">Create multiple sync groups</span></span> |
| <span data-ttu-id="185c2-185">동기화 그룹에서 표의 열</span><span class="sxs-lookup"><span data-stu-id="185c2-185">Columns in a table in a sync group</span></span>                              | <span data-ttu-id="185c2-186">1000</span><span class="sxs-lookup"><span data-stu-id="185c2-186">1000</span></span>                   |                             |
| <span data-ttu-id="185c2-187">표의 데이터 행 크기</span><span class="sxs-lookup"><span data-stu-id="185c2-187">Data row size on a table</span></span>                                        | <span data-ttu-id="185c2-188">24Mb</span><span class="sxs-lookup"><span data-stu-id="185c2-188">24 Mb</span></span>                  |                             |
| <span data-ttu-id="185c2-189">최소 동기화 간격</span><span class="sxs-lookup"><span data-stu-id="185c2-189">Minimum sync interval</span></span>                                           | <span data-ttu-id="185c2-190">5분</span><span class="sxs-lookup"><span data-stu-id="185c2-190">5 Minutes</span></span>              |                             |

## <a name="common-questions"></a><span data-ttu-id="185c2-191">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="185c2-191">Common questions</span></span>

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a><span data-ttu-id="185c2-192">데이터 동기화에서 데이터를 동기화하는 빈도는 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="185c2-192">How frequently can Data Sync synchronize my data?</span></span> 
<span data-ttu-id="185c2-193">hello 최소 빈도 5 분 마다입니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-193">hello minimum frequency is every five minutes.</span></span>

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a><span data-ttu-id="185c2-194">온-프레미스 데이터베이스에만 해당 SQL Server 간의 데이터 동기화 toosync를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="185c2-194">Can I use Data Sync toosync between SQL Server on-premises databases only?</span></span> 
<span data-ttu-id="185c2-195">직접 끌 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-195">Not directly.</span></span> <span data-ttu-id="185c2-196">하지만 동기화 할 수 있습니다 하지 온-프레미스 SQL Server 데이터베이스 간에 직접 Azure에서 허브 데이터베이스를 만들어 한 다음 hello 온-프레미스 데이터베이스 toohello 동기화 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-196">You can sync between SQL Server on-premises databases indirectly, however, by creating a Hub database in Azure, and then adding hello on-premises databases toohello sync group.</span></span>
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a><span data-ttu-id="185c2-197">내 프로덕션 데이터베이스 tooan 빈 데이터베이스에서 데이터 동기화 tooseed 데이터를 사용 하 여을 동기화 한 다음 할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="185c2-197">Can I use Data Sync tooseed data from my production database tooan empty database, and then keep them synchronized?</span></span> 
<span data-ttu-id="185c2-198">예.</span><span class="sxs-lookup"><span data-stu-id="185c2-198">Yes.</span></span> <span data-ttu-id="185c2-199">원래 hello에서 스크립팅 하 여 hello 새 데이터베이스에 수동으로 hello 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-199">Create hello schema manually in hello new database by scripting it from hello original.</span></span> <span data-ttu-id="185c2-200">Hello 스키마를 만든 후 hello 테이블 tooa 동기화 그룹 toocopy hello 데이터를 추가 하 고 동기화 된 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-200">After you create hello schema, add hello tables tooa sync group toocopy hello data and keep it synced.</span></span>

### <a name="why-do-i-see-tables-that-i-did-not-create"></a><span data-ttu-id="185c2-201">내가 만들지 않은 테이블이 표시되는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="185c2-201">Why do I see tables that I did not create?</span></span>  
<span data-ttu-id="185c2-202">데이터 동기화는 변경 내용 추적을 위해 데이터베이스에 추가 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-202">Data Sync creates side tables in your database for change tracking.</span></span> <span data-ttu-id="185c2-203">해당 테이블을 삭제하지 마세요. 삭제하면 데이터 동기화의 작동이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-203">Don't delete them or Data Sync stops working.</span></span>
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a><span data-ttu-id="185c2-204">라고 하는 오류 메시지가 수신 됨 "hello 열에 NULL hello 값을 삽입할 수 없습니다 \<열\>합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-204">I got an error message that said "cannot insert hello value NULL into hello column \<column\>.</span></span> <span data-ttu-id="185c2-205">열에는 Null을 사용할 수 없습니다."라는 오류 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-205">Column does not allow nulls."</span></span> <span data-ttu-id="185c2-206">그, 및 hello 오류 어떻게 해결할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="185c2-206">What does this mean, and how can I fix hello error?</span></span> 
<span data-ttu-id="185c2-207">이 오류 메시지는 hello 두 다음 문제 중 하나를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-207">This error message indicates one of hello two following issues:</span></span>
1.  <span data-ttu-id="185c2-208">기본 키가 없는 테이블이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-208">There may be a table without a primary key.</span></span> <span data-ttu-id="185c2-209">기본 키 tooall hello 테이블 추가 toofix이 문제를 동기화 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-209">toofix this issue, add a primary key tooall hello tables you're syncing.</span></span>
2.  <span data-ttu-id="185c2-210">CREATE INDEX 문에 WHERE 절이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-210">There may be a WHERE clause in your CREATE INDEX statement.</span></span> <span data-ttu-id="185c2-211">동기화에서는 이 조건이 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-211">Sync does not handle this condition.</span></span> <span data-ttu-id="185c2-212">toofix이이 문제를 hello WHERE 절을 제거 하거나 수동으로 변경할 hello tooall 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="185c2-212">toofix this issue, remove hello WHERE clause or manually make hello changes tooall databases.</span></span> 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a><span data-ttu-id="185c2-213">데이터 동기화에서는 어떻게 순환 참조가 처리되나요?</span><span class="sxs-lookup"><span data-stu-id="185c2-213">How does Data Sync handle circular references?</span></span> <span data-ttu-id="185c2-214">즉, hello 동일한 데이터를 여러 동기화 그룹 동기화 시점과 계속 결과적으로 변경?</span><span class="sxs-lookup"><span data-stu-id="185c2-214">That is, when hello same data is synced in multiple sync groups, and keeps changing as a result?</span></span>
<span data-ttu-id="185c2-215">데이터 동기화에서는 순환 참조가 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-215">Data Sync doesn’t handle circular references.</span></span> <span data-ttu-id="185c2-216">있는지 tooavoid 수 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-216">Be sure tooavoid them.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="185c2-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="185c2-217">Next steps</span></span>

<span data-ttu-id="185c2-218">SQL 데이터 동기화에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="185c2-218">For more info about SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="185c2-219">SQL 데이터 동기화 시작</span><span class="sxs-lookup"><span data-stu-id="185c2-219">Getting Started with SQL Data Sync</span></span>](sql-database-get-started-sql-data-sync.md)

-   <span data-ttu-id="185c2-220">완전 한 보여 주는 PowerShell 예제 tooconfigure SQL 데이터 동기화 방법:</span><span class="sxs-lookup"><span data-stu-id="185c2-220">Complete PowerShell examples that show how tooconfigure SQL Data Sync:</span></span>
    -   [<span data-ttu-id="185c2-221">여러 Azure SQL 데이터베이스 간에 toosync PowerShell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="185c2-221">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [<span data-ttu-id="185c2-222">Azure SQL 데이터베이스와 SQL Server 온-프레미스 데이터베이스 간의 toosync PowerShell을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="185c2-222">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [<span data-ttu-id="185c2-223">Hello 전체 SQL 데이터 동기화 기술 설명서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="185c2-223">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [<span data-ttu-id="185c2-224">Hello SQL 데이터 동기화 REST API 설명서 다운로드</span><span class="sxs-lookup"><span data-stu-id="185c2-224">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

<span data-ttu-id="185c2-225">SQL Database에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="185c2-225">For more info about SQL Database, see:</span></span>

-   [<span data-ttu-id="185c2-226">SQL 데이터베이스 개요</span><span class="sxs-lookup"><span data-stu-id="185c2-226">SQL Database Overview</span></span>](sql-database-technical-overview.md)

-   [<span data-ttu-id="185c2-227">데이터베이스 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="185c2-227">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
