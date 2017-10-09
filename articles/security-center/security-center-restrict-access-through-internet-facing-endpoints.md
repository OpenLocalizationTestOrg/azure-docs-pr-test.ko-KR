---
title: "Azure 보안 센터에서 인터넷 연결 끝점을 통해 aaaRestrict 액세스 | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 인터넷 끝점 * * 연결을 통해 액세스를 제한 합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="a0d72-103">Azure 보안 센터에서 인터넷 끝점을 x통한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="a0d72-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="a0d72-104">Azure 보안 센터는 네트워크 보안 그룹(NSG)에 "임의" 원본 IP 주소에서 액세스할 수 있도록 하는 인바운드 규칙이 하나 이상 있는 경우 인터넷 끝점을 통한 액세스를 제한할 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="a0d72-105">액세스를 너무 "any" 열기 설정할 공격자가 tooaccess 리소스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="a0d72-106">보안 센터는 이러한 인바운드 규칙 toorestrict 액세스 toosource IP 주소 실제로 액세스 해야 하는 편집 하는 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="a0d72-107">이 권장 사항은 "어떤 항목도" 원본으로 사용할 수 있는 웹이 아닌 모든 포트에 대해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="a0d72-108">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="a0d72-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="a0d72-110">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="a0d72-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="a0d72-111">Hello에 **권장 사항 블레이드에서**선택, **인터넷 연결 끝점을 통해 액세스를 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![인터넷 끝점을 통한 액세스 제한][1]
2. <span data-ttu-id="a0d72-113">Hello 블레이드가 열립니다 **인터넷 연결 끝점을 통해 액세스를 제한**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="a0d72-114">이 블레이드는 잠재적인 보안 문제가 만들 하는 인바운드 규칙으로 hello 가상 컴퓨터 (Vm)를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="a0d72-115">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-115">Select a VM.</span></span>

   ![VM 선택][2]
3. <span data-ttu-id="a0d72-117">hello **NSG** 블레이드 네트워크 보안 그룹 정보를 관련된 인바운드 규칙을 표시 하 고 hello VM에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="a0d72-118">선택 **인바운드 규칙을 편집할** tooproceed는 인바운드 규칙을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![네트워크 보안 그룹 블레이드][3]
4. <span data-ttu-id="a0d72-120">Hello에 **인바운드 보안 규칙** 블레이드 선택 hello 인바운드 규칙 tooedit 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="a0d72-121">이 예제에서는 **AllowWeb**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-121">In this example, let’s select **AllowWeb**.</span></span>

   ![인바운드 보안 규칙][4]

   <span data-ttu-id="a0d72-123">참고를 선택할 수도 있습니다 **규칙 기본** toosee hello 집합이 모든 Nsg에 포함 된 기본 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="a0d72-124">hello 기본 규칙 삭제할 수 없지만 만드는 hello 규칙에 의해 재정의할 수 이들이 낮은 우선 순위를 할당 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="a0d72-125">[규칙 기본](../virtual-network/virtual-networks-nsg.md#default-rules)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a0d72-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![기본 규칙][5]
5. <span data-ttu-id="a0d72-127">Hello에 **AllowWeb** 하는 hello 하므로 인바운드 규칙 hello의 편집 hello 속성 블레이드에서 **소스** 는 IP 주소 또는 IP 주소 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="a0d72-128">hello 인바운드 규칙의 hello 속성에 대해 자세히 toolearn 참조 [NSG 규칙](../virtual-network/virtual-networks-nsg.md#nsg-rules)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![인바운드 규칙 편집][6]

## <a name="see-also"></a><span data-ttu-id="a0d72-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a0d72-130">See also</span></span>
<span data-ttu-id="a0d72-131">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 사항 "액세스 제한에도 인터넷 연결 끝점을 통해 합니다."</span><span class="sxs-lookup"><span data-stu-id="a0d72-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="a0d72-132">Nsg와 규칙을 사용 하도록 설정에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="a0d72-133">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="a0d72-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="a0d72-134">Toomanage Nsg를 사용 하 여 Azure 포털을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a0d72-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="a0d72-135">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="a0d72-136">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a0d72-137">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a0d72-138">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="a0d72-139">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="a0d72-140">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="a0d72-141">[Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="a0d72-142">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a0d72-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
