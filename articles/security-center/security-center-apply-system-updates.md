---
title: "Azure 보안 센터의 시스템 업데이트 aaaApply | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 적용 시스템 업데이트 * * 및 * * 후 시스템 업데이트 * *를 다시 부팅 합니다."
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
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="f902b-103">Azure 보안 센터의 시스템 업데이트 적용</span><span class="sxs-lookup"><span data-stu-id="f902b-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="f902b-104">Azure Security Center는 누락된 운영 체제 업데이트에 대해 매일 Windows 및 Linux 가상 컴퓨터(VM)를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="f902b-105">보안 센터는 Windows VM에서 구성된 서비스에 따라 Windows 업데이트 또는 WSUS(Windows Server Update Services)에서 사용 가능한 보안 및 중요 업데이트의 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="f902b-106">또한 보안 센터 Linux 시스템에서 hello 최신 업데이트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="f902b-107">VM이 시스템 업데이트를 누락하는 경우 보안 센터는 시스템 업데이트 적용을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="f902b-108">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f902b-109">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f902b-110">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="f902b-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="f902b-111">Hello에 **권장 사항을** 블레이드를 **시스템 업데이트를 적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![시스템 업데이트 적용][1]
2. <span data-ttu-id="f902b-113">hello **시스템 업데이트를 적용** 블레이드 열리고 Vm 누락 된 시스템 업데이트의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="f902b-114">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-114">Select a VM.</span></span>

   ![VM 선택][2]
3. <span data-ttu-id="f902b-116">해당 VM에 대한 누락된 업데이트의 목록을 표시하는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="f902b-117">시스템 업데이트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-117">Select a system update.</span></span> <span data-ttu-id="f902b-118">이 예제에서는 KB3156016을 선택해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-118">In this example, let’s select KB3156016.</span></span>

   ![누락된 보안 업데이트][3]

4. <span data-ttu-id="f902b-120">Hello에 hello 단계를 따라 **보안 업데이트** 블레이드 tooapply hello 누락 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![보안 업데이트][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="f902b-122">시스템 업데이트 후 다시 부팅</span><span class="sxs-lookup"><span data-stu-id="f902b-122">Reboot after system updates</span></span>
1. <span data-ttu-id="f902b-123">Toohello 반환 **권장 사항을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="f902b-124">시스템 업데이트를 적용한 후 **시스템 업데이트 후 다시 부팅**이라는 새 항목이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="f902b-125">이 항목에는 tooreboot hello VM toocomplete hello 프로세스의 시스템 업데이트를 적용 해야 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![시스템 업데이트 후 다시 부팅][5]
2. <span data-ttu-id="f902b-127">**시스템 업데이트 후 다시 부팅**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="f902b-128">이렇게 하면 열립니다 **다시 시작이 보류 중인 toocomplete 시스템 업데이트** toorestart toocomplete hello 해야 하는 Vm의 목록 표시 블레이드 시스템 업데이트 프로세스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![다시 시작 보류 중][6]

<span data-ttu-id="f902b-130">Azure toocomplete hello 프로세스에서 VM hello를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="f902b-131">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f902b-131">See also</span></span>
<span data-ttu-id="f902b-132">보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f902b-133">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 Azure 구독 및 리소스 그룹에 대 한 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f902b-134">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f902b-135">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f902b-136">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f902b-137">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f902b-138">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f902b-139">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f902b-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
