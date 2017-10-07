---
title: aaaAzure DNS FAQ | Microsoft Docs
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
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a><span data-ttu-id="5b1eb-103">Azure DNS FAQ</span><span class="sxs-lookup"><span data-stu-id="5b1eb-103">Azure DNS FAQ</span></span>

## <a name="about-azure-dns"></a><span data-ttu-id="5b1eb-104">Azure DNS 정보</span><span class="sxs-lookup"><span data-stu-id="5b1eb-104">About Azure DNS</span></span>

### <a name="what-is-azure-dns"></a><span data-ttu-id="5b1eb-105">Azure DNS란?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-105">What is Azure DNS?</span></span>

<span data-ttu-id="5b1eb-106">Domain Name System hello 또는 DNS는 변환 합니다 (또는 해결) 웹 사이트 또는 서비스 이름을 지정 tooits IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-106">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="5b1eb-107">Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-107">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="5b1eb-108">Azure에서 도메인을 호스트 하 여 DNS를 관리할 수 있습니다 레코드를 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 대금 청구 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-108">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

<span data-ttu-id="5b1eb-109">Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-109">DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="5b1eb-110">각 DNS 쿼리에 사용 가능한 가장 가까운 DNS 서버 hello에 응답할 수 있도록 애니캐스트 네트워킹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-110">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="5b1eb-111">이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-111">This provides both fast performance and high availability for your domain.</span></span>

<span data-ttu-id="5b1eb-112">hello Azure DNS 서비스는 Azure 리소스 관리자에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-112">hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="5b1eb-113">이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-113">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="5b1eb-114">도메인 및 레코드 hello Azure 포털, Azure PowerShell cmdlet 통해 관리할 수 있으며, 플랫폼 간 Azure CLI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-114">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="5b1eb-115">자동 DNS 관리를 요구 하는 응용 프로그램은 REST API와 Sdk hello 통해 hello 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-115">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

### <a name="how-much-does-azure-dns-cost"></a><span data-ttu-id="5b1eb-116">Azure DNS 비용은 얼마입니까?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-116">How much does Azure DNS cost?</span></span>

<span data-ttu-id="5b1eb-117">hello Azure DNS 청구 모델 hello 수가 Azure DNS 및 DNS 쿼리를 받게 hello 수에서 호스트 되는 DNS 영역을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-117">hello Azure DNS billing model is based on hello number of DNS zones hosted in Azure DNS and hello number of DNS queries they receive.</span></span> <span data-ttu-id="5b1eb-118">할인은 사용량에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-118">Discounts are provided based on usage.</span></span>

