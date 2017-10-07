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
# <a name="overview-of-reverse-dns-and-support-in-azure"></a>Azure의 역방향 DNS 및 지원 개요

이 문서에서는 Azure에서 지원 되는 역방향 DNS 시나리오 어떻게 역방향 DNS 작동 하며 hello에 대 한 개요를 제공 합니다.

## <a name="what-is-reverse-dns"></a>역방향 DNS란?

규칙에 따른 DNS 레코드는 DNS 이름 (예: 'www.contoso.com') tooan IP 주소 (예: 64.4.6.100)에서 매핑을 사용합니다.  역방향 DNS에 IP 주소 (64.4.6.100) 백 tooa 이름 ('www.contoso.com')의 hello 번역을 수 있습니다.

역방향 DNS 레코드는 다양한 상황에 사용됩니다. 예를 들어 역방향 DNS 레코드는 전자 메일 스팸 전자 메일 메시지의 보낸 사람 hello를 확인 하기 위해 널리 사용 됩니다.  hello 받는 메일 서버 검색의 서버 IP 주소를 보내는 hello 역방향 DNS 레코드를 hello 하 고 호스팅하는 경우는 권한 있는 toosend 전자 메일 hello에서 시작 된 도메인을 확인 합니다. 

## <a name="how-reverse-dns-works"></a>역방향 DNS 작동 방식

역방향 DNS 레코드는 'ARPA' 영역이라는 특수한 DNS 영역에서 호스팅됩니다.  이러한 영역 만든 'contoso.com'와 같은 도메인 호스팅 hello 기본 계층 구조와 동시에 별도 DNS 계층 구조를 형성 합니다.

예를 들어 hello DNS 레코드 'www.contoso.com' hello 이름의 hello 영역 '만든 contoso.com'에서 ' w w w'는 'A' DNS 레코드를 사용 하 여 구현 됩니다.  이 A 레코드는이 경우 64.4.6.100 toohello 해당 IP 주소를 가리킵니다.  hello 역방향 조회는 구현 별도로 '100' hello '6.4.64.in-addr.arpa' 영역에 (참고 IP 주소에 ARPA 영역이 반대가 됩니다.) 라는 'PTR' 레코드를 사용 하 여  이 PTR 레코드를 올바르게 구성 되어 toohello 이름 'www.contoso.com' 가리킵니다.

조직은 IP 주소 블록에 할당 된 hello 오른쪽 toomanage hello 해당 ARPA 영역도 획득 합니다. hello ARPA 영역이 블록 Azure에서 사용 하는 호스트 및 Microsoft에서 관리 되는 toohello IP 주소에 해당 합니다. ISP를 고유한 IP 주소에 대 한 hello ARPA 영역을 호스팅할 수 있고 또는 풀기 Azure DNS의 DNS 서비스의 hello ARPA 영역이 tooyou 호스트를 허용할 수 있습니다.

> [!NOTE]
> 정방향 및 역방향 DNS 조회를 DNS 계층과 함께 별도로 구현합니다. hello 'www.contoso.com'에 대 한 역방향 조회는 **하지** 을 만든 ' contoso.com' hello 영역에서 호스트 대신 호스팅되는지 hello 해당 IP 주소 블록에 대 한 hello ARPA 영역입니다. IPv4 및 IPv6 주소 블록에 별도 영역이 사용됩니다.

### <a name="ipv4"></a>IPv4

형식에 따라 hello에 IPv4 역방향 조회 영역의 hello 이름 있어야: `<IPv4 network prefix in reverse order>.in-addr.arpa`합니다.

예를 들어를 만들 때 역방향 영역 toohost 레코드 hello 192.0.2.0/24 접두사에 있는 Ip와 호스트에 대 한 hello 영역 이름이 만들어집니다 (192.0.2) hello 주소 (2.0.192) hello 순서를 반대로 고 hello 추가의 hello 네트워크 접두사를 격리 하 여 접미사 `.in-addr.arpa`합니다.

|서브넷 클래스|네트워크 접두사  |역방향 네트워크 접두사  |표준 접미사  |역방향 영역 이름 |
|-------|----------------|------------|-----------------|---------------------------|
|클래스 A|203.0.0.0/8     | 203        | .in-addr.arpa   | `203.in-addr.arpa`        |
|클래스 B|198.51.0.0/16   | 51.198     | .in-addr.arpa   | `51.198.in-addr.arpa`     |
|클래스 C|192.0.2.0/24    | 2.0.192    | .in-addr.arpa   | `2.0.192.in-addr.arpa`    |

### <a name="classless-ipv4-delegation"></a>클래스 없는 IPv4 위임

경우에 따라 tooan 조직 할당 된 hello IP 범위 보다 작으면 클래스 C (/ 24) 범위입니다. 이 경우 hello IP 범위 떨어지지 hello 내 영역 경계에 `.in-addr.arpa` 계층 영역을 마우스 따라서 하위 영역으로 위임할 수 없습니다.

다른 메커니즘을 사용 하는 대신 개별 역방향 조회 (PTR)의 tootransfer 제어 전용 tooa DNS 영역을 기록 합니다. 이 메커니즘을 각 IP 범위에 대 한 자식 영역 위임 후 지도 hello에 각 IP 주소 범위는 개별적으로 CNAME 레코드를 사용 하 여 toothat 자식 영역.

