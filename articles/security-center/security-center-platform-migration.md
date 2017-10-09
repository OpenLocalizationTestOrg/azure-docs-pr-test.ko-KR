---
title: "보안 센터 플랫폼 마이그레이션 aaaAzure | Microsoft Docs"
description: "이 문서에서는 몇 가지 변경 내용이 toohello 방법이 Azure 보안 센터 데이터를 수집 합니다."
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
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a><span data-ttu-id="22e38-103">Azure Security Center 플랫폼 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="22e38-103">Azure Security Center platform migration</span></span>

<span data-ttu-id="22e38-104">초기 6 월 2017 년 부터는 Azure 보안 센터에서는 중요 변경 내용 toohello 방식으로 보안 데이터 수집 되 고 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-104">Beginning in early June 2017, Azure Security Center rolls out important changes toohello way security data is collected and stored.</span></span>  <span data-ttu-id="22e38-105">이러한 변경 내용은 hello 기능 tooeasily 검색 보안 데이터와 같은 새로운 기능을 잠금 해제 하 고 다른 Azure 관리 및 서비스 모니터링을 더 잘 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-105">These changes unlock new capabilities like hello ability tooeasily search security data and better aligns with other Azure management and monitoring services.</span></span>

> [!NOTE]
> <span data-ttu-id="22e38-106">hello 플랫폼 마이그레이션에서는 프로덕션 리소스를 영향을 주지 않아야 하 고 프로그램 측에서 필요한 작업은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-106">hello platform migration should not impact your production resources, and no action is necessary from your side.</span></span>


## <a name="whats-happening-during-this-platform-migration"></a><span data-ttu-id="22e38-107">이 플랫폼 마이그레이션 도중 어떤 상황이 발생합니까?</span><span class="sxs-lookup"><span data-stu-id="22e38-107">What’s happening during this platform migration?</span></span>

<span data-ttu-id="22e38-108">이전에 보안 센터 내 vm에서 hello toocollect 보안 데이터를 Azure 모니터링 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-108">Previously, Security Center used hello Azure Monitoring Agent toocollect security data from your VMs.</span></span> <span data-ttu-id="22e38-109">사용 되는 tooidentify 취약점 보안 구성 및 사용 되는 toodetect 위협 요소인 보안 이벤트에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-109">This includes information about security configurations, which are used tooidentify vulnerabilities, and security events, which are used toodetect threats.</span></span> <span data-ttu-id="22e38-110">이 데이터는 Azure의 Storage 계정에 저장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-110">This data was stored in your Storage account(s) in Azure.</span></span>

<span data-ttu-id="22e38-111">그 이후에 보안 센터 Microsoft Monitoring Agent – hello를 사용 하 여 Operations Management Suite hello 및 로그 분석 서비스에서 사용 되는 동일한 에이전트인 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-111">Going forward, Security Center uses hello Microsoft Monitoring Agent – this is hello same agent used by hello Operations Management Suite and Log Analytics service.</span></span> <span data-ttu-id="22e38-112">이 에이전트에서 수집 된 데이터는 기존에 저장 *로그 분석* [작업 영역](../log-analytics/log-analytics-manage-access.md) hello VM의 계정 hello 지리적 위치에 Azure 구독 또는 새 중와 연결 된 .</span><span class="sxs-lookup"><span data-stu-id="22e38-112">Data collected from this agent is stored in either an existing *Log Analytics* [workspace](../log-analytics/log-analytics-manage-access.md) associated with your Azure subscription or a new workspace(s), taking into account hello geolocation of hello VM.</span></span>

## <a name="agent"></a><span data-ttu-id="22e38-113">에이전트</span><span class="sxs-lookup"><span data-stu-id="22e38-113">Agent</span></span>

<span data-ttu-id="22e38-114">Hello 전환의 일부로 Microsoft Monitoring Agent hello (에 대 한 [Windows](../log-analytics/log-analytics-windows-agents.md) 또는 [Linux](../log-analytics/log-analytics-linux-agents.md))가 있는 현재 수집 된 데이터는 모든 Azure Vm에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-114">As part of hello transition, hello Microsoft Monitoring Agent (for [Windows](../log-analytics/log-analytics-windows-agents.md) or [Linux](../log-analytics/log-analytics-linux-agents.md)) is installed on all Azure VMs from which data is currently being collected.</span></span>  <span data-ttu-id="22e38-115">VM에 이미 설치 된 Microsoft Monitoring Agent hello hello 보안 센터 현재 hello를 활용 하 여 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-115">If hello VM already has hello Microsoft Monitoring Agent installed, Security Center leverages hello current installed agent.</span></span>

