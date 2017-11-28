---
title: "Azure Security Center에서 보안 경고 처리 | Microsoft Docs"
description: "이 문서는 Azure 보안 센터 기능을 사용하여 보안 인시던트를 처리하는 데 도움이 됩니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: a302f8cb2555eef469a24da2523fdd9b97cc5730
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="6c270-103">Azure Security Center에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="6c270-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="6c270-104">보안 경고를 심사 및 조사하는 작업은 가장 숙련된 보안 분석가라도 많은 시간이 걸릴 수 있고 분석가 중 다수는 어떻게 시작할지도 알지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="6c270-105">보안 센터에서는 고유한 [보안 경고](security-center-managing-and-responding-alerts.md) 간에 정보를 연결하기 위해 [분석](security-center-detection-capabilities.md)을 사용하여 공격 캠페인의 단일 보기 및 모든 관련된 경고를 제공할 수 있습니다. 공격자가 사용한 작업 및 영향을 받는 리소스를 신속하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="6c270-106">이 문서에서는 보안 센터에서 보안 경고 기능을 사용하여 보안 문제를 처리하는 데 도움이 되는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="6c270-107">보안 인시던트란?</span><span class="sxs-lookup"><span data-stu-id="6c270-107">What is a security incident?</span></span>
<span data-ttu-id="6c270-108">보안 센터에서 보안 인시던트는 [kill 체인](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="6c270-109">인시던트는 [보안 경고](security-center-managing-and-responding-alerts.md) 타일 및 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="6c270-110">인시던트는 관련된 경고 목록을 표시하므로 각 항목에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="6c270-111">보안 인시던트 관리</span><span class="sxs-lookup"><span data-stu-id="6c270-111">Managing security incidents</span></span>
<span data-ttu-id="6c270-112">보안 경고 타일을 확인하여 현재 보안 인시던트를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="6c270-113">Azure 포털에 액세스하고 다음 단계를 수행하여 각 보안 문제에 대 한 자세한 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="6c270-114">보안 센터 대시보드에서 **보안 경고** 타일을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![보안 센터의 보안 경고 타일](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="6c270-116">이 타일을 클릭하여 확장하고 보안 인시던트가 감지되면 아래에 표시된 대로 보안 경고 그래프에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="6c270-118">보안 인시던트 설명에 다른 경고와 다른 아이콘이 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="6c270-119">클릭하여 이 인시던트에 대한 자세한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-119">Click on it to view more details about this incident.</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="6c270-121">이 보안 인시던트에 대한 자세한 내용을 확인할 수 있는 **인시던트** 블레이드에는 인시던트의 전체 설명, 심각도(이 경우 높음), 인시던트의 현재 상태(이 경우 아직 *활성화*된 상태로, 이는 사용자가 해제 조치를 취하지 않았음을 의미하며, **보안 경고** 블레이드의 인시던트를 마우스 오른쪽 단추로 클릭하여 수행할 수 있음), 공격을 받은 리소스(이 경우에 *VM1*), 인시던트에 대한 해결 조치를 포함되어 있으며, 아래쪽 창에는 이 인시던트에 포함된 경고가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="6c270-122">각 경고에 대한 자세한 정보를 가져오는 경우 클릭하면 아래와 같이 다른 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="6c270-124">이 블레이드의 정보는 경고에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="6c270-125">이러한 경고를 관리하는 방법에 대한 자세한 내용은 [Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) 을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="6c270-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="6c270-126">이 기능에 대한 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="6c270-127">새 필터를 사용하면 인시던트만, 경고만 또는 둘 다 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="6c270-128">인시던트가 있는 경우 동일한 경고가 인시던트의 일부로 존재할 뿐만 아니라 독립 실행형 경고로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c270-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6c270-129">See also</span></span>
<span data-ttu-id="6c270-130">이 문서에서는 보안 센터에서 보안 인시던트 기능을 사용하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="6c270-131">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c270-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="6c270-132">Azure 보안 센터에서 보안 경고 관리 및 대응</span><span class="sxs-lookup"><span data-stu-id="6c270-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="6c270-133">Azure 보안 센터 감지 기능</span><span class="sxs-lookup"><span data-stu-id="6c270-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="6c270-134">Azure 보안 센터 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="6c270-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="6c270-135">Azure 보안 센터에서 보안 경고 관리 및 대응</span><span class="sxs-lookup"><span data-stu-id="6c270-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="6c270-136">[Azure 보안 센터 FAQ](security-center-faq.md)--서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6c270-137">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)--Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c270-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
