---
title: "aaaDNS 영역 및 개요-Azure DNS 기록 | Microsoft Docs"
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
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a><span data-ttu-id="8713e-103">DNS 영역 및 레코드 개요</span><span class="sxs-lookup"><span data-stu-id="8713e-103">Overview of DNS zones and records</span></span>

<span data-ttu-id="8713e-104">이 페이지에서는 도메인, DNS 영역 및 DNS 레코드 및 레코드 집합 및 Azure DNS에서 지원 되는 방식의 hello 주요 개념을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-104">This page explains hello key concepts of domains, DNS zones, and DNS records and record sets, and how they are supported in Azure DNS.</span></span>

## <a name="domain-names"></a><span data-ttu-id="8713e-105">도메인 이름</span><span class="sxs-lookup"><span data-stu-id="8713e-105">Domain names</span></span>

<span data-ttu-id="8713e-106">Domain Name System hello 도메인의 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-106">hello Domain Name System is a hierarchy of domains.</span></span> <span data-ttu-id="8713e-107">hello 계층 구조 이름이 단순히 hello '루트' 도메인에서 시작 '**.**'.</span><span class="sxs-lookup"><span data-stu-id="8713e-107">hello hierarchy starts from hello 'root' domain, whose name is simply '**.**'.</span></span>  <span data-ttu-id="8713e-108">그 아래에 'com', 'net', 'org', 'uk' 또는 'jp'와 같은 최상위 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-108">Below this come top-level domains, such as 'com', 'net', 'org', 'uk' or 'jp'.</span></span>  <span data-ttu-id="8713e-109">그 아래에 'org.uk' 또는 'co.jp'와 같은 두 번째 수준의 도메인이 있는</span><span class="sxs-lookup"><span data-stu-id="8713e-109">Below these are second-level domains, such as 'org.uk' or 'co.jp'.</span></span> <span data-ttu-id="8713e-110">hello 도메인 hello DNS 계층 구조에 전체적으로 배포 됩니다 hello 전 세계 DNS 이름 서버에서 호스트.</span><span class="sxs-lookup"><span data-stu-id="8713e-110">hello domains in hello DNS hierarchy are globally distributed, hosted by DNS name servers around hello world.</span></span>

<span data-ttu-id="8713e-111">도메인 이름 등록 기관 toopurchase 만든 'contoso.com' 등의 도메인 이름을 사용 하면 하는 조직입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-111">A domain name registrar is an organization that allows you toopurchase a domain name, such as 'contoso.com'.</span></span>  <span data-ttu-id="8713e-112">도메인 이름을 제공 오른쪽 toocontrol hello DNS에서 계층 구조에서 해당 이름의 예를 들어 toodirect hello 이름 'www.contoso.com' tooyour 회사 웹 사이트를 허용 hello 구입 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-112">Purchasing a domain name gives you hello right toocontrol hello DNS hierarchy under that name, for example allowing you toodirect hello name 'www.contoso.com' tooyour company web site.</span></span> <span data-ttu-id="8713e-113">hello 등록 기관에서 자동으로 자체 이름 서버 hello 도메인을 호스팅할 수도 toospecify 대체 이름 서버를 사용 하면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-113">hello registrar may host hello domain in its own name servers on your behalf, or allow you toospecify alternative name servers.</span></span>

<span data-ttu-id="8713e-114">Azure DNS 수 있는 전 세계적으로 분산, 고가용성 이름 서버 인프라를 제공 toohost 사용자 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-114">Azure DNS provides a globally distributed, high-availability name server infrastructure, which you can use toohost your domain.</span></span> <span data-ttu-id="8713e-115">Azure dns에서 도메인 호스팅하여 hello로 DNS 레코드를 관리할 수 있습니다 동일한 자격 증명, Api, 도구, 청구 및 기타 Azure 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-115">By hosting your domains in Azure DNS, you can manage your DNS records with hello same credentials, APIs, tools, billing, and support as your other Azure services.</span></span>

