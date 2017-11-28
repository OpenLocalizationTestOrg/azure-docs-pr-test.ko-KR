---
title: "Azure Security Center에서 Endpoint Protection 설치 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **Endpoint Protection 설치**를 구현하는 방법을 보여 줍니다."
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
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="a9ad7-103">Azure 보안 센터에서 Endpoint Protection 설치</span><span class="sxs-lookup"><span data-stu-id="a9ad7-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="a9ad7-104">Azure Security Center에서는 Endpoint Protection이 아직 사용하도록 설정되지 않은 경우 Azure VM(가상 컴퓨터)에 Endpoint Protection을 설치할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="a9ad7-105">이 권장 사항은 Windows VM에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ad7-106">이 배포 예에서는 Microsoft 맬웨어 방지 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="a9ad7-107">Security Center와 통합된 파트너 목록은 [Azure Security Center에서 파트너 통합](security-center-partner-integration.md#partners-that-integrate-with-security-center)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a9ad7-108">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="a9ad7-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="a9ad7-109">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="a9ad7-110">이 문서는 단계별 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="a9ad7-111">**권장 사항** 블레이드에서 **Endpoint Protection 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="a9ad7-112">![Endpoint Protection 설치 선택][1]</span><span class="sxs-lookup"><span data-stu-id="a9ad7-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="a9ad7-113">Endpoint Protection이 없는 VM의 목록을 표시하는 **Endpoint Protection 설치** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="a9ad7-114">목록에서 Endpoint Protection 프로그램을 설치하려는 VM을 선택하고 **VM에 설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="a9ad7-115">![Endpoint Protection을 설치할 VM 선택][2]</span><span class="sxs-lookup"><span data-stu-id="a9ad7-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="a9ad7-116">사용할 Endpoint Protection 솔루션을 선택할 수 있는 **Endpoint Protection 선택** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="a9ad7-117">이 예제에서는 **Microsoft 맬웨어 방지 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="a9ad7-118">![Endpoint Protection 선택][3]</span><span class="sxs-lookup"><span data-stu-id="a9ad7-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="a9ad7-119">Endpoint Protection 솔루션에 대한 추가 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="a9ad7-120">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-120">Select **Create**.</span></span>
   <span data-ttu-id="a9ad7-121">![맬웨어 방지 솔루션 만들기][4]</span><span class="sxs-lookup"><span data-stu-id="a9ad7-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="a9ad7-122">**확장 추가** 블레이드에서 필요한 구성 설정을 입력하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="a9ad7-123">구성 설정에 대한 자세한 내용은 [기본 및 사용자 지정 맬웨어 방지 구성](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="a9ad7-124">선택한 VM에서 [Microsoft 맬웨어 방지 프로그램](../security/azure-security-antimalware.md)이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="a9ad7-125">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a9ad7-125">See also</span></span>
<span data-ttu-id="a9ad7-126">이 문서에서는 보안 센터 권장 사항 "Endpoint Protection 설치"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="a9ad7-127">Azure에서 Microsoft 맬웨어 방지 프로그램을 사용하도록 설정하는 방법에 대해 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="a9ad7-128">[Cloud Services 및 Virtual Machines용 Microsoft 맬웨어 방지 프로그램](../security/azure-security-antimalware.md) -- Microsoft 맬웨어 방지 프로그램을 배포하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="a9ad7-129">Security Center에 대해 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="a9ad7-130">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="a9ad7-131">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a9ad7-132">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a9ad7-133">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a9ad7-134">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="a9ad7-135">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a9ad7-136">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ad7-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
