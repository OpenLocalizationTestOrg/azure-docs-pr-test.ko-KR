---
title: "Azure Security Center에서 차세대 방화벽 추가 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **차세대 방화벽 추가** 및 **NGFW를 통해서만 트래픽 라우팅**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 30589d0a943517c03394a3aae7c03c8094e78c1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="ebefd-103">Azure 보안 센터에서 차세대 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="ebefd-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="ebefd-104">Azure Security Center에서는 보안 보호를 증가시키기 위해 Microsoft 파트너의 차세대 방화벽(NGFW)을 추가하도록 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="ebefd-105">이 문서에서는 이를 수행하는 방법의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="ebefd-106">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ebefd-107">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ebefd-108">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="ebefd-108">Implement the recommendation</span></span>
1. <span data-ttu-id="ebefd-109">**권장 사항** 블레이드에서 **차세대 방화벽 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="ebefd-110">![차세대 방화벽 추가][1]</span><span class="sxs-lookup"><span data-stu-id="ebefd-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="ebefd-111">**차세대 방화벽 추가** 블레이드에서 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="ebefd-112">![끝점 선택][2]</span><span class="sxs-lookup"><span data-stu-id="ebefd-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="ebefd-113">두 번째 **차세대 방화벽 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="ebefd-114">새 솔루션을 사용할 수 있거나 만들 수 있는 경우 기존 솔루션을 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="ebefd-115">이 예제에서는 사용할 수 있는 기존 솔루션이 없으므로 NGFW를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="ebefd-116">![차세대 방화벽 만들기][3]</span><span class="sxs-lookup"><span data-stu-id="ebefd-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="ebefd-117">NGFW를 만들려면 통합 파트너 목록에서 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="ebefd-118">이 예제에서는 **검사점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="ebefd-119">![차세대 방화벽 솔루션 선택][4]</span><span class="sxs-lookup"><span data-stu-id="ebefd-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="ebefd-120">파트너 솔루션에 대한 정보를 제공하는 **검사점** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="ebefd-121">정보 블레이드에서 **만들기** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="ebefd-122">![방화벽 정보 블레이드][5]</span><span class="sxs-lookup"><span data-stu-id="ebefd-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="ebefd-123">**가상 컴퓨터 만들기** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="ebefd-124">여기서 NGFW를 실행하는 VM(가상 컴퓨터)을 스핀업하는 데 필요한 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="ebefd-125">단계를 수행하고 필요한 NGFW 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="ebefd-126">적용하려면 확인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-126">Select OK to apply.</span></span>
   <span data-ttu-id="ebefd-127">![NGFW를 실행하기 위해 가상 컴퓨터 만들기][6]</span><span class="sxs-lookup"><span data-stu-id="ebefd-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="ebefd-128">NGFW를 통해서만 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="ebefd-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="ebefd-129">**권장 사항** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="ebefd-130">Security Center를 통해 NGFW를 추가한 후 **NGFW를 통해서만 트래픽 라우팅**이라는 새 항목이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="ebefd-131">이 권장 사항은 보안 센터를 통해 NGFW를 설치한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="ebefd-132">인터넷 끝점이 있는 경우 Security Center는 NGFW를 통해 인바운드 트래픽을 VM으로 강제하는 네트워크 보안 그룹 규칙을 구성할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="ebefd-133">**권장 사항 블레이드**에서 **NGFW를 통해서만 트래픽 라우팅**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="ebefd-134">![NGFW를 통해서만 트래픽 라우팅][7]</span><span class="sxs-lookup"><span data-stu-id="ebefd-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="ebefd-135">트래픽을 라우팅할 수 있는 VM을 나열하는 **NGFW를 통해서만 트래픽 라우팅** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="ebefd-136">목록에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-136">Select a VM from the list.</span></span>
   <span data-ttu-id="ebefd-137">![VM 선택][8]</span><span class="sxs-lookup"><span data-stu-id="ebefd-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="ebefd-138">선택된 VM에 대한 블레이드가 열리고 관련 인바운드 규칙을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="ebefd-139">설명은 가능한 다음 단계에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="ebefd-140">**인바운드 규칙 편집** 을 선택하여 인바운드 규칙 편집을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="ebefd-141">NGFW로 연결된 인터넷 연결 끝점의 경우 **원본**이 **모두**로 설정되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="ebefd-142">인바운드 규칙의 속성에 대해 자세히 알아보려면 [NSG 규칙](../virtual-network/virtual-networks-nsg.md#nsg-rules)을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="ebefd-143">![액세스를 제한하는 규칙 구성][9]
   ![인바운드 규칙 편집][10]</span><span class="sxs-lookup"><span data-stu-id="ebefd-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="ebefd-144">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ebefd-144">See also</span></span>
<span data-ttu-id="ebefd-145">이 문서에서는 보안 센터 권장 사항 "차세대 방화벽 추가"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="ebefd-146">NGFW 및 검사점 파트너 솔루션에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebefd-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="ebefd-147">차세대 방화벽</span><span class="sxs-lookup"><span data-stu-id="ebefd-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="ebefd-148">검사점 vSEC</span><span class="sxs-lookup"><span data-stu-id="ebefd-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="ebefd-149">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebefd-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ebefd-150">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="ebefd-151">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ebefd-152">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ebefd-153">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ebefd-154">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ebefd-155">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ebefd-156">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ebefd-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
