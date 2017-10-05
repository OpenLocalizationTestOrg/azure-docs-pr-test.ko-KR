---
title: "Azure Log Analytics를 사용하여 System Center Operations Manager 환경 최적화 | Microsoft Docs"
description: "System Center Operations Manager 평가 솔루션을 사용하여 일정한 간격으로 서버 환경의 위험 및 상태를 평가할 수 있습니다."
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
ms.openlocfilehash: 4992d98397da409f7c1cfbdeb40fdb0cdd0d2f19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-environment-with-the-system-center-operations-manager-assessment-preview-solution"></a><span data-ttu-id="a605c-103">System Center Operations Manager 평가(미리 보기) 솔루션을 사용하여 환경 최적화</span><span class="sxs-lookup"><span data-stu-id="a605c-103">Optimize your environment with the System Center Operations Manager Assessment (Preview) solution</span></span>

![System Center Operations Manager 평가 기호](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

<span data-ttu-id="a605c-105">System Center Operations Manager 평가 솔루션을 사용하여 일정한 간격으로 System Center Operations Manager 서버 환경의 위험 및 상태를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-105">You can use the System Center Operations Manager Assessment solution to assess the risk and health of your System Center Operations Manager server environments on a regular interval.</span></span> <span data-ttu-id="a605c-106">이 문서에서는 잠재적인 문제에 대해 올바른 조치를 취할 수 있도록 솔루션을 설치하고, 구성하고, 사용하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-106">This article helps you install, configure, and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="a605c-107">이 솔루션은 배포된 서버 인프라 관련 우선순위가 지정된 권장 사항 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="a605c-108">권장 사항은 신속하게 위험을 이해하고 수정 조치를 취할 수 있도록 네 가지 주요 영역으로 분류되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="a605c-109">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="a605c-110">각 권장 사항은 문제가 중요할 수 있는 이유 및 제안된 변경 내용을 구현하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="a605c-111">조직에 가장 중요한 주요 영역을 선택하여 위험이 없는 정상 환경을 실행 중인 프로그램의 진행을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="a605c-112">솔루션을 추가하고 평가가 완료되면 주요 영역의 요약 정보가 인프라에 대한 **System Center Operations Manager 평가** 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **System Center Operations Manager Assessment** dashboard for your infrastructure.</span></span> <span data-ttu-id="a605c-113">다음 섹션에서는 **System Center Operations Manager 평가** 대시보드의 정보를 사용하는 방법을 설명합니다. 여기서는 이 대시보드의 정보를 보고 SCOM 서버 인프라에 대한 권장 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-113">The following sections describe how to use the information on the **System Center Operations Manager Assessment** dashboard, where you can view and then take recommended actions for your SCOM infrastructure.</span></span>

![System Center Operations Manager 솔루션 타일](./media/log-analytics-scom-assessment/scom-tile.png)

![System Center Operations Manager 평가 대시보드](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="a605c-116">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="a605c-116">Installing and configuring the solution</span></span>

<span data-ttu-id="a605c-117">이 솔루션은 Microsoft System Operations Manager 2012 R2 및 2012 SP1과 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-117">The solution works with Microsoft System Operations Manager 2012 R2 and 2012 SP1.</span></span>

<span data-ttu-id="a605c-118">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-118">Use the following information to install and configure the solution.</span></span>

 - <span data-ttu-id="a605c-119">OMS에서 평가 솔루션을 사용하려면 먼저 솔루션이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-119">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="a605c-120">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)의 지침에 따라 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-120">Install the solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) or by following the instructions in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

 - <span data-ttu-id="a605c-121">작업 영역에 솔루션을 추가한 후에 대시보드의 System Center Operations Manager 평가 타일은 추가 구성이 필요하다는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-121">After adding the solution to the workspace, the System Center Operations Manager Assessment tile on the dashboard displays the additional configuration required message.</span></span> <span data-ttu-id="a605c-122">타일을 클릭하고 페이지에 언급한 구성 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-122">Click on the tile and follow the configuration steps mentioned in the page</span></span>

 ![System Center Operations Manager 대시보드 타일](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 <span data-ttu-id="a605c-124">OMS의 솔루션 구성 페이지에 설명한 단계를 수행하여 스크립트를 통해 System Center Operations Manager를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-124">Configuration of the System Center Operations Manager can be done through the script by following the steps mentioned in the configuration page of the solution in OMS.</span></span>

 <span data-ttu-id="a605c-125">대신, SCOM 콘솔을 통해 평가를 구성하려면 아래와 동일한 순서로 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-125">Instead, to configure the assessment through SCOM Console, follow the below steps in the same order</span></span>
1. [<span data-ttu-id="a605c-126">System Center Operations Manager 평가를 위한 계정으로 실행 설정</span><span class="sxs-lookup"><span data-stu-id="a605c-126">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
2. [<span data-ttu-id="a605c-127">System Center Operations Manager 평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="a605c-127">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a><span data-ttu-id="a605c-128">System Center Operations Manager 평가 데이터 수집 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a605c-128">System Center Operations Manager assessment data collection details</span></span>

<span data-ttu-id="a605c-129">System Center Operations Manager 평가는 사용하도록 설정한 서버를 사용하여 Windows PowerShell, SQL 쿼리, 파일 정보 수집기를 통해 WMI 데이터, 레지스트리 데이터, EventLog 데이터, Operations Manager 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-129">The System Center Operations Manager assessment collects WMI data, Registry data, EventLog data, Operations Manager data through Windows PowerShell, SQL Queries, File information collector using the server that you have enabled.</span></span>

<span data-ttu-id="a605c-130">다음 테이블은 System Center Operations Manager 평가에 대한 데이터 수집 방법 및 에이전트에서 데이터가 수집되는 빈도를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-130">The following table shows data collection methods for System Center Operations Manager Assessment, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="a605c-131">플랫폼</span><span class="sxs-lookup"><span data-stu-id="a605c-131">platform</span></span> | <span data-ttu-id="a605c-132">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="a605c-132">Direct Agent</span></span> | <span data-ttu-id="a605c-133">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="a605c-133">SCOM agent</span></span> | <span data-ttu-id="a605c-134">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="a605c-134">Azure Storage</span></span> | <span data-ttu-id="a605c-135">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="a605c-135">SCOM required?</span></span> | <span data-ttu-id="a605c-136">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="a605c-136">SCOM agent data sent via management group</span></span> | <span data-ttu-id="a605c-137">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="a605c-137">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a605c-138">Windows</span><span class="sxs-lookup"><span data-stu-id="a605c-138">Windows</span></span> | | | | <span data-ttu-id="a605c-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="a605c-139">&#8226;</span></span> | | <span data-ttu-id="a605c-140">7일</span><span class="sxs-lookup"><span data-stu-id="a605c-140">seven days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="a605c-141">OMS용 Operations Manager 실행 계정</span><span class="sxs-lookup"><span data-stu-id="a605c-141">Operations Manager run-as accounts for OMS</span></span>

<span data-ttu-id="a605c-142">OMS는 부가 가치 서비스를 제공하는 작업을 위해 관리 팩을 토대로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-142">OMS builds on management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="a605c-143">도메인 계정과 같은 다른 보안 컨텍스트에서 관리 팩을 실행하려면 각 작업에 작업 관련 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-143">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="a605c-144">Operations Manager 실행 계정을 구성하여 자격 증명 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-144">Configure an Operations Manager Run As account to provide credential information.</span></span>

<span data-ttu-id="a605c-145">다음 정보를 사용하여 System Center Operations Manager 평가를 위한 Operations Manager 실행 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-145">Use the following information to set the Operations Manager run-as account for System Center Operations Manager Assessment.</span></span>

### <a name="set-the-run-as-account"></a><span data-ttu-id="a605c-146">실행 계정 설정</span><span class="sxs-lookup"><span data-stu-id="a605c-146">Set the Run As account</span></span>

1. <span data-ttu-id="a605c-147">Operations Manager 콘솔에서 **관리** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-147">In the Operations Manager Console, go to the **Administration** tab.</span></span>
2. <span data-ttu-id="a605c-148">**Run As Configuration**(실행 구성)에서 **계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-148">Under the **Run As Configuration**, click **Accounts**.</span></span>
3. <span data-ttu-id="a605c-149">Windows 계정을 만드는 마법사에 따라 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-149">Create the Run As Account, following through the Wizard, creating a Windows account.</span></span> <span data-ttu-id="a605c-150">사용할 계정은 아래와 같은 필수 조건을 모두 충족하는 식별된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-150">The account to use is the one identified and having all the prerequisites below:</span></span>

    >[!NOTE]
    <span data-ttu-id="a605c-151">실행 계정은 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-151">The Run As account must meet following requirements:</span></span>
    - <span data-ttu-id="a605c-152">환경의 모든 서버에서 로컬 관리자 그룹의 도메인 계정 구성원(모든 Operations Manager 역할 - 관리 서버, OpsMgr 데이터베이스, 데이터 웨어하우스, 보고, 웹 콘솔, 게이트웨이)</span><span class="sxs-lookup"><span data-stu-id="a605c-152">A domain account member of the local Administrators group on all servers in the environment (All Operations Manager Roles - Management Server, OpsMgr Database, Data Warehouse, Reporting, Web Console, Gateway)</span></span>
    - <span data-ttu-id="a605c-153">평가 중인 관리 그룹에 대한 Operation Manager 관리자 역할</span><span class="sxs-lookup"><span data-stu-id="a605c-153">Operation Manager Administrator Role for the management group being assessed</span></span>
    - <span data-ttu-id="a605c-154">[스크립트](#sql-script-to-grant-granular-permissions-to-the-run-as-account)를 실행하여 Operations Manager에서 사용하는 SQL 인스턴스의 실행 계정에 세부적인 사용 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-154">Execute the [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) to grant granular permissions to the account on SQL instance used by Operations Manager.</span></span>
      <span data-ttu-id="a605c-155">참고: 이 계정에 sysadmin 권한이 이미 있는 경우 스크립트 실행을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-155">Note: If this account has sysadmin rights already, then skip the script execution.</span></span>

4. <span data-ttu-id="a605c-156">**배포 보안**에서 **More secure**(보다 안전)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-156">Under **Distribution Security**, select **More secure**.</span></span>
5. <span data-ttu-id="a605c-157">계정이 분산되는 관리 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-157">Specify the management server where the account is distributed.</span></span>
3. <span data-ttu-id="a605c-158">Run As Configuration(실행 구성)으로 돌아가서 **프로필**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-158">Go back to the Run As Configuration and click **Profiles**.</span></span>
4. <span data-ttu-id="a605c-159">*SCOM 평가 프로필*을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-159">Search for the *SCOM Assessment Profile*.</span></span>
5. <span data-ttu-id="a605c-160">프로필 이름은 *Microsoft System Center Advisor SCOM 평가 실행 프로필*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-160">The profile name should be: *Microsoft System Center Advisor SCOM Assessment Run As Profile*.</span></span>
6. <span data-ttu-id="a605c-161">오른쪽 클릭하여 속성을 업데이트하고 조금 전 3단계에서 만든 실행 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-161">Right-click and update its properties and add the recently created Run As Account you created in step 3.</span></span>

### <a name="sql-script-to-grant-granular-permissions-to-the-run-as-account"></a><span data-ttu-id="a605c-162">실행 계정에 대한 세부적인 사용 권한을 부여하는 SQL 스크립트</span><span class="sxs-lookup"><span data-stu-id="a605c-162">SQL script to grant granular permissions to the Run As account</span></span>

<span data-ttu-id="a605c-163">Operations Manager에 사용되는 SQL 인스턴스에서 다음 SQL 스크립트를 실행하여 실행 계정에 필요한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-163">Execute the following SQL script to grant required permissions to the Run As account on the SQL instance used by Operations Manager.</span></span>

```
-- Replace <UserName> with the actual user name being used as Run As Account.
USE master

-- Create login for the user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions to user.
GRANT VIEW SERVER STATE TO [UserName]
GRANT VIEW ANY DEFINITION TO [UserName]
GRANT VIEW ANY DATABASE TO [UserName]

-- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
-- NOTE: This command must be run anytime new databases are added to SQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT To [UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace the Operations Manager database name with the one in your environment
Use [OperationsManager];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager DatawareHouse database name with the one in your environment
Use [OperationsManagerDW];
GRANT SELECT To [UserName]
GO

--Replace the Operations Manager Audit Collection database name with the one in your environment
Use [OperationsManagerAC];
GRANT SELECT To [UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace the Operations Manager database name with the one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-the-assessment-rule"></a><span data-ttu-id="a605c-164">평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="a605c-164">Configure the assessment rule</span></span>

<span data-ttu-id="a605c-165">System Center Operations Manager 평가 솔루션의 관리 팩에는 *Microsoft System Center Advisor SCOM 평가 실행 평가 규칙*이라는 규칙이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-165">The System Center Operations Manager Assessment solution’s management pack includes a rule named *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule*.</span></span> <span data-ttu-id="a605c-166">이 규칙은 평가 실행을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-166">This rule is responsible for running the assessment.</span></span> <span data-ttu-id="a605c-167">규칙을 사용하도록 설정하고 빈도를 구성하려면 아래 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-167">To enable the rule and configure the frequency, use the procedures below.</span></span>

<span data-ttu-id="a605c-168">기본적으로 Microsoft System Center Advisor SCOM 평가 실행 평가 규칙은 사용하지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-168">By default, the Microsoft System Center Advisor SCOM Assessment Run Assessment Rule is disabled.</span></span> <span data-ttu-id="a605c-169">평가를 실행하려면 관리 서버에서 규칙을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-169">To run the assessment, you must enable the rule on a management server.</span></span> <span data-ttu-id="a605c-170">다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a605c-170">Use the following steps.</span></span>

#### <a name="enable-the-rule-for-a-specific-management-server"></a><span data-ttu-id="a605c-171">특정 관리 서버에 대한 규칙을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a605c-171">Enable the rule for a specific management server</span></span>

1. <span data-ttu-id="a605c-172">Operations Manager 콘솔의 **제작** 작업 영역에서 **규칙** 창의 *Microsoft System Center Advisor SCOM 평가 실행 평가 규칙*이라는 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-172">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="a605c-173">검색 결과에서 *유형: 관리 서버*라는 텍스트를 포함하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-173">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="a605c-174">규칙을 오른쪽 클릭한 다음 **재정의** > **다음 클래스의 특정 개체: 관리 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-174">Right-click the rule and then click **Overrides** > **For a specific object of class: Management Server**.</span></span>
4.  <span data-ttu-id="a605c-175">사용 가능한 관리 서버 목록에서 규칙을 실행할 관리 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-175">In the available management servers list, select the management server where the rule should run.</span></span>
5.  <span data-ttu-id="a605c-176">**사용** 매개 변수 값에 대한 재정의 값을 **참**으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-176">Ensure that you change override value to **True** for the **Enabled** parameter value.</span></span>  
    <span data-ttu-id="a605c-177">![재정의 매개 변수](./media/log-analytics-scom-assessment/rule.png)</span><span class="sxs-lookup"><span data-stu-id="a605c-177">![override parameter](./media/log-analytics-scom-assessment/rule.png)</span></span>

<span data-ttu-id="a605c-178">이 창에 있는 동안 다음 정차를 사용하여 실행 빈도를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-178">While still in this window, configure the frequency of the run using the next procedure.</span></span>

#### <a name="configure-the-run-frequency"></a><span data-ttu-id="a605c-179">실행 빈도 구성</span><span class="sxs-lookup"><span data-stu-id="a605c-179">Configure the run frequency</span></span>

<span data-ttu-id="a605c-180">평가를 기본 간격인 10,080분(또는 7일)마다 실행하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-180">The assessment is configured to run every 10,080 minutes (or seven days), the default interval.</span></span> <span data-ttu-id="a605c-181">값을 최소값인 1440분(또는 1일)으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-181">You can override the value to a minimum value of 1440 minutes (or one day).</span></span> <span data-ttu-id="a605c-182">이 값은 연속적인 평가 실행 사이에 필요한 최소 시간 간격을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-182">The value represents the minimum time gap required between successive assessment runs.</span></span> <span data-ttu-id="a605c-183">간격을 재정의하려면 아래 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-183">To override the interval, use the steps below.</span></span>

1. <span data-ttu-id="a605c-184">Operations Manager 콘솔의 **제작** 작업 영역에서 **규칙** 창의 *Microsoft System Center Advisor SCOM 평가 실행 평가 규칙*이라는 규칙을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-184">In the **Authoring** workspace of the Operations Manager console, search for the rule *Microsoft System Center Advisor SCOM Assessment Run Assessment Rule* in the **Rules** pane.</span></span>
2. <span data-ttu-id="a605c-185">검색 결과에서 *유형: 관리 서버*라는 텍스트를 포함하는 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-185">In the search results, select the one that includes the text *Type: Management Server*.</span></span>
3. <span data-ttu-id="a605c-186">규칙을 오른쪽 클릭한 다음 **Override the Rule**(규칙 재정의) > **다음 클래스의 모든 개체: 관리 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-186">Right-click the rule and then click **Override the Rule** > **For all objects of class: Management Server**.</span></span>
4. <span data-ttu-id="a605c-187">**간격** 매개 변수 값을 원하는 간격 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-187">Change the **Interval** parameter value to your desired interval value.</span></span> <span data-ttu-id="a605c-188">아래 예의 경우 값이 1440분(1일)으로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-188">In the example below, the value is set to 1440 minutes (one day).</span></span>  
    <span data-ttu-id="a605c-189">![간격 매개 변수](./media/log-analytics-scom-assessment/interval.png)</span><span class="sxs-lookup"><span data-stu-id="a605c-189">![interval parameter](./media/log-analytics-scom-assessment/interval.png)</span></span>  
    <span data-ttu-id="a605c-190">값이 1440분 미만으로 설정되면 규칙이 하루 간격으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-190">If the value is set to less than 1440 minutes, then the rule runs at a one day interval.</span></span> <span data-ttu-id="a605c-191">이 예의 경우 규칙이 간격 값을 무시하고 하루 빈도로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-191">In this example, the rule ignores the interval value and runs at a frequency of one day.</span></span>


## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="a605c-192">권장 사항 우선 순위 이해</span><span class="sxs-lookup"><span data-stu-id="a605c-192">Understanding how recommendations are prioritized</span></span>

<span data-ttu-id="a605c-193">작성된 모든 권장 구성은 권장 사항의 상대적 중요도를 식별하는 가중치 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-193">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="a605c-194">10개의 가장 중요한 권장 사항만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-194">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="a605c-195">가중치 계산 방법</span><span class="sxs-lookup"><span data-stu-id="a605c-195">How weights are calculated</span></span>

<span data-ttu-id="a605c-196">가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-196">Weightings are aggregate values based on three key factors:</span></span>

- <span data-ttu-id="a605c-197">식별된 문제로 인해 문제가 발생될 수 있는 *확률* 입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-197">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="a605c-198">확률이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-198">A higher probability equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="a605c-199">문제가 발생된 경우 조직에 대한 문제의 *영향* 입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-199">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="a605c-200">영향이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-200">A higher impact equates to a larger overall score for the recommendation.</span></span>
- <span data-ttu-id="a605c-201">권장 구성을 구현하는 데 필요한 *노력* 입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-201">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="a605c-202">노력이 높을수록 권장 사항에 대한 전체 점수가 작아집니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-202">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="a605c-203">각 권장 사항에 대한 가중치는 각 주요 영역에 사용할 수 있는 총 점수에 대한 백분율로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-203">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="a605c-204">예를 들어 가용성 및 비즈니스 연속성 주요 영역의 권장 사항 점수가 5%이면 해당 권장 사항을 구현하면 전반적인 가용성 및 비즈니스 연속성 점수가 5% 상승합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-204">For example, if a recommendation in the Availability and Business Continuity focus area has a score of 5%, implementing that recommendation increases your overall Availability and Business Continuity score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="a605c-205">주요 영역</span><span class="sxs-lookup"><span data-stu-id="a605c-205">Focus areas</span></span>

<span data-ttu-id="a605c-206">**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-206">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="a605c-207">**성능 및 확장성** - 이 주요 영역은 조직의 IT 인프라를 확장하고, IT 환경이 현재 성능 요구 사항을 충족하며, 변화하는 인프라 요구 사항에 대응할 수 있도록 하는 데 도움이 되는 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-207">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="a605c-208">**업그레이드, 마이그레이션 및 배포** - 기존 인프라에서 SQL Server를 업그레이드, 마이그레이션 및 배포하는 데 도움이 되는 권장 사항을 보여 주는 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-208">**Upgrade, Migration, and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="a605c-209">**운영 및 모니터링** - IT 운영을 간소화하며, 예방 유지 관리를 구현하고, 성능을 최대화하는 데 도움이 되는 권장 사항을 보여 주는 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-209">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="a605c-210">모든 주요 영역에서 100%의 점수를 목표로 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="a605c-210">Should you aim to score 100% in every focus area?</span></span>

<span data-ttu-id="a605c-211">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-211">Not necessarily.</span></span> <span data-ttu-id="a605c-212">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-212">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="a605c-213">그러나 두 서버 인프라는 동일하지 않으며 특정 권장 사항은 거의 사용자와 관련 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-213">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="a605c-214">예를 들어, 가상 컴퓨터가 인터넷에 노출되지 않는 경우 일부 보안 권장 사항의 관련성은 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-214">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="a605c-215">일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-215">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="a605c-216">성숙한 비즈니스에 중요한 문제는 시작에 덜 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-216">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="a605c-217">우선하는 주요 영역을 식별하고 시간이 지남에 따라 다음 점수가 어떻게 변경되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-217">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="a605c-218">모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-218">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="a605c-219">IT 서비스의 특성 및 조직의 비즈니스 요구를 고려해 볼 때, 이 가이드를 사용하여 권장 사항 구현이 사용자에 적절한지 여부를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-219">Use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="a605c-220">평가 주요 영역 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="a605c-220">Use assessment focus area recommendations</span></span>

<span data-ttu-id="a605c-221">OMS에서 평가 솔루션을 사용하려면 먼저 솔루션이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-221">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="a605c-222">솔루션 설치에 대한 자세한 내용은 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a605c-222">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="a605c-223">설치 후 OMS의 개요 페이지에서 System Center Operations Manager 평가 타일을 사용하여 권장 사항의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-223">After it is installed, you can view the summary of recommendations by using the System Center Operations Manager Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="a605c-224">인프라에 대한 요약된 규정 준수 평가를 본 다음 세부 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-224">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="a605c-225">주요 영역에 대한 권장 사항을 보고 수정 작업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="a605c-225">To view recommendations for a focus area and take corrective action</span></span>

1. <span data-ttu-id="a605c-226">**개요** 페이지에서 **System Center Operations Manager 평가** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-226">On the **Overview** page, click the **System Center Operations Manager Assessment** tile.</span></span>
2. <span data-ttu-id="a605c-227">**System Center Operations Manager 평가** 페이지에서 주요 영역 블레이드 중 하나의 요약 정보를 검토한 다음 주요 영역 하나를 클릭하여 해당 주요 영역에 대한 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-227">On the **System Center Operations Manager Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="a605c-228">주요 영역 페이지에서 사용자 환경에 대해 우선순위가 지정된 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-228">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="a605c-229">권장하는 이유에 대한 세부 정보를 보려면 **영향을 받는 개체** 아래에서 해당 권장 사항을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-229">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="a605c-230">![주요 영역](./media/log-analytics-scom-assessment/focus-area.png)</span><span class="sxs-lookup"><span data-stu-id="a605c-230">![focus area](./media/log-analytics-scom-assessment/focus-area.png)</span></span>
4. <span data-ttu-id="a605c-231">**권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-231">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="a605c-232">항목의 주소가 지정되면, 이후 평가는 수행된 권장 조치 및 늘어난 규정 준수 점수를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-232">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="a605c-233">수정된 항목은 **전달된 개체**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-233">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="a605c-234">권장 사항 무시</span><span class="sxs-lookup"><span data-stu-id="a605c-234">Ignore recommendations</span></span>

<span data-ttu-id="a605c-235">무시하려는 권장 사항이 있는 경우 OMS에서 평가 결과에 권장 사항이 표시되는 것을 방지하는 데 사용할 텍스트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-235">If you have recommendations that you want to ignore, you can create a text file that OMS uses to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-want-to-ignore"></a><span data-ttu-id="a605c-236">무시할 권장 사항을 식별하려면</span><span class="sxs-lookup"><span data-stu-id="a605c-236">To identify recommendations that you want to ignore</span></span>

1. <span data-ttu-id="a605c-237">작업 영역에 로그인하고 로그 검색을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-237">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="a605c-238">다음 쿼리를 사용하여 사용자 환경의 컴퓨터에 대해 실패한 권장 사항을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-238">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    <span data-ttu-id="a605c-239">로그 검색 쿼리를 보여 주는 스크린샷은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-239">Here's a screen shot showing the Log Search query:</span></span>  
    ![로그 검색](./media/log-analytics-scom-assessment/scom-log-search.png)

2. <span data-ttu-id="a605c-241">무시할 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-241">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="a605c-242">RecommendationId 값은 다음 절차에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-242">You'll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="a605c-243">IgnoreRecommendations.txt 텍스트 파일을 만들고 사용하려면</span><span class="sxs-lookup"><span data-stu-id="a605c-243">To create and use an IgnoreRecommendations.txt text file</span></span>

1. <span data-ttu-id="a605c-244">IgnoreRecommendations.txt라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-244">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="a605c-245">OMS에서 무시할 각 권장 사항에 대한 RecommendationId를 별도의 줄에 붙여넣거나 입력한 다음 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-245">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="a605c-246">OMS에서 권장 사항을 무시할 각 컴퓨터의 다음 폴더에 파일을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-246">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
4. <span data-ttu-id="a605c-247">Operations Manager 관리 서버 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span><span class="sxs-lookup"><span data-stu-id="a605c-247">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="a605c-248">권장 사항이 무시되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="a605c-248">To verify that recommendations are ignored</span></span>

1. <span data-ttu-id="a605c-249">예약된 다음 평가가 실행된 후(기본적으로 7일마다) 지정된 권장 사항이 평가 대시보드에 무시됨으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-249">After the next scheduled assessment runs, by default every seven days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="a605c-250">다음 로그 검색 쿼리를 사용하여 무시된 모든 권장 사항을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-250">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. <span data-ttu-id="a605c-251">무시된 권장 사항을 나중에 보려면 IgnoreRecommendations.txt 파일을 제거합니다. 또는 파일에서 RecommendationID를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-251">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="system-center-operations-manager-assessment-solution-faq"></a><span data-ttu-id="a605c-252">System Center Operations Manager 평가 솔루션 FAQ</span><span class="sxs-lookup"><span data-stu-id="a605c-252">System Center Operations Manager Assessment solution FAQ</span></span>

<span data-ttu-id="a605c-253">*평가 솔루션을 내 OMS 작업 공간에 추가합니다. 하지만 권장 사항이 표시되지 않습니다. 이유*</span><span class="sxs-lookup"><span data-stu-id="a605c-253">*I added the assessment solution to my OMS workspace. But I don’t see the recommendations. Why not?*</span></span> <span data-ttu-id="a605c-254">솔루션을 추가한 후, 다음 단계 보기를 사용하여 OMS 대시보드의 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-254">After adding the solution, use the following steps view the recommendations on the OMS dashboard.</span></span>  

- [<span data-ttu-id="a605c-255">System Center Operations Manager 평가를 위한 계정으로 실행 설정</span><span class="sxs-lookup"><span data-stu-id="a605c-255">Set the Run As account for System Center Operations Manager Assessment</span></span>](#operations-manager-run-as-accounts-for-oms)  
- [<span data-ttu-id="a605c-256">System Center Operations Manager 평가 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="a605c-256">Configure the System Center Operations Manager Assessment rule</span></span>](#configure-the-assessment-rule)


<span data-ttu-id="a605c-257">*평가를 실행 빈도를 구성하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-257">*Is there a way to configure how often the assessment runs?*</span></span> <span data-ttu-id="a605c-258">예.</span><span class="sxs-lookup"><span data-stu-id="a605c-258">Yes.</span></span> <span data-ttu-id="a605c-259">[실행 빈도 구성](#configure-the-run-frequency)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a605c-259">See [Configure the run frequency](#configure-the-run-frequency).</span></span>

<span data-ttu-id="a605c-260">*System Center Operations Manager 평가 솔루션을 추가한 후 다른 서버가 발견되면, 이 서버를 평가하나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-260">*If another server is discovered after I’ve added the System Center Operations Manager Assessment solution, will it be assessed?*</span></span> <span data-ttu-id="a605c-261">예, 검색된 이후 기본적으로 7일마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-261">Yes, after discovery, it is assessed from then on--by default, every seven days.</span></span>

<span data-ttu-id="a605c-262">*데이터 수집을 수행하는 프로세스의 이름은 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-262">*What is the name of the process that does the data collection?*</span></span> <span data-ttu-id="a605c-263">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="a605c-263">AdvisorAssessment.exe</span></span>

<span data-ttu-id="a605c-264">*AdvisorAssessment.exe 프로세스가 왜 실행되나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-264">*Where does the AdvisorAssessment.exe process run?*</span></span> <span data-ttu-id="a605c-265">AdvisorAssessment.exe는 평가 규칙을 사용하도록 설정된 관리 서버의 HealthService에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-265">AdvisorAssessment.exe runs under the HealthService of the management server where the assessment rule is enabled.</span></span> <span data-ttu-id="a605c-266">이 프로세스를 사용하는 경우 전체 환경에 대한 검색은 원격 데이터 수집을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-266">Using that process, discovery of your entire environment is achieved through remote data collection.</span></span>

<span data-ttu-id="a605c-267">*데이터 수집에 시간이 얼마나 걸리나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-267">*How long does it take for data collection?*</span></span> <span data-ttu-id="a605c-268">서버의 데이터 수집은 약 1시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-268">Data collection on the server takes about one hour.</span></span> <span data-ttu-id="a605c-269">Operations Manager 인스턴스 또는 데이터베이스가 많은 환경에서는 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-269">It may take longer in environments that have many Operations Manager instances or databases.</span></span>

<span data-ttu-id="a605c-270">*평가 간격을 1440분 미만으로 설정하면 어떻게 되나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-270">*What if I set the interval of the assessment to less than 1440 minutes?*</span></span> <span data-ttu-id="a605c-271">평가는 최다 하루에 한번 실행하도록 미리 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-271">The assessment is pre-configured to run at a maximum of once per day.</span></span> <span data-ttu-id="a605c-272">간격 값을 1440분 미만의 값으로 재정의하면 평가는 1440분을 간격 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-272">If you override the interval value to a value less than 1440 minutes, then the assessment uses 1440 minutes as the interval value.</span></span>

<span data-ttu-id="a605c-273">*필수 구성 요소 오류가 있는지 어떻게 알 수 있나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-273">*How to know if there are pre-requisite failures?*</span></span> <span data-ttu-id="a605c-274">평가가 실행되었는데 결과가 보이지 않는다면 평가의 일부 필수 구성 요소에 오류가 있을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-274">If the assessment ran and you don't see results, then it is likely that some of the pre-requisites for the assessment failed.</span></span> <span data-ttu-id="a605c-275">로그 검색에서 `Type=Operation Solution=SCOMAssessment` 및 `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` 쿼리를 실행하여 실패한 필수 구성 요소를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-275">You can execute queries: `Type=Operation Solution=SCOMAssessment` and `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` in Log Search to see the failed pre-requisites.</span></span>

<span data-ttu-id="a605c-276">*필수 구성 요소 오류에 `Failed to connect to the SQL Instance (….).` 메시지가 있습니다. 문제가 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-276">*There is a `Failed to connect to the SQL Instance (….).` message in pre-requisite failures. What is the issue?*</span></span> <span data-ttu-id="a605c-277">데이터를 수집하는 프로세스 AdvisorAssessment.exe는 관리 서버의 HealthService에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-277">AdvisorAssessment.exe, the process that collects data, runs under the HealthService of the management server.</span></span> <span data-ttu-id="a605c-278">평가의 일환으로 이 프로세스는 Operations Manager 데이터베이스가 있는 SQL Server에 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-278">As part of the assessment, the process attempts to connect to the SQL Server where the Operations Manager database is present.</span></span> <span data-ttu-id="a605c-279">이 오류는 방화벽 규칙이 SQL Server 인스턴스에 대한 연결을 차단하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-279">This error can occur when firewall rules block the connection to the SQL Server instance.</span></span>

<span data-ttu-id="a605c-280">*어떤 유형의 데이터를 수집하나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-280">*What type of data is collected?*</span></span> <span data-ttu-id="a605c-281">다음 유형의 데이터를 수집합니다. Windows PowerShell, SQL 쿼리, 파일 정보 수집기를 통해 - WMI 데이터 - Registry 데이터 - EventLog 데이터 - Operations Manager 데이터.</span><span class="sxs-lookup"><span data-stu-id="a605c-281">The following types of data are collected: - WMI data - Registry data - EventLog data - Operations Manager data through Windows PowerShell, SQL Queries and File information collector.</span></span>

<span data-ttu-id="a605c-282">*왜 실행 계정을 구성해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-282">*Why do I have to configure a Run As Account?*</span></span> <span data-ttu-id="a605c-283">Operations Manager 서버의 경우 다양한 SQL 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-283">For an Operations Manager server, various SQL queries are run.</span></span> <span data-ttu-id="a605c-284">이러한 항목이 실행되려면 필요한 권한이 있는 실행 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-284">In order for them to run, you must use a Run As Account with necessary permissions.</span></span> <span data-ttu-id="a605c-285">또한 WMI를 쿼리하려면 로컬 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-285">In addition, local administrator credentials are required to query WMI.</span></span>

<span data-ttu-id="a605c-286">*왜 상위 10개의 권장 사항만을 표시하나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-286">*Why display only the top 10 recommendations?*</span></span> <span data-ttu-id="a605c-287">엄청나게 포괄적인 작업을 나열하는 대신, 먼저 우선 순위가 지정된 권장 사항 해결에 주의를 기울이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-287">Instead of giving you an exhaustive, overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="a605c-288">권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-288">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="a605c-289">자세한 목록을 참조하는 것을 선호하는 경우 로그 검색을 사용하여 모든 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-289">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="a605c-290">*권장 사항을 무시하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="a605c-290">*Is there a way to ignore a recommendation?*</span></span> <span data-ttu-id="a605c-291">예, [권장 사항 무시](#Ignore-recommendations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a605c-291">Yes, see the [Ignore recommendations](#Ignore-recommendations).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a605c-292">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a605c-292">Next steps</span></span>

- <span data-ttu-id="a605c-293">[로그를 검색](log-analytics-log-searches.md)하여 자세한 System Center Operations Manager 평가 데이터 및 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a605c-293">[Search logs](log-analytics-log-searches.md) to view detailed System Center Operations Manager Assessment data and recommendations.</span></span>
