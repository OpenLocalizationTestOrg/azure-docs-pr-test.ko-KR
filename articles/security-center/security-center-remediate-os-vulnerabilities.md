---
title: "Azure 보안 센터에서 운영 체제 aaaRemediate 취약성 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 수정 OS 취약점 * *입니다."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="2fd2c-103">Azure 보안 센터에서 OS 취약성 해결</span><span class="sxs-lookup"><span data-stu-id="2fd2c-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="2fd2c-104">Azure 보안 센터를 분석 하 여 매일 가상 컴퓨터 (VM) 운영 체제 (OS) 만들 수 있는 구성이 hello VM에 대 한 으로부터 더 취약 tooattack 하 고 권장 구성이 tooaddress 이러한 취약점을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="2fd2c-105">보안 센터는 VM의 OS 구성 권장 구성 규칙 hello 일치 하지 않는 경우 보안 문제를 해결 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="2fd2c-106">모니터링 되 고 hello 특정 구성에 대 한 자세한 내용은 참조 hello [권장 되는 구성 규칙 목록이](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="2fd2c-107">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="2fd2c-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="2fd2c-108">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="2fd2c-109">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="2fd2c-110">Hello에 **권장 사항을** 블레이드를 **재구성 OS 취약점**합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="2fd2c-111">![OS 취약성 해결][1]</span><span class="sxs-lookup"><span data-stu-id="2fd2c-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="2fd2c-112">hello **재구성 OS 취약점** 블레이드 열리고 권장 구성 규칙 hello와 일치 하지 않는 운영 체제 구성으로 Vm을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="2fd2c-113">각 VM에 대 한 hello 블레이드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="2fd2c-114">**못했습니다 규칙** -실패 한 hello 수 hello VM의 OS 구성 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="2fd2c-115">**마지막 검사 시간** --hello 날짜 및 시간을 보안 센터 마지막으로 검색 한 hello VM의 OS 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="2fd2c-116">**상태** -hello hello 취약점의 현재 상태:</span><span class="sxs-lookup"><span data-stu-id="2fd2c-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="2fd2c-117">열기: hello 취약점에 처리 되지 아직</span><span class="sxs-lookup"><span data-stu-id="2fd2c-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="2fd2c-118">진행: hello 취약점은 현재 적용 되 고, 사용자가 아무 작업도 필요</span><span class="sxs-lookup"><span data-stu-id="2fd2c-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="2fd2c-119">확인할: hello 취약점이 이미 해결 (hello 문제가 해결 되 면 hello 항목은 회색으로 표시)</span><span class="sxs-lookup"><span data-stu-id="2fd2c-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="2fd2c-120">**심각도** -모든 취약성이 설정 low tooa 심각도 즉 취약점을 해결 해야 하지만 즉각적인 주의가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="2fd2c-121">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-121">Select a VM.</span></span> <span data-ttu-id="2fd2c-122">해당 블레이드 VM 열리고 실패 한 hello 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="2fd2c-123">![실패한 구성 규칙][2]</span><span class="sxs-lookup"><span data-stu-id="2fd2c-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="2fd2c-124">규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-124">Select a rule.</span></span> <span data-ttu-id="2fd2c-125">이 예제에서는 **암호는 복잡성 조건을 만족해야 함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="2fd2c-126">블레이드 설명 하는 hello 실패 규칙 및 hello에 미치는 영향을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="2fd2c-127">Hello 세부 정보를 검토 하 고 운영 체제 구성이 적용 되는 방법을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="2fd2c-128">![Hello에 대 한 실패 규칙][3]</span><span class="sxs-lookup"><span data-stu-id="2fd2c-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="2fd2c-129">보안 센터 구성 규칙에 대 한 일반적인 구성 열거형 CCE () tooassign 고유 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="2fd2c-130">다음 정보는 hello이이 블레이드에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="2fd2c-131">이름 -- 규칙의 이름</span><span class="sxs-lookup"><span data-stu-id="2fd2c-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="2fd2c-132">심각도 -- CCE 심각도 값, 즉 요주의, 중요 또는 경고</span><span class="sxs-lookup"><span data-stu-id="2fd2c-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="2fd2c-133">CCE CCIED-hello 규칙에 대 한 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="2fd2c-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="2fd2c-134">설명 -- 규칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="2fd2c-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="2fd2c-135">취약성 -- 규칙이 적용되지 않은 경우 취약성 또는 위험에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="2fd2c-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="2fd2c-136">영향 -- 규칙이 적용될 때 비즈니스 영향</span><span class="sxs-lookup"><span data-stu-id="2fd2c-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="2fd2c-137">예상 값-값이 보안 센터 hello 규칙에 대해 VM OS 구성을 분석할 때 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2fd2c-138">Hello 규칙에 대해 VM OS 구성의 분석 하는 동안 보안 센터에서 사용 되는 규칙 작업-규칙 작업</span><span class="sxs-lookup"><span data-stu-id="2fd2c-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2fd2c-139">Hello 규칙에 대해 VM OS 구성의 분석 한 후 반환 된 값을 실제 값-</span><span class="sxs-lookup"><span data-stu-id="2fd2c-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2fd2c-140">평가 결과 –- 분석 결과: 통과, 실패</span><span class="sxs-lookup"><span data-stu-id="2fd2c-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="2fd2c-141">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2fd2c-141">See also</span></span>
<span data-ttu-id="2fd2c-142">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "재구성 OS 취약점입니다."</span><span class="sxs-lookup"><span data-stu-id="2fd2c-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="2fd2c-143">Hello 규칙 집합을 구성을 검토할 수 있습니다 [여기](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335)합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="2fd2c-144">보안 센터 CCE (Common Configuration Enumeration) tooassign 고유 식별자를 사용 하 여 구성 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="2fd2c-145">Hello 방문 [CCE](https://nvd.nist.gov/cce/index.cfm) 자세한 정보에 대 한 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="2fd2c-146">보안 센터에 대해 자세히 toolearn hello 다음 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="2fd2c-147">[Azure Security Center에서 지원되는 플랫폼](security-center-os-coverage.md) - 지원되는 Windows 및 Linux VM의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="2fd2c-148">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2fd2c-149">[Azure Security Center에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2fd2c-150">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2fd2c-151">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2fd2c-152">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="2fd2c-153">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2fd2c-154">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2fd2c-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
