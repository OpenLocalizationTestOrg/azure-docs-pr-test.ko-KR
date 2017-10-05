---
title: "Azure Security Center 플랫폼 마이그레이션 | Microsoft Docs"
description: "이 문서에서는 Azure Security Center 데이터를 수집하는 방법에 대한 일부 변경 내용을 설명합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 5ddf71dcd9c5a2b03e3b1441d8c9b4d91b6bad12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-security-center-platform-migration"></a><span data-ttu-id="de1b4-103">Azure Security Center 플랫폼 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="de1b4-103">Azure Security Center platform migration</span></span>

<span data-ttu-id="de1b4-104">2017년 6월 초를 시작으로 Azure Security Center에서는 보안 데이터를 수집하고 저장하는 방법에 대한 중요한 변경 사항을 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-104">Beginning in early June 2017, Azure Security Center rolls out important changes to the way security data is collected and stored.</span></span>  <span data-ttu-id="de1b4-105">이러한 변경 사항으로 쉽게 보안 데이터를 검색하는 등 새로운 기능의 잠금을 해제하고 다른 Azure Management 및 모니터링 서비스와 연계합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-105">These changes unlock new capabilities like the ability to easily search security data and better aligns with other Azure management and monitoring services.</span></span>

> [!NOTE]
> <span data-ttu-id="de1b4-106">플랫폼 마이그레이션은 프로덕션 리소스에 영향을 주지 않고 사용자 측에서 작업을 수행하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-106">The platform migration should not impact your production resources, and no action is necessary from your side.</span></span>


## <a name="whats-happening-during-this-platform-migration"></a><span data-ttu-id="de1b4-107">이 플랫폼 마이그레이션 도중 어떤 상황이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="de1b4-107">What’s happening during this platform migration?</span></span>

<span data-ttu-id="de1b4-108">이전에 Security Center는 Azure Monitoring Agent를 사용하여 VM에서 보안 데이터를 수집했습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-108">Previously, Security Center used the Azure Monitoring Agent to collect security data from your VMs.</span></span> <span data-ttu-id="de1b4-109">이 기능은 취약점 및 보안 이벤트를 식별하는 데 사용되는 보안 구성에 대한 정보를 포함하며 위협을 검색하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-109">This includes information about security configurations, which are used to identify vulnerabilities, and security events, which are used to detect threats.</span></span> <span data-ttu-id="de1b4-110">이 데이터는 Azure의 Storage 계정에 저장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-110">This data was stored in your Storage account(s) in Azure.</span></span>

<span data-ttu-id="de1b4-111">또한 Security Center는 Microsoft Monitoring Agent를 사용하며 이는 Operations Management Suite 및 Log Analytics 서비스에서 사용하는 동일한 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-111">Going forward, Security Center uses the Microsoft Monitoring Agent – this is the same agent used by the Operations Management Suite and Log Analytics service.</span></span> <span data-ttu-id="de1b4-112">이 에이전트에서 수집된 데이터는 VM의 지리적 위치를 고려하여 Azure 구독 또는 새 작업 영역에 연결된 기존 *Log Analytics* [작업 영역](../log-analytics/log-analytics-manage-access.md) 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-112">Data collected from this agent is stored in either an existing *Log Analytics* [workspace](../log-analytics/log-analytics-manage-access.md) associated with your Azure subscription or a new workspace(s), taking into account the geolocation of the VM.</span></span>

## <a name="agent"></a><span data-ttu-id="de1b4-113">에이전트</span><span class="sxs-lookup"><span data-stu-id="de1b4-113">Agent</span></span>

<span data-ttu-id="de1b4-114">전환의 일부로 Microsoft Monitoring Agent([Windows](../log-analytics/log-analytics-windows-agents.md)용 또는 [Linux](../log-analytics/log-analytics-linux-agents.md)용)가 현재 데이터를 수집하는 모든 Azure VM에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-114">As part of the transition, the Microsoft Monitoring Agent (for [Windows](../log-analytics/log-analytics-windows-agents.md) or [Linux](../log-analytics/log-analytics-linux-agents.md)) is installed on all Azure VMs from which data is currently being collected.</span></span>  <span data-ttu-id="de1b4-115">VM이 Microsoft Monitoring Agent에 이미 설치된 경우 Security Center는 현재 설치된 에이전트를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-115">If the VM already has the Microsoft Monitoring Agent installed, Security Center leverages the current installed agent.</span></span>

