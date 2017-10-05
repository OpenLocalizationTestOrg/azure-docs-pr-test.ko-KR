---
title: "Azure의 역방향 DNS 개요 | Microsoft Docs"
description: "역방향 DNS 작동 방법 및 Azure에서 사용하는 방법을 알아봅니다."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 70a1ad070e812951fca3d2b19da12c67f0725dd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a><span data-ttu-id="dd019-103">Azure의 역방향 DNS 및 지원 개요</span><span class="sxs-lookup"><span data-stu-id="dd019-103">Overview of reverse DNS and support in Azure</span></span>

<span data-ttu-id="dd019-104">이 문서에서는 역방향 DNS가 작동하는 방식과 Azure에서 지원되는 역방향 DNS 시나리오에 대해 대략적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-104">This article gives an overview of how reverse DNS works, and the reverse DNS scenarios supported in Azure.</span></span>

## <a name="what-is-reverse-dns"></a><span data-ttu-id="dd019-105">역방향 DNS란?</span><span class="sxs-lookup"><span data-stu-id="dd019-105">What is reverse DNS?</span></span>

<span data-ttu-id="dd019-106">기본 DNS 레코드를 통해 DNS 이름(예: 'www.contoso.com')을 IP 주소(예: 64.4.6.100)에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-106">Conventional DNS records enable a mapping from a DNS name (such as 'www.contoso.com') to an IP address (such as 64.4.6.100).</span></span>  <span data-ttu-id="dd019-107">역방향 DNS로는 IP 주소(64.4.6.100)를 다시 이름('www.contoso.com')으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-107">Reverse DNS enables the translation of an IP address (64.4.6.100) back to a name ('www.contoso.com').</span></span>

<span data-ttu-id="dd019-108">역방향 DNS 레코드는 다양한 상황에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-108">Reverse DNS records are used in a variety of situations.</span></span> <span data-ttu-id="dd019-109">예를 들어 역방향 DNS 레코드는 보낸 사람의 메일 메시지를 확인하여 스팸 메일을 방지하는 데 널리 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-109">For example, reverse DNS records are widely used in combating e-mail spam by verifying the sender of an e-mail message.</span></span>  <span data-ttu-id="dd019-110">수신 메일 서버는 보내는 서버의 IP 주소의 역방향 DNS 레코드를 검색하고, 해당 호스트가 원래의 도메인에서 메일을 보내도록 허가를 받았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-110">The receiving mail server retrieves the reverse DNS record of the sending server's IP address, and verifies if that host is authorized to send e-mail from the originating domain.</span></span> 

## <a name="how-reverse-dns-works"></a><span data-ttu-id="dd019-111">역방향 DNS 작동 방식</span><span class="sxs-lookup"><span data-stu-id="dd019-111">How reverse DNS works</span></span>

<span data-ttu-id="dd019-112">역방향 DNS 레코드는 'ARPA' 영역이라는 특수한 DNS 영역에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-112">Reverse DNS records are hosted in special DNS zones, known as 'ARPA' zones.</span></span>  <span data-ttu-id="dd019-113">이러한 영역은 'contoso.com'과 같은 일반적인 계층 구조 호스팅 도메인과 병렬로 별도의 DNS 계층 구조를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-113">These zones form a separate DNS hierarchy in parallel with the normal hierarchy hosting domains such as 'contoso.com'.</span></span>

<span data-ttu-id="dd019-114">예를 들어 DNS 레코드 'www.contoso.com'은 영역 'contoso.com'에 이름 'www'를 포함하는 DNS 'A' 레코드를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-114">For example, the DNS record 'www.contoso.com' is implemented using a DNS 'A' record with the name 'www' in the zone 'contoso.com'.</span></span>  <span data-ttu-id="dd019-115">이 A 레코드는 해당 IP 주소(이 경우 64.4.6.100)를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-115">This A record points to the corresponding IP address, in this case 64.4.6.100.</span></span>  <span data-ttu-id="dd019-116">역방향 조회는 영역 '6.4.64.in-addr.arpa'에서 '100'으로 명명된 'PTR' 레코드를 사용하여 별도로 구현됩니다(해당 IP 주소는 ARPA 영역에서 반전됨).  이 PTR 레코드가 올바르게 구성된 경우 이름 'www.contoso.com'을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-116">The reverse lookup is implemented separately, using a 'PTR' record named '100' in the zone '6.4.64.in-addr.arpa' (note that IP addresses are reversed in ARPA zones.)  This PTR record, if it has been configured correctly, points to the name 'www.contoso.com'.</span></span>