<span data-ttu-id="8713e-116">Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-116">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="8713e-117">Toopurchase 도메인 이름, 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-117">If you want toopurchase a domain name, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="8713e-118">hello 등록 기관에는 일반적으로 작은 연간 요금 요금.</span><span class="sxs-lookup"><span data-stu-id="8713e-118">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="8713e-119">hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-119">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="8713e-120">참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-120">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="dns-zones"></a><span data-ttu-id="8713e-121">DNS 영역 </span><span class="sxs-lookup"><span data-stu-id="8713e-121">DNS zones</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a><span data-ttu-id="8713e-122">DNS 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-122">DNS records</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a><span data-ttu-id="8713e-123">Time-to-Live</span><span class="sxs-lookup"><span data-stu-id="8713e-123">Time-to-live</span></span>

<span data-ttu-id="8713e-124">hello 시간 toolive, 또는 TTL, 다시 쿼리 중인 하기 전에 클라이언트에서 각 레코드 캐시 되는 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-124">hello time toolive, or TTL, specifies how long each record is cached by clients before being re-queried.</span></span> <span data-ttu-id="8713e-125">위 예제는 hello, hello TTL은 3600 초 또는 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-125">In hello above example, hello TTL is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="8713e-126">Azure DNS TTL은 각 레코드에 대 한 하지 hello 레코드 집합에 대 한 지정 된 hello에에서 있으므로 해당 레코드 내의 모든 레코드에 대해 동일한 값이 사용 하는 hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-126">In Azure DNS, hello TTL is specified for hello record set, not for each record, so hello same value is used for all records within that record set.</span></span>  <span data-ttu-id="8713e-127">1 ~ 2,147,483,647초 사이의 TTL 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-127">You can specify any TTL value between 1 and 2,147,483,647 seconds.</span></span>

### <a name="wildcard-records"></a><span data-ttu-id="8713e-128">와일드카드 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-128">Wildcard records</span></span>

