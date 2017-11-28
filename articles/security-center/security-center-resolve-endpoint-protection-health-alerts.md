---
title: "Azure 보안 센터에서 endpoint protection 상태 경고 aaaResolve | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 해결 Endpoint Protection 상태 경고 * *입니다."
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
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="8d704-103">Azure 보안 센터에서 Endpoint Protection 상태 경고 해결</span><span class="sxs-lookup"><span data-stu-id="8d704-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="8d704-104">Azure 보안 센터는 검색된 Endpoint Protection 상태 경고를 해결할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="8d704-105">보안 센터 toosee를 끝점 보호 실패와 발생 한 오류 수는 가상 컴퓨터 (Vm)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="8d704-106">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="8d704-107">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="8d704-108">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="8d704-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="8d704-109">Hello에 **권장 사항 블레이드에서**선택, **해결 Endpoint Protection 상태 경고**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="8d704-110">![Endpoint Protection 상태 경고 해결][1]</span><span class="sxs-lookup"><span data-stu-id="8d704-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="8d704-111">Hello 블레이드가 열립니다 **Endpoint Protection 오류** 각 VM에 대 한 실패 및 실패 hello 수와 Vm을 나열 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="8d704-112">Hello 목록에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="8d704-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="8d704-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="8d704-114">A **오류 목록** hello 실패 목록이 표시 하는 VM을 선택 하기 위해 블레이드에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="8d704-115">더 많은 hello 목록 toolearn에서 오류를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="8d704-116">Hello 선택 실패에 대 한 정보로는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="8d704-117">![오류 목록][3]
   ![오류 이벤트][4]</span><span class="sxs-lookup"><span data-stu-id="8d704-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="8d704-118">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8d704-118">See also</span></span>
<span data-ttu-id="8d704-119">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="8d704-120">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8d704-121">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8d704-122">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="8d704-123">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8d704-124">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="8d704-125">[Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8d704-126">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8d704-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