<span data-ttu-id="dd019-117">조직에 IP 주소 블록이 할당되면 해당 ARPA 영역을 관리할 권한도 획득하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-117">When an organization is assigned an IP address block, they also acquire the right to manage the corresponding ARPA zone.</span></span> <span data-ttu-id="dd019-118">Azure에 사용되는 IP 주소 블록에 해당되는 ARPA 영역은 Microsoft에서 호스트 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-118">The ARPA zones corresponding to the IP address blocks used by Azure are hosted and managed by Microsoft.</span></span> <span data-ttu-id="dd019-119">ISP는 사용자 고유의 IP 주소에 대한 ARPA 영역을 호스트하거나 사용자가 Azure DNS와 같은 선택한 DNS 서비스에서 ARPA 영역을 호스트하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-119">Your ISP may host the ARPA zone for your own IP addresses for you, or may allow to you host the ARPA zone in a DNS service of your choice, such as Azure DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="dd019-120">정방향 및 역방향 DNS 조회를 DNS 계층과 함께 별도로 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-120">Forward DNS lookups and reverse DNS lookups are implemented in separate, parallel DNS hierarchies.</span></span> <span data-ttu-id="dd019-121">'www.contoso.com'에 대한 역방향 조회는 영역 'contoso.com'에서 호스트되지 **않으며** 대신 해당 IP 주소 블록에 대한 ARPA 영역에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-121">The reverse lookup for 'www.contoso.com' is **not** hosted in the zone 'contoso.com', rather it is hosted in the ARPA zone for the corresponding IP address block.</span></span> <span data-ttu-id="dd019-122">IPv4 및 IPv6 주소 블록에 별도 영역이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-122">Separate zones are used for IPv4 and IPv6 address blocks.</span></span>

### <a name="ipv4"></a><span data-ttu-id="dd019-123">IPv4</span><span class="sxs-lookup"><span data-stu-id="dd019-123">IPv4</span></span>

<span data-ttu-id="dd019-124">IPv4 역방향 조회 영역의 이름은 `<IPv4 network prefix in reverse order>.in-addr.arpa` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-124">The name of an IPv4 reverse lookup zone should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span>

<span data-ttu-id="dd019-125">예를 들어 192.0.2.0/24 접두사에 있는 IP를 갖는 호스트의 레코드를 호스트하기 위해 역방향 영역을 만들 경우 주소의 네트워크 접두사를 분리한 다음(192.0.2) 순서를 뒤집고(2.0.192) 접미사 `.in-addr.arpa`를 추가하여 영역 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-125">For example, when creating a reverse zone to host records for hosts with IPs that are in the 192.0.2.0/24 prefix, the zone name would be created by isolating the network prefix of the address (192.0.2) and then reversing the order (2.0.192) and adding the suffix `.in-addr.arpa`.</span></span>