<span data-ttu-id="de1b4-116">일정 기간(일반적으로 몇 일) 동안 두 에이전트는 데이터의 손실 없이 원활하게 전환하기 위해 함께 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-116">For a period of time (typically a few days), both agents will run side by side to ensure a smooth transition without any loss of data.</span></span> <span data-ttu-id="de1b4-117">그러면 Microsoft가 현재 파이프라인의 사용을 중단하기 전에 새 데이터 파이프라인이 작동하는지 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-117">This will enable Microsoft to validate that the new data pipeline is operational before discontinuing use of the current pipeline.</span></span> <span data-ttu-id="de1b4-118">확인이 완료되면 Azure Monitoring Agent는 VM에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-118">Once verified, the Azure Monitoring Agent will be removed from your VMs.</span></span> <span data-ttu-id="de1b4-119">사용자 측에서는 아무 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-119">No work is required on your part.</span></span> <span data-ttu-id="de1b4-120">모든 고객 마이그레이션되는 경우 전자 메일로 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-120">An email will notify you when all customers have been migrated.</span></span>
 
<span data-ttu-id="de1b4-121">보안 데이터에 간격이 발생할 수 있으므로 마이그레이션하는 동안 Azure Monitoring Agent를 수동으로 제거하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-121">It is not recommended that you manually uninstall the Azure Monitoring Agent during the migration as gaps in security data could result.</span></span> <span data-ttu-id="de1b4-122">추가 지원이 필요한 경우 [Microsoft 고객 서비스 및 지원 센터](https://support.microsoft.com/contactus/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de1b4-122">Please consult [Microsoft Customer Service and Support](https://support.microsoft.com/contactus/) if you need further assistance.</span></span> 

<span data-ttu-id="de1b4-123">Windows용 Microsoft Monitoring Agent는 TCP 포트 443을 사용해야 합니다. 자세한 정보는 [Azure Security Center 문제 해결 가이드](security-center-troubleshooting-guide.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de1b4-123">The Microsoft Monitoring Agent for Windows requires use TCP port 443, read [Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md) for more information.</span></span>


> [!NOTE] 
> <span data-ttu-id="de1b4-124">다른 Azure Management 및 모니터링 서비스에서 Microsoft Monitoring Agent를 사용할 수 있기 때문에 Security Center에서 데이터 수집을 끄는 경우에도 자동으로 에이전트를 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-124">Because the Microsoft Monitoring Agent may be used by other Azure management and monitoring services, the agent will not be uninstalled automatically when you turn off data collection in Security Center.</span></span> <span data-ttu-id="de1b4-125">그러나 필요한 경우 에이전트를 수동으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-125">However, you can manually uninstall the agent if needed.</span></span>

## <a name="workspace"></a><span data-ttu-id="de1b4-126">작업 영역</span><span class="sxs-lookup"><span data-stu-id="de1b4-126">Workspace</span></span>

<span data-ttu-id="de1b4-127">위에서 설명한 대로 (Security Center 대신) Microsoft Monitoring Agent에서 수집된 데이터는 VM의 지리적 위치를 고려하여 Azure 구독 또는 새 작업 영역에 연결된 기존 Log Analytics 작업 영역 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-127">As described previously, data collected from the Microsoft Monitoring Agent (on behalf of Security Center) are stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account the geolocation of the VM.</span></span>

<span data-ttu-id="de1b4-128">Azure Portal에서 Security Center에서 만든 항목을 포함하여 Log Analytics 작업 영역 목록을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-128">In the Azure portal, you can browse to see a list of your Log Analytics workspaces, including any created by Security Center.</span></span> <span data-ttu-id="de1b4-129">새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-129">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="de1b4-130">둘 다 다음과 같은 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-130">Both follow this naming convention:</span></span>

- <span data-ttu-id="de1b4-131">작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="de1b4-131">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
- <span data-ttu-id="de1b4-132">리소스 그룹: *DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="de1b4-132">Resource Group: *DefaultResouceGroup-[geo]*</span></span> 
 
<span data-ttu-id="de1b4-133">Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-133">For workspaces created by Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="de1b4-134">기존 작업 영역의 경우 작업 영역 가격 책정 계층에 따라 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-134">For existing workspaces, retention is based on the workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="de1b4-135">Security Center에서 이전에 수집된 데이터는 Storage 계정에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-135">Data previously collected by Security Center remains in your Storage account(s).</span></span> <span data-ttu-id="de1b4-136">마이그레이션이 완료된 후에 이러한 Storage 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-136">After the migration is complete, you can delete these Storage accounts.</span></span>

### <a name="oms-security-solution"></a><span data-ttu-id="de1b4-137">OMS 보안 솔루션</span><span class="sxs-lookup"><span data-stu-id="de1b4-137">OMS Security Solution</span></span> 

<span data-ttu-id="de1b4-138">OMS 보안 솔루션을 설치하지 않은 기존 고객의 경우 Microsoft에서는 이를 해당 작업 영역에 설치하고 Azure VM만을 대상으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-138">For existing customers that don’t have OMS Security solution installed, Microsoft is installing it on their workspace, but targeting only Azure VMs.</span></span> <span data-ttu-id="de1b4-139">OMS 관리 콘솔에 설치된 경우 자동으로 재구성되지 않으므로 이 솔루션을 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-139">Do not uninstall this solution, as there is no automatic remediation if this is done from OMS management console.</span></span>


## <a name="other-updates"></a><span data-ttu-id="de1b4-140">다른 업데이트</span><span class="sxs-lookup"><span data-stu-id="de1b4-140">Other updates</span></span>

<span data-ttu-id="de1b4-141">플랫폼 마이그레이션과 함께 몇 가지 부분적인 추가 업데이트를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-141">In conjunction with the platform migration, we are rolling out some additional minor updates:</span></span>

- <span data-ttu-id="de1b4-142">OS 버전이 추가로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-142">Additional OS versions will be supported.</span></span> <span data-ttu-id="de1b4-143">[여기](security-center-faq.md#virtual-machines)에서 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de1b4-143">See the list [here](security-center-faq.md#virtual-machines).</span></span>
- <span data-ttu-id="de1b4-144">OS 취약점 목록이 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-144">The list of OS vulnerabilities will be expanded.</span></span> <span data-ttu-id="de1b4-145">[여기](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)에서 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de1b4-145">See the list [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
- <span data-ttu-id="de1b4-146">[가격 책정](https://azure.microsoft.com/pricing/details/security-center/)은 매시간(이전에는 매일) 비례 배분되며, 이로 인해 일부 고객의 비용이 절감될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-146">[Pricing](https://azure.microsoft.com/pricing/details/security-center/) will be pro-rated hourly (previously it was daily), which will result in cost savings for some customers.</span></span>
- <span data-ttu-id="de1b4-147">데이터 수집이 필요하며 표준 가격 책정 계층의 고객에게 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-147">Data Collection will be required and automatically enabled for customers on the Standard pricing tier.</span></span>
- <span data-ttu-id="de1b4-148">Azure Security Center는 Azure 확장을 통해 배포되지 않은 맬웨어 방지 솔루션을 검색하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-148">Azure Security Center will begin discovering antimalware solutions that were not deployed via Azure extensions.</span></span> <span data-ttu-id="de1b4-149">Symantec Endpoint Protection 검색 및 Windows 2016용 Defender를 먼저 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-149">Discovery of Symantec Endpoint Protection and Defender for Windows 2016 will be available first.</span></span>
- <span data-ttu-id="de1b4-150">방지 정책 및 알림은 *구독* 수준에서만 구성 가능하지만 가격은 여전히 *리소스 그룹* 수준에서 설정 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="de1b4-150">Prevention policies and notifications are only configurable at the *Subscription* level, but pricing can still be set at the *Resource Group* level</span></span>

