---
title: "다중 테넌트 앱에서 Azure SQL Database 스키마 관리 | Microsoft Docs"
description: "Azure SQL Database를 사용하는 다중 테넌트 응용 프로그램에서 여러 테넌트에 대한 스키마 관리"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: 78d76efb88bf11fa18a416b59e6f881539141232
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-schema-for-multiple-tenants-in-the-wingtip-saas-application"></a><span data-ttu-id="ac9a3-104">Wingtip SaaS 응용 프로그램에서 여러 테넌트에 대한 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="ac9a3-104">Manage schema for multiple tenants in the Wingtip SaaS application</span></span>

<span data-ttu-id="ac9a3-105">[첫 번째 Wingtip SaaS 자습서](sql-database-saas-tutorial.md)는 앱이 테넌트 데이터베이스를 프로비전하고 카탈로그에 등록하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-105">The [first Wingtip SaaS tutorial](sql-database-saas-tutorial.md) shows how the app can provision a tenant database and register it in the catalog.</span></span> <span data-ttu-id="ac9a3-106">다른 응용 프로그램과 마찬가지로 Wingtip SaaS 앱도 시간이 지나면서 개선될 것이며 때때로 데이터베이스를 변경해야 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-106">Like any application, the Wingtip SaaS app will evolve over time, and at times will require changes to the database.</span></span> <span data-ttu-id="ac9a3-107">변경 내용에는 최적의 앱 성능을 보장하기 위해 새로운 스키마나 변경된 스키마, 새로운 참조 데이터나 변경된 참조 데이터, 일상적인 데이터베이스 유지 관리 작업이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-107">Changes may include new or changed schema, new or changed reference data, and routine database maintenance tasks to ensure optimal app performance.</span></span> <span data-ttu-id="ac9a3-108">SaaS 응용 프로그램에서 이러한 변경 내용은 테넌트 데이터베이스의 잠재적인 대규모 fleet에 통합된 방식으로 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-108">With a SaaS application, these changes need to be deployed in a coordinated manner across a potentially massive fleet of tenant databases.</span></span> <span data-ttu-id="ac9a3-109">이러한 변경 내용을 이후 테넌트 데이터베이스에 포함하려면 프로비전 프로세스에 해당 변경 내용을 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-109">For these changes to be in future tenant databases, they need to be incorporated into the provisioning process.</span></span>

<span data-ttu-id="ac9a3-110">이 자습서에서는 모든 테넌트에 대한 참조 데이터 업데이트를 배포하고 참조 데이터가 포함된 테이블에서 인덱스를 재조정하는 두 시나리오에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-110">This tutorial explores two scenarios - deploying reference data updates for all tenants, and retuning an index on the table containing the reference data.</span></span> <span data-ttu-id="ac9a3-111">[탄력적 작업](sql-database-elastic-jobs-overview.md) 기능은 모든 테넌트 및 새 데이터베이스에 대한 템플릿으로 사용되는 *golden* 테넌트 데이터베이스 간에 이러한 작업을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-111">The [Elastic jobs](sql-database-elastic-jobs-overview.md) feature is used to execute these operations across all tenants, and the *golden* tenant database that is used as a template for new databases.</span></span>

<span data-ttu-id="ac9a3-112">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-112">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="ac9a3-113">작업 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-113">Create a job account</span></span>
> * <span data-ttu-id="ac9a3-114">여러 테넌트 쿼리</span><span class="sxs-lookup"><span data-stu-id="ac9a3-114">Query across multiple tenants</span></span>
> * <span data-ttu-id="ac9a3-115">모든 테넌트 데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="ac9a3-115">Update data in all tenant databases</span></span>
> * <span data-ttu-id="ac9a3-116">모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-116">Create an index on a table in all tenant databases</span></span>


<span data-ttu-id="ac9a3-117">이 자습서를 수행하려면 다음 필수 조건이 충족되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-117">To complete this tutorial, make sure the following prerequisites are met:</span></span>

