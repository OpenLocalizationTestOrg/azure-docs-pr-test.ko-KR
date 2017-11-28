---
title: "Azure Log Analytics를 사용하여 SQL Server 환경 최적화 | Microsoft Docs"
description: "Azure Log Analytics에서 SQL 평가 솔루션을 사용하여 일정한 간격으로 SQL Server 환경의 위험 및 상태를 평가할 수 있습니다."
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
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="39c63-103">Log Analytics에서 SQL 평가 솔루션을 사용하여 사용자 SQL Server 환경 최적화</span><span class="sxs-lookup"><span data-stu-id="39c63-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![SQL 평가 기호](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="39c63-105">SQL 평가 솔루션을 사용하여 일정한 간격으로 서버 환경의 위험 및 상태를 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="39c63-106">이 문서에서는 잠재적인 문제에 대해 올바른 조치를 취할 수 있도록 솔루션 설치를 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="39c63-107">이 솔루션은 배포된 서버 인프라 관련 우선순위가 지정된 권장 사항 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="39c63-108">권장 사항은 신속하게 위험을 이해하고 수정 조치를 취할 수 있도록 여섯 가지 주요 영역으로 분류되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="39c63-109">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="39c63-110">각 권장 사항은 문제가 중요할 수 있는 이유 및 제안된 변경 내용을 구현하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="39c63-111">조직에 가장 중요한 주요 영역을 선택하여 위험이 없는 정상 환경을 실행 중인 프로그램의 진행을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="39c63-112">솔루션을 추가하고 평가가 완료되면 주요 영역의 요약 정보가 사용자 환경의 인프라에 대한 **SQL 평가** 대시보드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="39c63-113">다음 섹션에서는 **SQL 평가** 대시보드의 정보를 사용하는 방법을 설명합니다. 여기서는 이 대시보드의 정보를 보고 SQL 서버 인프라에 대한 권장 조치를 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![SQL 평가 타일의 이미지](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![SQL 평가 대시보드의 이미지](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="39c63-116">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="39c63-116">Installing and configuring the solution</span></span>
<span data-ttu-id="39c63-117">SQL 평가는 현재 지원되는 모든 버전의 SQL Server Standard, Developer 및 Enterprise Edition에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="39c63-118">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="39c63-119">SQL Server가 설치된 서버에 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="39c63-120">SQL 평가 솔루션을 사용하려면 OMS 에이전트가 있는 각 컴퓨터에 지원되는 버전의 .NET Framework 4를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="39c63-121">솔루션을 설치하기 위해 Azure Portal을 사용하는 경우 사용자는 Azure 구독의 관리자 또는 참가자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="39c63-122">또한 사용자는 OMS 작업 영역 참가자의 구성원이거나 OMS 포털에서 관리자 역할이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="39c63-123">SQL 평가에서 Operations Manager 에이전트를 사용하는 경우 Operations Manager 실행 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="39c63-124">자세한 내용은 아래의 [OMS용 Operations Manager 실행 계정](#operations-manager-run-as-accounts-for-oms) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39c63-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="39c63-125">MMA 에이전트는 Operations Manager 실행 계정을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="39c63-126">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에 설명된 프로세스를 사용하여 OMS 작업 영역에 SQL 평가 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="39c63-127">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="39c63-128">솔루션을 추가하면 에이전트가 있는 서버에 AdvisorAssessment.exe 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="39c63-129">구성 데이터가 판독되고 처리를 위해 클라우드의 OMS 서비스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="39c63-130">논리는 수신된 데이터에 적용되며 클라우드 서비스는 데이터를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="39c63-131">SQL 평가 데이터 수집 정보</span><span class="sxs-lookup"><span data-stu-id="39c63-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="39c63-132">SQL 평가는 사용자가 설정한 에이전트를 사용하여 WMI 데이터, 레지스트리 데이터, 성능 데이터 및 SQL Server 동적 관리 보기 결과를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="39c63-133">다음 표에는 에이전트에 대한 데이터 수집 방법, Operations Manager(SCOM)가 필요한지 여부 및 에이전트에서 데이터가 수집되는 빈도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="39c63-134">플랫폼</span><span class="sxs-lookup"><span data-stu-id="39c63-134">platform</span></span> | <span data-ttu-id="39c63-135">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="39c63-135">Direct Agent</span></span> | <span data-ttu-id="39c63-136">SCOM 에이전트</span><span class="sxs-lookup"><span data-stu-id="39c63-136">SCOM agent</span></span> | <span data-ttu-id="39c63-137">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="39c63-137">Azure Storage</span></span> | <span data-ttu-id="39c63-138">SCOM 필요?</span><span class="sxs-lookup"><span data-stu-id="39c63-138">SCOM required?</span></span> | <span data-ttu-id="39c63-139">관리 그룹을 통해 전송되는 SCOM 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="39c63-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="39c63-140">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="39c63-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="39c63-141">Windows</span><span class="sxs-lookup"><span data-stu-id="39c63-141">Windows</span></span> | <span data-ttu-id="39c63-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="39c63-142">&#8226;</span></span> | <span data-ttu-id="39c63-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="39c63-143">&#8226;</span></span> |  |  | <span data-ttu-id="39c63-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="39c63-144">&#8226;</span></span> |<span data-ttu-id="39c63-145">7 일</span><span class="sxs-lookup"><span data-stu-id="39c63-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="39c63-146">OMS용 Operations Manager 실행 계정</span><span class="sxs-lookup"><span data-stu-id="39c63-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="39c63-147">OMS의 Log Analytics에서는 Operations Manager 에이전트와 관리 그룹을 사용하여 데이터를 수집하여 OMS 서비스로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="39c63-148">OMS는 부가 가치 서비스를 제공하는 작업을 위해 관리 팩을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="39c63-149">도메인 계정과 같은 다른 보안 컨텍스트에서 관리 팩을 실행하려면 각 작업에 작업 관련 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="39c63-150">Operations Manager 실행 계정을 구성하여 자격 증명 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="39c63-151">다음 정보를 사용하여 SQL 평가를 위한 Operations Manager 실행 계정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="39c63-152">SQL 평가에 대한 실행 계정 설정</span><span class="sxs-lookup"><span data-stu-id="39c63-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="39c63-153">SQL Server 관리 팩을 이미 사용 중인 경우 해당 실행 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="39c63-154">운영 콘솔에서 SQL 실행 계정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="39c63-155">SCOM 에이전트가 아닌 OMS 직접 에이전트를 사용하는 경우 관리 팩은 항상 로컬 시스템 계정의 보안 컨텍스트에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="39c63-156">아래의 1-5단계를 건너뛰고 T-SQL 또는 Powershell 샘플을 실행하고 NT AUTHORITY\SYSTEM을 사용자 이름으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="39c63-157">Operations Manager에서 운영 콘솔을 열고 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="39c63-158">**실행 구성**에서 **프로필**을 클릭하고 **OMS SQL 평가 실행 프로필**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="39c63-159">**실행 계정** 페이지에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="39c63-160">SQL Server에 필요한 자격 증명을 포함하는 Windows 실행 계정을 선택하거나 **새로 만들기** 를 클릭하여 계정을 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="39c63-161">실행 계정 유형은 Windows이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="39c63-162">실행 계정은 SQL Server 인스턴스를 호스팅하는 모든 Windows 서버에서 로컬 관리자 그룹의 일부이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="39c63-163">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-163">Click **Save**.</span></span>
6. <span data-ttu-id="39c63-164">SQL 평가에 실행 계정으로 필요한 최소 사용 권한을 부여하도록 각 SQL Server 인스턴스에서 다음 T-SQL 샘플을 수정한 다음 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="39c63-165">그러나 실행 계정이 SQL Server 인스턴스에서 이미 sysadmin 서버 역할의 일부인 경우, 이 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="39c63-166">Windows PowerShell을 사용하여 SQL 실행 계정을 구성하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="39c63-167">PowerShell 창을 열고 사용자 정보로 업데이트 한 후 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="39c63-168">권장 사항 우선 순위 이해</span><span class="sxs-lookup"><span data-stu-id="39c63-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="39c63-169">작성된 모든 권장 구성은 권장 사항의 상대적 중요도를 식별하는 가중치 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="39c63-170">10개의 가장 중요한 권장 사항만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="39c63-171">가중치 계산 방법</span><span class="sxs-lookup"><span data-stu-id="39c63-171">How weights are calculated</span></span>
<span data-ttu-id="39c63-172">가중치는 3개의 주요 요인을 기반으로 하는 집계 값입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="39c63-173">식별된 문제로 인해 문제가 발생될 수 있는 *확률* 입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="39c63-174">확률이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="39c63-175">문제가 발생된 경우 조직에 대한 문제의 *영향* 입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="39c63-176">영향이 높을수록 권장 사항에 대한 전체 점수가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="39c63-177">권장 구성을 구현하는 데 필요한 *노력* 입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="39c63-178">노력이 높을수록 권장 사항에 대한 전체 점수가 작아집니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="39c63-179">각 권장 사항에 대한 가중치는 각 주요 영역에 사용할 수 있는 총 점수에 대한 백분율로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="39c63-180">예를 들어, 보안 및 규정 준수 주요 영역의 권장 사항의 점수가 5%라면, 해당 권장 사항 구현에는 전체 보안 및 규정 준수 점수에서 5%가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="39c63-181">주요 영역</span><span class="sxs-lookup"><span data-stu-id="39c63-181">Focus areas</span></span>
<span data-ttu-id="39c63-182">**보안 및 규정 준수** - 이 주요 영역은 잠재적 보안 위협 및 위반, 회사 정책, 기술, 법률 및 규정 준수 요구 사항 등에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="39c63-183">**가용성 및 비즈니스 연속성** - 이 주요 영역은 서비스 가용성, 인프라 복원성 및 비즈니스 보호에 대한 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="39c63-184">**성능 및 확장성** - 이 주요 영역은 조직의 IT 인프라를 확장하고, IT 환경이 현재 성능 요구 사항을 충족하며, 변화하는 인프라 요구 사항에 대응할 수 있도록 하는 데 도움이 되는 권장 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="39c63-185">**업그레이드, 마이그레이션 및 배포** - 기존 인프라에서 SQL Server를 업그레이드, 마이그레이션 및 배포하는 데 도움이 되는 권장 사항을 보여 주는 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="39c63-186">**운영 및 모니터링** - IT 운영을 간소화하며, 예방 유지 관리를 구현하고, 성능을 최대화하는 데 도움이 되는 권장 사항을 보여 주는 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="39c63-187">**변경 및 구성 관리** - 일상 작업을 보호하고, 인프라에 부정적인 영향을 주는 변경 사항이 있는지 확인하며, 변경 제어 절차를 설정하고, 시스템 구성을 추적 및 감사하는 데 도움이 되는 권장 사항을 보여 주는 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="39c63-188">모든 주요 영역에서 100%의 점수를 목표로 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="39c63-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="39c63-189">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-189">Not necessarily.</span></span> <span data-ttu-id="39c63-190">권장 사항은 수천 번의 고객 방문에서 Microsoft 엔지니어가 얻은 지식과 경험을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="39c63-191">그러나 두 서버 인프라는 동일하지 않으며 특정 권장 사항은 거의 사용자와 관련 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="39c63-192">예를 들어, 가상 컴퓨터가 인터넷에 노출되지 않는 경우 일부 보안 권장 사항의 관련성은 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="39c63-193">일부 가용성 권장 사항은 우선순위가 낮은 임시 데이터 수집 및 보고를 제공하는 서비스와는 관련성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="39c63-194">성숙한 비즈니스에 중요한 문제는 시작에 덜 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="39c63-195">우선하는 주요 영역을 식별하고 시간이 지남에 따라 다음 점수가 어떻게 변경되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="39c63-196">모든 권장 사항에는 중요한 이유에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="39c63-197">IT 서비스의 특성 및 조직의 비즈니스 요구를 고려해 볼 때, 이 가이드를 사용하여 권장 사항 구현이 사용자에 적절한지 여부를 평가해야 합니다</span><span class="sxs-lookup"><span data-stu-id="39c63-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="39c63-198">평가 주요 영역 권장 사항 사용</span><span class="sxs-lookup"><span data-stu-id="39c63-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="39c63-199">OMS에서 평가 솔루션을 사용하려면 먼저 솔루션이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="39c63-200">솔루션 설치에 대한 자세한 내용은 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39c63-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="39c63-201">설치 후 OMS의 개요 페이지에서 SQL 평가 타일을 사용하여 권장 사항의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="39c63-202">인프라에 대한 요약된 규정 준수 평가를 본 다음 세부 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="39c63-203">주요 영역에 대한 권장 사항을 보고 수정 작업을 수행하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="39c63-204">**개요** 페이지에서 **SQL 평가** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="39c63-205">**SQL 평가** 페이지에서 주요 영역 블레이드 중 하나의 요약 정보를 검토한 다음 주요 영역 하나를 클릭하여 해당 주요 영역에 대한 권장 사항을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="39c63-206">주요 영역 페이지에서 사용자 환경에 대해 우선순위가 지정된 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="39c63-207">권장하는 이유에 대한 세부 정보를 보려면 **영향을 받는 개체** 아래에서 해당 권장 사항을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="39c63-208">![SQL 평가 권장 사항 이미지](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="39c63-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="39c63-209">**권장 조치**에 제안된 올바른 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="39c63-210">항목의 주소가 지정되면, 이후 평가는 수행된 권장 조치 및 늘어난 규정 준수 점수를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="39c63-211">수정된 항목은 **전달된 개체**로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="39c63-212">권장 사항 무시</span><span class="sxs-lookup"><span data-stu-id="39c63-212">Ignore recommendations</span></span>
<span data-ttu-id="39c63-213">무시하려는 권장 사항이 있는 경우 OMS에서 평가 결과에 권장 사항이 표시되는 것을 방지하는 데 사용할 텍스트 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="39c63-214">무시할 권장 사항을 식별하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="39c63-215">작업 영역에 로그인하고 로그 검색을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="39c63-216">다음 쿼리를 사용하여 사용자 환경의 컴퓨터에 대해 실패한 권장 사항을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="39c63-217">로그 검색 쿼리를 보여 주는 스크린샷은 다음과 같습니다.![실패한 권장 사항](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="39c63-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="39c63-218">무시할 권장 사항을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="39c63-219">RecommendationId 값은 다음 절차에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="39c63-220">IgnoreRecommendations.txt 텍스트 파일을 만들고 사용하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="39c63-221">IgnoreRecommendations.txt라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="39c63-222">OMS에서 무시할 각 권장 사항에 대한 RecommendationId를 별도의 줄에 붙여넣거나 입력한 다음 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="39c63-223">OMS에서 권장 사항을 무시할 각 컴퓨터의 다음 폴더에 파일을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="39c63-224">Microsoft Monitoring Agent(직접 또는 Operations Manager를 통해 연결됨)가 있는 컴퓨터 - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="39c63-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="39c63-225">Operations Manager 관리 서버 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="39c63-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="39c63-226">권장 사항이 무시되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="39c63-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="39c63-227">예약된 다음 평가가 실행된 후(기본적으로 7일마다) 지정된 권장 사항이 평가 대시보드에 무시됨으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="39c63-228">다음 로그 검색 쿼리를 사용하여 무시된 모든 권장 사항을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="39c63-229">무시된 권장 사항을 나중에 보려면 IgnoreRecommendations.txt 파일을 제거합니다. 또는 파일에서 RecommendationID를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="39c63-230">SQL 평가 솔루션 FAQ</span><span class="sxs-lookup"><span data-stu-id="39c63-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="39c63-231">*얼마나 자주 평가를 실행하나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="39c63-232">평가는 7일마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="39c63-233">*평가를 실행 빈도를 구성하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="39c63-234">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-234">Not at this time.</span></span>

<span data-ttu-id="39c63-235">*SQL 평가 솔루션을 추가한 후 다른 서버가 발견되면 이 서버를 평가하나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="39c63-236">예, 발견되면 그 시간부터 7일마다 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="39c63-237">*서버를 서비스 해제하는 경우 언제 평가에서 제거되나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="39c63-238">3주 동안 서버가 데이터를 전송하지 않은 경우 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="39c63-239">*데이터 수집을 수행하는 프로세스의 이름은 무엇인가요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="39c63-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="39c63-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="39c63-241">*데이터를 수집하려면 시간이 얼마나 걸리나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="39c63-242">서버에서의 실제 데이터 수집은 약 1시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="39c63-243">SQL 인스턴스 또는 데이터베이스가 많은 서버에서는 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="39c63-244">*어떤 유형의 데이터를 수집하나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="39c63-245">다음 유형의 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="39c63-246">WMI</span><span class="sxs-lookup"><span data-stu-id="39c63-246">WMI</span></span>
  * <span data-ttu-id="39c63-247">레지스트리</span><span class="sxs-lookup"><span data-stu-id="39c63-247">Registry</span></span>
  * <span data-ttu-id="39c63-248">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="39c63-248">Performance counters</span></span>
  * <span data-ttu-id="39c63-249">SQL 동적 관리 뷰(DMV)</span><span class="sxs-lookup"><span data-stu-id="39c63-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="39c63-250">*데이터를 수집하는 경우 구성하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="39c63-251">지금은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-251">Not at this time.</span></span>

<span data-ttu-id="39c63-252">*왜 실행 계정을 구성해야 하나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="39c63-253">SQL Server의 경우, 적은 수의 SQL 쿼리가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="39c63-254">실행하려면, SQL에 대한 서버 상태 보기 권한이 있는 실행 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="39c63-255">또한 WMI를 쿼리하기 위해 로컬 관리자 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="39c63-256">*왜 상위 10개의 권장 사항만을 표시하나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="39c63-257">엄청난 소비적인 작업을 나열하는 대신, 먼저 우선순위가 지정된 권장 사항 해결에 주의를 기울이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="39c63-258">권장 사항을 해결한 후에 추가 권장 사항을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="39c63-259">자세한 목록을 참조하는 것을 선호하는 경우 OMS 로그 검색을 사용하여 모든 권장 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="39c63-260">*권장 사항을 무시하는 방법이 있나요?*</span><span class="sxs-lookup"><span data-stu-id="39c63-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="39c63-261">예, 위의 [권장 사항 무시](#ignore-recommendations) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39c63-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c63-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39c63-262">Next steps</span></span>
* <span data-ttu-id="39c63-263">[로그를 검색](log-analytics-log-searches.md) 하여 자세한 SQL 평가 데이터 및 권장 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39c63-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
