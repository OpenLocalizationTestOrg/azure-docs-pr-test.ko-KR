---
title: "여러 Azure SQL 데이터베이스에 대해 분석 쿼리 실행 | Microsoft Docs"
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
ms.openlocfilehash: 4e32407d5f321198358e07980907c3420aaf56c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="0a5ba-104">오프라인 분석을 위해 테넌트 데이터베이스에서 분석 데이터베이스로 데이터 추출</span><span class="sxs-lookup"><span data-stu-id="0a5ba-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="0a5ba-105">이 자습서에서는 탄력적 작업을 사용하여 각 테넌트 데이터베이스에 대해 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-105">In this tutorial, you use an elastic job to run queries against each tenant database.</span></span> <span data-ttu-id="0a5ba-106">이 작업에서는 티켓 판매 데이터를 추출하여 분석을 위해 분석 데이터베이스(또는 데이터 웨어하우스)에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-106">The job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="0a5ba-107">그런 다음 이 분석 데이터베이스를 쿼리하면 모든 테넌트의 일상적인 운영 데이터로부터 유용한 정보를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-107">The analytics database is then queried to extract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="0a5ba-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a5ba-109">테넌트 분석 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-109">Create the tenant analytics database</span></span>
> * <span data-ttu-id="0a5ba-110">데이터를 검색하고 분석 데이터베이스를 채우는 예약된 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-110">Create a scheduled job to retrieve data and populate the analytics database</span></span>

