---
title: "Azure에서 DNS 역방향의 aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: 687663fb83469ab8e696bb714649d0856915bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reverse-dns-and-support-in-azure"></a><span data-ttu-id="744d4-103">Azure의 역방향 DNS 및 지원 개요</span><span class="sxs-lookup"><span data-stu-id="744d4-103">Overview of reverse DNS and support in Azure</span></span>

<span data-ttu-id="744d4-104">이 문서에서는 Azure에서 지원 되는 역방향 DNS 시나리오 어떻게 역방향 DNS 작동 하며 hello에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-104">This article gives an overview of how reverse DNS works, and hello reverse DNS scenarios supported in Azure.</span></span>

## <a name="what-is-reverse-dns"></a><span data-ttu-id="744d4-105">역방향 DNS란?</span><span class="sxs-lookup"><span data-stu-id="744d4-105">What is reverse DNS?</span></span>

<span data-ttu-id="744d4-106">규칙에 따른 DNS 레코드는 DNS 이름 (예: 'www.contoso.com') tooan IP 주소 (예: 64.4.6.100)에서 매핑을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-106">Conventional DNS records enable a mapping from a DNS name (such as 'www.contoso.com') tooan IP address (such as 64.4.6.100).</span></span>  <span data-ttu-id="744d4-107">역방향 DNS에 IP 주소 (64.4.6.100) 백 tooa 이름 ('www.contoso.com')의 hello 번역을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-107">Reverse DNS enables hello translation of an IP address (64.4.6.100) back tooa name ('www.contoso.com').</span></span>

<span data-ttu-id="744d4-108">역방향 DNS 레코드는 다양한 상황에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-108">Reverse DNS records are used in a variety of situations.</span></span> <span data-ttu-id="744d4-109">예를 들어 역방향 DNS 레코드는 전자 메일 스팸 전자 메일 메시지의 보낸 사람 hello를 확인 하기 위해 널리 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-109">For example, reverse DNS records are widely used in combating e-mail spam by verifying hello sender of an e-mail message.</span></span>  <span data-ttu-id="744d4-110">hello 받는 메일 서버 검색의 서버 IP 주소를 보내는 hello 역방향 DNS 레코드를 hello 하 고 호스팅하는 경우는 권한 있는 toosend 전자 메일 hello에서 시작 된 도메인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-110">hello receiving mail server retrieves hello reverse DNS record of hello sending server's IP address, and verifies if that host is authorized toosend e-mail from hello originating domain.</span></span> 

## <a name="how-reverse-dns-works"></a><span data-ttu-id="744d4-111">역방향 DNS 작동 방식</span><span class="sxs-lookup"><span data-stu-id="744d4-111">How reverse DNS works</span></span>

<span data-ttu-id="744d4-112">역방향 DNS 레코드는 'ARPA' 영역이라는 특수한 DNS 영역에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-112">Reverse DNS records are hosted in special DNS zones, known as 'ARPA' zones.</span></span>  <span data-ttu-id="744d4-113">이러한 영역 만든 'contoso.com'와 같은 도메인 호스팅 hello 기본 계층 구조와 동시에 별도 DNS 계층 구조를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-113">These zones form a separate DNS hierarchy in parallel with hello normal hierarchy hosting domains such as 'contoso.com'.</span></span>

<span data-ttu-id="744d4-114">예를 들어 hello DNS 레코드 'www.contoso.com' hello 이름의 hello 영역 '만든 contoso.com'에서 ' w w w'는 'A' DNS 레코드를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-114">For example, hello DNS record 'www.contoso.com' is implemented using a DNS 'A' record with hello name 'www' in hello zone 'contoso.com'.</span></span>  <span data-ttu-id="744d4-115">이 A 레코드는이 경우 64.4.6.100 toohello 해당 IP 주소를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-115">This A record points toohello corresponding IP address, in this case 64.4.6.100.</span></span>  <span data-ttu-id="744d4-116">hello 역방향 조회는 구현 별도로 '100' hello '6.4.64.in-addr.arpa' 영역에 (참고 IP 주소에 ARPA 영역이 반대가 됩니다.) 라는 'PTR' 레코드를 사용 하 여  이 PTR 레코드를 올바르게 구성 되어 toohello 이름 'www.contoso.com' 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-116">hello reverse lookup is implemented separately, using a 'PTR' record named '100' in hello zone '6.4.64.in-addr.arpa' (note that IP addresses are reversed in ARPA zones.)  This PTR record, if it has been configured correctly, points toohello name 'www.contoso.com'.</span></span>