<span data-ttu-id="22e38-116">일정 기간 (일반적으로 몇 일 동안)에 대 한 데이터의 손실 없이 부드러운 전환이 가능해 집니다 에이전트를 모두 함께 tooensure 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-116">For a period of time (typically a few days), both agents will run side by side tooensure a smooth transition without any loss of data.</span></span> <span data-ttu-id="22e38-117">이렇게 하면 Microsoft hello 현재 파이프라인의 사용 중단 하기 전에 새 데이터 파이프라인 hello toovalidate가 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-117">This will enable Microsoft toovalidate that hello new data pipeline is operational before discontinuing use of hello current pipeline.</span></span> <span data-ttu-id="22e38-118">한 번 확인 된 hello Azure 모니터링 에이전트는 Vm에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-118">Once verified, hello Azure Monitoring Agent will be removed from your VMs.</span></span> <span data-ttu-id="22e38-119">사용자 측에서는 아무 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-119">No work is required on your part.</span></span> <span data-ttu-id="22e38-120">모든 고객 마이그레이션되는 경우 전자 메일로 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-120">An email will notify you when all customers have been migrated.</span></span>
 
<span data-ttu-id="22e38-121">보안 데이터에 간격이 발생할 수 hello 마이그레이션 중 hello Azure 모니터링 에이전트를 수동으로 제거 하는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-121">It is not recommended that you manually uninstall hello Azure Monitoring Agent during hello migration as gaps in security data could result.</span></span> <span data-ttu-id="22e38-122">추가 지원이 필요한 경우 [Microsoft 고객 서비스 및 지원 센터](https://support.microsoft.com/contactus/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22e38-122">Please consult [Microsoft Customer Service and Support](https://support.microsoft.com/contactus/) if you need further assistance.</span></span> 

<span data-ttu-id="22e38-123">Microsoft 모니터링 에이전트에 대 한 Windows hello 사용 하 여 TCP 포트 443을 읽이 필요 [Azure 보안 센터 문제 해결 가이드](security-center-troubleshooting-guide.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-123">hello Microsoft Monitoring Agent for Windows requires use TCP port 443, read [Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md) for more information.</span></span>


> [!NOTE] 
> <span data-ttu-id="22e38-124">다른 Azure management에서 hello Microsoft Monitoring Agent를 사용할 수 있으며 서비스를 모니터링, hello 에이전트 제거 되지 것입니다 자동으로 하기 때문에 해제 하면 보안 센터에서 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-124">Because hello Microsoft Monitoring Agent may be used by other Azure management and monitoring services, hello agent will not be uninstalled automatically when you turn off data collection in Security Center.</span></span> <span data-ttu-id="22e38-125">그러나 필요한 경우 hello 에이전트를 제거할 수동으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-125">However, you can manually uninstall hello agent if needed.</span></span>

## <a name="workspace"></a><span data-ttu-id="22e38-126">작업 영역</span><span class="sxs-lookup"><span data-stu-id="22e38-126">Workspace</span></span>

<span data-ttu-id="22e38-127">Microsoft Monitoring Agent (대신 보안 센터)는 기존 로그 분석에 저장 된 hello에서 수집 된 데이터를 이전에 설명한 대로 중 또는 연결 된 Azure 구독 계정 hello를 고려 하는 새 중 hello VM의 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-127">As described previously, data collected from hello Microsoft Monitoring Agent (on behalf of Security Center) are stored in either an existing Log Analytics workspace(s) associated with your Azure subscription or a new workspace(s), taking into account hello geolocation of hello VM.</span></span>

<span data-ttu-id="22e38-128">Azure 포털 hello toosee 보안 센터에서 생성을 포함 하 여, 로그 분석 작업 영역 목록이 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-128">In hello Azure portal, you can browse toosee a list of your Log Analytics workspaces, including any created by Security Center.</span></span> <span data-ttu-id="22e38-129">새 작업 영역에 관련된 리소스 그룹이 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-129">A related resource group will be created for new workspaces.</span></span> <span data-ttu-id="22e38-130">둘 다 다음과 같은 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-130">Both follow this naming convention:</span></span>

- <span data-ttu-id="22e38-131">작업 영역: *DefaultWorkspace-[subscription-ID]-[geo]*</span><span class="sxs-lookup"><span data-stu-id="22e38-131">Workspace: *DefaultWorkspace-[subscription-ID]-[geo]*</span></span>
- <span data-ttu-id="22e38-132">리소스 그룹: *DefaultResouceGroup-[geo]*</span><span class="sxs-lookup"><span data-stu-id="22e38-132">Resource Group: *DefaultResouceGroup-[geo]*</span></span> 
 
<span data-ttu-id="22e38-133">Security Center에서 만든 작업 영역의 경우 데이터는 30일 동안 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-133">For workspaces created by Security Center, data is retained for 30 days.</span></span> <span data-ttu-id="22e38-134">기존 작업 영역에 대 한 보존은 가격 책정 계층 hello 작업 영역을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-134">For existing workspaces, retention is based on hello workspace pricing tier.</span></span>

> [!NOTE]
> <span data-ttu-id="22e38-135">Security Center에서 이전에 수집된 데이터는 Storage 계정에 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-135">Data previously collected by Security Center remains in your Storage account(s).</span></span> <span data-ttu-id="22e38-136">Hello 마이그레이션이 완료 된 후 이러한 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-136">After hello migration is complete, you can delete these Storage accounts.</span></span>

### <a name="oms-security-solution"></a><span data-ttu-id="22e38-137">OMS 보안 솔루션</span><span class="sxs-lookup"><span data-stu-id="22e38-137">OMS Security Solution</span></span> 

<span data-ttu-id="22e38-138">OMS 보안 솔루션을 설치하지 않은 기존 고객의 경우 Microsoft에서는 이를 해당 작업 영역에 설치하고 Azure VM만을 대상으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-138">For existing customers that don’t have OMS Security solution installed, Microsoft is installing it on their workspace, but targeting only Azure VMs.</span></span> <span data-ttu-id="22e38-139">OMS 관리 콘솔에 설치된 경우 자동으로 재구성되지 않으므로 이 솔루션을 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-139">Do not uninstall this solution, as there is no automatic remediation if this is done from OMS management console.</span></span>


## <a name="other-updates"></a><span data-ttu-id="22e38-140">다른 업데이트</span><span class="sxs-lookup"><span data-stu-id="22e38-140">Other updates</span></span>

<span data-ttu-id="22e38-141">Hello 플랫폼 마이그레이션와 함께, 우리 롤아웃하 몇 가지 추가 부분 업데이트:</span><span class="sxs-lookup"><span data-stu-id="22e38-141">In conjunction with hello platform migration, we are rolling out some additional minor updates:</span></span>

- <span data-ttu-id="22e38-142">OS 버전이 추가로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-142">Additional OS versions will be supported.</span></span> <span data-ttu-id="22e38-143">Hello 사항은 [여기](security-center-faq.md#virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-143">See hello list [here](security-center-faq.md#virtual-machines).</span></span>
- <span data-ttu-id="22e38-144">OS 취약점 hello 목록이 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-144">hello list of OS vulnerabilities will be expanded.</span></span> <span data-ttu-id="22e38-145">Hello 사항은 [여기](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-145">See hello list [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
- <span data-ttu-id="22e38-146">[가격 책정](https://azure.microsoft.com/pricing/details/security-center/)은 매시간(이전에는 매일) 비례 배분되며, 이로 인해 일부 고객의 비용이 절감될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-146">[Pricing](https://azure.microsoft.com/pricing/details/security-center/) will be pro-rated hourly (previously it was daily), which will result in cost savings for some customers.</span></span>
- <span data-ttu-id="22e38-147">데이터 수집 필요한 되며 hello 표준 가격 책정 계층에는 고객에 대 한 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-147">Data Collection will be required and automatically enabled for customers on hello Standard pricing tier.</span></span>
- <span data-ttu-id="22e38-148">Azure Security Center는 Azure 확장을 통해 배포되지 않은 맬웨어 방지 솔루션을 검색하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-148">Azure Security Center will begin discovering antimalware solutions that were not deployed via Azure extensions.</span></span> <span data-ttu-id="22e38-149">Symantec Endpoint Protection 검색 및 Windows 2016용 Defender를 먼저 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22e38-149">Discovery of Symantec Endpoint Protection and Defender for Windows 2016 will be available first.</span></span>
- <span data-ttu-id="22e38-150">방지 정책 및 알림은 hello에서 구성할 수만 *구독* 수준인 최소화 되지만 가격 여전히 hello에서 설정할 수 *리소스 그룹* 수준</span><span class="sxs-lookup"><span data-stu-id="22e38-150">Prevention policies and notifications are only configurable at hello *Subscription* level, but pricing can still be set at hello *Resource Group* level</span></span>

