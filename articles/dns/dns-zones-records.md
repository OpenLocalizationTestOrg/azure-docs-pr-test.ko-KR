---
title: "DNS 영역 및 레코드 개요-Azure DNS | Microsoft Docs"
description: "Microsoft Azure DNS에서 DNS 영역 및 레코드 호스팅에 대한 지원 개요."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: 5818986c939c464a364c52ab31225e15130ab30e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-dns-zones-and-records"></a><span data-ttu-id="034cd-103">DNS 영역 및 레코드 개요</span><span class="sxs-lookup"><span data-stu-id="034cd-103">Overview of DNS zones and records</span></span>

<span data-ttu-id="034cd-104">이 페이지는 도메인, DNS 영역, DNS 레코드 및 레코드 집합의 핵심 개념과 Azure DNS에서 지원되는 방식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-104">This page explains the key concepts of domains, DNS zones, and DNS records and record sets, and how they are supported in Azure DNS.</span></span>

## <a name="domain-names"></a><span data-ttu-id="034cd-105">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="034cd-105">Domain names</span></span>

<span data-ttu-id="034cd-106">Domain Name System은 도메인 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-106">The Domain Name System is a hierarchy of domains.</span></span> <span data-ttu-id="034cd-107">계층 구조는 이름이 단순히 '**.**'인 'root' 도메인에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-107">The hierarchy starts from the 'root' domain, whose name is simply '**.**'.</span></span>  <span data-ttu-id="034cd-108">그 아래에 'com', 'net', 'org', 'uk' 또는 'jp'와 같은 최상위 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-108">Below this come top-level domains, such as 'com', 'net', 'org', 'uk' or 'jp'.</span></span>  <span data-ttu-id="034cd-109">그 아래에 'org.uk' 또는 'co.jp'와 같은 두 번째 수준의 도메인이 있는</span><span class="sxs-lookup"><span data-stu-id="034cd-109">Below these are second-level domains, such as 'org.uk' or 'co.jp'.</span></span> <span data-ttu-id="034cd-110">DNS 계층 구조의 도메인은 전체적으로 분산되며 전 세계의 DNS 이름 서버에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-110">The domains in the DNS hierarchy are globally distributed, hosted by DNS name servers around the world.</span></span>

<span data-ttu-id="034cd-111">도메인 이름 등록 기관은 'contoso.com'과 같은 도메인 이름을 구입할 수 있는 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-111">A domain name registrar is an organization that allows you to purchase a domain name, such as 'contoso.com'.</span></span>  <span data-ttu-id="034cd-112">도메인 이름을 구입할 경우 해당 이름 하의 DNS 계층 구조를 관리할 수 있습니다. 예를 들어, 'www.contoso.com'이라는 이름을 회사 웹 사이트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-112">Purchasing a domain name gives you the right to control the DNS hierarchy under that name, for example allowing you to direct the name 'www.contoso.com' to your company web site.</span></span> <span data-ttu-id="034cd-113">등록 기관은 사용자 대신 자체 이름 서버에 도메인을 호스트하거나 사용자가 다른 이름 서버를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-113">The registrar may host the domain in its own name servers on your behalf, or allow you to specify alternative name servers.</span></span>

<span data-ttu-id="034cd-114">Azure DNS는 전 세계적으로 분산된 고가용성 이름 서버 인프라를 제공하므로 조직은 이러한 인프라를 사용하여 도메인을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-114">Azure DNS provides a globally distributed, high-availability name server infrastructure, which you can use to host your domain.</span></span> <span data-ttu-id="034cd-115">Azure에 도메인을 호스팅하면 다른 Azure 서비스와 동일한 자격 증명, API, 도구 및 대금 청구를 사용하여 DNS 레코드를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-115">By hosting your domains in Azure DNS, you can manage your DNS records with the same credentials, APIs, tools, billing, and support as your other Azure services.</span></span>

