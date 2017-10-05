---
title: "여러 Azure SQL 데이터베이스에 대해 임시 분석 쿼리 실행 | Microsoft Docs"
description: "Wingtip SaaS 다중 테넌트 앱에서 여러 SQL Database에 걸쳐 임시 분석 쿼리를 실행합니다."
keywords: "sql 데이터베이스 자습서"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: c287fe5d6b333c749b0580b5253e7e46ac27232b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a><span data-ttu-id="067d0-104">모든 Wingtip SaaS 테넌트에서 임시 분석 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="067d0-104">Run ad-hoc analytics queries across all Wingtip SaaS tenants</span></span>

<span data-ttu-id="067d0-105">이 자습서에서는 테넌트 데이터베이스의 전체 집합에서 배포된 쿼리를 실행하여 임시 분석을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-105">In this tutorial, you run distributed queries across the entire set of tenant databases to enable ad-hoc analytics.</span></span> <span data-ttu-id="067d0-106">배포된 쿼리를 사용하도록 설정하는 데 탄력적 쿼리를 사용합니다. 그러려면 추가 분석 데이터베이스를 카탈로그 서버에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-106">Elastic Query is used to enable distributed queries, which requires an additional analytics database is deployed (to the catalog server).</span></span> <span data-ttu-id="067d0-107">이러한 쿼리는 Wingtip SaaS 앱의 일일 운영 데이터에 담긴 정보를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-107">These queries can extract insights buried in the day-to-day operational data of the Wingtip SaaS app.</span></span>


<span data-ttu-id="067d0-108">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-108">In this tutorial you learn:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="067d0-109">테넌트 간 효율적인 쿼리를 활성화하는 각 데이터베이스의 전역 뷰 정보</span><span class="sxs-lookup"><span data-stu-id="067d0-109">About the global views in each database, that enable efficient querying across tenants</span></span>
> * <span data-ttu-id="067d0-110">임시 분석 데이터베이스를 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="067d0-110">How to deploy an ad-hoc analytics database</span></span>
> * <span data-ttu-id="067d0-111">모든 테넌트 데이터베이스 간에 분산 쿼리를 실행하는 방법</span><span class="sxs-lookup"><span data-stu-id="067d0-111">How to run distributed queries across all tenant databases</span></span>



<span data-ttu-id="067d0-112">이 자습서를 수행하려면 다음 필수 조건이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-112">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

* <span data-ttu-id="067d0-113">Wingtip SaaS 앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-113">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="067d0-114">5분 내에 배포하려면 [Wingtip SaaS 응용 프로그램 배포 및 탐색](sql-database-saas-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="067d0-114">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="067d0-115">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="067d0-116">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="067d0-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="067d0-117">SSMS(SQL Server Management Studio)가 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-117">SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="067d0-118">SSMS를 다운로드하고 설치하려면 [SSMS(SQL Server Management Studio) 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="067d0-118">To download and install SSMS, see [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


## <a name="ad-hoc-analytics-pattern"></a><span data-ttu-id="067d0-119">임시 분석 패턴</span><span class="sxs-lookup"><span data-stu-id="067d0-119">Ad-hoc analytics pattern</span></span>

<span data-ttu-id="067d0-120">SaaS 응용 프로그램을 사용했을 때의 큰 장점 중 하나는 클라우드 중앙에 저장된 광범위한 테넌트 데이터를 사용할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-120">One of the great opportunities with SaaS applications is to use the vast amount of tenant data stored centrally in the cloud.</span></span> <span data-ttu-id="067d0-121">이 데이터를 사용하여 응용 프로그램의 작업 및 사용, 테넌트, 사용자 및 사용자의 선호 및 행동 등에 관한 정보를 확보할 수 있습니다. 이러한 정보는 기능 개발, 활용성 향상 및 기타 앱 및 서비스 투자를 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-121">Use this data to gain insights into the operation and usage of your application, your tenants, their users, preferences, behaviors, etc. These insights can guide feature development, usability improvements, and other investments in your apps and services.</span></span>

