---
title: "Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항 | Microsoft Docs"
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
ms.openlocfilehash: 11244e0044eef8441e3a37ab8aeff0da30dacdb8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a><span data-ttu-id="cd441-103">Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항</span><span class="sxs-lookup"><span data-stu-id="cd441-103">Network topology considerations when using Azure Active Directory Application Proxy</span></span>

<span data-ttu-id="cd441-104">이 문서에서는 응용 프로그램을 원격으로 게시 및 액세스하기 위해 Azure AD(Azure Active Directory) 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-104">This article explains network topology considerations when using Azure Active Directory (Azure AD) Application Proxy for publishing and accessing your applications remotely.</span></span>

## <a name="traffic-flow"></a><span data-ttu-id="cd441-105">트래픽 흐름</span><span class="sxs-lookup"><span data-stu-id="cd441-105">Traffic flow</span></span>

<span data-ttu-id="cd441-106">Azure AD 응용 프로그램 프록시를 통해 응용 프로그램을 게시할 때 사용자에게서 응용 프로그램으로 이동하는 트래픽은 다음 3가지 연결을 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-106">When an application is published through Azure AD Application Proxy, traffic from the users to the applications flows through three connections:</span></span>

1. <span data-ttu-id="cd441-107">사용자가 Azure의 Azure AD 응용 프로그램 프록시 공용 끝점에 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-107">The user connects to the Azure AD Application Proxy service public endpoint on Azure</span></span>
2. <span data-ttu-id="cd441-108">응용 프로그램 프록시 서비스에서 응용 프로그램 프록시 커넥터에 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-108">The Application Proxy service connects to the Application Proxy connector</span></span>
3. <span data-ttu-id="cd441-109">응용 프로그램 프록시 커넥터에서 대상 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-109">The Application Proxy connector connects to the target application</span></span>

