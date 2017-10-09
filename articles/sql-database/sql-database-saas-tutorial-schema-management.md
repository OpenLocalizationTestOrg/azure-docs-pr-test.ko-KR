---
title: "다중 테 넌 트 응용 프로그램에서 Azure SQL 데이터베이스 스키마 aaaManage | Microsoft Docs"
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
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a><span data-ttu-id="1831b-104">Hello Wingtip SaaS 응용 프로그램에서에서 여러 테 넌 트에 대 한 스키마를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-104">Manage schema for multiple tenants in hello Wingtip SaaS application</span></span>

<span data-ttu-id="1831b-105">hello [첫 번째 Wingtip SaaS 자습서](sql-database-saas-tutorial.md) hello 앱 수 테 넌 트 데이터베이스 프로 비전 하 고 hello 카탈로그에 등록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-105">hello [first Wingtip SaaS tutorial](sql-database-saas-tutorial.md) shows how hello app can provision a tenant database and register it in hello catalog.</span></span> <span data-ttu-id="1831b-106">모든 응용 프로그램과 마찬가지로 시간이 지남에 따라 이동 하 고 때때로 Wingtip SaaS 앱 점점 발전 hello toohello 데이터베이스 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-106">Like any application, hello Wingtip SaaS app will evolve over time, and at times will require changes toohello database.</span></span> <span data-ttu-id="1831b-107">새롭거나 변경 된 스키마, 새롭거나 변경 된 참조 데이터 및 일상적인 데이터베이스 유지 관리 작업 tooensure 최적의 앱 성능을 변경 내용이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-107">Changes may include new or changed schema, new or changed reference data, and routine database maintenance tasks tooensure optimal app performance.</span></span> <span data-ttu-id="1831b-108">SaaS 응용 프로그램을 이러한 변경 내용은 잠재적으로 대규모 대 테 넌 트 데이터베이스에서 통합 된 방식으로 배포 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-108">With a SaaS application, these changes need toobe deployed in a coordinated manner across a potentially massive fleet of tenant databases.</span></span> <span data-ttu-id="1831b-109">이러한 변경 내용 toobe에 대 한 이후 테 넌 트 데이터베이스, 사용자가 toobe hello를 프로 비전 프로세스에 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-109">For these changes toobe in future tenant databases, they need toobe incorporated into hello provisioning process.</span></span>

<span data-ttu-id="1831b-110">이 자습서에서는 두 가지 시나리오-모든 테 넌 트에 대 한 참조 데이터 업데이트를 배포 하 고 hello 참조 데이터가 포함 된 테이블 재조정 hello에 대 한 인덱스 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-110">This tutorial explores two scenarios - deploying reference data updates for all tenants, and retuning an index on hello table containing hello reference data.</span></span> <span data-ttu-id="1831b-111">hello [탄력적 작업](sql-database-elastic-jobs-overview.md) 기능이 사용 되는 tooexecute를 이러한 작업은 모든 테 넌 트 및 hello에서 *골든* 새 데이터베이스에 대 한 템플릿으로 사용 되는 테 넌 트 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="1831b-111">hello [Elastic jobs](sql-database-elastic-jobs-overview.md) feature is used tooexecute these operations across all tenants, and hello *golden* tenant database that is used as a template for new databases.</span></span>

<span data-ttu-id="1831b-112">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-112">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="1831b-113">작업 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-113">Create a job account</span></span>
> * <span data-ttu-id="1831b-114">여러 테넌트 쿼리</span><span class="sxs-lookup"><span data-stu-id="1831b-114">Query across multiple tenants</span></span>
> * <span data-ttu-id="1831b-115">모든 테넌트 데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="1831b-115">Update data in all tenant databases</span></span>
> * <span data-ttu-id="1831b-116">모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-116">Create an index on a table in all tenant databases</span></span>


