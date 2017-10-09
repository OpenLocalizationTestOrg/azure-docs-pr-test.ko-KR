---
title: "aaaIntro Wingtip SaaS-Azure SQL 데이터베이스 다중 테 넌 트 응용 프로그램 | Microsoft Docs"
description: "Azure SQL 데이터베이스, hello Wingtip SaaS 응용 프로그램을 사용 하는 예제 다중 테 넌 트 응용 프로그램을 사용 하 여"
keywords: "SQL Database 자습서"
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a><span data-ttu-id="df8db-104">소개 toohello Wingtip SaaS 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="df8db-104">Introduction toohello Wingtip SaaS application</span></span>

<span data-ttu-id="df8db-105">hello *Wingtip SaaS* 응용 프로그램은 SQL 데이터베이스의 고유 장점 hello를 보여 주는 샘플 다중 테 넌 트 응용 프로그램, 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-105">hello *Wingtip SaaS* application is a sample multi-tenant app, that demonstrates hello unique advantages of SQL Database.</span></span> <span data-ttu-id="df8db-106">hello 앱 데이터베이스-당-테 넌 트, SaaS 응용 프로그램 패턴 tooservice 여러 테 넌 트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-106">hello app uses a database-per-tenant, SaaS application pattern, tooservice multiple tenants.</span></span> <span data-ttu-id="df8db-107">hello 응용 프로그램을 여러 가지 SaaS 디자인 및 관리 패턴을 비롯 한 SaaS 시나리오를 사용할 수 있는 Azure SQL 데이터베이스의 디자인 된 tooshowcase 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-107">hello app is designed tooshowcase features of Azure SQL Database that enable SaaS scenarios, including several SaaS design and management patterns.</span></span> <span data-ttu-id="df8db-108">tooquickly 가져오고 5 분 이내에 hello Wingtip SaaS 앱 배포, 실행!</span><span class="sxs-lookup"><span data-stu-id="df8db-108">tooquickly get up and running, hello Wingtip SaaS app deploys in less than five minutes!</span></span>

