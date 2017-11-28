---
title: "Azure DNS의 aaaOverview | Microsoft Docs"
description: "Microsoft Azure의 DNS 호스팅 서비스 개요입니다. Microsoft Azure에 도메인을 호스트하세요."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="f7075-104">Azure DNS 개요</span><span class="sxs-lookup"><span data-stu-id="f7075-104">Azure DNS overview</span></span>

<span data-ttu-id="f7075-105">Domain Name System hello 또는 DNS는 변환 합니다 (또는 해결) 웹 사이트 또는 서비스 이름을 지정 tooits IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="f7075-106">Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="f7075-107">Azure에서 도메인을 호스트 하 여 DNS를 관리할 수 있습니다 레코드를 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 대금 청구 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS 개요](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="f7075-109">기능</span><span class="sxs-lookup"><span data-stu-id="f7075-109">Features</span></span>

* <span data-ttu-id="f7075-110">**안정성 및 성능** - Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="f7075-111">각 DNS 쿼리에 사용 가능한 가장 가까운 DNS 서버 hello에 응답할 수 있도록 애니캐스트 네트워킹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="f7075-112">이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="f7075-113">**완벽 한 통합** -hello Azure DNS 서비스는 Azure 서비스에 대 한 DNS 레코드 사용된 toomanage 수 있으며 외부 리소스에 대 한 DNS tooprovide 사용된 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="f7075-114">Azure DNS 프로토콜은 hello Azure 포털에에서 통합 하 고 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, 청구 및 지원 계약 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="f7075-115">**보안** -hello Azure DNS 서비스는 Azure 리소스 관리자에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="f7075-116">이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="f7075-117">도메인 및 레코드 hello Azure 포털, Azure PowerShell cmdlet 통해 관리할 수 있으며, 플랫폼 간 Azure CLI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="f7075-118">자동 DNS 관리를 요구 하는 응용 프로그램은 REST API와 Sdk hello 통해 hello 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="f7075-119">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="f7075-120">Toopurchase 도메인을 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="f7075-121">hello 등록 기관에는 일반적으로 작은 연간 요금 요금.</span><span class="sxs-lookup"><span data-stu-id="f7075-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="f7075-122">hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="f7075-123">참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="f7075-124">가격</span><span class="sxs-lookup"><span data-stu-id="f7075-124">Pricing</span></span>

<span data-ttu-id="f7075-125">DNS 요금 청구는 hello 수가 hello DNS 쿼리 수 및 Azure에서 호스팅되는 DNS 영역을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="f7075-126">방문 가격에 대 한 자세한 toolearn [Azure DNS 가격](https://azure.microsoft.com/pricing/details/dns/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="f7075-127">FAQ</span><span class="sxs-lookup"><span data-stu-id="f7075-127">FAQ</span></span>

<span data-ttu-id="f7075-128">Azure DNS에 대 한 자주 묻는 질문에 대 한 참조 hello [Azure DNS FAQ](dns-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7075-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7075-129">Next steps</span></span>

<span data-ttu-id="f7075-130">[DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하여 DNS 영역 및 레코드에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="f7075-131">너무 방법에 대해 알아봅니다[DNS 영역을 만드는](./dns-getstarted-create-dnszone-portal.md) Azure DNS에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="f7075-132">일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7075-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

