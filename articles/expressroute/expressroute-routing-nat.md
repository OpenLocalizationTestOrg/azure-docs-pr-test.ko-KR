---
title: "Azure ExpressRoute용 NAT | Microsoft Docs"
description: "이 페이지는 Express 경로 회로에 라우팅을 구성하고 관리하는 자세한 요구 사항을 제공합니다."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>ExpressRoute용 NAT

ExpressRoute를 사용 하 여 tooconnect tooMicrosoft 클라우드 서비스, tooset 필요한 하 라우팅을 관리 합니다. 일부 연결 공급자는 라우팅을 관리 서비스로 설치하고 관리해 줍니다. 이 서비스를 제공 하는 경우 연결 공급자 toosee 확인 하십시오. 그렇지 않으면 toohello 요구 사항 준수 해야 합니다. 

Toohello 참조 [회로 및 라우팅 도메인](expressroute-circuit-peerings.md) 문서에 대 한 설명은 hello 라우팅 toobe 해야 하는 세션 toofacilitate 연결에서을 설정 합니다.

> [!NOTE]
> Microsoft는 고가용성 구성을 위해 라우터 중복 프로토콜(예: HSRP, VRRP)을 지원하지 않습니다. 고가용성에 대한 피어링에 대해 BGP 세션의 중복 쌍에 의존합니다.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>피어링에 사용된 IP 주소

IP의 몇 가지 블록 tooreserve 필요한 네트워크 및 Microsoft의 엔터프라이즈에 지 (MSEEs) 라우터 간에 tooconfigure 라우팅 주소입니다. 이 섹션의 요구 사항 목록을 제공 하 고 이러한 IP 주소 해야 획득와 사용 방법에 대 한 hello 규칙을 설명 합니다.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Azure 개인 피어링에 사용된 IP 주소

개인 IP 주소 또는 공용 IP 주소 tooconfigure hello 피어 링을 사용할 수 있습니다. 경로 구성 하는 데 사용 되는 hello 주소 범위 주소 사용 되는 범위 toocreate Azure의 가상 네트워크와 겹치지 않아야 합니다. 

