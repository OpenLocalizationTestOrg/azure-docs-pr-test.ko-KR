---
title: "여러 Azure SQL 데이터베이스에 걸쳐 aaaRun 임시 분석 쿼리 | Microsoft Docs"
description: "Hello Wingtip SaaS 다중 테 넌 트 응용 프로그램에서 여러 SQL 데이터베이스에 걸쳐 임시 분석 쿼리를 실행 합니다."
keywords: "SQL Database 자습서"
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
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a><span data-ttu-id="484c0-104">모든 Wingtip SaaS 테넌트에서 임시 분석 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="484c0-104">Run ad-hoc analytics queries across all Wingtip SaaS tenants</span></span>

<span data-ttu-id="484c0-105">이 자습서에서는 쿼리를 실행할 분산 테 넌 트 데이터베이스의 전체 집합 hello tooenable 임시 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-105">In this tutorial, you run distributed queries across hello entire set of tenant databases tooenable ad-hoc analytics.</span></span> <span data-ttu-id="484c0-106">탄력적 쿼리는 사용 되는 tooenable 분산 쿼리, 추가 분석 데이터베이스를 배포 해야 (toohello 카탈로그 서버).</span><span class="sxs-lookup"><span data-stu-id="484c0-106">Elastic Query is used tooenable distributed queries, which requires an additional analytics database is deployed (toohello catalog server).</span></span> <span data-ttu-id="484c0-107">이러한 쿼리는 hello Wingtip SaaS 응용 프로그램의 hello 일상적인 운영 데이터에 포함 된 정보를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-107">These queries can extract insights buried in hello day-to-day operational data of hello Wingtip SaaS app.</span></span>


<span data-ttu-id="484c0-108">이 자습서에서는 다음에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-108">In this tutorial you learn:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="484c0-109">각 데이터베이스에서 전역 뷰 hello에 대 한 수 있도록 하는 테 넌 트 간에 효율적인 쿼리</span><span class="sxs-lookup"><span data-stu-id="484c0-109">About hello global views in each database, that enable efficient querying across tenants</span></span>
> * <span data-ttu-id="484c0-110">어떻게 toodeploy 임시 분석 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="484c0-110">How toodeploy an ad-hoc analytics database</span></span>
> * <span data-ttu-id="484c0-111">Toorun 모든 테 넌 트 데이터베이스에서 쿼리를 분산 하는 방법</span><span class="sxs-lookup"><span data-stu-id="484c0-111">How toorun distributed queries across all tenant databases</span></span>



