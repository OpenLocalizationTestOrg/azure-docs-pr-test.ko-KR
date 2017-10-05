---
title: Azure DNS FAQ | Microsoft Docs
description: "Azure DNS에 대한 질문과 대답"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: f365574a12047f6952209dc3883af32a2e9ecd1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-faq"></a><span data-ttu-id="0dcd8-103">Azure DNS FAQ</span><span class="sxs-lookup"><span data-stu-id="0dcd8-103">Azure DNS FAQ</span></span>

## <a name="about-azure-dns"></a><span data-ttu-id="0dcd8-104">Azure DNS 정보</span><span class="sxs-lookup"><span data-stu-id="0dcd8-104">About Azure DNS</span></span>

### <a name="what-is-azure-dns"></a><span data-ttu-id="0dcd8-105">Azure DNS란?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-105">What is Azure DNS?</span></span>

<span data-ttu-id="0dcd8-106">Domain Name System, 즉 DNS는 웹 사이트 또는 서비스 이름을 해당 IP 주소로 변환(또는 확인)합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-106">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="0dcd8-107">Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-107">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="0dcd8-108">Azure에 도메인을 호스트하면 다른 Azure 서비스와 동일한 자격 증명, API, 도구 및 대금 청구를 사용하여 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-108">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

<span data-ttu-id="0dcd8-109">Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-109">DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="0dcd8-110">사용 가능한 가장 가까운 DNS 서버에서 각 DNS 쿼리에 응답하도록 애니캐스트 네트워킹이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-110">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="0dcd8-111">이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-111">This provides both fast performance and high availability for your domain.</span></span>

<span data-ttu-id="0dcd8-112">Azure DNS 서비스는 Azure Resource Manager를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-112">The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="0dcd8-113">이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-113">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="0dcd8-114">도메인과 레코드는 Azure 포털, Azure PowerShell cmdlet 및 플랫폼 간 Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-114">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="0dcd8-115">자동 DNS 관리가 필요한 응용 프로그램은 REST API 및 SDK를 통해 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-115">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

### <a name="how-much-does-azure-dns-cost"></a><span data-ttu-id="0dcd8-116">Azure DNS 비용은 얼마입니까?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-116">How much does Azure DNS cost?</span></span>

<span data-ttu-id="0dcd8-117">Azure DNS 요금 청구 모델은 Azure DNS에 호스트되는 DNS 영역의 수와 수신되는 DNS 쿼리 수를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-117">The Azure DNS billing model is based on the number of DNS zones hosted in Azure DNS and the number of DNS queries they receive.</span></span> <span data-ttu-id="0dcd8-118">할인은 사용량에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-118">Discounts are provided based on usage.</span></span>

