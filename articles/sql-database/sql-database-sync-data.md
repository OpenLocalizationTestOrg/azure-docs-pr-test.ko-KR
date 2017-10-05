---
title: "데이터 동기화(미리 보기) | Microsoft Docs"
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
ms.openlocfilehash: 926938a8ed20167e1f17a9883007cd993897f14a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a><span data-ttu-id="e3142-103">SQL 데이터 동기화를 사용하여 여러 클라우드 및 온-프레미스 데이터베이스의 데이터 동기화</span><span class="sxs-lookup"><span data-stu-id="e3142-103">Sync data across multiple cloud and on-premises databases with SQL Data Sync</span></span>

<span data-ttu-id="e3142-104">SQL 데이터 동기화는 여러 SQL Database 및 SQL Server 인스턴스 간에 양방향으로 선택한 데이터를 동기화할 수 있는 Azure SQL Database에 기반한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-104">SQL Data Sync is a service built on Azure SQL Database that lets you synchronize the data you select bi-directionally across multiple SQL databases and SQL Server instances.</span></span>

<span data-ttu-id="e3142-105">데이터 동기화는 동기화 그룹의 개념에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-105">Data Sync is based around the concept of a Sync Group.</span></span> <span data-ttu-id="e3142-106">동기화 그룹은 동기화하려는 데이터베이스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-106">A Sync Group is a group of databases that you want to synchronize.</span></span>

<span data-ttu-id="e3142-107">동기화 그룹의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-107">A Sync Group has the following properties:</span></span>

-   <span data-ttu-id="e3142-108">**동기화 스키마**는 동기화할 데이터에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-108">The **Sync Schema** describes which data is being synchronized.</span></span>

-   <span data-ttu-id="e3142-109">**동기화 방향**은 양방향일 수도 있고 한 방향으로만 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-109">The **Sync Direction** can be bi-directional or can flow in only one direction.</span></span> <span data-ttu-id="e3142-110">즉, 동기화 방향은 *허브에서 구성원*이거나 *구성원에게서 허브* 또는 양쪽 모두일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-110">That is, the Sync Direction can be *Hub to Member* or *Member to Hub*, or both.</span></span>

-   <span data-ttu-id="e3142-111">**동기화 간격**은 동기화가 발생하는 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-111">The **Sync Interval** is how often synchronization occurs.</span></span>

-   <span data-ttu-id="e3142-112">**충돌 해결 정책**은 그룹 수준 정책으로 *허브 우선*일 수도 있고 *구성원 우선*일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-112">The **Conflict Resolution Policy** is a group level policy, which can be *Hub wins* or *Member wins*.</span></span>

<span data-ttu-id="e3142-113">데이터 동기화는 허브 및 스포크 토폴로지를 사용하여 데이터를 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-113">Data Sync uses a hub and spoke topology to synchronize data.</span></span> <span data-ttu-id="e3142-114">그룹의 데이터베이스 중 하나를 허브 데이터베이스로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-114">You define one of the databases in the group as the Hub Database.</span></span> <span data-ttu-id="e3142-115">데이터베이스의 나머지 부분은 구성원 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-115">The rest of the databases are member databases.</span></span> <span data-ttu-id="e3142-116">동기화는 허브 및 개별 구성원 사이에서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-116">Sync occurs only between the Hub and individual members.</span></span>
-   <span data-ttu-id="e3142-117">**허브 데이터베이스**는 Azure SQL Database여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-117">The **Hub Database** must be an Azure SQL Database.</span></span>
-   <span data-ttu-id="e3142-118">**구성원 데이터베이스**는 SQL Database, 온-프레미스 SQL Server 데이터베이스 또는 Azure 가상 컴퓨터의 SQL Server 인스턴스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-118">The **member databases** can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances on Azure virtual machines.</span></span>
-   <span data-ttu-id="e3142-119">**동기화 데이터베이스**는 데이터 동기화에 대한 메타데이터 및 로그를 포함합니다. 동기화 데이터베이스는 허브 데이터베이스와 동일한 지역에 있는 Azure SQL Database여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-119">The **Sync Database** contains the metadata and log for Data Sync. The Sync Database has to be an Azure SQL Database located in the same region as the Hub Database.</span></span> <span data-ttu-id="e3142-120">동기화 데이터베이스는 생성된 고객 및 소유한 고객입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-120">The Sync Database is customer created and customer owned.</span></span>

