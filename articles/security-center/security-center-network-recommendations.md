---
title: "Azure Security Center에서 네트워크 보호 | Microsoft Docs"
description: "이 문서에서는 Azure 네트워크를 보호하고 보안 정책을 준수하는 데 도움이 되는 Azure 보안 센터의 권장 사항에 대해 설명합니다."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="e4507-103">Azure 보안 센터에서 네트워크 보호</span><span class="sxs-lookup"><span data-stu-id="e4507-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="e4507-104">Azure 보안 센터에서는 Azure 리소스의 보안 상태를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="e4507-105">보안 센터가 잠재적인 보안 취약점을 식별하는 경우 필요한 컨트롤을 구성하는 과정을 안내하는 권장 사항을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="e4507-106">이러한 권장 사항은 가상 컴퓨터(VM), 네트워킹, SQL, 응용 프로그램 등의 Azure 리소스 유형에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="e4507-107">이 문서에서는 네트워크에 적용되는 권장 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="e4507-108">네트워크 권장 사항은 차세대 방화벽, 네트워크 보안 그룹, 인바운드 트래픽 규칙 구성 등에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="e4507-109">아래 테이블을 참조로 사용하여 제공되는 네트워크 권장 사항을 이해하고 각 권장 사항을 적용할 경우 어떻게 되는지 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="e4507-110">제공되는 네트워크 권장 사항</span><span class="sxs-lookup"><span data-stu-id="e4507-110">Available network recommendations</span></span>
| <span data-ttu-id="e4507-111">권장 사항</span><span class="sxs-lookup"><span data-stu-id="e4507-111">Recommendation</span></span> | <span data-ttu-id="e4507-112">설명</span><span class="sxs-lookup"><span data-stu-id="e4507-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e4507-113">차세대 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="e4507-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="e4507-114">보안 보호를 증가시키기 위해 Microsoft 파트너의 차세대 방화벽(NGFW)을 추가하라는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="e4507-115">NGFW를 통해서만 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="e4507-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="e4507-116">인바운드 트래픽이 NGFW를 통해 VM로 강제하도록 네트워크 보안 그룹(NSG) 규칙을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="e4507-117">서브넷 또는 가상 컴퓨터에서 네트워크 보안 그룹 활성화</span><span class="sxs-lookup"><span data-stu-id="e4507-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="e4507-118">서브넷 또는 VM에서 NSG를 활성화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="e4507-119">인터넷 끝점을 통한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="e4507-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="e4507-120">NSG에 대한 인바운드 트래픽 규칙을 구성하라는 권장 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="e4507-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e4507-121">See also</span></span>
<span data-ttu-id="e4507-122">다른 Azure 리소스 유형에 적용되는 권장 사항에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4507-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="e4507-123">Azure 보안 센터에서 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="e4507-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="e4507-124">Azure 보안 센터에서 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="e4507-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="e4507-125">Azure 보안 센터에서 Azure SQL 서비스 보호</span><span class="sxs-lookup"><span data-stu-id="e4507-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="e4507-126">보안 센터에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4507-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e4507-127">[Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e4507-128">[Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e4507-129">[Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e4507-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