<span data-ttu-id="df8db-109">응용 프로그램 소스 코드 및 관리 스크립트 hello에서 사용할 수 있는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-109">Application source code and management scripts are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="df8db-110">toorun hello 스크립트 [다운로드 hello 학습 모듈 폴더](#download-and-unblock-the-wingtip-saas-scripts) tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-110">toorun hello scripts, [download hello Learning Modules folder](#download-and-unblock-the-wingtip-saas-scripts) tooyour local computer.</span></span>

## <a name="sql-database-wingtip-saas-tutorials"></a><span data-ttu-id="df8db-111">SQL Database Wingtip SaaS 자습서</span><span class="sxs-lookup"><span data-stu-id="df8db-111">SQL Database Wingtip SaaS tutorials</span></span>

<span data-ttu-id="df8db-112">Hello 앱을 배포한 후 hello 초기 배포를 구축 하는 자습서를 따라 hello를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-112">After deploying hello app, explore hello following tutorials that build upon hello initial deployment.</span></span> <span data-ttu-id="df8db-113">이러한 자습서에서는 SQL Database, SQL Data Warehouse 및 기타 Azure 서비스의 기본 제공 기능을 활용하는 일반적인 SaaS 패턴을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-113">These tutorials explore common SaaS patterns that take advantage of built-in features of SQL Database, SQL Data Warehouse, and other Azure services.</span></span> <span data-ttu-id="df8db-114">응용 프로그램에서 동일한 SaaS 관리 패턴 hello 구현 및 자습서를 이해 하 고 간소화 해 주는 상세한 설명 된 PowerShell 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-114">Tutorials include PowerShell scripts, with detailed explanations that greatly simplify understanding, and implementing hello same SaaS management patterns in your applications.</span></span>


| <span data-ttu-id="df8db-115">자습서</span><span class="sxs-lookup"><span data-stu-id="df8db-115">Tutorial</span></span> | <span data-ttu-id="df8db-116">설명</span><span class="sxs-lookup"><span data-stu-id="df8db-116">Description</span></span> |
|:--|:--|
|[<span data-ttu-id="df8db-117">배포 하 고 hello Wingtip SaaS 응용 프로그램 탐색</span><span class="sxs-lookup"><span data-stu-id="df8db-117">Deploy and explore hello Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)| <span data-ttu-id="df8db-118">**여기에서 시작하세요.**</span><span class="sxs-lookup"><span data-stu-id="df8db-118">**START HERE!**</span></span> <span data-ttu-id="df8db-119">배포 하 고 hello Wingtip SaaS 응용 프로그램 tooyour Azure 구독을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-119">Deploy and explore hello Wingtip SaaS application tooyour Azure subscription.</span></span> |
|[<span data-ttu-id="df8db-120">프로비전 및 카탈로그 테넌트</span><span class="sxs-lookup"><span data-stu-id="df8db-120">Provision and catalog tenants</span></span>](sql-database-saas-tutorial-provision-and-catalog.md)| <span data-ttu-id="df8db-121">Hello 응용 프로그램 카탈로그 데이터베이스를 사용 하 여 tootenants를 연결 하는 방법을 알아보고 tootheir 데이터는 테 넌 트가 hello 카탈로그를 매핑하는 방식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-121">Learn how hello application connects tootenants using a catalog database, and how hello catalog maps tenants tootheir data.</span></span> |
|[<span data-ttu-id="df8db-122">성능 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="df8db-122">Monitor and manage performance</span></span>](sql-database-saas-tutorial-performance-monitoring.md)| <span data-ttu-id="df8db-123">Toouse 모니터링 기능이 하는 방법에 대해 알아봅니다 tooset 경고 하는 경우는 어떻게 및 SQL 데이터베이스의 성능 임계값을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-123">Learn how toouse monitoring features of SQL Database, and how tooset alerts when performance thresholds are exceeded.</span></span> |
|[<span data-ttu-id="df8db-124">Log Analytics(OMS)로 모니터링</span><span class="sxs-lookup"><span data-stu-id="df8db-124">Monitor with Log Analytics (OMS)</span></span>](sql-database-saas-tutorial-log-analytics.md) | <span data-ttu-id="df8db-125">사용에 대 한 자세한 내용은 [로그 분석](../log-analytics/log-analytics-overview.md) toomonitor 많은 양의 리소스를 여러 풀에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-125">Learn about using [Log Analytics](../log-analytics/log-analytics-overview.md) toomonitor large amounts of resources, across multiple pools.</span></span> |
|[<span data-ttu-id="df8db-126">단일 테넌트 복원</span><span class="sxs-lookup"><span data-stu-id="df8db-126">Restore a single tenant</span></span>](sql-database-saas-tutorial-restore-single-tenant.md)| <span data-ttu-id="df8db-127">어떻게 toorestore 이전 테 넌 트 데이터베이스 tooa 지정 시간에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-127">Learn how toorestore a tenant database tooa prior point in time.</span></span> <span data-ttu-id="df8db-128">단계 toorestore tooa 병렬 데이터베이스, 종료 hello 기존 테 넌 트 데이터베이스 온라인으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-128">Steps toorestore tooa parallel database, leaving hello existing tenant database online, are also included.</span></span> |
|[<span data-ttu-id="df8db-129">테넌트 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="df8db-129">Manage tenant schema</span></span>](sql-database-saas-tutorial-schema-management.md)| <span data-ttu-id="df8db-130">어떻게 tooupdate 스키마 및 업데이트 참조 데이터를 모든 Wingtip SaaS 테 넌 트 간에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-130">Learn how tooupdate schema, and update reference data, across all Wingtip SaaS tenants.</span></span> |
|[<span data-ttu-id="df8db-131">임시 분석 실행</span><span class="sxs-lookup"><span data-stu-id="df8db-131">Run ad-hoc analytics</span></span>](sql-database-saas-tutorial-adhoc-analytics.md) | <span data-ttu-id="df8db-132">임시 분석 데이터베이스를 만들고 모든 테넌트에서 실시간 분산 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-132">Create an ad-hoc analytics database and run real-time distributed queries across all tenants.</span></span>  |
|[<span data-ttu-id="df8db-133">테넌트 분석 실행</span><span class="sxs-lookup"><span data-stu-id="df8db-133">Run tenant analytics</span></span>](sql-database-saas-tutorial-tenant-analytics.md) | <span data-ttu-id="df8db-134">오프라인 분석 쿼리를 실행하기 위해 테넌트 데이터를 분석 데이터베이스 또는 데이터 웨어하우스에 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-134">Extract tenant data into an analytics database or data warehouse for running offline analytic queries.</span></span> |



## <a name="application-architecture"></a><span data-ttu-id="df8db-135">응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="df8db-135">Application architecture</span></span>

<span data-ttu-id="df8db-136">hello Wingtip SaaS 앱 hello 테 넌 당 데이터베이스 모델을 사용 하 고 SQL 탄력적 풀 toomaximize 효율성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-136">hello Wingtip SaaS app uses hello database-per-tenant model, and uses SQL elastic pools toomaximize efficiency.</span></span> <span data-ttu-id="df8db-137">프로비저닝과 테 넌 트 tootheir 데이터 매핑 카탈로그 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-137">For provisioning and mapping tenants tootheir data, a catalog database is used.</span></span> <span data-ttu-id="df8db-138">hello 코어 Wingtip SaaS 응용 프로그램을 사용 하 여 3 개를 사용 하 여 풀 샘플 테 넌 트를 더한 hello 데이터베이스를 카탈로그입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-138">hello core Wingtip SaaS application, uses a pool with three sample tenants, plus hello catalog database.</span></span> <span data-ttu-id="df8db-139">다양 한 hello Wingtip SaaS 자습서 인해 추가 기능 toohello 초기 배포를 완료 분석 데이터베이스를 도입 하 여 데이터베이스 간 스키마 관리, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-139">Completing many of hello Wingtip SaaS tutorials result in add-ons toohello intial deployment, by introducing analytic databases, cross-database schema management, etc.</span></span>


![Wingtip SaaS 아키텍처](media/sql-database-wtp-overview/app-architecture.png)


<span data-ttu-id="df8db-141">Hello 자습서를 진행 하 고 hello 앱을 사용 하는 동안 이므로 hello SaaS 패턴에 대 한 중요 한 toofocus toohello 데이터 계층 관계.</span><span class="sxs-lookup"><span data-stu-id="df8db-141">While going through hello tutorials and working with hello app, it is important toofocus on hello SaaS patterns as they relate toohello data tier.</span></span> <span data-ttu-id="df8db-142">즉, hello 데이터 계층에 집중 하 고 hello 응용 프로그램 자체가 분석 넘는 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="df8db-142">In other words, focus on hello data tier, and don't over analyze hello app itself.</span></span> <span data-ttu-id="df8db-143">이러한 SaaS 패턴의 hello 구현을 이해 키 tooimplementing 응용 프로그램에서 이러한 패턴 특정 비즈니스 요구 사항에 맞게 필요한 수정이 적용을 고려 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-143">Understanding hello implementation of these SaaS patterns is key tooimplementing these patterns in your applications, while considering any necessary modifications for your specific business requirements.</span></span>

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a><span data-ttu-id="df8db-144">다운로드 하 고 hello Wingtip SaaS 스크립트를 차단 해제</span><span class="sxs-lookup"><span data-stu-id="df8db-144">Download and unblock hello Wingtip SaaS scripts</span></span>

<span data-ttu-id="df8db-145">zip 파일이 외부 원본에서 다운로드되고 추출될 때 Windows에서 실행 가능한 콘텐츠(스크립트, dll)를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-145">Executable contents (scripts, dlls) may be blocked by Windows when zip files are downloaded from an external source and extracted.</span></span> <span data-ttu-id="df8db-146">Hello 스크립트 zip 파일에서 추출할 때 ***추출 하기 전에 아래 toounblock hello.zip 파일 hello 같이***합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-146">When extracting hello scripts from a zip file, ***follow hello steps below toounblock hello .zip file before extracting***.</span></span> <span data-ttu-id="df8db-147">이렇게 하면 hello 스크립트 toorun 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-147">This ensures hello scripts are allowed toorun.</span></span>

1. <span data-ttu-id="df8db-148">너무 찾아보기[hello Wingtip SaaS github 리포지토리](https://github.com/Microsoft/WingtipSaaS)합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-148">Browse too[hello Wingtip SaaS github repo](https://github.com/Microsoft/WingtipSaaS).</span></span>
1. <span data-ttu-id="df8db-149">**복제 또는 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-149">Click **Clone or download**.</span></span>
1. <span data-ttu-id="df8db-150">클릭 **zip 파일 다운로드** hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-150">Click **Download ZIP** and save hello file.</span></span>
1. <span data-ttu-id="df8db-151">마우스 오른쪽 단추로 클릭 hello **WingtipSaaS master.zip** 파일을 찾아 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-151">Right-click hello **WingtipSaaS-master.zip** file, and select **Properties**.</span></span>
1. <span data-ttu-id="df8db-152">Hello에 **일반** 탭에서 **차단 해제**합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-152">On hello **General** tab, select **Unblock**.</span></span>
1. <span data-ttu-id="df8db-153">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-153">Click **OK**.</span></span>
1. <span data-ttu-id="df8db-154">Hello 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-154">Extract hello files.</span></span>

<span data-ttu-id="df8db-155">Hello에 있는 스크립트 *... \\WingtipSaaS 마스터\\학습 모듈* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-155">Scripts are located in hello *..\\WingtipSaaS-master\\Learning Modules* folder.</span></span>


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a><span data-ttu-id="df8db-156">Hello Wingtip SaaS PowerShell 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="df8db-156">Working with hello Wingtip SaaS PowerShell Scripts</span></span>

<span data-ttu-id="df8db-157">tooget hello 가장 hello 샘플에서 필요한 toodive hello 제공 된 스크립트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-157">tooget hello most out of hello sample you need toodive into hello provided scripts.</span></span> <span data-ttu-id="df8db-158">중단점을 사용 하 고 hello 다양 한 SaaS 패턴을 구현 하는 방법의 hello 세부 정보를 검사 하는 hello 스크립트를 단계별로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-158">Use breakpoints and step through hello scripts, examining hello details of how hello different SaaS patterns are implemented.</span></span> <span data-ttu-id="df8db-159">제공 된 hello 스크립트 및 가장 이해, hello를 사용 하는 것이 좋습니다 hello에 대 한 모듈을 통해 tooeasily 단계 [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-159">tooeasily step through hello provided scripts and modules for hello best understanding, we recommend using hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span>

### <a name="update-hello-configuration-file-for-your-deployment"></a><span data-ttu-id="df8db-160">배포에 대 한 hello 구성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="df8db-160">Update hello configuration file for your deployment</span></span>

<span data-ttu-id="df8db-161">Hello 편집 **UserConfig.psm1** hello 리소스 그룹 및 사용자 값을 갖는 배포 하는 동안 설정한 파일:</span><span class="sxs-lookup"><span data-stu-id="df8db-161">Edit hello **UserConfig.psm1** file with hello resource group and user value that you set during deployment:</span></span>

1. <span data-ttu-id="df8db-162">열기 hello *PowerShell ISE* 로드 중... \\학습 모듈\\*UserConfig.psm1*</span><span class="sxs-lookup"><span data-stu-id="df8db-162">Open hello *PowerShell ISE* and load ...\\Learning Modules\\*UserConfig.psm1*</span></span> 
1. <span data-ttu-id="df8db-163">업데이트 *ResourceGroupName* 및 *이름* hello (10과 11만 줄)에서 배포에 대 한 특정 값으로.</span><span class="sxs-lookup"><span data-stu-id="df8db-163">Update *ResourceGroupName* and *Name* with hello specific values for your deployment (on lines 10 and 11 only).</span></span>
1. <span data-ttu-id="df8db-164">Hello ब ा ळ!</span><span class="sxs-lookup"><span data-stu-id="df8db-164">Save hello changes!</span></span>

<span data-ttu-id="df8db-165">여기에 이러한 값을 설정 하는 모든 스크립트에서 tooupdate 이러한 배포 관련 값이 있으면에서 단순히 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-165">Setting these values here simply keeps you from having tooupdate these deployment-specific values in every script.</span></span>

### <a name="execute-scripts-by-pressing-f5"></a><span data-ttu-id="df8db-166">F5 키를 눌러 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="df8db-166">Execute Scripts by pressing F5</span></span>

<span data-ttu-id="df8db-167">여러 스크립트 사용 하 여 *$PSScriptRoot* toonavigate 폴더 및 *$PSScriptRoot* 키를 눌러 스크립트를 실행 하는 경우에 평가 되기 **F5**합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-167">Several scripts use *$PSScriptRoot* toonavigate folders, and *$PSScriptRoot* is only evaluated when scripts are executed by pressing **F5**.</span></span>  <span data-ttu-id="df8db-168">선택 내용을 강조 표시하고 실행(**F8**)하면 오류가 발생할 수 있으므로 스크립트를 실행할 때는 **F5** 키를 누르세요.</span><span class="sxs-lookup"><span data-stu-id="df8db-168">Highlighting and running a selection (**F8**) can result in errors, so press **F5** when running scripts.</span></span>

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a><span data-ttu-id="df8db-169">Hello 스크립트 tooexamine hello 구현 단계</span><span class="sxs-lookup"><span data-stu-id="df8db-169">Step through hello scripts tooexamine hello implementation</span></span>

<span data-ttu-id="df8db-170">하나씩 검사 하는 hello 가장 좋은 방법은 toounderstand hello 스크립트 toosee 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-170">hello best way toounderstand hello scripts is by stepping through them toosee what they do.</span></span> <span data-ttu-id="df8db-171">체크 아웃 포함 하는 hello **데모-** 쉽게 toofollow 수준의 워크플로 제공 하는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-171">Check out hello included **Demo-** scripts that present an easy toofollow high-level workflow.</span></span> <span data-ttu-id="df8db-172">hello **데모-** 하므로 중단점을 설정 하 고 hello 개별을 깊은 드릴 toosee 구현 세부 정보에 대 한 호출 hello 다양 한 SaaS 패턴 스크립트 hello 단계 필요한 tooaccomplish 각 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-172">hello **Demo-** scripts show hello steps required tooaccomplish each task, so set breakpoints and drill deeper into hello individual calls toosee implementation details for hello different SaaS patterns.</span></span>

<span data-ttu-id="df8db-173">PowerShell 스크립트 탐색 및 단계별 실행에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="df8db-173">Tips for exploring and stepping through PowerShell scripts:</span></span>

* <span data-ttu-id="df8db-174">열기 **데모-** hello PowerShell ISE에서에서 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-174">Open **Demo-** scripts in hello PowerShell ISE.</span></span>
* <span data-ttu-id="df8db-175">**F5** 키를 사용하여 실행하거나 계속합니다. 스크립트의 선택 항목을 실행할 때 *$PSScriptRoot*가 평가되지 않으므로 **F8** 키는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-175">Execute or continue with **F5** (using **F8** is not advised because *$PSScriptRoot* is not evaluated when running selections of a script).</span></span>
* <span data-ttu-id="df8db-176">행을 클릭하거나 선택하고 **F9** 키를 눌러 중단점을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-176">Place breakpoints by clicking or selecting a line and pressing **F9**.</span></span>
* <span data-ttu-id="df8db-177">**F10**을 사용하여 함수 또는 스크립트 호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-177">Step over a function or script call using **F10**.</span></span>
* <span data-ttu-id="df8db-178">**F11**을 사용하여 함수 또는 스크립트 호출 코드를 한 단계씩 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-178">Step into a function or script call using **F11**.</span></span>
* <span data-ttu-id="df8db-179">현재 함수 hello 외부로 단계별로 실행 하거나 스크립트를 사용 하 여 호출 **Shift + F11**합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-179">Step out of hello current function or script call using **Shift + F11**.</span></span>


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a><span data-ttu-id="df8db-180">데이터베이스 스키마를 탐색하고 SSMS를 사용하여 SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-180">Explore database schema and execute SQL queries using SSMS</span></span>

<span data-ttu-id="df8db-181">사용 하 여 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect 및 찾아보기 hello 응용 프로그램 서버 및 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-181">Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect and browse hello application servers and databases.</span></span>

<span data-ttu-id="df8db-182">hello 배포에는 처음 두 개의 SQL 데이터베이스 서버 tooconnect 너무-hello에 *tenants1-&lt;사용자&gt;*  서버 및 hello *카탈로그-&lt;사용자&gt;* 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-182">hello deployment initially has two SQL Database servers tooconnect too- hello *tenants1-&lt;User&gt;* server, and hello *catalog-&lt;User&gt;* server.</span></span> <span data-ttu-id="df8db-183">성공적인 데모 연결 tooensure 두 서버에 대 한는 [방화벽 규칙](sql-database-firewall-configure.md) 를 통해 모든 Ip 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-183">tooensure a successful demo connection, both servers have a [firewall rule](sql-database-firewall-configure.md) allowing all IPs through.</span></span>


1. <span data-ttu-id="df8db-184">열기 *SSMS* toohello 연결 *tenants1-&lt;사용자&gt;. database.windows.net* 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-184">Open *SSMS* and connect toohello *tenants1-&lt;User&gt;.database.windows.net* server.</span></span>
1. <span data-ttu-id="df8db-185">**연결** > **데이터베이스 엔진...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-185">Click **Connect** > **Database Engine...**:</span></span>

   ![카탈로그 서버](media/sql-database-wtp-overview/connect.png)

1. <span data-ttu-id="df8db-187">데모 자격 증명: 로그인 = *developer*, 암호 =*P@ssword1*</span><span class="sxs-lookup"><span data-stu-id="df8db-187">Demo credentials are: Login = *developer*, Password = *P@ssword1*</span></span>

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. <span data-ttu-id="df8db-189">2-3 단계를 반복 하 고 연결 toohello *카탈로그-&lt;사용자&gt;. database.windows.net* 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-189">Repeat steps 2-3 and connect toohello *catalog-&lt;User&gt;.database.windows.net* server.</span></span>

<span data-ttu-id="df8db-190">성공적으로 연결된 후 두 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-190">After successfully connecting you should see both servers.</span></span> <span data-ttu-id="df8db-191">데이터베이스 목록이 hello 프로 비전 한 테 넌 트에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df8db-191">Your list of databases might be different, depending on hello tenants you've provisioned:</span></span>

![개체 탐색기](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a><span data-ttu-id="df8db-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df8db-193">Next steps</span></span>

[<span data-ttu-id="df8db-194">Hello Wingtip SaaS 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="df8db-194">Deploy hello Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)
