---
title: "Azure 보안 센터에서 aaaManaging 파트너 솔루션 | Microsoft Docs"
description: "이 문서 Azure 보안 센터에서 Azure 구독과 통합 하 여 파트너 솔루션의 한 눈에 보기 hello 상태는 모니터를 통해 하는 방법 안내 합니다."
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
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="e13f9-103">Azure 보안 센터를 사용하여 파트너 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="e13f9-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="e13f9-104">이 문서 toomonitor Azure 보안 센터에서 파트너 솔루션의 상태를 hello 하는 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="e13f9-105">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="e13f9-106">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="e13f9-107">파트너 솔루션 모니터링</span><span class="sxs-lookup"><span data-stu-id="e13f9-107">Monitoring partner solutions</span></span>
<span data-ttu-id="e13f9-108">hello **파트너 솔루션** hello 타일 **보안 센터** 블레이드 통해 통합 Azure 구독 된 파트너 솔루션의 한 눈에 보기 hello 상태 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![파트너 솔루션 타일][1]

<span data-ttu-id="e13f9-110">hello **파트너 솔루션** 타일 통합 구독 된 파트너 솔루션의 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="e13f9-111">통합 된 솔루션이 없는 경우 hello 숫자를 0 hello 타일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="e13f9-112">파트너 솔루션의 tooview hello 상태:</span><span class="sxs-lookup"><span data-stu-id="e13f9-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="e13f9-113">선택 hello **파트너 솔루션** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="e13f9-114">hello **파트너 솔루션** 파트너 솔루션의 목록을 표시 하는 블레이드에서 열립니다 tooSecurity 센터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![파트너 솔루션][3]

   <span data-ttu-id="e13f9-116">파트너 솔루션의 hello 상태 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="e13f9-117">보호됨(녹색) - 상태 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="e13f9-118">비정상(빨강) - 즉각적인 주의가 필요한 상태 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="e13f9-119">중지 된 보고 (주황색)-hello 솔루션의 상태를 보고 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="e13f9-120">알 수 없는 보호 상태 (주황색)-hello 솔루션의 hello 상태 알려져 있지 않은 새 리소스 toohello 기존 솔루션 추가 하지 못했습니다 tooa 과정 있으므로이 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="e13f9-121">보고 되지 않습니다 (회색)-hello 솔루션 아무 것도 보고 하지 않았음을 아직 최근에 연결 여전히 배포 하는 경우 솔루션의 상태 보고 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="e13f9-122">파트너 솔루션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-122">Select a partner solution.</span></span> <span data-ttu-id="e13f9-123">이 예제에서는 select hello를 통해 **Qualys** 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="e13f9-124">Hello 업체 솔루션 및 hello 솔루션의 hello 상태 관련 리소스를 보여 주는 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="e13f9-125">선택 **솔루션 콘솔** 이 솔루션에 tooopen hello 파트너 관리 환경을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![파트너 솔루션 세부 정보][4]
3. <span data-ttu-id="e13f9-127">Toohello 돌아가서 **Qualys** 블레이드에 대 한 선택 **링크 VM**합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="e13f9-128">hello **링크 응용 프로그램** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="e13f9-129">여기서 리소스 toohello 업체 솔루션을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-129">Here you can connect resources toohello partner solution.</span></span>

   ![링크 리소스 toopartner 솔루션][5]

## <a name="next-steps"></a><span data-ttu-id="e13f9-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e13f9-131">Next steps</span></span>
<span data-ttu-id="e13f9-132">이 문서에 도입 된 toohello 던 **파트너 솔루션** 보안 센터에 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="e13f9-133">보안 센터에 대해 자세히 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="e13f9-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="e13f9-134">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -학습 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e13f9-135">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e13f9-136">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="e13f9-137">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="e13f9-138">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="e13f9-139">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e13f9-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
