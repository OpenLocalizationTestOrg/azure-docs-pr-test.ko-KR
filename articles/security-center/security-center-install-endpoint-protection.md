---
title: "Azure 보안 센터에서 Endpoint Protection aaaInstall | Microsoft Docs"
description: "이 문서에서는 어떻게 tooimplement hello Azure 보안 센터 권장 * * 설치 끝점 보호 * *입니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="b183b-103">Azure 보안 센터에서 Endpoint Protection 설치</span><span class="sxs-lookup"><span data-stu-id="b183b-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="b183b-104">Azure Security Center에서는 Endpoint Protection이 아직 사용하도록 설정되지 않은 경우 Azure VM(가상 컴퓨터)에 Endpoint Protection을 설치할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="b183b-105">이 권장 tooWindows Vm만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="b183b-106">이 배포 예에서는 Microsoft 맬웨어 방지 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="b183b-107">Security Center와 통합된 파트너 목록은 [Azure Security Center에서 파트너 통합](security-center-partner-integration.md#partners-that-integrate-with-security-center)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b183b-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b183b-108">Hello 권장 구성 구현</span><span class="sxs-lookup"><span data-stu-id="b183b-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="b183b-109">이 문서에서는 배포 예제를 사용 하 여 hello 서비스를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="b183b-110">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="b183b-111">Hello에 **권장 사항을** 블레이드를 **Endpoint Protection 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="b183b-112">![Endpoint Protection 설치 선택][1]</span><span class="sxs-lookup"><span data-stu-id="b183b-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="b183b-113">hello **Endpoint Protection 설치** 블레이드 열리고 끝점 보호 없이 Vm의 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="b183b-114">Hello 목록 hello에 tooinstall 끝점 보호 사용을 선택 하 고를 클릭 하는 Vm 중에서 선택 **Vm에 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="b183b-115">![Vm tooinstall Endpoint Protection을 선택 합니다.][2]</span><span class="sxs-lookup"><span data-stu-id="b183b-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="b183b-116">hello **Endpoint Protection 선택** 블레이드에서 열립니다 tooallow 있습니다 tooselect hello 끝점 보호 솔루션 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="b183b-117">이 예제에서는 **Microsoft 맬웨어 방지 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="b183b-118">![Endpoint Protection 선택][3]</span><span class="sxs-lookup"><span data-stu-id="b183b-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="b183b-119">Hello 끝점 보호 솔루션에 대 한 추가 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="b183b-120">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-120">Select **Create**.</span></span>
   <span data-ttu-id="b183b-121">![맬웨어 방지 솔루션 만들기][4]</span><span class="sxs-lookup"><span data-stu-id="b183b-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="b183b-122">Hello에서 필요한 hello 구성 설정을 입력 **확장 추가** 블레이드에서 다음을 선택 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="b183b-123">hello 구성 설정에 대해 자세히 toolearn 참조 [기본 및 사용자 지정 맬웨어 방지 구성](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="b183b-124">[Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) 이제 hello 사용 중인 Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="b183b-125">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b183b-125">See also</span></span>
<span data-ttu-id="b183b-126">이 문서에 설명 했습니다 어떻게 tooimplement hello 보안 센터 권장 "Endpoint Protection."</span><span class="sxs-lookup"><span data-stu-id="b183b-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="b183b-127">Microsoft Azure에서 맬웨어 방지 프로그램 사용에 대 한 더 toolearn hello 다음 문서 참조:</span><span class="sxs-lookup"><span data-stu-id="b183b-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="b183b-128">[클라우드 서비스 및 가상 컴퓨터에 대 한 Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) -자세한 방법을 toodeploy Microsoft 맬웨어 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="b183b-129">보안 센터에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b183b-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="b183b-130">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -자세한 방법을 tooconfigure 보안 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="b183b-131">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b183b-132">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b183b-133">[Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -자세한 방법을 toomanage 및 응답 toosecurity 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b183b-134">[Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b183b-135">[Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답입니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b183b-136">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b183b-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