|<span data-ttu-id="dd019-126">서브넷 클래스</span><span class="sxs-lookup"><span data-stu-id="dd019-126">Subnet class</span></span>|<span data-ttu-id="dd019-127">네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="dd019-127">Network prefix</span></span>  |<span data-ttu-id="dd019-128">역방향 네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="dd019-128">Reversed network prefix</span></span>  |<span data-ttu-id="dd019-129">표준 접미사</span><span class="sxs-lookup"><span data-stu-id="dd019-129">Standard suffix</span></span>  |<span data-ttu-id="dd019-130">역방향 영역 이름</span><span class="sxs-lookup"><span data-stu-id="dd019-130">Reverse zone name</span></span> |
|-------|----------------|------------|-----------------|---------------------------|
|<span data-ttu-id="dd019-131">클래스 A</span><span class="sxs-lookup"><span data-stu-id="dd019-131">Class A</span></span>|<span data-ttu-id="dd019-132">203.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="dd019-132">203.0.0.0/8</span></span>     | <span data-ttu-id="dd019-133">203</span><span class="sxs-lookup"><span data-stu-id="dd019-133">203</span></span>        | <span data-ttu-id="dd019-134">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="dd019-134">.in-addr.arpa</span></span>   | `203.in-addr.arpa`        |
|<span data-ttu-id="dd019-135">클래스 B</span><span class="sxs-lookup"><span data-stu-id="dd019-135">Class B</span></span>|<span data-ttu-id="dd019-136">198.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="dd019-136">198.51.0.0/16</span></span>   | <span data-ttu-id="dd019-137">51.198</span><span class="sxs-lookup"><span data-stu-id="dd019-137">51.198</span></span>     | <span data-ttu-id="dd019-138">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="dd019-138">.in-addr.arpa</span></span>   | `51.198.in-addr.arpa`     |
|<span data-ttu-id="dd019-139">클래스 C</span><span class="sxs-lookup"><span data-stu-id="dd019-139">Class C</span></span>|<span data-ttu-id="dd019-140">192.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="dd019-140">192.0.2.0/24</span></span>    | <span data-ttu-id="dd019-141">2.0.192</span><span class="sxs-lookup"><span data-stu-id="dd019-141">2.0.192</span></span>    | <span data-ttu-id="dd019-142">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="dd019-142">.in-addr.arpa</span></span>   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a><span data-ttu-id="dd019-143">클래스 없는 IPv4 위임</span><span class="sxs-lookup"><span data-stu-id="dd019-143">Classless IPv4 delegation</span></span>

<span data-ttu-id="dd019-144">일부 경우에 조직에 할당된 IP 범위가 클래스 C(/24) 범위보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-144">In some cases, the IP range allocated to an organization is smaller than a Class C (/24) range.</span></span> <span data-ttu-id="dd019-145">이 경우 IP 범위는 `.in-addr.arpa` 영역 계층 구조 내의 영역 경계에 속하지 않으므로 하위 영역으로 위임할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-145">In this case, the IP range does not fall on a zone boundary within the `.in-addr.arpa` zone hierarchy, and hence cannot be delegated as a child zone.</span></span>

<span data-ttu-id="dd019-146">대신 다른 메커니즘을 통해 개별 역방향 조회(PTR) 레코드에 대한 제어 권한을 전용 DNS 영역으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-146">Instead, a different mechanism is used to transfer control of individual reverse lookup (PTR) records to a dedicated DNS zone.</span></span> <span data-ttu-id="dd019-147">이 메커니즘은 각 IP 범위에 대한 자식 영역을 위임한 다음 CNAME 레코드를 사용하여 범위의 각 IP 주소를 해당 자식 영역에 개별적으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-147">This mechanism delegates a child zone for each IP range, then maps each IP address in the range individually to that child zone using CNAME records.</span></span>

<span data-ttu-id="dd019-148">예를 들어 조직에는 ISP에 의해 IP 범위 192.0.2.128/26이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-148">For example, suppose an organization is granted the IP range 192.0.2.128/26 by its ISP.</span></span> <span data-ttu-id="dd019-149">이것은 192.0.2.128에서 192.0.2.191까지의 64개 IP 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-149">This represents 64 IP addresses, from 192.0.2.128 to 192.0.2.191.</span></span> <span data-ttu-id="dd019-150">이 범위에 대한 역방향 DNS는 다음과 같이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-150">Reverse DNS for this range is implemented as follows:</span></span>
- <span data-ttu-id="dd019-151">조직에서는 128-26.2.0.192.in-addr.arpa라는 역방향 조회 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-151">The organization creates a reverse lookup zone called 128-26.2.0.192.in-addr.arpa.</span></span> <span data-ttu-id="dd019-152">접두사 '128-26'은 클래스 C(/24) 범위 내 조직에 할당된 네트워크 세그먼트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-152">The prefix '128-26' represents the network segment assigned to the organization within the Class C (/24) range.</span></span>
- <span data-ttu-id="dd019-153">ISP는 클래스 C 부모 영역에서 위 영역에 대한 DNS 위임을 설정하기 위한 NS 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-153">The ISP creates NS records to set up the DNS delegation for the above zone from the Class C parent zone.</span></span> <span data-ttu-id="dd019-154">또한 부모(클래스 C) 역방향 조회 영역에 CNAME 레코드를 생성하고 IP 범위의 각 IP 주소를 조직에서 만드는 새 영역에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-154">It also creates CNAME records in the parent (Class C) reverse lookup zone, mapping each IP address in the IP range to the new zone created by the organization:</span></span>