<span data-ttu-id="5b1eb-119">자세한 내용은 참조 hello [가격 책정 페이지 Azure DNS](https://azure.microsoft.com/pricing/details/dns/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-119">For more information, see hello [Azure DNS pricing page](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="what-is-hello-sla-for-azure-dns"></a><span data-ttu-id="5b1eb-120">Azure DNS에 대 한 hello SLA 란?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-120">What is hello SLA for Azure DNS?</span></span>

<span data-ttu-id="5b1eb-121">유효한 DNS 요청 받음을 응답 하나 이상의 Azure DNS 이름 서버에서 이상 hello 시간의 99.99% 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-121">We guarantee that valid DNS requests will receive a response from at least one Azure DNS name server at least 99.99% of hello time.</span></span>

<span data-ttu-id="5b1eb-122">자세한 내용은 참조 hello [Azure DNS SLA 페이지](https://azure.microsoft.com/support/legal/sla/dns)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-122">For more information, see hello [Azure DNS SLA page](https://azure.microsoft.com/support/legal/sla/dns).</span></span>

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a><span data-ttu-id="5b1eb-123">'DNS 영역'이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-123">What is a ‘DNS zone’?</span></span> <span data-ttu-id="5b1eb-124">동일한 DNS 도메인으로 hello 것은?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-124">Is it hello same as a DNS domain?</span></span> 

<span data-ttu-id="5b1eb-125">도메인 예를 들어 만든 'contoso.com' hello 도메인 이름 시스템에는 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-125">A domain is a unique name in hello domain name system, for example ‘contoso.com’.</span></span>

<span data-ttu-id="5b1eb-126">DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-126">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="5b1eb-127">예를 들어 contoso.com' hello 도메인' 예: (메일 서버)에 대 한 ' mail.contoso.com' 및 'www.contoso.com' (웹 사이트)에 대 한 여러 DNS 레코드를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-127">For example, hello domain ‘contoso.com’ may contain several DNS records, such as ‘mail.contoso.com’ (for a mail server) and ‘www.contoso.com’ (for a web site).</span></span> <span data-ttu-id="5b1eb-128">이러한 hello DNS 영역 'contoso.com'에서 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-128">These would be hosted in hello DNS zone 'contoso.com'.</span></span>

<span data-ttu-id="5b1eb-129">도메인 이름이 *이름만*인 반면, DNS 영역은 도메인 이름에 대 한 hello DNS 레코드를 포함 하는 데이터 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-129">A domain name is *just a name*, whereas a DNS zone is a data resource containing hello DNS records for a domain name.</span></span> <span data-ttu-id="5b1eb-130">Azure DNS toohost DNS 영역을 허용 하 고 Azure에서 도메인에 대 한 hello DNS 레코드를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-130">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="5b1eb-131">DNS 이름 서버 hello 인터넷에서에서 tooanswer DNS 쿼리도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-131">It also provides DNS name servers tooanswer DNS queries from hello Internet.</span></span>

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a><span data-ttu-id="5b1eb-132">DNS 도메인 이름 toouse Azure DNS toopurchase 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-132">Do I need toopurchase a DNS domain name toouse Azure DNS?</span></span> 

<span data-ttu-id="5b1eb-133">그럴 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-133">Not necessarily.</span></span>

<span data-ttu-id="5b1eb-134">Toopurchase 도메인 toohost Azure DNS에 DNS 영역을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-134">You do not need toopurchase a domain toohost a DNS zone in Azure DNS.</span></span> <span data-ttu-id="5b1eb-135">Hello 도메인 이름을 소유 하지 않고 언제 든 지 DNS 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-135">You can create a DNS zone at any time without owning hello domain name.</span></span> <span data-ttu-id="5b1eb-136">이 영역에 대 한 DNS 쿼리 하는 경우 이러한 보내지는지 toohello Azure DNS 이름 서버 toohello 영역 할당을 해결만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-136">DNS queries for this zone will only resolve if they are directed toohello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="5b1eb-137">Hello 글로벌 DNS 계층-이 사용 하면 DNS에서 아무 곳 이나의 쿼리 hello world toofind DNS 영역 및 DNS 레코드를 응답에 toolink DNS 영역이 복원할 toopurchase hello 도메인 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-137">You need toopurchase hello domain name if you want toolink your DNS zone into hello global DNS hierarchy – this enables DNS queries from anywhere in hello world toofind your DNS zone and be answered with your DNS records.</span></span>

## <a name="azure-dns-features"></a><span data-ttu-id="5b1eb-138">Azure DNS 기능</span><span class="sxs-lookup"><span data-stu-id="5b1eb-138">Azure DNS Features</span></span>

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a><span data-ttu-id="5b1eb-139">Azure DNS는 DNS 기반 트래픽 라우팅 또는 끝점 장애 조치(failover)를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-139">Does Azure DNS support DNS-based traffic routing or endpoint failover?</span></span>

<span data-ttu-id="5b1eb-140">DNS 기반 트래픽 라우팅 및 끝점 장애 조치(failover)는 Azure Traffic Manager에 의해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-140">DNS-based traffic routing and endpoint failover are provided by Azure Traffic Manager.</span></span> <span data-ttu-id="5b1eb-141">이것은 Azure DNS와 함께 사용할 수 있는 별도 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-141">This is a separate Azure service that can be used together with Azure DNS.</span></span> <span data-ttu-id="5b1eb-142">자세한 내용은 참조 hello [트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-142">For more information, see hello [Traffic Manager overview](../traffic-manager/traffic-manager-overview.md).</span></span>

<span data-ttu-id="5b1eb-143">Azure DNS가 지정된 된 DNS 레코드에 대 한 각 DNS 쿼리에 hello를 항상 받는 'static' DNS 도메인 호스팅만 지원 같은 DNS 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-143">Azure DNS only supports hosting 'static' DNS domains, where each DNS query for a given DNS record always receives hello same DNS response.</span></span>

### <a name="does-azure-dns-support-domain-name-registration"></a><span data-ttu-id="5b1eb-144">Azure DNS는 도메인 이름 등록을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-144">Does Azure DNS support domain name registration?</span></span>

<span data-ttu-id="5b1eb-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-145">No.</span></span> <span data-ttu-id="5b1eb-146">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-146">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="5b1eb-147">Toopurchase 도메인을 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-147">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="5b1eb-148">hello 등록 기관에는 일반적으로 작은 연간 요금 요금.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-148">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="5b1eb-149">hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-149">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="5b1eb-150">참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-150">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

<span data-ttu-id="5b1eb-151">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-151">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="5b1eb-152">피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-152">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).</span></span>

### <a name="does-azure-dns-support-private-domains"></a><span data-ttu-id="5b1eb-153">Azure DNS에서는 '개인' 도메인을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-153">Does Azure DNS support 'private' domains?</span></span>

<span data-ttu-id="5b1eb-154">아니요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-154">No.</span></span> <span data-ttu-id="5b1eb-155">Azure DNS는 현재 인터넷 연결 도메인만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-155">Azure DNS currently only supports Internet-facing domains.</span></span>

<span data-ttu-id="5b1eb-156">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-156">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="5b1eb-157">피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-157">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).</span></span>

<span data-ttu-id="5b1eb-158">Azure의 내부 DNS 옵션에 대한 자세한 내용은 [VM 및 역할 인스턴스에 대한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-158">For information on internal DNS options in Azure, see [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

### <a name="does-azure-dns-support-dnssec"></a><span data-ttu-id="5b1eb-159">Azure DNS에서는 DNSSEC를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-159">Does Azure DNS support DNSSEC?</span></span>

<span data-ttu-id="5b1eb-160">아니요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-160">No.</span></span> <span data-ttu-id="5b1eb-161">Azure DNS는 현재 DNSSEC를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-161">Azure DNS does not currently support DNSSEC.</span></span>

<span data-ttu-id="5b1eb-162">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-162">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="5b1eb-163">피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-163">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).</span></span>

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a><span data-ttu-id="5b1eb-164">Azure DNS에서는 영역 전송(AXFR/IXFR)을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-164">Does Azure DNS support zone transfers (AXFR/IXFR)?</span></span>

<span data-ttu-id="5b1eb-165">아니요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-165">No.</span></span> <span data-ttu-id="5b1eb-166">Azure DNS는 현재 영역 전송을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-166">Azure DNS does not currently support zone transfers.</span></span> <span data-ttu-id="5b1eb-167">DNS 영역 수 [hello Azure CLI를 사용 하 여 Azure DNS로 가져온](dns-import-export.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-167">DNS zones can be [imported into Azure DNS using hello Azure CLI](dns-import-export.md).</span></span> <span data-ttu-id="5b1eb-168">DNS 레코드 hello를 통해 관리할 수 있습니다 [Azure DNS 관리 포털](dns-operations-recordsets-portal.md), 우리의 [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md), 또는 [ CLI 도구](dns-operations-recordsets-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-168">DNS records can then be managed via hello [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

<span data-ttu-id="5b1eb-169">이 기능은 백로그에서 추적하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-169">This is a feature we are tracking on our backlog.</span></span> <span data-ttu-id="5b1eb-170">피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-170">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).</span></span>

### <a name="does-azure-dns-support-url-redirects"></a><span data-ttu-id="5b1eb-171">Azure DNS에서는 URL 리디렉션을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-171">Does Azure DNS support URL redirects?</span></span>

<span data-ttu-id="5b1eb-172">아니요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-172">No.</span></span> <span data-ttu-id="5b1eb-173">URL 리디렉션 서비스는 DNS 서비스에 실제로 없는-hello DNS 수준 대신 hello HTTP 수준에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-173">URL redirect services are not actually a DNS service - they work at hello HTTP level, rather than hello DNS level.</span></span> <span data-ttu-id="5b1eb-174">일부 URL의 DNS 공급자 toobundle 서비스를 전반적인 제공의 일환으로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-174">Some DNS providers toobundle a URL redirect service as part of their overall offering.</span></span> <span data-ttu-id="5b1eb-175">현재 이 기능은 Azure DNS에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-175">This is not currently supported by Azure DNS.</span></span>

<span data-ttu-id="5b1eb-176">이 기능은 백로그에서 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-176">This feature is tracked on our backlog.</span></span> <span data-ttu-id="5b1eb-177">피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-177">You can use our feedback site too[register your support for this feature](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).</span></span>

## <a name="using-azure-dns"></a><span data-ttu-id="5b1eb-178">Azure DNS 사용</span><span class="sxs-lookup"><span data-stu-id="5b1eb-178">Using Azure DNS</span></span>

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a><span data-ttu-id="5b1eb-179">Azure DNS 및 다른 DNS 공급자를 사용하여 도메인을 공동 호스트할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-179">Can I co-host a domain using Azure DNS and another DNS provider?</span></span>

<span data-ttu-id="5b1eb-180">예.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-180">Yes.</span></span> <span data-ttu-id="5b1eb-181">Azure DNS에서는 다른 DNS 서비스와의 도메인 공동 호스팅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-181">Azure DNS supports co-hosting domains with other DNS services.</span></span>

<span data-ttu-id="5b1eb-182">toodo 따라서 hello 도메인 (어떤 공급자 DNS를 수신 하는 컨트롤 hello 도메인에 대 한 쿼리)에 대 한 toomodify hello NS 레코드를 해야 하는 두 공급자의 toopoint toohello 이름 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-182">toodo so, you need toomodify hello NS records for hello domain (which control which providers receive DNS queries for hello domain) toopoint toohello name servers of both providers.</span></span> <span data-ttu-id="5b1eb-183">이러한 NS 레코드 toobe 3 위치 수정 필요: Azure DNS에서 다른 공급자를 hello 및 hello 부모 영역 (도메인 이름 등록 기관 hello 통해 일반적으로 구성 됨).</span><span class="sxs-lookup"><span data-stu-id="5b1eb-183">These NS records need toobe modified in 3 places: in Azure DNS, in hello other provider, and in hello parent zone (typically configured via hello domain name registrar).</span></span> <span data-ttu-id="5b1eb-184">DNS 위임에 대한 자세한 내용은 [DNS 도메인 위임](dns-domain-delegation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-184">For more information on DNS delegation, see [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="5b1eb-185">또한 tooensure hello 도메인에 대 한 hello DNS 레코드는 모두 DNS 공급자 간의 동기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-185">In addition, you need tooensure that hello DNS records for hello domain are in sync between both DNS providers.</span></span> <span data-ttu-id="5b1eb-186">Azure DNS는 현재 DNS 영역 전송을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-186">Azure DNS does not currently support DNS zone transfers.</span></span> <span data-ttu-id="5b1eb-187">Hello 중 하나를 사용 하 여 toosynchronize DNS 레코드를 필요한 [Azure DNS 관리 포털](dns-operations-recordsets-portal.md), 우리의 [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md) 또는 [CLI 도구](dns-operations-recordsets-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-187">You need toosynchronize DNS records using either hello [Azure DNS management portal](dns-operations-recordsets-portal.md), our [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlets](dns-operations-recordsets.md), or [CLI tool](dns-operations-recordsets-cli.md).</span></span>

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a><span data-ttu-id="5b1eb-188">용량은 toodelegate 내 도메인 tooall 4 Azure DNS 이름 서버</span><span class="sxs-lookup"><span data-stu-id="5b1eb-188">Do I have toodelegate my domain tooall 4 Azure DNS name servers?</span></span>

<span data-ttu-id="5b1eb-189">예.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-189">Yes.</span></span> <span data-ttu-id="5b1eb-190">Azure DNS 오류 격리 및 향상 된 복원 력 tooeach DNS 영역 이름은 4 대의 서버를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-190">Azure DNS assigns 4 name servers tooeach DNS zone, for fault isolation and increased resilience.</span></span> <span data-ttu-id="5b1eb-191">에 대 한 tooqualify hello Azure DNS SLA toodelegate tooall 4 도메인 이름 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-191">tooqualify for hello Azure DNS SLA, you need toodelegate your domain tooall 4 name servers.</span></span>

### <a name="what-are-hello-usage-limits-for-azure-dns"></a><span data-ttu-id="5b1eb-192">Azure DNS에 대 한 hello 사용 제한 사항은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-192">What are hello usage limits for Azure DNS?</span></span>

<span data-ttu-id="5b1eb-193">기본 제한 값을 다음 hello Azure DNS를 사용 하는 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-193">hello following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a><span data-ttu-id="5b1eb-194">리소스 그룹 또는 구독 간에 Azure DNS 영역을 이동할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-194">Can I move an Azure DNS zone between resource groups or between subscriptions?</span></span>

<span data-ttu-id="5b1eb-195">예.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-195">Yes.</span></span> <span data-ttu-id="5b1eb-196">리소스 그룹 또는 구독 간에 DNS 영역을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-196">DNS zones can be moved between resource groups, or between subscriptions.</span></span>

<span data-ttu-id="5b1eb-197">DNS 영역을 이동할 때 DNS 쿼리는 아무런 영향도 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-197">There is no impact on DNS queries when moving a DNS zone.</span></span> <span data-ttu-id="5b1eb-198">hello 이름 서버 toohello 영역 할당 유지 hello를 동일 하 고 DNS 쿼리 전체에서 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-198">hello name servers assigned toohello zone remain hello same, and DNS queries are processed as normal throughout.</span></span>

<span data-ttu-id="5b1eb-199">자세한 내용 및 방법에 대 한 toomove DNS 영역 참조 [리소스 tooa 새 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-199">For more information and instructions on how toomove DNS zones, see [Move resources tooa new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a><span data-ttu-id="5b1eb-200">가 소요 DNS 변경 내용 tootake 효과 대 한?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-200">How long does it take for DNS changes tootake effect?</span></span>

<span data-ttu-id="5b1eb-201">새 DNS 영역 및 DNS 레코드 일반적으로 내에 반영 되도록 hello Azure DNS 이름 서버에 신속 하 게 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-201">New DNS zones and DNS records are typically reflected on hello Azure DNS name servers quickly, within a few seconds.</span></span>

<span data-ttu-id="5b1eb-202">Tooexisting DNS 레코드 변경 내용 약간 더 길 걸릴 수 있지만 60 초 이내 hello Azure DNS 이름 서버에 여전히 반영 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-202">Changes tooexisting DNS records can take a little longer, but should still be reflected on hello Azure DNS name servers within 60 seconds.</span></span> <span data-ttu-id="5b1eb-203">이 경우 DNS (DNS 클라이언트 및 DNS 재귀 확인자)에서 Azure DNS 외부에서 캐싱도 DNS 변경 toobe 효과적인에 걸린 hello 시간을 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-203">In this case, DNS caching outside of Azure DNS (by DNS clients and DNS recursive resolvers) can also impact hello time taken for a DNS change toobe effective.</span></span> <span data-ttu-id="5b1eb-204">각 레코드 집합의 hello Time To Live (TTL) 속성을 사용 하 여이 캐시 기간을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-204">This cache duration can be controlled using hello Time-To-Live (TTL) property of each record set.</span></span>

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a><span data-ttu-id="5b1eb-205">실수로 삭제되지 않도록 내 DNS 영역을 보호하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-205">How can I protect my DNS zones against accidental deletion?</span></span>

<span data-ttu-id="5b1eb-206">Azure DNS는 Azure 리소스 관리자를 사용 하 여 관리 되 고 하면 도움이 hello Azure 리소스 관리자는 제어 기능에 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-206">Azure DNS is managed using Azure Resource Manager, and benefits from hello access control features that Azure Resource Manager provides.</span></span> <span data-ttu-id="5b1eb-207">역할 기반 액세스 제어에 사용 되는 toocontrol 읽기 또는 쓰기 액세스 tooDNS 영역 및 레코드 집합 수 있는 사용자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-207">Role-based access control can be used toocontrol which users have read or write access tooDNS zones and record sets.</span></span> <span data-ttu-id="5b1eb-208">리소스 잠금을 DNS 영역 및 레코드 집합의 적용 된 tooprevent 실수로 수정 또는 삭제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-208">Resource locks can be applied tooprevent accidental modification or deletion of DNS zones and record sets.</span></span>

<span data-ttu-id="5b1eb-209">자세한 내용은 [DNS 영역 및 레코드 보호](dns-protect-zones-recordsets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-209">For more information, see [Protecting DNS Zones and Records](dns-protect-zones-recordsets.md).</span></span>

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a><span data-ttu-id="5b1eb-210">Azure DNS에서 SPF 레코드를 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-210">How do I set up SPF records in Azure DNS?</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a><span data-ttu-id="5b1eb-211">Azure DNS에서 IDN(국제 도메인 이름)을 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="5b1eb-211">How do I set up an International Domain Name (IDN) in Azure DNS?</span></span>

<span data-ttu-id="5b1eb-212">IDN(국제 도메인 이름)은 '[punycode](https://en.wikipedia.org/wiki/Punycode)'로 각 DNS 이름을 인코딩하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-212">International Domain Names (IDNs) work by encoding each DNS name using '[punycode](https://en.wikipedia.org/wiki/Punycode)'.</span></span> <span data-ttu-id="5b1eb-213">DNS 쿼리는 이러한 punycode로 인코딩된 이름을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-213">DNS queries are made using these punycode-encoded names.</span></span>

<span data-ttu-id="5b1eb-214">레코드 집합 이름 toopunycode 또는 첫 번째 변환 하는 동안 hello 영역 이름으로 Azure DNS에 국제 Idn (도메인 이름)을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-214">You can configure International Domain Names (IDNs) in Azure DNS by first converting hello zone name or record set name toopunycode.</span></span> <span data-ttu-id="5b1eb-215">Azure DNS는 현재 punycode로/부터의 기본 제공 변환을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b1eb-215">Azure DNS does not currently support built-in conversion to/from punycode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b1eb-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b1eb-216">Next steps</span></span>

<span data-ttu-id="5b1eb-217">[Azure DNS에 대해 자세히 알아보기](dns-overview.md)
</span><span class="sxs-lookup"><span data-stu-id="5b1eb-217">[Learn more about Azure DNS](dns-overview.md)
</span></span><br><span data-ttu-id="5b1eb-218">
[DNS 영역 및 레코드에 대해 자세히 알아보기](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="5b1eb-218">
[Learn more about DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5b1eb-219">
[Azure DNS 시작](dns-getstarted-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5b1eb-219">
[Get started with Azure DNS](dns-getstarted-portal.md)</span></span>