<span data-ttu-id="067d0-122">단일 다중 테넌트 데이터베이스에 있을 때 이 데이터에 액세스하는 것은 쉽지만 잠재적인 수천 개의 데이터베이스 규모로 분산되는 경우는 그렇게 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-122">Accessing this data in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="067d0-123">한 가지 방법은 공통 스키마를 통해 배포된 데이터베이스 집합 전체에서 쿼리를 구현하는 [탄력적 쿼리](sql-database-elastic-query-overview.md)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-123">One approach is to use [Elastic Query](sql-database-elastic-query-overview.md), which enables querying across a distributed set of databases with common schema.</span></span> <span data-ttu-id="067d0-124">탄력적 쿼리는 분산된(테넌트) 데이터베이스에서 테이블 또는 뷰를 미러링하는 외부 테이블이 정의되는 단일 *헤드* 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-124">Elastic Query uses a single *head* database in which external tables are defined that mirror tables or views in the distributed (tenant) databases.</span></span> <span data-ttu-id="067d0-125">이 헤드 데이터베이스에 제출된 쿼리는 분산 쿼리 계획을 생성하기 위해 컴파일되며 이 쿼리 중 일부는 필요에 따라 테넌트 데이터베이스에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-125">Queries submitted to this head database are compiled to produce a distributed query plan, with portions of the query pushed down to the tenant databases as needed.</span></span> <span data-ttu-id="067d0-126">탄력적 쿼리는 카탈로그 데이터베이스에서 분할된 데이터베이스 맵을 사용하여 테넌트 데이터베이스의 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-126">Elastic Query uses the shard map in the catalog database to provide the location of the tenant databases.</span></span> <span data-ttu-id="067d0-127">설정 및 쿼리는 일반 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)을 사용하여 바로 진행되며 Power BI 또는 Excel 같은 도구에서의 임시 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-127">Setup and query are straightforward using standard [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference), and support ad-hoc querying from tools like Power BI and Excel.</span></span>

<span data-ttu-id="067d0-128">탄력적 쿼리는 테넌트 데이터베이스에 쿼리를 배포하여 라이브 프로덕션 데이터에 즉시 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-128">By distributing queries across the tenant databases, Elastic Query provides immediate insight into live production data.</span></span> <span data-ttu-id="067d0-129">그러나 탄력적 쿼리가 잠재적으로 많은 데이터베이스에서 데이터를 가져오면 쿼리 대기 시간이 단일 다중 테넌트 데이터베이스에 제출되는 해당 쿼리보다 높아지는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-129">However, as Elastic Query pulls data from potentially many databases, query latency can sometimes be higher than for equivalent queries submitted to a single multi-tenant database.</span></span> <span data-ttu-id="067d0-130">반환되는 데이터를 최소화하기 위해 쿼리를 설계하는 경우 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-130">Care should be taken when designing queries to minimize the data that is returned.</span></span> <span data-ttu-id="067d0-131">탄력적 쿼리는 자주 사용되는 문서 또는 복잡한 분석 쿼리나 보고서를 빌드하는 경우와 달리 적은 양의 실시간 데이터를 쿼리하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-131">Elastic Query is often best suited for querying small amounts of real-time data, as opposed to building frequently used or complex analytics queries or reports.</span></span> <span data-ttu-id="067d0-132">쿼리 성능이 좋지 않은 경우 [실행 계획](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan)을 보고 원격 데이터베이스에 푸시되는 쿼리의 부분 및 반환되는 데이터의 양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-132">If queries don't perform well, look at the [execution plan](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) to see what part of the query has been pushed down to the remote database and how much data is being returned.</span></span> <span data-ttu-id="067d0-133">때때로 테넌트 데이터를 분석 쿼리에 최적화된 전용 데이터베이스 또는 데이터 웨어하우스로 추출하는 경우 복잡한 분석 처리를 필요로 하는 쿼리가 효율적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-133">Queries that require complex analytical processing may be better served in some cases by extracting tenant data into a dedicated database or data warehouse optimized for analytics queries.</span></span> <span data-ttu-id="067d0-134">이 패턴은 [테넌트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md)에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-134">This pattern is explained in the [tenant analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md).</span></span> 

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="067d0-135">Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="067d0-135">Get the Wingtip application scripts</span></span>

