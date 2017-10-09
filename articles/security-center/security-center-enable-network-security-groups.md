---
title: "Azure 보안 센터의 네트워크 보안 그룹 aaaEnable | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * *를 사용 하도록 설정 네트워크 보안 그룹 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="ee724-103">Azure 보안 센터의 네트워크 보안 그룹 활성화</span><span class="sxs-lookup"><span data-stu-id="ee724-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="ee724-104">Azure Security Center는 아직 활성화되지 않은 경우 NSG(네트워크 보안 그룹)를 활성화하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="ee724-105">Nsg에 허용 하거나 거부할 네트워크 트래픽을 가상 네트워크에서 VM 인스턴스 tooyour 하는 액세스 제어 목록 (ACL) 규칙의 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="ee724-106">NSG는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="ee724-107">NSG를 서브넷과 연결 하는 경우 해당 서브넷에 tooall hello VM 인스턴스 hello ACL 규칙에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="ee724-108">또한 트래픽 tooan 개별 VM을 제한할 수 NSG를 연결 하 여 추가 VM toothat 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="ee724-109">toolearn 더 참조 [는 보안 그룹 NSG (네트워크) 이란?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="ee724-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="ee724-110">보안 센터 두 가지 권장 사항 tooyou 제공 활성화 Nsg가: 가상 컴퓨터에서 네트워크 보안 그룹을 사용 하도록 설정 하 고 서브넷에 네트워크 보안 그룹을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="ee724-111">어떤 수준, 서브넷 또는 VM에 Nsg tooapply 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="ee724-112">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="ee724-113">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ee724-114">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="ee724-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="ee724-115">Hello에 **권장 사항을** 블레이드를 **네트워크 보안 그룹 사용** 가상 컴퓨터 또는 서브넷에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="ee724-116">![네트워크 보안 그룹 활성화][1]</span><span class="sxs-lookup"><span data-stu-id="ee724-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="ee724-117">Hello 블레이드가 열립니다 **누락 된 네트워크 보안 그룹 구성** 서브넷에 대 한 또는 선택한 hello 권장 사항에 따라 가상 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="ee724-118">서브넷 또는 가상 컴퓨터 tooconfigure NSG 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![서브넷에 대한 NSG 구성][2]

   ![VM에 대한 NSG 구성][3]
3. <span data-ttu-id="ee724-121">Hello에 **네트워크 보안 그룹 선택** 블레이드에서 기존 NSG를 선택 하거나 선택 **새로 만들기** toocreate NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![네트워크 보안 그룹 선택][4]

<span data-ttu-id="ee724-123">NSG를 만들면 hello 단계에 따라 [어떻게 toomanage Nsg를 사용 하 여 Azure 포털을 hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate NSG 보안 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="ee724-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ee724-124">See also</span></span>
<span data-ttu-id="ee724-125">이 문서는 어떻게 tooimplement hello 보안 센터 권장 사항 "네트워크 보안 그룹 사용" 서브넷 또는 가상 컴퓨터에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="ee724-126">Nsg를 사용에 대 한 더 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="ee724-127">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="ee724-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="ee724-128">Toomanage Nsg를 사용 하 여 Azure 포털을 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ee724-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="ee724-129">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ee724-130">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ee724-131">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ee724-132">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ee724-133">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ee724-134">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ee724-135">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ee724-136">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ee724-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