<span data-ttu-id="744d4-117">조직은 IP 주소 블록에 할당 된 hello 오른쪽 toomanage hello 해당 ARPA 영역도 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-117">When an organization is assigned an IP address block, they also acquire hello right toomanage hello corresponding ARPA zone.</span></span> <span data-ttu-id="744d4-118">hello ARPA 영역이 블록 Azure에서 사용 하는 호스트 및 Microsoft에서 관리 되는 toohello IP 주소에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-118">hello ARPA zones corresponding toohello IP address blocks used by Azure are hosted and managed by Microsoft.</span></span> <span data-ttu-id="744d4-119">ISP를 고유한 IP 주소에 대 한 hello ARPA 영역을 호스팅할 수 있고 또는 풀기 Azure DNS의 DNS 서비스의 hello ARPA 영역이 tooyou 호스트를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-119">Your ISP may host hello ARPA zone for your own IP addresses for you, or may allow tooyou host hello ARPA zone in a DNS service of your choice, such as Azure DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="744d4-120">정방향 및 역방향 DNS 조회를 DNS 계층과 함께 별도로 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-120">Forward DNS lookups and reverse DNS lookups are implemented in separate, parallel DNS hierarchies.</span></span> <span data-ttu-id="744d4-121">hello 'www.contoso.com'에 대 한 역방향 조회는 **하지** 을 만든 ' contoso.com' hello 영역에서 호스트 대신 호스팅되는지 hello 해당 IP 주소 블록에 대 한 hello ARPA 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-121">hello reverse lookup for 'www.contoso.com' is **not** hosted in hello zone 'contoso.com', rather it is hosted in hello ARPA zone for hello corresponding IP address block.</span></span> <span data-ttu-id="744d4-122">IPv4 및 IPv6 주소 블록에 별도 영역이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-122">Separate zones are used for IPv4 and IPv6 address blocks.</span></span>

### <a name="ipv4"></a><span data-ttu-id="744d4-123">IPv4</span><span class="sxs-lookup"><span data-stu-id="744d4-123">IPv4</span></span>

<span data-ttu-id="744d4-124">형식에 따라 hello에 IPv4 역방향 조회 영역의 hello 이름 있어야: `<IPv4 network prefix in reverse order>.in-addr.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-124">hello name of an IPv4 reverse lookup zone should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span>

<span data-ttu-id="744d4-125">예를 들어를 만들 때 역방향 영역 toohost 레코드 hello 192.0.2.0/24 접두사에 있는 Ip와 호스트에 대 한 hello 영역 이름이 만들어집니다 (192.0.2) hello 주소 (2.0.192) hello 순서를 반대로 고 hello 추가의 hello 네트워크 접두사를 격리 하 여 접미사 `.in-addr.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-125">For example, when creating a reverse zone toohost records for hosts with IPs that are in hello 192.0.2.0/24 prefix, hello zone name would be created by isolating hello network prefix of hello address (192.0.2) and then reversing hello order (2.0.192) and adding hello suffix `.in-addr.arpa`.</span></span>

