---
title: "aaaSecurity Center 플랫폼 마이그레이션 관련 FAQ | Microsoft Docs"
description: "이 FAQ hello Azure 보안 센터 플랫폼 마이그레이션에 대 한 질문에 답변 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a><span data-ttu-id="9c29c-103">Security Center 마이그레이션 FAQ</span><span class="sxs-lookup"><span data-stu-id="9c29c-103">Security Center platform migration FAQ</span></span>
<span data-ttu-id="9c29c-104">초기 6 월 2017 Azure 보안 센터 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 하 여 시작 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-104">In early June 2017, Azure Security Center began using hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="9c29c-105">toolearn 더 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-105">toolearn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="9c29c-106">이 FAQ hello 플랫폼 마이그레이션에 대 한 질문에 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-106">This FAQ answers questions about hello platform migration.</span></span>

## <a name="data-collection-agents-and-workspaces"></a><span data-ttu-id="9c29c-107">데이터 수집, 에이전트 및 작업 영역</span><span class="sxs-lookup"><span data-stu-id="9c29c-107">Data collection, agents, and workspaces</span></span>

### <a name="how-is-data-collected"></a><span data-ttu-id="9c29c-108">데이터를 어떻게 수집해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-108">How is data collected?</span></span>
<span data-ttu-id="9c29c-109">보안 센터 Vm의 hello toocollect 보안 데이터를 Microsoft Monitoring Agent를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-109">Security Center uses hello Microsoft Monitoring Agent toocollect security data from your VMs.</span></span> <span data-ttu-id="9c29c-110">hello 보안 데이터에는 사용 되는 tooidentify 취약점 보안 구성 및 사용 되는 toodetect 위협 요소인 보안 이벤트에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-110">hello security data includes information about security configurations, which are used tooidentify vulnerabilities, and security events, which are used toodetect threats.</span></span> <span data-ttu-id="9c29c-111">Hello 에이전트에 의해 수집 된 데이터는 기존 로그 분석 작업 영역 연결 toohello VM 또는 보안 센터에서 만든 새 작업 영역 중 하나에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-111">Data collected by hello agent is stored in either an existing Log Analytics workspace connected toohello VM or a new workspace created by Security Center.</span></span> <span data-ttu-id="9c29c-112">보안 센터 새 작업 영역을 만들 때의 hello hello geolocation VM 고려 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-112">When Security Center creates a new workspace, hello geolocation of hello VM is taken into account.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29c-113">hello Microsoft Monitoring Agent는 hello Operations Management Suite (OMS), 로그 분석 서비스 및 System Center Operations Manager (SCOM)에서 사용 되는 동일한 에이전트인 hello는입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-113">hello Microsoft Monitoring Agent is hello same agent used by hello Operations Management Suite (OMS), Log Analytics service and System Center Operations Manager (SCOM).</span></span>
>
>

<span data-ttu-id="9c29c-114">처음으로 또는 구독을 마이그레이션하는 경우 hello에 대 한 데이터 수집을 활성화 하는 경우 각 Vm에 Azure 확장으로 hello Microsoft Monitoring Agent가 이미 설치 되어 있는 경우 보안 센터 toosee를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-114">When data collection is enabled for hello first time or when your subscriptions are migrated, Security Center checks toosee if hello Microsoft Monitoring Agent is already installed as an Azure extension on each of your VMs.</span></span> <span data-ttu-id="9c29c-115">Hello Microsoft Monitoring Agent 설치 되지 않은 경우 다음 보안 센터를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-115">If hello Microsoft Monitoring Agent is not installed, then Security Center will:</span></span>

