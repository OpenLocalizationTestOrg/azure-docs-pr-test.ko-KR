---
title: "Azure Security Center의 시스템 업데이트 적용 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **시스템 업데이트 적용** 및 **시스템 업데이트 후 다시 부팅**을 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="dddeb-103">Azure 보안 센터의 시스템 업데이트 적용</span><span class="sxs-lookup"><span data-stu-id="dddeb-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="dddeb-104">Azure Security Center는 누락된 운영 체제 업데이트에 대해 매일 Windows 및 Linux 가상 컴퓨터(VM)를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="dddeb-105">보안 센터는 Windows VM에서 구성된 서비스에 따라 Windows 업데이트 또는 WSUS(Windows Server Update Services)에서 사용 가능한 보안 및 중요 업데이트의 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="dddeb-106">보안 센터는 또한 Linux 시스템에서 최신 업데이트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="dddeb-107">VM이 시스템 업데이트를 누락하는 경우 보안 센터는 시스템 업데이트 적용을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="dddeb-108">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="dddeb-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="dddeb-110">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="dddeb-110">Implement the recommendation</span></span>
1. <span data-ttu-id="dddeb-111">**권장 사항** 블레이드에서 **시스템 업데이트 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![시스템 업데이트 적용][1]
2. <span data-ttu-id="dddeb-113">시스템 업데이트를 누락한 VM의 목록을 표시하는 **시스템 업데이트 적용** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="dddeb-114">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-114">Select a VM.</span></span>

   ![VM 선택][2]
3. <span data-ttu-id="dddeb-116">해당 VM에 대한 누락된 업데이트의 목록을 표시하는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="dddeb-117">시스템 업데이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-117">Select a system update.</span></span> <span data-ttu-id="dddeb-118">이 예제에서는 KB3156016을 선택해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-118">In this example, let’s select KB3156016.</span></span>

   ![누락된 보안 업데이트][3]

4. <span data-ttu-id="dddeb-120">**보안 업데이트** 블레이드의 단계를 따라 누락된 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![보안 업데이트][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="dddeb-122">시스템 업데이트 후 다시 부팅</span><span class="sxs-lookup"><span data-stu-id="dddeb-122">Reboot after system updates</span></span>
1. <span data-ttu-id="dddeb-123">**권장 사항** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="dddeb-124">시스템 업데이트를 적용한 후 **시스템 업데이트 후 다시 부팅**이라는 새 항목이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="dddeb-125">이 항목을 통해 시스템 업데이트 적용 프로세스를 완료하려면 VM을 다시 부팅해야 한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![시스템 업데이트 후 다시 부팅][5]
2. <span data-ttu-id="dddeb-127">**시스템 업데이트 후 다시 부팅**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="dddeb-128">시스템 업데이트 적용 프로세스를 완료하기 위해 다시 시작해야 하는 VM의 목록을 표시하는 **시스템 업데이트를 완료하기 위한 다시 시작이 보류 중입니다** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![다시 시작 보류 중][6]

<span data-ttu-id="dddeb-130">프로세스를 완료하려면 Azure에서 VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="dddeb-131">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dddeb-131">See also</span></span>
<span data-ttu-id="dddeb-132">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dddeb-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="dddeb-133">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="dddeb-134">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="dddeb-135">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="dddeb-136">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="dddeb-137">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="dddeb-138">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="dddeb-139">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dddeb-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
