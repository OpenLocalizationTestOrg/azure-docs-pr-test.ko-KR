---
title: "Azure 보안 센터에서 다음 세대 방화벽 aaaAdd | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 추가 된 다음 생성 방화벽 * 및 * * 경로 트래픽을 통해 NGFW만 * * 합니다."
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
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="b4648-103">Azure 보안 센터에서 차세대 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="b4648-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="b4648-104">Azure 보안 센터를 추가한 다음 세대 방화벽 (NGFW)에서 Microsoft 파트너 tooincrease 보안 보호를 권장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="b4648-105">이 문서 과정을 안내 하는 방법의 예 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="b4648-106">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="b4648-107">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b4648-108">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="b4648-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="b4648-109">Hello에 **권장 사항을** 블레이드를 **다음 세대 방화벽을 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="b4648-110">![차세대 방화벽 추가][1]</span><span class="sxs-lookup"><span data-stu-id="b4648-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="b4648-111">Hello에 **다음 세대 방화벽을 추가할** 블레이드에서 끝점을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="b4648-112">![끝점 선택][2]</span><span class="sxs-lookup"><span data-stu-id="b4648-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="b4648-113">두 번째 **차세대 방화벽 추가** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="b4648-114">선택할 수 있습니다 toouse 기존 솔루션 사용 가능한 경우 또는 새를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="b4648-115">이 예제에서는 사용할 수 있는 기존 솔루션이 없으므로 NGFW를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="b4648-116">![차세대 방화벽 만들기][3]</span><span class="sxs-lookup"><span data-stu-id="b4648-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="b4648-117">NGFW toocreate hello 통합된 파트너 목록에서 솔루션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="b4648-118">이 예제에서는 **검사점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="b4648-119">![차세대 방화벽 솔루션 선택][4]</span><span class="sxs-lookup"><span data-stu-id="b4648-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="b4648-120">hello **검사점** 블레이드에서 열립니다 hello 업체 솔루션에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="b4648-121">선택 **만들기** hello 정보 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="b4648-122">![방화벽 정보 블레이드][5]</span><span class="sxs-lookup"><span data-stu-id="b4648-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="b4648-123">hello **가상 컴퓨터를 만들** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="b4648-124">여기서 실행 하는 가상 컴퓨터 (VM)를 필요한 toospin hello NGFW 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="b4648-125">Hello 단계를 수행 하 고 필요한 hello NGFW 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="b4648-126">확인 tooapply를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-126">Select OK tooapply.</span></span>
   <span data-ttu-id="b4648-127">![가상 컴퓨터 toorun NGFW 만들기][6]</span><span class="sxs-lookup"><span data-stu-id="b4648-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="b4648-128">NGFW를 통해서만 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="b4648-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="b4648-129">Toohello 반환 **권장 사항을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="b4648-130">Security Center를 통해 NGFW를 추가한 후 **NGFW를 통해서만 트래픽 라우팅**이라는 새 항목이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="b4648-131">이 권장 사항은 보안 센터를 통해 NGFW를 설치한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="b4648-132">인터넷 연결 끝점의 경우 보안 센터 인바운드 트래픽을 tooyour 프로그램 NGFW 통해 VM을 강제 하는 네트워크 보안 그룹 규칙을 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="b4648-133">Hello에 **권장 사항 블레이드에서**선택, **만 NGFW 트래픽을 라우팅하**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="b4648-134">![NGFW를 통해서만 트래픽 라우팅][7]</span><span class="sxs-lookup"><span data-stu-id="b4648-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="b4648-135">Hello 블레이드가 열립니다 **만 NGFW 트래픽을 라우팅하**에 대 한 트래픽을 라우팅할 수 있는 Vm을 나열 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="b4648-136">Hello 목록에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="b4648-137">![VM 선택][8]</span><span class="sxs-lookup"><span data-stu-id="b4648-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="b4648-138">Hello에 대 한 블레이드 선택한 VM가 열리고 관련된 인바운드 규칙을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="b4648-139">설명은 가능한 다음 단계에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="b4648-140">선택 **인바운드 규칙을 편집할** tooproceed는 인바운드 규칙을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="b4648-141">hello 예상은 **소스** 너무 설정 하지 않으면**모든** 로 연결 된 hello 인터넷 연결 끝점에 대 한 hello NGFW 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="b4648-142">hello 인바운드 규칙의 hello 속성에 대해 자세히 toolearn 참조 [NSG 규칙](../virtual-network/virtual-networks-nsg.md#nsg-rules)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="b4648-143">![규칙 toolimit 액세스 구성][9]
   ![인바운드 규칙 편집][10]</span><span class="sxs-lookup"><span data-stu-id="b4648-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="b4648-144">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b4648-144">See also</span></span>
<span data-ttu-id="b4648-145">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "" 다음 세대 방화벽 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="b4648-146">NGFWs 및 hello 검사점 업체 솔루션에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="b4648-147">차세대 방화벽</span><span class="sxs-lookup"><span data-stu-id="b4648-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="b4648-148">검사점 vSEC</span><span class="sxs-lookup"><span data-stu-id="b4648-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="b4648-149">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b4648-150">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="b4648-151">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b4648-152">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b4648-153">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b4648-154">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b4648-155">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b4648-156">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4648-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