- <span data-ttu-id="9c29c-116">hello VM에 hello Microsoft Monitoring agent를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-116">install hello Microsoft Monitoring agent on hello VM</span></span>
   - <span data-ttu-id="9c29c-117">에이전트는 작업 영역 연결된 toothis 보안 센터에서 이미 만든 작업 영역 동일한 지리적 위치의 hello VM을 같이 hello hello에 있는 경우</span><span class="sxs-lookup"><span data-stu-id="9c29c-117">if a workspace created by Security Center already exists in hello same geolocation as hello VM, hello agent is connected toothis workspace</span></span>
   - <span data-ttu-id="9c29c-118">작업 영역이 없는 경우 보안 센터 새 리소스 그룹 및 해당 지리적 위치에서 작업 영역을 기본 만들고 hello 에이전트 toothat 작업 영역을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-118">if a workspace does not exist, Security Center creates a new resource group and default workspace in that geolocation, and connect hello agent toothat workspace.</span></span> <span data-ttu-id="9c29c-119">hello hello 작업 영역 및 리소스 그룹에 대 한 명명 규칙은:</span><span class="sxs-lookup"><span data-stu-id="9c29c-119">hello naming convention for hello workspace and resource group are:</span></span>

       <span data-ttu-id="9c29c-120">작업 영역: DefaultWorkspace-[subscription-ID]-[geo]</span><span class="sxs-lookup"><span data-stu-id="9c29c-120">Workspace: DefaultWorkspace-[subscription-ID]-[geo]</span></span>

       <span data-ttu-id="9c29c-121">리소스 그룹: DefaultResouceGroup-[geo]</span><span class="sxs-lookup"><span data-stu-id="9c29c-121">Resource Group: DefaultResouceGroup-[geo]</span></span>
- <span data-ttu-id="9c29c-122">hello 작업 영역에서 보안 센터 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-122">install a Security Center solution on hello workspace</span></span>

