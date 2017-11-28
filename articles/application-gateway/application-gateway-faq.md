---
title: "Azure 응용 프로그램 게이트웨이에 대 한 질문과 대답 aaaFrequently | Microsoft Docs"
description: "이 페이지에서는 답변 toofrequently Azure 응용 프로그램 게이트웨이에 대 한 질문과 대답"
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
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="c7f1d-103">Application Gateway에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="c7f1d-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="c7f1d-104">일반</span><span class="sxs-lookup"><span data-stu-id="c7f1d-104">General</span></span>

<span data-ttu-id="c7f1d-105">**Q. Application Gateway란?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-106">Azure Application Gateway는 서비스 형태의 ADC(응용 프로그램 전달 컨트롤러)이며 응용 프로그램에 대한 다양한 계층 7 부하 분산 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="c7f1d-107">Azure에서 완전히 관리되는 고가용성의 확장성 있는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="c7f1d-108">**Q. Application Gateway에서 지원하는 기능은 어떤 것이 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="c7f1d-109">응용 프로그램 게이트웨이 SSL 오프 로딩 및 끝 tooend SSL, 웹 응용 프로그램 방화벽, 쿠키 기반 세션 선호도, url 경로 기반 라우팅, 다중 사이트 호스팅 및 다른 사용자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="c7f1d-110">지원 되는 기능의 전체 목록을 보려면 방문 [소개 tooApplication 게이트웨이](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c7f1d-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="c7f1d-111">**Q. 응용 프로그램 게이트웨이와 Azure 부하 분산 장치 간의 hello 차이점은 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="c7f1d-112">Application Gateway는 웹 트래픽(HTTP/HTTPS/WebSocket)에서만 작동하는 7계층 부하 분산 장치로서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="c7f1d-113">SSL 종료, 쿠키 기반 세션 선호도, 트래픽 부하 분산을 위한 라운드 로빈과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="c7f1d-114">부하 분산 장치, 계층 4(TCP/UDP)에서 트래픽 부하 분산.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="c7f1d-115">**Q. Application Gateway에서 지원하는 프로토콜은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="c7f1d-116">Application Gateway는 HTTP, HTTPS 및 WebSocket을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="c7f1d-117">**Q. 현재 백 엔드 풀의 일부로 어떤 리소스가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="c7f1d-118">백 엔드 풀은 NIC, 가상 컴퓨터 확장 집합, 공용 IP, 내부 IP, FQDN(정규화된 도메인 이름) 및 다중 테넌트 백 엔드(예: Azure Web Apps)로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="c7f1d-119">응용 프로그램 게이트웨이 백 엔드 풀 멤버가 하지 않습니다. tooan 가용성 집합을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="c7f1d-120">백 엔드 풀의 멤버는 IP 연결이 있는 경우 클러스터, 데이터 센터 간 또는 Azure 외부에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="c7f1d-121">**Q. 어떤 영역은 hello 서비스에서 사용할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="c7f1d-122">Application Gateway는 Azure 전체의 모든 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="c7f1d-123">[Azure China](https://www.azure.cn/) 및 [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="c7f1d-124">**Q. 내 구독에 대한 전용 배포인가요? 아니면 고객 간에 공유되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="c7f1d-125">Application Gateway는 가상 네트워크에서 전용 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="c7f1d-126">**Q. HTTP->HTTPS 리디렉션이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="c7f1d-127">리디렉션은 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-127">Redirection is supported.</span></span> <span data-ttu-id="c7f1d-128">방문 [응용 프로그램 게이트웨이 리디렉션 개요](application-gateway-redirect-overview.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="c7f1d-129">**Q. 수신기는 어떤 순서로 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="c7f1d-130">수신기는 표시 된 hello 순서 대로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="c7f1d-131">이러한 이유로 기본 수신기에서 들어오는 요청과 일치하는 경우 이 요청을 먼저 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="c7f1d-132">다중 사이트 수신기 기본 수신기 tooensure 트래픽 라우팅된 toohello 올바른 백 엔드 되기 전에 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="c7f1d-133">**Q. Application Gateway의 IP 및 DNS는 어디에서 확인하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="c7f1d-134">공용 IP 주소를 끝점으로 사용할 경우이 정보가 있습니다 hello 개요 페이지에서 또는 hello 공용 IP 주소 리소스에 hello 포털에서 응용 프로그램 게이트웨이 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="c7f1d-135">내부 IP 주소에 대 한 hello 개요 페이지에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="c7f1d-136">**Q. 가 hello IP 또는 DNS 변경 hello 응용 프로그램 게이트웨이 hello 기간 동안 합니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-137">hello VIP hello 게이트웨이 중지 되 고 hello 고객에서 시작 하는 경우 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="c7f1d-138">응용 프로그램 게이트웨이에 연결 된 DNS hello hello 게이트웨이의 hello 수명 주기를 통해 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="c7f1d-139">이러한 이유로 toouse CNAME 별칭을 권장 하 고 응용 프로그램 게이트웨이 hello toohello DNS 주소를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="c7f1d-140">**Q. Application Gateway에서 고정 IP를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="c7f1d-141">아니요, Application Gateway에서는 고정 공용 IP 주소를 지원하지 않고 고정 내부 IP를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="c7f1d-142">**Q. 응용 프로그램 게이트웨이 hello 게이트웨이에 여러 공용 Ip를 지원 합니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="c7f1d-143">Application Gateway에서는 하나의 공용 IP 주소만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="c7f1d-144">**Q. Application Gateway에서 x-forwarded-for 헤더를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="c7f1d-145">예, x-전달-프로토콜, x-전달 기능에 대 한 응용 프로그램 게이트웨이 삽입 하 고 hello 요청으로 x 전달 포트 헤더가 toohello 백 엔드 전달.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="c7f1d-146">x-전달 기능에 대 한 헤더에 대 한 hello 형식은 쉼표로 구분 된 목록 ip: port입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="c7f1d-147">hello x 전달 프로토콜에 대 한 유효한 값은 http 또는 https입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="c7f1d-148">X 전달 된 포트에 응용 프로그램 게이트웨이 hello에 도달 하는 hello 요청 시 hello 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="c7f1d-149">**Q. 얼마나 오래 걸립니까 toodeploy 응용 프로그램 게이트웨이? Application Gateway가 업데이트되어도 여전히 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="c7f1d-150">새 응용 프로그램 게이트웨이 배포 too20 분 tooprovision 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="c7f1d-151">변경 내용을 tooinstance 크기/수 장치를 중단할 필요가 되지 않으며 hello 게이트웨이이 시간 동안 활성 상태로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="c7f1d-152">구성</span><span class="sxs-lookup"><span data-stu-id="c7f1d-152">Configuration</span></span>

<span data-ttu-id="c7f1d-153">**Q. Application Gateway가 가상 네트워크에서 항상 배포되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="c7f1d-154">예, Application Gateway는 항상 가상 네트워크 서브넷에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="c7f1d-155">이 서브넷은 Application Gateway만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="c7f1d-156">**Q. 응용 프로그램 게이트웨이 해당 가상 네트워크 외부 tooinstances 서로 연결할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="c7f1d-157">응용 프로그램 게이트웨이 IP로 연결 되어으로 컴퓨터가 hello 가상 네트워크 외부에서 tooinstances를 문의 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="c7f1d-158">백 엔드 풀 멤버 이면 내부 Ip 필요 toouse 계획 이라면 [VNET 피어 링](../virtual-network/virtual-network-peering-overview.md) 또는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="c7f1d-159">**Q. 배포할 수 있습니까 hello 응용 프로그램 게이트웨이 서브넷의 다른 부분?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="c7f1d-160">아니요, 하지만 hello 서브넷에서 다른 응용 프로그램 게이트웨이 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="c7f1d-161">**Q. Hello 응용 프로그램 게이트웨이 서브넷에 네트워크 보안 그룹 지원 되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="c7f1d-162">네트워크 보안 그룹은 다음 제한 사항이 hello로 hello 응용 프로그램 게이트웨이 서브넷에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="c7f1d-163">예외에 배치 해야 들어오는 트래픽에 대 한 백 엔드 상태 toowork에 대 한 65503 65534 포트에서 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="c7f1d-164">아웃바운드 인터넷 연결은 차단할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="c7f1d-165">Hello AzureLoadBalancer 태그에서에서 트래픽을 허용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="c7f1d-166">**Q. 응용 프로그램 게이트웨이 hello 제한 사항은 무엇입니까? 이러한 한도를 늘릴 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="c7f1d-167">방문 [응용 프로그램 게이트웨이 제한](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="c7f1d-168">**Q. 외부 및 내부 트래픽 모두에 Application Gateway를 동시에 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="c7f1d-169">예, Application Gateway에서는 Application Gateway당 내부 IP 하나와 외부 IP 하나를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="c7f1d-170">**Q. VNet 피어링이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="c7f1d-171">예, VNet 피어링이 지원되며 다른 가상 네트워크에서 트래픽을 부하 분산시키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="c7f1d-172">**Q. 문의 해야 합니까 tooon 온-프레미스 서버 ExpressRoute 또는 VPN 터널으로 연결 되어 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="c7f1d-173">예, 트래픽이 허용되기만 한다면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="c7f1d-174">**Q. 한 개의 백 엔드 풀에서 서로 다른 포트로 많은 응용 프로그램을 제공할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="c7f1d-175">마이크로 서비스 아키텍처가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-175">Micro service architecture is supported.</span></span> <span data-ttu-id="c7f1d-176">서로 다른 포트에서 여러 http 구성 된 설정을 tooprobe를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="c7f1d-177">**Q. 사용자 지정 프로브가 응답 데이터에 와일드 카드/regex를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="c7f1d-178">사용자 지정 프로브는 응답 데이터에 와일드 카드 또는 regex를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="c7f1d-179">**Q. 규칙은 어떻게 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="c7f1d-180">규칙은 구성 된 hello 순서로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="c7f1d-181">Hello 기본 규칙 평가 되는 포트 이전 toohello 다중 사이트 규칙에 따라 트래픽의 일치 하는 기본 규칙 tooreduce hello 가능성이 트래픽이 toohello 부적절 한 백 엔드를 라우트하기 전에 멀티 사이트 규칙이 구성 된 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="c7f1d-182">**Q. 규칙은 어떻게 처리되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="c7f1d-183">규칙은 만들어질 hello 순서로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="c7f1d-184">다중 사이트 규칙이 기본 규칙보다 먼저 구성되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="c7f1d-185">다중 사이트 수신기를 먼저 구성 하면이 구성은 트래픽이 라우트된 toohello 부적절 한 백 엔드 되 hello 가능성을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="c7f1d-186">Hello 기본 규칙 평가 되는 포트 이전 toohello 다중 사이트 규칙에 따라 트래픽의 일치 하는 것이 라우팅 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="c7f1d-187">**Q. 사용자 지정 프로브에 대해 hello 호스트 필드는 나타낼 하는?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="c7f1d-188">호스트 필드는 hello 이름 toosend hello 검색을 실행 하려면를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="c7f1d-189">다중 사이트를 Application Gateway에 구성하는 경우에만 적용할 수 있습니다. 그렇지 않으면 '127.0.0.1'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="c7f1d-190">이 값은 VM 호스트 이름과 다르며 \<프로토콜\>://\<호스트\>:\<포트\>\<경로\> 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="c7f1d-191">**Q. 수 있는 응용 프로그램 게이트웨이 액세스 tooa 화이트 리스트 Ip 소스 지원 되는 몇?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="c7f1d-192">이 시나리오는 Application Gateway 서브넷에서 NSG를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="c7f1d-193">우선 순위에 따라 나열 된 hello hello 서브넷에 넣을 hello 다음 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="c7f1d-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="c7f1d-194">원본 IP/IP 범위에서 들어오는 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="c7f1d-195">들어오는 요청에 대 한 모든 소스 tooports 65503 65534 허용 [백 엔드 상태 통신](application-gateway-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="c7f1d-196">Hello에 대 한 들어오는 Azure 부하 분산 장치 프로브 (AzureLoadBalancer 태그)와 가상 인바운드 네트워크 트래픽을 (VirtualNetwork 태그) 가능 [NSG](../virtual-network/virtual-networks-nsg.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="c7f1d-197">모두 거부 규칙을 사용하여 다른 모든 들어오는 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="c7f1d-198">아웃 바운드 트래픽을 toohello 허용 모든 대상에 대 한 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="c7f1d-199">성능</span><span class="sxs-lookup"><span data-stu-id="c7f1d-199">Performance</span></span>

<span data-ttu-id="c7f1d-200">**Q. Application Gateway는 고가용성과 확장성을 어떤 방식으로 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="c7f1d-201">둘 이상의 인스턴스가 배포된 경우에 Application Gateway에서 고가용성 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="c7f1d-202">Azure hello에서 모든 인스턴스가 실패 하지 않는 업데이트 및 오류 도메인 tooensure 분산 이러한 인스턴스에 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="c7f1d-203">응용 프로그램 게이트웨이 hello의 여러 인스턴스를 추가 하 여 확장성을 지원 게이트웨이 tooshare hello 부하를 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="c7f1d-204">**Q. Application Gateway에서 데이터 센터 간 DR 시나리오를 어떻게 달성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-205">고객이 다른 데이터 센터에서 여러 응용 프로그램 게이트웨이 트래픽 관리자 toodistribute 트래픽을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="c7f1d-206">**Q. 자동 크기 조정이 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="c7f1d-207">아니요, 하지만 응용 프로그램 게이트웨이 처리량 메트릭을 사용 하는 tooalert 일 수 있는 하 한 임계값에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="c7f1d-208">수동으로 인스턴스를 추가 또는 크기를 변경 hello 게이트웨이 다시 시작 되지 않으면 하며 기존 트래픽을 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="c7f1d-209">**Q. 수동 강화/규모 축소 시 가동 중지 시간이 발생하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="c7f1d-210">가동 중지 시간 없이 인스턴스가 업그레이드 도메인 및 장애 도메인 간에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="c7f1d-211">**Q. 중지 하지 않고 중간 toolarge 인스턴스 크기를 변경할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="c7f1d-212">Azure hello에서 모든 인스턴스가 실패 하지 않는 업데이트 및 오류 도메인 tooensure에서 인스턴스를 배포 하는 예, 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="c7f1d-213">여러 인스턴스를 추가 하 여 크기 조정 응용 프로그램 게이트웨이 지원 hello 게이트웨이 tooshare hello 부하를 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="c7f1d-214">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="c7f1d-214">SSL Configuration</span></span>

<span data-ttu-id="c7f1d-215">**Q. Application Gateway에서 어떤 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-216">자체 서명된 인증서, CA 인증서 및 와일드 카드 인증서가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="c7f1d-217">EV 인증서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-217">EV certs are not supported.</span></span>

<span data-ttu-id="c7f1d-218">**Q. 응용 프로그램 게이트웨이 원하는 hello 현재 암호 그룹은 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-219">hello 다음 원하는 응용 프로그램 게이트웨이 hello 현재 암호 그룹은입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="c7f1d-220">방문: [SSL 구성 정책 버전 및 응용 프로그램 게이트웨이에 암호 그룹](application-gateway-configure-ssl-policy-powershell.md) toolearn 어떻게 toocustomize SSL 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="c7f1d-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="c7f1d-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="c7f1d-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c7f1d-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c7f1d-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c7f1d-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c7f1d-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c7f1d-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c7f1d-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="c7f1d-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="c7f1d-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="c7f1d-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="c7f1d-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="c7f1d-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="c7f1d-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="c7f1d-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="c7f1d-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="c7f1d-247">**Q. 트래픽 toohello 백 엔드를 다시 암호화는 응용 프로그램 게이트웨이도 지원 합니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="c7f1d-248">예, 응용 프로그램 게이트웨이 지원 SSL 오프 로드 및 끝 tooend hello 트래픽 toohello 백 엔드를 다시 암호화 하는 SSL 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="c7f1d-249">**Q. SSL 정책 toocontrol SSL 프로토콜 버전을 구성할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="c7f1d-250">예, 응용 프로그램 게이트웨이 toodeny를 구성할 수 있습니다 TLS1.0, TLS1.1 및 TLS1.2 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="c7f1d-251">SSL 2.0 및 3.0은 기본적으로 비활성화되며 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="c7f1d-252">**Q. 암호 그룹 및 정책 순서를 구성할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="c7f1d-253">예, [암호 그룹을 구성](application-gateway-ssl-policy-overview.md)하도록 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="c7f1d-254">사용자 지정 정책의 정의할 때는 hello 암호 그룹이 다음 중 하나 이상이 사용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="c7f1d-255">응용 프로그램 게이트웨이 s h a 256 toofor 백 엔드 관리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="c7f1d-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="c7f1d-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="c7f1d-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="c7f1d-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="c7f1d-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="c7f1d-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="c7f1d-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="c7f1d-262">**Q. 몇 개의 SSL 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="c7f1d-263">too20 SSL 인증서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="c7f1d-264">**Q. 백 엔드 재암호화에 몇 개의 인증 인증서가 지원되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="c7f1d-265">Too10를 인증 인증서는 이며 기본값은 5 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="c7f1d-266">**Q. Application Gateway가 Azure Key Vault와 고유하게 통합되나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="c7f1d-267">아니요, Azure Key Vault와 통합되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="c7f1d-268">WAF(웹 응용 프로그램 방화벽) 구성</span><span class="sxs-lookup"><span data-stu-id="c7f1d-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="c7f1d-269">**Q. Hello WAF SKU hello 표준 SKU로 사용할 수 있는 모든 hello 기능을 제공 합니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="c7f1d-270">예, WAF hello 표준 SKU의에서 모든 hello 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="c7f1d-271">**Q. 응용 프로그램 게이트웨이 지원 hello CRS 버전은 무엇입니까?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="c7f1d-272">Application Gateway는 CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) 및 CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="c7f1d-273">**Q. WAF를 모니터링하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="c7f1d-274">WAF는 진단 로깅을 통해 모니터링되며 진단 로깅에 대한 자세한 내용은 [Application Gateway에 대한 진단 로깅 및 메트릭](application-gateway-diagnostics.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="c7f1d-275">**Q. 검색 모드에서 트래픽을 차단하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="c7f1d-276">아니요, 검색 모드는 WAF 규칙을 트리거한 트래픽만 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="c7f1d-277">**Q. WAF 규칙을 사용자 지정하려면 어떻게 하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="c7f1d-278">예, WAF 규칙은 toocustomize을 방문할 방법에 대 한 자세한 내용은 사용자 지정 가능한 [WAF 사용자 지정 규칙 그룹 및 규칙](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c7f1d-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="c7f1d-279">**Q. 현재 사용 가능한 규칙은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="c7f1d-280">WAF CRS는 현재 지원 [2.2.9 퀵](application-gateway-crs-rulegroups-rules.md#owasp229) 및 [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), 대부분의 hello에 대 한 초기 보안을 제공 하는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) ´ ֿ ´로 식별 되는 상위 10 개의 취약성 [OWASP 상위 10 개의 취약성](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="c7f1d-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="c7f1d-281">SQL 삽입 공격 보호</span><span class="sxs-lookup"><span data-stu-id="c7f1d-281">SQL injection protection</span></span>

* <span data-ttu-id="c7f1d-282">교차 사이트 스크립팅 공격 보호</span><span class="sxs-lookup"><span data-stu-id="c7f1d-282">Cross site scripting protection</span></span>

* <span data-ttu-id="c7f1d-283">명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할, 원격 파일 포함 공격 등의 일반 웹 공격 보호</span><span class="sxs-lookup"><span data-stu-id="c7f1d-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="c7f1d-284">HTTP 프로토콜 위반 보호</span><span class="sxs-lookup"><span data-stu-id="c7f1d-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="c7f1d-285">누락된 호스트 사용자-에이전트 및 수락 헤더 같은 HTTP 프로토콜 이상 보호</span><span class="sxs-lookup"><span data-stu-id="c7f1d-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="c7f1d-286">보트, 크롤러 및 스캐너 방지</span><span class="sxs-lookup"><span data-stu-id="c7f1d-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="c7f1d-287">일반적인 응용 프로그램 구성 오류(즉 Apache, IIS 등) 검색</span><span class="sxs-lookup"><span data-stu-id="c7f1d-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="c7f1d-288">**Q. WAF에서 DDoS 방지도 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="c7f1d-289">아니요, WAF는 DDoS 방지를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="c7f1d-290">진단 및 로깅</span><span class="sxs-lookup"><span data-stu-id="c7f1d-290">Diagnostics and Logging</span></span>

<span data-ttu-id="c7f1d-291">**Q. Application Gateway에서 어떤 유형의 로그를 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-292">Application Gateway에서는 3가지 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="c7f1d-293">이러한 로그 및 기타 진단 기능에 대한 자세한 내용은 [Application Gateway에 대한 백 엔드 상태, 진단 로깅 및 메트릭](application-gateway-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="c7f1d-294">**ApplicationGatewayAccessLog** -hello 액세스 로그에 제출 된 각 요청 toohello 응용 프로그램 게이트웨이 프런트 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="c7f1d-295">축소 및 반환 코드, 바이트, hello 데이터 hello 호출자의 IP, URL, 요청 응답 대기 시간이 포함 됩니다. 액세스 로그는 300초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="c7f1d-296">이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="c7f1d-297">**ApplicationGatewayPerformanceLog** -hello 성능 로그에 정보가 성능 인스턴스별로 서비스를 제공 하는 총 요청을 포함 하 여 처리량 (바이트), 총 요청 제공을 정상 및 비정상 실패 한 요청 수 백 엔드 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="c7f1d-298">**ApplicationGatewayFirewallLog** -hello 방화벽 로그 감지 하거나 방지 모드의 웹 응용 프로그램 방화벽으로 구성 된 응용 프로그램 게이트웨이 통해 기록 된 요청을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="c7f1d-299">**Q. 내 백 엔드 풀 멤버가 정상인지 어떻게 알 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="c7f1d-300">Hello PowerShell cmdlet을 사용할 수 있습니다 `Get-AzureRmApplicationGatewayBackendHealth` 방문 하 여 hello 포털을 통해 상태를 확인 또는 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="c7f1d-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="c7f1d-301">**Q. Hello 진단 로그에 hello 보존 정책 이란?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="c7f1d-302">진단 로그 흐름 toohello 고객 저장소 계정 및 고객의 기본 설정에 따라 hello 보존 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="c7f1d-303">진단 로그 이벤트 허브 또는 로그 분석 tooan을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="c7f1d-304">자세한 내용을 보려면 [Application Gateway 진단](application-gateway-diagnostics.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="c7f1d-305">**Q. Application Gateway에 대한 감사 로그를 어떻게 얻나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-306">Application Gateway에 대해 감사 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="c7f1d-307">Hello 포털에서 클릭 **활동 로그** 응용 프로그램 게이트웨이 tooaccess hello 감사 로그의 hello 메뉴 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="c7f1d-308">**Q. Application Gateway로 경고를 설정할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="c7f1d-309">예, Application Gateway는 경고를 지원하며 메트릭에 따라 경고를 해제하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="c7f1d-310">현재 응용 프로그램 게이트웨이 보유 한 메트릭 "처리량" tooalert 구성된 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="c7f1d-311">경고에 대 한 더 toolearn 방문 [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="c7f1d-312">**Q. 백 엔드 상태에서 알 수 없는 상태를 반환할 경우 이 상태의 원인은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="c7f1d-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="c7f1d-313">hello 가장 일반적인 이유는 액세스 toohello 백 엔드는 NSG 나 사용자 지정 DNS에서 차단 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="c7f1d-314">방문 [백 엔드 상태, 진단 로깅 및 응용 프로그램 게이트웨이 대 한 메트릭을](application-gateway-diagnostics.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7f1d-315">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c7f1d-315">Next Steps</span></span>

<span data-ttu-id="c7f1d-316">응용 프로그램 게이트웨이에 대해 자세히 방문 toolearn [소개 tooApplication 게이트웨이](application-gateway-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c7f1d-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
