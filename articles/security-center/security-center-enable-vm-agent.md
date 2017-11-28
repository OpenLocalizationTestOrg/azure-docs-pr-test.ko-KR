---
title: "Azure 보안 센터에서 VM 에이전트 aaaEnable | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * *를 사용 하도록 설정 VM 에이전트 * *입니다."
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
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="7b691-103">Azure 보안 센터에서 VM 에이전트 사용</span><span class="sxs-lookup"><span data-stu-id="7b691-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="7b691-104">hello VM 에이전트를 설치 해야 순서 대로 가상 컴퓨터 (Vm)에 너무[데이터 컬렉션 활성화](security-center-enable-data-collection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="7b691-105">Azure 보안 센터는 사용 하도록 하면 toosee Vm 해야 하는 hello VM 에이전트에서 사용 하는 권장 hello 해당 Vm에서 VM 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="7b691-106">hello Azure Marketplace에서에서 배포 되는 Vm에 대 한 hello VM 에이전트는 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="7b691-107">hello 문서 [VM 에이전트 및 확장-2 부](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) tooinstall VM 에이전트를 hello 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="7b691-108">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="7b691-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7b691-110">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="7b691-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="7b691-111">Hello에 **권장 사항 블레이드에서**선택, **VM 에이전트 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="7b691-112">![VM 에이전트 사용][1]</span><span class="sxs-lookup"><span data-stu-id="7b691-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="7b691-113">Hello 블레이드가 열립니다 **VM 에이전트가 누락 또는 응답 하지 않아**합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="7b691-114">이 블레이드는 hello VM 에이전트를 필요로 하는 hello Vm을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="7b691-115">Hello 블레이드 tooinstall hello VM 에이전트에 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="7b691-116">![VM 에이전트가 없습니다][2]</span><span class="sxs-lookup"><span data-stu-id="7b691-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="7b691-117">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7b691-117">See also</span></span>
<span data-ttu-id="7b691-118">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7b691-119">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md)-자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7b691-120">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md)-- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7b691-121">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md)-toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7b691-122">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md)-자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7b691-123">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7b691-124">[Azure 보안 센터 FAQ](security-center-faq.md)-찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7b691-125">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/)-hello 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7b691-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
