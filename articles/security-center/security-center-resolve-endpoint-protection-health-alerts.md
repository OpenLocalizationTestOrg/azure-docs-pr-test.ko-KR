---
title: "Azure Security Center에서 Endpoint Protection 상태 경고 해결| Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **Endpoint Protection 상태 경고 해결**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 5e6b136d6bd3b11fb82126d104fd0cb149255118
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="89c69-103">Azure 보안 센터에서 Endpoint Protection 상태 경고 해결</span><span class="sxs-lookup"><span data-stu-id="89c69-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="89c69-104">Azure 보안 센터는 검색된 Endpoint Protection 상태 경고를 해결할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="89c69-105">보안 센터에서 Endpoint Protection 오류가 있는 가상 컴퓨터(VM) 및 오류 횟수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="89c69-106">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="89c69-107">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="89c69-108">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="89c69-108">Implement the recommendation</span></span>
1. <span data-ttu-id="89c69-109">**권장 사항 블레이드**에서 **Endpoint Protection 상태 경고 해결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="89c69-110">![Endpoint Protection 상태 경고 해결][1]</span><span class="sxs-lookup"><span data-stu-id="89c69-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="89c69-111">오류가 있는 VM 및 각 VM에 대한 오류 횟수를 나열하는 **Endpoint Protection 오류** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="89c69-112">목록에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-112">Select a VM from the list.</span></span>
   <span data-ttu-id="89c69-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="89c69-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="89c69-114">선택한 VM에 대해 오류 목록을 표시하는 **오류 목록** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="89c69-115">자세한 내용을 알아보려면 목록에서 오류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="89c69-116">선택한 오류에 대한 정보가 포함된 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="89c69-117">![오류 목록][3]
   ![오류 이벤트][4]</span><span class="sxs-lookup"><span data-stu-id="89c69-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="89c69-118">참고 항목</span><span class="sxs-lookup"><span data-stu-id="89c69-118">See also</span></span>
<span data-ttu-id="89c69-119">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89c69-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="89c69-120">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="89c69-121">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="89c69-122">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)--Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="89c69-123">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)--보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="89c69-124">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="89c69-125">[Azure 보안 센터 FAQ](security-center-faq.md)--서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="89c69-126">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="89c69-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