<span data-ttu-id="484c0-112">toocomplete이이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-112">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="484c0-113">hello Wingtip SaaS 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-113">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="484c0-114">5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="484c0-114">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="484c0-115">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-115">Azure PowerShell is installed.</span></span> <span data-ttu-id="484c0-116">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="484c0-116">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="484c0-117">SSMS(SQL Server Management Studio)가 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-117">SQL Server Management Studio (SSMS) is installed.</span></span> <span data-ttu-id="484c0-118">SSMS 설치 하 고 toodownload 참조 [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-118">toodownload and install SSMS, see [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


## <a name="ad-hoc-analytics-pattern"></a><span data-ttu-id="484c0-119">임시 분석 패턴</span><span class="sxs-lookup"><span data-stu-id="484c0-119">Ad-hoc analytics pattern</span></span>

<span data-ttu-id="484c0-120">Hello 좋은 기회 SaaS 응용 프로그램 중 하나 toouse hello 방대한 양의 hello 클라우드에 저장 하는 테 넌 트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-120">One of hello great opportunities with SaaS applications is toouse hello vast amount of tenant data stored centrally in hello cloud.</span></span> <span data-ttu-id="484c0-121">이 데이터 toogain 이해력 hello 작업 및 응용 프로그램, 테 넌 트, 사용자, 기본 설정, 동작, 등의 사용을 사용 합니다. 이러한 정보는 기능 개발, 활용성 향상 및 기타 앱 및 서비스 투자를 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-121">Use this data toogain insights into hello operation and usage of your application, your tenants, their users, preferences, behaviors, etc. These insights can guide feature development, usability improvements, and other investments in your apps and services.</span></span>

<span data-ttu-id="484c0-122">단일 다중 테넌트 데이터베이스에 있을 때 이 데이터에 액세스하는 것은 쉽지만 잠재적인 수천 개의 데이터베이스 규모로 분산되는 경우는 그렇게 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-122">Accessing this data in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="484c0-123">한 가지 방법은 toouse [탄력적 쿼리](sql-database-elastic-query-overview.md), 분산된 된 집합의 공통 스키마로 데이터베이스 간 쿼리 할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-123">One approach is toouse [Elastic Query](sql-database-elastic-query-overview.md), which enables querying across a distributed set of databases with common schema.</span></span> <span data-ttu-id="484c0-124">탄력적 쿼리에서 단일을 사용 하 여 *h e a d* hello에 미러 테이블이 나 뷰가 (테 넌 트) 데이터베이스를 분산 하는 외부 테이블은 정의 되는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-124">Elastic Query uses a single *head* database in which external tables are defined that mirror tables or views in hello distributed (tenant) databases.</span></span> <span data-ttu-id="484c0-125">쿼리를 제출할 toothis 헤드 데이터베이스는 컴파일된 tooproduce hello 쿼리 필요에 따라 toohello 테 넌 트 데이터베이스 적용의 부분으로 분산된 쿼리 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-125">Queries submitted toothis head database are compiled tooproduce a distributed query plan, with portions of hello query pushed down toohello tenant databases as needed.</span></span> <span data-ttu-id="484c0-126">탄력적 쿼리에서 hello 분할 맵을 사용 하 여 hello 테 넌 트 데이터베이스의 hello 카탈로그 데이터베이스 tooprovide hello 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-126">Elastic Query uses hello shard map in hello catalog database tooprovide hello location of hello tenant databases.</span></span> <span data-ttu-id="484c0-127">설정 및 쿼리는 일반 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)을 사용하여 바로 진행되며 Power BI 또는 Excel 같은 도구에서의 임시 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-127">Setup and query are straightforward using standard [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference), and support ad-hoc querying from tools like Power BI and Excel.</span></span>

<span data-ttu-id="484c0-128">쿼리 hello 테 넌 트 데이터베이스를 배포 하 여 탄력적 쿼리 라이브 프로덕션 데이터에 대 한 즉시 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-128">By distributing queries across hello tenant databases, Elastic Query provides immediate insight into live production data.</span></span> <span data-ttu-id="484c0-129">그러나 탄력적인 쿼리는 잠재적으로 많은 데이터베이스에서 데이터를 가져오고, 쿼리 대기 시간이 해당 하는 쿼리에 대 한 보다 높은 수 tooa 단일 다중 테 넌 트 데이터베이스를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-129">However, as Elastic Query pulls data from potentially many databases, query latency can sometimes be higher than for equivalent queries submitted tooa single multi-tenant database.</span></span> <span data-ttu-id="484c0-130">디자인 toominimize hello 반환 되는 데이터를 쿼리할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-130">Care should be taken when designing queries toominimize hello data that is returned.</span></span> <span data-ttu-id="484c0-131">탄력적 쿼리는 종종 가장 자주 사용 하는 것과 반대로 toobuilding 또는 복잡 한 분석 쿼리 또는 보고서도 적은 양의 실시간 데이터를 쿼리 하기 위한 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-131">Elastic Query is often best suited for querying small amounts of real-time data, as opposed toobuilding frequently used or complex analytics queries or reports.</span></span> <span data-ttu-id="484c0-132">쿼리 성능이 좋지, hello 속도가 확인 [실행 계획](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) hello 쿼리의 어떤 부분 toohello 원격 데이터베이스와 반환 되는 데이터의 양을 아래로 밀어넣은 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-132">If queries don't perform well, look at hello [execution plan](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee what part of hello query has been pushed down toohello remote database and how much data is being returned.</span></span> <span data-ttu-id="484c0-133">때때로 테넌트 데이터를 분석 쿼리에 최적화된 전용 데이터베이스 또는 데이터 웨어하우스로 추출하는 경우 복잡한 분석 처리를 필요로 하는 쿼리가 효율적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-133">Queries that require complex analytical processing may be better served in some cases by extracting tenant data into a dedicated database or data warehouse optimized for analytics queries.</span></span> <span data-ttu-id="484c0-134">이 패턴 hello에 대해서는 설명 [테 넌 트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-134">This pattern is explained in hello [tenant analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md).</span></span> 

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="484c0-135">Hello Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="484c0-135">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="484c0-136">hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-136">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="484c0-137">[Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-137">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-ticket-sales-data"></a><span data-ttu-id="484c0-138">티켓 판매 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="484c0-138">Create ticket sales data</span></span>

<span data-ttu-id="484c0-139">더 흥미로운 데이터 집합에 대해 쿼리를 toorun hello 티켓 생성기를 실행 하 여 티켓 판매 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-139">toorun queries against a more interesting data set, create ticket sales data by running hello ticket-generator.</span></span>

1. <span data-ttu-id="484c0-140">Hello에 *PowerShell ISE*개방형 hello... \\학습 모듈\\운영 분석\\임시 분석\\*데모 AdhocAnalytics.ps1* 스크립팅하고 hello 다음 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-140">In hello *PowerShell ISE*, open hello ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* script and set hello following values:</span></span>
   * <span data-ttu-id="484c0-141">**$DemoScenario** = 1, **모든 부문에서 이벤트 티켓을 구입합니다**.</span><span class="sxs-lookup"><span data-stu-id="484c0-141">**$DemoScenario** = 1, **Purchase tickets for events at all venues**.</span></span>
2. <span data-ttu-id="484c0-142">키를 눌러 **F5** 하 hello 스크립트를 실행 하 고 티켓 판매를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-142">Press **F5** to run hello script and generate ticket sales.</span></span> <span data-ttu-id="484c0-143">Hello 스크립트를 실행 하는 동안이 자습서에서는 hello 단계를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-143">While hello script is running, continue hello steps in this tutorial.</span></span> <span data-ttu-id="484c0-144">hello에 hello 티켓 데이터를 쿼리 *임시 분산 쿼리를 실행* 섹션에서 toothat 연습을 얻으면 계속 실행 되므로 hello 티켓 생성기 toocomplete 동안 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-144">hello ticket data is queried in hello *Run ad-hoc distributed queries* section, so wait for hello ticket generator toocomplete if it's still running when you get toothat exercise.</span></span>

## <a name="explore-hello-global-views"></a><span data-ttu-id="484c0-145">Hello 전역 보기를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-145">Explore hello global views</span></span>

<span data-ttu-id="484c0-146">hello Wingtip SaaS 응용 프로그램 hello 테 넌 트 데이터베이스 스키마에 단일 테 넌 트 관점에서 정의 되며 테 넌 트 당 데이터베이스 모델을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-146">hello Wingtip SaaS application is built using a tenant-per-database model, so hello tenant database schema is defined from a single-tenant perspective.</span></span> <span data-ttu-id="484c0-147">테넌트 전용 정보는 하나의 테이블 *Venue*에 존재하며 이 테이블에는 항상 하나의 행이 있고 따라서 기본 키가 없는 힙으로 실현됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-147">Tenant-specific information exists in one table, *Venue*, which always has a single row, and is implemented as a heap, without a primary key.</span></span> <span data-ttu-id="484c0-148">Hello 스키마의 다른 테이블과 관련 된 toobe 필요 하지 않은 toohello *장소* 존재할 수 없으므로 일반적인 사용 시에 테 넌 트 hello 데이터가 속한 확실 하지 않을 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-148">Other tables in hello schema don't need toobe related toohello *Venue* table, because in normal use, there is never any doubt which tenant hello data belongs to.</span></span>

<span data-ttu-id="484c0-149">그러나 모든 데이터베이스를 쿼리할 때 반드시 테 넌 트 별로 분할 된 단일 논리 데이터베이스의 일부 이면 처럼 탄력적 쿼리가 hello 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-149">However, when querying across all databases, it's important that Elastic Query can treat hello data as if it is part of a single logical database sharded by tenant.</span></span> <span data-ttu-id="484c0-150">tooachieve 추가 toohello 테 넌 트 데이터베이스 테 넌 트 id에 전역으로 쿼리되지 않는 hello 테이블의 각 프로젝트에이 'g l o b 뷰 집합.</span><span class="sxs-lookup"><span data-stu-id="484c0-150">tooachieve this, a set of 'global' views are added toohello tenant database that project a tenant id into each of hello tables that are queried globally.</span></span> <span data-ttu-id="484c0-151">예를 들어 hello *VenueEvents* 보기 추가 계산 *VenueId* hello에서 toohello 열 프로젝션 *이벤트* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-151">For example, hello *VenueEvents* view adds a computed *VenueId* toohello columns projected from hello *Events* table.</span></span> <span data-ttu-id="484c0-152">통해 hello hello 헤드 데이터베이스에서 외부 테이블을 정의 하 여 *VenueEvents* (아니라 hello 기반이 *이벤트* 테이블), 탄력적 쿼리는 기준으로 조인 아래로 수 toopush *VenueId* 각 원격 데이터베이스에서 (아닌 hello 헤드 데이터베이스) 병렬로 실행 될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-152">By defining hello external table in hello head database over *VenueEvents* (rather than hello underlying *Events* table), Elastic Query is able toopush down joins based on *VenueId* so they can be executed in parallel on each remote database (rather than on hello head database).</span></span> <span data-ttu-id="484c0-153">그 결과 쿼리가 많은 경우 성능이 크게 증가 하는 반환 되는 데이터 양을 hello 횟수가 상당히 줄어들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-153">This dramatically reduces hello amount of data that is returned, which results in a substantial increase in performance for many queries.</span></span> <span data-ttu-id="484c0-154">이러한 전역 보기는 모든 테넌트 데이터베이스(및 *basetenantdb*)에서 미리 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-154">These global views have been pre-created in all tenant databases (and in *basetenantdb*).</span></span>

1. <span data-ttu-id="484c0-155">SSMS를 열고 및 [연결 toohello tenants1-&lt;사용자&gt; 서버](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-155">Open SSMS and [connect toohello tenants1-&lt;USER&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).</span></span>
2. <span data-ttu-id="484c0-156">**데이터베이스**를 확장하고 **contosoconcerthall**을 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-156">Expand **Databases**, right-click **contosoconcerthall**, and select **New Query**.</span></span>
3. <span data-ttu-id="484c0-157">Hello hello 단일 테 넌 트 테이블과 hello 전역 보기 간 쿼리 tooexplore hello 차이 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-157">Run hello following queries tooexplore hello difference between hello single-tenant tables and hello global views:</span></span>

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

<span data-ttu-id="484c0-158">이러한 보기에서는 hello *VenueId* 을 hello 장소 이름의 접근 방식은 해시 고유한 값을 사용 하는 toointroduce 수으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-158">In these views, hello *VenueId* is computed as a hash of hello Venue name, but any approach could be used toointroduce a unique value.</span></span> <span data-ttu-id="484c0-159">이 방법은 toohello도 이와 비슷하게 hello 테 넌 트 키 hello 카탈로그에서 사용 하기 위해 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-159">This approach is similar toohello way hello tenant key is computed for use in hello catalog.</span></span>

<span data-ttu-id="484c0-160">hello의 tooexamine hello 정의 *운송 수단* 보기:</span><span class="sxs-lookup"><span data-stu-id="484c0-160">tooexamine hello definition of hello *Venues* view:</span></span>

1. <span data-ttu-id="484c0-161">**개체 탐색기**에서 **contosoconcethall** > **뷰**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-161">In **Object Explorer**, expand **contosoconcethall** > **Views**:</span></span>

   ![뷰](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. <span data-ttu-id="484c0-163">**dbo.Venues**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-163">Right-click **dbo.Venues**.</span></span>
3. <span data-ttu-id="484c0-164">**뷰 스크립팅** > **CREATE** > **새 쿼리 편집기 창**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-164">Select **Script View as** > **CREATE To** > **New Query Editor Window**</span></span>

<span data-ttu-id="484c0-165">스크립트의 다른 hello *장소* toosee 뷰 hello 더 추가 하는 방법을 *VenueId*합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-165">Script any of hello other *Venue* views toosee how they add hello *VenueId*.</span></span>

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a><span data-ttu-id="484c0-166">임시 분산 쿼리에 사용 되는 hello 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="484c0-166">Deploy hello database used for ad-hoc distributed queries</span></span>

<span data-ttu-id="484c0-167">이 연습 배포 hello *adhocanalytics* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-167">This exercise deploys hello *adhocanalytics* database.</span></span> <span data-ttu-id="484c0-168">이 모든 테 넌 트 데이터베이스에서 쿼리 하는 데 hello 스키마를 포함 하는 hello 헤드 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-168">This is hello head database that will contain hello schema used for querying across all tenant databases.</span></span> <span data-ttu-id="484c0-169">hello 데이터베이스는 기존 카탈로그 서버 hello 샘플 응용 프로그램의 모든 관리 관련 데이터베이스에 사용 되는 hello 서버 이며 배포 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-169">hello database is deployed toohello existing catalog server, which is hello server used for all management-related databases in hello sample app.</span></span>

1. <span data-ttu-id="484c0-170">열기... \\학습 모듈\\운영 분석\\임시 분석\\*데모 AdhocAnalytics.ps1* hello에 *PowerShell ISE* 및 집합 hello 다음 값:</span><span class="sxs-lookup"><span data-stu-id="484c0-170">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalytics.ps1* in hello *PowerShell ISE* and set hello following values:</span></span>
   * <span data-ttu-id="484c0-171">**$DemoScenario** = 2, **임시 분석 데이터베이스 배포**.</span><span class="sxs-lookup"><span data-stu-id="484c0-171">**$DemoScenario** = 2, **Deploy Ad-hoc analytics database**.</span></span>

2. <span data-ttu-id="484c0-172">키를 눌러 **F5** toorun 스크립트 hello 만들고 hello *adhocanalytics* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-172">Press **F5** toorun hello script and create hello *adhocanalytics* database.</span></span>

<span data-ttu-id="484c0-173">Hello 다음 섹션을 사용 하는 toorun 분산 쿼리에 사용할 수 있도록 스키마 toohello 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-173">In hello next section, you add schema toohello database so it can be used toorun distributed queries.</span></span>

## <a name="configure-hello-database-for-running-distributed-queries"></a><span data-ttu-id="484c0-174">분산된 쿼리를 실행 하기 위한 hello 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="484c0-174">Configure hello database for running distributed queries</span></span>

<span data-ttu-id="484c0-175">이 연습 모든 테 넌 트 데이터베이스에서 쿼리할 수 있는 스키마 (hello 외부 데이터 원본 및 외부 테이블 정의) toohello 임시 분석 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-175">This exercise adds schema (hello external data source and external table definitions) toohello ad-hoc analytics database that enables querying across all tenant databases.</span></span>

1. <span data-ttu-id="484c0-176">SQL Server Management Studio를 열고 toohello hello 이전 단계에서 만든 임시 분석 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-176">Open SQL Server Management Studio, and connect toohello Adhoc Analytics database you created in hello previous step.</span></span> <span data-ttu-id="484c0-177">hello 데이터베이스의 이름 hello adhocanalytics 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-177">hello name of hello database will be adhocanalytics.</span></span>
2. <span data-ttu-id="484c0-178">SSMS에서...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-178">Open ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* in SSMS.</span></span>
3. <span data-ttu-id="484c0-179">Hello SQL 스크립트를 검토 하 고 hello 다음에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="484c0-179">Review hello SQL script and note hello following:</span></span>

   <span data-ttu-id="484c0-180">탄력적 쿼리는 데이터베이스 범위 자격 증명 tooaccess 각 hello 테 넌 트 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-180">Elastic Query uses a database-scoped credential tooaccess each of hello tenant databases.</span></span> <span data-ttu-id="484c0-181">이 자격 증명 toobe hello는 모든 데이터베이스에서 사용할 수 있는 되어야 하며 일반적으로 데 필요한 tooenable 이러한 임시 쿼리 hello 최소 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-181">This credential needs toobe available in all hello databases and should normally be granted hello minimum rights required tooenable these ad-hoc queries.</span></span>

    ![자격 증명 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   <span data-ttu-id="484c0-183">hello를 외부 데이터 원본에에서 정의 된 toouse hello 테 넌 트 분할 맵을 hello 카탈로그 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-183">hello external data source, that is defined toouse hello tenant shard map in hello catalog database.</span></span> <span data-ttu-id="484c0-184">를 사용 하 여이 hello 외부 데이터 원본으로 쿼리는 hello 쿼리가 실행 될 때 hello 카달로그에 등록 하는 분산된 tooall 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-184">By using this as hello external data source, queries are distributed tooall databases registered in hello catalog when hello query is run.</span></span> <span data-ttu-id="484c0-185">이 초기화 스크립트 hello 현재 서버를 검색 하 여 hello 카탈로그 데이터베이스의 hello 위치를 가져옵니다 서버 이름은 각 배포에 대해 다르기 때문에 (@@servername) hello 스크립트가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-185">Because server names are different for each deployment, this initialization script gets hello location of hello catalog database by retrieving hello current server (@@servername) where hello script is executed.</span></span>

    ![외부 데이터 원본 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   <span data-ttu-id="484c0-187">hello 이전 섹션에서 설명 하 고 정의 된 전역 보기 hello를 참조 하는 외부 테이블 hello **배포 SHARDED(VenueId) =**합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-187">hello external tables that reference hello global views described in hello previous section, and defined with **DISTRIBUTION = SHARDED(VenueId)**.</span></span> <span data-ttu-id="484c0-188">때문에 각 *VenueId* tooa 단일 데이터베이스 매핑됩니다 hello 다음 섹션에 나와 있는 것 처럼이 많은 시나리오에 대 한 성능이 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-188">Because each *VenueId* maps tooa single database, this improves performance for many scenarios as shown in hello next section.</span></span>

    ![외부 테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   <span data-ttu-id="484c0-190">로컬 테이블 hello *VenueTypes* 만들고 채운입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-190">hello local table *VenueTypes* that is created and populated.</span></span> <span data-ttu-id="484c0-191">이 참조 데이터 테이블 모든 테 넌 트 데이터베이스에서 일반적으로 이므로 로컬 테이블로 사용 하 고 hello 일반 데이터로 채워진 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-191">This reference data table is common in all tenant databases, so it can be represented here as a local table and populated with hello common data.</span></span> <span data-ttu-id="484c0-192">일부 쿼리 hello 줄어들 수 있습니다에 대 한 데이터의 양을 hello 테 넌 트 데이터베이스과 hello 간에 이동 *adhocanalytics* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-192">For some queries this may reduce hello amount of data moved between hello tenant databases and hello *adhocanalytics* database.</span></span>

    ![테이블 만들기](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   <span data-ttu-id="484c0-194">이런이 방식으로 참조 테이블을 포함 하는 경우 수 있는지 tooupdate hello 테이블 스키마 및 데이터 hello 테 넌 트 데이터베이스를 업데이트할 때마다.</span><span class="sxs-lookup"><span data-stu-id="484c0-194">If you include reference tables in this manner, be sure tooupdate hello table schema and data whenever you update hello tenant databases.</span></span>

4. <span data-ttu-id="484c0-195">키를 눌러 **F5** toorun 스크립트 hello 및 hello 초기화 *adhocanalytics* 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-195">Press **F5** toorun hello script and initialize hello *adhocanalytics* database.</span></span> 

<span data-ttu-id="484c0-196">이제 배포된 쿼리를 실행하고 모든 테넌트 간에 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-196">Now you can run distributed queries, and gather insights across all tenants!</span></span>

## <a name="run-ad-hoc-distributed-queries"></a><span data-ttu-id="484c0-197">임시 배포된 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="484c0-197">Run ad-hoc distributed queries</span></span>

<span data-ttu-id="484c0-198">이제 해당 hello *adhocanalytics* 데이터베이스 설정 계속 진행 하 고, 일부 분산된 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-198">Now that hello *adhocanalytics* database is set up, go ahead and run some distributed queries.</span></span> <span data-ttu-id="484c0-199">Hello 쿼리 처리를 발생 하는에 대 한 hello 실행 계획을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-199">Include hello execution plan for a better understanding of where hello query processing is happening.</span></span> 

<span data-ttu-id="484c0-200">Hello 실행 계획을 검사할 때 세부 정보에 대 한 hello 계획 아이콘 위로 마우스를 가져가고 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-200">When inspecting hello execution plan, hover over hello plan icons for details.</span></span> 

<span data-ttu-id="484c0-201">중요 한 toonote 설정은 **배포 SHARDED(VenueId) =** hello 외부 데이터 소스를 정의 하는 경우에 다양 한 시나리오에 대 한 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-201">Important toonote, is that setting **DISTRIBUTION = SHARDED(VenueId)** when we defined hello external data source, improves performance for many scenarios.</span></span> <span data-ttu-id="484c0-202">때문에 각 *VenueId* tooa 매핑합니다 단일 데이터베이스 필터링은 쉽게 실행 취소할 원격으로 반환 하면서만 hello 데이터 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-202">Because each *VenueId* maps tooa single database, filtering is easily done remotely, returning only hello data we need.</span></span>

1. <span data-ttu-id="484c0-203">SSMS에서 \\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-203">Open ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* in SSMS.</span></span>
2. <span data-ttu-id="484c0-204">연결 된 toohello 준수할 **adhocanalytics** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-204">Ensure you are connected toohello **adhocanalytics** database.</span></span>
3. <span data-ttu-id="484c0-205">선택 hello **쿼리** 메뉴 **실제 실행 계획 포함**</span><span class="sxs-lookup"><span data-stu-id="484c0-205">Select hello **Query** menu and click **Include Actual Execution Plan**</span></span>
4. <span data-ttu-id="484c0-206">Hello를 강조 표시 *현재 등록 되어 있는 지역?* 쿼리 및 키를 눌러 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-206">Highlight hello *Which venues are currently registered?* query, and press **F5**.</span></span>

   <span data-ttu-id="484c0-207">hello 쿼리 방법을 보여 주기 위해, hello 전체 장소 목록을 반환 하 고 쉬운지 tooquery 모든 테 넌 트와 각 테 넌 트의 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-207">hello query returns hello entire venue list, illustrating how quick and easy it is tooquery across all tenants and return data from each tenant.</span></span>

   <span data-ttu-id="484c0-208">Hello 계획 검사 하 고 hello 전체 비용 hello 원격 쿼리 하므로 진행 중인 tooeach 테 넌 트 데이터베이스와 hello 위치 정보를 선택 하면 단순히 we're 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-208">Inspect hello plan and see that hello entire cost is hello remote query because we're simply going tooeach tenant database and selecting hello venue information.</span></span>

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. <span data-ttu-id="484c0-210">다음 쿼리 선택 hello 및 키를 눌러 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-210">Select hello next query, and press **F5**.</span></span>

   <span data-ttu-id="484c0-211">Hello 테 넌 트 데이터베이스 및 hello 로컬에서 데이터를 조인 하는이 쿼리 *VenueTypes* 테이블 (하므로 로컬은 hello에서 테이블 *adhocanalytics* 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="484c0-211">This query joins data from hello tenant databases and hello local *VenueTypes* table (local, as its a table in hello *adhocanalytics* database).</span></span>

   <span data-ttu-id="484c0-212">Hello 계획을 검사 하 고 해당 hello 참조 하므로 각 테 넌 트의 위치 정보 (dbo 쿼리 비용의 대부분은 hello 원격 쿼리. 지역) 한 후 로컬 hello 사용 하 여 빠른 로컬 연결을 수행 *VenueTypes* 테이블 toodisplay hello에 대 한 알기 쉬운 이름.</span><span class="sxs-lookup"><span data-stu-id="484c0-212">Inspect hello plan and see that hello majority of cost is hello remote query because we query each tenant's venue info (dbo.Venues), and then do a quick local join with hello local *VenueTypes* table toodisplay hello friendly name.</span></span>

   ![원격 및 로컬 데이터에 조인](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. <span data-ttu-id="484c0-214">이제 선택 하는 hello *일 기준 hello 대부분 티켓 판매 된?* 쿼리 및 키를 눌러 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-214">Now select hello *On which day were hello most tickets sold?* query, and press **F5**.</span></span>

   <span data-ttu-id="484c0-215">이 쿼리는 좀 더 복잡한 조인 및 집계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-215">This query does a bit more complex joining and aggregation.</span></span> <span data-ttu-id="484c0-216">중요 한 toonote은 대부분 hello 처리의 원격으로 수행 되 고 다시 한 번 당사는 다시 필요한 하루 각 장소 집계 티켓 판매 개수에 대 한 단일 행만 반환 하는 hello 행만입니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-216">What's important toonote is that most of hello processing is done remotely, and once again, we bring back only hello rows we need, returning just a single row for each venue's aggregate ticket sale count per day.</span></span>

   ![쿼리](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a><span data-ttu-id="484c0-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="484c0-218">Next steps</span></span>

<span data-ttu-id="484c0-219">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-219">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="484c0-220">모든 테넌트 데이터베이스에서 분산 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="484c0-220">Run distributed queries across all tenant databases</span></span>
> * <span data-ttu-id="484c0-221">임시 분석 데이터베이스를 배포 하 고 스키마 tooit toorun 분산 쿼리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="484c0-221">Deploy an ad-hoc analytics database and add schema tooit toorun distributed queries.</span></span>


<span data-ttu-id="484c0-222">이제 hello 시도 [테 넌 트 분석 자습서](sql-database-saas-tutorial-tenant-analytics.md) tooexplore 더 복잡 한 분석 처리에 대 한 데이터 tooa 별도 분석 데이터베이스 추출...</span><span class="sxs-lookup"><span data-stu-id="484c0-222">Now try hello [Tenant Analytics tutorial](sql-database-saas-tutorial-tenant-analytics.md) tooexplore extracting data tooa separate analytics database for more complex analytics processing...</span></span>

## <a name="additional-resources"></a><span data-ttu-id="484c0-223">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="484c0-223">Additional resources</span></span>

* <span data-ttu-id="484c0-224">추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="484c0-224">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="484c0-225">탄력적 쿼리</span><span class="sxs-lookup"><span data-stu-id="484c0-225">Elastic Query</span></span>](sql-database-elastic-query-overview.md)