* 라우팅 인터페이스에 하나의 /29 서브넷 또는 두 개의 /30 서브넷을 예약해야 합니다.
* 라우팅에 사용 되는 hello 서브넷은 개인 IP 주소 또는 공용 IP 주소 될 수 있습니다.
* hello 서브넷 hello 고객 hello Microsoft 클라우드에서 사용 하기 위해 예약한 hello 범위와 충돌 하지 않아야 합니다.
* /29 서브넷을 사용한 경우 두 개의 /30 서브넷으로 분할됩니다. 
  * 먼저 hello/30 서브넷 hello 기본 링크에 대 한 사용 되 고 hello 두 번째/30 서브넷 hello 보조 링크에 사용 됩니다.
  * 각 hello/30 서브넷에 대 한 라우터에서 hello hello/30 서브넷의 첫 번째 IP 주소를 사용 해야 합니다. Microsoft는 hello BGP 세션을 hello/30 서브넷 tooset의 두 번째 IP 주소로 사용 합니다.
  * 에 대 한 BGP 세션을 모두 설정 해야이 [가용성 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 유효 합니다.  

#### <a name="example-for-private-peering"></a>개인 피어링에 대한 예제

Toouse a.b.c.d/29 tooset hello 피어 링을 선택 하면 두 개의/30 서브넷으로 분할 됩니다. Hello 아래 예제에서는 hello a.b.c.d/29 서브넷은 사용 하는 방법에 대해 살펴보겠습니다. 

a.b.c.d/29 분할 tooa.b.c.d/30 및 a.b.c.d+4/30 되 고 tooMicrosoft Api를 프로 비전 하는 hello 통해 전달 합니다. Hello VRF IP 기본 PE hello 및 Microsoft을 사용 하면 a.b.c.d+2 VRF IP에 대 한 hello 대로 대 한 hello 기본 MSEE 대로 a.b.c.d+1를 사용 합니다. Hello VRF IP hello 보조 PE 및 Microsoft ´ ֲ a.b.c.d+6 대로 VRF IP에 대 한 hello에 대 한 hello 보조 MSEE 대로 a.b.c.d+5를 사용 합니다.

개인 피어 링을 192.168.100.128/29 tooset 선택할 수 있는 경우를 고려해 보십시오. 192.168.100.128/29 192.168.100.128 주소가 포함 되어 too192.168.100.135 중:

* 192.168.100.128/30 toolink1, 192.168.100.129 및 192.168.100.130를 사용 하 여 Microsoft를 사용 하 여 공급자와 함께 지정 됩니다.
* 192.168.100.132/30 toolink2, 192.168.100.133 및 192.168.100.134를 사용 하 여 Microsoft를 사용 하 여 공급자와 함께 지정 됩니다.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Azure 공용 네트워크 및 Microsoft 피어링에 사용된 IP 주소

소유 하 고 있는 공용 IP 주소를 사용 하 여 hello BGP 세션을 설정 해야 합니다. Microsoft은 인터넷 레지스트리에 라우팅 및 인터넷 라우팅 레지스트리에 통해 hello IP 주소의 수 tooverify hello 소유권 이어야 합니다. 

* 고유한 사용 해야/29 서브넷 또는 두 개의/30 서브넷 tooset hello BGP 각 피어 링 express 경로 회로 당 (있는 경우 둘 이상의)에 대 한 피어 링입니다. 
* /29 서브넷을 사용한 경우 두 개의 /30 서브넷으로 분할됩니다. 
  * 먼저 hello/30 서브넷 hello 기본 링크에 대 한 사용 되 고 hello 두 번째/30 서브넷 hello 보조 링크에 사용 됩니다.
  * 각 hello/30 서브넷에 대 한 라우터에서 hello hello/30 서브넷의 첫 번째 IP 주소를 사용 해야 합니다. Microsoft는 hello BGP 세션을 hello/30 서브넷 tooset의 두 번째 IP 주소로 사용 합니다.
  * 에 대 한 BGP 세션을 모두 설정 해야이 [가용성 SLA](https://azure.microsoft.com/support/legal/sla/) toobe 유효 합니다.

## <a name="public-ip-address-requirement"></a>공용 IP 주소 요구 사항

### <a name="private-peering"></a>개인 피어링

개인 피어 링에 대 한 공용 또는 개인 IPv4 주소가 toouse를 선택할 수 있습니다. 개인 피어링의 경우 다른 고객과 주소가 중첩되지 않도록 트래픽의 종단 간 격리를 제공합니다. 이러한 주소는 보급된 tooInternet 하지 않습니다. 

### <a name="public-peering"></a>공용 피어링

hello Azure 공용 피어 링 경로 있습니다 tooconnect tooall Azure에서 호스팅된 서비스를 공용 IP 주소를 통해 수 있습니다. 여기에 hello에 나열 된 서비스가 [ExpessRoute FAQ](expressroute-faqs.md) 및 isv Microsoft Azure에서 호스트 되는 모든 서비스입니다. 연결 tooMicrosoft Azure 서비스에 공용 피어 링 항상 초기화 네트워크에서 Microsoft 네트워크 hello로 합니다. Hello 트래픽 보내는 tooMicrosoft 네트워크에 대 한 공용 IP 주소를 사용 해야 합니다.

### <a name="microsoft-peering"></a>Microsoft 피어링

hello Microsoft 피어 링 경로 사용 하면 hello Azure 공용 피어 링 경로 통해 지원 되지 않는 tooMicrosoft 클라우드 서비스를 연결할 수 있습니다. Exchange Online, SharePoint Online, 비즈니스용 Skype를 및 Dynamics 365 등의 Office 365 서비스를 포함 하는 서비스의 hello 목록이 나타납니다. Microsoft는 hello Microsoft 피어 링에 양방향 연결을 지원합니다. 전송 트래픽을 tooMicrosoft 클라우드 서비스는 hello Microsoft 네트워크를 입력 하기 전까지 유효한 공용 IPv4 주소를 사용 해야 합니다.

IP 주소와 마찬가지로 번호는 확인 아래에 나열 된 hello 레지스트리 중 하나에 등록 된 tooyou 됩니다.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> 공용 IP 주소 보급 tooMicrosoft ExpressRoute 통해 보급된 toohello 인터넷 되지 않아야 합니다. 이 연결 tooother Microsoft 서비스를 바꿀 수 있습니다. 그러나 ExpressRoute를 통해 Microsoft 내에서 O365 끝점과 통신하는 네트워크의 서버에서 사용하는 공용 IP 주소를 보급할 수 있습니다. 
> 
> 

## <a name="dynamic-route-exchange"></a>동적 경로 Exchange

라우팅 Exchange는 eBGP 프로토콜을 통합니다. Hello MSEEs와 라우터 간의 EBGP 세션이 설정 됩니다. BGP 세션의 인증은 요구되지 않습니다. 필요한 경우 MD5 해시를 구성할 수 있습니다. Hello 참조 [구성 라우팅](expressroute-howto-routing-classic.md) 및 [프로비저닝 워크플로 회로 및 상태 회로](expressroute-workflows.md) BGP 세션을 구성 하는 방법에 대 한 정보에 대 한 합니다.

## <a name="autonomous-system-numbers"></a>자치 시스템 번호

Microsoft는 Azure 공용, Azure 개인 및 Microsoft 피어링에 AS 12076를 사용합니다. Asn 내부 용도로 65515 too65520에서 예약 했습니다. 16 및 32비트 AS 번호를 모두 지원합니다.

데이터 전송 대칭에 요구 사항이 없습니다. hello 전달 및 반환 경로 서로 다른 라우터 쌍을 포함할 수 있습니다. 동일한 경로는 사용자에게 속한 여러 회로 쌍에 걸쳐 한 쪽에서 보급해야 합니다. 경로 메트릭을 필요한 toobe 동일 하지 않습니다.

## <a name="route-aggregation-and-prefix-limits"></a>경로 집계 및 접두사 제한

Too4000를 지원 접두사 toous hello Azure 개인 피어 링을 통해 보급 합니다. 이 too10, 000 접두사 hello ExpressRoute premium 추가 기능에서 사용 되는 경우를 늘릴 수 있습니다. 공용 Azure에 대 한 BGP 세션당 too200 접두사와 Microsoft 피어 링를 수락합니다. 

hello BGP 세션에는 접두사 수 hello hello 제한을 초과 하면 삭제 됩니다. 기본 경로 hello 개인 피어 링 링크에만 허용 됩니다. 기본 경로 및 hello 공용 Azure에서에서 개인 IP 주소 (RFC 1918) 및 Microsoft 피어 링 경로 공급자 필터링 해야 합니다. 

## <a name="transit-routing-and-cross-region-routing"></a>전송 라우팅 및 영역 간 라우팅

ExpressRoute는 전송 라우터로 구성할 수 없습니다. 전송 라우팅 서비스에 대 한 연결 공급자에 toorely를 해야 합니다.

## <a name="advertising-default-routes"></a>기본 경로 광고

기본 경로는 Azure 개인 피어링 세션에서만 허용됩니다. 이 경우에서는 hello 연결 된 가상 네트워크 tooyour 네트워크에서 모든 트래픽을 라우팅합니다. 개인 피어 링에 기본 경로 알리면 hello 인터넷 경로 차단 되 고 Azure에서 발생 합니다. Toohello Azure에서 호스팅된 서비스에 대 한 인터넷 및에서 회사 가장자리 tooroute 트래픽에 사용 하며 해야 합니다. 

 tooenable 연결 tooother Azure 서비스 및 인프라 서비스 hello 다음 항목 중 하나는 위치에 있는지 확인 해야 합니다.

* 활성화 된 tooroute 트래픽 toopublic 끝점은 azure 공용 피어 링
* 모든 서브넷 필요한 인터넷 연결에 사용자 지정 라우팅 tooallow 인터넷에 연결을 사용합니다.

> [!NOTE]
> 기본 경로를 보급하면 Windows 및 다른 VM 라이선스 정품 인증이 중단됩니다. 지침에 따라 [여기](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork이 있습니다.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>BGP 커뮤니티에 대한 지원(미리 보기)

이 섹션에서는 BGP 커뮤니티를 어떻게 ExpressRoute와 함께 사용하는지에 대한 개요를 제공합니다. Microsoft은 커뮤니티 적절 한 값으로 태그가 지정 된 경로 가진 공용 hello 및 Microsoft 피어 링 경로에서 경로 보급 합니다. 이렇게 근거 hello 및 hello 아래 값을 설명 하는 커뮤니티에 대 한 세부 정보입니다. 그러나 Microsoft,는 인식 하지 못합니다 된 커뮤니티 값 태그가 지정 된 tooroutes tooMicrosoft 보급 합니다.

TooMicrosoft 지리적 지역 내에서 모든 한 피어 링 위치에서 ExpressRoute를 통해 연결 하는 경우에 hello 지정 학적 경계 내에서 모든 지역에 걸쳐 tooall Microsoft 클라우드 서비스 액세스를 해야 합니다. 

예를 들어 암스테르담에서 tooMicrosoft ExpressRoute를 통해 연결을 액세스 tooall Microsoft 클라우드 서비스 유럽 북부 및 서 부 유럽에서 호스트 해야 합니다. 

Toohello 참조 [express 경로 파트너 및 피어 링 위치](expressroute-locations.md) 자세한 목록은 지리적 영역, 연결 된 Azure 지역 및 해당 ExpressRoute 위치 피어 링에 대 한 페이지입니다.

지정학적 지역 마다 하나 이상의 ExpressRoute 회로를 구입할 수 있습니다. 고가용성에 상당한 이점을 제공 여러 개의 연결이 있는 due toogeo 중복 됩니다. ExpressRoute 회로 여러 개 있는 경우에 접두사의 동일한 집합 보급 hello hello 공용 피어 링에 Microsoft 및 Microsoft 경로 피어 링으로 표시 됩니다. 즉, 네트워크에서 Microsoft까지 여러 경로가 있습니다. 네트워크 내에서 라우팅 결정 toobe 성능이 저하 될 수 있습니다. 결과적으로, 최적 상태의 연결 환경을 toodifferent 서비스 발생할 수 있습니다. 

Microsoft는 공용 피어 링을 통해 보급 되는 접두사를 태그 및 hello 지역 hello 접두사를 나타내는 적절 한 BGP 커뮤니티 값으로 피어 링 하는 Microsoft에서 호스팅되는 합니다. Hello 커뮤니티 값 toomake 적절 한 라우팅 결정 toooffer에 의존할 수 있습니다 [최적의 라우팅 toocustomers](expressroute-optimize-routing.md)합니다.

| **지역** | **Microsoft Azure 지역** | **BGP 커뮤니티 값** |
| --- | --- | --- |
| **북아메리카** | | |
| 미국 동부 |12076분 51004초 | |
| 미국 동부 2 |12076분 51005초 | |
| 미국 서부 |12076분 51006초 | |
| 미국 서부 2 |12076분 51026초 | |
| 미국 중서부 |12076분 51027초 | |
| 미국 중북부 |12076분 51007초 | |
| 미국 중남부 |12076분 51008초 | |
| 미국 중부 |12076분 51009초 | |
| 캐나다 중부 |12076분 51020초 | |
| 캐나다 동부 |12076분 51021초 | |
| **남미** | | |
| 브라질 남부 |12076분 51014초 | |
| **유럽** | | |
| 북유럽 |12076분 51003초 | |
| 서유럽 |12076:51002 | |
| **아시아 태평양** | | |
| 동아시아 |12076분 51010초 | |
| 동남아시아 |12076분 51011초 | |
| **일본** | | |
| 일본 동부 |12076분 51012초 | |
| 일본 서부 |12076분 51013초 | |
| **오스트레일리아** | | |
| 오스트레일리아 동부 |12076분 51015초 | |
| 오스트레일리아 남동부 |12076분 51016초 | |
| **인도** | | |
| 인도 남부 |12076분 51019초 | |
| 인도 서부 |12076분 51018초 | |
| 인도 중부 |12076분 51017초 | |

Microsoft에서 보급 하는 모든 경로 hello 커뮤니티 적절 한 값으로 태그를 지정 합니다. 

> [!IMPORTANT]
> 전역 접두사는 적절한 커뮤니티 값으로 태그가 지정되며 ExpressRoute Premium 추가 기능을 사용하는 경우에만 보급됩니다.
> 
> 

또한 toohello 위의 Microsoft는 또한 태그 접두사에 속해 hello 서비스에 따라입니다. 이 피어 링만 toohello Microsoft 적용 됩니다. hello 표에서 서비스 tooBGP 커뮤니티 값의 매핑을 제공합니다.

| **서비스** | **BGP 커뮤니티 값** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **비즈니스용 Skype** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **다른 Office 365 서비스** |12076분 5100초 |

> [!NOTE]
> Microsoft는 hello 경로 보급된 tooMicrosoft에 설정한 모든 BGP 커뮤니티 값을 준수 하지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계

* ExpressRoute 연결을 구성합니다.
  
  * [Hello 클래식 배포 모델에 대 한 ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 또는 [만들기 및 Azure 리소스 관리자를 사용 하 여 ExpressRoute 회로 수정 합니다.](expressroute-howto-circuit-arm.md)
  * [Hello 클래식 배포 모델에 대 한 라우팅을 구성](expressroute-howto-routing-classic.md) 또는 [hello 리소스 관리자 배포 모델에 대 한 라우팅을 구성 합니다.](expressroute-howto-routing-arm.md)
  * [클래식 VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md) 또는 [리소스 관리자 VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)

