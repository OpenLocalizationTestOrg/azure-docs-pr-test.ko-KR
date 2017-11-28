---
title: "Security Center 플랫폼 마이그레이션 FAQ | Microsoft Docs"
description: "이 FAQ는 Azure Security Center 플랫폼 마이그레이션에 대한 질문에 답변합니다."
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
ms.openlocfilehash: 2ffbaca614d667db565197f3c13b1658fffc2a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="security-center-platform-migration-faq"></a><span data-ttu-id="c1e12-103">Security Center 마이그레이션 FAQ</span><span class="sxs-lookup"><span data-stu-id="c1e12-103">Security Center platform migration FAQ</span></span>
<span data-ttu-id="c1e12-104">2017년 6월 초에 Azure Security Center는 Microsoft Monitoring Agent를 사용하여 데이터를 수집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-104">In early June 2017, Azure Security Center began using the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="c1e12-105">자세한 내용은 [Azure Security Center 플랫폼 마이그레이션](security-center-platform-migration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-105">To learn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="c1e12-106">이 FAQ는 플랫폼 마이그레이션에 대한 질문에 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-106">This FAQ answers questions about the platform migration.</span></span>

## <a name="data-collection-agents-and-workspaces"></a><span data-ttu-id="c1e12-107">데이터 수집, 에이전트 및 작업 영역</span><span class="sxs-lookup"><span data-stu-id="c1e12-107">Data collection, agents, and workspaces</span></span>

### <a name="how-is-data-collected"></a><span data-ttu-id="c1e12-108">데이터를 어떻게 수집해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-108">How is data collected?</span></span>
<span data-ttu-id="c1e12-109">Security Center는 Microsoft Monitoring Agent를 사용하여 VM에서 보안 데이터를 수집했습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-109">Security Center uses the Microsoft Monitoring Agent to collect security data from your VMs.</span></span> <span data-ttu-id="c1e12-110">이 보안 데이터는 취약점 및 보안 이벤트를 식별하는 데 사용되는 보안 구성에 대한 정보를 포함하며 위협을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-110">The security data includes information about security configurations, which are used to identify vulnerabilities, and security events, which are used to detect threats.</span></span> <span data-ttu-id="c1e12-111">에이전트에 의해 수집된 데이터는 VM에 연결된 기존 Log Analytics 작업 영역 또는 Security Center에서 만든 새 작업 영역 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-111">Data collected by the agent is stored in either an existing Log Analytics workspace connected to the VM or a new workspace created by Security Center.</span></span> <span data-ttu-id="c1e12-112">Security Center가 새 작업 영역을 만들 때 VM의 지리적 위치가 고려됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-112">When Security Center creates a new workspace, the geolocation of the VM is taken into account.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e12-113">Microsoft Monitoring Agent는 OMS(Operations Management Suite), Log Analytics 서비스 및 SCOM(System Center Operations Manager)에서 사용되는 것과 동일한 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-113">The Microsoft Monitoring Agent is the same agent used by the Operations Management Suite (OMS), Log Analytics service and System Center Operations Manager (SCOM).</span></span>
>
>

<span data-ttu-id="c1e12-114">처음으로 데이터 수집을 활성화하거나 구독을 마이그레이션하는 경우 Security Center는 각 VM에 대한 Azure 확장으로 Microsoft Monitoring Agent가 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-114">When data collection is enabled for the first time or when your subscriptions are migrated, Security Center checks to see if the Microsoft Monitoring Agent is already installed as an Azure extension on each of your VMs.</span></span> <span data-ttu-id="c1e12-115">Microsoft Monitoring Agent가 설치되지 않은 경우 Security Center는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-115">If the Microsoft Monitoring Agent is not installed, then Security Center will:</span></span>

