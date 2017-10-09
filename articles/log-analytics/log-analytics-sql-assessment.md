---
title: "aaaOptimize Azure 로그 분석으로 SQL Server 환경 | Microsoft Docs"
description: "Azure 로그 분석 hello SQL 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 SQL server 환경의 hello을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="1f334-103">Hello 로그 분석에서 SQL 평가 솔루션으로 SQL Server 환경 최적화</span><span class="sxs-lookup"><span data-stu-id="1f334-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![SQL 평가 기호](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="1f334-105">SQL 평가 솔루션 tooassess 일정 한 간격으로 위험 및 상태를 서버 환경 hello hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="1f334-106">이 문서는 잠재적인 문제에 대 한 수정 동작을 수행할 수 있도록 hello 솔루션을 설치 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="1f334-107">이 솔루션은 권장 사항 특정 tooyour 배포 된 서버 인프라의 우선 순위 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="1f334-108">hello 권장 사항은 6 개의 포커스 위험 hello 수정 작업을 수행 하는 데 도움이 신속 하 게 영역 이해으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="1f334-109">hello 권장 hello 지식과 수천 고객 방문에서에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="1f334-110">각 권장 사항은 문제가 tooyou에 중요할 수 있는 이유 및 tooimplement hello 변경 내용을 제안 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="1f334-111">가장 중요 한 tooyour 조직 되어 하 여 위험이 없는 정상 환경을 실행 하기 위한 진행률을 추적 하는 주요 영역을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="1f334-112">Hello에 중점 영역에 대 한 정보를 표시 한 평가 결과 완료 된, 요약 hello 솔루션을 추가한 후 **SQL 평가** hello 사용자 환경의 인프라에에서 대 한 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="1f334-113">hello 다음 섹션에서는 설명 toouse hello에 대 한 정보를 hello 방법을 **SQL 평가** 대시보드를 보고 하 고 취할 수 있는 권장 SQL server 인프라에 대 한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL 평가 타일의 이미지](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL 평가 대시보드의 이미지](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="1f334-116">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="1f334-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="1f334-117">SQL 평가 hello Standard, Developer 및 Enterprise edition 용 SQL Server의 현재 지원 되는 모든 버전에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="1f334-118">다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="1f334-119">SQL Server가 설치된 서버에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="1f334-120">SQL 평가 솔루션 hello OMS 에이전트가 각 컴퓨터에 설치 된.NET Framework 4 지원 되는 버전이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="1f334-121">순서 tooinstall hello 솔루션의 경우 Azure 포털 hello를 사용 하 여 hello 사용자는 관리자 또는 참가자 toohello Azure 구독 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="1f334-122">또한 hello 사용자 역할의 멤버인 hello OMS 작업 영역 관리자 또는 참가자 hello OMS 포털에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="1f334-123">SQL 평가 통한 hello Operations Manager 에이전트를 사용 하는 경우 Operations Manager Run-As 계정을 toouse가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="1f334-124">자세한 내용은 아래의 [OMS용 Operations Manager 실행 계정](#operations-manager-run-as-accounts-for-oms) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f334-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1f334-125">hello MMA 에이전트는 Operations Manager Run-As 계정을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="1f334-126">Hello 프로세스를 사용 하 여 OMS 작업 영역에서 설명 하는 hello SQL 평가 솔루션 tooyour 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="1f334-127">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="1f334-128">Hello 솔루션을 추가한 후 에이전트와 함께 tooservers hello AdvisorAssessment.exe 파일에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="1f334-129">구성 데이터를 읽고 처리를 위해 hello 클라우드에서 toohello OMS 서비스로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="1f334-130">논리는 수신 적용된 toohello 데이터 및 hello 클라우드 서비스는 hello 데이터를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="1f334-131">SQL 평가 데이터 수집 정보</span><span class="sxs-lookup"><span data-stu-id="1f334-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="1f334-132">SQL 평가는 WMI 데이터, 레지스트리 데이터, 성능 데이터 및 사용 하도록 설정한 hello 에이전트를 사용 하 여 SQL Server 동적 관리 뷰 결과 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="1f334-133">hello 다음 표에서 데이터 수집 방법과 에이전트, Operations Manager (SCOM)가 필요한 지 여부와 방법을 에이전트에서 주로 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="1f334-134">플랫폼</span><span class="sxs-lookup"><span data-stu-id="1f334-134">platform</span></span> | <span data-ttu-id="1f334-135">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="1f334-135">Direct Agent</span></span> | <span data-ttu-id="1f334-136">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="1f334-136">SCOM agent</span></span> | <span data-ttu-id="1f334-137">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="1f334-137">Azure Storage</span></span> | <span data-ttu-id="1f334-138">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="1f334-138">SCOM required?</span></span> | <span data-ttu-id="1f334-139">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="1f334-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="1f334-140">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="1f334-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1f334-141">Windows</span><span class="sxs-lookup"><span data-stu-id="1f334-141">Windows</span></span> | <span data-ttu-id="1f334-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1f334-142">&#8226;</span></span> | <span data-ttu-id="1f334-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1f334-143">&#8226;</span></span> |  |  | <span data-ttu-id="1f334-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1f334-144">&#8226;</span></span> |<span data-ttu-id="1f334-145">7 일</span><span class="sxs-lookup"><span data-stu-id="1f334-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="1f334-146">OMS용 Operations Manager 실행 계정</span><span class="sxs-lookup"><span data-stu-id="1f334-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="1f334-147">OMS의 로그 분석 hello Operations Manager 에이전트와 관리 그룹 toocollect를 사용 하 고 데이터 toohello OMS 서비스로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="1f334-148">Tooprovide 워크 로드에 대 한 관리 팩을 빌드합니다 OMS는 부가 가치 서비스.</span><span class="sxs-lookup"><span data-stu-id="1f334-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="1f334-149">각 작업은 도메인 계정과 같은 다른 보안 컨텍스트에서 작업 관련 권한이 toorun 관리 팩 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="1f334-150">Operations Manager 실행 계정을 구성 하 여 tooprovide 자격 증명 정보를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="1f334-151">SQL 평가 대 한 정보 tooset hello Operations Manager 실행 계정을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="1f334-152">SQL 평가 대 한 계정으로 실행 hello 설정</span><span class="sxs-lookup"><span data-stu-id="1f334-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="1f334-153">Hello SQL Server 관리 팩을 이미 사용 중인 경우 해당 실행 계정을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="1f334-154">tooconfigure hello SQL 실행 계정 hello 운영 콘솔에서</span><span class="sxs-lookup"><span data-stu-id="1f334-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="1f334-155">사용 하는 hello OMS 직접 hello SCOM 에이전트 보다는 에이전트, 관리 팩 hello는 항상 로컬 시스템 계정 hello의 hello 보안 컨텍스트에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="1f334-156">Skip 단계 1-5 아래 및 실행 하거나 NT AUTHORITY\SYSTEM hello 사용자 이름으로 지정 하는 샘플 T-SQL 또는 Powershell를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="1f334-157">Operations Manager에서 hello 운영 콘솔을 열고 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="1f334-158">**실행 구성**에서 **프로필**을 클릭하고 **OMS SQL 평가 실행 프로필**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="1f334-159">Hello에 **실행 계정** 페이지 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="1f334-160">SQL Server에 필요한 hello 자격 증명을 포함 하는 Windows 계정으로 실행 계정을 선택 하거나 클릭 **새로** toocreate 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1f334-161">hello 실행 계정 유형은 Windows 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="1f334-162">hello 실행 계정에 SQL Server 인스턴스를 호스팅하는 모든 Windows 서버에서 로컬 관리자 그룹의 일부 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="1f334-163">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-163">Click **Save**.</span></span>
6. <span data-ttu-id="1f334-164">수정 하 고 T-SQL 샘플에 나오는 각 SQL Server 인스턴스 toogrant 최소한의 권한만 필요한 tooRun 계정 tooperform SQL 평가에 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="1f334-165">그러나 않아도 toodo이 실행 계정을 이미 SQL Server 인스턴스에서 hello sysadmin 서버 역할의 일부인 경우 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="1f334-166">SQL 실행 계정 Windows PowerShell을 사용 하 여 tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="1f334-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="1f334-167">PowerShell 창을 열고 사용자 정보로 업데이트 한 후 스크립트를 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="1f334-168">권장 사항 우선 순위 이해</span><span class="sxs-lookup"><span data-stu-id="1f334-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="1f334-169">작성 된 모든 권장 hello hello 권장 사항의 상대적 중요도 식별 하는 가중치 값을 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="1f334-170">Hello 10 개의 가장 중요 한 권장 사항만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="1f334-171">가중치 계산 방법</span><span class="sxs-lookup"><span data-stu-id="1f334-171">How weights are calculated</span></span>
<span data-ttu-id="1f334-172">가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="1f334-173">hello *확률* 식별 된 문제로 인해 문제가 발생 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="1f334-174">더 높은 확률을 tooa hello 권장 사항의 전체 점을 수도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="1f334-175">hello *영향* 문제가 발생 하는 경우 조직에 hello 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="1f334-176">영향이 높을수록 tooa hello 권장 사항의 전체 점을 수도 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="1f334-177">hello *노력* tooimplement hello 권장 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="1f334-178">노력이 높을수록 tooa 전체 점수가 작아집니다 hello 권장 사항에 대 한 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="1f334-179">각 권장 사항에 대 한 가중치 hello은 각 주요 영역에 대해 사용할 수 있는 총 점수 hello에 대 한 백분율로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="1f334-180">예를 들어 hello 보안 및 규정 준수 주요 영역의 권장 사항 점수가 5%가 있으면 해당 권장 사항을 구현 전체 보안 및 규정 준수 점수에서 5% 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="1f334-181">주요 영역</span><span class="sxs-lookup"><span data-stu-id="1f334-181">Focus areas</span></span>
<span data-ttu-id="1f334-182">**보안 및 규정 준수** - 이 주요 영역은 잠재적 보안 위협 및 위반, 회사 정책, 기술, 법률 및 규정 준수 요구 사항 등에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="1f334-183">**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="1f334-184">**성능 및 확장성** -이 포커스 영역 표시 권장 사항을 toohelp 조직의 IT 인프라 증가, IT 환경의 현재 성능 요구 사항을 충족 하며 수 toorespond toochanging 있는지 확인 하십시오 인프라 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="1f334-185">**업그레이드, 마이그레이션 및 배포** -이 포커스 영역 표시 권장 사항을 toohelp 업그레이드, 마이그레이션 및 SQL Server tooyour 기존 인프라를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="1f334-186">**작업 및 모니터링** -이 포커스 영역 표시 권장 사항을 toohelp 약식 IT 운영을 예방 유지 관리를 구현 하 고 성능을 최대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="1f334-187">**변경 및 구성 관리** -이 중점 영역 권장 사항에 표시 toohelp 일상적인 작업 보호, 변경 인프라에 영향을 줄 tootrack 및 변경 제어 프로시저를 설정 및 감사 부정적인 하지 않습니다 시스템 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="1f334-188">목표로 해야 tooscore 모든 중점 영역에서 100%?</span><span class="sxs-lookup"><span data-stu-id="1f334-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="1f334-189">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-189">Not necessarily.</span></span> <span data-ttu-id="1f334-190">hello 권장 사항은 hello 지식과 수천 고객 방문에서 Microsoft 엔지니어가 얻은 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="1f334-191">그러나 서버 인프라는 동일 hello 및 특정 권장 사항의 관련성이 더 높을 tooyou 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="1f334-192">예를 들어 일부 보안 권장 사항의 관련성이 낮이 노출된 toohello 인터넷 없으면 가상 컴퓨터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="1f334-193">일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="1f334-194">성숙한 비즈니스에 중요 한 tooa 문제도 tooa 시작에 덜 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="1f334-195">수 tooidentify 우선 하는 주요 영역을 다음 점수가 시간에 따라 어떻게 변경 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="1f334-196">모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="1f334-197">Hello 권장 사항 구현에 적절 한지, 조직의 IT 서비스 및 hello 비즈니스 요구의 hello 특성을 지정 된이 지침 tooevaluate를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="1f334-198">평가 주요 영역 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="1f334-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="1f334-199">OMS에서 평가 솔루션을 사용 하려면 먼저 hello 솔루션이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="1f334-200">솔루션 설치에 대 한 더 tooread 참조 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="1f334-201">설치 된 후 OMS의 개요 페이지 hello에 hello SQL 평가 타일을 사용 하 여 hello 권장 사항 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="1f334-202">보기 hello 인프라와 다음 권장 사항에 주입할에 대 한 호환성 평가 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="1f334-203">포커스 영역과 take 해결 작업에 대 한 tooview 권장 사항</span><span class="sxs-lookup"><span data-stu-id="1f334-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="1f334-204">Hello에 **개요** 페이지에서 hello **SQL 평가** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="1f334-205">Hello에 **SQL 평가** 페이지 hello 중점 영역 블레이드 중 하나에 hello 요약 정보를 검토 한 다음 하나 해당 주요 영역에 대 한 권장 사항을 tooview를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="1f334-206">Hello 주요 영역 페이지에서 사용자 환경에 대 한 우선 순위를 지정 하는 hello 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="1f334-207">권장 클릭 **영향을 받는 개체** hello 권장 사항을 따르면 이유에 대 한 자세한 내용을 tooview 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="1f334-208">![SQL 평가 권장 사항 이미지](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="1f334-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="1f334-209">**권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="1f334-210">Hello 항목 해결 되 면 이후 평가 기록 동작이 수행 되었습니다 및 규정 준수 점수를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="1f334-211">수정된 항목은 **전달된 개체**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="1f334-212">권장 사항 무시</span><span class="sxs-lookup"><span data-stu-id="1f334-212">Ignore recommendations</span></span>
<span data-ttu-id="1f334-213">권장 사항을 tooignore 원하는 설정한 경우에 OMS 평가 결과에 나타나지 않도록 tooprevent 권장 사항을 사용 하는 텍스트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="1f334-214">tooidentify 권장 사항이 무시 합니다</span><span class="sxs-lookup"><span data-stu-id="1f334-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="1f334-215">Tooyour 작업 영역에 로그인 하 고 로그 검색을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="1f334-216">사용자 환경의 컴퓨터에 대 한 실패 한 쿼리 toolist 권장 사항을 따르면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="1f334-217">표시 된 스크린 샷 hello 로그 검색 쿼리는 다음과 같습니다: ![권장 구성 하지 못했습니다.](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="1f334-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="1f334-218">권장 tooignore 되도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="1f334-219">Hello 다음 절차에서 RecommendationId에 대 한 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="1f334-220">IgnoreRecommendations.txt 텍스트 파일을 사용 하 여 toocreate</span><span class="sxs-lookup"><span data-stu-id="1f334-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="1f334-221">IgnoreRecommendations.txt라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="1f334-222">붙여넣거나 OMS tooignore 별도 줄에 원하는 하 고 저장 하 고 hello 파일을 닫고 각 권장 사항에 대 한 각 RecommendationId를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="1f334-223">Hello 파일을 hello OMS tooignore 권장 사항을 원하는 각 컴퓨터에서 폴더를 다음에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="1f334-224">Microsoft Monitoring Agent (직접 또는 Operations Manager를 통해 연결)-hello로 컴퓨터에 *SystemDrive*: files\microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="1f334-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="1f334-225">Hello Operations Manager 관리 서버- *SystemDrive*: files\microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="1f334-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="1f334-226">권장 사항이 무시 되는지 tooverify</span><span class="sxs-lookup"><span data-stu-id="1f334-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="1f334-227">기본적으로 7 일 간격 hello 예약 된 다음 평가 실행 된 후 권장 사항은 무시 됨으로 표시 되 고 hello 평가 대시보드에 표시 되지 것입니다 hello 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="1f334-228">다음 로그 검색 쿼리 toolist hello 모든 무시 하는 hello 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="1f334-229">나중에 권장 사항을 무시 toosee 한다고 결정 하면 IgnoreRecommendations.txt 파일을 제거 하거나 Recommendationid를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="1f334-230">SQL 평가 솔루션 FAQ</span><span class="sxs-lookup"><span data-stu-id="1f334-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="1f334-231">*얼마나 자주 평가를 실행하나요?*</span><span class="sxs-lookup"><span data-stu-id="1f334-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="1f334-232">hello 평가 7 일 마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="1f334-233">*이 방식으로 tooconfigure 얼마나 자주 hello 평가 실행 있습니까?*</span><span class="sxs-lookup"><span data-stu-id="1f334-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="1f334-234">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-234">Not at this time.</span></span>

<span data-ttu-id="1f334-235">*SQL 평가 솔루션 hello 추가한 후 다른 서버가 발견 되 면이 서버를 평가?*</span><span class="sxs-lookup"><span data-stu-id="1f334-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="1f334-236">예, 발견되면 그 시간부터 7일마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="1f334-237">*서버 서비스를 해제 하 고 언제 수 제거 hello 평가에서?*</span><span class="sxs-lookup"><span data-stu-id="1f334-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="1f334-238">3주 동안 서버가 데이터를 전송하지 않은 경우 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="1f334-239">*데이터 수집을 hello는 hello 프로세스의 hello 이름은 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="1f334-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="1f334-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="1f334-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="1f334-241">*가 소요 데이터 toobe 수집에 대 한?*</span><span class="sxs-lookup"><span data-stu-id="1f334-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="1f334-242">hello 서버의 hello 실제 데이터 수집은 약 1 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="1f334-243">SQL 인스턴스 또는 데이터베이스가 많은 서버에서는 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="1f334-244">*어떤 유형의 데이터를 수집하나요?*</span><span class="sxs-lookup"><span data-stu-id="1f334-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="1f334-245">hello 다음 유형의 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="1f334-246">WMI</span><span class="sxs-lookup"><span data-stu-id="1f334-246">WMI</span></span>
  * <span data-ttu-id="1f334-247">레지스트리</span><span class="sxs-lookup"><span data-stu-id="1f334-247">Registry</span></span>
  * <span data-ttu-id="1f334-248">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="1f334-248">Performance counters</span></span>
  * <span data-ttu-id="1f334-249">SQL 동적 관리 뷰(DMV)</span><span class="sxs-lookup"><span data-stu-id="1f334-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="1f334-250">*방식으로 tooconfigure 데이터를 수집 하는 경우 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="1f334-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="1f334-251">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-251">Not at this time.</span></span>

<span data-ttu-id="1f334-252">*Tooconfigure 실행 계정으로 있는 이유*</span><span class="sxs-lookup"><span data-stu-id="1f334-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="1f334-253">SQL Server의 경우, 적은 수의 SQL 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="1f334-254">에 대 한 한 실행 계정 VIEW SERVER STATE 권한 tooSQL toorun를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="1f334-255">또한 순서 tooquery WMI 로컬 관리자 자격 증명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="1f334-256">*왜 hello 상위 10 개의 권장 사항만 표시 하나요?*</span><span class="sxs-lookup"><span data-stu-id="1f334-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="1f334-257">작업의 포함 된 긴 목록을 제공 하는 대신 먼저 hello 우선 순위가 지정 된 권장 사항 해결에 주의 기울여야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="1f334-258">권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="1f334-259">Toosee hello에 대 한 자세한 목록을 원하는 경우 hello OMS 로그 검색을 사용 하 여 모든 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="1f334-260">*방식으로 tooignore 권장 사항은 무엇입니까?*</span><span class="sxs-lookup"><span data-stu-id="1f334-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="1f334-261">예, 위의 [권장 사항 무시](#ignore-recommendations) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f334-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f334-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f334-262">Next steps</span></span>
* <span data-ttu-id="1f334-263">[로그 검색](log-analytics-log-searches.md) SQL 평가 데이터와 권장 tooview 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f334-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