예를 들어 조직 hello IP 범위 192.0.2.128/26 ISP 하 여 부여 합니다. 이 IP 주소가 64 192.0.2.128에서 나타냅니다 too192.0.2.191 합니다. 이 범위에 대한 역방향 DNS는 다음과 같이 구현됩니다.
- hello 조직 addr.arpa-26.2.0.192.in-128을 호출 하는 역방향 조회 영역을 만듭니다. hello 접두사 ' 128-26' 나타냅니다 hello 네트워크 세그먼트 할당 toohello 조직 내에서 클래스 C hello (/ 24) 범위입니다.
- hello ISP hello 클래스 C 부모 영역에서 NS 레코드 tooset을 영역 위에 hello에 대 한 DNS 위임 hello 만듭니다. 또한 만듭니다 CNAME 레코드 hello 부모 (클래스 C) 역방향 조회 영역에서 각 IP 주소 hello IP 범위 toohello 새 영역 hello 조직에서 만드는에 매핑:

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
- hello 조직 다음 자식 영역 내에서 hello 개별 PTR 레코드를 관리합니다.

```
$ORIGIN 128-26.2.0.192.in-addr.arpa
; PTR records for each UIP address. Names match CNAME targets in parent zone
129      PTR    www.contoso.com
130      PTR    mail.contoso.com
131      PTR    partners.contoso.com
; etc
```
PTR 레코드에 대 한 IP 주소 '192.0.2.129' 쿼리 hello에 대 한 역방향 조회 이름이 '129.2.0.192.in-addr.arpa'입니다. 이 쿼리는 hello 자식 영역에 hello 부모 영역 toohello PTR 레코드에 CNAME hello를 통해 확인합니다.

### <a name="ipv6"></a>IPv6

IPv6 역방향 조회 영역의 hello 이름 hello 다음 형식 이어야 합니다.`<IPv6 network prefix in reverse order>.ip6.arpa`

예제: Hello 2001:db8:1000:abdc에 있는 Ip와 호스트에 대 한 역방향 영역 toohost 레코드를 만들 때:: / 64 접두사 hello 영역 이름 hello 주소의 hello 네트워크 접두사를 격리 하 여 만들 수는 (2001:db8:abdc::). 다음 hello IPv6 네트워크 접두사 tooremove 확장 [0을 압축](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx)사용된 tooshorten hello IPv6 주소 접두사 인 경우, (2001:0db8:abdc:0000::). Hello 순서를 반대로, toobuild hello 되돌릴 마침표를 사용 하 여 hello hello 접두사에서 각 16 진수 사이의 구분으로, 네트워크 접두사 (`0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2`) hello 접미사를 추가 하 고 `.ip6.arpa`합니다.


|네트워크 접두사  |확장된 역방향 네트워크 접두사 |표준 접미사 |역방향 영역 이름  |
|---------|---------|---------|---------|
|2001:db8:abdc::/64    | 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2        | .ip6.arpa        | `0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa`       |
|2001:db8:1000:9102::/64    | 2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2        | .ip6.arpa        | `2.0.1.9.0.0.0.1.8.b.d.0.1.0.0.2.ip6.arpa`        |


## <a name="azure-support-for-reverse-dns"></a>역방향 DNS에 대한 Azure 지원

Azure는 DNS tooreverse와 관련 된 두 가지 별도 시나리오를 지원 합니다.

**호스팅 hello 역방향 조회 영역 해당 tooyour IP 주소 블록입니다.**
Azure DNS도 사용할 수 있습니다[역방향 조회 영역을 호스트 하 고 각 역방향 DNS 조회에 대 한 PTR 레코드 hello 관리](dns-reverse-dns-hosting.md), IPv4 및 IPv6 모두에 대 한 합니다.  hello 위임을 설정 hello (ARPA) 역방향 조회 영역을 만드는 과정을 hello 및 구성 PTR 레코드는 hello 동일한 일반 DNS 영역 구문과 합니다.  hello만 차이가 발생 hello 위임 DNS 등록을 하지 않고 인터넷 서비스 공급자를 통해 구성 되어야 하 고 hello PTR 레코드 종류를 사용 해야 합니다.

**Hello tooyour Azure 서비스를 할당 한 IP 주소에 대 한 hello 역방향 DNS 레코드를 구성 합니다.** Azure를 사용 하면 너무[hello IP 주소가 할당 tooyour Azure 서비스에 대 한 역방향 조회 hello 구성](dns-reverse-dns-for-azure-services.md)합니다.  이 역방향 조회는 hello 해당 ARPA 영역에는 PTR 레코드를 Azure에 의해 구성 됩니다.  Microsoft에서 호스팅되는 Azure에서 사용 되는 tooall hello IP 범위에 해당 이러한 ARPA 영역이

## <a name="next-steps"></a>다음 단계

역방향 DNS에 대한 자세한 내용은 [Wikipedia에서 역방향 DNS 조회](http://en.wikipedia.org/wiki/Reverse_DNS_lookup)를 참조하세요.
<br>
너무 방법에 대해 알아봅니다[Azure dns에서 ISP에 할당 된 IP 범위에 대 한 호스트 hello 역방향 조회 영역](dns-reverse-dns-for-azure-services.md)합니다.
<br>
너무 방법에 대해 알아봅니다[Azure 서비스에 대 한 역방향 DNS 레코드 관리](dns-reverse-dns-for-azure-services.md)합니다.

