---
title: "Azure Active Directory 응용 프로그램 프록시를 사용 하는 경우 aaaNetwork 토폴로지 고려 사항 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항을 다룹니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="94eed-103">Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="94eed-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="94eed-104">이 문서에서는 응용 프로그램을 원격으로 게시 및 액세스하기 위해 Azure AD(Azure Active Directory) 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="94eed-105">트래픽 흐름</span><span class="sxs-lookup"><span data-stu-id="94eed-105">Traffic flow</span></span>

<span data-ttu-id="94eed-106">응용 프로그램은 Azure AD 응용 프로그램 프록시를 통해 게시 되 면 트래픽 hello 사용자 toohello 응용 프로그램에서 3 개의 연결을 통해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-106">When an application is published through Azure AD Application Proxy, traffic from hello users toohello applications flows through three connections:</span></span>

1. <span data-ttu-id="94eed-107">hello 사용자가 Azure에서 toohello Azure AD 응용 프로그램 프록시 서비스 공용 끝점 연결</span><span class="sxs-lookup"><span data-stu-id="94eed-107">hello user connects toohello Azure AD Application Proxy service public endpoint on Azure</span></span>
2. <span data-ttu-id="94eed-108">응용 프로그램 프록시 서비스 hello toohello 응용 프로그램 프록시 커넥터 연결</span><span class="sxs-lookup"><span data-stu-id="94eed-108">hello Application Proxy service connects toohello Application Proxy connector</span></span>
3. <span data-ttu-id="94eed-109">hello 응용 프로그램 프록시 커넥터 toohello 대상 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="94eed-109">hello Application Proxy connector connects toohello target application</span></span>