<span data-ttu-id="1831b-117">이 자습서에서는 다음 필수 구성 요소 확인 되었는지 hello 만족할 toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1831b-117">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="1831b-118">hello Wingtip SaaS 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-118">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="1831b-119">5 분 이내에 toodeploy 참조 [배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="1831b-119">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="1831b-120">Azure PowerShell이 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-120">Azure PowerShell is installed.</span></span> <span data-ttu-id="1831b-121">자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1831b-121">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="1831b-122">SQL Server Management Studio (SSMS) hello 최신 버전이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-122">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="1831b-123">SSMS 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="1831b-123">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

<span data-ttu-id="1831b-124">*이 자습서에서는 제한 된 미리 보기 (탄력적 데이터베이스 작업)에 있는 hello SQL 데이터베이스 서비스의 기능을 사용 합니다. 이 자습서 toodo을 원할 경우 구독 id를 제공 tooSaaSFeedback@microsoft.com 주체 = 탄력적 작업 미리 보기. 구독에서 사용할 수 있는 확인 메시지가 나타나면 [다운로드 하 여 hello 최신 시험판 작업 cmdlet 설치](https://github.com/jaredmoo/azure-powershell/releases)합니다. 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="1831b-124">*This tutorial uses features of hello SQL Database service that are in a limited preview (Elastic Database jobs). If you wish toodo this tutorial, provide your subscription id tooSaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install hello latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>


## <a name="introduction-toosaas-schema-management-patterns"></a><span data-ttu-id="1831b-125">소개 tooSaaS 스키마 관리 패턴</span><span class="sxs-lookup"><span data-stu-id="1831b-125">Introduction tooSaaS Schema Management patterns</span></span>

<span data-ttu-id="1831b-126">hello 데이터베이스 마다 단일 테 넌 트 SaaS 패턴 여러 면에서 결과 hello 데이터 격리 이점을 있지만 hello에 동시 hello 유지 및 많은 데이터베이스 관리의 복잡성이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-126">hello single tenant per database SaaS pattern benefits in many ways from hello data isolation that results, but at hello same time introduces hello additional complexity of maintaining and managing many databases.</span></span> <span data-ttu-id="1831b-127">[탄력적 작업](sql-database-elastic-jobs-overview.md) hello SQL 데이터 계층의 관리를 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-127">[Elastic Jobs](sql-database-elastic-jobs-overview.md) facilitates administration and management of hello SQL data tier.</span></span> <span data-ttu-id="1831b-128">Toosecurely를 활성화 하 고 안전 하 게 데이터베이스 그룹에 대 한 작업 (T-SQL 스크립트) 사용자 상호 작용 및 입력을에 관계 없이 실행 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-128">Jobs enable you toosecurely and reliably, run tasks (T-SQL scripts) independent of user interaction or input, against a group of databases.</span></span> <span data-ttu-id="1831b-129">이 메서드는 응용 프로그램에서 모든 테 넌 트 간에 사용 되는 toodeploy 스키마 및 일반 참조 데이터 변경 내용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-129">This method can be used toodeploy schema and common reference data changes across all tenants in an application.</span></span> <span data-ttu-id="1831b-130">탄력적 작업에 사용 되는 toomaintain 될 수도 있습니다는 *골든* hello 데이터베이스의 복사본이 toocreate 새 테 넌 트를 hello 최신 스키마 및 참조 데이터를 항상에 확인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-130">Elastic Jobs can also be used toomaintain a *golden* copy of hello database used toocreate new tenants, ensuring it always has hello latest schema and reference data.</span></span>

![화면](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a><span data-ttu-id="1831b-132">탄력적 작업의 제한된 미리 보기</span><span class="sxs-lookup"><span data-stu-id="1831b-132">Elastic Jobs limited preview</span></span>

<span data-ttu-id="1831b-133">현재 Azure SQL Database(추가 서비스 또는 구성 요소 불필요)의 통합 기능인 새로운 탄력적 작업 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-133">There is a new version of Elastic Jobs that is now an integrated feature of Azure SQL Database (that requires no additional services or components).</span></span> <span data-ttu-id="1831b-134">이 새로운 탄력적 작업 버전은 현재 제한된 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-134">This new version of Elastic Jobs is currently in limited preview.</span></span> <span data-ttu-id="1831b-135">이 제한 된 미리 보기는 현재 PowerShell toocreate 작업 계정 및 T-SQL toocreate 지원 하 고 작업을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-135">This limited preview currently supports PowerShell toocreate job accounts, and T-SQL toocreate and manage jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="1831b-136">*이 자습서에서는 제한 된 미리 보기 (탄력적 데이터베이스 작업)에 있는 hello SQL 데이터베이스 서비스의 기능을 사용 합니다. 이 자습서 toodo을 원할 경우 구독 id를 제공 tooSaaSFeedback@microsoft.com 주체 = 탄력적 작업 미리 보기. 구독에서 사용할 수 있는 확인 메시지가 나타나면 [다운로드 하 여 hello 최신 시험판 작업 cmdlet 설치](https://github.com/jaredmoo/azure-powershell/releases)합니다. 이 미리 보기는 제한적으로만 제공되므로 관련 질문이 있거나 지원이 필요한 경우 SaaSFeedback@microsoft.com에 문의해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="1831b-136">*This tutorial uses features of hello SQL Database service that are in a limited preview (Elastic Database jobs). If you wish toodo this tutorial, provide your subscription id tooSaaSFeedback@microsoft.com with subject=Elastic Jobs Preview. After you receive confirmation that your subscription has been enabled, [download and install hello latest pre-release jobs cmdlets](https://github.com/jaredmoo/azure-powershell/releases). This preview is limited, so contact SaaSFeedback@microsoft.com for related questions or support.*</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="1831b-137">Hello Wingtip 응용 프로그램 스크립트 가져오기</span><span class="sxs-lookup"><span data-stu-id="1831b-137">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="1831b-138">hello Wingtip SaaS 스크립트 및 응용 프로그램 소스 코드에서에서 사용할 수 있는 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-138">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="1831b-139">[Toodownload hello Wingtip SaaS 스크립트 단계](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-139">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="create-a-job-account-database-and-new-job-account"></a><span data-ttu-id="1831b-140">작업 계정 데이터베이스 및 새 작업 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-140">Create a job account database and new job account</span></span>

<span data-ttu-id="1831b-141">이 자습서에서는 계정을 사용 하 여 PowerShell toocreate hello 작업 계정 데이터베이스와 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-141">This tutorial requires you use PowerShell toocreate hello job account database and job account.</span></span> <span data-ttu-id="1831b-142">MSDB 등 SQL 에이전트 탄력적 작업 사용 하 여 Azure SQL 데이터베이스 toostore 작업 정의 작업 상태 및 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-142">Like MSDB and SQL Agent, Elastic Jobs uses an Azure SQL database toostore job definitions, job status, and history.</span></span> <span data-ttu-id="1831b-143">Hello 작업 계정이 만들어지면 만들 수 있으며 작업을 즉시 모니터링.</span><span class="sxs-lookup"><span data-stu-id="1831b-143">Once hello job account is created, you can create and monitor jobs immediately.</span></span>

1. <span data-ttu-id="1831b-144">열기... \\학습 모듈\\스키마 관리\\*데모 SchemaManagement.ps1* hello에 **PowerShell ISE**합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-144">Open …\\Learning Modules\\Schema Management\\*Demo-SchemaManagement.ps1* in hello **PowerShell ISE**.</span></span>
1. <span data-ttu-id="1831b-145">키를 눌러 **F5** toorun hello 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-145">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="1831b-146">hello *데모 SchemaManagement.ps1* 스크립트 호출 hello *배포 SchemaManagement.ps1* toocreate 스크립트는 *S2* 라는 데이터베이스 **jobaccount** hello 카탈로그 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-146">hello *Demo-SchemaManagement.ps1* script calls hello *Deploy-SchemaManagement.ps1* script toocreate an *S2* database named **jobaccount** on hello catalog server.</span></span> <span data-ttu-id="1831b-147">그런 다음 hello jobaccount 데이터베이스 매개 변수 toohello 작업 계정 만들기 호출으로 전달 되는 hello 작업 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-147">It then creates hello job account, passing hello jobaccount database as a parameter toohello job account creation call.</span></span>

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a><span data-ttu-id="1831b-148">작업 toodeploy 새 참조 데이터 tooall 테 넌 트 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-148">Create a job toodeploy new reference data tooall tenants</span></span>

<span data-ttu-id="1831b-149">각 테 넌 트 데이터베이스 한 장소에서 호스트 되는 이벤트의 hello 종류를 정의 하는 장소 형식의 집합을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-149">Each tenant database includes a set of venue types that define hello kind of events that are hosted at a venue.</span></span> <span data-ttu-id="1831b-150">이 연습에서는 업데이트 tooall hello 테 넌 트 데이터베이스 tooadd 두 추가 장소 형식을 배포 있습니다: *오토바이 레이싱* 및 *수영 클럽*합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-150">In this exercise, you deploy an update tooall hello tenant databases tooadd two additional venue types: *Motorcycle Racing* and *Swimming Club*.</span></span> <span data-ttu-id="1831b-151">이러한 장소 형식은 해당 toohello 배경 이미지 hello 테 넌 트에 대 한 이벤트 응용 프로그램에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-151">These venue types correspond toohello background image you see in hello tenant events app.</span></span>

<span data-ttu-id="1831b-152">Hello 장소 유형 드롭다운 메뉴를 클릭 하 고 10 개만 장소 유형 옵션을 사용할 수 있고 특히 해당 ' 오토바이 레이싱 ' 및 ' 수영 클럽 ' hello 목록에 포함 되지 않습니다 하는지 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-152">Click hello Venue Type drop down menu and validate that only 10 venue type options are available, and specifically that ‘Motorcycle Racing’ and ‘Swimming Club’ are not included in hello list.</span></span>

<span data-ttu-id="1831b-153">이제 작업 tooupdate hello를 만들어 보겠습니다 *VenueTypes* 모든 hello 테 넌 트 데이터베이스에서 테이블을 hello 새 장소 유형을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-153">Now let’s create a job tooupdate hello *VenueTypes* table in all hello tenant databases and add hello new venue types.</span></span>

<span data-ttu-id="1831b-154">toocreate 새 작업을 사용 하 여 작업 집합이 시스템 저장 프로시저 hello 작업 계정을 만들 때 hello jobaccount 데이터베이스에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-154">toocreate a new job, we use a set of jobs system stored procedures created in hello jobaccount database when hello job account was created.</span></span>

1. <span data-ttu-id="1831b-155">SSMS를 열고 고 toohello 카탈로그 서버에 연결: 카탈로그-\<사용자\>. database.windows.net 서버</span><span class="sxs-lookup"><span data-stu-id="1831b-155">Open SSMS and connect toohello catalog server: catalog-\<user\>.database.windows.net server</span></span>
1. <span data-ttu-id="1831b-156">또한 toohello 테 넌 트 서버를 연결할: tenants1-\<사용자\>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="1831b-156">Also connect toohello tenant server: tenants1-\<user\>.database.windows.net</span></span>
1. <span data-ttu-id="1831b-157">Toohello 찾아보기 *contosoconcerthall* hello에 대 한 데이터베이스 *tenants1* 서버와 쿼리 hello *VenueTypes* 테이블 tooconfirm는 *오토바이 레이싱*  및 *수영 클럽* **없는** hello 결과 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-157">Browse toohello *contosoconcerthall* database on hello *tenants1* server and query hello *VenueTypes* table tooconfirm that *Motorcycle Racing* and *Swimming Club* **are not** in hello results list.</span></span>
1. <span data-ttu-id="1831b-158">파일 열기 hello 중... \\학습 모듈\\스키마 관리\\DeployReferenceData.sql</span><span class="sxs-lookup"><span data-stu-id="1831b-158">Open hello file …\\Learning Modules\\Schema Management\\DeployReferenceData.sql</span></span>
1. <span data-ttu-id="1831b-159">Hello 문을 수정: 설정 @wtpUser = &lt;사용자&gt; hello Wingtip 앱을 배포할 때 사용 하는 hello 사용자 값 대체</span><span class="sxs-lookup"><span data-stu-id="1831b-159">Modify hello statement: SET @wtpUser = &lt;user&gt; and substitute hello User value used when you deployed hello Wingtip app</span></span>
1. <span data-ttu-id="1831b-160">연결 된 toohello jobaccount 데이터베이스 및 키를 눌러 준수할 **F5** hello 스크립트를 실행 하려면</span><span class="sxs-lookup"><span data-stu-id="1831b-160">Ensure you are connected toohello jobaccount database and press **F5** to run hello script</span></span>

* <span data-ttu-id="1831b-161">**sp\_추가\_대상\_그룹** tooadd 대상 멤버 필요 이제 hello 대상 그룹 이름, DemoServerGroup를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-161">**sp\_add\_target\_group** creates hello target group name DemoServerGroup, now we need tooadd target members.</span></span>
* <span data-ttu-id="1831b-162">**sp\_추가\_대상\_그룹\_멤버** 추가 *서버* 대상 해당 서버 (이 hello tenants1내의모든데이터베이스하다고판단되는멤버유형&lt; 사용자&gt; hello 테 넌 트 데이터베이스를 포함 하는 서버) 작업의 시간에 실행에에서 포함 되어야 hello 작업 hello 두 번째로 추가 하는 것을 *데이터베이스* 대상 멤버 유형, 특히 '골든' 데이터베이스 (hello basetenantdb) 카탈로그에 있는&lt;사용자&gt; 서버 및 마지막으로 다른 *데이터베이스* 대상 그룹 멤버 형식 tooinclude hello adhocanalytics 데이터베이스는 이후 자습서에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-162">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello tenants1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job, hello second is adding a *database* target member type, specifically hello ‘golden’ database (basetenantdb) that resides on catalog-&lt;User&gt; server, and lastly another *database* target group member type tooinclude hello adhocanalytics database that is used in a later tutorial.</span></span>
* <span data-ttu-id="1831b-163">**sp\_add\_job**은 "참조 데이터 배포"라는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-163">**sp\_add\_job** creates a job called “Reference Data Deployment”</span></span>
* <span data-ttu-id="1831b-164">**sp\_추가\_jobstep** T-SQL 명령 텍스트 tooupdate hello 참조 테이블 VenueTypes를 포함 하는 hello 작업 단계를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="1831b-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooupdate hello reference table, VenueTypes</span></span>
* <span data-ttu-id="1831b-165">hello 스크립트에 hello 나머지 보기 hello 개체 및 모니터링 작업을 실행의 hello 존재 여부를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="1831b-166">이러한 쿼리 tooreview hello 상태 값을 사용 하 여 hello에 **수명 주기** 열 toodetermine hello 작업이 모든 테 넌 트 데이터베이스 및 hello 참조 테이블을 포함 하는 hello 두 추가 데이터베이스에서 성공적으로 완료 된 경우.</span><span class="sxs-lookup"><span data-stu-id="1831b-166">Use these queries tooreview hello status value in hello **lifecycle** column toodetermine when hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

1. <span data-ttu-id="1831b-167">SSMS에서 찾아보기 toohello *contosoconcerthall* hello에 대 한 데이터베이스 *tenants1* 서버와 쿼리 hello *VenueTypes* 테이블 tooconfirm는 *오토바이 레이싱* 및 *수영 클럽* **는** hello 결과 목록에서 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-167">In SSMS, browse toohello *contosoconcerthall* database on hello *tenants1* server and query hello *VenueTypes* table tooconfirm that *Motorcycle Racing* and *Swimming Club* **are** now in hello results list.</span></span>


## <a name="create-a-job-toomanage-hello-reference-table-index"></a><span data-ttu-id="1831b-168">작업 toomanage hello 참조 테이블 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-168">Create a job toomanage hello reference table index</span></span>

<span data-ttu-id="1831b-169">비슷한 toohello 이전 연습이이 연습 작업 toorebuild hello 인덱스 hello 참조 테이블에 대 한 기본 키에, 테이블에 대형 데이터 로드 후 관리자가 일반적인 데이터베이스 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-169">Similar toohello previous exercise, this exercise creates a job toorebuild hello index on hello reference table primary key, a typical database management operation an administrator might perform after a large data load into a table.</span></span>

<span data-ttu-id="1831b-170">동일한 작업 'system' hello를 사용 하 여 작업을 만드는 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-170">Create a job using hello same jobs 'system' stored procedures.</span></span>

1. <span data-ttu-id="1831b-171">SSMS를 열고 연결 toohello 카탈로그-&lt;사용자&gt;. database.windows.net 서버</span><span class="sxs-lookup"><span data-stu-id="1831b-171">Open SSMS and connect toohello catalog-&lt;User&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="1831b-172">파일 열기 hello 중... \\학습 모듈\\스키마 관리\\OnlineReindex.sql</span><span class="sxs-lookup"><span data-stu-id="1831b-172">Open hello file …\\Learning Modules\\Schema Management\\OnlineReindex.sql</span></span>
1. <span data-ttu-id="1831b-173">마우스 오른쪽 단추로 클릭 하 고, 연결을 선택 하 고, 연결 toohello 카탈로그-&lt;사용자&gt;. 아직 연결 되지 경우 database.windows.net 서버</span><span class="sxs-lookup"><span data-stu-id="1831b-173">Right click, select Connection, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="1831b-174">연결 된 toohello jobaccount 데이터베이스를 있으며 toorun hello 스크립트 F5 키를 눌러 확인</span><span class="sxs-lookup"><span data-stu-id="1831b-174">Ensure you are connected toohello jobaccount database and press F5 toorun hello script</span></span>

* <span data-ttu-id="1831b-175">sp\_add\_job은 "Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885"라는 새 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-175">sp\_add\_job creates a new job called “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”</span></span>
* <span data-ttu-id="1831b-176">sp\_추가\_jobstep T-SQL 명령 텍스트 tooupdate hello 인덱스를 포함 하는 hello 작업 단계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-176">sp\_add\_jobstep creates hello job step containing T-SQL command text tooupdate hello index</span></span>




## <a name="next-steps"></a><span data-ttu-id="1831b-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1831b-177">Next steps</span></span>

<span data-ttu-id="1831b-178">이 자습서에서는 다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1831b-178">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="1831b-179">여러 테 넌 트 플랫폼에서 작업 계정 tooquery 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-179">Create a job account tooquery across multiple tenants</span></span>
> * <span data-ttu-id="1831b-180">모든 테넌트 데이터베이스의 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="1831b-180">Update data in all tenant databases</span></span>
> * <span data-ttu-id="1831b-181">모든 테넌트 데이터베이스의 테이블에서 인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="1831b-181">Create an index on a table in all tenant databases</span></span>

[<span data-ttu-id="1831b-182">임시 분석 자습서</span><span class="sxs-lookup"><span data-stu-id="1831b-182">Ad-hoc analytics tutorial</span></span>](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a><span data-ttu-id="1831b-183">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1831b-183">Additional resources</span></span>

* [<span data-ttu-id="1831b-184">Hello Wingtip SaaS 응용 프로그램 배포를 구축 하는 추가 자습서</span><span class="sxs-lookup"><span data-stu-id="1831b-184">Additional tutorials that build upon hello Wingtip SaaS application deployment</span></span>](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [<span data-ttu-id="1831b-185">규모가 확장된 클라우드 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="1831b-185">Managing scaled-out cloud databases</span></span>](sql-database-elastic-jobs-overview.md)
* [<span data-ttu-id="1831b-186">규모가 확장된 클라우드 데이터베이스 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="1831b-186">Create and manage scaled-out cloud databases</span></span>](sql-database-elastic-jobs-create-and-manage.md)