```
$ORIGIN 2.0.192.in-addr.arpa
; Delegate child zone
128-26    NS       <name server 1 for 128-26.2.0.192.in-addr.arpa>
128-26    NS       <name server 2 for 128-26.2.0.192.in-addr.arpa>
; CNAME records for each IP address
129       CNAME    129.128-26.2.0.192.in-addr.arpa
130       CNAME    130.128-26.2.0.192.in-addr.arpa
131       CNAME    131.128-26.2.0.192.in-addr.arpa
; etc
```
- <span data-ttu-id="dd019-155">그런 다음 해당 자식 영역 내에서 개별 PTR 레코드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-155">The organization then manages the individual PTR records within their child zone.</span></span>

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
<span data-ttu-id="dd019-156">IP 주소 '192.0.2.129'에 대한 역방향 조회는 이름이 '129.2.0.192.in-addr.arpa'인 PTR 레코드를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-156">A reverse lookup for the IP address '192.0.2.129' queries for a PTR record named '129.2.0.192.in-addr.arpa'.</span></span> <span data-ttu-id="dd019-157">이 쿼리는 부모 영역의 CNAME을 통해 자식 영역에 있는 PTR 레코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-157">This query resolves via the CNAME in the parent zone to the PTR record in the child zone.</span></span>

### <a name="ipv6"></a><span data-ttu-id="dd019-158">IPv6</span><span class="sxs-lookup"><span data-stu-id="dd019-158">IPv6</span></span>

<span data-ttu-id="dd019-159">IPv6 역방향 조회 영역의 이름은 `<IPv6 network prefix in reverse order>.ip6.arpa` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-159">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`</span></span>

<span data-ttu-id="dd019-160">예제:</span><span class="sxs-lookup"><span data-stu-id="dd019-160">For example,.</span></span> <span data-ttu-id="dd019-161">2001:db8:1000:abdc::/64 접두사에 있는 IP를 갖는 호스트의 레코드를 호스트하기 위해 역방향 영역을 만들 경우 주소의 네트워크 접두사를 분리하여 영역 이름을 만듭니다(2001:db8:abdc::).</span><span class="sxs-lookup"><span data-stu-id="dd019-161">When creating a reverse zone to host records for hosts with IPs that are in the 2001:db8:1000:abdc::/64 prefix, the zone name would be created by isolating the network prefix of the address (2001:db8:abdc::).</span></span> <span data-ttu-id="dd019-162">그런 다음 [제로 압축](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)이 IPv6 주소 접두사를 줄이기 위해 사용된 경우 이 압축을 제거하여 IPv6 네트워크 접두사를 확장합니다(2001:0db8:abdc:0000::).</span><span class="sxs-lookup"><span data-stu-id="dd019-162">Next expand the IPv6 network prefix to remove [zero compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), if it was used to shorten the IPv6 address prefix (2001:0db8:abdc:0000::).</span></span> <span data-ttu-id="dd019-163">접두사의 각 16진수 숫자 간을 마침표로 구분하고 순서를 뒤집어 역순서의 네트워크 접두사(`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`)를 작성하고 접미사 `.ip6.arpa`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-163">Reverse the order, using a period as the delimiter between each hexadecimal number in the prefix, to build the reversed network prefix (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) and add the suffix `.ip6.arpa`.</span></span>