<span data-ttu-id="0dcd8-119">자세한 내용은 [Azure DNS 가격 책정 페이지](https://azure.microsoft.com/pricing/details/dns/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-119">For more information, see the [Azure DNS pricing page](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="what-is-the-sla-for-azure-dns"></a><span data-ttu-id="0dcd8-120">Azure DNS에 대한 SLA는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-120">What is the SLA for Azure DNS?</span></span>

<span data-ttu-id="0dcd8-121">Microsoft는 유효한 DNS 요청에 대해 99.99% 이상의 시간 동안 하나 이상의 Azure DNS 이름 서버에서 응답을 제공할 것을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-121">We guarantee that valid DNS requests will receive a response from at least one Azure DNS name server at least 99.99% of the time.</span></span>

<span data-ttu-id="0dcd8-122">자세한 내용은 [Azure DNS SLA 페이지](https://azure.microsoft.com/support/legal/sla/dns)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-122">For more information, see the [Azure DNS SLA page](https://azure.microsoft.com/support/legal/sla/dns).</span></span>

### <a name="what-is-a-dns-zone-is-it-the-same-as-a-dns-domain"></a><span data-ttu-id="0dcd8-123">'DNS 영역'이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-123">What is a ‘DNS zone’?</span></span> <span data-ttu-id="0dcd8-124">DNS 도메인과 같은 것인가요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-124">Is it the same as a DNS domain?</span></span> 

<span data-ttu-id="0dcd8-125">도메인은 Domain Name System의 고유 이름입니다(예: 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="0dcd8-125">A domain is a unique name in the domain name system, for example ‘contoso.com’.</span></span>

<span data-ttu-id="0dcd8-126">DNS 영역은 특정 도메인에 대한 DNS 레코드를 호스트하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-126">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="0dcd8-127">예를 들어 'contoso.com' 도메인은 'mail.contoso.com'(메일 서버) 및 'www.contoso.com'(웹 사이트)과 같은 여러 DNS 레코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-127">For example, the domain ‘contoso.com’ may contain several DNS records, such as ‘mail.contoso.com’ (for a mail server) and ‘www.contoso.com’ (for a web site).</span></span> <span data-ttu-id="0dcd8-128">이러한 레코드는 DNS 영역 'contoso.com'에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-128">These would be hosted in the DNS zone 'contoso.com'.</span></span>

<span data-ttu-id="0dcd8-129">도메인 이름은 *이름만*으로 구성되지만 DNS 영역은 도메인 이름에 대한 DNS 레코드를 포함하는 데이터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-129">A domain name is *just a name*, whereas a DNS zone is a data resource containing the DNS records for a domain name.</span></span> <span data-ttu-id="0dcd8-130">Azure DNS를 사용하면 DNS 영역을 호스트하고 Azure에서 도메인에 대한 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-130">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="0dcd8-131">또한 인터넷의 DNS 쿼리에 응답하기 위해 DNS 이름 서버를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-131">It also provides DNS name servers to answer DNS queries from the Internet.</span></span>

### <a name="do-i-need-to-purchase-a-dns-domain-name-to-use-azure-dns"></a><span data-ttu-id="0dcd8-132">Azure DNS를 사용하기 위해 DNS 도메인 이름을 구입해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-132">Do I need to purchase a DNS domain name to use Azure DNS?</span></span> 

<span data-ttu-id="0dcd8-133">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-133">Not necessarily.</span></span>

<span data-ttu-id="0dcd8-134">Azure DNS에서 DNS 영역을 호스트하기 위해 도메인을 구입할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-134">You do not need to purchase a domain to host a DNS zone in Azure DNS.</span></span> <span data-ttu-id="0dcd8-135">도메인 이름을 소유하지 않고도 언제든지 DNS 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-135">You can create a DNS zone at any time without owning the domain name.</span></span> <span data-ttu-id="0dcd8-136">이 영역에 대한 DNS 쿼리는 해당 영역에 할당된 Azure DNS 이름 서버로 전송되는 경우에만 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-136">DNS queries for this zone will only resolve if they are directed to the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="0dcd8-137">DNS 영역을 전역 DNS 계층 구조에 연결하려면 도메인 이름을 구입해야 합니다. 이 경우 전 세계 어디에서든지 DNS 쿼리를 수행하여 DNS 영역을 찾고 DNS 레코드로 응답을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-137">You need to purchase the domain name if you want to link your DNS zone into the global DNS hierarchy – this enables DNS queries from anywhere in the world to find your DNS zone and be answered with your DNS records.</span></span>

## <a name="azure-dns-features"></a><span data-ttu-id="0dcd8-138">Azure DNS 기능</span><span class="sxs-lookup"><span data-stu-id="0dcd8-138">Azure DNS Features</span></span>

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a><span data-ttu-id="0dcd8-139">Azure DNS는 DNS 기반 트래픽 라우팅 또는 끝점 장애 조치(failover)를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-139">Does Azure DNS support DNS-based traffic routing or endpoint failover?</span></span>

<span data-ttu-id="0dcd8-140">DNS 기반 트래픽 라우팅 및 끝점 장애 조치(failover)는 Azure Traffic Manager에 의해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-140">DNS-based traffic routing and endpoint failover are provided by Azure Traffic Manager.</span></span> <span data-ttu-id="0dcd8-141">이것은 Azure DNS와 함께 사용할 수 있는 별도 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-141">This is a separate Azure service that can be used together with Azure DNS.</span></span> <span data-ttu-id="0dcd8-142">자세한 내용은 [Traffic Manager 개요](../traffic-manager/traffic-manager-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-142">For more information, see the [Traffic Manager overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="0dcd8-143">Azure DNS는 지정된 DNS 레코드에 대한 각 DNS 쿼리가 항상 동일한 DNS 응답을 수신하는 '고정' DNS 도메인 호스트만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-143">Azure DNS only supports hosting 'static' DNS domains, where each DNS query for a given DNS record always receives the same DNS response.</span></span>

### <a name="does-azure-dns-support-domain-name-registration"></a><span data-ttu-id="0dcd8-144">Azure DNS는 도메인 이름 등록을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-144">Does Azure DNS support domain name registration?</span></span>

<span data-ttu-id="0dcd8-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-145">No.</span></span> <span data-ttu-id="0dcd8-146">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-146">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="0dcd8-147">도메인을 구입하려면 타사 도메인 이름 등록 기관을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-147">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="0dcd8-148">등록 기관은 일반적으로 소액의 연간 요금을 부과합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-148">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="0dcd8-149">그런 다음, DNS 레코드의 관리를 위해 Azure DNS에 해당 도메인을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-149">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="0dcd8-150">자세한 내용은 [Azure DNS에 도메인 위임](dns-domain-delegation.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-150">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

<span data-ttu-id="0dcd8-151">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-151">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="0dcd8-152">피드백 사이트를 사용하여 [이 기능에 대한 지원을 등록](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-152">You can use our feedback site to [register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).</span></span>

### <a name="does-azure-dns-support-private-domains"></a><span data-ttu-id="0dcd8-153">Azure DNS에서는 '개인' 도메인을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-153">Does Azure DNS support 'private' domains?</span></span>

<span data-ttu-id="0dcd8-154">아니요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-154">No.</span></span> <span data-ttu-id="0dcd8-155">Azure DNS는 현재 인터넷 연결 도메인만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-155">Azure DNS currently only supports Internet-facing domains.</span></span>

<span data-ttu-id="0dcd8-156">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-156">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="0dcd8-157">피드백 사이트를 사용하여 [이 기능에 대한 지원을 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-157">You can use our feedback site to [register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).</span></span>

<span data-ttu-id="0dcd8-158">Azure의 내부 DNS 옵션에 대한 자세한 내용은 [VM 및 역할 인스턴스에 대한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-158">For information on internal DNS options in Azure, see [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

### <a name="does-azure-dns-support-dnssec"></a><span data-ttu-id="0dcd8-159">Azure DNS에서는 DNSSEC를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-159">Does Azure DNS support DNSSEC?</span></span>

<span data-ttu-id="0dcd8-160">아니요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-160">No.</span></span> <span data-ttu-id="0dcd8-161">Azure DNS는 현재 DNSSEC를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-161">Azure DNS does not currently support DNSSEC.</span></span>

<span data-ttu-id="0dcd8-162">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-162">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="0dcd8-163">피드백 사이트를 사용하여 [이 기능에 대한 지원을 등록](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-163">You can use our feedback site to [register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).</span></span>

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a><span data-ttu-id="0dcd8-164">Azure DNS에서는 영역 전송(AXFR/IXFR)을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-164">Does Azure DNS support zone transfers (AXFR/IXFR)?</span></span>

<span data-ttu-id="0dcd8-165">아니요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-165">No.</span></span> <span data-ttu-id="0dcd8-166">Azure DNS는 현재 영역 전송을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-166">Azure DNS does not currently support zone transfers.</span></span> <span data-ttu-id="0dcd8-167">DNS 영역은 [Azure CLI를 사용하여 Azure DNS로 가져올 수 있습니다](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="0dcd8-167">DNS zones can be [imported into Azure DNS using the Azure CLI](dns-import-export.md).</span></span> <span data-ttu-id="0dcd8-168">그런 후 [Azure DNS 관리 포털](dns-operations-recordsets-portal.md), [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md) 또는 [CLI 도구](dns-operations-recordsets-cli.md)를 통해 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-168">DNS records can then be managed via the [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

<span data-ttu-id="0dcd8-169">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-169">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="0dcd8-170">피드백 사이트를 사용하여 [이 기능에 대한 지원을 등록](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-170">You can use our feedback site to [register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).</span></span>

### <a name="does-azure-dns-support-url-redirects"></a><span data-ttu-id="0dcd8-171">Azure DNS에서는 URL 리디렉션을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-171">Does Azure DNS support URL redirects?</span></span>

<span data-ttu-id="0dcd8-172">아니요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-172">No.</span></span> <span data-ttu-id="0dcd8-173">URL 리디렉션 서비스는 실제로 DNS 서비스가 아닙니다. 따라서 DNS 수준이 아닌 HTTP 수준에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-173">URL redirect services are not actually a DNS service - they work at the HTTP level, rather than the DNS level.</span></span> <span data-ttu-id="0dcd8-174">URL을 번들로 묶는 일부 DNS 공급자는 서비스를 전체 제품의 일부로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-174">Some DNS providers to bundle a URL redirect service as part of their overall offering.</span></span> <span data-ttu-id="0dcd8-175">현재 이 기능은 Azure DNS에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-175">This is not currently supported by Azure DNS.</span></span>

<span data-ttu-id="0dcd8-176">이 기능은 백로그에서 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-176">This feature is tracked on our backlog.</span></span> <span data-ttu-id="0dcd8-177">피드백 사이트를 사용하여 [이 기능에 대한 지원을 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-177">You can use our feedback site to [register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).</span></span>

## <a name="using-azure-dns"></a><span data-ttu-id="0dcd8-178">Azure DNS 사용</span><span class="sxs-lookup"><span data-stu-id="0dcd8-178">Using Azure DNS</span></span>

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a><span data-ttu-id="0dcd8-179">Azure DNS 및 다른 DNS 공급자를 사용하여 도메인을 공동 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-179">Can I co-host a domain using Azure DNS and another DNS provider?</span></span>

<span data-ttu-id="0dcd8-180">예.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-180">Yes.</span></span> <span data-ttu-id="0dcd8-181">Azure DNS에서는 다른 DNS 서비스와의 도메인 공동 호스팅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-181">Azure DNS supports co-hosting domains with other DNS services.</span></span>

<span data-ttu-id="0dcd8-182">이렇게 하려면 도메인의 NS 레코드(도메인에 대한 DNS 쿼리를 수신하는 공급자 제어)가 두 공급자의 이름 서버를 가리키도록 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-182">To do so, you need to modify the NS records for the domain (which control which providers receive DNS queries for the domain) to point to the name servers of both providers.</span></span> <span data-ttu-id="0dcd8-183">이러한 NS 레코드는 Azure DNS, 다른 공급자 및 부모 영역(일반적으로 도메인 이름 등록자를 통해 구성됨)의 세 위치에서 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-183">These NS records need to be modified in 3 places: in Azure DNS, in the other provider, and in the parent zone (typically configured via the domain name registrar).</span></span> <span data-ttu-id="0dcd8-184">DNS 위임에 대한 자세한 내용은 [DNS 도메인 위임](dns-domain-delegation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-184">For more information on DNS delegation, see [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="0dcd8-185">또한 도메인에 대한 DNS 레코드가 두 DNS 공급자 간에 동기화되는지도 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-185">In addition, you need to ensure that the DNS records for the domain are in sync between both DNS providers.</span></span> <span data-ttu-id="0dcd8-186">Azure DNS는 현재 DNS 영역 전송을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-186">Azure DNS does not currently support DNS zone transfers.</span></span> <span data-ttu-id="0dcd8-187">[Azure DNS 관리 포털](dns-operations-recordsets-portal.md), [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md) 또는 [CLI 도구](dns-operations-recordsets-cli.md)를 사용해서 DNS 레코드를 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-187">You need to synchronize DNS records using either the [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

### <a name="do-i-have-to-delegate-my-domain-to-all-4-azure-dns-name-servers"></a><span data-ttu-id="0dcd8-188">4개의 Azure DNS 이름 서버 모두에 도메인을 위임해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-188">Do I have to delegate my domain to all 4 Azure DNS name servers?</span></span>

<span data-ttu-id="0dcd8-189">예.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-189">Yes.</span></span> <span data-ttu-id="0dcd8-190">Azure DNS는 오류 격리 및 복원력 증가를 위해 각 DNS 영역에 4개의 이름 서버를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-190">Azure DNS assigns 4 name servers to each DNS zone, for fault isolation and increased resilience.</span></span> <span data-ttu-id="0dcd8-191">Azure DNS SLA를 충족하려면 4개의 이름 서버 모두에 도메인을 위임해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-191">To qualify for the Azure DNS SLA, you need to delegate your domain to all 4 name servers.</span></span>

### <a name="what-are-the-usage-limits-for-azure-dns"></a><span data-ttu-id="0dcd8-192">Azure DNS에 대한 사용량 제한은 얼마나 되나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-192">What are the usage limits for Azure DNS?</span></span>

<span data-ttu-id="0dcd8-193">Azure DNS를 사용할 경우 다음과 같은 기본 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-193">The following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a><span data-ttu-id="0dcd8-194">리소스 그룹 또는 구독 간에 Azure DNS 영역을 이동할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-194">Can I move an Azure DNS zone between resource groups or between subscriptions?</span></span>

<span data-ttu-id="0dcd8-195">예.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-195">Yes.</span></span> <span data-ttu-id="0dcd8-196">리소스 그룹 또는 구독 간에 DNS 영역을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-196">DNS zones can be moved between resource groups, or between subscriptions.</span></span>

<span data-ttu-id="0dcd8-197">DNS 영역을 이동할 때 DNS 쿼리는 아무런 영향도 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-197">There is no impact on DNS queries when moving a DNS zone.</span></span> <span data-ttu-id="0dcd8-198">영역에 할당된 이름 서버는 동일하게 유지되고 DNS 쿼리는 정상 처리량으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-198">The name servers assigned to the zone remain the same, and DNS queries are processed as normal throughout.</span></span>

<span data-ttu-id="0dcd8-199">DNS 영역을 이동하는 방법에 대한 자세한 내용 및 지침을 보려면 [새 리소스 그룹 또는 구독으로 리소스 이동](../azure-resource-manager/resource-group-move-resources.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-199">For more information and instructions on how to move DNS zones, see [Move resources to a new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

### <a name="how-long-does-it-take-for-dns-changes-to-take-effect"></a><span data-ttu-id="0dcd8-200">DNS 변경 내용이 적용되는 데 시간이 얼마나 걸리나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-200">How long does it take for DNS changes to take effect?</span></span>

<span data-ttu-id="0dcd8-201">새 DNS 영역 및 DNS 레코드는 일반적으로 Azure DNS 이름 서버에 몇 초 안에 신속하게 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-201">New DNS zones and DNS records are typically reflected on the Azure DNS name servers quickly, within a few seconds.</span></span>

<span data-ttu-id="0dcd8-202">기존 DNS 레코드에 대한 변경은 조금 더 오래 걸릴 수 있지만 60초 이내에 Azure DNS 이름 서버에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-202">Changes to existing DNS records can take a little longer, but should still be reflected on the Azure DNS name servers within 60 seconds.</span></span> <span data-ttu-id="0dcd8-203">이 경우 Azure DNS 외부의 DNS 캐싱(DNS 클라이언트 및 DNS 재귀 확인자에 의한) 또한 DNS 변경 내용이 적용되는 데 소요되는 시간에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-203">In this case, DNS caching outside of Azure DNS (by DNS clients and DNS recursive resolvers) can also impact the time taken for a DNS change to be effective.</span></span> <span data-ttu-id="0dcd8-204">이러한 캐시 기간은 각 레코드 집합의 TTL(Time-To-Live) 속성을 사용하여 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-204">This cache duration can be controlled using the Time-To-Live (TTL) property of each record set.</span></span>

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a><span data-ttu-id="0dcd8-205">실수로 삭제되지 않도록 내 DNS 영역을 보호하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-205">How can I protect my DNS zones against accidental deletion?</span></span>

<span data-ttu-id="0dcd8-206">Azure DNS는 Azure Resource Manager를 사용하여 관리되며 Azure Resource Manager가 제공하는 Access Control 기능을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-206">Azure DNS is managed using Azure Resource Manager, and benefits from the access control features that Azure Resource Manager provides.</span></span> <span data-ttu-id="0dcd8-207">역할 기반 Access Control는 DNS 영역 및 레코드 집합에 대한 읽기 또는 쓰기 액세스 권한이 있는 사용자를 제어하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-207">Role-based access control can be used to control which users have read or write access to DNS zones and record sets.</span></span> <span data-ttu-id="0dcd8-208">실수로 DNS 영역 및 레코드 집합을 수정하거나 삭제하지 않도록 하기 위해 리소스 잠금을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-208">Resource locks can be applied to prevent accidental modification or deletion of DNS zones and record sets.</span></span>

<span data-ttu-id="0dcd8-209">자세한 내용은 [DNS 영역 및 레코드 보호](dns-protect-zones-recordsets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-209">For more information, see [Protecting DNS Zones and Records](dns-protect-zones-recordsets.md).</span></span>

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a><span data-ttu-id="0dcd8-210">Azure DNS에서 SPF 레코드를 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-210">How do I set up SPF records in Azure DNS?</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a><span data-ttu-id="0dcd8-211">Azure DNS에서 IDN(국제 도메인 이름)을 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="0dcd8-211">How do I set up an International Domain Name (IDN) in Azure DNS?</span></span>

<span data-ttu-id="0dcd8-212">IDN(국제 도메인 이름)은 '[punycode](https://en.wikipedia.org/wiki/Punycode)'로 각 DNS 이름을 인코딩하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-212">International Domain Names (IDNs) work by encoding each DNS name using '[punycode](https://en.wikipedia.org/wiki/Punycode)'.</span></span> <span data-ttu-id="0dcd8-213">DNS 쿼리는 이러한 punycode로 인코딩된 이름을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-213">DNS queries are made using these punycode-encoded names.</span></span>

<span data-ttu-id="0dcd8-214">먼저 영역 이름 또는 레코드 집합 이름을 punycode로 변환하여 Azure DNS에서 IDN(국제 도메인 이름)을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-214">You can configure International Domain Names (IDNs) in Azure DNS by first converting the zone name or record set name to punycode.</span></span> <span data-ttu-id="0dcd8-215">Azure DNS는 현재 punycode로/부터의 기본 제공 변환을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0dcd8-215">Azure DNS does not currently support built-in conversion to/from punycode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dcd8-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0dcd8-216">Next steps</span></span>

<span data-ttu-id="0dcd8-217">[Azure DNS에 대해 자세히 알아보기](dns-overview.md)
</span><span class="sxs-lookup"><span data-stu-id="0dcd8-217">[Learn more about Azure DNS](dns-overview.md)
</span></span><br><span data-ttu-id="0dcd8-218">
[DNS 영역 및 레코드에 대해 자세히 알아보기](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="0dcd8-218">
[Learn more about DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="0dcd8-219">
[Azure DNS 시작](dns-getstarted-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0dcd8-219">
[Get started with Azure DNS](dns-getstarted-portal.md)</span></span>