<span data-ttu-id="067d0-136">Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-136">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="067d0-137">[Wingtip SaaS 스크립트를 다운로드하는 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="067d0-137">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-ticket-sales-data"></a><span data-ttu-id="067d0-138">티켓 판매 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="067d0-138">Create ticket sales data</span></span>

<span data-ttu-id="067d0-139">흥미로운 데이터 집합에 대해 쿼리를 실행하려면 티켓 생성기를 실행하여 티켓 판매 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-139">To run queries against a more interesting data set, create ticket sales data by running the ticket-generator.</span></span>

1. <span data-ttu-id="067d0-140">*PowerShell ISE*에서 \\학습 모듈\\운영 분석\\임시 분석\\*Demo-AdhocAnalytics.ps1* 스크립트를 열고 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-140">In the *PowerShell ISE*, open the ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* script and set the following values:</span></span>
   * <span data-ttu-id="067d0-141">**$DemoScenario** = 1, **모든 부문에서 이벤트 티켓을 구입합니다**.</span><span class="sxs-lookup"><span data-stu-id="067d0-141">**$DemoScenario** = 1, **Purchase tickets for events at all venues**.</span></span>
2. <span data-ttu-id="067d0-142">**F5** 키를 눌러 스크립트를 실행하고 티켓 판매를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-142">Press **F5** to run the script and generate ticket sales.</span></span> <span data-ttu-id="067d0-143">스크립트를 실행하는 동안 이 자습서의 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-143">While the script is running, continue the steps in this tutorial.</span></span> <span data-ttu-id="067d0-144">*임시 배포된 쿼리 실행* 섹션에서 티켓 데이터를 쿼리하여 티켓 생성자가 해당 연습에 도달할 때 실행되는 경우 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-144">The ticket data is queried in the *Run ad-hoc distributed queries* section, so wait for the ticket generator to complete if it's still running when you get to that exercise.</span></span>

## <a name="explore-the-global-views"></a><span data-ttu-id="067d0-145">전역 뷰 탐색</span><span class="sxs-lookup"><span data-stu-id="067d0-145">Explore the global views</span></span>

<span data-ttu-id="067d0-146">Wingtip SaaS 응용 프로그램은 데이터베이스 당 테넌트 모델을 사용하여 빌드되므로 테넌트 데이터베이스 스키마는 단일 테넌트 관점에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-146">The Wingtip SaaS application is built using a tenant-per-database model, so the tenant database schema is defined from a single-tenant perspective.</span></span> <span data-ttu-id="067d0-147">테넌트 전용 정보는 하나의 테이블 *Venue*에 존재하며 이 테이블에는 항상 하나의 행이 있고 따라서 기본 키가 없는 힙으로 실현됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-147">Tenant-specific information exists in one table, *Venue*, which always has a single row, and is implemented as a heap, without a primary key.</span></span> <span data-ttu-id="067d0-148">정상적인 사용에서는 데이터가 속해 있는 테넌트에 의심의 여지가 없기 때문에 스키마의 다른 테이블은 *Venue* 테이블과 관련될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-148">Other tables in the schema don't need to be related to the *Venue* table, because in normal use, there is never any doubt which tenant the data belongs to.</span></span>