- <span data-ttu-id="c1e12-116">VM에 Microsoft Monitoring Agent 설치</span><span class="sxs-lookup"><span data-stu-id="c1e12-116">install the Microsoft Monitoring agent on the VM</span></span>
   - <span data-ttu-id="c1e12-117">Security Center에서 만든 작업 영역이 이미 VM과 동일한 지리적 위치에 있는 경우 에이전트는 이 작업 영역에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-117">if a workspace created by Security Center already exists in the same geolocation as the VM, the agent is connected to this workspace</span></span>
   - <span data-ttu-id="c1e12-118">작업 영역이 없는 경우 Security Center는 해당 지리적 위치에서 새 리소스 그룹 및 기본 작업 영역을 만들고 해당 작업 영역에 에이전트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-118">if a workspace does not exist, Security Center creates a new resource group and default workspace in that geolocation, and connect the agent to that workspace.</span></span> <span data-ttu-id="c1e12-119">작업 영역 및 리소스 그룹에 대한 명명 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-119">The naming convention for the workspace and resource group are:</span></span>

       <span data-ttu-id="c1e12-120">작업 영역: DefaultWorkspace-[subscription-ID]-[geo]</span><span class="sxs-lookup"><span data-stu-id="c1e12-120">Workspace: DefaultWorkspace-[subscription-ID]-[geo]</span></span>

       <span data-ttu-id="c1e12-121">리소스 그룹: DefaultResouceGroup-[geo]</span><span class="sxs-lookup"><span data-stu-id="c1e12-121">Resource Group: DefaultResouceGroup-[geo]</span></span>
- <span data-ttu-id="c1e12-122">작업 영역에서 Security Center 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="c1e12-122">install a Security Center solution on the workspace</span></span>

