---
title: "Azure ExpressRoute 도입을 위한 필수 구성 요소 | Microsoft Docs"
description: "이 페이지에서는 Azure ExpressRoute 회로를 주문하기 전에 충족해야 하는 요구 사항 목록을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 8629235511e0dda149ceef6a9c834c3042f64f90
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-prerequisites--checklist"></a><span data-ttu-id="51b96-103">ExpressRoute 필수 구성 요소 및 검사 목록</span><span class="sxs-lookup"><span data-stu-id="51b96-103">ExpressRoute prerequisites & checklist</span></span>
<span data-ttu-id="51b96-104">ExpressRoute를 사용하여 Microsoft 클라우드 서비스에 연결하려면 다음 섹션에 나열된 다음 요구 사항을 충족하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-104">To connect to Microsoft cloud services using ExpressRoute, you need to verify that the following requirements listed in the following sections have been met.</span></span>

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a><span data-ttu-id="51b96-105">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="51b96-105">Azure account</span></span>
* <span data-ttu-id="51b96-106">유효한 활성 Microsoft Azure 계정</span><span class="sxs-lookup"><span data-stu-id="51b96-106">A valid and active Microsoft Azure account.</span></span> <span data-ttu-id="51b96-107">ExpressRoute 회로를 설정하려면 이 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-107">This account is required to set up the ExpressRoute circuit.</span></span> <span data-ttu-id="51b96-108">ExpressRoute 회로는 Azure 구독 내의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-108">ExpressRoute circuits are resources within Azure subscriptions.</span></span> <span data-ttu-id="51b96-109">Azure 구독은 Office 365 서비스 및 Dynamics 365와 같은 Azure 이외의 Microsoft 클라우드 서비스에 대한 연결이 제한되는 경우에도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-109">An Azure subscription is a requirement even if connectivity is limited to non-Azure Microsoft cloud services, such as Office 365 services and Dynamics 365.</span></span>
* <span data-ttu-id="51b96-110">활성 Office 365 구독(Office 365 서비스를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="51b96-110">An active Office 365 subscription (if using Office 365 services).</span></span> <span data-ttu-id="51b96-111">자세한 내용은 이 문서의 [Office 365 특정 요구 사항](#office-365-specific-requirements) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51b96-111">For more information, see the [Office 365 specific requirements](#office-365-specific-requirements) section of this article.</span></span>

## <a name="connectivity-provider"></a><span data-ttu-id="51b96-112">연결 공급자</span><span class="sxs-lookup"><span data-stu-id="51b96-112">Connectivity provider</span></span>

* <span data-ttu-id="51b96-113">Microsoft 클라우드에 연결하는 데 [ExpressRoute 연결 파트너](expressroute-locations.md#partners)와 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-113">You can work with an [ExpressRoute connectivity partner](expressroute-locations.md#partners) to connect to the Microsoft cloud.</span></span> <span data-ttu-id="51b96-114">[세 가지 방법](expressroute-introduction.md)으로 온-프레미스 네트워크와 Microsoft 간에 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-114">You can set up a connection between your on-premises network and Microsoft in [three ways](expressroute-introduction.md).</span></span>
* <span data-ttu-id="51b96-115">공급자가 ExpressRoute 연결 파트너가 아닌 경우 [클라우드 Exchange 공급자](expressroute-locations.md#connectivity-through-exchange-providers)를 통해 Microsoft 클라우드에 계속 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-115">If your provider is not an ExpressRoute connectivity partner, you can still connect to the Microsoft cloud through a [cloud exchange provider](expressroute-locations.md#connectivity-through-exchange-providers).</span></span>

## <a name="network-requirements"></a><span data-ttu-id="51b96-116">네트워크 요구 사항</span><span class="sxs-lookup"><span data-stu-id="51b96-116">Network requirements</span></span>
* <span data-ttu-id="51b96-117">**중복 연결**: 사용자와 공급자 간 물리적 연결에서 중복성 요구 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-117">**Redundant connectivity**: there is no redundancy requirement on physical connectivity between you and your provider.</span></span> <span data-ttu-id="51b96-118">[클라우드 Exchange에 대해 단 하나의 물리적 연결만](expressroute-faqs.md#onep2plink)있는 경우에도 Microsoft의 라우터 및 피어링 라우터 간에 중복 BGP 세션을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-118">Microsoft does require redundant BGP sessions to be set up between Microsoft’s routers and the peering routers, even when you have just [one physical connection to a cloud exchange](expressroute-faqs.md#onep2plink).</span></span>
* <span data-ttu-id="51b96-119">**라우팅**: Microsoft Cloud에 연결하는 방법에 따라 사용자와 공급자는 [라우팅 도메인](expressroute-circuit-peerings.md)에 대한 BGP 세션을 설정 및 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-119">**Routing**: depending on how you connect to the Microsoft Cloud, you or your provider need to set up and manage the BGP sessions for [routing domains](expressroute-circuit-peerings.md).</span></span> <span data-ttu-id="51b96-120">일부 이더넷 연결 공급자 또는 클라우드 Exchange 공급자는 가치 추가 서비스로 BGP 관리를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-120">Some Ethernet connectivity provider or cloud exchange provider may offer BGP management as a value-add service.</span></span>
* <span data-ttu-id="51b96-121">**NAT**: Microsoft만 Microsoft 피어링을 통해 공용 IP 주소를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-121">**NAT**: Microsoft only accepts public IP addresses through Microsoft peering.</span></span> <span data-ttu-id="51b96-122">온-프레미스 네트워크에서 개인 IP 주소를 사용하는 경우 사용자 또는 공급자는 [NAT를 사용](expressroute-nat.md)하여 개인 IP 주소를 공용 IP 주소로 번역해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-122">If you are using private IP addresses in your on-premises network, you or your provider need to translate the private IP addresses to the public IP addresses [using the NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="51b96-123">**QoS**: 비즈니스용 Skype에는 차별화된 QoS 처리를 필요로 하는 다양한 서비스(예: 음성, 비디오, 텍스트)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-123">**QoS**: Skype for Business has various services (for example; voice, video, text) that require differentiated QoS treatment.</span></span> <span data-ttu-id="51b96-124">사용자와 공급자는 [QoS 요구 사항](expressroute-qos.md)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-124">You and your provider should follow the [QoS requirements](expressroute-qos.md).</span></span>
* <span data-ttu-id="51b96-125">**네트워크 보안**: ExpressRoute를 통해 Microsoft Cloud에 연결할 때 [네트워크 보안](../best-practices-network-security.md)을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-125">**Network Security**: consider [network security](../best-practices-network-security.md) when connecting to the Microsoft Cloud via ExpressRoute.</span></span>

## <a name="office-365"></a><span data-ttu-id="51b96-126">Office 365</span><span class="sxs-lookup"><span data-stu-id="51b96-126">Office 365</span></span>
<span data-ttu-id="51b96-127">ExpressRoute에서 Office 365를 사용하도록 설정하려는 경우 Office 365 요구 사항에 대한 자세한 내용은 다음 문서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-127">If you plan to enable Office 365 on ExpressRoute, review the following documents for more information about Office 365 requirements.</span></span>

* [<span data-ttu-id="51b96-128">Office 365용 ExpressRoute 개요</span><span class="sxs-lookup"><span data-stu-id="51b96-128">Overview of ExpressRoute for Office 365</span></span>](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [<span data-ttu-id="51b96-129">Office 365용 ExpressRoute로 라우팅</span><span class="sxs-lookup"><span data-stu-id="51b96-129">Routing with ExpressRoute for Office 365</span></span>](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [<span data-ttu-id="51b96-130">Office 365 URL 및 IP 주소 범위</span><span class="sxs-lookup"><span data-stu-id="51b96-130">Office 365 URLs and IP address ranges</span></span>](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [<span data-ttu-id="51b96-131">Office 365에 대한 네트워크 계획 및 성능 조정</span><span class="sxs-lookup"><span data-stu-id="51b96-131">Network planning and performance tuning for Office 365</span></span>](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [<span data-ttu-id="51b96-132">네트워크 대역폭 계산기 및 도구</span><span class="sxs-lookup"><span data-stu-id="51b96-132">Network bandwidth calculators and tools</span></span>](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [<span data-ttu-id="51b96-133">온-프레미스 환경과 Office 365 통합</span><span class="sxs-lookup"><span data-stu-id="51b96-133">Office 365 integration with on-premises environments</span></span>](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [<span data-ttu-id="51b96-134">Office 365 고급 교육 비디오의 ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="51b96-134">ExpressRoute on Office 365 advanced training videos</span></span>](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a><span data-ttu-id="51b96-135">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="51b96-135">Dynamics 365</span></span>
<span data-ttu-id="51b96-136">ExpressRoute에서 Dynamics 365를 사용하도록 설정하려는 경우 Dynamics 365에 대한 자세한 내용은 다음 문서를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-136">If you plan to enable Dynamics 365 on ExpressRoute, review the following documents for more information about Dynamics 365</span></span>

* [<span data-ttu-id="51b96-137">Dynamics 365 및 ExpressRoute 백서</span><span class="sxs-lookup"><span data-stu-id="51b96-137">Dynamics 365 and ExpressRoute whitepaper</span></span>](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* <span data-ttu-id="51b96-138">[Dynamics 365 URL](https://support.microsoft.com/kb/2655102) 및 [IP 주소 범위](https://support.microsoft.com/kb/2728473)</span><span class="sxs-lookup"><span data-stu-id="51b96-138">[Dynamics 365 URLs](https://support.microsoft.com/kb/2655102) and [IP address ranges](https://support.microsoft.com/kb/2728473)</span></span>

## <a name="next-steps"></a><span data-ttu-id="51b96-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51b96-139">Next steps</span></span>
* <span data-ttu-id="51b96-140">ExpressRoute에 대한 자세한 내용은 [ExpressRoute FAQ](expressroute-faqs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51b96-140">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
* <span data-ttu-id="51b96-141">ExpressRoute 연결 공급자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-141">Find an ExpressRoute connectivity provider.</span></span> <span data-ttu-id="51b96-142">[ExpressRoute 파트너 및 피어링 위치](expressroute-locations.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="51b96-142">See [ExpressRoute partners and peering locations](expressroute-locations.md).</span></span>
* <span data-ttu-id="51b96-143">[라우팅](expressroute-routing.md), [NAT](expressroute-nat.md) 및 [QoS](expressroute-qos.md)에 대한 요구 사항을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-143">Refer to requirements for [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), and [QoS](expressroute-qos.md).</span></span>
* <span data-ttu-id="51b96-144">ExpressRoute 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="51b96-144">Configure your ExpressRoute connection.</span></span>
  * [<span data-ttu-id="51b96-145">ExpressRoute 회로 만들기</span><span class="sxs-lookup"><span data-stu-id="51b96-145">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="51b96-146">라우팅 구성</span><span class="sxs-lookup"><span data-stu-id="51b96-146">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="51b96-147">VNet을 ExpressRoute 회로에 연결</span><span class="sxs-lookup"><span data-stu-id="51b96-147">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)