<span data-ttu-id="0a5ba-111">이 자습서를 수행하려면 다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-111">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="0a5ba-112">Wingtip SaaS 앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-112">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="0a5ba-113">5분 내에 배포하려면 [Wingtip SaaS 응용 프로그램 배포 및 탐색](sql-database-saas-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-113">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="0a5ba-114">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="0a5ba-115">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="0a5ba-116">최신 버전의 SSMS(SQL Server Management Studio)가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-116">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="0a5ba-117">SSMS 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="0a5ba-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="0a5ba-118">테넌트 운영 분석 패턴</span><span class="sxs-lookup"><span data-stu-id="0a5ba-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="0a5ba-119">SaaS 응용 프로그램을 사용했을 때의 커다란 기회 중 하나는 클라우드에 저장되어 있는 풍부한 테넌트 데이터를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-119">One of the great opportunities with SaaS applications is to use the rich tenant data that is stored in the cloud.</span></span> <span data-ttu-id="0a5ba-120">이 데이터를 사용하여 응용 프로그램의 사용 및 작업, 그리고 테넌트에 대한 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-120">Use this data to gain insights into the operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="0a5ba-121">이 데이터는 기능 개발, 향상된 유용성, 앱 및 플랫폼의 기타 투자에 대한 지침을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-121">This data can guide feature development, usability improvements, and other investments in the app and platform.</span></span> <span data-ttu-id="0a5ba-122">단일 다중 테넌트 데이터베이스에 있을 때 이 데이터에 액세스하는 것은 쉽지만 잠재적인 수천 개의 데이터베이스 규모로 분산되는 경우는 그렇게 쉽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="0a5ba-123">이 데이터에 액세스하는 한 가지 방법은 작업 실행의 결과 반환 쿼리 결과가 출력 데이터베이스 및 테이블에 캡처되도록 할 수 있는 탄력적 작업을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-123">One approach to accessing this data is to use Elastic jobs, which enable result-returning query results from job execution to be captured in an output database and table.</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="0a5ba-124">Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-124">Get the Wingtip application scripts</span></span>

<span data-ttu-id="0a5ba-125">Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-125">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="0a5ba-126">[Wingtip SaaS 스크립트를 다운로드하는 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="0a5ba-126">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="0a5ba-127">테넌트 분석 결과에 대한 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="0a5ba-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="0a5ba-128">이 자습서를 사용하려면 결과 반환 쿼리가 포함된 스크립트의 작업 실행 결과를 캡처할 데이터베이스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-128">This tutorial requires you to have a database deployed to capture the results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="0a5ba-129">이 용도로 사용할 tenantanalytics라는 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="0a5ba-130">*PowerShell ISE*에서 ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1*을 열고 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="0a5ba-131">**$DemoScenario** = **2** *운영 분석 데이터베이스 배포*</span><span class="sxs-lookup"><span data-stu-id="0a5ba-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="0a5ba-132">**F5**를 눌러 테넌트 분석 데이터베이스를 만드는 데모 스크립트(*Deploy-TenantAnalyticsDB.ps1* 스크립트 호출)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-132">Press **F5** to run the demo script (that calls the *Deploy-TenantAnalyticsDB.ps1* script) which creates the tenant analytics database.</span></span>

## <a name="create-some-data-for-the-demo"></a><span data-ttu-id="0a5ba-133">데모를 위한 몇 가지 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-133">Create some data for the demo</span></span>

1. <span data-ttu-id="0a5ba-134">*PowerShell ISE*에서 ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1*을 열고 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in the *PowerShell ISE* and set the following value:</span></span>
   * <span data-ttu-id="0a5ba-135">**$DemoScenario** = **1** *모든 장소에서 이벤트 티켓 구입*</span><span class="sxs-lookup"><span data-stu-id="0a5ba-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="0a5ba-136">**F5**를 눌러 스크립트를 실행하고 티켓 구입 기록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-136">Press **F5** to run the script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-to-retrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="0a5ba-137">티켓 구입에 대한 테넌트 분석을 검색하는 예약된 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-137">Create a scheduled job to retrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="0a5ba-138">이 스크립트는 모든 테넌트에서 티켓 구입 정보를 검색하는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-138">This script creates a job to retrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="0a5ba-139">단일 테이블에 집계한 후, 테넌트 간에 티켓 구입 패턴에 대한 많은 유용한 메트릭을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across the tenants.</span></span>

1. <span data-ttu-id="0a5ba-140">SSMS를 열고 catalog-&lt;user&gt;.database.windows.net 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-140">Open SSMS and connect to the catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="0a5ba-141">...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="0a5ba-142">&lt;User&gt;를 수정하고 스크립트 상단에 Wingtip SaaS 앱을 배포할 때 사용한 사용자 이름을 사용합니다(**sp\_add\_target\_group\_member** 및 **sp\_add\_jobstep**).</span><span class="sxs-lookup"><span data-stu-id="0a5ba-142">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app at the top of the script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="0a5ba-143">마우스 오른쪽 단추로 클릭하고 **연결**을 선택한 후 catalog-&lt;User&gt;.database.windows.net server 서버에 연결합니다(아직 연결하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="0a5ba-143">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="0a5ba-144">**jobaccount** 데이터베이스에 연결되어 있는지 확인하고 **F5**를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-144">Ensure you are connected to the **jobaccount** database and press **F5** to run the script</span></span>

* <span data-ttu-id="0a5ba-145">**sp\_add\_target\_group**은 대상 그룹 이름 *TenantGroup*을 만듭니다. 이제 대상 멤버를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-145">**sp\_add\_target\_group** creates the target group name *TenantGroup*, now we need to add target members.</span></span>
* <span data-ttu-id="0a5ba-146">**sp\_add\_target\_group\_member**는 *server* 대상 멤버 유형을 추가하는데, 작업 실행 시 해당 서버(테넌트 데이터베이스를 포함하는 customer1-&lt;User&gt; 서버) 내의 모든 데이터베이스가 작업에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the customer1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job.</span></span>
* <span data-ttu-id="0a5ba-147">**sp\_add\_job**은 "Ticket Purchases from all Tenants"라는 새로운 주별 예약 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="0a5ba-148">**sp\_add\_jobstep**은 모든 테넌트의 티켓 구입 정보를 검색하는 T-SQL 명령 텍스트를 포함하는 작업 단계를 만들고 *AllTicketsPurchasesfromAllTenants* 테이블에 반환 결과 집합을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-148">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="0a5ba-149">스크립트의 남은 보기에서 개체의 존재 여부를 표시하고 작업 실행을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-149">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="0a5ba-150">**lifecycle** 열에서 상태 값을 검토하여 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-150">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="0a5ba-151">성공하고 나면, 모든 테넌트 데이터베이스 및 참조 테이블을 포함하는 두 개의 추가 데이터베이스에서 작업을 성공적으로 끝마친 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-151">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

<span data-ttu-id="0a5ba-152">스크립트를 성공적으로 실행하면 다음과 비슷한 결과가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-152">Successfully running the script should result in similar results:</span></span>

![결과](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-to-retrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="0a5ba-154">모든 테넌트의 티켓 구입 요약 개수를 검색하는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-154">Create a job to retrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="0a5ba-155">이 스크립트는 모든 테넌트의 모든 티켓 구입 합계를 검색하는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-155">This script creates a job to retrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="0a5ba-156">SSMS를 열고 *catalog-&lt;User&gt;.database.windows.net* 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-156">Open SSMS and connect to the *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="0a5ba-157">...\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-157">Open the file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="0a5ba-158">&lt;User&gt;를 수정합니다. 스크립트에서 Wingtip SaaS 앱을 배포할 때 **sp\_add\_jobstep** 저장 프로시저에서 사용한 사용자 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-158">Modify &lt;User&gt;, use the user name used when you deployed the Wingtip SaaS app in the script, in the **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="0a5ba-159">마우스 오른쪽 단추로 클릭하고 **연결**을 선택한 후 catalog-&lt;User&gt;.database.windows.net server 서버에 연결합니다(아직 연결하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="0a5ba-159">Right click, select **Connection**, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="0a5ba-160">**tenantanalytics** 데이터베이스에 연결되어 있는지 확인하고 **F5**를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-160">Ensure you are connected to the **tenantanalytics** database and press **F5** to run the script</span></span>

<span data-ttu-id="0a5ba-161">스크립트를 성공적으로 실행하면 다음과 비슷한 결과가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-161">Successfully running the script should result in similar results:</span></span>

![결과](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="0a5ba-163">**sp\_add\_job**은 "ResultsTicketsOrders"라는 새로운 주별 예약된 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="0a5ba-164">**sp\_add\_jobstep**은 모든 테넌트의 티켓 구입 정보를 검색하는 T-SQL 명령 텍스트를 포함하는 작업 단계를 만들고 CountofTicketOrders 테이블에 반환 결과 집합을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to retrieve all the ticket purchase information from all tenants and copy the returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="0a5ba-165">스크립트의 남은 보기에서 개체의 존재 여부를 표시하고 작업 실행을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="0a5ba-166">**lifecycle** 열에서 상태 값을 검토하여 상태를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-166">Review the status value from the **lifecycle** column to monitor the status.</span></span> <span data-ttu-id="0a5ba-167">성공하고 나면, 모든 테넌트 데이터베이스 및 참조 테이블을 포함하는 두 개의 추가 데이터베이스에서 작업을 성공적으로 끝마친 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-167">Once, Succeeded, the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0a5ba-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0a5ba-168">Next steps</span></span>

<span data-ttu-id="0a5ba-169">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a5ba-170">테넌트 분석 데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="0a5ba-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="0a5ba-171">테넌트 간에 분석 데이터를 검색하는 예약된 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="0a5ba-171">Create a scheduled job to retrieve analytical data across tenants</span></span>

<span data-ttu-id="0a5ba-172">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="0a5ba-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a5ba-173">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0a5ba-173">Additional resources</span></span>

* <span data-ttu-id="0a5ba-174">[Wingtip SaaS 응용 프로그램을 기반으로 작성된](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="0a5ba-174">Additional [tutorials that build upon the Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="0a5ba-175">탄력적 작업</span><span class="sxs-lookup"><span data-stu-id="0a5ba-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
