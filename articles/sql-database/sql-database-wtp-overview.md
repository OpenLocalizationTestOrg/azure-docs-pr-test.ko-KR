---
title: "Wingtip SaaS - Azure SQL Database 다중 테넌트 앱 소개 | Microsoft Docs"
description: "Azure SQL Database를 사용하는 샘플 다중 테넌트 응용 프로그램인 Wingtip SaaS 앱 사용에 대해 알아봅니다."
keywords: "sql 데이터베이스 자습서"
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
ms.openlocfilehash: 6d4a5df599137e95ca5458fae74b8daa565b0338
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-wingtip-saas-application"></a><span data-ttu-id="81679-104">Wingtip SaaS 응용 프로그램 소개</span><span class="sxs-lookup"><span data-stu-id="81679-104">Introduction to the Wingtip SaaS application</span></span>

<span data-ttu-id="81679-105">*Wingtip SaaS* 응용 프로그램은 SQL Database의 고유 장점을 보여주는 샘플 다중 테넌트 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="81679-105">The *Wingtip SaaS* application is a sample multi-tenant app, that demonstrates the unique advantages of SQL Database.</span></span> <span data-ttu-id="81679-106">앱은 테넌트별 데이터베이스(SaaS 응용 프로그램 패턴)를 사용하여 여러 테넌트에 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-106">The app uses a database-per-tenant, SaaS application pattern, to service multiple tenants.</span></span> <span data-ttu-id="81679-107">이 앱은 여러 SaaS 디자인 및 관리 패턴을 포함한 SaaS 시나리오를 사용할 수 있게 해주는 Azure SQL Database의 기능을 보여주기 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-107">The app is designed to showcase features of Azure SQL Database that enable SaaS scenarios, including several SaaS design and management patterns.</span></span> <span data-ttu-id="81679-108">신속하게 가동 및 실행하기 위해 Wingtip SaaS 앱에서 5분 내에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-108">To quickly get up and running, the Wingtip SaaS app deploys in less than five minutes!</span></span>

