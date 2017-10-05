---
title: "Azure Application Gateway에 대한 질문과 대답 | Microsoft Docs"
description: "이 페이지에서는 Azure Application Gateway에 대한 질문과 대답을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="8926f-103">Application Gateway에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="8926f-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="8926f-104">일반</span><span class="sxs-lookup"><span data-stu-id="8926f-104">General</span></span>

<span data-ttu-id="8926f-105">**Q. Application Gateway란?**</span><span class="sxs-lookup"><span data-stu-id="8926f-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="8926f-106">Azure Application Gateway는 서비스 형태의 ADC(응용 프로그램 전달 컨트롤러)이며 응용 프로그램에 대한 다양한 계층 7 부하 분산 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="8926f-107">Azure에서 완전히 관리되는 고가용성의 확장성 있는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="8926f-108">**Q. Application Gateway에서 지원하는 기능은 어떤 것이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="8926f-109">Application Gateway에서는 SSL 오프로딩 및 종단 간 SSL, 웹 응용 프로그램 방화벽, 쿠키 기반 세션 선호도, URL 경로 기반 라우팅, 다중 사이트 호스팅 등을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="8926f-110">지원되는 기능의 전체 목록은 [Application Gateway 소개](application-gateway-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="8926f-111">**Q. Application Gateway와 Azure Load Balancer 간의 차이는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="8926f-112">Application Gateway는 웹 트래픽(HTTP/HTTPS/WebSocket)에서만 작동하는 7계층 부하 분산 장치로서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="8926f-113">SSL 종료, 쿠키 기반 세션 선호도, 트래픽 부하 분산을 위한 라운드 로빈과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="8926f-114">부하 분산 장치, 계층 4(TCP/UDP)에서 트래픽 부하 분산.</span><span class="sxs-lookup"><span data-stu-id="8926f-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="8926f-115">**Q. Application Gateway에서 지원하는 프로토콜은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="8926f-116">Application Gateway는 HTTP, HTTPS 및 WebSocket을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="8926f-117">**Q. 현재 백 엔드 풀의 일부로 어떤 리소스가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="8926f-118">백 엔드 풀은 NIC, 가상 컴퓨터 확장 집합, 공용 IP, 내부 IP, FQDN(정규화된 도메인 이름) 및 다중 테넌트 백 엔드(예: Azure Web Apps)로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="8926f-119">Application Gateway 백 엔드 풀 멤버는 가용성 집합에 연결되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="8926f-120">백 엔드 풀의 멤버는 IP 연결이 있는 경우 클러스터, 데이터 센터 간 또는 Azure 외부에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="8926f-121">**Q. 어떤 지역에서 서비스를 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="8926f-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="8926f-122">Application Gateway는 Azure 전체의 모든 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="8926f-123">[Azure China](https://www.azure.cn/) 및 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="8926f-124">**Q. 내 구독에 대한 전용 배포인가요? 아니면 고객 간에 공유되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="8926f-125">Application Gateway는 가상 네트워크에서 전용 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="8926f-126">**Q. HTTP->HTTPS 리디렉션이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="8926f-127">리디렉션은 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-127">Redirection is supported.</span></span> <span data-ttu-id="8926f-128">자세한 내용은 [Application Gateway 리디렉션 개요](application-gateway-redirect-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="8926f-129">**Q. 수신기는 어떤 순서로 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="8926f-130">수신기는 표시된 순서대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="8926f-131">이러한 이유로 기본 수신기에서 들어오는 요청과 일치하는 경우 이 요청을 먼저 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="8926f-132">트래픽이 올바른 백 엔드로 라우팅되려면 다중 사이트 수신기를 기본 수신기보다 먼저 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="8926f-133">**Q. Application Gateway의 IP 및 DNS는 어디에서 확인하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="8926f-134">공용 IP 주소를 끝점으로 사용하는 경우 이 정보를 공용 IP 주소 리소스 또는 포털의 Application Gateway에 대한 개요 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="8926f-135">내부 IP 주소는 개요 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="8926f-136">**Q. Application Gateway의 수명 중에 IP 또는 DNS가 변경되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="8926f-137">게이트웨이가 고객에 의해 중지 및 시작된 경우 VIP를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="8926f-138">Application Gateway와 연결된 DNS는 게이트웨이 수명 중에 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="8926f-139">이러한 이유로 CNAME 별칭을 사용하고 Application Gateway의 DNS 주소를 가리키도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="8926f-140">**Q. Application Gateway에서 고정 IP를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="8926f-141">아니요, Application Gateway에서는 고정 공용 IP 주소를 지원하지 않고 고정 내부 IP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="8926f-142">**Q. Application Gateway가 게이트웨이에서 여러 공용 IP를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="8926f-143">Application Gateway에서는 하나의 공용 IP 주소만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="8926f-144">**Q. Application Gateway에서 x-forwarded-for 헤더를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="8926f-145">예, Application Gateway는 백 엔드로 전달되는 요청에 x-forwarded-for, x-forwarded-proto 및 x-forwarded-port 헤더를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="8926f-146">x-forwarded-for 헤더의 형식은 쉼표로 구분된 IP:Port 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="8926f-147">x-forwarded-proto 에 대해 유효한 값은 http 또는 https입니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="8926f-148">X-forwarded-port는 Application Gateway에서 요청이 도달한 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="8926f-149">**Q. Application Gateway를 배포하는 데 얼마의 시간이 걸리나요? Application Gateway가 업데이트되어도 여전히 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="8926f-150">새 Application Gateway 배포 시 프로비전하는 데 최대 20분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="8926f-151">인스턴스 크기/수가 변경되어도 중단되지 않으며, 게이트웨이는 이 시간 동안 활성 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="8926f-152">구성</span><span class="sxs-lookup"><span data-stu-id="8926f-152">Configuration</span></span>

<span data-ttu-id="8926f-153">**Q. Application Gateway가 가상 네트워크에서 항상 배포되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="8926f-154">예, Application Gateway는 항상 가상 네트워크 서브넷에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="8926f-155">이 서브넷은 Application Gateway만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="8926f-156">**Q. Application Gateway는 가상 네트워크 외부 인스턴스와 통신할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="8926f-157">Application Gateway는 IP 연결이 있는 경우 가상 네트워크 외부 인스턴스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="8926f-158">백 엔드 풀 멤버로 내부 IP를 사용할 계획인 경우 [VNET 피어링](../virtual-network/virtual-network-peering-overview.md) 또는 [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="8926f-159">**Q. Application Gateway 서브넷에서 다른 항목을 배포할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="8926f-160">아니요, 그러나 서브넷에 다른 응용 프로그램 게이트웨이를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="8926f-161">**Q. Application Gateway 서브넷에서 네트워크 보안 그룹이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="8926f-162">네트워크 보안 그룹은 Application Gateway 서브넷에서 지원되지만, 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="8926f-163">백 엔드 상태가 올바르게 작동하도록 포트 65503-65534에 들어오는 트래픽에 대한 예외를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="8926f-164">아웃바운드 인터넷 연결은 차단할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="8926f-165">AzureLoadBalancer 태그의 트래픽을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="8926f-166">**Q. Application Gateway에서 한도는 어떻게 되나요? 이러한 한도를 늘릴 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="8926f-167">한도를 보려면 [Application Gateway 한도](../azure-subscription-service-limits.md#application-gateway-limits)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="8926f-168">**Q. 외부 및 내부 트래픽 모두에 Application Gateway를 동시에 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="8926f-169">예, Application Gateway에서는 Application Gateway당 내부 IP 하나와 외부 IP 하나를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="8926f-170">**Q. VNet 피어링이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="8926f-171">예, VNet 피어링이 지원되며 다른 가상 네트워크에서 트래픽을 부하 분산시키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="8926f-172">**Q. 온-프레미스 서버가 ExpressRoute 또는 VPN 터널과 연결되어 있으면 이 서버와 통신할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="8926f-173">예, 트래픽이 허용되기만 한다면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="8926f-174">**Q. 한 개의 백 엔드 풀에서 서로 다른 포트로 많은 응용 프로그램을 제공할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="8926f-175">마이크로 서비스 아키텍처가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-175">Micro service architecture is supported.</span></span> <span data-ttu-id="8926f-176">서로 다른 포트의 프로브에 대해 여러 http 설정이 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="8926f-177">**Q. 사용자 지정 프로브가 응답 데이터에 와일드 카드/regex를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="8926f-178">사용자 지정 프로브는 응답 데이터에 와일드 카드 또는 regex를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="8926f-179">**Q. 규칙은 어떻게 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="8926f-180">규칙은 구성된 순서대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="8926f-181">기본 규칙은 다중 사이트 규칙보다 먼저 포트를 기준으로 트래픽과 일치하는지 평가되므로 트래픽이 잘못된 백 엔드로 라우팅될 가능성을 줄이려면 기본 규칙보다 먼저 다중 사이트 규칙을 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="8926f-182">**Q. 규칙은 어떻게 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="8926f-183">규칙은 만들어진 순서대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="8926f-184">다중 사이트 규칙이 기본 규칙보다 먼저 구성되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="8926f-185">다중 사이트 수신기를 먼저 구성하면 트래픽이 부적절한 백 엔드로 라우팅될 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="8926f-186">이 라우팅 문제는 다중 사이트 규칙을 평가하기 전에 먼저 기본 규칙이 포트 기반 트래픽과 일치함으로써 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="8926f-187">**Q. 사용자 지정 프로브에 대한 호스트 필드는 무엇을 나타내나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="8926f-188">호스트 필드는 프로브를 보낼 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="8926f-189">다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="8926f-190">이 값은 VM 호스트 이름과 다르며 \<프로토콜\>://\<호스트\>:\<포트\>\<경로\> 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="8926f-191">**Q. 몇 가지 원본 IP에 대한 Application Gateway 액세스를 허용 목록에 추가할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="8926f-192">이 시나리오는 Application Gateway 서브넷에서 NSG를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="8926f-193">우선 순위에 따라 나열된 다음 제한 사항을 서브넷에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="8926f-194">원본 IP/IP 범위에서 들어오는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="8926f-195">[백 엔드 상태 통신](application-gateway-diagnostics.md)을 위해 모든 원본에서 포트 65503-65534로 들어오는 요청을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="8926f-196">[NSG](../virtual-network/virtual-networks-nsg.md)에 대한 들어오는 Azure Load Balancer 프로브(AzureLoadBalancer 태그) 및 인바운드 가상 네트워크 트래픽(VirtualNetwork 태그)을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="8926f-197">모두 거부 규칙을 사용하여 다른 모든 들어오는 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="8926f-198">모든 대상에 대해 인터넷으로의 아웃바운드 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="8926f-199">성능</span><span class="sxs-lookup"><span data-stu-id="8926f-199">Performance</span></span>

<span data-ttu-id="8926f-200">**Q. Application Gateway는 고가용성과 확장성을 어떤 방식으로 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="8926f-201">둘 이상의 인스턴스가 배포된 경우에 Application Gateway에서 고가용성 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="8926f-202">Azure에서는 이러한 인스턴스를 업데이트 및 장애 도메인 간에 배포하여 모든 인스턴스가 동시에 실패하는 일이 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="8926f-203">Application Gateway는 로드를 공유하기 위해 동일한 게이트웨이의 여러 인스턴스를 추가하여 확장성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="8926f-204">**Q. Application Gateway에서 데이터 센터 간 DR 시나리오를 어떻게 달성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="8926f-205">고객은 Traffic Manager를 사용하여 서로 다른 데이터 센터에 있는 여러 Application Gateway 간에 트래픽을 분산시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="8926f-206">**Q. 자동 크기 조정이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="8926f-207">아니요, 하지만 Application Gateway에는 임계값에 도달했을 때 경고하는 데 사용할 수 있는 처리량 메트릭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="8926f-208">인스턴스를 수동으로 추가하거나 크기를 변경해도 게이트웨이가 다시 시작되지 않으며 기존 트래픽에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="8926f-209">**Q. 수동 강화/규모 축소 시 가동 중지 시간이 발생하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="8926f-210">가동 중지 시간 없이 인스턴스가 업그레이드 도메인 및 장애 도메인 간에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="8926f-211">**Q. 중단 없이 인스턴스 크기를 중간에서 큼으로 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="8926f-212">예, Azure에서는 인스턴스를 업데이트 및 장애 도메인 간에 배포하여 모든 인스턴스가 동시에 실패하는 일이 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="8926f-213">Application Gateway는 로드를 공유하기 위해 동일한 게이트웨이의 여러 인스턴스를 추가하여 크기 조정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="8926f-214">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="8926f-214">SSL Configuration</span></span>

<span data-ttu-id="8926f-215">**Q. Application Gateway에서 어떤 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="8926f-216">자체 서명된 인증서, CA 인증서 및 와일드 카드 인증서가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="8926f-217">EV 인증서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-217">EV certs are not supported.</span></span>

<span data-ttu-id="8926f-218">**Q. Application Gateway에서 지원되는 현재 암호 그룹은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="8926f-219">Application Gateway에서 지원되는 현재 암호 그룹은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="8926f-220">[Application Gateway에서 SSL 정책 버전 및 암호 그룹 구성](application-gateway-configure-ssl-policy-powershell.md)을 방문하여 SSL 옵션을 사용자 지정하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="8926f-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="8926f-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="8926f-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="8926f-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="8926f-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="8926f-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="8926f-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="8926f-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="8926f-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="8926f-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="8926f-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="8926f-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="8926f-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="8926f-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="8926f-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="8926f-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="8926f-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="8926f-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="8926f-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="8926f-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="8926f-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="8926f-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="8926f-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="8926f-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="8926f-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="8926f-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="8926f-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="8926f-247">**Q. Application Gateway에서 백 엔드에 대해 트래픽의 재암호화를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="8926f-248">예, Application Gateway는 SSL 오프로드와 백 엔드에 대한 트래픽을 다시 암호화하는 종단 간 SSL을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="8926f-249">**Q. SSL 프로토콜 버전을 제어하는 SSL 정책을 구성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="8926f-250">예, TLS1.0, TLS1.1 및 TLS1.2를 거부하도록 Application Gateway를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="8926f-251">SSL 2.0 및 3.0은 기본적으로 비활성화되며 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="8926f-252">**Q. 암호 그룹 및 정책 순서를 구성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="8926f-253">예, [암호 그룹을 구성](application-gateway-ssl-policy-overview.md)하도록 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="8926f-254">사용자 지정 정책을 정의할 때 다음 암호 그룹 중 하나 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="8926f-255">Application Gateway는 백 엔드 관리를 위해 SHA256을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="8926f-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="8926f-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="8926f-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="8926f-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="8926f-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="8926f-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8926f-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="8926f-262">**Q. 몇 개의 SSL 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="8926f-263">최대 20개의 SSL 인증서가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="8926f-264">**Q. 백 엔드 재암호화에 몇 개의 인증 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="8926f-265">5의 기본값으로 최대 10개의 인증 인증서가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="8926f-266">**Q. Application Gateway가 Azure Key Vault와 고유하게 통합되나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="8926f-267">아니요, Azure Key Vault와 통합되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="8926f-268">WAF(웹 응용 프로그램 방화벽) 구성</span><span class="sxs-lookup"><span data-stu-id="8926f-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="8926f-269">**Q. WAF SKU는 표준 SKU에서 사용 가능한 모든 기능을 제공하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="8926f-270">예, WAF는 표준 SKU에서 모든 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="8926f-271">**Q. Application Gateway에서 지원하는 CRS 버전은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="8926f-272">Application Gateway는 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 및 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="8926f-273">**Q. WAF를 모니터링하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="8926f-274">WAF는 진단 로깅을 통해 모니터링되며 진단 로깅에 대한 자세한 내용은 [Application Gateway에 대한 진단 로깅 및 메트릭](application-gateway-diagnostics.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="8926f-275">**Q. 검색 모드에서 트래픽을 차단하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="8926f-276">아니요, 검색 모드는 WAF 규칙을 트리거한 트래픽만 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="8926f-277">**Q. WAF 규칙을 사용자 지정하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="8926f-278">예, WAF 규칙은 사용자 지정이 가능합니다. 사용자 지정 방법에 대한 자세한 내용을 보려면 [WAF 규칙 그룹 및 규칙 사용자 지정](application-gateway-customize-waf-rules-portal.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="8926f-279">**Q. 현재 사용 가능한 규칙은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="8926f-280">현재 WAF는 [OWASP 상위 10개 취약점](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)에서 확인할 수 있는 OWASP(Open Web Application Security Project)에 의해 식별된 상위 10개 취약점 대부분에 대해 보안 기준을 제공하는 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 및 [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="8926f-281">SQL 삽입 공격 보호</span><span class="sxs-lookup"><span data-stu-id="8926f-281">SQL injection protection</span></span>

* <span data-ttu-id="8926f-282">교차 사이트 스크립팅 공격 보호</span><span class="sxs-lookup"><span data-stu-id="8926f-282">Cross site scripting protection</span></span>

* <span data-ttu-id="8926f-283">명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호</span><span class="sxs-lookup"><span data-stu-id="8926f-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="8926f-284">HTTP 프로토콜 위반 보호</span><span class="sxs-lookup"><span data-stu-id="8926f-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="8926f-285">누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호</span><span class="sxs-lookup"><span data-stu-id="8926f-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="8926f-286">보트, 크롤러 및 스캐너 방지</span><span class="sxs-lookup"><span data-stu-id="8926f-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="8926f-287">일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색</span><span class="sxs-lookup"><span data-stu-id="8926f-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="8926f-288">**Q. WAF에서 DDoS 방지도 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="8926f-289">아니요, WAF는 DDoS 방지를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="8926f-290">진단 및 로깅</span><span class="sxs-lookup"><span data-stu-id="8926f-290">Diagnostics and Logging</span></span>

<span data-ttu-id="8926f-291">**Q. Application Gateway에서 어떤 유형의 로그를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="8926f-292">Application Gateway에서는 3가지 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="8926f-293">이러한 로그 및 기타 진단 기능에 대한 자세한 내용은 [Application Gateway에 대한 백 엔드 상태, 진단 로깅 및 메트릭](application-gateway-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="8926f-294">**ApplicationGatewayAccessLog** - 이 액세스 로그에는 Application Gateway 프런트 엔드에 제출된 각 요청이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="8926f-295">이 데이터에는 호출자의 IP, 요청된 URL, 응답 대기 시간, 반환 코드, 바이트 입출력을 포함합니다. 액세스 로그는 300초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="8926f-296">이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="8926f-297">**ApplicationGatewayPerformanceLog** - 이 성능 로그는 처리된 총 요청 수, 처리량(바이트), 실패한 요청 수, 실패한 요청 수, 정상 및 비정상 백 엔드 인스턴스 수 등을 포함한 인스턴스별 성능 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="8926f-298">**ApplicationGatewayFirewallLog** - 이 방화벽 로그에는 웹 응용 프로그램 방화벽으로 구성된 응용 프로그램 게이트웨이의 검색 모드 또는 방지 모드를 통해 기록된 요청이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="8926f-299">**Q. 내 백 엔드 풀 멤버가 정상인지 어떻게 알 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="8926f-300">PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth`를 사용하거나 [Application Gateway 진단](application-gateway-diagnostics.md)을 방문하여 포털을 통해 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="8926f-301">**Q. 진단 로그에서 보존 정책은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="8926f-302">진단 로그는 고객 저장소 계정으로 전달되고 고객은 기본 설정에 따라 보존 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="8926f-303">진단 로그는 Event Hub 또는 Log Analytics로도 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="8926f-304">자세한 내용을 보려면 [Application Gateway 진단](application-gateway-diagnostics.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="8926f-305">**Q. Application Gateway에 대한 감사 로그를 어떻게 얻나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="8926f-306">Application Gateway에 대해 감사 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="8926f-307">포털에서 감사 로그에 액세스하려면 Application Gateway의 메뉴 블레이드에서 **활동 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="8926f-308">**Q. Application Gateway로 경고를 설정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="8926f-309">예, Application Gateway는 경고를 지원하며 메트릭에 따라 경고를 해제하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="8926f-310">Application Gateway에서는 현재 경고를 구성할 수 있는 "처리량" 메트릭을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="8926f-311">경고에 대한 자세한 내용을 보려면 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="8926f-312">**Q. 백 엔드 상태에서 알 수 없는 상태를 반환할 경우 이 상태의 원인은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="8926f-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="8926f-313">백 엔드에 액세스하는 가장 일반적인 이유는 NSG 또는 사용자 지정 DNS로 차단되는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8926f-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="8926f-314">자세한 내용은 [Application Gateway에 대한 백 엔드 상태, 진단 로깅 및 메트릭](application-gateway-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8926f-315">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8926f-315">Next Steps</span></span>

<span data-ttu-id="8926f-316">Application Gateway에 대한 자세한 내용은 [Application Gateway 소개](application-gateway-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8926f-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