<span data-ttu-id="8713e-129">Azure DNS는 [와일드카드 레코드](https://en.wikipedia.org/wiki/Wildcard_DNS_record)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-129">Azure DNS supports [wildcard records](https://en.wikipedia.org/wiki/Wildcard_DNS_record).</span></span> <span data-ttu-id="8713e-130">와일드 카드 레코드 (비 와일드 카드 레코드 집합에서 더 알맞은 아니면) 이름이 일치 하는 응답 tooany 쿼리에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-130">Wildcard records are returned in response tooany query with a matching name (unless there is a closer match from a non-wildcard record set).</span></span> <span data-ttu-id="8713e-131">Azure DNS는 NS 및 SOA를 제외한 모든 레코드 종류에 대해 와일드카드 레코드 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-131">Azure DNS supports wildcard record sets for all record types except NS and SOA.</span></span>

<span data-ttu-id="8713e-132">와일드 카드 레코드 toocreate 설정 hello 레코드 집합 이름을 사용 합니다. '\*'.</span><span class="sxs-lookup"><span data-stu-id="8713e-132">toocreate a wildcard record set, use hello record set name '\*'.</span></span> <span data-ttu-id="8713e-133">또는 맨 왼쪽의 레이블로 '\*'가 포함된 이름을 사용할 수 있습니다(예: '\*.foo').</span><span class="sxs-lookup"><span data-stu-id="8713e-133">Alternatively, you can also use a name with '\*' as its left-most label, for example, '\*.foo'.</span></span>

### <a name="cname-records"></a><span data-ttu-id="8713e-134">CNAME 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-134">CNAME records</span></span>

<span data-ttu-id="8713e-135">CNAME 레코드 집합 공존할 수 없으며 hello로 다른 레코드 집합에서 같은 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-135">CNAME record sets cannot coexist with other record sets with hello same name.</span></span> <span data-ttu-id="8713e-136">예를 들어 hello 상대 이름이 'w w w'를 사용 하 여 설정 하는 CNAME 레코드를 만들 수 없습니다 및 동일한 hello 상대 이름이 'w w w'에 hello 사용 하 여 A 기록 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-136">For example, you cannot create a CNAME record set with hello relative name 'www' and an A record with hello relative name 'www' at hello same time.</span></span>

<span data-ttu-id="8713e-137">때문에 hello 영역 루트 (이름 = ' @') hello NS 및 SOA 레코드를 포함 하는 항상 hello 영역을 만들 때 생성 된 집합을 hello 영역 루트에서 설정 하는 CNAME 레코드를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-137">Because hello zone apex (name = '@') always contains hello NS and SOA record sets that were created when hello zone was created, you can't create a CNAME record set at hello zone apex.</span></span>

<span data-ttu-id="8713e-138">이러한 제약 조건은 hello DNS 표준에서 발생 하 고 Azure DNS의 제한 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-138">These constraints arise from hello DNS standards and are not limitations of Azure DNS.</span></span>

### <a name="ns-records"></a><span data-ttu-id="8713e-139">NS 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-139">NS records</span></span>

<span data-ttu-id="8713e-140">hello NS 레코드 hello 영역 루트에서 설정 (name ' @')은 자동으로 각 DNS 영역과 만들어지며 hello 영역 삭제 될 때 자동으로 삭제 됩니다 (삭제할 수 없습니다 별도로).</span><span class="sxs-lookup"><span data-stu-id="8713e-140">hello NS record set at hello zone apex (name '@') is created automatically with each DNS zone, and is deleted automatically when hello zone is deleted (it cannot be deleted separately).</span></span>

<span data-ttu-id="8713e-141">이 레코드 집합에는 hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-141">This record set contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span> <span data-ttu-id="8713e-142">추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-142">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="8713e-143">또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-143">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="8713e-144">그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-144">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span> 

<span data-ttu-id="8713e-145">Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-145">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="8713e-146">(사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합 작성, 수정 및 제약 조건 없이 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-146">Other NS record sets in your zone (as used toodelegate child zones) can be created, modified and deleted without constraint.</span></span>

### <a name="soa-records"></a><span data-ttu-id="8713e-147">SOA 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-147">SOA records</span></span>

<span data-ttu-id="8713e-148">각 영역의 hello 루트에 SOA 레코드 집합을 자동으로 생성 됩니다 (이름 = ' @'), hello 영역 삭제 될 때 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-148">A SOA record set is created automatically at hello apex of each zone (name = '@'), and is deleted automatically when hello zone is deleted.</span></span>  <span data-ttu-id="8713e-149">SOA 레코드는 별도로 생성 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-149">SOA records cannot be created or deleted separately.</span></span>

<span data-ttu-id="8713e-150">Azure DNS에서 제공 하는 미리 구성 된 toorefer toohello 주 이름 서버 이름을 hello 'host' 속성을 제외 하 고 hello SOA 레코드의 모든 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-150">You can modify all properties of hello SOA record except for hello 'host' property, which is pre-configured toorefer toohello primary name server name provided by Azure DNS.</span></span>

### <a name="spf-records"></a><span data-ttu-id="8713e-151">SPF 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-151">SPF records</span></span>

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a><span data-ttu-id="8713e-152">SRV 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-152">SRV records</span></span>

<span data-ttu-id="8713e-153">[SRV 레코드](https://en.wikipedia.org/wiki/SRV_record) 다양 한 서비스 toospecify 서버 위치에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-153">[SRV records](https://en.wikipedia.org/wiki/SRV_record) are used by various services toospecify server locations.</span></span> <span data-ttu-id="8713e-154">Azure DNS에서 SRV 레코드를 지정할 경우</span><span class="sxs-lookup"><span data-stu-id="8713e-154">When specifying an SRV record in Azure DNS:</span></span>

* <span data-ttu-id="8713e-155">hello *서비스* 및 *프로토콜* hello 레코드 집합 이름의 일부로 지정 된, 밑줄 접두사로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-155">hello *service* and *protocol* must be specified as part of hello record set name, prefixed with underscores.</span></span>  <span data-ttu-id="8713e-156">예를 들어 '\_sip.\_tcp.name'입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-156">For example, '\_sip.\_tcp.name'.</span></span>  <span data-ttu-id="8713e-157">Hello 영역 루트에서 레코드에 대 한이 없는 필요 toospecify ' @' hello 레코드 이름 하기만 하면 사용 하 여 hello 서비스 및 프로토콜, 예를 들어 '\_sip.\_ tcp'.</span><span class="sxs-lookup"><span data-stu-id="8713e-157">For a record at hello zone apex, there is no need toospecify '@' in hello record name, simply use hello service and protocol, for example '\_sip.\_tcp'.</span></span>
* <span data-ttu-id="8713e-158">hello *우선 순위*, *가중치*, *포트*, 및 *대상* hello 레코드 집합의 각 레코드의 매개 변수로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-158">hello *priority*, *weight*, *port*, and *target* are specified as parameters of each record in hello record set.</span></span>

### <a name="txt-records"></a><span data-ttu-id="8713e-159">TXT 레코드</span><span class="sxs-lookup"><span data-stu-id="8713e-159">TXT records</span></span>

<span data-ttu-id="8713e-160">TXT 레코드는 사용 되는 toomap 도메인 이름을 tooarbitrary 텍스트 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-160">TXT records are used toomap domain names tooarbitrary text strings.</span></span> <span data-ttu-id="8713e-161">여러 응용 프로그램에서는 hello 등 특히 관련된 tooemail 구성 사용 하는 [보낸 사람 정책 프레임 워크 (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) 및 [DomainKeys 식별 된 메일 (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-161">They are used in multiple applications, in particular related tooemail configuration, such as hello [Sender Policy Framework (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) and [DomainKeys Identified Mail (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail).</span></span>

<span data-ttu-id="8713e-162">hello DNS 표준은 단일 TXT 레코드 toocontain too254 자 하거나 나타낼 수 있으며 각 하는 여러 문자열을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-162">hello DNS standards permit a single TXT record toocontain multiple strings, each of which may be up too254 characters in length.</span></span> <span data-ttu-id="8713e-163">여러 문자열이 사용되는 경우 이러한 문자열은 클라이언트에 의해 연결되고 단일 문자열로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-163">Where multiple strings are used, they are concatenated by clients and treated as a single string.</span></span>

<span data-ttu-id="8713e-164">Hello Azure DNS REST API를 호출할 때 필요한 toospecify 각 TXT 문자열 별도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-164">When calling hello Azure DNS REST API, you need toospecify each TXT string separately.</span></span>  <span data-ttu-id="8713e-165">Hello Azure 포털을 사용할 때 PowerShell 또는 CLI 인터페이스 지정 해야 자동으로 구분 되어 254 자 세그먼트로 필요한 경우 레코드당 단일 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-165">When using hello Azure portal, PowerShell or CLI interfaces you should specify a single string per record, which is automatically divided into 254-character segments if necessary.</span></span>

<span data-ttu-id="8713e-166">TXT 레코드 집합의 여러 TXT 레코드 hello 하는 hello DNS 레코드의 여러 문자열와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-166">hello multiple strings in a DNS record should not be confused with hello multiple TXT records in a TXT record set.</span></span>  <span data-ttu-id="8713e-167">TXT 레코드 집합은 여러 레코드를 포함할 수 있으며 *각각의 레코드*는 여러 문자열을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-167">A TXT record set can contain multiple records, *each of which* can contain multiple strings.</span></span>  <span data-ttu-id="8713e-168">Azure DNS 세트 (모든 레코드를 결합) 각 TXT 레코드의 총 문자열 길이는 too1024 문자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-168">Azure DNS supports a total string length of up too1024 characters in each TXT record set (across all records combined).</span></span>

## <a name="tags-and-metadata"></a><span data-ttu-id="8713e-169">태그 및 메타데이터</span><span class="sxs-lookup"><span data-stu-id="8713e-169">Tags and metadata</span></span>

### <a name="tags"></a><span data-ttu-id="8713e-170">태그들</span><span class="sxs-lookup"><span data-stu-id="8713e-170">Tags</span></span>

<span data-ttu-id="8713e-171">태그 이름-값 쌍의 목록이 되며 Azure 리소스 관리자 toolabel 리소스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-171">Tags are a list of name-value pairs and are used by Azure Resource Manager toolabel resources.</span></span>  <span data-ttu-id="8713e-172">Azure 리소스 관리자, Azure 청구서의 태그 필터링 tooenable 뷰를 사용 하 여을 통해 있습니다 tooset 정책 태그에는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-172">Azure Resource Manager uses tags tooenable filtered views of your Azure bill, and also enables you tooset a policy on which tags are required.</span></span> <span data-ttu-id="8713e-173">태그에 대 한 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-173">For more information about tags, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

<span data-ttu-id="8713e-174">Azure DNS에서는 DNS 영역 리소스에 Azure Resource Manager 태그를 사용할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="8713e-174">Azure DNS supports using Azure Resource Manager tags on DNS zone resources.</span></span>  <span data-ttu-id="8713e-175">아래 설명된 대로 대체 ‘메타데이터’가 DNS 레코드 집합에서 지원되기는 하지만 DNS 레코드 집합의 태그는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-175">It does not support tags on DNS record sets, although as an alternative 'metadata' is supported on DNS record sets as explained below.</span></span>

### <a name="metadata"></a><span data-ttu-id="8713e-176">Metadata</span><span class="sxs-lookup"><span data-stu-id="8713e-176">Metadata</span></span>

<span data-ttu-id="8713e-177">대체 toorecord 태그 설정, Azure DNS 'metadata'를 사용 하 여 레코드 집합을 주석 처리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-177">As an alternative toorecord set tags, Azure DNS supports annotating record sets using 'metadata'.</span></span>  <span data-ttu-id="8713e-178">비슷한 tootags 있습니다 tooassociate 이름-값 쌍으로 각 레코드 집합 메타 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-178">Similar tootags, metadata enables you tooassociate name-value pairs with each record set.</span></span>  <span data-ttu-id="8713e-179">이 유용할 수 있습니다, 그리고 예를 들어 각 레코드의 toorecord hello 목적은 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-179">This can be useful, for example toorecord hello purpose of each record set.</span></span>  <span data-ttu-id="8713e-180">태그와는 달리 메타 데이터 사용된 tooprovide, Azure 청구서의 필터링 된 뷰일 수 없습니다 및 Azure 리소스 관리자 정책에서 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-180">Unlike tags, metadata cannot be used tooprovide a filtered view of your Azure bill and cannot be specified in an Azure Resource Manager policy.</span></span>

## <a name="etags"></a><span data-ttu-id="8713e-181">Etag</span><span class="sxs-lookup"><span data-stu-id="8713e-181">Etags</span></span>

<span data-ttu-id="8713e-182">두 사람이 나 두 프로세스 시도 toomodify 가정 DNS에서 레코드를 hello 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-182">Suppose two people or two processes try toomodify a DNS record at hello same time.</span></span> <span data-ttu-id="8713e-183">어느 쪽이 성공할까요?</span><span class="sxs-lookup"><span data-stu-id="8713e-183">Which one wins?</span></span> <span data-ttu-id="8713e-184">및 hello 승자 알고 있는지 다른 사용자가 만든 변경 내용을 덮어은?</span><span class="sxs-lookup"><span data-stu-id="8713e-184">And does hello winner know that they've overwritten changes created by someone else?</span></span>

<span data-ttu-id="8713e-185">Azure DNS toohandle 동시 변경 toohello Etag를 사용 하 여 동일한 리소스 안전 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-185">Azure DNS uses Etags toohandle concurrent changes toohello same resource safely.</span></span> <span data-ttu-id="8713e-186">Etags는 [Azure Resource Manager '태그'](#tags)와 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-186">Etags are separate from [Azure Resource Manager 'Tags'](#tags).</span></span> <span data-ttu-id="8713e-187">각 DNS 리소스(영역 또는 레코드 집합)에는 Etag가 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-187">Each DNS resource (zone or record set) has an Etag associated with it.</span></span> <span data-ttu-id="8713e-188">리소스를 검색할 때마다 해당 Etag도 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-188">Whenever a resource is retrieved, its Etag is also retrieved.</span></span> <span data-ttu-id="8713e-189">리소스를 업데이트할 때 다시 toopass hello Etag Azure DNS hello 서버 일치 해당 hello Etag를 확인할 수 있도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-189">When updating a resource, you can choose toopass back hello Etag so Azure DNS can verify that hello Etag on hello server matches.</span></span> <span data-ttu-id="8713e-190">각 업데이트 tooa 리소스 Etag 다시 생성 되 고 hello에 결과가 이후 Etag 불일치 동시 변경 발생 했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-190">Since each update tooa resource results in hello Etag being regenerated, an Etag mismatch indicates a concurrent change has occurred.</span></span> <span data-ttu-id="8713e-191">Hello 리소스가 이미 존재 하지 않는 새 리소스 tooensure를 만들 때 Etag은 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-191">Etags can also be used when creating a new resource tooensure that hello resource does not already exist.</span></span>

<span data-ttu-id="8713e-192">기본적으로 Azure DNS PowerShell Etag tooblock 동시 변경 toozones 및 레코드 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-192">By default, Azure DNS PowerShell uses Etags tooblock concurrent changes toozones and record sets.</span></span> <span data-ttu-id="8713e-193">선택적 hello *-덮어쓰기* 스위치 사용된 toosuppress Etag 검사를 수 있으며,이 경우 모든 동시에 발생 한 변경 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-193">hello optional *-Overwrite* switch can be used toosuppress Etag checks, in which case any concurrent changes that have occurred are overwritten.</span></span>

<span data-ttu-id="8713e-194">Hello Azure DNS REST API의 hello 수준 Etag는 HTTP 헤더를 사용 하 여 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-194">At hello level of hello Azure DNS REST API, Etags are specified using HTTP headers.</span></span>  <span data-ttu-id="8713e-195">해당 명령의 동작은 다음 표에 hello에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-195">Their behavior is given in hello following table:</span></span>

| <span data-ttu-id="8713e-196">헤더</span><span class="sxs-lookup"><span data-stu-id="8713e-196">Header</span></span> | <span data-ttu-id="8713e-197">동작</span><span class="sxs-lookup"><span data-stu-id="8713e-197">Behavior</span></span> |
| --- | --- |
| <span data-ttu-id="8713e-198">없음</span><span class="sxs-lookup"><span data-stu-id="8713e-198">None</span></span> |<span data-ttu-id="8713e-199">PUT 항상 성공(Etag 검사 안 함)</span><span class="sxs-lookup"><span data-stu-id="8713e-199">PUT always succeeds (no Etag checks)</span></span> |
| <span data-ttu-id="8713e-200">If-match <etag></span><span class="sxs-lookup"><span data-stu-id="8713e-200">If-match <etag></span></span> |<span data-ttu-id="8713e-201">리소스가 있고 Etag가 일치하는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="8713e-201">PUT only succeeds if resource exists and Etag matches</span></span> |
| <span data-ttu-id="8713e-202">If-match *</span><span class="sxs-lookup"><span data-stu-id="8713e-202">If-match *</span></span> |<span data-ttu-id="8713e-203">리소스가 있는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="8713e-203">PUT only succeeds if resource exists</span></span> |
| <span data-ttu-id="8713e-204">If-none-match *</span><span class="sxs-lookup"><span data-stu-id="8713e-204">If-none-match *</span></span> |<span data-ttu-id="8713e-205">리소스가 없는 경우에만 PUT 성공</span><span class="sxs-lookup"><span data-stu-id="8713e-205">PUT only succeeds if resource does not exist</span></span> |


## <a name="limits"></a><span data-ttu-id="8713e-206">제한</span><span class="sxs-lookup"><span data-stu-id="8713e-206">Limits</span></span>

<span data-ttu-id="8713e-207">기본 제한 값을 다음 hello Azure DNS를 사용 하는 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-207">hello following default limits apply when using Azure DNS:</span></span>

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a><span data-ttu-id="8713e-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8713e-208">Next steps</span></span>

* <span data-ttu-id="8713e-209">Azure DNS를 사용 하 여 toostart 너무 방법을 알아봅니다[DNS 영역을 만드는](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-209">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="8713e-210">toomigrate 기존 DNS 영역을 알아보려면 어떻게 너무[DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8713e-210">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>