![사용자 tootarget 응용 프로그램에서 트래픽 흐름을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="94eed-111">테넌트 위치 및 응용 프로그램 프록시 서비스</span><span class="sxs-lookup"><span data-stu-id="94eed-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="94eed-112">Azure AD 테 넌 트에 가입 하면 테 넌 트의 hello 영역 지정 hello 국가별로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-112">When you sign up for an Azure AD tenant, hello region of your tenant is determined by hello country you specify.</span></span> <span data-ttu-id="94eed-113">테 넌 트에 대 한 hello 응용 프로그램 프록시 서비스 인스턴스는 선택 하거나 동일한 hello에서 만든 응용 프로그램 프록시를 사용 하도록 설정 하면 Azure AD 테 넌 트 또는 가장 가까운 지역 tooit hello와 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-113">When you enable Application Proxy, hello Application Proxy service instances for your tenant are chosen or created in hello same region as your Azure AD tenant, or hello closest region tooit.</span></span>

<span data-ttu-id="94eed-114">예를 들어, EU (유럽 연합) hello Azure AD 테 넌 트의 영역을 사용 하는 경우 모든 응용 프로그램 프록시 커넥터 hello EU에서에서 Azure 데이터 센터에서 서비스 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-114">For example, if your Azure AD tenant’s region is hello European Union (EU), all your Application Proxy connectors use service instances in Azure datacenters in hello EU.</span></span> <span data-ttu-id="94eed-115">사용자가 액세스 응용 프로그램을 게시할 때는 트래픽을이 위치에 hello 응용 프로그램 프록시 서비스 인스턴스를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-115">When your users access published applications, their traffic goes through hello Application Proxy service instances in this location.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="94eed-116">대기 시간 단축을 위한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="94eed-116">Considerations for reducing latency</span></span>

<span data-ttu-id="94eed-117">모든 프록시 솔루션은 네트워크 연결에 대기 시간을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="94eed-118">프록시 또는 VPN 솔루션을 설정 하면 원격 액세스 솔루션으로에 관계 없이 항상 지 원하는 서버 hello 연결 tooinside 회사 네트워크의 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling hello connection tooinside your corporate network.</span></span>

<span data-ttu-id="94eed-119">조직은 일반적으로 자신의 경계 네트워크에 서버 끝점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-119">Organizations typically include server endpoints in their perimeter network.</span></span> <span data-ttu-id="94eed-120">그러나 Azure AD 응용 프로그램 프록시 트래픽 흐름 hello 클라우드에서 hello 프록시 서비스를 통해 hello 커넥터 회사 네트워크에 있는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-120">With Azure AD Application Proxy, however, traffic flows through hello proxy service in hello cloud while hello connectors reside on your corporate network.</span></span> <span data-ttu-id="94eed-121">경계 네트워크는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-121">No perimeter network is required.</span></span>

<span data-ttu-id="94eed-122">hello 다음 섹션에는 대기 시간을 더욱 줄일 추가 제안 toohelp을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-122">hello next sections contain additional suggestions toohelp you reduce latency even further.</span></span> 

### <a name="connector-placement"></a><span data-ttu-id="94eed-123">커넥터 배치</span><span class="sxs-lookup"><span data-stu-id="94eed-123">Connector placement</span></span>

<span data-ttu-id="94eed-124">응용 프로그램 프록시는 테 넌 트의 현재 위치에 따라 인스턴스 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-124">Application Proxy chooses hello location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="94eed-125">그러나 얻게 toodecide tooinstall hello 커넥터를 제공 전원 toodefine hello 대기 시간 특징의 네트워크 트래픽 hello 위치.</span><span class="sxs-lookup"><span data-stu-id="94eed-125">However, you get toodecide where tooinstall hello connector, giving you hello power toodefine hello latency characteristics of your network traffic.</span></span>

<span data-ttu-id="94eed-126">Hello 응용 프로그램 프록시 서비스를 설정할 때 다음 질문 hello를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-126">When setting up hello Application Proxy service, ask hello following questions:</span></span>

* <span data-ttu-id="94eed-127">Hello 앱 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="94eed-127">Where is hello app located?</span></span>
* <span data-ttu-id="94eed-128">대부분의 사용자가 있는 hello 앱에 액세스 하는 어디 입니까?</span><span class="sxs-lookup"><span data-stu-id="94eed-128">Where are most users who access hello app located?</span></span>
* <span data-ttu-id="94eed-129">Hello 응용 프로그램 프록시 인스턴스 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="94eed-129">Where is hello Application Proxy instance located?</span></span>
* <span data-ttu-id="94eed-130">이미 Azure express 경로 또는 유사한 VPN과 같은 설정 하는 전용된 네트워크 연결 tooAzure 센터?</span><span class="sxs-lookup"><span data-stu-id="94eed-130">Do you already have a dedicated network connection tooAzure datacenters set up, like Azure ExpressRoute or a similar VPN?</span></span>

<span data-ttu-id="94eed-131">hello 커넥터와가 모두 Azure 응용 프로그램 (2 단계와 3 단계에서 hello 트래픽 흐름 다이어그램) toocommunicate, 하므로 hello 커넥터 영향을 줌 hello 대기 시간의 두 가지 연결의 배치를 hello 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-131">hello connector has toocommunicate with both Azure and your applications (steps 2 and 3 in hello Traffic flow diagram), so hello placement of hello connector affects hello latency of those two connections.</span></span> <span data-ttu-id="94eed-132">Hello 커넥터의 hello 배치를 평가할 때는 유의 hello 지점 다음에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94eed-132">When evaluating hello placement of hello connector, keep in mind hello following points:</span></span>

* <span data-ttu-id="94eed-133">Single sign on에 대 한 Kerberos 제한 위임 toouse KCD ()를 원하는 경우 hello 커넥터 시야 tooa 데이터 센터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-133">If you want toouse Kerberos constrained delegation (KCD) for single sign-on, then hello connector needs a line of sight tooa datacenter.</span></span> <span data-ttu-id="94eed-134">또한 hello 커넥터 서버 toobe 도메인에 가입 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-134">Additionally, hello connector server needs toobe domain joined.</span></span>  
* <span data-ttu-id="94eed-135">의심에서 hello 커넥터 자세히 toohello 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-135">When in doubt, install hello connector closer toohello application.</span></span>

### <a name="general-approach-toominimize-latency"></a><span data-ttu-id="94eed-136">일반적인 방법 toominimize 대기 시간</span><span class="sxs-lookup"><span data-stu-id="94eed-136">General approach toominimize latency</span></span>

<span data-ttu-id="94eed-137">각 네트워크 연결을 최적화 하 여 hello 종단 간 트래픽의 hello 대기 시간을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-137">You can minimize hello latency of hello end-to-end traffic by optimizing each network connection.</span></span> <span data-ttu-id="94eed-138">각 연결은 다음을 통해 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-138">Each connection can be optimized by:</span></span>

* <span data-ttu-id="94eed-139">Hello 홉의 양쪽 hello hello 간격을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-139">Reducing hello distance between hello two ends of hello hop.</span></span>
* <span data-ttu-id="94eed-140">적합 한 네트워크 tootraverse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-140">Choosing hello right network tootraverse.</span></span> <span data-ttu-id="94eed-141">예를 들어 hello 아닌 개인 네트워크를 통과 공용 인터넷 빠를 수 있습니다, 때문 toodedicated 링크.</span><span class="sxs-lookup"><span data-stu-id="94eed-141">For example, traversing a private network rather than hello public Internet may be faster, due toodedicated links.</span></span>

<span data-ttu-id="94eed-142">회사 네트워크와 Azure 간 VPN 또는 express 경로 전용된 링크를 설정한 경우 toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-142">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want toouse that.</span></span>

## <a name="focus-your-optimization-strategy"></a><span data-ttu-id="94eed-143">최적화 전략에 집중</span><span class="sxs-lookup"><span data-stu-id="94eed-143">Focus your optimization strategy</span></span>

<span data-ttu-id="94eed-144">거의 사용자와 응용 프로그램 프록시 서비스 hello 간의 toocontrol hello 연결을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-144">There's little that you can do toocontrol hello connection between your users and hello Application Proxy service.</span></span> <span data-ttu-id="94eed-145">사용자는 홈 네트워크, 인터넷 카페 또는 다른 국가에서 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-145">Users may access your apps from a home network, a coffee shop, or a different country.</span></span> <span data-ttu-id="94eed-146">대신, hello 응용 프로그램 프록시 서비스 toohello 응용 프로그램 프록시 커넥터 toohello 앱의 hello 연결을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-146">Instead, you can optimize hello connections from hello Application Proxy service toohello Application Proxy connectors toohello apps.</span></span> <span data-ttu-id="94eed-147">사용자 환경에서 패턴을 따른 hello를 통합 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-147">Consider incorporating hello following patterns in your environment.</span></span>

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a><span data-ttu-id="94eed-148">패턴 1: Put hello 커넥터 닫기 toohello 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="94eed-148">Pattern 1: Put hello connector close toohello application</span></span>

<span data-ttu-id="94eed-149">현재 위치 hello 커넥터 닫기 toohello에서에서 대상 응용 프로그램 hello 고객 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-149">Place hello connector close toohello target application in hello customer network.</span></span> <span data-ttu-id="94eed-150">이 구성은 hello 커넥터와 응용 프로그램 닫기 있으므로 hello 토폴로지 다이어그램에서 3 단계를 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-150">This configuration minimizes step 3 in hello topography diagram, because hello connector and application are close.</span></span> 

<span data-ttu-id="94eed-151">커넥터 시야 toohello 도메인 컨트롤러를 필요한 경우이 패턴은 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-151">If your connector needs a line of sight toohello domain controller, then this pattern is advantageous.</span></span> <span data-ttu-id="94eed-152">대부분의 시나리오에 적합하기 때문에 대부분의 고객이 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-152">Most of our customers use this pattern, because it works well for most scenarios.</span></span> <span data-ttu-id="94eed-153">이 패턴 hello 서비스 사이 hello 커넥터 패턴 2 toooptimize 트래픽을와 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-153">This pattern can also be combined with pattern 2 toooptimize traffic between hello service and hello connector.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="94eed-154">패턴 2: 공용 피어링이 있는 ExpressRoute 활용</span><span class="sxs-lookup"><span data-stu-id="94eed-154">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="94eed-155">ExpressRoute를 사용 하 여 공용 피어 링 설정를 설정한 경우에 응용 프로그램 프록시 커넥터 hello 사이의 트래픽에 대 한 hello 더 빠른 ExpressRoute 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-155">If you have ExpressRoute set up with public peering, you can use hello faster ExpressRoute connection for traffic between Application Proxy and hello connector.</span></span> <span data-ttu-id="94eed-156">닫기 toohello 응용 프로그램 네트워크에 여전히 hello 커넥터는입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-156">hello connector is still on your network, close toohello app.</span></span>

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="94eed-157">패턴 3: 개인 피어링이 있는 ExpressRoute 활용</span><span class="sxs-lookup"><span data-stu-id="94eed-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="94eed-158">Azure 및 회사 네트워크 간에 개인 피어링이 있는 전용 VPN 또는 ExpressRoute를 설정한 경우 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="94eed-159">이 구성에서는 Azure의 hello 가상 네트워크 hello 회사 네트워크의 확장 기능으로 일반적으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-159">In this configuration, hello virtual network in Azure is typically considered as an extension of hello corporate network.</span></span> <span data-ttu-id="94eed-160">따라서 hello Azure 데이터 센터에에서 hello 커넥터를 설치 하 고 여전히 hello 커넥터 응용 프로그램 연결의 hello 짧은 대기 시간 요구 사항을 충족 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-160">So you can install hello connector in hello Azure datacenter, and still satisfy hello low latency requirements of hello connector-to-app connection.</span></span>

<span data-ttu-id="94eed-161">트래픽은 전용 연결을 통해 전송되므로 대기 시간에 나쁜 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-161">Latency is not compromised because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="94eed-162">또한 hello 커넥터 Azure 데이터 센터 닫기 tooyour Azure AD 테 넌 트 위치에에서 설치 되어 향상 된 응용 프로그램 프록시 커넥터에 서비스 대기 시간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-162">You also get improved Application Proxy service-to-connector latency because hello connector is installed in an Azure datacenter close tooyour Azure AD tenant location.</span></span>

![Azure 데이터 센터 내에 설치된 커넥터를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="94eed-164">다른 방법</span><span class="sxs-lookup"><span data-stu-id="94eed-164">Other approaches</span></span>

<span data-ttu-id="94eed-165">이 문서의 hello 핵심은 커넥터 배치를 hello 응용 프로그램 tooget 더 나은 대기 시간 특성의 hello 배치를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-165">Although hello focus of this article is connector placement, you can also change hello placement of hello application tooget better latency characteristics.</span></span>

<span data-ttu-id="94eed-166">조직은 더욱 더 네트워크를 호스티드 환경으로 이동하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-166">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="94eed-167">이렇게 하면 사용자 tooplace 자신의 회사 네트워크의 일부 이기도 고 여전히 hello 도메인 내에서 호스트 된 환경에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-167">This enables them tooplace their apps in a hosted environment that is also part of their corporate network, and still be within hello domain.</span></span> <span data-ttu-id="94eed-168">이 경우 hello 이전 섹션에서에서 설명한 hello 패턴에 적용 된 toohello 새 응용 프로그램 위치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-168">In this case, hello patterns discussed in hello preceding sections can be applied toohello new application location.</span></span> <span data-ttu-id="94eed-169">이 옵션을 고려하는 경우 [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94eed-169">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

<span data-ttu-id="94eed-170">또한, 커넥터를 사용 하 여 구성 고려 [커넥터 그룹](active-directory-application-proxy-connectors.md) 다른 위치와 네트워크에 있는 tootarget 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-170">Additionally, consider organizing your connectors using [connector groups](active-directory-application-proxy-connectors.md) tootarget apps that are in different locations and networks.</span></span> 

## <a name="common-use-cases"></a><span data-ttu-id="94eed-171">일반 사용 예</span><span class="sxs-lookup"><span data-stu-id="94eed-171">Common use cases</span></span>

<span data-ttu-id="94eed-172">이 섹션에서는 몇 가지 일반적인 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-172">In this section, we walk through a few common scenarios.</span></span> <span data-ttu-id="94eed-173">Azure AD 테 넌 트 해당 hello 가정 (및 그에 따른 프록시 서비스 끝점) hello United States (US)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-173">Assume that hello Azure AD tenant (and therefore proxy service endpoint) is located in hello United States (US).</span></span> <span data-ttu-id="94eed-174">hello 설명에서 이러한 고려 사항을 사용 사례 hello 전 세계 tooother 영역에도 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-174">hello considerations discussed in these use cases also apply tooother regions around hello globe.</span></span>

<span data-ttu-id="94eed-175">이러한 시나리오에서는 각 연결을 "홉"으로 지칭하고 보다 쉬운 이해를 위해 번호를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-175">For these scenarios, we call each connection a "hop" and number them for easier discussion:</span></span>

- <span data-ttu-id="94eed-176">**1 홉**: 사용자 toohello 응용 프로그램 프록시 서비스</span><span class="sxs-lookup"><span data-stu-id="94eed-176">**Hop 1**: User toohello Application Proxy service</span></span>
- <span data-ttu-id="94eed-177">**2 홉**: 응용 프로그램 프록시 서비스 toohello 응용 프로그램 프록시 커넥터</span><span class="sxs-lookup"><span data-stu-id="94eed-177">**Hop 2**: Application Proxy service toohello Application Proxy connector</span></span>
- <span data-ttu-id="94eed-178">**3 홉**: 응용 프로그램 프록시 커넥터 toohello 대상 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="94eed-178">**Hop 3**: Application Proxy connector toohello target application</span></span> 

### <a name="use-case-1"></a><span data-ttu-id="94eed-179">사용 사례 1</span><span class="sxs-lookup"><span data-stu-id="94eed-179">Use case 1</span></span>

<span data-ttu-id="94eed-180">**시나리오:** hello 앱은 hello에서 조직의 네트워크에서 US, hello에 있는 사용자와 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-180">**Scenario:** hello app is in an organization's network in hello US, with users in hello same region.</span></span> <span data-ttu-id="94eed-181">Express 경로 또는 VPN 없습니다 hello Azure 데이터 센터 및 회사 네트워크 hello 사이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-181">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="94eed-182">**권장 사항:** 수행 패턴 1, hello 이전 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-182">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> <span data-ttu-id="94eed-183">대기 시간 개선을 위해 필요한 경우 ExpressRoute를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-183">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="94eed-184">이것은 단순한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-184">This is a simple pattern.</span></span> <span data-ttu-id="94eed-185">Hello 커넥터 hello 앱 근처에 배치 하 여 3 홉을 최적화 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-185">You optimize hop 3 by placing hello connector near hello app.</span></span> <span data-ttu-id="94eed-186">일반적으로 hello 커넥터 시야 toohello 앱과 toohello datacenter tooperform KCD 작업에 설치 되어 있으므로 자연 스러운 선택 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-186">This is also a natural choice, because hello connector typically is installed with line of sight toohello app and toohello datacenter tooperform KCD operations.</span></span>

![사용자, 프록시, 커넥터 및 응용 프로그램은 모두 hello US를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="94eed-188">사용 사례 2</span><span class="sxs-lookup"><span data-stu-id="94eed-188">Use case 2</span></span>

<span data-ttu-id="94eed-189">**시나리오:** hello 앱은 hello에서 조직의 네트워크에서 US, 전역적으로 분산 된 사용자와 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-189">**Scenario:** hello app is in an organization's network in hello US, with users spread out globally.</span></span> <span data-ttu-id="94eed-190">Express 경로 또는 VPN 없습니다 hello Azure 데이터 센터 및 회사 네트워크 hello 사이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-190">No ExpressRoute or VPN exists between hello Azure datacenter and hello corporate network.</span></span>

<span data-ttu-id="94eed-191">**권장 사항:** 수행 패턴 1, hello 이전 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-191">**Recommendation:** Follow pattern 1, explained in hello previous section.</span></span> 

<span data-ttu-id="94eed-192">다시 hello 일반적인 방법은 toooptimize 홉 3, hello 커넥터 hello 앱 근처에 배치 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-192">Again, hello common pattern is toooptimize hop 3, where you place hello connector near hello app.</span></span> <span data-ttu-id="94eed-193">홉 3 일반적으로 비용이 많이 들지 않습니다, 내에서 동일한 hello 경우 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-193">Hop 3 is not typically expensive, if it is all within hello same region.</span></span> <span data-ttu-id="94eed-194">그러나 hello 전 세계 사용자 hello 미국에서에서 hello 응용 프로그램 프록시 인스턴스에 액세스 해야 하기 때문에 1 홉 hello 사용자가 인지에 따라 비용이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-194">However, hop 1 can be more expensive depending on where hello user is, because users across hello world must access hello Application Proxy instance in hello US.</span></span> <span data-ttu-id="94eed-195">모든 프록시 솔루션은 전 세계에 분산된 사용자에 따라 유사한 특성을 포함한다는 것에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-195">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![사용자가 전역으로 분산 되어 하지만 hello 프록시 커넥터를 앱에에서는, 및 hello US를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="94eed-197">사용 사례 3</span><span class="sxs-lookup"><span data-stu-id="94eed-197">Use case 3</span></span>

<span data-ttu-id="94eed-198">**시나리오:** hello에서 조직 네트워크의 hello 앱은 US입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-198">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="94eed-199">회사 네트워크를 Azure와 hello 사이 공용 피어 링 express 경로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-199">ExpressRoute with public peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="94eed-200">**권장 사항:** 1 및 2를 hello 이전 섹션에서 설명한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-200">**Recommendation:** Follow patterns 1 and 2, explained in hello previous section.</span></span>

<span data-ttu-id="94eed-201">먼저, 가능한 toohello 응용 프로그램으로 가까운 hello 커넥터를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-201">First, place hello connector as close as possible toohello app.</span></span> <span data-ttu-id="94eed-202">그런 다음 hello 시스템 홉 2에 대 한 express 경로 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-202">Then, hello system automatically uses ExpressRoute for hop 2.</span></span> 

<span data-ttu-id="94eed-203">Hello ExpressRoute 연결을 사용 하는 공용 피어 링 하는 경우 해당 링크를 통해 hello 트래픽 hello 프록시와 hello 커넥터 간에 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-203">If hello ExpressRoute link is using public peering, hello traffic between hello proxy and hello connector flows over that link.</span></span> <span data-ttu-id="94eed-204">홉 2는 대기 시간을 최적화하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-204">Hop 2 has optimized latency.</span></span>

![Hello 프록시 사이의 커넥터 express 경로 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="94eed-206">사용 사례 4</span><span class="sxs-lookup"><span data-stu-id="94eed-206">Use case 4</span></span>

<span data-ttu-id="94eed-207">**시나리오:** hello에서 조직 네트워크의 hello 앱은 US입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-207">**Scenario:** hello app is in an organization's network in hello US.</span></span> <span data-ttu-id="94eed-208">회사 네트워크를 Azure와 hello 사이 개인 피어 링 express 경로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-208">ExpressRoute with private peering exists between Azure and hello corporate network.</span></span>

<span data-ttu-id="94eed-209">**권장 사항:** 수행 패턴 3, hello 이전 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-209">**Recommendation:** Follow pattern 3, explained in hello previous section.</span></span>

<span data-ttu-id="94eed-210">Hello 커넥터 hello 개인 피어 링 express 경로 통해 연결 된 toohello 회사 네트워크를 Azure 데이터 센터에에서 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-210">Place hello connector in hello Azure datacenter that is connected toohello corporate network through ExpressRoute private peering.</span></span> 

<span data-ttu-id="94eed-211">hello 커넥터 hello Azure 데이터 센터에에서 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-211">hello connector can be placed in hello Azure datacenter.</span></span> <span data-ttu-id="94eed-212">Hello 커넥터 여전히에 있으므로 시야 toohello 응용 프로그램 및 hello 개인 네트워크를 통해 데이터 센터 hello 홉 3 최적화 된 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-212">Since hello connector still has a line of sight toohello application and hello datacenter through hello private network, hop 3 remains optimized.</span></span> <span data-ttu-id="94eed-213">또한 홉 2는 더욱 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-213">In addition, hop 2 is optimized further.</span></span>

![Hello 커넥터와 응용 프로그램 간에 Azure 데이터 센터 및 express 경로에 hello 커넥터를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="94eed-215">사용 사례 5</span><span class="sxs-lookup"><span data-stu-id="94eed-215">Use case 5</span></span>

<span data-ttu-id="94eed-216">**시나리오:** hello 응용 프로그램 프록시 인스턴스와 사용자가 대부분 hello 사용 하 여 hello EU에서에서 조직 네트워크의 hello 앱은 US입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-216">**Scenario:** hello app is in an organization's network in hello EU, with hello Application Proxy instance and most users in hello US.</span></span>

<span data-ttu-id="94eed-217">**권장 사항:** hello 앱 가까운 곳 hello 커넥터입니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-217">**Recommendation:** Place hello connector near hello app.</span></span> <span data-ttu-id="94eed-218">미국 사용자가 toobe hello에서 발생 하는 응용 프로그램 프록시 인스턴스를 액세스 하기 때문에 동일한 지역 홉 1 가격이 너무 비쌉니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-218">Because US users are accessing an Application Proxy instance that happens toobe in hello same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="94eed-219">홉 3이 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-219">Hop 3 is optimized.</span></span> <span data-ttu-id="94eed-220">ExpressRoute toooptimize 홉 2를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-220">Consider using ExpressRoute toooptimize hop 2.</span></span> 

![Hello, 미국 hello 커넥터와 hello EU에서에서 응용 프로그램에서에서 사용자와 프록시를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="94eed-222">이 상황에서 다른 한 가지 변수를 사용하도록 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-222">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="94eed-223">대부분 조직의 사용자에 게 hello에 있는 경우 hello 우리 가능성을 네트워크 확장 toohello US도 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-223">If most users in hello organization are in hello US, then chances are that your network extends toohello US as well.</span></span> <span data-ttu-id="94eed-224">Hello, 미국에에서 hello 커넥터를 배치 하 고 hello EU 전용 hello 내부 회사 네트워크 줄 toohello 응용 프로그램 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-224">Place hello connector in hello US, and use hello dedicated internal corporate network line toohello application in hello EU.</span></span> <span data-ttu-id="94eed-225">이 방식으로 홉 2와 3이 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="94eed-225">This way hops 2 and 3 are optimized.</span></span>

![Hello 미국, 유럽 hello에서 응용 프로그램에서에서 사용자, 프록시 및 연결선을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="94eed-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94eed-227">Next steps</span></span>

- [<span data-ttu-id="94eed-228">응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="94eed-228">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="94eed-229">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="94eed-229">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="94eed-230">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="94eed-230">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="94eed-231">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="94eed-231">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