|<span data-ttu-id="744d4-126">서브넷 클래스</span><span class="sxs-lookup"><span data-stu-id="744d4-126">Subnet class</span></span>|<span data-ttu-id="744d4-127">네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="744d4-127">Network prefix</span></span>  |<span data-ttu-id="744d4-128">역방향 네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="744d4-128">Reversed network prefix</span></span>  |<span data-ttu-id="744d4-129">표준 접미사</span><span class="sxs-lookup"><span data-stu-id="744d4-129">Standard suffix</span></span>  |<span data-ttu-id="744d4-130">역방향 영역 이름</span><span class="sxs-lookup"><span data-stu-id="744d4-130">Reverse zone name</span></span> |
|-------|----------------|------------|-----------------|---------------------------|
|<span data-ttu-id="744d4-131">클래스 A</span><span class="sxs-lookup"><span data-stu-id="744d4-131">Class A</span></span>|<span data-ttu-id="744d4-132">203.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="744d4-132">203.0.0.0/8</span></span>     | <span data-ttu-id="744d4-133">203</span><span class="sxs-lookup"><span data-stu-id="744d4-133">203</span></span>        | <span data-ttu-id="744d4-134">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="744d4-134">.in-addr.arpa</span></span>   | `203.in-addr.arpa`        |
|<span data-ttu-id="744d4-135">클래스 B</span><span class="sxs-lookup"><span data-stu-id="744d4-135">Class B</span></span>|<span data-ttu-id="744d4-136">198.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="744d4-136">198.51.0.0/16</span></span>   | <span data-ttu-id="744d4-137">51.198</span><span class="sxs-lookup"><span data-stu-id="744d4-137">51.198</span></span>     | <span data-ttu-id="744d4-138">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="744d4-138">.in-addr.arpa</span></span>   | `51.198.in-addr.arpa`     |
|<span data-ttu-id="744d4-139">클래스 C</span><span class="sxs-lookup"><span data-stu-id="744d4-139">Class C</span></span>|<span data-ttu-id="744d4-140">192.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="744d4-140">192.0.2.0/24</span></span>    | <span data-ttu-id="744d4-141">2.0.192</span><span class="sxs-lookup"><span data-stu-id="744d4-141">2.0.192</span></span>    | <span data-ttu-id="744d4-142">.in-addr.arpa</span><span class="sxs-lookup"><span data-stu-id="744d4-142">.in-addr.arpa</span></span>   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a><span data-ttu-id="744d4-143">클래스 없는 IPv4 위임</span><span class="sxs-lookup"><span data-stu-id="744d4-143">Classless IPv4 delegation</span></span>

<span data-ttu-id="744d4-144">경우에 따라 tooan 조직 할당 된 hello IP 범위 보다 작으면 클래스 C (/ 24) 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-144">In some cases, hello IP range allocated tooan organization is smaller than a Class C (/24) range.</span></span> <span data-ttu-id="744d4-145">이 경우 hello IP 범위 떨어지지 hello 내 영역 경계에 `.in-addr.arpa` 계층 영역을 마우스 따라서 하위 영역으로 위임할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-145">In this case, hello IP range does not fall on a zone boundary within hello `.in-addr.arpa` zone hierarchy, and hence cannot be delegated as a child zone.</span></span>

<span data-ttu-id="744d4-146">다른 메커니즘을 사용 하는 대신 개별 역방향 조회 (PTR)의 tootransfer 제어 전용 tooa DNS 영역을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-146">Instead, a different mechanism is used tootransfer control of individual reverse lookup (PTR) records tooa dedicated DNS zone.</span></span> <span data-ttu-id="744d4-147">이 메커니즘을 각 IP 범위에 대 한 자식 영역 위임 후 지도 hello에 각 IP 주소 범위는 개별적으로 CNAME 레코드를 사용 하 여 toothat 자식 영역.</span><span class="sxs-lookup"><span data-stu-id="744d4-147">This mechanism delegates a child zone for each IP range, then maps each IP address in hello range individually toothat child zone using CNAME records.</span></span>

<span data-ttu-id="744d4-148">예를 들어 조직 hello IP 범위 192.0.2.128/26 ISP 하 여 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-148">For example, suppose an organization is granted hello IP range 192.0.2.128/26 by its ISP.</span></span> <span data-ttu-id="744d4-149">이 IP 주소가 64 192.0.2.128에서 나타냅니다 too192.0.2.191 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-149">This represents 64 IP addresses, from 192.0.2.128 too192.0.2.191.</span></span> <span data-ttu-id="744d4-150">이 범위에 대한 역방향 DNS는 다음과 같이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-150">Reverse DNS for this range is implemented as follows:</span></span>
- <span data-ttu-id="744d4-151">hello 조직 addr.arpa-26.2.0.192.in-128을 호출 하는 역방향 조회 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-151">hello organization creates a reverse lookup zone called 128-26.2.0.192.in-addr.arpa.</span></span> <span data-ttu-id="744d4-152">hello 접두사 ' 128-26' 나타냅니다 hello 네트워크 세그먼트 할당 toohello 조직 내에서 클래스 C hello (/ 24) 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-152">hello prefix '128-26' represents hello network segment assigned toohello organization within hello Class C (/24) range.</span></span>
- <span data-ttu-id="744d4-153">hello ISP hello 클래스 C 부모 영역에서 NS 레코드 tooset을 영역 위에 hello에 대 한 DNS 위임 hello 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-153">hello ISP creates NS records tooset up hello DNS delegation for hello above zone from hello Class C parent zone.</span></span> <span data-ttu-id="744d4-154">또한 만듭니다 CNAME 레코드 hello 부모 (클래스 C) 역방향 조회 영역에서 각 IP 주소 hello IP 범위 toohello 새 영역 hello 조직에서 만드는에 매핑:</span><span class="sxs-lookup"><span data-stu-id="744d4-154">It also creates CNAME records in hello parent (Class C) reverse lookup zone, mapping each IP address in hello IP range toohello new zone created by hello organization:</span></span>

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
- <span data-ttu-id="744d4-155">hello 조직 다음 자식 영역 내에서 hello 개별 PTR 레코드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-155">hello organization then manages hello individual PTR records within their child zone.</span></span>

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
<span data-ttu-id="744d4-156">PTR 레코드에 대 한 IP 주소 '192.0.2.129' 쿼리 hello에 대 한 역방향 조회 이름이 '129.2.0.192.in-addr.arpa'입니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-156">A reverse lookup for hello IP address '192.0.2.129' queries for a PTR record named '129.2.0.192.in-addr.arpa'.</span></span> <span data-ttu-id="744d4-157">이 쿼리는 hello 자식 영역에 hello 부모 영역 toohello PTR 레코드에 CNAME hello를 통해 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-157">This query resolves via hello CNAME in hello parent zone toohello PTR record in hello child zone.</span></span>