* <span data-ttu-id="ac9a3-118">Wingtip SaaS 앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-118">The Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="ac9a3-119">5분 내에 배포하려면 [Wingtip SaaS 응용 프로그램 배포 및 탐색](sql-database-saas-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-119">To deploy in less than five minutes, see [Deploy and explore the Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="ac9a3-120">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-120">Azure PowerShell is installed.</span></span> <span data-ttu-id="ac9a3-121">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-121">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="ac9a3-122">최신 버전의 SSMS(SQL Server Management Studio)가 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-122">The latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="ac9a3-123">SSMS 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="ac9a3-123">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

<span data-ttu-id="ac9a3-124">*이 자습서에서는 제한된 미리 보기(Elastic Database 작업)에 있는 SQL Database 서비스의 기능을 사용합니다. 이 자습서를 수행하려는 경우 subject=탄력적인 작업 미리 보기를 사용하여 구독 ID를 SaaSFeedback@microsoft.com에 제공하세요. 구독이 활성화되었다는 확인을 받은 후 [최신 시험판 작업 cmdlet을 다운로드하여 설치하세요](https://github.com/jaredmoo/azure-powershell/releases). 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ac9a3-124">*This tutorial uses features of the SQL Database service that are in a limited preview (Elastic Database jobs). If you wish to do this tutorial, provide your subscription id to SaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install the latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>


## <a name="introduction-to-saas-schema-management-patterns"></a><span data-ttu-id="ac9a3-125">SaaS 스키마 관리 패턴 소개</span><span class="sxs-lookup"><span data-stu-id="ac9a3-125">Introduction to SaaS Schema Management patterns</span></span>

<span data-ttu-id="ac9a3-126">데이터베이스 SaaS 패턴당 단일 테넌트는 그 결과 데이터 격리로부터 여러 면에서 장점이 있지만, 동시에 많은 데이터베이스의 유지 관리 및 관리에서 복잡성이 더 커집니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-126">The single tenant per database SaaS pattern benefits in many ways from the data isolation that results, but at the same time introduces the additional complexity of maintaining and managing many databases.</span></span> <span data-ttu-id="ac9a3-127">[탄력적 작업](sql-database-elastic-jobs-overview.md)은 SQL 데이터 계층의 관리를 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-127">[Elastic Jobs](sql-database-elastic-jobs-overview.md) facilitates administration and management of the SQL data tier.</span></span> <span data-ttu-id="ac9a3-128">이 작업을 통해 데이터베이스 그룹에 대한 작업(T-SQL 스크립트)을 사용자 상호 작용 또는 입력과 관계 없이 안전하고 안정적으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-128">Jobs enable you to securely and reliably, run tasks (T-SQL scripts) independent of user interaction or input, against a group of databases.</span></span> <span data-ttu-id="ac9a3-129">이 메서드는 응용 프로그램의 모든 테넌트에서 스키마 및 일반 참조 데이터 변경 내용을 배포하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-129">This method can be used to deploy schema and common reference data changes across all tenants in an application.</span></span> <span data-ttu-id="ac9a3-130">탄력적 작업은 항상 최신 스키마 및 참조 데이터가 포함되도록 데이터베이스의 *golden* 복사본을 유지 관리하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-130">Elastic Jobs can also be used to maintain a *golden* copy of the database used to create new tenants, ensuring it always has the latest schema and reference data.</span></span>

![화면](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a><span data-ttu-id="ac9a3-132">탄력적 작업의 제한된 미리 보기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-132">Elastic Jobs limited preview</span></span>

<span data-ttu-id="ac9a3-133">현재 Azure SQL Database(추가 서비스 또는 구성 요소 불필요)의 통합 기능인 새로운 탄력적 작업 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-133">There is a new version of Elastic Jobs that is now an integrated feature of Azure SQL Database (that requires no additional services or components).</span></span> <span data-ttu-id="ac9a3-134">이 새로운 탄력적 작업 버전은 현재 제한된 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-134">This new version of Elastic Jobs is currently in limited preview.</span></span> <span data-ttu-id="ac9a3-135">이 제한된 미리 보기에서는 현재 작업 계정을 만드는 PowerShell 및 작업을 만들고 관리하는 T-SQL을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-135">This limited preview currently supports PowerShell to create job accounts, and T-SQL to create and manage jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="ac9a3-136">*이 자습서에서는 제한된 미리 보기(Elastic Database 작업)에 있는 SQL Database 서비스의 기능을 사용합니다. 이 자습서를 수행하려는 경우 subject=탄력적인 작업 미리 보기를 사용하여 구독 ID를 SaaSFeedback@microsoft.com에 제공하세요. 구독이 활성화되었다는 확인을 받은 후 [최신 시험판 작업 cmdlet을 다운로드하여 설치하세요](https://github.com/jaredmoo/azure-powershell/releases). 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ac9a3-136">*This tutorial uses features of the SQL Database service that are in a limited preview (Elastic Database jobs). If you wish to do this tutorial, provide your subscription id to SaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install the latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>

## <a name="get-the-wingtip-application-scripts"></a><span data-ttu-id="ac9a3-137">Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-137">Get the Wingtip application scripts</span></span>

<span data-ttu-id="ac9a3-138">Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-138">The Wingtip SaaS scripts and application source code are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="ac9a3-139">[Wingtip SaaS 스크립트를 다운로드하는 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="ac9a3-139">[Steps to download the Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-a-job-account-database-and-new-job-account"></a><span data-ttu-id="ac9a3-140">작업 계정 데이터베이스 및 새 작업 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-140">Create a job account database and new job account</span></span>

<span data-ttu-id="ac9a3-141">이 자습서를 사용하려면 PowerShell을 사용하여 작업 계정 데이터베이스 및 작업 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-141">This tutorial requires you use PowerShell to create the job account database and job account.</span></span> <span data-ttu-id="ac9a3-142">MSDB 및 SQL 에이전트와 같이, 탄력적 작업에서는 Azure SQL Database를 사용하여 작업 정의, 작업 상태 및 기록을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-142">Like MSDB and SQL Agent, Elastic Jobs uses an Azure SQL database to store job definitions, job status, and history.</span></span> <span data-ttu-id="ac9a3-143">작업 계정이 만들어지면 작업을 만들어 즉시 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-143">Once the job account is created, you can create and monitor jobs immediately.</span></span>

1. <span data-ttu-id="ac9a3-144">**PowerShell ISE**에서 ...\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1*을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-144">Open …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1* in the **PowerShell ISE**.</span></span>
1. <span data-ttu-id="ac9a3-145">**F5** 키를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-145">Press **F5** to run the script.</span></span>

<span data-ttu-id="ac9a3-146">*Demo-SchemaManagement.ps1* 스크립트는 *Deploy-SchemaManagement.ps1*을 호출하여 카탈로그 서버에서 **jobaccount**라는 이름의 *S2* 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-146">The *Demo-SchemaManagement.ps1* script calls the *Deploy-SchemaManagement.ps1* script to create an *S2* database named **jobaccount** on the catalog server.</span></span> <span data-ttu-id="ac9a3-147">그런 다음, 작업 계정을 만들어 jobaccount 데이터베이스를 매개 변수로 작업 계정 생성 호출로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-147">It then creates the job account, passing the jobaccount database as a parameter to the job account creation call.</span></span>

## <a name="create-a-job-to-deploy-new-reference-data-to-all-tenants"></a><span data-ttu-id="ac9a3-148">모든 테넌트에 새 참조 데이터를 배포하는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-148">Create a job to deploy new reference data to all tenants</span></span>

<span data-ttu-id="ac9a3-149">각 테넌트 데이터베이스에는 한 장소에서 호스팅되는 이벤트 종류를 정의하는 일련의 장소 유형이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-149">Each tenant database includes a set of venue types that define the kind of events that are hosted at a venue.</span></span> <span data-ttu-id="ac9a3-150">이 연습에서는 두 개의 추가 장소 유형인 *Motorcycle Racing* 및 *Swimming Club*을 추가하기 위해 모든 테넌트 데이터베이스에 업데이트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-150">In this exercise, you deploy an update to all the tenant databases to add two additional venue types: *Motorcycle Racing* and *Swimming Club*.</span></span> <span data-ttu-id="ac9a3-151">이러한 장소 유형은 테넌트 이벤트 앱에 표시된 배경 이미지에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-151">These venue types correspond to the background image you see in the tenant events app.</span></span>

<span data-ttu-id="ac9a3-152">장소 유형 드롭다운 메뉴를 클릭하고 10개 장소 유형 옵션만 사용할 수 있고 특히 'Motorcycle Racing' 및 'Swimming Club'이 목록에 포함되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-152">Click the Venue Type drop down menu and validate that only 10 venue type options are available, and specifically that ‘Motorcycle Racing’ and ‘Swimming Club’ are not included in the list.</span></span>

<span data-ttu-id="ac9a3-153">이제 모든 테넌트 데이터베이스의 *VenueTypes* 테이블을 업데이트하고 새 장소 유형을 추가하는 작업을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-153">Now let’s create a job to update the *VenueTypes* table in all the tenant databases and add the new venue types.</span></span>

<span data-ttu-id="ac9a3-154">새 작업을 만들려면 작업 계정을 만들 때 jobaccount 데이터베이스에서 생성한 작업 시스템 저장 프로시저 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-154">To create a new job, we use a set of jobs system stored procedures created in the jobaccount database when the job account was created.</span></span>

1. <span data-ttu-id="ac9a3-155">SSMS를 열고 카탈로그 서버에 연결: catalog-\<사용자\>.database.windows.net 서버</span><span class="sxs-lookup"><span data-stu-id="ac9a3-155">Open SSMS and connect to the catalog server: catalog-\<user\>.database.windows.net server</span></span>
1. <span data-ttu-id="ac9a3-156">테넌트 서버에 연결: tenants1-\<사용자\>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="ac9a3-156">Also connect to the tenant server: tenants1-\<user\>.database.windows.net</span></span>
1. <span data-ttu-id="ac9a3-157">*tenants1* 서버에서 *contosoconcerthall* 데이터베이스로 이동한 후 *VenueTypes* 테이블을 쿼리하여 *Motorcycle Racing* 및 *Swimming Club*이 결과 목록에 **없는지** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-157">Browse to the *contosoconcerthall* database on the *tenants1* server and query the *VenueTypes* table to confirm that *Motorcycle Racing* and *Swimming Club* **are not** in the results list.</span></span>
1. <span data-ttu-id="ac9a3-158">...\\Learning Modules\\Schema Management\\DeployReferenceData.sql 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-158">Open the file …\\Learning Modules\\Schema Management\\DeployReferenceData.sql</span></span>
1. <span data-ttu-id="ac9a3-159">문을 SET @wtpUser = &lt;user&gt;로 수정하고 Wingtip 앱을 배포할 때 사용했던 User 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-159">Modify the statement: SET @wtpUser = &lt;user&gt; and substitute the User value used when you deployed the Wingtip app</span></span>
1. <span data-ttu-id="ac9a3-160">jobaccount 데이터베이스에 연결되어 있는지 확인하고 **F5**를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-160">Ensure you are connected to the jobaccount database and press **F5** to run the script</span></span>

* <span data-ttu-id="ac9a3-161">**sp\_add\_target\_group**은 대상 그룹 이름 DemoServerGroup를 만듭니다. 이제 대상 멤버를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-161">**sp\_add\_target\_group** creates the target group name DemoServerGroup, now we need to add target members.</span></span>
* <span data-ttu-id="ac9a3-162">**sp\_add\_target\_group\_member**는 *server* 대상 멤버 유형을 추가하는데, 작업 실행 시 해당 서버(테넌트 데이터베이스를 포함하고 있는 tenants1-&lt;User&gt; 서버) 내의 모든 데이터베이스가 작업에 포함되어야 합니다. 두 번째로는 *database* 대상 멤버 유형이 추가됩니다. 이 유형은 구체적으로는 catalog-&lt;User&gt; 서버에 있는 'golden' 데이터베이스(basetenantdb)입니다. 그리고 마지막으로 자습서 뒷부분에서 사용되는 adhocanalytics 데이터베이스를 포함하는 또 다른 *database* 대상 그룹 멤버 유형이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-162">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is the tenants1-&lt;User&gt; server containing the tenant databases) at time of job execution should be included in the job, the second is adding a *database* target member type, specifically the ‘golden’ database (basetenantdb) that resides on catalog-&lt;User&gt; server, and lastly another *database* target group member type to include the adhocanalytics database that is used in a later tutorial.</span></span>
* <span data-ttu-id="ac9a3-163">**sp\_add\_job**은 "참조 데이터 배포"라는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-163">**sp\_add\_job** creates a job called “Reference Data Deployment”</span></span>
* <span data-ttu-id="ac9a3-164">**sp\_add\_jobstep**은 VenueTypes 참조 테이블을 업데이트하기 위한 T-SQL 명령 텍스트가 포함된 작업 단계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-164">**sp\_add\_jobstep** creates the job step containing T-SQL command text to update the reference table, VenueTypes</span></span>
* <span data-ttu-id="ac9a3-165">스크립트의 남은 보기에서 개체의 존재 여부를 표시하고 작업 실행을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-165">The remaining views in the script display the existence of the objects and monitor job execution.</span></span> <span data-ttu-id="ac9a3-166">이러한 쿼리를 사용하여 **lifecycle** 열의 상태 값을 검토해 모든 테넌트 데이터베이스와 참조 테이블이 포함된 추가 데이터베이스 2개에서 작업이 정상적으로 완료된 시기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-166">Use these queries to review the status value in the **lifecycle** column to determine when the job has successfully finished on all tenant databases and the two additional databases containing the reference table.</span></span>

1. <span data-ttu-id="ac9a3-167">SSMS에서 *tenants1* 서버의 *contosoconcerthall* 데이터베이스로 이동한 후 *VenueTypes* 테이블을 쿼리하여 이제 *Motorcycle Racing* 및 *Swimming Club***이** 결과 목록에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-167">In SSMS, browse to the *contosoconcerthall* database on the *tenants1* server and query the *VenueTypes* table to confirm that *Motorcycle Racing* and *Swimming Club* **are** now in the results list.</span></span>


## <a name="create-a-job-to-manage-the-reference-table-index"></a><span data-ttu-id="ac9a3-168">참조 테이블 인덱스를 관리하는 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-168">Create a job to manage the reference table index</span></span>

<span data-ttu-id="ac9a3-169">이전 연습과 비슷하게, 이 연습에서는 참조 테이블 기본 키의 인덱스를 다시 작성하는 작업을 만듭니다. 이 작업은 테이블에 대량의 데이터를 로드한 후 관리자가 수행할 수 있는 일반적인 데이터베이스 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-169">Similar to the previous exercise, this exercise creates a job to rebuild the index on the reference table primary key, a typical database management operation an administrator might perform after a large data load into a table.</span></span>

<span data-ttu-id="ac9a3-170">동일한 작업 '시스템' 저장 프로시저를 사용하여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-170">Create a job using the same jobs 'system' stored procedures.</span></span>

1. <span data-ttu-id="ac9a3-171">SSMS를 열고 catalog-&lt;User&gt;.database.windows.net 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-171">Open SSMS and connect to the catalog-&lt;User&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="ac9a3-172">...\\Learning Modules\\Schema Management\\OnlineReindex.sql 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-172">Open the file …\\Learning Modules\\Schema Management\\OnlineReindex.sql</span></span>
1. <span data-ttu-id="ac9a3-173">마우스 오른쪽 단추로 클릭하고 연결을 선택한 후 catalog-&lt;User&gt;.database.windows.net 서버에 연결합니다(아직 연결하지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="ac9a3-173">Right click, select Connection, and connect to the catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="ac9a3-174">jobaccount 데이터베이스에 연결되어 있는지 확인하고 F5를 눌러 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-174">Ensure you are connected to the jobaccount database and press F5 to run the script</span></span>

* <span data-ttu-id="ac9a3-175">sp\_add\_job은 "Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885"라는 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-175">sp\_add\_job creates a new job called “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”</span></span>
* <span data-ttu-id="ac9a3-176">sp\_add\_jobstep은 인덱스를 업데이트할 T-SQL 명령 텍스트를 포함하는 작업 단계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-176">sp\_add\_jobstep creates the job step containing T-SQL command text to update the index</span></span>




## <a name="next-steps"></a><span data-ttu-id="ac9a3-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac9a3-177">Next steps</span></span>

<span data-ttu-id="ac9a3-178">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac9a3-178">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="ac9a3-179">여러 테넌트에서 쿼리하는 작업 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-179">Create a job account to query across multiple tenants</span></span>
> * <span data-ttu-id="ac9a3-180">모든 테넌트 데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="ac9a3-180">Update data in all tenant databases</span></span>
> * <span data-ttu-id="ac9a3-181">모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="ac9a3-181">Create an index on a table in all tenant databases</span></span>

[<span data-ttu-id="ac9a3-182">임시 분석 자습서</span><span class="sxs-lookup"><span data-stu-id="ac9a3-182">Ad-hoc analytics tutorial</span></span>](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a><span data-ttu-id="ac9a3-183">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ac9a3-183">Additional resources</span></span>

* [<span data-ttu-id="ac9a3-184">Wingtip SaaS 응용 프로그램 배포를 기반으로 작성된 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="ac9a3-184">Additional tutorials that build upon the Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="ac9a3-185">규모가 확장된 클라우드 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="ac9a3-185">Managing scaled-out cloud databases</span></span>](sql-database-elastic-jobs-overview.md)
* [<span data-ttu-id="ac9a3-186">규모가 확장된 클라우드 데이터베이스 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="ac9a3-186">Create and manage scaled-out cloud databases</span></span>](sql-database-elastic-jobs-create-and-manage.md)
