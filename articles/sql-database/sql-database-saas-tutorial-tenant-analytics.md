---
title: "여러 Azure SQL 데이터베이스에 대 한 분석 쿼리 aaaRun | Microsoft Docs"
description: "오프라인 분석을 위해 테넌트 데이터베이스에서 분석 데이터베이스로 데이터 추출"
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="6b85f-104">오프라인 분석을 위해 테넌트 데이터베이스에서 분석 데이터베이스로 데이터 추출</span><span class="sxs-lookup"><span data-stu-id="6b85f-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="6b85f-105">이 자습서에서는 각 테 넌 트 데이터베이스에 대 한 탄력적 작업 toorun 쿼리는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="6b85f-106">hello 작업 티켓 판매 데이터를 추출 및 분석을 위해 분석 데이터베이스 (또는 데이터 웨어하우스)에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="6b85f-107">hello 분석 데이터베이스는 다음의 모든 테 넌 트가이 일상적인 운영 데이터 로부터 이해를 tooextract 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="6b85f-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b85f-109">Hello 테 넌 트 분석 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="6b85f-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="6b85f-110">예약 된 작업 tooretrieve 데이터를 만들고 hello 분석 데이터베이스 채우기</span><span class="sxs-lookup"><span data-stu-id="6b85f-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="6b85f-111">이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 만족할 toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6b85f-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="6b85f-112">hello Wingtip SaaS 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="6b85f-113">5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="6b85f-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="6b85f-114">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="6b85f-115">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b85f-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="6b85f-116">SQL Server Management Studio (SSMS) hello 최신 버전이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="6b85f-117">SSMS 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="6b85f-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="6b85f-118">테넌트 운영 분석 패턴</span><span class="sxs-lookup"><span data-stu-id="6b85f-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="6b85f-119">Hello 좋은 기회 SaaS 응용 프로그램 중 하나에 hello 클라우드에 저장 되어 있는 toouse hello 효율적인 테 넌 트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="6b85f-120">이 데이터 toogain 이해력 hello 작업과 응용 프로그램 및 테 넌 트의 사용을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="6b85f-121">이 데이터는 기능 개발, 유용성 향상 및 기타 투자 hello 응용 프로그램 및 플랫폼에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="6b85f-122">단일 다중 테넌트 데이터베이스에 있을 때 이 데이터에 액세스하는 것은 쉽지만 잠재적인 수천 개의 데이터베이스 규모로 분산되는 경우는 그렇게 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="6b85f-123">한 접근 방식을 tooaccessing이이 데이터는 있도록 쿼리 결과 출력 데이터베이스 및 테이블에서 캡처된 작업 실행 toobe에서 결과 반환 하는 toouse 탄력적 작업.</span><span class="sxs-lookup"><span data-stu-id="6b85f-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="6b85f-124">Hello Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="6b85f-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="6b85f-125">hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="6b85f-126">[Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="6b85f-127">테넌트 분석 결과에 대한 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="6b85f-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="6b85f-128">이 자습서에서 작업 실행 결과 반환 하는 쿼리를 포함 하는 스크립트의 결과 데이터베이스 배포 toocapture hello toohave를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="6b85f-129">이 용도로 사용할 tenantanalytics라는 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="6b85f-130">열기... \\학습 모듈\\운영 분석\\테 넌 트 분석\\*데모 TenantAnalyticsDB.ps1* hello에 *PowerShell ISE* 설정 다음 값 hello:</span><span class="sxs-lookup"><span data-stu-id="6b85f-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="6b85f-131">**$DemoScenario** = **2** *운영 분석 데이터베이스 배포*</span><span class="sxs-lookup"><span data-stu-id="6b85f-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="6b85f-132">키를 눌러 **F5** toorun hello 데모 스크립트 (해당 호출 hello *배포 TenantAnalyticsDB.ps1* 스크립트)는 hello 테 넌 트 분석 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="6b85f-133">Hello 데모에 대 한 일부 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="6b85f-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="6b85f-134">열기... \\학습 모듈\\운영 분석\\테 넌 트 분석\\*데모 TenantAnalyticsDB.ps1* hello에 *PowerShell ISE* 설정 다음 값 hello:</span><span class="sxs-lookup"><span data-stu-id="6b85f-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="6b85f-135">**$DemoScenario** = **1** *모든 장소에서 이벤트 티켓 구입*</span><span class="sxs-lookup"><span data-stu-id="6b85f-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="6b85f-136">키를 눌러 **F5** toorun 스크립트 hello 및 구매 기록을 티켓을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="6b85f-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="6b85f-137">티켓 구매에 대 한 예약 된 작업 tooretrieve 테 넌 트 분석 만들기</span><span class="sxs-lookup"><span data-stu-id="6b85f-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="6b85f-138">이 스크립트는 모든 테 넌 트의 작업 tooretrieve 티켓 구매 정보를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="6b85f-139">단일 테이블에 집계, 후 hello 테 넌 트 간에 패턴을 구매 하는 티켓에 대 한 풍부한 통찰력 메트릭을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="6b85f-140">SSMS를 열고 연결 toohello 카탈로그-&lt;사용자&gt;. database.windows.net 서버</span><span class="sxs-lookup"><span data-stu-id="6b85f-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="6b85f-141">...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="6b85f-142">수정 &lt;사용자&gt;, hello 스크립트의 hello 위쪽 hello Wingtip SaaS 앱을 배포할 때 사용 하는 사용 하 여 hello 사용자 이름 **sp\_추가\_대상\_그룹\_멤버** 및 **sp\_추가\_작업 단계**</span><span class="sxs-lookup"><span data-stu-id="6b85f-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="6b85f-143">마우스 오른쪽 단추로 클릭 하 여, 선택 **연결**, 연결 toohello 카탈로그-&lt;사용자&gt;. database.windows.net 서버에 아직 연결 되지</span><span class="sxs-lookup"><span data-stu-id="6b85f-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="6b85f-144">연결 된 toohello을 준수할 **jobaccount** 데이터베이스 및 키를 눌러 **F5** hello 스크립트를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="6b85f-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="6b85f-145">**sp\_추가\_대상\_그룹** hello 대상 그룹 이름 만듭니다 *TenantGroup*, 이제 tooadd 대상 멤버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="6b85f-146">**sp\_추가\_대상\_그룹\_멤버** 추가 *서버* 대상 내의 해당 서버 (이 hello customer1-모든 데이터베이스 하다 고 판단 되는 멤버 유형 &lt;사용자&gt; hello 테 넌 트 데이터베이스를 포함 하는 서버) 작업의 시간에 실행 hello 작업에 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="6b85f-147">**sp\_add\_job**은 "Ticket Purchases from all Tenants"라는 새로운 주별 예약 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="6b85f-148">**sp\_추가\_jobstep** 모든 테 넌 트 및 결과 집합 이라고 하는 테이블을 반환 하는 복사 hello hello 작업 단계 명령 텍스트 tooretrieve T-SQL 포함 된 모든 hello 티켓 구매 정보를 생성  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="6b85f-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="6b85f-149">hello 스크립트에 hello 나머지 보기 hello 개체 및 모니터링 작업을 실행의 hello 존재 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="6b85f-150">Hello에서 hello 상태 값을 검토 **수명 주기** 열 toomonitor hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="6b85f-151">한 번 hello 작업이 모든 테 넌 트 데이터베이스에서 성공적으로 완료 된 한 hello hello를 포함 하는 두 개의 추가 데이터베이스 테이블을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="6b85f-152">비슷한 결과에서 발생 해야 성공적으로 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-152">Successfully running hello script should result in similar results:</span></span>

![결과](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="6b85f-154">모든 테 넌 트에서 티켓의 요약 개수 구입 작업 tooretrieve 만들기</span><span class="sxs-lookup"><span data-stu-id="6b85f-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="6b85f-155">이 스크립트에서 모든 테 넌 트의 모든 티켓 구입 작업 tooretrieve 합계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="6b85f-156">SSMS를 열고 toohello 연결 *카탈로그-&lt;사용자&gt;. database.windows.net* 서버</span><span class="sxs-lookup"><span data-stu-id="6b85f-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="6b85f-157">파일 열기 hello 중... \\학습 모듈\\프로 비전 및 카탈로그\\운영 분석\\분석 테 넌 트\\*결과 TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="6b85f-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="6b85f-158">수정 &lt;사용자&gt;, hello 스크립트 hello에 hello Wingtip SaaS 앱을 배포할 때 사용 하는 사용 하 여 hello 사용자 이름 **sp\_추가\_jobstep** 저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="6b85f-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="6b85f-159">마우스 오른쪽 단추로 클릭 하 여, 선택 **연결**, 연결 toohello 카탈로그-&lt;사용자&gt;. database.windows.net 서버에 아직 연결 되지</span><span class="sxs-lookup"><span data-stu-id="6b85f-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="6b85f-160">연결 된 toohello을 준수할 **tenantanalytics** 데이터베이스 및 키를 눌러 **F5** hello 스크립트를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="6b85f-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="6b85f-161">비슷한 결과에서 발생 해야 성공적으로 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-161">Successfully running hello script should result in similar results:</span></span>

![결과](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="6b85f-163">**sp\_add\_job**은 "ResultsTicketsOrders"라는 새로운 주별 예약된 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="6b85f-164">**sp\_추가\_jobstep** 모든 테 넌 트 및 결과 집합에 CountofTicketOrders 라는 테이블을 반환 하는 복사 hello hello 작업 단계 명령 텍스트 tooretrieve T-SQL 포함 된 모든 hello 티켓 구매 정보를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="6b85f-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="6b85f-165">hello 스크립트에 hello 나머지 보기 hello 개체 및 모니터링 작업을 실행의 hello 존재 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="6b85f-166">Hello에서 hello 상태 값을 검토 **수명 주기** 열 toomonitor hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="6b85f-167">한 번 hello 작업이 모든 테 넌 트 데이터베이스에서 성공적으로 완료 된 한 hello hello를 포함 하는 두 개의 추가 데이터베이스 테이블을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b85f-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b85f-168">Next steps</span></span>

<span data-ttu-id="6b85f-169">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b85f-170">테넌트 분석 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="6b85f-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="6b85f-171">테 넌 트 간에 예약 된 작업 tooretrieve 분석 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="6b85f-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="6b85f-172">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="6b85f-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b85f-173">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="6b85f-173">Additional resources</span></span>

* <span data-ttu-id="6b85f-174">추가 [hello Wingtip SaaS 응용 프로그램을 구축 하는 자습서](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="6b85f-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="6b85f-175">탄력적 작업</span><span class="sxs-lookup"><span data-stu-id="6b85f-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