<span data-ttu-id="034cd-116">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-116">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="034cd-117">도메인 이름을 구입하려면 타사 도메인 이름 등록 기관을 이용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-117">If you want to purchase a domain name, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="034cd-118">등록 기관은 일반적으로 소액의 연간 요금을 부과합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-118">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="034cd-119">그런 다음, DNS 레코드의 관리를 위해 Azure DNS에 해당 도메인을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-119">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="034cd-120">자세한 내용은 [Azure DNS에 도메인 위임](dns-domain-delegation.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="034cd-120">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="dns-zones"></a><span data-ttu-id="034cd-121">DNS 영역 </span><span class="sxs-lookup"><span data-stu-id="034cd-121">DNS zones</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a><span data-ttu-id="034cd-122">DNS 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-122">DNS records</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a><span data-ttu-id="034cd-123">Time-to-Live</span><span class="sxs-lookup"><span data-stu-id="034cd-123">Time-to-live</span></span>

<span data-ttu-id="034cd-124">Time-to-Live, 즉 TTL은 각 레코드가 다시 쿼리되기 전에 클라이언트에 캐시되는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-124">The time to live, or TTL, specifies how long each record is cached by clients before being re-queried.</span></span> <span data-ttu-id="034cd-125">위 예제에서 TTL은 3600초, 즉 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-125">In the above example, the TTL is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="034cd-126">Azure DNS에서 TTL은 각 레코드가 아니라 레코드 집합에 대해 지정되므로 해당 레코드 집합 내의 모든 레코드에 동일한 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-126">In Azure DNS, the TTL is specified for the record set, not for each record, so the same value is used for all records within that record set.</span></span>  <span data-ttu-id="034cd-127">1 ~ 2,147,483,647초 사이의 TTL 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-127">You can specify any TTL value between 1 and 2,147,483,647 seconds.</span></span>

### <a name="wildcard-records"></a><span data-ttu-id="034cd-128">와일드카드 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-128">Wildcard records</span></span>

<span data-ttu-id="034cd-129">Azure DNS는 [와일드카드 레코드](https://en.wikipedia.org/wiki/Wildcard_DNS_record)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-129">Azure DNS supports [wildcard records](https://en.wikipedia.org/wiki/Wildcard_DNS_record).</span></span> <span data-ttu-id="034cd-130">와일드카드 레코드는 쿼리에 대한 응답으로 일치하는 이름을 반환합니다(와일드카드가 아닌 레코드 집합에서 가까운 일치 항목이 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="034cd-130">Wildcard records are returned in response to any query with a matching name (unless there is a closer match from a non-wildcard record set).</span></span> <span data-ttu-id="034cd-131">Azure DNS는 NS 및 SOA를 제외한 모든 레코드 종류에 대해 와일드카드 레코드 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-131">Azure DNS supports wildcard record sets for all record types except NS and SOA.</span></span>

<span data-ttu-id="034cd-132">와일드카드 레코드 집합을 만들려면 레코드 집합 이름 '\*'을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-132">To create a wildcard record set, use the record set name '\*'.</span></span> <span data-ttu-id="034cd-133">또는 맨 왼쪽의 레이블로 '\*'가 포함된 이름을 사용할 수 있습니다(예: '\*.foo').</span><span class="sxs-lookup"><span data-stu-id="034cd-133">Alternatively, you can also use a name with '\*' as its left-most label, for example, '\*.foo'.</span></span>

### <a name="cname-records"></a><span data-ttu-id="034cd-134">CNAME 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-134">CNAME records</span></span>

<span data-ttu-id="034cd-135">CNAME 레코드 집합은 동일한 이름의 다른 레코드 집합과 함께 존재할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-135">CNAME record sets cannot coexist with other record sets with the same name.</span></span> <span data-ttu-id="034cd-136">예를 들어 상대 이름이 'www'인 CNAME 레코드 집합과 상대 이름이 'www'인 A 레코드를 동시에 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-136">For example, you cannot create a CNAME record set with the relative name 'www' and an A record with the relative name 'www' at the same time.</span></span>

<span data-ttu-id="034cd-137">영역 루트(이름 = '@')는 항상 영역을 만들 때 생성된 NS 및 SOA 레코드 집합을 포함하므로 영역 루트에 CNAME 레코드 집합을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-137">Because the zone apex (name = '@') always contains the NS and SOA record sets that were created when the zone was created, you can't create a CNAME record set at the zone apex.</span></span>

<span data-ttu-id="034cd-138">이러한 제약 조건은 DNS 표준에서 발생하며 Azure DNS의 제한 사항이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-138">These constraints arise from the DNS standards and are not limitations of Azure DNS.</span></span>

### <a name="ns-records"></a><span data-ttu-id="034cd-139">NS 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-139">NS records</span></span>

<span data-ttu-id="034cd-140">영역 루트의 NS 레코드 집합(name '@')은 각 DNS 영역과 함께 자동으로 생성되며 영역이 삭제될 경우 자동으로 삭제됩니다(별도로 삭제할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="034cd-140">The NS record set at the zone apex (name '@') is created automatically with each DNS zone, and is deleted automatically when the zone is deleted (it cannot be deleted separately).</span></span>

<span data-ttu-id="034cd-141">이 레코드 집합에는 영역에 할당된 Azure DNS 이름 서버의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-141">This record set contains the names of the Azure DNS name servers assigned to the zone.</span></span> <span data-ttu-id="034cd-142">이 NS 레코드 집합에 추가 이름 서버를 추가하여 DNS 공급자가 2개 이상 있는 공동 호스팅 도메인을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-142">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="034cd-143">또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-143">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="034cd-144">그러나 미리 채워진 Azure DNS 이름 서버를 제거 또는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-144">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span> 

<span data-ttu-id="034cd-145">이는 영역 루트에 있는 NS 레코드 집합에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-145">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="034cd-146">영역의 다른 NS 레코드 집합은 제약 없이 생성, 수정 및 삭제할 수 있습니다(자식 영역을 위임하는 데 사용되므로).</span><span class="sxs-lookup"><span data-stu-id="034cd-146">Other NS record sets in your zone (as used to delegate child zones) can be created, modified and deleted without constraint.</span></span>

### <a name="soa-records"></a><span data-ttu-id="034cd-147">SOA 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-147">SOA records</span></span>

<span data-ttu-id="034cd-148">SOA 레코드는 각 영역의 루트(name = '@')에서 자동으로 생성되며 영역이 삭제될 경우 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-148">A SOA record set is created automatically at the apex of each zone (name = '@'), and is deleted automatically when the zone is deleted.</span></span>  <span data-ttu-id="034cd-149">SOA 레코드는 별도로 생성 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-149">SOA records cannot be created or deleted separately.</span></span>

<span data-ttu-id="034cd-150">SOA 레코드에서 'host' 속성(Azure DNS에서 제공한 기본 이름 서버 이름을 참조하도록 사전 구성됨)을 제외한 모든 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-150">You can modify all properties of the SOA record except for the 'host' property, which is pre-configured to refer to the primary name server name provided by Azure DNS.</span></span>

### <a name="spf-records"></a><span data-ttu-id="034cd-151">SPF 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-151">SPF records</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a><span data-ttu-id="034cd-152">SRV 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-152">SRV records</span></span>

<span data-ttu-id="034cd-153">[SRV 레코드](https://en.wikipedia.org/wiki/SRV_record)는 다양한 서비스에서 서버 위치를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-153">[SRV records](https://en.wikipedia.org/wiki/SRV_record) are used by various services to specify server locations.</span></span> <span data-ttu-id="034cd-154">Azure DNS에서 SRV 레코드를 지정할 경우</span><span class="sxs-lookup"><span data-stu-id="034cd-154">When specifying an SRV record in Azure DNS:</span></span>

* <span data-ttu-id="034cd-155">*서비스*와 *프로토콜*은 레코드 집합 이름에 포함하여 지정하고 밑줄로 접두사를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-155">The *service* and *protocol* must be specified as part of the record set name, prefixed with underscores.</span></span>  <span data-ttu-id="034cd-156">예를 들어 '\_sip.\_tcp.name'입니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-156">For example, '\_sip.\_tcp.name'.</span></span>  <span data-ttu-id="034cd-157">영역 루트에 있는 레코드의 경우 레코드 이름에 '@'를 지정하지 않아도 되며 서비스와 프로토콜만 사용합니다(예: '\_sip.\_tcp').</span><span class="sxs-lookup"><span data-stu-id="034cd-157">For a record at the zone apex, there is no need to specify '@' in the record name, simply use the service and protocol, for example '\_sip.\_tcp'.</span></span>
* <span data-ttu-id="034cd-158">*우선 순위*, *가중치*, *포트*, *대상*은 레코드 집합에서 각 레코드의 매개 변수로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-158">The *priority*, *weight*, *port*, and *target* are specified as parameters of each record in the record set.</span></span>

### <a name="txt-records"></a><span data-ttu-id="034cd-159">TXT 레코드</span><span class="sxs-lookup"><span data-stu-id="034cd-159">TXT records</span></span>

<span data-ttu-id="034cd-160">TXT 레코드는 도메인 이름을 임의의 텍스트 문자열에 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-160">TXT records are used to map domain names to arbitrary text strings.</span></span> <span data-ttu-id="034cd-161">이들은 특히 [SPF(Sender Policy Framework)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) 및 [DKIM(DomainKeys Identified Mail)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)과 같은 메일 구성과 관련된 여러 응용 프로그램에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-161">They are used in multiple applications, in particular related to email configuration, such as the [Sender Policy Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) and [DomainKeys Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).</span></span>

<span data-ttu-id="034cd-162">DNS 표준은 여러 문자열을 포함하는 하나의 TXT 레코드를 허용하며 각각의 문자열 길이는 최대 254자까지 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-162">The DNS standards permit a single TXT record to contain multiple strings, each of which may be up to 254 characters in length.</span></span> <span data-ttu-id="034cd-163">여러 문자열이 사용되는 경우 이러한 문자열은 클라이언트에 의해 연결되고 단일 문자열로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-163">Where multiple strings are used, they are concatenated by clients and treated as a single string.</span></span>

<span data-ttu-id="034cd-164">Azure DNS REST API를 호출할 때 각 TXT 문자열을 별도로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-164">When calling the Azure DNS REST API, you need to specify each TXT string separately.</span></span>  <span data-ttu-id="034cd-165">Azure Portal, PowerShell 또는 CLI 인터페이스를 사용할 때는 레코드당 하나의 문자열을 지정해야 하며 필요한 경우 자동으로 254자 세그먼트로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-165">When using the Azure portal, PowerShell or CLI interfaces you should specify a single string per record, which is automatically divided into 254-character segments if necessary.</span></span>

<span data-ttu-id="034cd-166">DNS 레코드의 여러 문자열을 TXT 레코드 집합의 여러 TXT 레코드와 혼동해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-166">The multiple strings in a DNS record should not be confused with the multiple TXT records in a TXT record set.</span></span>  <span data-ttu-id="034cd-167">TXT 레코드 집합은 여러 레코드를 포함할 수 있으며 *각각의 레코드*는 여러 문자열을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-167">A TXT record set can contain multiple records, *each of which* can contain multiple strings.</span></span>  <span data-ttu-id="034cd-168">Azure DNS는 모든 레코드가 결합된 각 TXT 레코드 집합에서 총 문자열 길이를 최대 1024자까지 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-168">Azure DNS supports a total string length of up to 1024 characters in each TXT record set (across all records combined).</span></span>

## <a name="tags-and-metadata"></a><span data-ttu-id="034cd-169">태그 및 메타데이터</span><span class="sxs-lookup"><span data-stu-id="034cd-169">Tags and metadata</span></span>

### <a name="tags"></a><span data-ttu-id="034cd-170">태그</span><span class="sxs-lookup"><span data-stu-id="034cd-170">Tags</span></span>

<span data-ttu-id="034cd-171">태그는 이름-값 쌍의 목록으로, Azure Resource Manager에서 리소스에 레이블을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-171">Tags are a list of name-value pairs and are used by Azure Resource Manager to label resources.</span></span>  <span data-ttu-id="034cd-172">Azure Resource Manager는 태그를 사용하여 Azure 청구서를 필터링하여 표시할 수 있으며 태그가 필요한 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-172">Azure Resource Manager uses tags to enable filtered views of your Azure bill, and also enables you to set a policy on which tags are required.</span></span> <span data-ttu-id="034cd-173">태그에 대한 자세한 내용은 [태그를 사용하여 Azure 리소스 구성](../azure-resource-manager/resource-group-using-tags.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="034cd-173">For more information about tags, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

<span data-ttu-id="034cd-174">Azure DNS에서는 DNS 영역 리소스에 Azure Resource Manager 태그를 사용할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="034cd-174">Azure DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span>  <span data-ttu-id="034cd-175">아래 설명된 대로 대체 ‘메타데이터’가 DNS 레코드 집합에서 지원되기는 하지만 DNS 레코드 집합의 태그는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-175">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained below.</span></span>

### <a name="metadata"></a><span data-ttu-id="034cd-176">Metadata</span><span class="sxs-lookup"><span data-stu-id="034cd-176">Metadata</span></span>

<span data-ttu-id="034cd-177">Azure DNS에서는 레코드 집합 태그 대신 '메타데이터'를 사용하여 레코드 집합에 주석을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-177">As an alternative to record set tags, Azure DNS supports annotating record sets using 'metadata'.</span></span>  <span data-ttu-id="034cd-178">태그와 유사한 메타데이터를 사용하면 각 레코드 집합에 이름-값 쌍을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-178">Similar to tags, metadata enables you to associate name-value pairs with each record set.</span></span>  <span data-ttu-id="034cd-179">이는 각 레코드 집합의 목적을 기록하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-179">This can be useful, for example to record the purpose of each record set.</span></span>  <span data-ttu-id="034cd-180">태그와 달리, 메타데이터는 Azure 청구서를 필터링하여 표시하는 데 사용할 수 없으며 Azure Resource Manager 정책에서 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-180">Unlike tags, metadata cannot be used to provide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

## <a name="etags"></a><span data-ttu-id="034cd-181">Etag</span><span class="sxs-lookup"><span data-stu-id="034cd-181">Etags</span></span>

<span data-ttu-id="034cd-182">두 사용자 또는 두 프로세스가 동시에 DNS 레코드 수정을 시도한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-182">Suppose two people or two processes try to modify a DNS record at the same time.</span></span> <span data-ttu-id="034cd-183">어느 쪽이 성공할까요?</span><span class="sxs-lookup"><span data-stu-id="034cd-183">Which one wins?</span></span> <span data-ttu-id="034cd-184">그리고 성공한 사용자 자신이 다른 사용자가 만든 변경 내용을 덮어썼다는 것을 알고 있을까요?</span><span class="sxs-lookup"><span data-stu-id="034cd-184">And does the winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="034cd-185">Azure DNS는 Etag를 사용하여 동일한 리소스에 대한 동시 변경을 안전하게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-185">Azure DNS uses Etags to handle concurrent changes to the same resource safely.</span></span> <span data-ttu-id="034cd-186">Etags는 [Azure Resource Manager '태그'](#tags)와 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-186">Etags are separate from [Azure Resource Manager 'Tags'](#tags).</span></span> <span data-ttu-id="034cd-187">각 DNS 리소스(영역 또는 레코드 집합)에는 Etag가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-187">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="034cd-188">리소스를 검색할 때마다 해당 Etag도 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-188">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="034cd-189">리소스를 업데이트할 때 Azure DNS에서 서버의 Etag가 일치하는지 확인할 수 있도록 Etag를 다시 전달하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-189">When updating a resource, you can choose to pass back the Etag so Azure DNS can verify that the Etag on the server matches.</span></span> <span data-ttu-id="034cd-190">리소스를 업데이트할 때마다 Etag가 다시 생성되므로 Etag 불일치는 동시 변경이 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-190">Since each update to a resource results in the Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="034cd-191">새 리소스를 만들 때도 Etag를 사용하여 리소스가 존재하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-191">Etags can also be used when creating a new resource to ensure that the resource does not already exist.</span></span>

<span data-ttu-id="034cd-192">기본적으로 Azure DNS PowerShell은 Etag를 사용하여 영역 및 레코드 집합에 대한 동시 변경을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-192">By default, Azure DNS PowerShell uses Etags to block concurrent changes to zones and record sets.</span></span> <span data-ttu-id="034cd-193">선택적 *-Overwrite* 스위치를 사용하여 Etag 검사를 무시할 수 있으며, 이 경우 발생한 동시 변경 내용을 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-193">The optional *-Overwrite* switch can be used to suppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="034cd-194">Azure DNS REST API 수준에서 Etag는 HTTP 헤더를 사용하여 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-194">At the level of the Azure DNS REST API, Etags are specified using HTTP headers.</span></span>  <span data-ttu-id="034cd-195">해당 동작은 다음 표에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-195">Their behavior is given in the following table:</span></span>

| <span data-ttu-id="034cd-196">헤더</span><span class="sxs-lookup"><span data-stu-id="034cd-196">Header</span></span> | <span data-ttu-id="034cd-197">동작</span><span class="sxs-lookup"><span data-stu-id="034cd-197">Behavior</span></span> |
| --- | --- |
| <span data-ttu-id="034cd-198">없음</span><span class="sxs-lookup"><span data-stu-id="034cd-198">None</span></span> |<span data-ttu-id="034cd-199">PUT 항상 성공(Etag 검사 안 함)</span><span class="sxs-lookup"><span data-stu-id="034cd-199">PUT always succeeds (no Etag checks)</span></span> |
| <span data-ttu-id="034cd-200">If-match <etag></span><span class="sxs-lookup"><span data-stu-id="034cd-200">If-match <etag></span></span> |<span data-ttu-id="034cd-201">리소스가 있고 Etag가 일치하는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="034cd-201">PUT only succeeds if resource exists and Etag matches</span></span> |
| <span data-ttu-id="034cd-202">If-match *</span><span class="sxs-lookup"><span data-stu-id="034cd-202">If-match *</span></span> |<span data-ttu-id="034cd-203">리소스가 있는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="034cd-203">PUT only succeeds if resource exists</span></span> |
| <span data-ttu-id="034cd-204">If-none-match *</span><span class="sxs-lookup"><span data-stu-id="034cd-204">If-none-match *</span></span> |<span data-ttu-id="034cd-205">리소스가 없는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="034cd-205">PUT only succeeds if resource does not exist</span></span> |


## <a name="limits"></a><span data-ttu-id="034cd-206">제한</span><span class="sxs-lookup"><span data-stu-id="034cd-206">Limits</span></span>

<span data-ttu-id="034cd-207">Azure DNS를 사용할 경우 다음과 같은 기본 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="034cd-207">The following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a><span data-ttu-id="034cd-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="034cd-208">Next steps</span></span>

* <span data-ttu-id="034cd-209">Azure DNS 사용을 시작하려면 [DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="034cd-209">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="034cd-210">기존 DNS 영역을 마이그레이션하려면 [DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md) 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="034cd-210">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>