![대상 응용 프로그램에 사용자의 트래픽 흐름을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a><span data-ttu-id="cd441-111">테넌트 위치 및 응용 프로그램 프록시 서비스</span><span class="sxs-lookup"><span data-stu-id="cd441-111">Tenant location and Application Proxy service</span></span>

<span data-ttu-id="cd441-112">Azure AD 테넌트에 등록할 때 테넌트의 지역은 지정한 국가에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-112">When you sign up for an Azure AD tenant, the region of your tenant is determined by the country you specify.</span></span> <span data-ttu-id="cd441-113">응용 프로그램 프록시를 사용하도록 설정하면 테넌트에 대한 응용 프로그램 프록시 서비스 인스턴스가 Azure AD 테넌트와 동일한 지역이나 가장 가까운 지역에서 선택되거나 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-113">When you enable Application Proxy, the Application Proxy service instances for your tenant are chosen or created in the same region as your Azure AD tenant, or the closest region to it.</span></span>

<span data-ttu-id="cd441-114">예를 들어, Azure AD 테넌트의 영역이 EU인 경우 모든 응용 프로그램 프록시 커넥터는 EU에 있는 Azure 데이터 센터의 서비스 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-114">For example, if your Azure AD tenant’s region is the European Union (EU), all your Application Proxy connectors use service instances in Azure datacenters in the EU.</span></span> <span data-ttu-id="cd441-115">사용자가 게시된 응용 프로그램에 액세스할 때 해당 트래픽은 이러한 위치의 응용 프로그램 프록시 서비스 인스턴스를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-115">When your users access published applications, their traffic goes through the Application Proxy service instances in this location.</span></span>

## <a name="considerations-for-reducing-latency"></a><span data-ttu-id="cd441-116">대기 시간 단축을 위한 고려 사항</span><span class="sxs-lookup"><span data-stu-id="cd441-116">Considerations for reducing latency</span></span>

<span data-ttu-id="cd441-117">모든 프록시 솔루션은 네트워크 연결에 대기 시간을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-117">All proxy solutions introduce latency into your network connection.</span></span> <span data-ttu-id="cd441-118">원격 액세스 솔루션으로 프록시 또는 VPN 솔루션 중 어느 것을 선택하든지 간에 항상 회사 네트워크 내부에 연결을 사용하는 일련의 서버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-118">No matter which proxy or VPN solution you choose as your remote access solution, it always includes a set of servers enabling the connection to inside your corporate network.</span></span>

<span data-ttu-id="cd441-119">조직은 일반적으로 자신의 경계 네트워크에 서버 끝점을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-119">Organizations typically include server endpoints in their perimeter network.</span></span> <span data-ttu-id="cd441-120">그렇지만 Azure AD 응용 프로그램 프록시를 사용할 경우 커넥터는 회사 네트워크에 있으나 트래픽은 클라우드의 프록시 서비스를 통해 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-120">With Azure AD Application Proxy, however, traffic flows through the proxy service in the cloud while the connectors reside on your corporate network.</span></span> <span data-ttu-id="cd441-121">경계 네트워크는 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-121">No perimeter network is required.</span></span>

<span data-ttu-id="cd441-122">다음 섹션에서는 대기 시간을 더 줄이는 데 도움이 되는 추가 제안 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-122">The next sections contain additional suggestions to help you reduce latency even further.</span></span> 

### <a name="connector-placement"></a><span data-ttu-id="cd441-123">커넥터 배치</span><span class="sxs-lookup"><span data-stu-id="cd441-123">Connector placement</span></span>

<span data-ttu-id="cd441-124">응용 프로그램 프록시는 테넌트 위치에 따라 사용자의 인스턴스 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-124">Application Proxy chooses the location of instances for you, based on your tenant location.</span></span> <span data-ttu-id="cd441-125">그러나 커넥터를 설치할 위치를 결정하면 네트워크 트래픽의 대기 시간 특성을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-125">However, you get to decide where to install the connector, giving you the power to define the latency characteristics of your network traffic.</span></span>

<span data-ttu-id="cd441-126">응용 프로그램 프록시 서비스를 설정할 때 다음과 같은 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-126">When setting up the Application Proxy service, ask the following questions:</span></span>

* <span data-ttu-id="cd441-127">앱은 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="cd441-127">Where is the app located?</span></span>
* <span data-ttu-id="cd441-128">앱에 액세스하는 대부분의 사용자는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="cd441-128">Where are most users who access the app located?</span></span>
* <span data-ttu-id="cd441-129">응용 프로그램 프록시 인스턴스는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="cd441-129">Where is the Application Proxy instance located?</span></span>
* <span data-ttu-id="cd441-130">Azure ExpressRoute 또는 유사한 VPN처럼 Azure 데이터 센터 설정에 대한 기존의 전용 네트워크 연결이 있나요?</span><span class="sxs-lookup"><span data-stu-id="cd441-130">Do you already have a dedicated network connection to Azure datacenters set up, like Azure ExpressRoute or a similar VPN?</span></span>

<span data-ttu-id="cd441-131">커넥터는 Azure 및 응용 프로그램과 통신해야 하므로(트래픽 흐름 다이어그램 2단계 및 3단계) 커넥터의 배치는 이러한 두 연결의 대기 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-131">The connector has to communicate with both Azure and your applications (steps 2 and 3 in the Traffic flow diagram), so the placement of the connector affects the latency of those two connections.</span></span> <span data-ttu-id="cd441-132">커넥터의 배치를 평가할 때 다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="cd441-132">When evaluating the placement of the connector, keep in mind the following points:</span></span>

* <span data-ttu-id="cd441-133">Single Sign-On에 대해 KCD(Kerberos 제한 위임)을 사용하려는 경우 커넥터에서 데이터 센터에 대한 가시성을 확보해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-133">If you want to use Kerberos constrained delegation (KCD) for single sign-on, then the connector needs a line of sight to a datacenter.</span></span> <span data-ttu-id="cd441-134">또한 커넥터 서버는 도메인에 가입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-134">Additionally, the connector server needs to be domain joined.</span></span>  
* <span data-ttu-id="cd441-135">확실하지 않은 경우 응용 프로그램에 더 가깝게 커넥터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-135">When in doubt, install the connector closer to the application.</span></span>

### <a name="general-approach-to-minimize-latency"></a><span data-ttu-id="cd441-136">대기 시간을 최소화하는 일반적인 방법</span><span class="sxs-lookup"><span data-stu-id="cd441-136">General approach to minimize latency</span></span>

<span data-ttu-id="cd441-137">각 네트워크 연결을 최적화하여 종단 간 트래픽의 대기 시간을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-137">You can minimize the latency of the end-to-end traffic by optimizing each network connection.</span></span> <span data-ttu-id="cd441-138">각 연결은 다음을 통해 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-138">Each connection can be optimized by:</span></span>

* <span data-ttu-id="cd441-139">홉의 두 끝 사이의 거리 줄이기</span><span class="sxs-lookup"><span data-stu-id="cd441-139">Reducing the distance between the two ends of the hop.</span></span>
* <span data-ttu-id="cd441-140">트래버스하기 적합한 네트워크 선택.</span><span class="sxs-lookup"><span data-stu-id="cd441-140">Choosing the right network to traverse.</span></span> <span data-ttu-id="cd441-141">예를 들어 공용 인터넷보다 개인 네트워크를 트래버스하는 것이 전용 링크가 있으므로 더 빠를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-141">For example, traversing a private network rather than the public Internet may be faster, due to dedicated links.</span></span>

<span data-ttu-id="cd441-142">Azure 및 회사 네트워크 간에 전용 VPN 또는 ExpressRoute가 있는 경우 다음을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-142">If you have a dedicated VPN or ExpressRoute link between Azure and your corporate network, you may want to use that.</span></span>

## <a name="focus-your-optimization-strategy"></a><span data-ttu-id="cd441-143">최적화 전략에 집중</span><span class="sxs-lookup"><span data-stu-id="cd441-143">Focus your optimization strategy</span></span>

<span data-ttu-id="cd441-144">사용자와 응용 프로그램 프록시 서비스 간의 연결을 제어할 수 있는 방법은 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-144">There's little that you can do to control the connection between your users and the Application Proxy service.</span></span> <span data-ttu-id="cd441-145">사용자는 홈 네트워크, 인터넷 카페 또는 다른 국가에서 앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-145">Users may access your apps from a home network, a coffee shop, or a different country.</span></span> <span data-ttu-id="cd441-146">대신 응용 프로그램 프록시 서비스에서 응용 프로그램 프록시 커넥터로, 그런 다음 앱으로 연결을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-146">Instead, you can optimize the connections from the Application Proxy service to the Application Proxy connectors to the apps.</span></span> <span data-ttu-id="cd441-147">사용자 환경에서 다음과 같은 패턴을 통합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-147">Consider incorporating the following patterns in your environment.</span></span>

### <a name="pattern-1-put-the-connector-close-to-the-application"></a><span data-ttu-id="cd441-148">패턴 1: 커넥터를 응용 프로그램 가까이에 배치</span><span class="sxs-lookup"><span data-stu-id="cd441-148">Pattern 1: Put the connector close to the application</span></span>

<span data-ttu-id="cd441-149">커넥터를 고객 네트워크의 대상 응용 프로그램 가까이에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-149">Place the connector close to the target application in the customer network.</span></span> <span data-ttu-id="cd441-150">이 구성은 커넥터와 응용 프로그램이 가까이 있기 때문에 토폴로지 다이어그램에서 3단계를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-150">This configuration minimizes step 3 in the topography diagram, because the connector and application are close.</span></span> 

<span data-ttu-id="cd441-151">도메인 컨트롤러에 대한 가시선이 커넥터에 필요한 경우 이 패턴이 유리합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-151">If your connector needs a line of sight to the domain controller, then this pattern is advantageous.</span></span> <span data-ttu-id="cd441-152">대부분의 시나리오에 적합하기 때문에 대부분의 고객이 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-152">Most of our customers use this pattern, because it works well for most scenarios.</span></span> <span data-ttu-id="cd441-153">이 패턴을 패턴 2와 조합하여 서비스와 커넥터 사이의 트래픽을 최적화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-153">This pattern can also be combined with pattern 2 to optimize traffic between the service and the connector.</span></span>

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a><span data-ttu-id="cd441-154">패턴 2: 공용 피어링이 있는 ExpressRoute 활용</span><span class="sxs-lookup"><span data-stu-id="cd441-154">Pattern 2: Take advantage of ExpressRoute with public peering</span></span>

<span data-ttu-id="cd441-155">공용 피어링이 있는 ExpressRoute를 설정한 경우 응용 프로그램 프록시와 커넥터 간 트래픽에 대해 더 빨라진 ExpressRoute 연결을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-155">If you have ExpressRoute set up with public peering, you can use the faster ExpressRoute connection for traffic between Application Proxy and the connector.</span></span> <span data-ttu-id="cd441-156">커넥터는 여전히 네트워크에서 앱에 가까운 위치를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-156">The connector is still on your network, close to the app.</span></span>

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a><span data-ttu-id="cd441-157">패턴 3: 개인 피어링이 있는 ExpressRoute 활용</span><span class="sxs-lookup"><span data-stu-id="cd441-157">Pattern 3: Take advantage of ExpressRoute with private peering</span></span>

<span data-ttu-id="cd441-158">Azure 및 회사 네트워크 간에 개인 피어링이 있는 전용 VPN 또는 ExpressRoute를 설정한 경우 다른 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-158">If you have a dedicated VPN or ExpressRoute set up with private peering between Azure and your corporate network, you have another option.</span></span> <span data-ttu-id="cd441-159">이 구성에서는 일반적으로 Azure의 가상 네트워크가 회사 네트워크의 확장으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-159">In this configuration, the virtual network in Azure is typically considered as an extension of the corporate network.</span></span> <span data-ttu-id="cd441-160">따라서 Azure 데이터 센터에 커넥터를 설치할 수 있으며, 커넥터-앱 연결에 낮은 대기 시간 요구 사항을 계속해서 충족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-160">So you can install the connector in the Azure datacenter, and still satisfy the low latency requirements of the connector-to-app connection.</span></span>

<span data-ttu-id="cd441-161">트래픽은 전용 연결을 통해 전송되므로 대기 시간에 나쁜 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-161">Latency is not compromised because traffic is flowing over a dedicated connection.</span></span> <span data-ttu-id="cd441-162">또한 커넥터가 Azure AD 테넌트 위치와 가까운 Azure 데이터 센터에 설치되어 있으므로 응용 프로그램 프록시 서비스와 커넥터 간 대기 시간이 단축됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-162">You also get improved Application Proxy service-to-connector latency because the connector is installed in an Azure datacenter close to your Azure AD tenant location.</span></span>

![Azure 데이터 센터 내에 설치된 커넥터를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a><span data-ttu-id="cd441-164">다른 방법</span><span class="sxs-lookup"><span data-stu-id="cd441-164">Other approaches</span></span>

<span data-ttu-id="cd441-165">이 문서에서는 커넥터 배치를 집중적으로 설명하지만 대기 시간을 개선하기 위해 응용 프로그램의 배치를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-165">Although the focus of this article is connector placement, you can also change the placement of the application to get better latency characteristics.</span></span>

<span data-ttu-id="cd441-166">조직은 더욱 더 네트워크를 호스티드 환경으로 이동하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-166">Increasingly, organizations are moving their networks into hosted environments.</span></span> <span data-ttu-id="cd441-167">이렇게 함으로써 회사 네트워크에 포함되는 호스티드 환경에 앱을 배치할 수 있으며 계속 도메인 내에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-167">This enables them to place their apps in a hosted environment that is also part of their corporate network, and still be within the domain.</span></span> <span data-ttu-id="cd441-168">이 경우 이전 섹션에서 설명한 패턴을 새 응용 프로그램 위치에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-168">In this case, the patterns discussed in the preceding sections can be applied to the new application location.</span></span> <span data-ttu-id="cd441-169">이 옵션을 고려하는 경우 [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cd441-169">If you're considering this option, see [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).</span></span>

<span data-ttu-id="cd441-170">또한 다른 위치 및 네트워크에 있는 대상 앱에 [커넥터 그룹](active-directory-application-proxy-connectors.md)을 사용하여 커넥터를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-170">Additionally, consider organizing your connectors using [connector groups](active-directory-application-proxy-connectors.md) to target apps that are in different locations and networks.</span></span> 

## <a name="common-use-cases"></a><span data-ttu-id="cd441-171">일반 사용 예</span><span class="sxs-lookup"><span data-stu-id="cd441-171">Common use cases</span></span>

<span data-ttu-id="cd441-172">이 섹션에서는 몇 가지 일반적인 시나리오를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-172">In this section, we walk through a few common scenarios.</span></span> <span data-ttu-id="cd441-173">Azure AD 테넌트(즉, 프록시 서비스 끝점)가 미국에 위치한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-173">Assume that the Azure AD tenant (and therefore proxy service endpoint) is located in the United States (US).</span></span> <span data-ttu-id="cd441-174">이러한 사용 사례에서 설명한 고려 사항은 전 세계 다른 지역에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-174">The considerations discussed in these use cases also apply to other regions around the globe.</span></span>

<span data-ttu-id="cd441-175">이러한 시나리오에서는 각 연결을 "홉"으로 지칭하고 보다 쉬운 이해를 위해 번호를 매깁니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-175">For these scenarios, we call each connection a "hop" and number them for easier discussion:</span></span>

- <span data-ttu-id="cd441-176">**홉 1**: 사용자-응용 프로그램 프록시 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-176">**Hop 1**: User to the Application Proxy service</span></span>
- <span data-ttu-id="cd441-177">**홉 2**: 응용 프로그램 프록시 서비스-응용 프로그램 프록시 커넥터 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-177">**Hop 2**: Application Proxy service to the Application Proxy connector</span></span>
- <span data-ttu-id="cd441-178">**홉 3**: 응용 프로그램 프록시 커넥터-대상 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="cd441-178">**Hop 3**: Application Proxy connector to the target application</span></span> 

### <a name="use-case-1"></a><span data-ttu-id="cd441-179">사용 사례 1</span><span class="sxs-lookup"><span data-stu-id="cd441-179">Use case 1</span></span>

<span data-ttu-id="cd441-180">**시나리오:** 앱이 동일한 지역의 사용자와 함께 미국에 있는 조직의 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-180">**Scenario:** The app is in an organization's network in the US, with users in the same region.</span></span> <span data-ttu-id="cd441-181">Azure 데이터 센터 및 회사 네트워크 간에 ExpressRoute 또는 VPN이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-181">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="cd441-182">**권장 사항:** 이전 섹션에서 설명한 대로 패턴 1을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-182">**Recommendation:** Follow pattern 1, explained in the previous section.</span></span> <span data-ttu-id="cd441-183">대기 시간 개선을 위해 필요한 경우 ExpressRoute를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-183">For improved latency, consider using ExpressRoute, if needed.</span></span>

<span data-ttu-id="cd441-184">이것은 단순한 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-184">This is a simple pattern.</span></span> <span data-ttu-id="cd441-185">커넥터를 앱 가까이에 배치하여 홉 3을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-185">You optimize hop 3 by placing the connector near the app.</span></span> <span data-ttu-id="cd441-186">일반적으로 커넥터는 KCD 작업을 수행하기 위해 앱과 데이터 센터에 대한 시야를 사용하여 설치되므로 자연스러운 선택이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-186">This is also a natural choice, because the connector typically is installed with line of sight to the app and to the datacenter to perform KCD operations.</span></span>

![사용자, 프록시, 커넥터 및 앱이 모두 미국에 있음을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a><span data-ttu-id="cd441-188">사용 사례 2</span><span class="sxs-lookup"><span data-stu-id="cd441-188">Use case 2</span></span>

<span data-ttu-id="cd441-189">**시나리오:** 앱이 전 세계에 분산된 사용자와 함께 미국에 있는 조직의 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-189">**Scenario:** The app is in an organization's network in the US, with users spread out globally.</span></span> <span data-ttu-id="cd441-190">Azure 데이터 센터 및 회사 네트워크 간에 ExpressRoute 또는 VPN이 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-190">No ExpressRoute or VPN exists between the Azure datacenter and the corporate network.</span></span>

<span data-ttu-id="cd441-191">**권장 사항:** 이전 섹션에서 설명한 대로 패턴 1을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-191">**Recommendation:** Follow pattern 1, explained in the previous section.</span></span> 

<span data-ttu-id="cd441-192">일반적인 패턴은 홉 3을 최적화하는 것이며, 이 경우 커넥터를 앱 근처에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-192">Again, the common pattern is to optimize hop 3, where you place the connector near the app.</span></span> <span data-ttu-id="cd441-193">홉 3이 모두 동일한 지역에 있는 경우 일반적으로 비용이 많이 들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-193">Hop 3 is not typically expensive, if it is all within the same region.</span></span> <span data-ttu-id="cd441-194">하지만 전 세계의 사용자가 미국에 있는 응용 프로그램 프록시 인스턴스에 액세스하므로 홉 1은 사용자 위치에 따라 비용이 더 높을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-194">However, hop 1 can be more expensive depending on where the user is, because users across the world must access the Application Proxy instance in the US.</span></span> <span data-ttu-id="cd441-195">모든 프록시 솔루션은 전 세계에 분산된 사용자에 따라 유사한 특성을 포함한다는 것에 주목해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-195">It's worth noting that any proxy solution has similar characteristics regarding users being spread out globally.</span></span>

![사용자는 전 세계에 분포되어 있으나 프록시, 커넥터 및 앱은 미국에 있음을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a><span data-ttu-id="cd441-197">사용 사례 3</span><span class="sxs-lookup"><span data-stu-id="cd441-197">Use case 3</span></span>

<span data-ttu-id="cd441-198">**시나리오:** 앱이 미국에 있는 조직의 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-198">**Scenario:** The app is in an organization's network in the US.</span></span> <span data-ttu-id="cd441-199">공용 피어링이 있는 ExpressRoute는 Azure 및 회사 네트워크 간에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-199">ExpressRoute with public peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="cd441-200">**권장 사항:** 이전 섹션에서 설명한 패턴 1과 2를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-200">**Recommendation:** Follow patterns 1 and 2, explained in the previous section.</span></span>

<span data-ttu-id="cd441-201">먼저 커넥터를 앱에 최대한 가까이 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-201">First, place the connector as close as possible to the app.</span></span> <span data-ttu-id="cd441-202">그런 다음 시스템에서 홉 2에 ExpressRoute를 자동으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-202">Then, the system automatically uses ExpressRoute for hop 2.</span></span> 

<span data-ttu-id="cd441-203">ExpressRoute 링크가 공용 피어링을 사용하는 경우 프록시와 커넥터 간의 트래픽은 해당 링크를 통해 흐르게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-203">If the ExpressRoute link is using public peering, the traffic between the proxy and the connector flows over that link.</span></span> <span data-ttu-id="cd441-204">홉 2는 대기 시간을 최적화하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-204">Hop 2 has optimized latency.</span></span>

![프록시와 커넥터 간 ExpressRoute를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a><span data-ttu-id="cd441-206">사용 사례 4</span><span class="sxs-lookup"><span data-stu-id="cd441-206">Use case 4</span></span>

<span data-ttu-id="cd441-207">**시나리오:** 앱이 미국에 있는 조직의 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-207">**Scenario:** The app is in an organization's network in the US.</span></span> <span data-ttu-id="cd441-208">개인 피어링이 있는 ExpressRoute는 Azure 및 회사 네트워크 간에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-208">ExpressRoute with private peering exists between Azure and the corporate network.</span></span>

<span data-ttu-id="cd441-209">**권장 사항:** 이전 섹션에서 설명한 패턴 3을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-209">**Recommendation:** Follow pattern 3, explained in the previous section.</span></span>

<span data-ttu-id="cd441-210">ExpressRoute 개인 피어링을 통해 회사 네트워크에 연결된 Azure 데이터 센터에 커넥터를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-210">Place the connector in the Azure datacenter that is connected to the corporate network through ExpressRoute private peering.</span></span> 

<span data-ttu-id="cd441-211">커넥터를 Azure 데이터 센터에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-211">The connector can be placed in the Azure datacenter.</span></span> <span data-ttu-id="cd441-212">커넥터가 개인 네트워크를 통해 응용 프로그램 및 데이터 센터에 대한 가시권을 계속 확보하므로 홉 3은 최적화된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-212">Since the connector still has a line of sight to the application and the datacenter through the private network, hop 3 remains optimized.</span></span> <span data-ttu-id="cd441-213">또한 홉 2는 더욱 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-213">In addition, hop 2 is optimized further.</span></span>

![Azure 데이터 센터의 커넥터, 커넥터와 앱 간 ExpressRoute를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a><span data-ttu-id="cd441-215">사용 사례 5</span><span class="sxs-lookup"><span data-stu-id="cd441-215">Use case 5</span></span>

<span data-ttu-id="cd441-216">**시나리오:** 앱은 EU의 조직 네트워크에 있고 응용 프로그램 프록시 인스턴스와 대부분의 사용자는 미국에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-216">**Scenario:** The app is in an organization's network in the EU, with the Application Proxy instance and most users in the US.</span></span>

<span data-ttu-id="cd441-217">**권장 사항:** 커넥터를 앱 가까이 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-217">**Recommendation:** Place the connector near the app.</span></span> <span data-ttu-id="cd441-218">미국 사용자는 동일한 지역에 있는 응용 프로그램 프록시 인스턴스에 액세스하므로 홉 1의 비용은 그다지 비싸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-218">Because US users are accessing an Application Proxy instance that happens to be in the same region, hop 1 is not too expensive.</span></span> <span data-ttu-id="cd441-219">홉 3이 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-219">Hop 3 is optimized.</span></span> <span data-ttu-id="cd441-220">ExpressRoute를 사용하여 홉 2를 최적화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-220">Consider using ExpressRoute to optimize hop 2.</span></span> 

![사용자와 프록시는 미국에 있고 커넥터 및 앱은 EU에 있음을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

<span data-ttu-id="cd441-222">이 상황에서 다른 한 가지 변수를 사용하도록 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-222">You can also consider using one other variant in this situation.</span></span> <span data-ttu-id="cd441-223">조직에 있는 대부분 사용자가 미국에 있는 경우 네트워크가 미국으로도 확장될 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-223">If most users in the organization are in the US, then chances are that your network extends to the US as well.</span></span> <span data-ttu-id="cd441-224">커넥터를 미국에 배치하고, 전용 내부 회사 네트워크 회선을 유럽에 있는 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-224">Place the connector in the US, and use the dedicated internal corporate network line to the application in the EU.</span></span> <span data-ttu-id="cd441-225">이 방식으로 홉 2와 3이 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd441-225">This way hops 2 and 3 are optimized.</span></span>

![사용자, 프록시 및 커넥터는 미국에 있고 앱은 EU에 있음을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a><span data-ttu-id="cd441-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cd441-227">Next steps</span></span>

- [<span data-ttu-id="cd441-228">응용 프로그램 프록시 사용</span><span class="sxs-lookup"><span data-stu-id="cd441-228">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
- [<span data-ttu-id="cd441-229">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="cd441-229">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="cd441-230">조건부 액세스 사용</span><span class="sxs-lookup"><span data-stu-id="cd441-230">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
- [<span data-ttu-id="cd441-231">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="cd441-231">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