<span data-ttu-id="9c29c-123">hello 영역의 hello 위치 hello VM의 hello 위치를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-123">hello location of hello workspace is based on hello location of hello VM.</span></span> <span data-ttu-id="9c29c-124">toolearn 더 참조 [데이터 보안](security-center-data-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-124">toolearn more, see [Data Security](security-center-data-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c29c-125">이전 tooplatform 마이그레이션 보안 센터는 hello Azure 모니터링 에이전트를 사용 하 여 Vm에서 보안 데이터를 수집 하 고 저장소 계정에 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-125">Prior tooplatform migration, Security Center collected security data from your VMs using hello Azure Monitoring Agent, and data was stored in your storage account.</span></span> <span data-ttu-id="9c29c-126">Hello 플랫폼 마이그레이션 후 보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 및 작업 영역 toocollect 및 스토어 hello 같은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-126">After hello platform migration, Security Center uses hello Microsoft Monitoring Agent and workspace toocollect and store hello same data.</span></span> <span data-ttu-id="9c29c-127">hello 마이그레이션 후 hello 저장소 계정을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-127">hello storage account can be removed after hello migration.</span></span>
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a><span data-ttu-id="9c29c-128">로그 분석 또는 보안 센터에서 만든 hello 작업 영역에서 OMS에 대 한 요금이 청구 하나요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-128">Am I billed for Log Analytics or OMS on hello workspaces created by Security Center?</span></span>
<span data-ttu-id="9c29c-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="9c29c-129">No.</span></span> <span data-ttu-id="9c29c-130">Security Center에서 만든 작업 영역은 노드 요금 청구당 OMS에 구성되는 동안 OMS 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-130">Workspaces created by Security Center, while configured for OMS per node billing, do not incur OMS charges.</span></span> <span data-ttu-id="9c29c-131">보안 센터 청구는 항상 사용자 보안 센터 보안 정책 및 hello 솔루션 작업 영역에 설치 된 기준:</span><span class="sxs-lookup"><span data-stu-id="9c29c-131">Security Center billing is always based on your Security Center security policy and hello solutions installed on a workspace:</span></span>

- <span data-ttu-id="9c29c-132">**무료 계층** – 보안 센터 hello 기본 작업 영역에 hello 'SecurityCenterFree' 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-132">**Free tier** – Security Center installs hello 'SecurityCenterFree' solution on hello default workspace.</span></span> <span data-ttu-id="9c29c-133">Hello 무료 계층에 대 한 요금이 청구 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-133">You are not billed for hello Free tier.</span></span>
- <span data-ttu-id="9c29c-134">**표준 계층** – 보안 센터 'SecurityCenterFree' hello를 설치 하 고 솔루션에 'Security' hello 기본 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-134">**Standard tier** – Security Center installs hello 'SecurityCenterFree' and 'Security’ solutions on hello default workspace.</span></span>

<span data-ttu-id="9c29c-135">자세한 내용은 [Security Center 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c29c-135">For more information on pricing, see [Security Center pricing](https://azure.microsoft.com/pricing/details/security-center/).</span></span> <span data-ttu-id="9c29c-136">가격 페이지 주소 hello toosecurity 데이터 저장 및 2017 년 6 월에에서 할부 청구 시작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-136">hello pricing page addresses changes toosecurity data storage and prorated billing starting in June 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29c-137">보안 센터에서 만든 작업 영역의 hello OMS 가격 책정 계층에 보안 센터 청구 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-137">hello OMS pricing tier of workspaces created by Security Center does not affect Security Center billing.</span></span>
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a><span data-ttu-id="9c29c-138">보안 센터에서 만든 hello 기본 작업 영역을 삭제할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="9c29c-138">Can I delete hello default workspaces created by Security Center?</span></span>
<span data-ttu-id="9c29c-139">**Hello 기본 작업 영역 삭제 권장 되지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9c29c-139">**Deleting hello default workspace is not recommended.**</span></span> <span data-ttu-id="9c29c-140">보안 센터 내 vm에서 hello 기본 작업 영역 toostore 보안 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-140">Security Center uses hello default workspaces toostore security data from your VMs.</span></span>  <span data-ttu-id="9c29c-141">보안 센터 작업 영역을 삭제 하는 경우는 없습니다 toocollect이이 데이터 및 몇 가지 보안 권장 사항 및 경고를 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="9c29c-141">If you delete a workspace, Security Center is unable toocollect this data and some security recommendations and alerts are unavailable</span></span>

<span data-ttu-id="9c29c-142">toorecover, 제거 hello hello Vm 삭제 하는 연결 된 toohello 작업 영역에서 Microsoft Monitoring Agent입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-142">toorecover, remove hello Microsoft Monitoring Agent on hello VMs connected toohello deleted workspace.</span></span> <span data-ttu-id="9c29c-143">보안 센터 hello 에이전트를 다시 설치 하 고 새 기본 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-143">Security Center reinstalls hello agent and creates new default workspaces.</span></span>

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a><span data-ttu-id="9c29c-144">경우에 어떻게 hello Microsoft Monitoring Agent hello VM에 대 한 확장으로 이미 설치 된?</span><span class="sxs-lookup"><span data-stu-id="9c29c-144">What if hello Microsoft Monitoring Agent was already installed as an extension on hello VM?</span></span>
<span data-ttu-id="9c29c-145">보안 센터에서 기존 연결 toouser 작업 영역을 재정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-145">Security Center does not override existing connections toouser workspaces.</span></span> <span data-ttu-id="9c29c-146">보안 센터 hello hello 작업 영역에서 VM에서에서 보안 데이터를 저장 이미 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-146">Security Center stores security data from hello VM in hello workspace already connected.</span></span>

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a><span data-ttu-id="9c29c-147">경우에 어떻게 확장 아니라 hello 컴퓨터에 설치 된 Microsoft Monitoring Agent 해야 했던?</span><span class="sxs-lookup"><span data-stu-id="9c29c-147">What if I had a Microsoft Monitoring Agent installed on hello machine but not as an extension?</span></span>
<span data-ttu-id="9c29c-148">Hello Microsoft Monitoring Agent가 직접 설치 된 경우 hello에 VM (이 아니라 Azure 확장), 보안 센터를 설치 하지 않습니다 hello Microsoft Monitoring Agent 및 보안 모니터링 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-148">If hello Microsoft Monitoring Agent is installed directly on hello VM (not as an Azure extension), Security Center will not install hello Microsoft Monitoring Agent and security monitoring will be limited.</span></span>

### <a name="what-is-hello-impact-of-removing-these-extensions"></a><span data-ttu-id="9c29c-149">이러한 확장을 제거할 경우의 hello 영향 이란?</span><span class="sxs-lookup"><span data-stu-id="9c29c-149">What is hello impact of removing these extensions?</span></span>
<span data-ttu-id="9c29c-150">Hello Microsoft 모니터링 확장을 제거 하는 경우 보안 센터 hello VM 수 toocollect 보안 데이터는 하지 않으며 일부 보안 권장 사항 및 경고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-150">If you remove hello Microsoft Monitoring Extension, Security Center is not able toocollect security data from hello VM and some security recommendations and alerts are unavailable.</span></span> <span data-ttu-id="9c29c-151">보안 센터에는 24 시간 이내 hello VM hello 확장 없습니다 및 파일이 손실 hello 확장 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-151">Within 24 hours, Security Center determines that hello VM is missing hello extension and reinstalls hello extension.</span></span>

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a><span data-ttu-id="9c29c-152">Hello 자동 에이전트 설치 및 작업 영역 만들기를 중지 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9c29c-152">How do I stop hello automatic agent installation and workspace creation?</span></span>
<span data-ttu-id="9c29c-153">Hello 보안 정책에서 구독에 대 한 데이터 수집을 해제할 수 있지만 권장 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-153">You can turn off data collection for your subscriptions in hello security policy but this is not recommended.</span></span> <span data-ttu-id="9c29c-154">데이터 컬렉션을 해제하면 Security Center 권장 사항 및 경고를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-154">Turning off data collection limits Security Center recommendations and alerts.</span></span> <span data-ttu-id="9c29c-155">데이터 수집 hello 표준 가격 책정 계층에 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-155">Data collection is required for subscriptions on hello Standard pricing tier.</span></span> <span data-ttu-id="9c29c-156">toodisable 데이터 수집:</span><span class="sxs-lookup"><span data-stu-id="9c29c-156">toodisable data collection:</span></span>

1. <span data-ttu-id="9c29c-157">구독 hello 표준 계층으로 구성 된 경우 해당 구독에 대 한 보안 정책을 hello 열고 hello 선택 **무료** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-157">If your subscription is configured for hello Standard tier, open hello security policy for that subscription and select hello **Free** tier.</span></span>

   ![가격 책정 계층 ][1]

2. <span data-ttu-id="9c29c-159">다음으로, 선택 하 여 데이터 수집을 해제할 **오프** hello에 **보안 정책-데이터 수집** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-159">Next, turn off data collection by selecting **Off** on hello **Security policy – Data collection** blade.</span></span>

   ![데이터 수집][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a><span data-ttu-id="9c29c-161">Security Center에서 설치한 OMS 확장을 제거하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-161">How do I remove OMS extensions installed by Security Center?</span></span>
<span data-ttu-id="9c29c-162">Microsoft Monitoring Agent hello를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-162">You can manually remove hello Microsoft Monitoring Agent.</span></span> <span data-ttu-id="9c29c-163">Security Center 권장 사항 및 경고를 제한하기 때문에 권장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-163">This is not recommended as it limits Security Center recommendations and alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="9c29c-164">데이터 수집을 사용 하는 경우 보안 센터를 다시 설치 하려고 hello 에이전트 제거 하 고 나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-164">If data collection is enabled, Security Center will reinstall hello agent after you remove it.</span></span>  <span data-ttu-id="9c29c-165">Hello 에이전트를 수동으로 제거 하기 전에 toodisable 데이터 수집을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-165">You need toodisable data collection before manually removing hello agent.</span></span> <span data-ttu-id="9c29c-166">참조 [hello 자동 에이전트 설치 및 작업 영역 만들기 중지 어떻게?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) 에 대 한 데이터 수집을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-166">See [How do I stop hello automatic agent installation and workspace creation?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) for instructions on disabling data collection.</span></span>
>
>

<span data-ttu-id="9c29c-167">toomanually는 hello 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-167">toomanually remove hello agent:</span></span>

1.  <span data-ttu-id="9c29c-168">Hello 포털을 열고 **로그 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-168">In hello portal, open **Log Analytics**.</span></span>
2.  <span data-ttu-id="9c29c-169">Hello 로그 분석 블레이드에서 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-169">On hello Log Analytics blade, select a workspace:</span></span>
3.  <span data-ttu-id="9c29c-170">원하는 toomonitor 및 선택 하지 않는 각 VM 선택 **연결 끊기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-170">Select each VM that you don’t want toomonitor and select **Disconnect**.</span></span>

   ![Hello 에이전트 제거][3]

> [!NOTE]
> <span data-ttu-id="9c29c-172">Linux VM에 이미 비 확장 OMS 에이전트 hello 에이전트도 제거 hello 확장 제거 되 고 hello 고객에 게 tooreinstall 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-172">If a Linux VM already has a non-extension OMS agent, removing hello extension removes hello agent as well and hello customer has tooreinstall it.</span></span>
>
>

## <a name="existing-oms-customers"></a><span data-ttu-id="9c29c-173">기존 OMS 고객</span><span class="sxs-lookup"><span data-stu-id="9c29c-173">Existing OMS customers</span></span>

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a><span data-ttu-id="9c29c-174">Security Center에서 VM과 작업 영역 간의 모든 기존 연결을 재정의하나요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-174">Does Security Center override any existing connections between VMs and workspaces?</span></span>
<span data-ttu-id="9c29c-175">VM에 Azure 확장으로 설치 된 Microsoft Monitoring Agent hello 이미 있으면 보안 센터 hello 기존 작업 영역 연결을 재정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-175">If a VM already has hello Microsoft Monitoring Agent installed as an Azure extension, Security Center does not override hello existing workspace connection.</span></span> <span data-ttu-id="9c29c-176">대신, 보안 센터 hello 기존 작업 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-176">Instead, Security Center uses hello existing workspace.</span></span>

<span data-ttu-id="9c29c-177">보안 센터 솔루션은 hello 작업 영역에 없는 경우 설치를 이미 사용 하며 hello 솔루션은 적용 된 유일한 toohello 관련 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-177">A Security Center solution is installed on hello workspace if not present already, and hello solution is applied only toohello relevant VMs.</span></span> <span data-ttu-id="9c29c-178">솔루션에 추가 하면 기본 tooall Windows 및 Linux 에이전트 연결된 tooyour 로그 분석 작업 영역에 의해 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-178">When you add a solution, it's automatically deployed by default tooall Windows and Linux agents connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="9c29c-179">[솔루션 Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), tooapply 범위를 허용 하는 OMS 기능, tooyour 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-179">[Solution Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), which is an OMS feature, allows you tooapply a scope tooyour solutions.</span></span>

<span data-ttu-id="9c29c-180">Hello Microsoft Monitoring Agent가 직접 설치 된 경우 hello에 VM (이 아니라 Azure 확장), 보안 센터를 설치 하지 않습니다 hello Microsoft Monitoring Agent 및 보안 모니터링 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-180">If hello Microsoft Monitoring Agent is installed directly on hello VM (not as an Azure extension), Security Center will not install hello Microsoft Monitoring Agent and security monitoring is limited.</span></span>

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a><span data-ttu-id="9c29c-181">hello 데이터 플랫폼 마이그레이션 hello 연결 내 Vm 및 내 작업 영역 중 하나를 위반 하는 것으로 의심 되는 경우 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-181">What should I do if I suspect that hello data platform migration broke hello connection between one of my VMs and my workspace?</span></span>
<span data-ttu-id="9c29c-182">이런 상황은 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-182">This should not happen.</span></span> <span data-ttu-id="9c29c-183">있다면 않습니다 [Azure 지원 요청 만들기](../azure-supportability/how-to-create-azure-support-request.md) hello 다음 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-183">If it does happen, then [Create an Azure support request](../azure-supportability/how-to-create-azure-support-request.md) and include hello following details:</span></span>

- <span data-ttu-id="9c29c-184">VM을 영향을 받음 hello의 hello Azure 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="9c29c-184">hello Azure resource ID of hello impacted VM</span></span>
- <span data-ttu-id="9c29c-185">hello 연결이 끊겼습니다 전에 hello 확장에 구성 된 hello 영역의 hello Azure 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="9c29c-185">hello Azure resource ID of hello workspace configured on hello extension before hello connection was broken</span></span>
- <span data-ttu-id="9c29c-186">hello 에이전트와 이전에 설치 된 버전</span><span class="sxs-lookup"><span data-stu-id="9c29c-186">hello agent and version that was previously installed</span></span>

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a><span data-ttu-id="9c29c-187">Security Center에서 기존 OMS 작업 영역에 솔루션을 설치하나요?</span><span class="sxs-lookup"><span data-stu-id="9c29c-187">Does Security Center install solutions on my existing OMS workspaces?</span></span> <span data-ttu-id="9c29c-188">Hello 요금이 청구 될 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9c29c-188">What are hello billing implications?</span></span>
<span data-ttu-id="9c29c-189">Tooyour 가격 책정 계층에 따라이 작업 영역에서 솔루션을 사용 하면 VM은 이미 연결 된 tooa 작업 영역을 만든 보안 센터 보안 센터를 식별 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="9c29c-189">When Security Center identifies that a VM is already connected tooa workspace you created, Security Center enables solutions on this workspace according tooyour pricing tier.</span></span> <span data-ttu-id="9c29c-190">솔루션 hello를 통해 적용 된 유일한 toohello 관련 Azure Vm은 [솔루션을 대상으로](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)이므로 hello 청구 남아 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-190">hello solutions are applied only toohello relevant Azure VMs, via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), so hello billing remains hello same.</span></span>

- <span data-ttu-id="9c29c-191">**무료 계층** – 보안 센터 hello 작업 영역에 hello 'SecurityCenterFree' 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-191">**Free tier** – Security Center installs hello 'SecurityCenterFree' solution on hello workspace.</span></span> <span data-ttu-id="9c29c-192">Hello 무료 계층에 대 한 요금이 청구 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-192">You are not billed for hello Free tier.</span></span>
- <span data-ttu-id="9c29c-193">**표준 계층** – 보안 센터 'SecurityCenterFree' hello를 설치 하 고 솔루션에 'Security' hello 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-193">**Standard tier** – Security Center installs hello 'SecurityCenterFree' and 'Security' solutions on hello workspace.</span></span>

   ![기본 작업 영역의 솔루션][4]

> [!NOTE]
> <span data-ttu-id="9c29c-195">hello 로그 분석에서 'Security' 솔루션은 hello 보안 및 감사 솔루션을 OMS에입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-195">hello ‘Security’ solution in Log Analytics is hello Security & Audit solution in OMS.</span></span>
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a><span data-ttu-id="9c29c-196">내 환경에서 이미 작업 영역, 사용 합니까 toocollect 보안 데이터?</span><span class="sxs-lookup"><span data-stu-id="9c29c-196">I already have workspaces in my environment, can I use them toocollect security data?</span></span>
<span data-ttu-id="9c29c-197">VM에 Azure 확장으로 설치 된 Microsoft Monitoring Agent hello 이미 있으면 보안 센터 hello 기존 연결 된 작업 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-197">If a VM already has hello Microsoft Monitoring Agent installed as an Azure extension, Security Center uses hello existing connected workspace.</span></span> <span data-ttu-id="9c29c-198">보안 센터 솔루션은 hello 작업 영역에 없는 경우 설치를 이미 사용 하며 hello 솔루션은 적용 된 유일한 toohello 통해 관련 Vm [솔루션을 대상으로](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-198">A Security Center solution is installed on hello workspace if not present already, and hello solution is applied only toohello relevant VMs via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).</span></span>

<span data-ttu-id="9c29c-199">보안 센터 Vm에서 hello Microsoft Monitoring Agent는 설치 될 때 보안 센터에서 만든 hello 기본 중 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-199">When Security Center installs hello Microsoft Monitoring Agent on VMs, it uses hello default workspace(s) created by Security Center.</span></span> <span data-ttu-id="9c29c-200">곧 고객은 어떤 중 사용 되는 수 tooconfigure 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-200">Soon customers will be able tooconfigure which workspace(s) are used.</span></span>

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a><span data-ttu-id="9c29c-201">내 작업 영역에 보안 솔루션이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-201">I already have security solution on my workspaces.</span></span> <span data-ttu-id="9c29c-202">Hello 요금이 청구 될 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="9c29c-202">What are hello billing implications?</span></span>
<span data-ttu-id="9c29c-203">hello 보안 및 감사 솔루션은 Azure Vm에 대 한 보안 센터 표준 계층 기능을 사용 하는 tooenable입니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-203">hello Security & Audit solution is used tooenable Security Center Standard tier features for Azure VMs.</span></span> <span data-ttu-id="9c29c-204">Hello 보안 및 감사 솔루션 작업 영역에 이미 설치 되어 있는 경우 보안 센터 hello 기존 솔루션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-204">If hello Security & Audit solution is already installed on a workspace, Security Center uses hello existing solution.</span></span> <span data-ttu-id="9c29c-205">요금 청구는 변하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c29c-205">There is no change in billing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c29c-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c29c-206">Next steps</span></span>
<span data-ttu-id="9c29c-207">hello 보안 센터 플랫폼 마이그레이션에 대해 자세히 toolearn 참조</span><span class="sxs-lookup"><span data-stu-id="9c29c-207">toolearn more about hello Security Center platform migration, see</span></span>

- [<span data-ttu-id="9c29c-208">Azure Security Center 플랫폼 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="9c29c-208">Azure Security Center Platform Migration</span></span>](security-center-platform-migration.md)
- <span data-ttu-id="9c29c-209">[Azure Security Center 문제 해결 가이드](security-center-troubleshooting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="9c29c-209">[Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md)</span></span>

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