> [!NOTE]
> <span data-ttu-id="e3142-121">온-프레미스 데이터베이스를 사용하는 경우 [로컬 에이전트를 구성](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-121">If you're using an on premises database, you have to [configure a local agent.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)</span></span>

![데이터베이스 간 데이터 동기화](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-to-use-data-sync"></a><span data-ttu-id="e3142-123">데이터 동기화를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="e3142-123">When to use Data Sync</span></span>

<span data-ttu-id="e3142-124">데이터 동기화는 몇몇 Azure SQL Database 또는 SQL Server 데이터베이스 간에 데이터를 최신 상태로 유지해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-124">Data Sync is useful in cases where data needs to be kept up to date across several Azure SQL Databases or SQL Server databases.</span></span> <span data-ttu-id="e3142-125">데이터 동기화에 대한 주요 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-125">Here are the main use cases for Data Sync:</span></span>

-   <span data-ttu-id="e3142-126">**하이브리드 데이터 동기화:** 데이터 동기화를 사용하면 온-프레미스 데이터베이스와 Azure SQL Databases 간에 데이터를 동기화하여 하이브리드 응용 프로그램을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-126">**Hybrid Data Synchronization:** With Data Sync, you can keep data synchronized between your on-premises databases and Azure SQL Databases to enable hybrid applications.</span></span> <span data-ttu-id="e3142-127">이 기능은 클라우드로 이동하려는 고객에게 표시되고 Azure에 응용 프로그램의 일부를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-127">This capability may appeal to customers who are considering moving to the cloud and would like to put some of their application in Azure.</span></span>

-   <span data-ttu-id="e3142-128">**배포된 응용 프로그램:** 많은 경우에 다른 데이터베이스에서 다양한 워크로드를 구분하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-128">**Distributed Applications:** In many cases, it's beneficial to separate different workloads across different databases.</span></span> <span data-ttu-id="e3142-129">예를 들어 대형 프로덕션 데이터베이스가 있지만 이 데이터에 대한 보고 또는 분석 워크로드를 실행해야 하는 경우 해당 추가 워크로드에 대한 두 번째 데이터베이스를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-129">For example, if you have a large production database, but you also need to run a reporting or analytics workload on this data, it's helpful to have a second database for this additional workload.</span></span> <span data-ttu-id="e3142-130">이 방법을 사용하면 프로덕션 워크로드에 미치는 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-130">This approach minimizes the performance impact on your production workload.</span></span> <span data-ttu-id="e3142-131">데이터 동기화를 사용하여 이러한 두 데이터베이스의 동기화를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-131">You can use Data Sync to keep these two databases synchronized.</span></span>

-   <span data-ttu-id="e3142-132">**전역 분산 응용 프로그램:** 많은 비즈니스는 여러 지역 및 여러 국가 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-132">**Globally Distributed Applications:** Many businesses span several regions and even several countries.</span></span> <span data-ttu-id="e3142-133">네트워크 대기 시간을 최소화하려면 가까운 지역에 데이터가 위치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-133">To minimize network latency, it's best to have your data in a region close to you.</span></span> <span data-ttu-id="e3142-134">데이터 동기화를 사용하면 전 세계 여러 지역에서 데이터베이스를 쉽게 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-134">With Data Sync, you can easily keep databases in regions around the world synchronized.</span></span>

<span data-ttu-id="e3142-135">다음과 같은 시나리오에서는 데이터 동기화를 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-135">We don't recommend Data Sync for the following scenarios:</span></span>

-   <span data-ttu-id="e3142-136">재해 복구</span><span class="sxs-lookup"><span data-stu-id="e3142-136">Disaster Recovery</span></span>

-   <span data-ttu-id="e3142-137">읽기 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e3142-137">Read Scale</span></span>

-   <span data-ttu-id="e3142-138">ETL(OLTP 및 OLAP 간)</span><span class="sxs-lookup"><span data-stu-id="e3142-138">ETL (OLTP to OLAP)</span></span>

-   <span data-ttu-id="e3142-139">온-프레미스 SQL Server에서 Azure SQL Database로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3142-139">Migration from on-premises SQL Server to Azure SQL Database</span></span>

## <a name="how-does-data-sync-work"></a><span data-ttu-id="e3142-140">데이터 동기화는 어떻게 작동하나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-140">How does Data Sync work?</span></span> 

-   <span data-ttu-id="e3142-141">**데이터 변경 내용 추적:** 데이터 동기화는 트리거 삽입, 업데이트 및 삭제를 사용하여 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-141">**Tracking data changes:** Data Sync tracks changes using insert, update, and delete triggers.</span></span> <span data-ttu-id="e3142-142">변경 내용은 사용자 데이터베이스에 있는 추가 표에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-142">The changes are recorded in a side table in the user database.</span></span>

-   <span data-ttu-id="e3142-143">**데이터 동기화:** 데이터 동기화는 허브 및 스포크 모델에서 설계됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-143">**Synchronizing data:** Data Sync is designed in a Hub and Spoke model.</span></span> <span data-ttu-id="e3142-144">허브는 개별적으로 각 구성원과 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-144">The Hub syncs with each member individually.</span></span> <span data-ttu-id="e3142-145">허브의 변경 내용이 구성원에 다운로드된 다음 구성원의 변경 내용은 허브에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-145">Changes from the Hub are downloaded to the member and then changes from the member are uploaded to the Hub.</span></span>

-   <span data-ttu-id="e3142-146">**충돌 해결:** 데이터 동기화는 충돌 해결을 위해 *허브 우선* 또는 *멤버 우선*이라는 두 가지 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-146">**Resolving conflicts:** Data Sync provides two options for conflict resolution, *Hub wins* or *Member wins*.</span></span>
    -   <span data-ttu-id="e3142-147">*허브 우선*을 선택하는 경우 허브의 변경 내용은 항상 구성원의 변경 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-147">If you select *Hub wins*, the changes in the hub always overwrite changes in the member.</span></span>
    -   <span data-ttu-id="e3142-148">*구성원 우선*을 선택하는 경우 구성원의 변경 내용은 항상 허브의 변경 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-148">If you select *Member wins*, the changes in the member overwrite changes in the hub.</span></span> <span data-ttu-id="e3142-149">구성원이 둘 이상인 경우 최종 값은 먼저 동기화된 구성원에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-149">If there's more than one member, the final value depends on which member syncs first.</span></span>

## <a name="limitations-and-considerations"></a><span data-ttu-id="e3142-150">제한 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e3142-150">Limitations and considerations</span></span>

### <a name="performance-impact"></a><span data-ttu-id="e3142-151">성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="e3142-151">Performance impact</span></span>
<span data-ttu-id="e3142-152">데이터 동기화는 트리거 삽입, 업데이트 및 삭제를 사용하여 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-152">Data Sync uses insert, update, and delete triggers to track changes.</span></span> <span data-ttu-id="e3142-153">변경 내용 추적을 위해 사용자 데이터베이스에 추가 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-153">It creates side tables in the user database for change tracking.</span></span> <span data-ttu-id="e3142-154">이러한 변경 내용 추적 작업은 데이터베이스 워크로드에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-154">These change tracking activities have an impact on your database workload.</span></span> <span data-ttu-id="e3142-155">서비스 계층을 평가하고 필요한 경우 업그레이드합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-155">Assess your service tier and upgrade if needed.</span></span>

### <a name="eventual-consistency"></a><span data-ttu-id="e3142-156">결과적 일관성</span><span class="sxs-lookup"><span data-stu-id="e3142-156">Eventual consistency</span></span>
<span data-ttu-id="e3142-157">데이터 동기화가 트리거 기반이기 때문에 트랜잭션 일관성이 보장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-157">Since Data Sync is trigger-based, transactional consistency is not guaranteed.</span></span> <span data-ttu-id="e3142-158">Microsoft는 결과적으로 모든 변경 내용을 적용하고 데이터 동기화가 데이터 손실을 발생하지 않도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-158">Microsoft guarantees that all changes are made eventually and that Data Sync does not cause data loss.</span></span>

### <a name="unsupported-data-types"></a><span data-ttu-id="e3142-159">지원되지 않는 데이터 형식</span><span class="sxs-lookup"><span data-stu-id="e3142-159">Unsupported data types</span></span>

-   <span data-ttu-id="e3142-160">FileStream</span><span class="sxs-lookup"><span data-stu-id="e3142-160">FileStream</span></span>

-   <span data-ttu-id="e3142-161">SQL/CLR UDT</span><span class="sxs-lookup"><span data-stu-id="e3142-161">SQL/CLR UDT</span></span>

-   <span data-ttu-id="e3142-162">XMLSchemaCollection(XML 지원)</span><span class="sxs-lookup"><span data-stu-id="e3142-162">XMLSchemaCollection (XML supported)</span></span>

-   <span data-ttu-id="e3142-163">Cursor, Timestamp, Hierarchyid</span><span class="sxs-lookup"><span data-stu-id="e3142-163">Cursor, Timestamp, Hierarchyid</span></span>

### <a name="requirements"></a><span data-ttu-id="e3142-164">요구 사항</span><span class="sxs-lookup"><span data-stu-id="e3142-164">Requirements</span></span>

-   <span data-ttu-id="e3142-165">각 표에는 기본 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-165">Each table must have a primary key.</span></span>

-   <span data-ttu-id="e3142-166">테이블에는 기본 키가 없는 ID 열이 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-166">A table cannot have an identity column that is not the primary key.</span></span>

-   <span data-ttu-id="e3142-167">개체(데이터베이스, 테이블 및 열) 이름에는 인쇄 가능한 문자 마침표(.), 왼쪽 대괄호([) 또는 오른쪽 대괄호(])를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-167">The names of objects (databases, tables, and columns) cannot contain the printable characters period (.), left square bracket ([), or right square bracket (]).</span></span>

### <a name="limitations-on-service-and-database-dimensions"></a><span data-ttu-id="e3142-168">서비스 및 데이터베이스 차원에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="e3142-168">Limitations on service and database dimensions</span></span>

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| <span data-ttu-id="e3142-169">**차원**</span><span class="sxs-lookup"><span data-stu-id="e3142-169">**Dimensions**</span></span>                                                      | <span data-ttu-id="e3142-170">**제한**</span><span class="sxs-lookup"><span data-stu-id="e3142-170">**Limit**</span></span>              | <span data-ttu-id="e3142-171">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="e3142-171">**Workaround**</span></span>              |
| <span data-ttu-id="e3142-172">데이터베이스가 속할 수 있는 동기화 그룹의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-172">Maximum number of sync groups any database can belong to.</span></span>       | <span data-ttu-id="e3142-173">5</span><span class="sxs-lookup"><span data-stu-id="e3142-173">5</span></span>                      |                             |
| <span data-ttu-id="e3142-174">단일 동기화 그룹에서 끝점의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-174">Maximum number of endpoints in a single sync group</span></span>              | <span data-ttu-id="e3142-175">30</span><span class="sxs-lookup"><span data-stu-id="e3142-175">30</span></span>                     | <span data-ttu-id="e3142-176">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e3142-176">Create multiple sync groups</span></span> |
| <span data-ttu-id="e3142-177">단일 동기화 그룹에서 온-프레미스 끝점의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-177">Maximum number of on-premises endpoints in a single sync group.</span></span> | <span data-ttu-id="e3142-178">5</span><span class="sxs-lookup"><span data-stu-id="e3142-178">5</span></span>                      | <span data-ttu-id="e3142-179">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e3142-179">Create multiple sync groups</span></span> |
| <span data-ttu-id="e3142-180">데이터베이스, 테이블, 스키마 및 열 이름</span><span class="sxs-lookup"><span data-stu-id="e3142-180">Database, table, schema, and column names</span></span>                       | <span data-ttu-id="e3142-181">이름당 50자</span><span class="sxs-lookup"><span data-stu-id="e3142-181">50 characters per name</span></span> |                             |
| <span data-ttu-id="e3142-182">동기화 그룹의 표</span><span class="sxs-lookup"><span data-stu-id="e3142-182">Tables in a sync group</span></span>                                          | <span data-ttu-id="e3142-183">500</span><span class="sxs-lookup"><span data-stu-id="e3142-183">500</span></span>                    | <span data-ttu-id="e3142-184">여러 동기화 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e3142-184">Create multiple sync groups</span></span> |
| <span data-ttu-id="e3142-185">동기화 그룹에서 표의 열</span><span class="sxs-lookup"><span data-stu-id="e3142-185">Columns in a table in a sync group</span></span>                              | <span data-ttu-id="e3142-186">1000</span><span class="sxs-lookup"><span data-stu-id="e3142-186">1000</span></span>                   |                             |
| <span data-ttu-id="e3142-187">표의 데이터 행 크기</span><span class="sxs-lookup"><span data-stu-id="e3142-187">Data row size on a table</span></span>                                        | <span data-ttu-id="e3142-188">24Mb</span><span class="sxs-lookup"><span data-stu-id="e3142-188">24 Mb</span></span>                  |                             |
| <span data-ttu-id="e3142-189">최소 동기화 간격</span><span class="sxs-lookup"><span data-stu-id="e3142-189">Minimum sync interval</span></span>                                           | <span data-ttu-id="e3142-190">5분</span><span class="sxs-lookup"><span data-stu-id="e3142-190">5 Minutes</span></span>              |                             |

## <a name="common-questions"></a><span data-ttu-id="e3142-191">일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="e3142-191">Common questions</span></span>

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a><span data-ttu-id="e3142-192">데이터 동기화에서 데이터를 동기화하는 빈도는 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-192">How frequently can Data Sync synchronize my data?</span></span> 
<span data-ttu-id="e3142-193">최소 빈도는 5분마다입니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-193">The minimum frequency is every five minutes.</span></span>

### <a name="can-i-use-data-sync-to-sync-between-sql-server-on-premises-databases-only"></a><span data-ttu-id="e3142-194">데이터 동기화를 사용하여 SQL Server 온-프레미스 데이터베이스 사이에서 동기화할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-194">Can I use Data Sync to sync between SQL Server on-premises databases only?</span></span> 
<span data-ttu-id="e3142-195">직접 끌 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-195">Not directly.</span></span> <span data-ttu-id="e3142-196">그러나 Azure에서 허브 데이터베이스를 만든 다음 온-프레미스 데이터베이스를 동기화 그룹에 추가하여 간접적으로 SQL Server 온-프레미스 데이터베이스 사이에서 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-196">You can sync between SQL Server on-premises databases indirectly, however, by creating a Hub database in Azure, and then adding the on-premises databases to the sync group.</span></span>
   
### <a name="can-i-use-data-sync-to-seed-data-from-my-production-database-to-an-empty-database-and-then-keep-them-synchronized"></a><span data-ttu-id="e3142-197">데이터 동기화를 사용하여 프로덕션 데이터베이스에서 빈 데이터베이스로 데이터를 시드한 다음 동기화된 상태로 유지할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-197">Can I use Data Sync to seed data from my production database to an empty database, and then keep them synchronized?</span></span> 
<span data-ttu-id="e3142-198">예.</span><span class="sxs-lookup"><span data-stu-id="e3142-198">Yes.</span></span> <span data-ttu-id="e3142-199">원본에서 스크립팅하여 수동으로 새 데이터베이스에 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-199">Create the schema manually in the new database by scripting it from the original.</span></span> <span data-ttu-id="e3142-200">스키마를 만든 후 테이블을 동기화 그룹에 추가하여 데이터를 복사하고 동기화된 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-200">After you create the schema, add the tables to a sync group to copy the data and keep it synced.</span></span>

### <a name="why-do-i-see-tables-that-i-did-not-create"></a><span data-ttu-id="e3142-201">내가 만들지 않은 테이블이 표시되는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e3142-201">Why do I see tables that I did not create?</span></span>  
<span data-ttu-id="e3142-202">데이터 동기화는 변경 내용 추적을 위해 데이터베이스에 추가 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-202">Data Sync creates side tables in your database for change tracking.</span></span> <span data-ttu-id="e3142-203">해당 테이블을 삭제하지 마세요. 삭제하면 데이터 동기화의 작동이 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-203">Don't delete them or Data Sync stops working.</span></span>
   
### <a name="i-got-an-error-message-that-said-cannot-insert-the-value-null-into-the-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-the-error"></a><span data-ttu-id="e3142-204">"\<column\> 열에 NULL 값을 삽입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-204">I got an error message that said "cannot insert the value NULL into the column \<column\>.</span></span> <span data-ttu-id="e3142-205">열에는 Null을 사용할 수 없습니다."라는 오류 메시지를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-205">Column does not allow nulls."</span></span> <span data-ttu-id="e3142-206">이 오류는 어떤 의미이며 오류를 수정할 수 있는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="e3142-206">What does this mean, and how can I fix the error?</span></span> 
<span data-ttu-id="e3142-207">이 오류 메시지는 다음 두 가지 문제 중 하나를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-207">This error message indicates one of the two following issues:</span></span>
1.  <span data-ttu-id="e3142-208">기본 키가 없는 테이블이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-208">There may be a table without a primary key.</span></span> <span data-ttu-id="e3142-209">이 문제를 해결하려면 동기화하는 모든 테이블에 기본 키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-209">To fix this issue, add a primary key to all the tables you're syncing.</span></span>
2.  <span data-ttu-id="e3142-210">CREATE INDEX 문에 WHERE 절이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-210">There may be a WHERE clause in your CREATE INDEX statement.</span></span> <span data-ttu-id="e3142-211">동기화에서는 이 조건이 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-211">Sync does not handle this condition.</span></span> <span data-ttu-id="e3142-212">이 문제를 해결하려면 WHERE 절을 제거하거나 수동으로 모든 데이터베이스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-212">To fix this issue, remove the WHERE clause or manually make the changes to all databases.</span></span> 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-the-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a><span data-ttu-id="e3142-213">데이터 동기화에서는 어떻게 순환 참조가 처리되나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-213">How does Data Sync handle circular references?</span></span> <span data-ttu-id="e3142-214">즉, 여러 동기화 그룹에서 동일한 데이터가 동기화되어 결과적으로 계속 변경되는 경우 어떻게 처리되나요?</span><span class="sxs-lookup"><span data-stu-id="e3142-214">That is, when the same data is synced in multiple sync groups, and keeps changing as a result?</span></span>
<span data-ttu-id="e3142-215">데이터 동기화에서는 순환 참조가 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-215">Data Sync doesn’t handle circular references.</span></span> <span data-ttu-id="e3142-216">순환 참조가 발생하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3142-216">Be sure to avoid them.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3142-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e3142-217">Next steps</span></span>

<span data-ttu-id="e3142-218">SQL 데이터 동기화에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3142-218">For more info about SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="e3142-219">SQL 데이터 동기화 시작</span><span class="sxs-lookup"><span data-stu-id="e3142-219">Getting Started with SQL Data Sync</span></span>](sql-database-get-started-sql-data-sync.md)

-   <span data-ttu-id="e3142-220">SQL Data Sync 구성 방법을 보여주는 전체 PowerShell 예제:</span><span class="sxs-lookup"><span data-stu-id="e3142-220">Complete PowerShell examples that show how to configure SQL Data Sync:</span></span>
    -   [<span data-ttu-id="e3142-221">PowerShell을 사용하여 여러 Azure SQL Database 간 동기화</span><span class="sxs-lookup"><span data-stu-id="e3142-221">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [<span data-ttu-id="e3142-222">PowerShell을 사용하여 Azure SQL Database와 SQL Server 온-프레미스 데이터베이스 간 동기화</span><span class="sxs-lookup"><span data-stu-id="e3142-222">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [<span data-ttu-id="e3142-223">전체 SQL 데이터 동기화 기술 설명서 다운로드</span><span class="sxs-lookup"><span data-stu-id="e3142-223">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [<span data-ttu-id="e3142-224">SQL 데이터 동기화 REST API 설명서 다운로드</span><span class="sxs-lookup"><span data-stu-id="e3142-224">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

<span data-ttu-id="e3142-225">SQL Database에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3142-225">For more info about SQL Database, see:</span></span>

-   [<span data-ttu-id="e3142-226">SQL 데이터베이스 개요</span><span class="sxs-lookup"><span data-stu-id="e3142-226">SQL Database Overview</span></span>](sql-database-technical-overview.md)

-   [<span data-ttu-id="e3142-227">데이터베이스 수명 주기 관리</span><span class="sxs-lookup"><span data-stu-id="e3142-227">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
