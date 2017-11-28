---
title: "aaaOptimize Azure 로그 분석으로 System Center Operations Manager 환경 | Microsoft Docs"
description: "System Center Operations Manager 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 서버 환경 hello hello를 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="71cf6-103">Hello System Center Operations Manager 평가 (미리 보기) 솔루션으로 환경 최적화</span><span class="sxs-lookup"><span data-stu-id="71cf6-103">Optimize your environment with hello System Center Operations Manager Assessment (Preview) solution</span></span>

![System Center Operations Manager 평가 기호](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

<span data-ttu-id="71cf6-105">System Center Operations Manager 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 System Center Operations Manager 서버 환경의 hello hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-105">You can use hello System Center Operations Manager Assessment solution tooassess hello risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="71cf6-106">이 문서에서는 설치, 구성 및 솔루션 hello를 사용 하 여 잠재적인 문제에 대 한 수정 동작을 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-106">This article helps you install, configure, and use hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="71cf6-107">이 솔루션은 권장 사항 특정 tooyour 배포 된 서버 인프라의 우선 순위 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="71cf6-108">hello 권장 사항은 신속 하 게 하는 데 있는 영역 이해 위험 hello 수정 작업을 수행 하는 4 개의 포커스도 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-108">hello recommendations are categorized across four focus areas, which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="71cf6-109">hello 권장 hello 지식과 수천 고객 방문에서에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="71cf6-110">각 권장 사항은 문제가 tooyou에 중요할 수 있는 이유 및 tooimplement hello 변경 내용을 제안 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="71cf6-111">가장 중요 한 tooyour 조직 되어 하 여 위험이 없는 정상 환경을 실행 하기 위한 진행률을 추적 하는 주요 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="71cf6-112">Hello에 중점 영역에 대 한 정보를 표시 한 평가 결과 완료 된, 요약 hello 솔루션을 추가한 후 **System Center Operations Manager 평가** 인프라에 대 한 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="71cf6-113">hello 다음 섹션에서는 설명 toouse hello에 대 한 정보를 hello 방법을 **System Center Operations Manager 평가** 대시보드를 보고 하 고 취할 수 있는 권장 SCOM 인프라에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-113">hello following sections describe how toouse hello information on hello **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager 솔루션 타일](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 평가 대시보드](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="71cf6-116">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="71cf6-116">Installing and configuring hello solution</span></span>

<span data-ttu-id="71cf6-117">hello 솔루션이 Microsoft 시스템 Operations Manager 2012 R2 및 2012 s p 1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-117">hello solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="71cf6-118">다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-118">Use hello following information tooinstall and configure hello solution.</span></span>

 - <span data-ttu-id="71cf6-119">OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-119">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="71cf6-120">설치에서 솔루션을 hello [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) 또는 hello 지침에 따라 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-120">Install hello solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following hello instructions in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="71cf6-121">Hello 솔루션 toohello 작업 영역을 추가한 후 hello 대시보드의 hello System Center Operations Manager 평가 타일 hello 추가 구성이 필요한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-121">After adding hello solution toohello workspace, hello System Center Operations Manager Assessment tile on hello dashboard displays hello additional configuration required message.</span></span> <span data-ttu-id="71cf6-122">Hello 타일을 클릭 하 고 hello 페이지에 언급 된 hello 구성 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-122">Click on hello tile and follow hello configuration steps mentioned in hello page</span></span>

 ![System Center Operations Manager 대시보드 타일](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 <span data-ttu-id="71cf6-124">Hello System Center Operations Manager의 구성 hello 구성 페이지의 hello 솔루션을 OMS에 언급 된 hello 단계를 수행 하 여 hello 스크립트를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-124">Configuration of hello System Center Operations Manager can be done through hello script by following hello steps mentioned in hello configuration page of hello solution in OMS.</span></span>

 <span data-ttu-id="71cf6-125">대신, 아래에 따라 hello SCOM 콘솔을 통해 tooconfigure hello 평가 단계 hello에 동일 주문</span><span class="sxs-lookup"><span data-stu-id="71cf6-125">Instead, tooconfigure hello assessment through SCOM Console, follow hello below steps in hello same order</span></span>
1. [<span data-ttu-id="71cf6-126">System Center Operations Manager 평가 대 한 hello 계정으로 실행 계정 설정</span><span class="sxs-lookup"><span data-stu-id="71cf6-126">Set hello Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="71cf6-127">Hello System Center Operations Manager 평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="71cf6-127">Configure hello System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="71cf6-128">System Center Operations Manager 평가 데이터 수집 세부 정보</span><span class="sxs-lookup"><span data-stu-id="71cf6-128">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="71cf6-129">System Center Operations Manager 평가 hello WMI 데이터, 레지스트리 데이터, 이벤트 로그 데이터, Windows PowerShell, SQL 쿼리, 사용 하도록 설정한 hello 서버를 사용 하 여 파일 정보 수집기를 통해 Operations Manager 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-129">hello System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using hello server that you have enabled.</span></span>

<span data-ttu-id="71cf6-130">hello 다음 표에서 데이터 수집 방법과 System Center Operations Manager 평가 대 한 얼마나 자주 에이전트에서 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-130">hello following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="71cf6-131">플랫폼</span><span class="sxs-lookup"><span data-stu-id="71cf6-131">platform</span></span> | <span data-ttu-id="71cf6-132">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="71cf6-132">Direct Agent</span></span> | <span data-ttu-id="71cf6-133">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="71cf6-133">SCOM agent</span></span> | <span data-ttu-id="71cf6-134">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="71cf6-134">Azure Storage</span></span> | <span data-ttu-id="71cf6-135">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="71cf6-135">SCOM required?</span></span> | <span data-ttu-id="71cf6-136">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="71cf6-136">SCOM agent data sent via management group</span></span> | <span data-ttu-id="71cf6-137">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="71cf6-137">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="71cf6-138">Windows</span><span class="sxs-lookup"><span data-stu-id="71cf6-138">Windows</span></span> | | | | <span data-ttu-id="71cf6-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="71cf6-139">&#8226;</span></span> | | <span data-ttu-id="71cf6-140">7일</span><span class="sxs-lookup"><span data-stu-id="71cf6-140">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="71cf6-141">OMS용 Operations Manager 실행 계정</span><span class="sxs-lookup"><span data-stu-id="71cf6-141">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="71cf6-142">Tooprovide 워크 로드에 대 한 관리 팩에서 빌드를 OMS는 부가 가치 서비스.</span><span class="sxs-lookup"><span data-stu-id="71cf6-142">OMS builds on management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="71cf6-143">각 작업은 도메인 계정과 같은 다른 보안 컨텍스트에서 작업 관련 권한이 toorun 관리 팩 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-143">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="71cf6-144">Operations Manager 계정으로 실행 계정 tooprovide 자격 증명 정보를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-144">Configure an Operations Manager Run As account tooprovide credential information.</span></span>

<span data-ttu-id="71cf6-145">다음 정보 tooset System Center Operations Manager 평가 대 한 Operations Manager 실행 계정을 hello hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-145">Use hello following information tooset hello Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-hello-run-as-account"></a><span data-ttu-id="71cf6-146">집합 hello 실행 계정</span><span class="sxs-lookup"><span data-stu-id="71cf6-146">Set hello Run As account</span></span>

1. <span data-ttu-id="71cf6-147">Operations Manager 콘솔 hello 이동 toohello **관리** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-147">In hello Operations Manager Console, go toohello **Administration** tab.</span></span>
2. <span data-ttu-id="71cf6-148">Hello에서 **실행 구성**, 클릭 **계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-148">Under hello **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="71cf6-149">Hello 실행 계정, hello Windows 계정 만들기 마법사를 통해 다음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-149">Create hello Run As Account, following through hello Wizard, creating a Windows account.</span></span> <span data-ttu-id="71cf6-150">hello 계정 toouse hello 식별 하나 및 모든 hello 다음과 같은 전제 조건 것입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-150">hello account toouse is hello one identified and having all hello prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="71cf6-151">hello 실행 계정은 다음 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-151">hello Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="71cf6-152">Hello hello 환경 (모든 Operations Manager 역할-관리 서버, OpsMgr 데이터베이스, 데이터 웨어하우스, 보고, 웹 콘솔, 게이트웨이)에서 모든 서버에서 로컬 관리자 그룹의 도메인 계정 멤버</span><span class="sxs-lookup"><span data-stu-id="71cf6-152">A domain account member of hello local Administrators group on all servers in hello environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="71cf6-153">평가 중인 hello 관리 그룹에 대 한 작업 Manager 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="71cf6-153">Operation Manager Administrator Role for hello management group being assessed</span></span>
    - <span data-ttu-id="71cf6-154">Hello 실행 [스크립트](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant Operations Manager에서 사용 하는 SQL 인스턴스에서 toohello 계정 세분화 된 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="71cf6-154">Execute hello [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant granular permissions toohello account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="71cf6-155">참고:이 계정에 sysadmin 권한이 이미 건너뜁니다 hello 스크립트 실행.</span><span class="sxs-lookup"><span data-stu-id="71cf6-155">Note: If this account has sysadmin rights already, then skip hello script execution.</span></span>

4. <span data-ttu-id="71cf6-156">**배포 보안**에서 **More secure**(보다 안전)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-156">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="71cf6-157">Hello 관리 서버 hello 계정을 배포할 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-157">Specify hello management server where hello account is distributed.</span></span>
3. <span data-ttu-id="71cf6-158">실행 구성 toohello 돌아가서 클릭 **프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-158">Go back toohello Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="71cf6-159">Hello에 대 한 검색 *SCOM 평가 프로필*합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-159">Search for hello *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="71cf6-160">hello 프로필 이름 이어야 합니다: *Microsoft System Center Advisor SCOM 평가 실행 프로필*합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-160">hello profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="71cf6-161">마우스 오른쪽 단추로 클릭 하 고 해당 속성을 업데이트 실행 계정 3 단계에서 만든를 최근에 만든 hello에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-161">Right-click and update its properties and add hello recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a><span data-ttu-id="71cf6-162">SQL 스크립트 toogrant 세부적인 권한 toohello 실행 계정</span><span class="sxs-lookup"><span data-stu-id="71cf6-162">SQL script toogrant granular permissions toohello Run As account</span></span>

<span data-ttu-id="71cf6-163">Hello SQL 스크립트 toogrant 필요한 사용 권한을 toohello 실행 계정이 Operations Manager에서 사용 하는 hello SQL 인스턴스에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-163">Execute hello following SQL script toogrant required permissions toohello Run As account on hello SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a><span data-ttu-id="71cf6-164">Hello 평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="71cf6-164">Configure hello assessment rule</span></span>

<span data-ttu-id="71cf6-165">System Center Operations Manager 평가 솔루션의 관리 팩 규칙을 포함 hello *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행*합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-165">hello System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="71cf6-166">이 규칙은 hello 평가 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-166">This rule is responsible for running hello assessment.</span></span> <span data-ttu-id="71cf6-167">tooenable 규칙 hello 및 hello 빈도 사용 하 여 hello 아래 절차를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-167">tooenable hello rule and configure hello frequency, use hello procedures below.</span></span>

<span data-ttu-id="71cf6-168">기본적으로 hello Microsoft System Center Advisor SCOM 평가 실행 평가 규칙을 사용 하는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-168">By default, hello Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="71cf6-169">toorun hello 평가, 관리 서버에 hello 규칙을 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-169">toorun hello assessment, you must enable hello rule on a management server.</span></span> <span data-ttu-id="71cf6-170">단계를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-170">Use hello following steps.</span></span>

#### <a name="enable-hello-rule-for-a-specific-management-server"></a><span data-ttu-id="71cf6-171">특정 관리 서버에 대 한 hello 규칙을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="71cf6-171">Enable hello rule for a specific management server</span></span>

1. <span data-ttu-id="71cf6-172">Hello에 **제작** hello 규칙에 대 한 검색 hello Operations Manager 콘솔의 작업 영역 *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행* hello에 **규칙** 창.</span><span class="sxs-lookup"><span data-stu-id="71cf6-172">In hello **Authoring** workspace of hello Operations Manager console, search for hello rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in hello **Rules** pane.</span></span>
2. <span data-ttu-id="71cf6-173">Hello 검색 결과에서 선택 hello 텍스트를 포함 하는 hello *유형: 관리 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-173">In hello search results, select hello one that includes hello text *Type: Management Server*.</span></span>
3. <span data-ttu-id="71cf6-174">Hello 규칙을 마우스 오른쪽 단추로 누른 **재정의** > **클래스의 특정 개체: 관리 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-174">Right-click hello rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="71cf6-175">Hello 사용 가능한 관리 서버 목록에 hello 규칙 실행 해야 하는 hello 관리 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-175">In hello available management servers list, select hello management server where hello rule should run.</span></span>
5.  <span data-ttu-id="71cf6-176">재정의 값을 너무 변경 해야**True** hello에 대 한 **Enabled** 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-176">Ensure that you change override value too**True** for hello **Enabled** parameter value.</span></span>  
    <span data-ttu-id="71cf6-177">![재정의 매개 변수](./media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="71cf6-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="71cf6-178">이 창에 여전히 동안 hello hello hello 다음 절차를 사용 하 여 실행 빈도 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-178">While still in this window, configure hello frequency of hello run using hello next procedure.</span></span>

#### <a name="configure-hello-run-frequency"></a><span data-ttu-id="71cf6-179">Hello 실행 빈도 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-179">Configure hello run frequency</span></span>

<span data-ttu-id="71cf6-180">hello 평가 모든 10, 080 분 (또는 7 일), 구성 된 toorun hello 기본 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-180">hello assessment is configured toorun every 10,080 minutes (or seven days), hello default interval.</span></span> <span data-ttu-id="71cf6-181">Hello 값 tooa 1440 분 (또는 1 일)의 최소 값을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-181">You can override hello value tooa minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="71cf6-182">hello 값 연속 평가 실행 사이 필요한 hello 최소 시간 간격을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-182">hello value represents hello minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="71cf6-183">toooverride hello 간격을 사용 하 여 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-183">toooverride hello interval, use hello steps below.</span></span>

1. <span data-ttu-id="71cf6-184">Hello에 **제작** hello 규칙에 대 한 검색 hello Operations Manager 콘솔의 작업 영역 *Microsoft System Center Advisor SCOM 평가 평가 규칙 실행* hello에 **규칙** 창.</span><span class="sxs-lookup"><span data-stu-id="71cf6-184">In hello **Authoring** workspace of hello Operations Manager console, search for hello rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in hello **Rules** pane.</span></span>
2. <span data-ttu-id="71cf6-185">Hello 검색 결과에서 선택 hello 텍스트를 포함 하는 hello *유형: 관리 서버*합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-185">In hello search results, select hello one that includes hello text *Type: Management Server*.</span></span>
3. <span data-ttu-id="71cf6-186">Hello 규칙을 마우스 오른쪽 단추로 누른 **재정의 hello 규칙** > **클래스의 모든 개체: 관리 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-186">Right-click hello rule and then click **Override hello Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="71cf6-187">변경 hello **간격** 매개 변수 값 tooyour 원하는 간격 값입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-187">Change hello **Interval** parameter value tooyour desired interval value.</span></span> <span data-ttu-id="71cf6-188">Hello 아래 예제에서는 hello 값은 설정 too1440 분 (1 일)입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-188">In hello example below, hello value is set too1440 minutes (one day).</span></span>  
    <span data-ttu-id="71cf6-189">![간격 매개 변수](./media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="71cf6-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="71cf6-190">Hello 값 1440 분 보다 tooless 설정 되 면 hello 규칙 1 일 간격으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-190">If hello value is set tooless than 1440 minutes, then hello rule runs at a one day interval.</span></span> <span data-ttu-id="71cf6-191">이 예제에서는 hello 규칙 hello 간격 값을 무시 하 고 1 일의 주파수로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-191">In this example, hello rule ignores hello interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="71cf6-192">권장 사항 우선 순위 이해</span><span class="sxs-lookup"><span data-stu-id="71cf6-192">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="71cf6-193">작성 된 모든 권장 hello hello 권장 사항의 상대적 중요도 식별 하는 가중치 값을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-193">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="71cf6-194">Hello 10 가장 중요 한 권장 구성만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-194">Only hello 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="71cf6-195">가중치 계산 방법</span><span class="sxs-lookup"><span data-stu-id="71cf6-195">How weights are calculated</span></span>

<span data-ttu-id="71cf6-196">가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-196">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="71cf6-197">hello *확률* 식별 된 문제로 인해 문제가 발생 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-197">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="71cf6-198">더 높은 확률을 tooa hello 권장 사항의 전체 점을 수도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-198">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
- <span data-ttu-id="71cf6-199">hello *영향* 문제가 발생 하는 경우 조직에 hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-199">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="71cf6-200">영향이 높을수록 tooa hello 권장 사항의 전체 점을 수도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-200">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
- <span data-ttu-id="71cf6-201">hello *노력* tooimplement hello 권장 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-201">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="71cf6-202">노력이 높을수록 tooa 전체 점수가 작아집니다 hello 권장 사항에 대 한 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-202">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="71cf6-203">각 권장 사항에 대 한 가중치 hello은 각 주요 영역에 대해 사용할 수 있는 총 점수 hello에 대 한 백분율로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-203">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="71cf6-204">예를 들어 hello 가용성 및 비즈니스 연속성 중점 영역 권장 사항 점수가 5%가 있으면 해당 권장 사항을 구현 전체 가용성 및 비즈니스 연속성 점수에서 5% 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-204">For example, if a recommendation in hello Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="71cf6-205">주요 영역</span><span class="sxs-lookup"><span data-stu-id="71cf6-205">Focus areas</span></span>

<span data-ttu-id="71cf6-206">**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-206">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="71cf6-207">**성능 및 확장성** -이 포커스 영역 표시 권장 사항을 toohelp 조직의 IT 인프라 증가, IT 환경의 현재 성능 요구 사항을 충족 하며 수 toorespond toochanging 있는지 확인 하십시오 인프라 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-207">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="71cf6-208">**업그레이드, 마이그레이션 및 배포** -이 포커스 영역 표시 권장 사항을 toohelp 업그레이드, 마이그레이션 및 SQL Server tooyour 기존 인프라를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-208">**Upgrade, Migration, and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="71cf6-209">**작업 및 모니터링** -이 포커스 영역 표시 권장 사항을 toohelp 약식 IT 운영을 예방 유지 관리를 구현 하 고 성능을 최대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-209">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="71cf6-210">목표로 해야 tooscore 모든 중점 영역에서 100%?</span><span class="sxs-lookup"><span data-stu-id="71cf6-210">Should you aim tooscore 100% in every focus area?</span></span>

<span data-ttu-id="71cf6-211">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-211">Not necessarily.</span></span> <span data-ttu-id="71cf6-212">hello 권장 사항은 hello 지식과 수천 고객 방문에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-212">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="71cf6-213">그러나 서버 인프라는 동일 hello 및 특정 권장 사항의 관련성이 더 높을 tooyou 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-213">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="71cf6-214">예를 들어 일부 보안 권장 사항의 관련성이 낮이 노출된 toohello 인터넷 없으면 가상 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-214">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="71cf6-215">일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-215">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="71cf6-216">성숙한 비즈니스에 중요 한 tooa 문제도 tooa 시작에 덜 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-216">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="71cf6-217">수 tooidentify 우선 하는 주요 영역을 다음 점수가 시간에 따라 어떻게 변경 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-217">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="71cf6-218">모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-218">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="71cf6-219">이 지침 tooevaluate를 사용 하 여 hello 권장 사항 구현에 적절 한지, 조직의 IT 서비스 및 hello 비즈니스 요구의 hello 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-219">Use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="71cf6-220">평가 주요 영역 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="71cf6-220">Use assessment focus area recommendations</span></span>

<span data-ttu-id="71cf6-221">OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-221">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="71cf6-222">솔루션 설치에 대 한 더 tooread 참조 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-222">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="71cf6-223">설치 된 후 OMS의 개요 페이지 hello에 hello System Center Operations Manager 평가 타일을 사용 하 여 hello 권장 사항 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-223">After it is installed, you can view hello summary of recommendations by using hello System Center Operations Manager Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="71cf6-224">보기 hello 인프라와 다음 권장 사항에 주입할에 대 한 호환성 평가 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-224">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="71cf6-225">포커스 영역과 take 해결 작업에 대 한 tooview 권장 사항</span><span class="sxs-lookup"><span data-stu-id="71cf6-225">tooview recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="71cf6-226">Hello에 **개요** 페이지에서 hello **System Center Operations Manager 평가** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-226">On hello **Overview** page, click hello **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="71cf6-227">Hello에 **System Center Operations Manager 평가** 페이지 hello 중점 영역 블레이드 중 하나에 hello 요약 정보를 검토 한 다음 하나 해당 주요 영역에 대 한 권장 사항을 tooview를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-227">On hello **System Center Operations Manager Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="71cf6-228">Hello 주요 영역 페이지에서 사용자 환경에 대 한 우선 순위를 지정 하는 hello 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-228">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="71cf6-229">권장 클릭 **영향을 받는 개체** hello 권장 사항을 따르면 이유에 대 한 자세한 내용을 tooview 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-229">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="71cf6-230">![주요 영역](./media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="71cf6-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="71cf6-231">**권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-231">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="71cf6-232">Hello 항목 해결 되 면 이후 평가 기록 동작이 수행 되었습니다 및 규정 준수 점수를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-232">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="71cf6-233">수정된 항목은 **전달된 개체**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-233">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="71cf6-234">권장 사항 무시</span><span class="sxs-lookup"><span data-stu-id="71cf6-234">Ignore recommendations</span></span>

<span data-ttu-id="71cf6-235">권장 사항을 tooignore 원하는 설정한 경우에 OMS 평가 결과에 나타나지 않도록 tooprevent 권장 사항을 사용 하는 텍스트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-235">If you have recommendations that you want tooignore, you can create a text file that OMS uses tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a><span data-ttu-id="71cf6-236">원하는 tooignore tooidentify 권장 사항</span><span class="sxs-lookup"><span data-stu-id="71cf6-236">tooidentify recommendations that you want tooignore</span></span>

1. <span data-ttu-id="71cf6-237">Tooyour 작업 영역에 로그인 하 고 로그 검색을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-237">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="71cf6-238">사용자 환경의 컴퓨터에 대 한 실패 한 쿼리 toolist 권장 사항을 따르면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-238">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="71cf6-239">표시 된 스크린 샷 hello 로그 검색 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-239">Here's a screen shot showing hello Log Search query:</span></span>  
    ![로그 검색](./media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="71cf6-241">권장 tooignore 되도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-241">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="71cf6-242">Hello 다음 절차에서 RecommendationId에 대 한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-242">You'll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="71cf6-243">IgnoreRecommendations.txt 텍스트 파일을 사용 하 여 toocreate</span><span class="sxs-lookup"><span data-stu-id="71cf6-243">toocreate and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="71cf6-244">IgnoreRecommendations.txt라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-244">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="71cf6-245">붙여넣거나 OMS tooignore 별도 줄에 원하는 하 고 저장 하 고 hello 파일을 닫고 각 권장 사항에 대 한 각 RecommendationId를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-245">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="71cf6-246">Hello 파일을 hello OMS tooignore 권장 사항을 원하는 각 컴퓨터에서 폴더를 다음에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-246">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
4. <span data-ttu-id="71cf6-247">Hello Operations Manager 관리 서버- *SystemDrive*: files\microsoft System Center 2012 R2\Operations Manager\Server 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-247">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="71cf6-248">권장 사항이 무시 되는지 tooverify</span><span class="sxs-lookup"><span data-stu-id="71cf6-248">tooverify that recommendations are ignored</span></span>

1. <span data-ttu-id="71cf6-249">기본적으로 7 일 간격 hello 예약 된 다음 평가 실행 된 후 권장 사항은 무시 됨으로 표시 되 고 hello 평가 대시보드에 표시 되지 것입니다 hello 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-249">After hello next scheduled assessment runs, by default every seven days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="71cf6-250">다음 로그 검색 쿼리 toolist hello 모든 무시 하는 hello 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-250">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="71cf6-251">나중에 권장 사항을 무시 toosee 한다고 결정 하면 IgnoreRecommendations.txt 파일을 제거 하거나 Recommendationid를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-251">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="71cf6-252">System Center Operations Manager 평가 솔루션 FAQ</span><span class="sxs-lookup"><span data-stu-id="71cf6-252">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="71cf6-253">*Hello 평가 솔루션 toomy OMS 작업 영역을 추가 했습니다. 하지만 hello 권장 사항 표시 되지 않습니다. 이유*</span><span class="sxs-lookup"><span data-stu-id="71cf6-253">*I added hello assessment solution toomy OMS workspace. But I don’t see hello recommendations. Why not?*</span></span> <span data-ttu-id="71cf6-254">Hello 솔루션을 추가한 후 hello OMS 대시보드에서 단계 보기에 대 한 hello 권장 사항을 따르면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-254">After adding hello solution, use hello following steps view hello recommendations on hello OMS dashboard.</span></span>  

- [<span data-ttu-id="71cf6-255">System Center Operations Manager 평가 대 한 hello 계정으로 실행 계정 설정</span><span class="sxs-lookup"><span data-stu-id="71cf6-255">Set hello Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="71cf6-256">Hello System Center Operations Manager 평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="71cf6-256">Configure hello System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="71cf6-257">*이 방식으로 tooconfigure 얼마나 자주 hello 평가 실행 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-257">*Is there a way tooconfigure how often hello assessment runs?*</span></span> <span data-ttu-id="71cf6-258">예.</span><span class="sxs-lookup"><span data-stu-id="71cf6-258">Yes.</span></span> <span data-ttu-id="71cf6-259">참조 [실행 빈도 구성 hello](#configure-the-run-frequency)합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-259">See [Configure hello run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="71cf6-260">*System Center Operations Manager 평가 솔루션 hello 추가한 후 다른 서버가 발견 되 면이 서버를 평가?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-260">*If another server is discovered after I’ve added hello System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="71cf6-261">예, 검색된 이후 기본적으로 7일마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-261">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="71cf6-262">*데이터 수집을 hello는 hello 프로세스의 hello 이름은 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-262">*What is hello name of hello process that does hello data collection?*</span></span> <span data-ttu-id="71cf6-263">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="71cf6-263">AdvisorAssessment.exe</span></span>

<span data-ttu-id="71cf6-264">*Hello AdvisorAssessment.exe 프로세스를 실행 하나요?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-264">*Where does hello AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="71cf6-265">AdvisorAssessment.exe는 hello 평가 규칙이 활성화 되어 hello hello 관리 서버의 health Service에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-265">AdvisorAssessment.exe runs under hello HealthService of hello management server where hello assessment rule is enabled.</span></span> <span data-ttu-id="71cf6-266">이 프로세스를 사용하는 경우 전체 환경에 대한 검색은 원격 데이터 수집을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-266">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="71cf6-267">*데이터 수집에 시간이 얼마나 걸리나요?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-267">*How long does it take for data collection?*</span></span> <span data-ttu-id="71cf6-268">Hello 서버에서 데이터 수집에는 약 1 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-268">Data collection on hello server takes about one hour.</span></span> <span data-ttu-id="71cf6-269">Operations Manager 인스턴스 또는 데이터베이스가 많은 환경에서는 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-269">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="71cf6-270">*경우에 어떻게 1440 분 보다 hello 평가 tooless의 hello 간격 설정 해야 합니까?*  hello 평가 하루에 한 번의 최대는 미리 구성 된 toorun 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-270">*What if I set hello interval of hello assessment tooless than 1440 minutes?* hello assessment is pre-configured toorun at a maximum of once per day.</span></span> <span data-ttu-id="71cf6-271">Hello 간격 값 tooa 값을 1440 분 안에 재정의할 hello 평가 hello 간격 값으로 분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-271">If you override hello interval value tooa value less than 1440 minutes, then hello assessment uses 1440 minutes as hello interval value.</span></span>

<span data-ttu-id="71cf6-272">*어떻게 tooknow 필수 구성 요소 오류가 발생 하는 경우?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-272">*How tooknow if there are pre-requisite failures?*</span></span> <span data-ttu-id="71cf6-273">Hello 평가 실행 하는 경우 결과 표시 되지 않으면 다음 되었을 일부 hello hello 평가 대 한 필수 구성 요소 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-273">If hello assessment ran and you don't see results, then it is likely that some of hello pre-requisites for hello assessment failed.</span></span> <span data-ttu-id="71cf6-274">쿼리를 실행할 수 있습니다: `Type=Operation Solution=SCOMAssessment` 및 `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` 로그 검색 toosee hello에 필수 구성 요소 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-274">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search toosee hello failed pre-requisites.</span></span>

<span data-ttu-id="71cf6-275">*필수 구성 요소 오류에 `Failed tooconnect toohello SQL Instance (….).` 메시지가 있습니다. Hello 문제는 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-275">*There is a `Failed tooconnect toohello SQL Instance (….).` message in pre-requisite failures. What is hello issue?*</span></span> <span data-ttu-id="71cf6-276">AdvisorAssessment.exe, 데이터를 수집 하는 hello 프로세스 hello hello 관리 서버의 health Service에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-276">AdvisorAssessment.exe, hello process that collects data, runs under hello HealthService of hello management server.</span></span> <span data-ttu-id="71cf6-277">Hello 평가의 일부로 hello 프로세스 tooconnect toohello hello Operations Manager 데이터베이스는 존재 하는 SQL Server를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-277">As part of hello assessment, hello process attempts tooconnect toohello SQL Server where hello Operations Manager database is present.</span></span> <span data-ttu-id="71cf6-278">방화벽 규칙 hello 연결 toohello SQL Server 인스턴스를 차단 하는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-278">This error can occur when firewall rules block hello connection toohello SQL Server instance.</span></span>

<span data-ttu-id="71cf6-279">*어떤 유형의 데이터를 수집 하나요?*  hello 데이터 형식에 따라 수집 됩니다: Windows PowerShell, SQL 쿼리 및 파일 정보 수집기를 통해 WMI-데이터 요금-레지스트리 데이터-이벤트 로그 데이터 요금-Operations Manager 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-279">*What type of data is collected?* hello following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="71cf6-280">*Tooconfigure 실행 계정으로 있는 이유*</span><span class="sxs-lookup"><span data-stu-id="71cf6-280">*Why do I have tooconfigure a Run As Account?*</span></span> <span data-ttu-id="71cf6-281">Operations Manager 서버의 경우 다양한 SQL 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-281">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="71cf6-282">해당 템플릿을 toorun, 실행 계정을 사용 하 여 필요한 권한을 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-282">In order for them toorun, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="71cf6-283">또한 로컬 관리자 자격 증명이 필요한 tooquery WMI 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-283">In addition, local administrator credentials are required tooquery WMI.</span></span>

<span data-ttu-id="71cf6-284">*왜 hello 상위 10 개의 권장 사항만 표시 하나요?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-284">*Why display only hello top 10 recommendations?*</span></span> <span data-ttu-id="71cf6-285">작업의 완전 한 목록이 고 부담이 된 목록을 제공 하는 대신 먼저 hello 우선 순위가 지정 된 권장 사항 해결에 주의 기울여야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-285">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="71cf6-286">권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-286">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="71cf6-287">Toosee hello에 대 한 자세한 목록을 원하는 경우 로그 검색을 사용 하 여 모든 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-287">If you prefer toosee hello detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="71cf6-288">*방식으로 tooignore 권장 사항은 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="71cf6-288">*Is there a way tooignore a recommendation?*</span></span> <span data-ttu-id="71cf6-289">예, hello 참조 [권장 구성은 무시할](#Ignore-recommendations)합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-289">Yes, see hello [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="71cf6-290">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71cf6-290">Next steps</span></span>

- <span data-ttu-id="71cf6-291">[로그 검색](log-analytics-log-searches.md) tooview System Center Operations Manager 평가 데이터 및 권장 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cf6-291">[Search logs](log-analytics-log-searches.md) tooview detailed System Center Operations Manager Assessment data and recommendations.</span></span>
