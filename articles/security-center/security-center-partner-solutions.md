---
title: "Azure Security Center에서 파트너 솔루션 관리 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서, Azure 구독에 통합된 파트너 솔ㄹ션의 보안 상태를 한 눈에 모니터링하는 방법을 살펴봅니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="ab7f2-103">Azure 보안 센터를 사용하여 파트너 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="ab7f2-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="ab7f2-104">이 문서에서는 Azure 보안 센터에서 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="ab7f2-105">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="ab7f2-106">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="ab7f2-107">파트너 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="ab7f2-107">Monitoring partner solutions</span></span>
<span data-ttu-id="ab7f2-108">**Security Center** 블레이드의 **파트너 솔루션** 타일을 통해 Azure 구독과 통합된 파트너 솔루션의 상태를 한 눈에 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![파트너 솔루션 타일][1]

<span data-ttu-id="ab7f2-110">**파트너 솔루션** 타일에는 구독과 통합된 파트너 솔루션 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="ab7f2-111">통합된 솔루션이 없는 경우 숫자 0이 타일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="ab7f2-112">파트너 솔루션의 상태를 보려면:</span><span class="sxs-lookup"><span data-stu-id="ab7f2-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="ab7f2-113">**파트너 솔루션** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="ab7f2-114">**파트너 솔루션** 블레이드가 열리고 Security Center에 연결된 파트너 솔루션의 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![파트너 솔루션][3]

   <span data-ttu-id="ab7f2-116">파트너 솔루션의 상태는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="ab7f2-117">보호됨(녹색) - 상태 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="ab7f2-118">비정상(빨강) - 즉각적인 주의가 필요한 상태 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="ab7f2-119">중지된 보고(주황) - 솔루션이 상태의 보고를 중지했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="ab7f2-120">알 수 없는 보호 상태(주황) - 이 때에는 기존 솔루션에 새 리소스를 추가하는 실패한 프로세스로 인해 솔루션의 상태를 알 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="ab7f2-121">보고되지 않음(회색) - 솔루션이 아무 것도 보고하지 않았습니다. 솔루션이 최근에 연결되었고 여전히 배포 중인 경우 솔루션의 상태를 보고하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="ab7f2-122">파트너 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-122">Select a partner solution.</span></span> <span data-ttu-id="ab7f2-123">이 예제에서는 **Qualys** 솔루션을 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="ab7f2-124">블레이드가 열리고 파트너 솔루션의 상태 및 솔루션의 관련 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="ab7f2-125">**솔루션 콘솔** 을 선택하여 이 솔루션에 대한 파트너 관리 환경을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![파트너 솔루션 세부 정보][4]
3. <span data-ttu-id="ab7f2-127">**Qualys** 블레이드로 돌아가 **VM 연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="ab7f2-128">**응용 프로그램 연결** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="ab7f2-129">여기서 리소스를 파트너 솔루션에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-129">Here you can connect resources to the partner solution.</span></span>

   ![리소스를 파트너 솔루션에 연결][5]

## <a name="next-steps"></a><span data-ttu-id="ab7f2-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab7f2-131">Next steps</span></span>
<span data-ttu-id="ab7f2-132">이 문서에서는 보안 센터의 **파트너 솔루션** 타일을 소개했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="ab7f2-133">Security Center에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="ab7f2-134">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ab7f2-135">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ab7f2-136">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ab7f2-137">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ab7f2-138">[Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ab7f2-139">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ab7f2-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