<span data-ttu-id="c1e12-123">작업 영역의 위치는 VM의 위치를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-123">The location of the workspace is based on the location of the VM.</span></span> <span data-ttu-id="c1e12-124">자세한 내용은 [데이터 보안](security-center-data-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-124">To learn more, see [Data Security](security-center-data-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c1e12-125">플랫폼 마이그레이션 이전에 Security Center는 Azure Monitoring Agent를 사용하여 VM에서 보안 데이터를 수집하고 저장소 계정에 데이터를 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-125">Prior to platform migration, Security Center collected security data from your VMs using the Azure Monitoring Agent, and data was stored in your storage account.</span></span> <span data-ttu-id="c1e12-126">플랫폼 마이그레이션 후에 Security Center는 Microsoft Monitoring Agent 및 작업 영역을 사용하여 동일한 데이터를 수집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-126">After the platform migration, Security Center uses the Microsoft Monitoring Agent and workspace to collect and store the same data.</span></span> <span data-ttu-id="c1e12-127">저장소 계정은 마이그레이션 후에 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-127">The storage account can be removed after the migration.</span></span>
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-the-workspaces-created-by-security-center"></a><span data-ttu-id="c1e12-128">Security Center에서 만든 작업 영역에서 Log Analytics 또는 OMS에 대한 요금을 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-128">Am I billed for Log Analytics or OMS on the workspaces created by Security Center?</span></span>
<span data-ttu-id="c1e12-129">아니요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-129">No.</span></span> <span data-ttu-id="c1e12-130">Security Center에서 만든 작업 영역은 노드 요금 청구당 OMS에 구성되는 동안 OMS 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-130">Workspaces created by Security Center, while configured for OMS per node billing, do not incur OMS charges.</span></span> <span data-ttu-id="c1e12-131">Security Center 청구는 항상 작업 영역에 설치된 Security Center 보안 정책 및 솔루션에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-131">Security Center billing is always based on your Security Center security policy and the solutions installed on a workspace:</span></span>

- <span data-ttu-id="c1e12-132">**무료 계층** – Security Center는 기본 작업 영역에서 'SecurityCenterFree' 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-132">**Free tier** – Security Center installs the 'SecurityCenterFree' solution on the default workspace.</span></span> <span data-ttu-id="c1e12-133">체험 계층에 대한 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-133">You are not billed for the Free tier.</span></span>
- <span data-ttu-id="c1e12-134">**표준 계층** – Security Center는 기본 작업 영역에서 'SecurityCenterFree' 및 'Security' 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-134">**Standard tier** – Security Center installs the 'SecurityCenterFree' and 'Security’ solutions on the default workspace.</span></span>

<span data-ttu-id="c1e12-135">자세한 내용은 [Security Center 가격 책정](https://azure.microsoft.com/pricing/details/security-center/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-135">For more information on pricing, see [Security Center pricing](https://azure.microsoft.com/pricing/details/security-center/).</span></span> <span data-ttu-id="c1e12-136">가격 책정 페이지 주소는 2017년 6월부터 보안 데이터 저장소 및 비례 배분 청구로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-136">The pricing page addresses changes to security data storage and prorated billing starting in June 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e12-137">Security Center에서 만든 작업 영역의 OMS 가격 책정 계층은 Security Center 청구에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-137">The OMS pricing tier of workspaces created by Security Center does not affect Security Center billing.</span></span>
>
>

### <a name="can-i-delete-the-default-workspaces-created-by-security-center"></a><span data-ttu-id="c1e12-138">Security Center에서 만든 기본 작업 영역을 삭제할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-138">Can I delete the default workspaces created by Security Center?</span></span>
<span data-ttu-id="c1e12-139">**기본 작업 영역을 삭제하지 않는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="c1e12-139">**Deleting the default workspace is not recommended.**</span></span> <span data-ttu-id="c1e12-140">Security Center는 기본 작업 영역을 사용하여 VM의 보안 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-140">Security Center uses the default workspaces to store security data from your VMs.</span></span>  <span data-ttu-id="c1e12-141">작업 영역을 삭제하는 경우 Security Center는 이 데이터 및 일부 보안 권장 사항을 수집할 수 없고 경고를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-141">If you delete a workspace, Security Center is unable to collect this data and some security recommendations and alerts are unavailable</span></span>

<span data-ttu-id="c1e12-142">복구하려면 삭제된 작업 영역에 연결된 VM에서 Microsoft Monitoring Agent를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-142">To recover, remove the Microsoft Monitoring Agent on the VMs connected to the deleted workspace.</span></span> <span data-ttu-id="c1e12-143">Security Center는 에이전트를 다시 설치하고 새 기본 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-143">Security Center reinstalls the agent and creates new default workspaces.</span></span>

### <a name="what-if-the-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-the-vm"></a><span data-ttu-id="c1e12-144">Microsoft Monitoring Agent가 VM에 확장으로 이미 설치되어 있으면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-144">What if the Microsoft Monitoring Agent was already installed as an extension on the VM?</span></span>
<span data-ttu-id="c1e12-145">Security Center는 사용자 작업 영역에 대한 기존 연결을 재정의하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-145">Security Center does not override existing connections to user workspaces.</span></span> <span data-ttu-id="c1e12-146">Security Center는 이미 연결된 작업 영역에서 VM의 보안 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-146">Security Center stores security data from the VM in the workspace already connected.</span></span>

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-the-machine-but-not-as-an-extension"></a><span data-ttu-id="c1e12-147">컴퓨터에 확장판이 아닌 Microsoft Monitoring Agent를 설치하면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-147">What if I had a Microsoft Monitoring Agent installed on the machine but not as an extension?</span></span>
<span data-ttu-id="c1e12-148">Microsoft Monitoring Agent가 (Azure 확장이 아니라) VM에 직접 설치되면 Security Center는 Microsoft Monitoring Agent를 설치하지 않고 보안 모니터링이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-148">If the Microsoft Monitoring Agent is installed directly on the VM (not as an Azure extension), Security Center will not install the Microsoft Monitoring Agent and security monitoring will be limited.</span></span>

### <a name="what-is-the-impact-of-removing-these-extensions"></a><span data-ttu-id="c1e12-149">이러한 확장을 제거할 경우 어떤 영향이 있나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-149">What is the impact of removing these extensions?</span></span>
<span data-ttu-id="c1e12-150">Microsoft Monitoring 확장을 제거하는 경우 Security Center는 VM의 보안 데이터 및 일부 보안 권장 사항을 수집할 수 없고 경고를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-150">If you remove the Microsoft Monitoring Extension, Security Center is not able to collect security data from the VM and some security recommendations and alerts are unavailable.</span></span> <span data-ttu-id="c1e12-151">24시간 이내에 Security Center는 VM이 확장을 누락하고 확장을 다시 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-151">Within 24 hours, Security Center determines that the VM is missing the extension and reinstalls the extension.</span></span>

### <a name="how-do-i-stop-the-automatic-agent-installation-and-workspace-creation"></a><span data-ttu-id="c1e12-152">자동 에이전트 설치 및 작업 영역 생성을 중지하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-152">How do I stop the automatic agent installation and workspace creation?</span></span>
<span data-ttu-id="c1e12-153">Security Center에서 구독에 대한 데이터 수집을 해제할 수 있지만 권장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-153">You can turn off data collection for your subscriptions in the security policy but this is not recommended.</span></span> <span data-ttu-id="c1e12-154">데이터 컬렉션을 해제하면 Security Center 권장 사항 및 경고를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-154">Turning off data collection limits Security Center recommendations and alerts.</span></span> <span data-ttu-id="c1e12-155">데이터 수집은 표준 가격 책정 계층의 구독에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-155">Data collection is required for subscriptions on the Standard pricing tier.</span></span> <span data-ttu-id="c1e12-156">데이터 수집을 비활성화하려면:</span><span class="sxs-lookup"><span data-stu-id="c1e12-156">To disable data collection:</span></span>

1. <span data-ttu-id="c1e12-157">표준 계층에 대한 구독이 구성된 경우 해당 구독에 대한 보안 정책을 열고 **체험** 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-157">If your subscription is configured for the Standard tier, open the security policy for that subscription and select the **Free** tier.</span></span>

   ![가격 책정 계층 ][1]

2. <span data-ttu-id="c1e12-159">다음으로 **보안 정책 - 데이터 수집** 블레이드에서 **끄기**를 선택하여 데이터 수집을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-159">Next, turn off data collection by selecting **Off** on the **Security policy – Data collection** blade.</span></span>

   ![데이터 수집][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a><span data-ttu-id="c1e12-161">Security Center에서 설치한 OMS 확장을 제거하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-161">How do I remove OMS extensions installed by Security Center?</span></span>
<span data-ttu-id="c1e12-162">Microsoft Monitoring Agent를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-162">You can manually remove the Microsoft Monitoring Agent.</span></span> <span data-ttu-id="c1e12-163">Security Center 권장 사항 및 경고를 제한하기 때문에 권장되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-163">This is not recommended as it limits Security Center recommendations and alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e12-164">데이터 수집을 사용하는 경우 Security Center는 에이전트를 제거한 후에 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-164">If data collection is enabled, Security Center will reinstall the agent after you remove it.</span></span>  <span data-ttu-id="c1e12-165">수동으로 에이전트를 제거하기 전에 데이터 수집을 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-165">You need to disable data collection before manually removing the agent.</span></span> <span data-ttu-id="c1e12-166">데이터 수집을 사용하지 않도록 설정하는 지침은 [자동 에이전트 설치 및 작업 영역 생성을 중지하려면 어떻게 할까요?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-166">See [How do I stop the automatic agent installation and workspace creation?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) for instructions on disabling data collection.</span></span>
>
>

<span data-ttu-id="c1e12-167">수동으로 에이전트를 제거하려면:</span><span class="sxs-lookup"><span data-stu-id="c1e12-167">To manually remove the agent:</span></span>

1.  <span data-ttu-id="c1e12-168">포털에서 **Log Analytics**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-168">In the portal, open **Log Analytics**.</span></span>
2.  <span data-ttu-id="c1e12-169">Log Analytics 블레이드에서 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-169">On the Log Analytics blade, select a workspace:</span></span>
3.  <span data-ttu-id="c1e12-170">모니터링하지 않을 각 VM을 선택하고 **연결 끊기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-170">Select each VM that you don’t want to monitor and select **Disconnect**.</span></span>

   ![에이전트 제거][3]

> [!NOTE]
> <span data-ttu-id="c1e12-172">Linux VM에 이미 비확장 OMS 에이전트가 설치된 경우 확장명을 제거하면 에이전트도 제거되고 고객이 다시 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-172">If a Linux VM already has a non-extension OMS agent, removing the extension removes the agent as well and the customer has to reinstall it.</span></span>
>
>

## <a name="existing-oms-customers"></a><span data-ttu-id="c1e12-173">기존 OMS 고객</span><span class="sxs-lookup"><span data-stu-id="c1e12-173">Existing OMS customers</span></span>

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a><span data-ttu-id="c1e12-174">Security Center에서 VM과 작업 영역 간의 모든 기존 연결을 재정의하나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-174">Does Security Center override any existing connections between VMs and workspaces?</span></span>
<span data-ttu-id="c1e12-175">VM에 Azure 확장으로 Microsoft Monitoring Agent가 이미 설치되어 있으면 Security Center에서 기존 작업 영역 연결을 재정의하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-175">If a VM already has the Microsoft Monitoring Agent installed as an Azure extension, Security Center does not override the existing workspace connection.</span></span> <span data-ttu-id="c1e12-176">대신 Security Center에서 기존 작업 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-176">Instead, Security Center uses the existing workspace.</span></span>

<span data-ttu-id="c1e12-177">Security Center 솔루션이 작업 영역에 없는 경우 설치되고 솔루션은 관련 VM에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-177">A Security Center solution is installed on the workspace if not present already, and the solution is applied only to the relevant VMs.</span></span> <span data-ttu-id="c1e12-178">솔루션을 추가하면 기본적으로 Log Analytics 작업 영역에 연결된 모든 Windows 및 Linux 에이전트에 의해 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-178">When you add a solution, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span></span> <span data-ttu-id="c1e12-179">OMS 기능인 [솔루션 대상 지정](../operations-management-suite/operations-management-suite-solution-targeting.md)을 사용하면 솔루션에 범위를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-179">[Solution Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), which is an OMS feature, allows you to apply a scope to your solutions.</span></span>

<span data-ttu-id="c1e12-180">Microsoft Monitoring Agent가 (Azure 확장이 아니라) VM에 직접 설치되면 Security Center는 Microsoft Monitoring Agent를 설치하지 않고 보안 모니터링이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-180">If the Microsoft Monitoring Agent is installed directly on the VM (not as an Azure extension), Security Center will not install the Microsoft Monitoring Agent and security monitoring is limited.</span></span>

### <a name="what-should-i-do-if-i-suspect-that-the-data-platform-migration-broke-the-connection-between-one-of-my-vms-and-my-workspace"></a><span data-ttu-id="c1e12-181">데이터 플랫폼 마이그레이션이 내 VM과 내 작업 영역 간에 연결을 끊는 것으로 의심되는 경우 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-181">What should I do if I suspect that the data platform migration broke the connection between one of my VMs and my workspace?</span></span>
<span data-ttu-id="c1e12-182">이런 상황은 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-182">This should not happen.</span></span> <span data-ttu-id="c1e12-183">발생하는 경우 [Azure 지원을 요청](../azure-supportability/how-to-create-azure-support-request.md)하고 다음 세부 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-183">If it does happen, then [Create an Azure support request](../azure-supportability/how-to-create-azure-support-request.md) and include the following details:</span></span>

- <span data-ttu-id="c1e12-184">영향을 받는 VM의 Azure 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="c1e12-184">The Azure resource ID of the impacted VM</span></span>
- <span data-ttu-id="c1e12-185">연결이 끊기기 전에 확장에 구성된 작업 영역의 Azure 리소스 ID</span><span class="sxs-lookup"><span data-stu-id="c1e12-185">The Azure resource ID of the workspace configured on the extension before the connection was broken</span></span>
- <span data-ttu-id="c1e12-186">이전에 설치된 에이전트 및 버전</span><span class="sxs-lookup"><span data-stu-id="c1e12-186">The agent and version that was previously installed</span></span>

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-the-billing-implications"></a><span data-ttu-id="c1e12-187">Security Center에서 기존 OMS 작업 영역에 솔루션을 설치하나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-187">Does Security Center install solutions on my existing OMS workspaces?</span></span> <span data-ttu-id="c1e12-188">요금 청구에 영향을 주는 요인은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-188">What are the billing implications?</span></span>
<span data-ttu-id="c1e12-189">Security Center에서 VM이 만든 작업 영역에 이미 연결되어 있는지를 식별하는 경우 Security Center를 통해 가격 책정 계층에 따라 이 작업 영역에서 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-189">When Security Center identifies that a VM is already connected to a workspace you created, Security Center enables solutions on this workspace according to your pricing tier.</span></span> <span data-ttu-id="c1e12-190">솔루션이 [솔루션 대상 지정](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)을 통해 관련 Azure VM에만 적용되므로 청구는 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-190">The solutions are applied only to the relevant Azure VMs, via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), so the billing remains the same.</span></span>

- <span data-ttu-id="c1e12-191">**체험 계층** – Security Center는 작업 영역에서 'SecurityCenterFree' 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-191">**Free tier** – Security Center installs the 'SecurityCenterFree' solution on the workspace.</span></span> <span data-ttu-id="c1e12-192">체험 계층에 대한 요금이 청구되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-192">You are not billed for the Free tier.</span></span>
- <span data-ttu-id="c1e12-193">**표준 계층** – Security Center는 작업 영역에서 'SecurityCenterFree' 및 'Security' 솔루션을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-193">**Standard tier** – Security Center installs the 'SecurityCenterFree' and 'Security' solutions on the workspace.</span></span>

   ![기본 작업 영역의 솔루션][4]

> [!NOTE]
> <span data-ttu-id="c1e12-195">Log Analytics에서 'Security' 솔루션은 OMS의 보안 및 감사 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-195">The ‘Security’ solution in Log Analytics is the Security & Audit solution in OMS.</span></span>
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-to-collect-security-data"></a><span data-ttu-id="c1e12-196">내 환경에 이미 작업 영역이 있는 경우 보안 데이터를 수집하는 데 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-196">I already have workspaces in my environment, can I use them to collect security data?</span></span>
<span data-ttu-id="c1e12-197">VM에 Azure 확장으로 Microsoft Monitoring Agent가 이미 설치되어 있으면 Security Center에서 기존 연결된 작업 영역 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-197">If a VM already has the Microsoft Monitoring Agent installed as an Azure extension, Security Center uses the existing connected workspace.</span></span> <span data-ttu-id="c1e12-198">Security Center 솔루션이 작업 영역에 없는 경우 설치되고 솔루션은 [솔루션 대상 지정](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)을 통해 관련 VM에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-198">A Security Center solution is installed on the workspace if not present already, and the solution is applied only to the relevant VMs via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).</span></span>

<span data-ttu-id="c1e12-199">Security Center에서 VM에 Microsoft Monitoring Agent를 설치하면 Security Center에서 만든 기본 작업 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-199">When Security Center installs the Microsoft Monitoring Agent on VMs, it uses the default workspace(s) created by Security Center.</span></span> <span data-ttu-id="c1e12-200">곧 고객은 사용되는 작업 영역을 구성할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-200">Soon customers will be able to configure which workspace(s) are used.</span></span>

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-the-billing-implications"></a><span data-ttu-id="c1e12-201">내 작업 영역에 보안 솔루션이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-201">I already have security solution on my workspaces.</span></span> <span data-ttu-id="c1e12-202">요금 청구에 영향을 주는 요인은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="c1e12-202">What are the billing implications?</span></span>
<span data-ttu-id="c1e12-203">보안 및 감사 솔루션은 Azure VM에 대한 Security Center 표준 계층 기능을 활성화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-203">The Security & Audit solution is used to enable Security Center Standard tier features for Azure VMs.</span></span> <span data-ttu-id="c1e12-204">보안 및 감사 솔루션이 작업 영역에 이미 설치되어 있는 경우 Security Center에서는 기존 솔루션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-204">If the Security & Audit solution is already installed on a workspace, Security Center uses the existing solution.</span></span> <span data-ttu-id="c1e12-205">요금 청구는 변하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1e12-205">There is no change in billing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1e12-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1e12-206">Next steps</span></span>
<span data-ttu-id="c1e12-207">Security Center 플랫폼 마이그레이션을 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1e12-207">To learn more about the Security Center platform migration, see</span></span>

- [<span data-ttu-id="c1e12-208">Azure Security Center 플랫폼 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="c1e12-208">Azure Security Center Platform Migration</span></span>](security-center-platform-migration.md)
- <span data-ttu-id="c1e12-209">[Azure Security Center 문제 해결 가이드](security-center-troubleshooting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c1e12-209">[Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md)</span></span>

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