### <a name="ipv6"></a><span data-ttu-id="744d4-158">IPv6</span><span class="sxs-lookup"><span data-stu-id="744d4-158">IPv6</span></span>

<span data-ttu-id="744d4-159">IPv6 역방향 조회 영역의 hello 이름 hello 다음 형식 이어야 합니다.`<IPv6 network prefix in reverse order>.ip6.arpa`</span><span class="sxs-lookup"><span data-stu-id="744d4-159">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`</span></span>

<span data-ttu-id="744d4-160">예제:</span><span class="sxs-lookup"><span data-stu-id="744d4-160">For example,.</span></span> <span data-ttu-id="744d4-161">Hello 2001:db8:1000:abdc에 있는 Ip와 호스트에 대 한 역방향 영역 toohost 레코드를 만들 때:: / 64 접두사 hello 영역 이름 hello 주소의 hello 네트워크 접두사를 격리 하 여 만들 수는 (2001:db8:abdc::).</span><span class="sxs-lookup"><span data-stu-id="744d4-161">When creating a reverse zone toohost records for hosts with IPs that are in hello 2001:db8:1000:abdc::/64 prefix, hello zone name would be created by isolating hello network prefix of hello address (2001:db8:abdc::).</span></span> <span data-ttu-id="744d4-162">다음 hello IPv6 네트워크 접두사 tooremove 확장 [0을 압축](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)사용된 tooshorten hello IPv6 주소 접두사 인 경우, (2001:0db8:abdc:0000::).</span><span class="sxs-lookup"><span data-stu-id="744d4-162">Next expand hello IPv6 network prefix tooremove [zero compression](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx), if it was used tooshorten hello IPv6 address prefix (2001:0db8:abdc:0000::).</span></span> <span data-ttu-id="744d4-163">Hello 순서를 반대로, toobuild hello 되돌릴 마침표를 사용 하 여 hello hello 접두사에서 각 16 진수 사이의 구분으로, 네트워크 접두사 (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) hello 접미사를 추가 하 고 `.ip6.arpa`합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-163">Reverse hello order, using a period as hello delimiter between each hexadecimal number in hello prefix, toobuild hello reversed network prefix (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) and add hello suffix `.ip6.arpa`.</span></span>


|<span data-ttu-id="744d4-164">네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="744d4-164">Network prefix</span></span>  |<span data-ttu-id="744d4-165">확장된 역방향 네트워크 접두사</span><span class="sxs-lookup"><span data-stu-id="744d4-165">Expanded and reversed network prefix</span></span> |<span data-ttu-id="744d4-166">표준 접미사</span><span class="sxs-lookup"><span data-stu-id="744d4-166">Standard suffix</span></span> |<span data-ttu-id="744d4-167">역방향 영역 이름</span><span class="sxs-lookup"><span data-stu-id="744d4-167">Reverse zone name</span></span>  |
|---------|---------|---------|---------|
|<span data-ttu-id="744d4-168">2001:db8:abdc::/64</span><span class="sxs-lookup"><span data-stu-id="744d4-168">2001:db8:abdc::/64</span></span>    | <span data-ttu-id="744d4-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="744d4-169">0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="744d4-170">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="744d4-170">.ip6.arpa</span></span>        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|<span data-ttu-id="744d4-171">2001:db8:1000:9102::/64</span><span class="sxs-lookup"><span data-stu-id="744d4-171">2001:db8:1000:9102::/64</span></span>    | <span data-ttu-id="744d4-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span><span class="sxs-lookup"><span data-stu-id="744d4-172">2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2</span></span>        | <span data-ttu-id="744d4-173">.ip6.arpa</span><span class="sxs-lookup"><span data-stu-id="744d4-173">.ip6.arpa</span></span>        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a><span data-ttu-id="744d4-174">역방향 DNS에 대한 Azure 지원</span><span class="sxs-lookup"><span data-stu-id="744d4-174">Azure support for reverse DNS</span></span>

<span data-ttu-id="744d4-175">Azure는 DNS tooreverse와 관련 된 두 가지 별도 시나리오를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-175">Azure supports two separate scenarios relating tooreverse DNS:</span></span>

<span data-ttu-id="744d4-176">**호스팅 hello 역방향 조회 영역 해당 tooyour IP 주소 블록입니다.**</span><span class="sxs-lookup"><span data-stu-id="744d4-176">**Hosting hello reverse lookup zone corresponding tooyour IP address block.**</span></span>
<span data-ttu-id="744d4-177">Azure DNS도 사용할 수 있습니다[역방향 조회 영역을 호스트 하 고 각 역방향 DNS 조회에 대 한 PTR 레코드 hello 관리](dns-reverse-dns-hosting.md), IPv4 및 IPv6 모두에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-177">Azure DNS can be used too[host your reverse lookup zones and manage hello PTR records for each reverse DNS lookup](dns-reverse-dns-hosting.md), for both IPv4 and IPv6.</span></span>  <span data-ttu-id="744d4-178">hello 위임을 설정 hello (ARPA) 역방향 조회 영역을 만드는 과정을 hello 및 구성 PTR 레코드는 hello 동일한 일반 DNS 영역 구문과 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-178">hello process of creating hello reverse lookup (ARPA) zone, setting up hello delegation, and configuring PTR records is hello same as for regular DNS zones.</span></span>  <span data-ttu-id="744d4-179">hello만 차이가 발생 hello 위임 DNS 등록을 하지 않고 인터넷 서비스 공급자를 통해 구성 되어야 하 고 hello PTR 레코드 종류를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-179">hello only differences are that hello delegation must be configured via your ISP rather than your DNS registrar, and only hello PTR record type should be used.</span></span>

<span data-ttu-id="744d4-180">**Hello tooyour Azure 서비스를 할당 한 IP 주소에 대 한 hello 역방향 DNS 레코드를 구성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="744d4-180">**Configure hello reverse DNS record for hello IP address assigned tooyour Azure service.**</span></span> <span data-ttu-id="744d4-181">Azure를 사용 하면 너무[hello IP 주소가 할당 tooyour Azure 서비스에 대 한 역방향 조회 hello 구성](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-181">Azure enables you too[configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>  <span data-ttu-id="744d4-182">이 역방향 조회는 hello 해당 ARPA 영역에는 PTR 레코드를 Azure에 의해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-182">This reverse lookup is configured by Azure as a PTR record in hello corresponding ARPA zone.</span></span>  <span data-ttu-id="744d4-183">Microsoft에서 호스팅되는 Azure에서 사용 되는 tooall hello IP 범위에 해당 이러한 ARPA 영역이</span><span class="sxs-lookup"><span data-stu-id="744d4-183">These ARPA zones, corresponding tooall hello IP ranges used by Azure, are hosted by Microsoft</span></span>

## <a name="next-steps"></a><span data-ttu-id="744d4-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="744d4-184">Next steps</span></span>

<span data-ttu-id="744d4-185">역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="744d4-185">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="744d4-186">너무 방법에 대해 알아봅니다[Azure dns에서 ISP에 할당 된 IP 범위에 대 한 호스트 hello 역방향 조회 영역](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-186">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>
<br>
<span data-ttu-id="744d4-187">너무 방법에 대해 알아봅니다[Azure 서비스에 대 한 역방향 DNS 레코드 관리](dns-reverse-dns-for-azure-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="744d4-187">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>