|<span data-ttu-id="dd019-164">네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="dd019-164">Network prefix</span></span>  |<span data-ttu-id="dd019-165">확장된 역방향 네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="dd019-165">Expanded and reversed network prefix</span></span> |<span data-ttu-id="dd019-166">표준 접미사</span><span class="sxs-lookup"><span data-stu-id="dd019-166">Standard suffix</span></span> |<span data-ttu-id="dd019-167">역방향 영역 이름</span><span class="sxs-lookup"><span data-stu-id="dd019-167">Reverse zone name</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="dd019-168">2001:db8:abdc::/64</span><span class="sxs-lookup"><span data-stu-id="dd019-168">2001:db8:abdc::/64</span></span>    | <span data-ttu-id="dd019-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="dd019-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="dd019-170">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="dd019-170">.ip6.arpa</span></span>        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|<span data-ttu-id="dd019-171">2001:db8:1000:9102::/64</span><span class="sxs-lookup"><span data-stu-id="dd019-171">2001:db8:1000:9102::/64</span></span>    | <span data-ttu-id="dd019-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="dd019-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="dd019-173">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="dd019-173">.ip6.arpa</span></span>        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a><span data-ttu-id="dd019-174">역방향 DNS에 대한 Azure 지원</span><span class="sxs-lookup"><span data-stu-id="dd019-174">Azure support for reverse DNS</span></span>

<span data-ttu-id="dd019-175">Azure에서는 역방향 DNS와 관련하여 두 가지 별도의 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-175">Azure supports two separate scenarios relating to reverse DNS:</span></span>

<span data-ttu-id="dd019-176">**IP 주소 블록에 해당하는 역방향 조회 영역 호스팅**</span><span class="sxs-lookup"><span data-stu-id="dd019-176">**Hosting the reverse lookup zone corresponding to your IP address block.**</span></span>
<span data-ttu-id="dd019-177">Azure DNS를 사용하여 IPv4 및 IPv6 둘 다에 대해 [역방향 조회 영역을 호스트하고 각 역방향 DNS 조회를 위해 PTR 레코드를 관리](dns-reverse-dns-hosting.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-177">Azure DNS can be used to [host your reverse lookup zones and manage the PTR records for each reverse DNS lookup](dns-reverse-dns-hosting.md), for both IPv4 and IPv6.</span></span>  <span data-ttu-id="dd019-178">역방향 조회(ARPA) 영역을 만들고 위임을 설정하며 PTR 레코드를 구성하는 과정은 일반 DNS 영역과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-178">The process of creating the reverse lookup (ARPA) zone, setting up the delegation, and configuring PTR records is the same as for regular DNS zones.</span></span>  <span data-ttu-id="dd019-179">유일한 차이점은 DNS 등록 기관보다는 ISP를 통해 위임을 구성해야 하며 PTR 레코드 유형만 사용해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-179">The only differences are that the delegation must be configured via your ISP rather than your DNS registrar, and only the PTR record type should be used.</span></span>

<span data-ttu-id="dd019-180">**Azure 서비스에 할당된 IP 주소에 대한 역방향 DNS를 구성합니다.**</span><span class="sxs-lookup"><span data-stu-id="dd019-180">**Configure the reverse DNS record for the IP address assigned to your Azure service.**</span></span> <span data-ttu-id="dd019-181">Azure에서는 [Azure 서비스에 할당된 IP 주소에 대한 역방향 조회를 구성](dns-reverse-dns-for-azure-services.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-181">Azure enables you to [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>  <span data-ttu-id="dd019-182">이 역방향 조회는 Azure에 의해 해당 ARPA 영역에서 PTR 레코드로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-182">This reverse lookup is configured by Azure as a PTR record in the corresponding ARPA zone.</span></span>  <span data-ttu-id="dd019-183">Azure에 사용되는 모든 IP 범위에 해당되는 이러한 ARPA 영역은 Microsoft에서 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-183">These ARPA zones, corresponding to all the IP ranges used by Azure, are hosted by Microsoft</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd019-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd019-184">Next steps</span></span>

<span data-ttu-id="dd019-185">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd019-185">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="dd019-186">[Azure DNS에서 ISP 할당 IP 범위에 대한 역방향 조회 영역 호스트](dns-reverse-dns-for-azure-services.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-186">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>
<br>
<span data-ttu-id="dd019-187">[Azure 서비스에 대한 역방향 DNS 레코드를 관리](dns-reverse-dns-for-azure-services.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="dd019-187">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