<span data-ttu-id="067d0-149">그러나 탄력적 쿼리는 모든 데이터베이스에 쿼리할 경우 테넌트 별로 분할된 단일 논리 데이터베이스의 일부인 경우와 같이 해당 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-149">However, when querying across all databases, it's important that Elastic Query can treat the data as if it is part of a single logical database sharded by tenant.</span></span> <span data-ttu-id="067d0-150">이를 위해 '전역' 뷰 집합이 전역적으로 쿼리되는 각 테이블에 테넌트 ID를 프로젝션하는 테넌트 데이터베이스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-150">To achieve this, a set of 'global' views are added to the tenant database that project a tenant id into each of the tables that are queried globally.</span></span> <span data-ttu-id="067d0-151">예를 들어 *VenueEvents* 보기는 계산된 *VenueId*를 *이벤트* 테이블에서 프로젝션된 열에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-151">For example, the *VenueEvents* view adds a computed *VenueId* to the columns projected from the *Events* table.</span></span> <span data-ttu-id="067d0-152">탄력적 쿼리는 (기본 *이벤트* 테이블이 아닌) *VenueEvents*를 통해 헤드 데이터베이스에서 외부 테이블을 정의하여 *VenueId*에 따라 조인을 밀어넣을 수 있습니다. 그러면 각 원격 데이터베이스에서 병렬로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-152">By defining the external table in the head database over *VenueEvents* (rather than the underlying *Events* table), Elastic Query is able to push down joins based on *VenueId* so they can be executed in parallel on each remote database (rather than on the head database).</span></span> <span data-ttu-id="067d0-153">이렇게 하면 반환되는 데이터의 양이 크게 줄어듭니다. 그 결과 많은 쿼리의 성능이 크게 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-153">This dramatically reduces the amount of data that is returned, which results in a substantial increase in performance for many queries.</span></span> <span data-ttu-id="067d0-154">이러한 전역 보기는 모든 테넌트 데이터베이스(및 *basetenantdb*)에서 미리 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-154">These global views have been pre-created in all tenant databases (and in *basetenantdb*).</span></span>

