---
title: "Azure DNS 개요 | Microsoft 문서"
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
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="45a76-104">Azure DNS 개요</span><span class="sxs-lookup"><span data-stu-id="45a76-104">Azure DNS overview</span></span>

<span data-ttu-id="45a76-105">Domain Name System, 즉 DNS는 웹 사이트 또는 서비스 이름을 해당 IP 주소로 변환(또는 확인)합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="45a76-106">Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="45a76-107">Azure에 도메인을 호스트하면 다른 Azure 서비스와 동일한 자격 증명, API, 도구 및 대금 청구를 사용하여 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS 개요](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="45a76-109">기능</span><span class="sxs-lookup"><span data-stu-id="45a76-109">Features</span></span>

* <span data-ttu-id="45a76-110">**안정성 및 성능** - Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="45a76-111">사용 가능한 가장 가까운 DNS 서버에서 각 DNS 쿼리에 응답하도록 애니캐스트 네트워킹이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="45a76-112">이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="45a76-113">**원활한 통합** - Azure DNS 서비스를 사용하여 Azure 서비스에 대한 DNS 레코드를 관리하고 외부 리소스에 DNS를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="45a76-114">Azure DNS는 Azure Portal에 통합되며 다른 Azure 서비스와 동일한 자격 증명, 청구 및 지원 계약을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="45a76-115">**보안** - Azure DNS 서비스는 Azure Resource Manager를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="45a76-116">이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="45a76-117">도메인과 레코드는 Azure 포털, Azure PowerShell cmdlet 및 플랫폼 간 Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="45a76-118">자동 DNS 관리가 필요한 응용 프로그램은 REST API 및 SDK를 통해 서비스와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="45a76-119">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="45a76-120">도메인을 구입하려면 타사 도메인 이름 등록 기관을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="45a76-121">등록 기관은 일반적으로 소액의 연간 요금을 부과합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="45a76-122">그런 다음, DNS 레코드의 관리를 위해 Azure DNS에 해당 도메인을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="45a76-123">자세한 내용은 [Azure DNS에 도메인 위임](dns-domain-delegation.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a76-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="45a76-124">가격</span><span class="sxs-lookup"><span data-stu-id="45a76-124">Pricing</span></span>

<span data-ttu-id="45a76-125">DNS 요금 청구는 Azure에 호스트되는 DNS 영역의 수와 DNS 쿼리 수를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="45a76-126">가격 책정에 대한 자세한 내용은 [Azure DNS 가격 책정](https://azure.microsoft.com/pricing/details/dns/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a76-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="45a76-127">FAQ</span><span class="sxs-lookup"><span data-stu-id="45a76-127">FAQ</span></span>

<span data-ttu-id="45a76-128">Azure DNS에 대한 질문과 대답을 보려면 [Azure DNS FAQ](dns-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45a76-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a76-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45a76-129">Next steps</span></span>

<span data-ttu-id="45a76-130">[DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하여 DNS 영역 및 레코드에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="45a76-131">Azure DNS에 [DNS 영역을 만드는](./dns-getstarted-create-dnszone-portal.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="45a76-132">Azure의 다른 주요 [네트워킹 기능](../networking/networking-overview.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="45a76-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

