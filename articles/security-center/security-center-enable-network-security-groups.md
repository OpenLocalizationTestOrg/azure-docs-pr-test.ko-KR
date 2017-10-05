---
title: "Azure Security Center의 네트워크 보안 그룹 활성화 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **네트워크 보안 그룹 활성화**를 구현하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="d1dff-103">Azure 보안 센터의 네트워크 보안 그룹 활성화</span><span class="sxs-lookup"><span data-stu-id="d1dff-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="d1dff-104">Azure Security Center는 아직 활성화되지 않은 경우 NSG(네트워크 보안 그룹)를 활성화하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="d1dff-105">NSG는 ACL(액세스 제어 목록)의 가상 네트워크에 VM 인스턴스에 대한 허용 또는 거부 네트워크 트래픽 규칙의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="d1dff-106">Nsg는 서브넷 또는 서브넷 내의 개별 VM 인스턴스 중 하나와 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="d1dff-107">NSG를 서브넷과 연결한 경우 ACL 규칙은 해당 서브넷에 있는 모든 VM 인스턴스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="d1dff-108">또한 개별 VM에 대한 트래픽은 해당 VM에 직접 NSG를 연결하여 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="d1dff-109">자세한 내용은 [NSG(네트워크 보안 그룹)란?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="d1dff-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="d1dff-110">NSG를 활성화하지 않은 경우 Security Center는 서브넷에서 네트워크 보안 그룹 활성화 및 가상 컴퓨터에서 네트워크 보안 그룹 활성화라는 두 가지 권장 사항을 제시합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="d1dff-111">NSG를 적용할 수준, 서브넷 또는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="d1dff-112">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="d1dff-113">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="d1dff-114">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="d1dff-114">Implement the recommendation</span></span>
1. <span data-ttu-id="d1dff-115">**권장 사항** 블레이드의 서브넷 또는 가상 컴퓨터에서 **네트워크 보안 그룹 활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="d1dff-116">![네트워크 보안 그룹 활성화][1]</span><span class="sxs-lookup"><span data-stu-id="d1dff-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="d1dff-117">이렇게 하면 선택한 권장 사항에 따라 서브넷 또는 가상 컴퓨터에 대한 **누락된 네트워크 보안 그룹 구성** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="d1dff-118">NSG를 구성할 서브넷 또는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![서브넷에 대한 NSG 구성][2]

   ![VM에 대한 NSG 구성][3]
3. <span data-ttu-id="d1dff-121">**네트워크 보안 그룹 선택** 블레이드에서 기존 NSG를 선택하거나 **새로 만들기**를 선택하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![네트워크 보안 그룹 선택][4]

<span data-ttu-id="d1dff-123">NSG를 만드는 경우 [Azure Portal을 사용하여 NSG를 관리하는 방법](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)의 단계에 따라 NSG를 만들고 보안 규칙을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="d1dff-124">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d1dff-124">See also</span></span>
<span data-ttu-id="d1dff-125">이 문서에서는 보안 센터 권장 사항 서브넷 또는 가상 컴퓨터에 대한 "네트워크 보안 그룹 활성화"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="d1dff-126">NSG 활성화에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1dff-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="d1dff-127">NSG(네트워크 보안 그룹)란?</span><span class="sxs-lookup"><span data-stu-id="d1dff-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="d1dff-128">Azure 포털을 사용하여 NSG 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1dff-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="d1dff-129">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1dff-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d1dff-130">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d1dff-131">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d1dff-132">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d1dff-133">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d1dff-134">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d1dff-135">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d1dff-136">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1dff-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