1. <span data-ttu-id="067d0-155">SSMS를 열고 [테넌트1-&lt;사용자&gt; 서버에 연결](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-155">Open SSMS and [connect to the tenants1-&lt;USER&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).</span></span>
2. <span data-ttu-id="067d0-156">**데이터베이스**를 확장하고 **contosoconcerthall**을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-156">Expand **Databases**, right-click **contosoconcerthall**, and select **New Query**.</span></span>
3. <span data-ttu-id="067d0-157">다음 쿼리를 실행하여 단일 테넌트 테이블과 전역 뷰 간의 차이를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-157">Run the following queries to explore the difference between the single-tenant tables and the global views:</span></span>

   ```T-SQL
   -- The base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice the plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- The base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects the VenueId retrieved from the Venues table.
   SELECT * FROM VenueEvents
   ```

<span data-ttu-id="067d0-158">이러한 보기에서 *VenueId*는 부문 이름의 해시로 계산되지만 어떤 방법으로든 고유한 값을 도입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-158">In these views, the *VenueId* is computed as a hash of the Venue name, but any approach could be used to introduce a unique value.</span></span> <span data-ttu-id="067d0-159">이 방법은 카탈로그에서 사용하기 위해 테넌트 키를 계산하는 방식과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-159">This approach is similar to the way the tenant key is computed for use in the catalog.</span></span>

<span data-ttu-id="067d0-160">*부문* 보기의 정의를 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="067d0-160">To examine the definition of the *Venues* view:</span></span>

1. <span data-ttu-id="067d0-161">**개체 탐색기**에서 **contosoconcethall** > **뷰**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-161">In **Object Explorer**, expand **contosoconcethall** > **Views**:</span></span>

   ![뷰](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. <span data-ttu-id="067d0-163">**dbo.Venues**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-163">Right-click **dbo.Venues**.</span></span>
3. <span data-ttu-id="067d0-164">**뷰 스크립팅** > **CREATE** > **새 쿼리 편집기 창**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-164">Select **Script View as** > **CREATE To** > **New Query Editor Window**</span></span>

<span data-ttu-id="067d0-165">다른 *부문* 보기를 스크립팅하여 *VenueId*를 추가하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-165">Script any of the other *Venue* views to see how they add the *VenueId*.</span></span>

## <a name="deploy-the-database-used-for-ad-hoc-distributed-queries"></a><span data-ttu-id="067d0-166">임시 배포된 쿼리에 사용되는 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="067d0-166">Deploy the database used for ad-hoc distributed queries</span></span>

<span data-ttu-id="067d0-167">이 연습에서는 *adhocanalytics* 데이터베이스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-167">This exercise deploys the *adhocanalytics* database.</span></span> <span data-ttu-id="067d0-168">모든 테넌트 데이터베이스에 쿼리하는 데 사용되는 스키마를 포함하는 헤드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-168">This is the head database that will contain the schema used for querying across all tenant databases.</span></span> <span data-ttu-id="067d0-169">데이터베이스는 샘플 앱에서 모든 관리 관련 데이터베이스에 사용되는 서버인 기존 카탈로그 서버에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-169">The database is deployed to the existing catalog server, which is the server used for all management-related databases in the sample app.</span></span>

1. <span data-ttu-id="067d0-170">*PowerShell ISE*에서 \\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1*를 열고 다음 갚을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-170">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* in the *PowerShell ISE* and set the following values:</span></span>
   * <span data-ttu-id="067d0-171">**$DemoScenario** = 2, **임시 분석 데이터베이스 배포**.</span><span class="sxs-lookup"><span data-stu-id="067d0-171">**$DemoScenario** = 2, **Deploy Ad-hoc analytics database**.</span></span>

2. <span data-ttu-id="067d0-172">스크립트를 실행하고 *adhocanalytics* 데이터베이스를 만들려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-172">Press **F5** to run the script and create the *adhocanalytics* database.</span></span>

<span data-ttu-id="067d0-173">다음 섹션에서 배포된 쿼리를 실행하는 데 사용할 수 있도록 데이터베이스에 스키마를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-173">In the next section, you add schema to the database so it can be used to run distributed queries.</span></span>

## <a name="configure-the-database-for-running-distributed-queries"></a><span data-ttu-id="067d0-174">배포된 쿼리를 실행하기 위한 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="067d0-174">Configure the database for running distributed queries</span></span>

<span data-ttu-id="067d0-175">이 연습에서는 모든 테넌트 데이터베이스에서 쿼리할 수 있도록 하는 임시 분석 데이터베이스에 스키마(외부 데이터 원본 및 외부 테이블 정의)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-175">This exercise adds schema (the external data source and external table definitions) to the ad-hoc analytics database that enables querying across all tenant databases.</span></span>

1. <span data-ttu-id="067d0-176">SQL Server Management Studio를 열고 이전 단계에서 만든 임시 분석 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-176">Open SQL Server Management Studio, and connect to the Adhoc Analytics database you created in the previous step.</span></span> <span data-ttu-id="067d0-177">데이터베이스의 이름은 adhocanalytics입니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-177">The name of the database will be adhocanalytics.</span></span>
2. <span data-ttu-id="067d0-178">SSMS에서...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-178">Open ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* in SSMS.</span></span>
3. <span data-ttu-id="067d0-179">SQL 스크립트를 검토하고 다음을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-179">Review the SQL script and note the following:</span></span>

   <span data-ttu-id="067d0-180">탄력적인 쿼리는 데이터베이스 범위 자격 증명을 사용하여 각 테넌트 데이터베이스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-180">Elastic Query uses a database-scoped credential to access each of the tenant databases.</span></span> <span data-ttu-id="067d0-181">이 자격 증명은 모든 데이터베이스에서 사용할 수 있어야 하며 일반적으로 이러한 임시 쿼리를 사용하는 데 필요한 최소 권한이 부여되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-181">This credential needs to be available in all the databases and should normally be granted the minimum rights required to enable these ad-hoc queries.</span></span>

    ![자격 증명 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   <span data-ttu-id="067d0-183">카탈로그 데이터베이스에서 테넌트 Shard Map을 사용하도록 정의된 외부 데이터 원본.</span><span class="sxs-lookup"><span data-stu-id="067d0-183">The external data source, that is defined to use the tenant shard map in the catalog database.</span></span> <span data-ttu-id="067d0-184">이것을 외부 데이터 원본으로 사용하면 쿼리가 실행되는 경우 카탈로그에 등록된 모든 데이터베이스에 쿼리가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-184">By using this as the external data source, queries are distributed to all databases registered in the catalog when the query is run.</span></span> <span data-ttu-id="067d0-185">각 배포에 대한 서버 이름이 다르기 때문에 이 초기화 스크립트는 스크립트가 실행되는 현재 서버(@@servername)를 검색하여 카탈로그 데이터베이스의 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-185">Because server names are different for each deployment, this initialization script gets the location of the catalog database by retrieving the current server (@@servername) where the script is executed.</span></span>

    ![외부 데이터 원본 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   <span data-ttu-id="067d0-187">이전 섹션에서 설명한 전역 뷰를 참조하고 **DISTRIBUTION = SHARDED(VenueId)**로 정의되는 외부 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-187">The external tables that reference the global views described in the previous section, and defined with **DISTRIBUTION = SHARDED(VenueId)**.</span></span> <span data-ttu-id="067d0-188">각 *VenueId*가 단일 데이터베이스에 매핑되기 때문에 다음 섹션에 표시된 대로 다양한 시나리오의 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-188">Because each *VenueId* maps to a single database, this improves performance for many scenarios as shown in the next section.</span></span>

    ![외부 테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   <span data-ttu-id="067d0-190">생성되고 채워진 로컬 테이블 *VenueTypes*.</span><span class="sxs-lookup"><span data-stu-id="067d0-190">The local table *VenueTypes* that is created and populated.</span></span> <span data-ttu-id="067d0-191">이 참조 데이터 테이블은 모든 테넌트 데이터베이스에서 일반적이므로 여기에서 로컬 테이블로 표시되며 일반 데이터로 채워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-191">This reference data table is common in all tenant databases, so it can be represented here as a local table and populated with the common data.</span></span> <span data-ttu-id="067d0-192">이 일부 쿼리의 경우 테넌트 데이터베이스와 *adhocanalytics* 데이터베이스 간에 이동되는 데이터의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-192">For some queries this may reduce the amount of data moved between the tenant databases and the *adhocanalytics* database.</span></span>

    ![테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   <span data-ttu-id="067d0-194">이러한 방식으로 참조 테이블을 포함하는 경우 테넌트 데이터베이스를 업데이트할 때마다 테이블 스키마 및 데이터를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-194">If you include reference tables in this manner, be sure to update the table schema and data whenever you update the tenant databases.</span></span>

4. <span data-ttu-id="067d0-195">스크립트를 실행하고 *adhocanalytics* 데이터베이스를 초기화하려면 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-195">Press **F5** to run the script and initialize the *adhocanalytics* database.</span></span> 

<span data-ttu-id="067d0-196">이제 배포된 쿼리를 실행하고 모든 테넌트 간에 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-196">Now you can run distributed queries, and gather insights across all tenants!</span></span>

## <a name="run-ad-hoc-distributed-queries"></a><span data-ttu-id="067d0-197">임시 배포된 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="067d0-197">Run ad-hoc distributed queries</span></span>

<span data-ttu-id="067d0-198">이제 *adhocanalytics* 데이터베이스가 설정되었으므로 앞에서 배포된 몇 가지 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-198">Now that the *adhocanalytics* database is set up, go ahead and run some distributed queries.</span></span> <span data-ttu-id="067d0-199">쿼리 처리가 발생하는 위치를 이해하는 실행 계획을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-199">Include the execution plan for a better understanding of where the query processing is happening.</span></span> 

<span data-ttu-id="067d0-200">실행 계획을 검사할 때 자세한 내용을 보려면 계획 아이콘 위로 마우스를 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-200">When inspecting the execution plan, hover over the plan icons for details.</span></span> 

<span data-ttu-id="067d0-201">기억할 점은 외부 데이터 소스를 정의하는 경우 **DISTRIBUTION = SHARDED(VenueId)**를 설정하는 것입니다. 그러면 다양한 시나리오의 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-201">Important to note, is that setting **DISTRIBUTION = SHARDED(VenueId)** when we defined the external data source, improves performance for many scenarios.</span></span> <span data-ttu-id="067d0-202">각 *VenueId*가 단일 데이터베이스에 매핑하기 때문에 쉽게 원격으로 필터링할 수 있으며 필요한 데이터만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-202">Because each *VenueId* maps to a single database, filtering is easily done remotely, returning only the data we need.</span></span>

1. <span data-ttu-id="067d0-203">SSMS에서 \\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-203">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.</span></span>
2. <span data-ttu-id="067d0-204">**adhocanalytics** 데이터베이스에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-204">Ensure you are connected to the **adhocanalytics** database.</span></span>
3. <span data-ttu-id="067d0-205">**쿼리** 메뉴를 선택하고 **실제 실행 계획 포함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-205">Select the **Query** menu and click **Include Actual Execution Plan**</span></span>
4. <span data-ttu-id="067d0-206">*현재 등록된 부문* 쿼리를 강조 표시하고 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-206">Highlight the *Which venues are currently registered?* query, and press **F5**.</span></span>

   <span data-ttu-id="067d0-207">쿼리는 전체 부문 목록을 반환하고 모든 테넌트에 쉽고 빠르게 쿼리하는 방법 및 각 테넌트의 데이터를 반환하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-207">The query returns the entire venue list, illustrating how quick and easy it is to query across all tenants and return data from each tenant.</span></span>

   <span data-ttu-id="067d0-208">각 테넌트 데이터베이스로 이동하고 부문 정보를 선택하기 때문에 계획을 검사하고 전체 비용이 원격 쿼리인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-208">Inspect the plan and see that the entire cost is the remote query because we're simply going to each tenant database and selecting the venue information.</span></span>

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. <span data-ttu-id="067d0-210">다음 쿼리를 선택하고 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-210">Select the next query, and press **F5**.</span></span>

   <span data-ttu-id="067d0-211">이 쿼리는 테넌트 데이터베이스 및 로컬 *VenueTypes* 테이블의 데이터를 조인합니다(로컬인 *adhocanalytics* 데이터베이스의 테이블임).</span><span class="sxs-lookup"><span data-stu-id="067d0-211">This query joins data from the tenant databases and the local *VenueTypes* table (local, as its a table in the *adhocanalytics* database).</span></span>

   <span data-ttu-id="067d0-212">각 테넌트의 부문 정보(dbo.Venues)를 쿼리한 다음 *VenueTypes* 테이블과 빠르게 로컬 조인하여 친숙한 이름을 표시하기 때문에 계획을 검사하고 비용의 대부분이 원격 쿼리인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-212">Inspect the plan and see that the majority of cost is the remote query because we query each tenant's venue info (dbo.Venues), and then do a quick local join with the local *VenueTypes* table to display the friendly name.</span></span>

   ![원격 및 로컬 데이터에 조인](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. <span data-ttu-id="067d0-214">이제 *가장 많은 티켓을 판매한 날짜* 쿼리를 선택하고 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-214">Now select the *On which day were the most tickets sold?* query, and press **F5**.</span></span>

   <span data-ttu-id="067d0-215">이 쿼리는 좀 더 복잡한 조인 및 집계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-215">This query does a bit more complex joining and aggregation.</span></span> <span data-ttu-id="067d0-216">대부분 처리를 원격으로 수행하는 것이 중요합니다. 또한 여기서는 다시 필요한 행만을 가져오고 일당 각 부문의 집계 티켓 판매 개수의 단일 행만을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-216">What's important to note is that most of the processing is done remotely, and once again, we bring back only the rows we need, returning just a single row for each venue's aggregate ticket sale count per day.</span></span>

   ![쿼리](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a><span data-ttu-id="067d0-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="067d0-218">Next steps</span></span>

<span data-ttu-id="067d0-219">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-219">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="067d0-220">모든 테넌트 데이터베이스에서 분산 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="067d0-220">Run distributed queries across all tenant databases</span></span>
> * <span data-ttu-id="067d0-221">임시 분석 데이터베이스를 배포하고 스키마를 추가하여 배포된 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-221">Deploy an ad-hoc analytics database and add schema to it to run distributed queries.</span></span>


<span data-ttu-id="067d0-222">이제 [테넌트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md)를 시도하여 복잡한 분석을 처리하기 위해 별도 분석 데이터베이스에 추출하는 데이터를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="067d0-222">Now try the [Tenant Analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md) to explore extracting data to a separate analytics database for more complex analytics processing...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="067d0-223">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="067d0-223">Additional resources</span></span>

* <span data-ttu-id="067d0-224">[Wingtip SaaS 응용 프로그램을 기반으로 작성된](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="067d0-224">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="067d0-225">탄력적 쿼리</span><span class="sxs-lookup"><span data-stu-id="067d0-225">Elastic Query</span></span>](sql-database-elastic-query-overview.md)