<span data-ttu-id="81679-109">응용 프로그램 소스 코드는 [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) GitHub 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-109">Application source code and management scripts are available in the [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="81679-110">스크립트를 실행하려면 로컬 컴퓨터에 [Learning Modules 폴더를 다운로드](#download-and-unblock-the-wingtip-saas-scripts)합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-110">To run the scripts, [download the Learning Modules folder](#download-and-unblock-the-wingtip-saas-scripts) to your local computer.</span></span>

## <a name="sql-database-wingtip-saas-tutorials"></a><span data-ttu-id="81679-111">SQL Database Wingtip SaaS 자습서</span><span class="sxs-lookup"><span data-stu-id="81679-111">SQL Database Wingtip SaaS tutorials</span></span>

<span data-ttu-id="81679-112">앱을 배포한 후 초기 배포 시 작성된 다음 자습서를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-112">After deploying the app, explore the following tutorials that build upon the initial deployment.</span></span> <span data-ttu-id="81679-113">이러한 자습서에서는 SQL Database, SQL Data Warehouse 및 기타 Azure 서비스의 기본 제공 기능을 활용하는 일반적인 SaaS 패턴을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-113">These tutorials explore common SaaS patterns that take advantage of built-in features of SQL Database, SQL Data Warehouse, and other Azure services.</span></span> <span data-ttu-id="81679-114">자습서에는 PowerShell 스크립트와 함께 응용 프로그램에서 동일한 SaaS 관리 패턴에 대한 이해 및 구현을 간소화해주는 상세한 설명이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81679-114">Tutorials include PowerShell scripts, with detailed explanations that greatly simplify understanding, and implementing the same SaaS management patterns in your applications.</span></span>


| <span data-ttu-id="81679-115">자습서</span><span class="sxs-lookup"><span data-stu-id="81679-115">Tutorial</span></span> | <span data-ttu-id="81679-116">설명</span><span class="sxs-lookup"><span data-stu-id="81679-116">Description</span></span> |
|:--|:--|
|[<span data-ttu-id="81679-117">Wingtip SaaS 응용 프로그램 배포 및 탐색</span><span class="sxs-lookup"><span data-stu-id="81679-117">Deploy and explore the Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)| <span data-ttu-id="81679-118">**여기에서 시작하세요.**</span><span class="sxs-lookup"><span data-stu-id="81679-118">**START HERE!**</span></span> <span data-ttu-id="81679-119">Azure 구독에 Wingtip SaaS 응용 프로그램을 배포하고 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-119">Deploy and explore the Wingtip SaaS application to your Azure subscription.</span></span> |
|[<span data-ttu-id="81679-120">프로비전 및 카탈로그 테넌트</span><span class="sxs-lookup"><span data-stu-id="81679-120">Provision and catalog tenants</span></span>](sql-database-saas-tutorial-provision-and-catalog.md)| <span data-ttu-id="81679-121">카탈로그 데이터베이스를 사용하여 응용 프로그램을 테넌트에 연결하는 방법 및 카탈로그가 테넌트를 해당 데이터에 매핑하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-121">Learn how the application connects to tenants using a catalog database, and how the catalog maps tenants to their data.</span></span> |
|[<span data-ttu-id="81679-122">성능 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="81679-122">Monitor and manage performance</span></span>](sql-database-saas-tutorial-performance-monitoring.md)| <span data-ttu-id="81679-123">SQL Database의 모니터링 기능을 사용하는 방법 및 성능 임계값이 초과된 경우 경고를 설정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-123">Learn how to use monitoring features of SQL Database, and how to set alerts when performance thresholds are exceeded.</span></span> |
|[<span data-ttu-id="81679-124">Log Analytics(OMS)로 모니터링</span><span class="sxs-lookup"><span data-stu-id="81679-124">Monitor with Log Analytics (OMS)</span></span>](sql-database-saas-tutorial-log-analytics.md) | <span data-ttu-id="81679-125">[Log Analytics](../log-analytics/log-analytics-overview.md)를 사용하여 여러 풀에 걸쳐 있는 많은 양의 리소스를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-125">Learn about using [Log Analytics](../log-analytics/log-analytics-overview.md) to monitor large amounts of resources, across multiple pools.</span></span> |
|[<span data-ttu-id="81679-126">단일 테넌트 복원</span><span class="sxs-lookup"><span data-stu-id="81679-126">Restore a single tenant</span></span>](sql-database-saas-tutorial-restore-single-tenant.md)| <span data-ttu-id="81679-127">테넌트 데이터베이스를 이전 시점으로 복원하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-127">Learn how to restore a tenant database to a prior point in time.</span></span> <span data-ttu-id="81679-128">기존 테넌트 데이터베이스를 온라인으로 유지한 상태에서 병렬 데이터베이스를 복원하는 단계도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="81679-128">Steps to restore to a parallel database, leaving the existing tenant database online, are also included.</span></span> |
|[<span data-ttu-id="81679-129">테넌트 스키마 관리</span><span class="sxs-lookup"><span data-stu-id="81679-129">Manage tenant schema</span></span>](sql-database-saas-tutorial-schema-management.md)| <span data-ttu-id="81679-130">모든 Wingtip SaaS 테넌트에서 스키마를 업데이트하고 참조 데이터를 업데이트하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="81679-130">Learn how to update schema, and update reference data, across all Wingtip SaaS tenants.</span></span> |
|[<span data-ttu-id="81679-131">임시 분석 실행</span><span class="sxs-lookup"><span data-stu-id="81679-131">Run ad-hoc analytics</span></span>](sql-database-saas-tutorial-adhoc-analytics.md) | <span data-ttu-id="81679-132">임시 분석 데이터베이스를 만들고 모든 테넌트에서 실시간 분산 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-132">Create an ad-hoc analytics database and run real-time distributed queries across all tenants.</span></span>  |
|[<span data-ttu-id="81679-133">테넌트 분석 실행</span><span class="sxs-lookup"><span data-stu-id="81679-133">Run tenant analytics</span></span>](sql-database-saas-tutorial-tenant-analytics.md) | <span data-ttu-id="81679-134">오프라인 분석 쿼리를 실행하기 위해 테넌트 데이터를 분석 데이터베이스 또는 데이터 웨어하우스에 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-134">Extract tenant data into an analytics database or data warehouse for running offline analytic queries.</span></span> |



## <a name="application-architecture"></a><span data-ttu-id="81679-135">응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="81679-135">Application architecture</span></span>

<span data-ttu-id="81679-136">Wingtip SaaS 앱은 테넌트별 데이터베이스 모델을 사용하며 효율을 극대화하기 위해 SQL 탄력적 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-136">The Wingtip SaaS app uses the database-per-tenant model, and uses SQL elastic pools to maximize efficiency.</span></span> <span data-ttu-id="81679-137">테넌트를 해당 데이터에 매핑하고 프로비전하는 데 카탈로그 데이터베이스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="81679-137">For provisioning and mapping tenants to their data, a catalog database is used.</span></span> <span data-ttu-id="81679-138">핵심 Wingtip SaaS 응용 프로그램은 세 가지 샘플 테넌트가 있는 풀 및 카탈로그 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-138">The core Wingtip SaaS application, uses a pool with three sample tenants, plus the catalog database.</span></span> <span data-ttu-id="81679-139">다양한 Wingtip SaaS 자습서를 완료하면 초기 배포에 분석 데이터베이스, 데이터베이스 간 스키마 관리 등의 추가 기능을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-139">Completing many of the Wingtip SaaS tutorials result in add-ons to the intial deployment, by introducing analytic databases, cross-database schema management, etc.</span></span>


![Wingtip SaaS 아키텍처](media/sql-database-wtp-overview/app-architecture.png)


<span data-ttu-id="81679-141">자습서를 진행하고 앱을 사용하는 동안 데이터 계층과 관련된 SaaS 패턴에 중점을 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-141">While going through the tutorials and working with the app, it is important to focus on the SaaS patterns as they relate to the data tier.</span></span> <span data-ttu-id="81679-142">즉, 데이터 계층에 집중하고 앱 자체를 과도하게 분석하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="81679-142">In other words, focus on the data tier, and don't over analyze the app itself.</span></span> <span data-ttu-id="81679-143">이러한 SaaS 패턴의 구현 방식을 이해하는 것은 특정 비즈니스 요구 사항에 필요한 모든 수정을 고려하면서 응용 프로그램에서 이러한 패턴을 구현하기 위한 열쇠입니다.</span><span class="sxs-lookup"><span data-stu-id="81679-143">Understanding the implementation of these SaaS patterns is key to implementing these patterns in your applications, while considering any necessary modifications for your specific business requirements.</span></span>

## <a name="download-and-unblock-the-wingtip-saas-scripts"></a><span data-ttu-id="81679-144">Wingtip SaaS 스크립트 다운로드 및 차단 해제</span><span class="sxs-lookup"><span data-stu-id="81679-144">Download and unblock the Wingtip SaaS scripts</span></span>

<span data-ttu-id="81679-145">zip 파일이 외부 원본에서 다운로드되고 추출될 때 Windows에서 실행 가능한 콘텐츠(스크립트, dll)를 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-145">Executable contents (scripts, dlls) may be blocked by Windows when zip files are downloaded from an external source and extracted.</span></span> <span data-ttu-id="81679-146">Zip 파일에서 스크립트를 추출할 경우 ***아래 단계에 따라 추출하기 전에 .zip 파일을 차단 해제***하세요.</span><span class="sxs-lookup"><span data-stu-id="81679-146">When extracting the scripts from a zip file, ***follow the steps below to unblock the .zip file before extracting***.</span></span> <span data-ttu-id="81679-147">이렇게 하면 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-147">This ensures the scripts are allowed to run.</span></span>

1. <span data-ttu-id="81679-148">[Wingtip SaaS GitHub 리포지토리](https://github.com/Microsoft/WingtipSaaS)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-148">Browse to [the Wingtip SaaS github repo](https://github.com/Microsoft/WingtipSaaS).</span></span>
1. <span data-ttu-id="81679-149">**복제 또는 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-149">Click **Clone or download**.</span></span>
1. <span data-ttu-id="81679-150">**ZIP 다운로드**를 클릭하고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-150">Click **Download ZIP** and save the file.</span></span>
1. <span data-ttu-id="81679-151">**WingtipSaaS-master.zip** 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-151">Right-click the **WingtipSaaS-master.zip** file, and select **Properties**.</span></span>
1. <span data-ttu-id="81679-152">**일반** 탭에서 **차단 해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-152">On the **General** tab, select **Unblock**.</span></span>
1. <span data-ttu-id="81679-153">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-153">Click **OK**.</span></span>
1. <span data-ttu-id="81679-154">파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="81679-154">Extract the files.</span></span>

<span data-ttu-id="81679-155">스크립트는 *..\\WingtipSaaS-master\\Learning Modules* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-155">Scripts are located in the *..\\WingtipSaaS-master\\Learning Modules* folder.</span></span>


## <a name="working-with-the-wingtip-saas-powershell-scripts"></a><span data-ttu-id="81679-156">Wingtip SaaS PowerShell 스크립트 작업</span><span class="sxs-lookup"><span data-stu-id="81679-156">Working with the Wingtip SaaS PowerShell Scripts</span></span>

<span data-ttu-id="81679-157">샘플을 최대한 활용하려면 제공된 스크립트를 자세히 살펴보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-157">To get the most out of the sample you need to dive into the provided scripts.</span></span> <span data-ttu-id="81679-158">중단점을 사용하고 스크립트를 단계별로 실행하면서 다양한 SaaS 패턴이 구현된 방식을 자세히 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="81679-158">Use breakpoints and step through the scripts, examining the details of how the different SaaS patterns are implemented.</span></span> <span data-ttu-id="81679-159">가장 잘 이해할 수 있도록 제공된 스크립트 및 모듈을 손쉽게 단계별로 실행하려면 [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-159">To easily step through the provided scripts and modules for the best understanding, we recommend using the [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span>

### <a name="update-the-configuration-file-for-your-deployment"></a><span data-ttu-id="81679-160">배포에 대한 구성 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="81679-160">Update the configuration file for your deployment</span></span>

<span data-ttu-id="81679-161">배포 중에 설정한 사용자 값 및 리소스 그룹을 사용하여 **UserConfig.psm1** 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-161">Edit the **UserConfig.psm1** file with the resource group and user value that you set during deployment:</span></span>

1. <span data-ttu-id="81679-162">*PowerShell ISE*를 열고 ...\\Learning Modules\\*UserConfig.psm1*을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-162">Open the *PowerShell ISE* and load ...\\Learning Modules\\*UserConfig.psm1*</span></span> 
1. <span data-ttu-id="81679-163">배포에 대한 특정 값(줄 10 및 11에서만)으로 *ResourceGroupName* 및 *Name*을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-163">Update *ResourceGroupName* and *Name* with the specific values for your deployment (on lines 10 and 11 only).</span></span>
1. <span data-ttu-id="81679-164">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-164">Save the changes!</span></span>

<span data-ttu-id="81679-165">여기서 이러한 값을 설정하면 모든 스크립트에서 이러한 배포별 값을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-165">Setting these values here simply keeps you from having to update these deployment-specific values in every script.</span></span>

### <a name="execute-scripts-by-pressing-f5"></a><span data-ttu-id="81679-166">F5 키를 눌러 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="81679-166">Execute Scripts by pressing F5</span></span>

<span data-ttu-id="81679-167">여러 스크립트에서 *$PSScriptRoot*를 사용하여 폴더를 탐색할 수 있으며 *$PSScriptRoot*는 **F5** 키를 눌러 스크립트를 실행할 때만 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="81679-167">Several scripts use *$PSScriptRoot* to navigate folders, and *$PSScriptRoot* is only evaluated when scripts are executed by pressing **F5**.</span></span>  <span data-ttu-id="81679-168">선택 내용을 강조 표시하고 실행(**F8**)하면 오류가 발생할 수 있으므로 스크립트를 실행할 때는 **F5** 키를 누르세요.</span><span class="sxs-lookup"><span data-stu-id="81679-168">Highlighting and running a selection (**F8**) can result in errors, so press **F5** when running scripts.</span></span>

### <a name="step-through-the-scripts-to-examine-the-implementation"></a><span data-ttu-id="81679-169">스크립트를 단계별로 실행하여 구현 검사</span><span class="sxs-lookup"><span data-stu-id="81679-169">Step through the scripts to examine the implementation</span></span>

<span data-ttu-id="81679-170">스크립트를 이해하는 가장 좋은 방법은 단계별로 실행하여 수행되는 작업을 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-170">The best way to understand the scripts is by stepping through them to see what they do.</span></span> <span data-ttu-id="81679-171">개략적인 워크플로를 따르는 포함된 **Demo-** 스크립트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-171">Check out the included **Demo-** scripts that present an easy to follow high-level workflow.</span></span> <span data-ttu-id="81679-172">**Demo-** 스크립트는 각 작업을 완료하는 데 필요한 단계를 보여 주므로 중단점을 설정하고 개별 호출로 드릴다운하여 여러 SaaS 패턴에 대한 구현 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-172">The **Demo-** scripts show the steps required to accomplish each task, so set breakpoints and drill deeper into the individual calls to see implementation details for the different SaaS patterns.</span></span>

<span data-ttu-id="81679-173">PowerShell 스크립트 탐색 및 단계별 실행에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="81679-173">Tips for exploring and stepping through PowerShell scripts:</span></span>

* <span data-ttu-id="81679-174">PowerShell ISE에서 **Demo-** 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81679-174">Open **Demo-** scripts in the PowerShell ISE.</span></span>
* <span data-ttu-id="81679-175">**F5** 키를 사용하여 실행하거나 계속합니다. 스크립트의 선택 항목을 실행할 때 *$PSScriptRoot*가 평가되지 않으므로 **F8** 키는 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-175">Execute or continue with **F5** (using **F8** is not advised because *$PSScriptRoot* is not evaluated when running selections of a script).</span></span>
* <span data-ttu-id="81679-176">행을 클릭하거나 선택하고 **F9** 키를 눌러 중단점을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-176">Place breakpoints by clicking or selecting a line and pressing **F9**.</span></span>
* <span data-ttu-id="81679-177">**F10**을 사용하여 함수 또는 스크립트 호출을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-177">Step over a function or script call using **F10**.</span></span>
* <span data-ttu-id="81679-178">**F11**을 사용하여 함수 또는 스크립트 호출 코드를 한 단계씩 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-178">Step into a function or script call using **F11**.</span></span>
* <span data-ttu-id="81679-179">**Shift + F11**을 사용하여 현재 함수 또는 스크립트 호출을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-179">Step out of the current function or script call using **Shift + F11**.</span></span>


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a><span data-ttu-id="81679-180">데이터베이스 스키마를 탐색하고 SSMS를 사용하여 SQL 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-180">Explore database schema and execute SQL queries using SSMS</span></span>

<span data-ttu-id="81679-181">[SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 사용하여 응용 프로그램 서버 및 데이터베이스에 연결하고 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-181">Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) to connect and browse the application servers and databases.</span></span>

<span data-ttu-id="81679-182">초기에 배포에는 연결할 두 SQL Database 서버가 있는데 *tenants1-&lt;User&gt;* 서버 및 *catalog-&lt;User&gt;* 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="81679-182">The deployment initially has two SQL Database servers to connect to - the *tenants1-&lt;User&gt;* server, and the *catalog-&lt;User&gt;* server.</span></span> <span data-ttu-id="81679-183">성공적인 데모 연결을 위해 두 서버 모두에 모든 IP의 통과를 허용하는 [방화벽 규칙](sql-database-firewall-configure.md)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-183">To ensure a successful demo connection, both servers have a [firewall rule](sql-database-firewall-configure.md) allowing all IPs through.</span></span>


1. <span data-ttu-id="81679-184">*SSMS*를 열고 *tenants1-&lt;User&gt;.database.windows.net* 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-184">Open *SSMS* and connect to the *tenants1-&lt;User&gt;.database.windows.net* server.</span></span>
1. <span data-ttu-id="81679-185">**연결** > **데이터베이스 엔진...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-185">Click **Connect** > **Database Engine...**:</span></span>

   ![카탈로그 서버](media/sql-database-wtp-overview/connect.png)

1. <span data-ttu-id="81679-187">데모 자격 증명: 로그인 = *developer*, 암호 =*P@ssword1*</span><span class="sxs-lookup"><span data-stu-id="81679-187">Demo credentials are: Login = *developer*, Password = *P@ssword1*</span></span>

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. <span data-ttu-id="81679-189">2-3단계를 반복하고 *catalog-&lt;User&gt;.database.windows.net* 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="81679-189">Repeat steps 2-3 and connect to the *catalog-&lt;User&gt;.database.windows.net* server.</span></span>

<span data-ttu-id="81679-190">성공적으로 연결된 후 두 서버가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="81679-190">After successfully connecting you should see both servers.</span></span> <span data-ttu-id="81679-191">프로비전한 테넌트에 따라 데이터베이스 목록이 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81679-191">Your list of databases might be different, depending on the tenants you've provisioned:</span></span>

![개체 탐색기](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a><span data-ttu-id="81679-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81679-193">Next steps</span></span>

[<span data-ttu-id="81679-194">Wingtip SaaS 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="81679-194">Deploy the Wingtip SaaS application</span></span>](sql-database-saas-tutorial.md)