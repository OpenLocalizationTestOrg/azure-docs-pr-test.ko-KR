---
title: "Azure Security Center에서 OS 버전 업데이트 | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터 권장 사항 **OS 버전 업데이트**를 구현하는 방법을 보여 줍니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="4f3e5-103">Azure 보안 센터에서 OS 버전 업데이트</span><span class="sxs-lookup"><span data-stu-id="4f3e5-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="4f3e5-104">클라우드 서비스의 가상 컴퓨터(VM)의 경우 Azure 보안 센터는 사용 가능한 최신 버전이 있는 경우 운영 체제(OS) 업데이트를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="4f3e5-105">프로덕션 슬롯에서 실행되는 클라우드 서비스 웹 및 작업자 역할만 모니터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="4f3e5-106">이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="4f3e5-107">단계별 가이드는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="4f3e5-108">권장 사항 구현</span><span class="sxs-lookup"><span data-stu-id="4f3e5-108">Implement the recommendation</span></span>
1. <span data-ttu-id="4f3e5-109">**권장 사항** 블레이드에서 **OS 버전 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="4f3e5-110">![OS 버전 업데이트][1]</span><span class="sxs-lookup"><span data-stu-id="4f3e5-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="4f3e5-111">이렇게 하면 **OS 버전 업데이트**블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="4f3e5-112">이 블레이드의 단계를 따라 OS 버전을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="4f3e5-113">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4f3e5-113">See also</span></span>
<span data-ttu-id="4f3e5-114">이 문서에서는 보안 센터 권장 사항 "OS 버전 업데이트"를 구현하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="4f3e5-115">클라우드 서비스 및 클라우드 서비스에 대한 OS 버전 업데이트에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="4f3e5-116">클라우드 서비스 개요</span><span class="sxs-lookup"><span data-stu-id="4f3e5-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="4f3e5-117">클라우드 서비스를 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f3e5-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="4f3e5-118">클라우드 서비스를 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="4f3e5-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="4f3e5-119">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="4f3e5-120">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) -- Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4f3e5-121">[Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) -- 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4f3e5-122">[Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) –- Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="4f3e5-123">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) -- 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="4f3e5-124">[Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -- 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="4f3e5-125">[Azure 보안 센터 FAQ](security-center-faq.md) -- 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="4f3e5-126">[Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) -- 최신 Azure 보안 뉴스 및 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f3e5-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
