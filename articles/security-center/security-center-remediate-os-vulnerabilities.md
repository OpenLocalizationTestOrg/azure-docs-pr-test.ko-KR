---
title: "Azure Security Center에서 OS 취약성 해결 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **OS 취약성 해결**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="c70cb-103">Azure 보안 센터에서 OS 취약성 해결</span><span class="sxs-lookup"><span data-stu-id="c70cb-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="c70cb-104">Azure 보안 센터는 매일 가상 컴퓨터(VM) 운영 체제(OS)를 분석하여 VM을 공격에 더 취약하게 만들 수 있는 구성을 찾고 이러한 취약성을 해결하기 위한 구성 변경을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="c70cb-105">Security Center는 VM의 OS 구성이 권장 구성 규칙과 일치하지 않는 경우 취약성 해결을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="c70cb-106">모니터링되는 특정 구성에 대한 자세한 내용은 [권장 구성 규칙 목록](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c70cb-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c70cb-107">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="c70cb-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="c70cb-108">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c70cb-109">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="c70cb-110">**권장 사항** 블레이드에서 **OS 취약성 해결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="c70cb-111">![OS 취약성 해결][1]</span><span class="sxs-lookup"><span data-stu-id="c70cb-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="c70cb-112">**OS 취약성 해결** 블레이드가 열리고 권장 구성 규칙과 일치하지 않는 OS 구성이 있는 VM이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="c70cb-113">각 VM에 대해 블레이드에서 다음을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="c70cb-114">**실패한 규칙** -- VM의 OS 구성이 실패한 규칙 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="c70cb-115">**마지막 검사 시간** : 보안 센터가 VM을 마지막으로 검사한 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="c70cb-116">**상태** : 권장 사항의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="c70cb-117">열기: 취약성이 아직 해결되지 않음</span><span class="sxs-lookup"><span data-stu-id="c70cb-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="c70cb-118">진행 중: 취약성이 현재 적용되고 있으며 아무런 작업도 수행할 필요가 없음</span><span class="sxs-lookup"><span data-stu-id="c70cb-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="c70cb-119">해결됨: 취약성이 이미 해결됨(문제가 해결되면 항목이 회색으로 표시됨)</span><span class="sxs-lookup"><span data-stu-id="c70cb-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="c70cb-120">**심각도** - 모든 취약성이 낮음 심각도로 설정됩니다. 즉, 취약성을 해결해야 하지만 즉시 주의할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="c70cb-121">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-121">Select a VM.</span></span> <span data-ttu-id="c70cb-122">해당 VM에 대한 블레이드가 열리고 실패한 규칙이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="c70cb-123">![실패한 구성 규칙][2]</span><span class="sxs-lookup"><span data-stu-id="c70cb-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="c70cb-124">규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-124">Select a rule.</span></span> <span data-ttu-id="c70cb-125">이 예제에서는 **암호는 복잡성 조건을 만족해야 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="c70cb-126">실패한 규칙 및 영향을 설명하는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="c70cb-127">세부 정보를 검토하고 운영 체제 구성을 적용할 방법을 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="c70cb-128">![실패한 규칙에 대한 설명][3]</span><span class="sxs-lookup"><span data-stu-id="c70cb-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="c70cb-129">보안 센터는 일반 구성 열거형(CCE)을 사용하여 구성 규칙에 대한 고유 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="c70cb-130">이 블레이드에 다음과 같은 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="c70cb-131">이름 -- 규칙의 이름</span><span class="sxs-lookup"><span data-stu-id="c70cb-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="c70cb-132">심각도 -- CCE 심각도 값, 즉 요주의, 중요 또는 경고</span><span class="sxs-lookup"><span data-stu-id="c70cb-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="c70cb-133">CCIED -- 규칙에 대한 CCE 고유 ID</span><span class="sxs-lookup"><span data-stu-id="c70cb-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="c70cb-134">설명 -- 규칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="c70cb-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="c70cb-135">취약성 -- 규칙이 적용되지 않은 경우 취약성 또는 위험에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="c70cb-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="c70cb-136">영향 -- 규칙이 적용될 때 비즈니스 영향</span><span class="sxs-lookup"><span data-stu-id="c70cb-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="c70cb-137">예상 값 -- 보안 센터가 규칙을 기준으로 VM OS 구성을 분석할 때 예상되는 값</span><span class="sxs-lookup"><span data-stu-id="c70cb-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="c70cb-138">규칙 작업 -- 규칙을 기준으로 VM OS 구성을 분석하는 동안 보안 센터가 사용하는 규칙 작업</span><span class="sxs-lookup"><span data-stu-id="c70cb-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="c70cb-139">실제 값 -- 규칙을 기준으로 VM OS 구성을 분석한 후 반환되는 값</span><span class="sxs-lookup"><span data-stu-id="c70cb-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="c70cb-140">평가 결과 –- 분석 결과: 통과, 실패</span><span class="sxs-lookup"><span data-stu-id="c70cb-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="c70cb-141">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c70cb-141">See also</span></span>
<span data-ttu-id="c70cb-142">이 문서에서는 보안 센터 권장 사항 "OS 취약성 해결"을 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="c70cb-143">[여기](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)서 구성 규칙 집합을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="c70cb-144">보안 센터는 일반 구성 열거형(CCE)을 사용하여 구성 규칙에 대한 고유 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="c70cb-145">자세한 내용은 [CCE](https://nvd.nist.gov/cce/index.cfm) 사이트를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c70cb-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="c70cb-146">Security Center에 대해 알아보려면 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c70cb-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="c70cb-147">[Azure Security Center에서 지원되는 플랫폼](security-center-os-coverage.md) - 지원되는 Windows 및 Linux VM의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="c70cb-148">[Azure Security Center에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c70cb-149">[Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c70cb-150">[Azure Security Center에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c70cb-151">[Azure Security Center에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c70cb-152">[Azure Security Center를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) - 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c70cb-153">[Azure Security Center FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c70cb-154">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c70cb-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
