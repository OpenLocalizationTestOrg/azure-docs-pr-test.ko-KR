---
title: "Azure 보안 센터에서 보안 경고 aaaHandling | Microsoft Docs"
description: "이 문서 toouse Azure 보안 센터 기능 toohandle 보안 사고 수 있습니다."
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
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="ede6f-103">Azure Security Center에서 보안 인시던트 처리</span><span class="sxs-lookup"><span data-stu-id="ede6f-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="ede6f-104">에 대 한 심사 및 보안 경고를 조사 숙련 보안 분석가 hello에 대 한 시간이 걸릴 수 있으며 여러 하드 tooeven 위치를 알 수는 toobegin 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="ede6f-105">사용 하 여 [분석](security-center-detection-capabilities.md) 고유 간에 tooconnect hello 정보 [보안 경고](security-center-managing-and-responding-alerts.md), 보안 센터 공격 캠페인의 단일 뷰를 제공할 수 있습니다 및 관련 된 모든 hello 경고-할 수 있습니다 어떤 작업 hello 공격자는 적용 하 고 리소스에 영향을 받은 신속 하 게 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="ede6f-106">이 문서에서는 어떻게 toouse 보안 경고의 보안 센터 tooassist 기능 보안 문제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="ede6f-107">보안 인시던트란?</span><span class="sxs-lookup"><span data-stu-id="ede6f-107">What is a security incident?</span></span>
<span data-ttu-id="ede6f-108">보안 센터에서 보안 인시던트는 [kill 체인](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) 패턴과 일치하는 리소스에 대한 모든 경고의 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="ede6f-109">Hello에 인시던트 표시 [보안 경고](security-center-managing-and-responding-alerts.md) 타일 및 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="ede6f-110">인시던트 각 항목에 대 한 자세한 내용은 tooobtain 있습니다 수 있도록 하는 hello 목록이 관련된 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="ede6f-111">보안 인시던트 관리</span><span class="sxs-lookup"><span data-stu-id="ede6f-111">Managing security incidents</span></span>
<span data-ttu-id="ede6f-112">Hello 보안 경고 타일 확인 하 여 현재 보안 인시던트를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="ede6f-113">Hello Azure 포털에 액세스 하 고 각 보안 문제에 대 한 자세한 내용은 아래 toosee hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="ede6f-114">Hello 보안 센터 대시보드에서 hello 나타납니다 **보안 경고** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![보안 센터의 보안 경고 타일](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="ede6f-116">이 타일 tooexpand 클릭할 한 경우 보안 문제가 감지 되 면 아래와 같이 hello 보안 경고 그래프 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="ede6f-118">Hello 보안 문제 설명에 아이콘은 tooother 경고를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="ede6f-119">클릭 하 여 조치 tooview이이 인시던트에 대 한 더 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-119">Click on it tooview more details about this incident.</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="ede6f-121">Hello에 **인시던트** 현재 상태의 전체 설명 (경우에이 높은)의 심각도 포함 하는이 보안 사고에 대 한 세부 정보 블레이드에서 더 표시 됩니다 (이 경우 이것이 여전히 *활성*hello 사용자를 의미 있는 작업 tooit 수행 하지 않은-hello에서 hello 인시던트를 마우스 오른쪽 단추로 클릭 하 여이 작업을 수행할 수 있습니다, **보안 경고** 블레이드), hello 공격 리소스 (이 경우 *VM1*), hello 인시던트에 대 한 업데이트 관리 단계가 hello 및이 서비스에 포함 된 hello 경고가 hello 아래쪽 창에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="ede6f-122">각 경고에 대 한 자세한 내용은 tooobtain 하려는 경우 아래와 같이 다른 블레이드를 클릭 하기만 열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![보안 인시던트](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="ede6f-124">이 블레이드는 hello 방법은 toohello 경고에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="ede6f-125">읽기 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) 방법에 대 한 자세한 내용은 toomanage 이러한 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="ede6f-126">이 기능에 대한 몇 가지 중요한 고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="ede6f-127">새 필터를 사용 하면 toocustomize 보기 tooIncident만만, 경고 또는 둘 다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="ede6f-128">hello 동일한 경고에서는 인시던트 (있는 경우)는 물론 toobe 독립 실행형 경고로 표시의 일부로 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="ede6f-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ede6f-129">See also</span></span>
<span data-ttu-id="ede6f-130">이 문서에서는 toouse 보안 센터에서 인시던트 기능 보안 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="ede6f-131">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="ede6f-132">관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답</span><span class="sxs-lookup"><span data-stu-id="ede6f-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="ede6f-133">Azure 보안 센터 감지 기능</span><span class="sxs-lookup"><span data-stu-id="ede6f-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="ede6f-134">Azure Security Center 계획 및 작업 가이드</span><span class="sxs-lookup"><span data-stu-id="ede6f-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="ede6f-135">관리 하 고 Azure 보안 센터에서 toosecurity 경고 응답</span><span class="sxs-lookup"><span data-stu-id="ede6f-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="ede6f-136">[Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ede6f-137">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)--Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ede6f-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
