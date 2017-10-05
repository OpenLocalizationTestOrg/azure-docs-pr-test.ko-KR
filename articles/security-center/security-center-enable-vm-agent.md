---
title: "Azure Security Center에서 VM 에이전트 사용 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **VM 에이전트 사용** 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="1c284-103">Azure 보안 센터에서 VM 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="1c284-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="1c284-104">[데이터 컬렉션을 사용하도록 설정](security-center-enable-data-collection.md)하려면 VM(가상 컴퓨터)에 VM 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="1c284-105">Azure 보안 센터에서 VM 에이전트가 필요한 VM을 확인하고 해당 VM에서 VM 에이전트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="1c284-106">Azure 마켓플레이스에서 배포된 VM에 VM 에이전트가 기본적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="1c284-107">[VM 에이전트 및 확장 - 2부](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) 문서에 VM 에이전트 설치 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="1c284-108">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="1c284-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="1c284-110">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="1c284-110">Implement the recommendation</span></span>
1. <span data-ttu-id="1c284-111">**권장 사항 블레이드**에서 **VM 에이전트 활성화**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="1c284-112">![VM 에이전트 사용][1]</span><span class="sxs-lookup"><span data-stu-id="1c284-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="1c284-113">이렇게 하면 **VM 에이전트가 없거나 응답하지 않습니다.**블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="1c284-114">이 블레이드에 VM 에이전트가 필요한 VM을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="1c284-115">VM 에이전트를 설치하려면 블레이드의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="1c284-116">![VM 에이전트가 없습니다][2]</span><span class="sxs-lookup"><span data-stu-id="1c284-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="1c284-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1c284-117">See also</span></span>
<span data-ttu-id="1c284-118">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c284-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="1c284-119">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1c284-120">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1c284-121">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)--Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="1c284-122">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md)--보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="1c284-123">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="1c284-124">[Azure 보안 센터 FAQ](security-center-faq.md)--서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1c284-125">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1c284-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
