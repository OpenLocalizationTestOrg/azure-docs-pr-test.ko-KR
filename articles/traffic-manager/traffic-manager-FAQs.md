---
title: "트래픽 관리자-aaaAzure Faq | Microsoft Docs"
description: "이 문서에서는 답변 toofrequently 묻는 질문에 대 한 트래픽 관리자"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Traffic Manager FAQ(질문과 대답)

## <a name="traffic-manager-basics"></a>Traffic Manager 기본 사항

### <a name="what-ip-address-does-traffic-manager-use"></a>트래픽 관리자가 사용하는 IP 주소는 어떻게 되나요?

에 설명 된 대로 [트래픽 관리자 작동 방식](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), 트래픽 관리자는 hello DNS 수준에서 작동 합니다. DNS 응답이 toodirect 클라이언트 toohello 적절 한 서비스 보내는 끝점입니다. 클라이언트가 다음 toohello 서비스 끝점 직접 연결을 통해 트래픽 관리자가 아닌 합니다.

따라서 트래픽 관리자가 클라이언트 tooconnect에 대 한 끝점 또는 IP 주소를 제공 하지 않습니다. 따라서 서비스에 대 한 고정 IP 주소를 원하는에 트래픽 관리자가 아닌 hello 서비스만 하를 구성 되어야 합니다.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Traffic Manager는 '고정' 세션을 지원하나요?

에 설명 된 대로 [트래픽 관리자 작동 방식](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), 트래픽 관리자는 hello DNS 수준에서 작동 합니다. DNS 응답 toodirect 클라이언트 toohello 적절 한 서비스 끝점을 사용합니다. 클라이언트를 통해 트래픽 관리자가 아닌 toohello 서비스 끝점을 직접 연결합니다. 따라서 트래픽 관리자는 hello 클라이언트와 서버 hello hello HTTP 트래픽을 표시 되지 않습니다.

또한 트래픽 관리자에서 받은 hello DNS 쿼리의 hello 원본 IP 주소 toohello 재귀 DNS 서비스를 hello 클라이언트가 아닌 속해 있습니다. 따라서 트래픽 관리자에 방법은 tootrack 개별 클라이언트가 없습니다를 '고정' 세션을 구현할 수 없습니다. 이 제한은 일반적인 tooall DNS 기반 트래픽 관리 시스템 이며 특정 tooTraffic 관리자 않습니다.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Traffic Manager를 사용할 때 HTTP 오류가 나타나는 이유는 무엇인가요?

에 설명 된 대로 [트래픽 관리자 작동 방식](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), 트래픽 관리자는 hello DNS 수준에서 작동 합니다. DNS 응답 toodirect 클라이언트 toohello 적절 한 서비스 끝점을 사용합니다. 클라이언트가 다음 toohello 서비스 끝점 직접 연결을 통해 트래픽 관리자가 아닌 합니다. Traffic Manager는 클라이언트와 서버 간에 HTTP 트래픽을 표시하지 않습니다. 따라서 표시된 모든 HTTP 오류는 응용 프로그램에서 가져온 것이어야 합니다. Hello 클라이언트 tooconnect toohello 응용 프로그램에 대 한 모든 DNS 확인 단계를 완료 합니다. 트래픽 관리자 hello 응용 프로그램 트래픽 흐름에 있는 모든 상호 작용 포함 됩니다.

추가 조사 따라서 hello 응용 프로그램에 초점을 맞추어야 합니다.

hello 클라이언트의 브라우저에서 전송 하는 hello HTTP 호스트 헤더 란 hello 문제의 가장 일반적인 소스입니다. Hello 응용 프로그램 사용 하는 hello 도메인 이름에 대해 구성 된 tooaccept hello 올바른 호스트 헤더 인지 확인 합니다. 끝점을 사용 하 여 hello Azure 앱 서비스, 참조 [트래픽 관리자를 사용 하 여 Azure 앱 서비스에서 웹 앱에 대 한 사용자 지정 도메인 이름을 구성](../app-service-web/web-sites-traffic-manager-custom-domain-name.md)합니다.

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>트래픽 관리자를 사용 하 여 hello 성능에 미치는 이란?

에 설명 된 대로 [트래픽 관리자 작동 방식](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), 트래픽 관리자는 hello DNS 수준에서 작동 합니다. 클라이언트가 tooyour 서비스 끝점을 직접 연결 이므로 hello 연결이 설정 되 면 트래픽 관리자를 사용 하는 경우 발생 되는 성능 영향을 주지 않습니다.

트래픽 관리자는 hello DNS 수준에서 응용 프로그램으로 통합, 되므로 hello DNS 확인 체인에 삽입 하는 추가 DNS 조회 toobe가 필요가 없습니다. hello에 미치는 영향을 트래픽 관리자의 DNS 확인 시간 최소화 됩니다. 트래픽 관리자의 이름 서버 글로벌 네트워크를 사용 하 여 한 [애니캐스트](https://en.wikipedia.org/wiki/Anycast) 네트워킹 tooensure DNS 쿼리는 항상 사용할 수 있는 이름 서버를 가장 가까운 라우트된 toohello 합니다. 또한 DNS 응답의 캐싱 hello 추가 DNS 대기 시간 발생 되는 트래픽 관리자를 사용 하 여 세션의 tooa 비율에만 적용 된다는 의미 합니다.

hello 성능 메서드 경로 toohello 가장 가까운 사용 가능한 끝점이 트래픽 합니다. hello 그 결과 해당 hello이이 메서드와 연결 된 전체 성능 영향을 최소화 해야 합니다. DNS 대기 시간 증가 시 키 지 낮은 네트워크 대기 시간 toohello 끝점에서 오프셋할지 합니다.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>트래픽 관리자에는 어떤 응용 프로그램 프로토콜을 사용할 수 있나요?

에 설명 된 대로 [트래픽 관리자 작동 방식](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), 트래픽 관리자는 hello DNS 수준에서 작동 합니다. Hello DNS 조회 완료 되 면 클라이언트 연결 toohello 응용 프로그램 끝점을 직접 통해 트래픽 관리자가 아닌 합니다. 따라서 hello 연결 모든 응용 프로그램 프로토콜을 사용할 수 있습니다. 모니터링 프로토콜, 트래픽 관리자의 hello으로 TCP를 선택할 경우 모든 응용 프로그램 프로토콜을 사용 하지 않고 끝점 상태 모니터링이 수행할 수 있습니다. Toohave hello 상태 응용 프로그램 프로토콜을 사용 하 여 확인을 선택 하면 hello 끝점 toobe 수 toorespond tooeither HTTP 또는 HTTPS GET 요청에 있어야 합니다.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>'naked' 도메인 이름으로 Traffic Manager를 사용할 수 있나요?

아니요. hello DNS 표준 CNAMEs tooco 허용 하지-다른 DNS 레코드의 hello와 동일한 존재 이름입니다. DNS 영역의 hello 구로 (또는 루트)는 항상 두 개의 기존 DNS 레코드; 포함 hello SOA 및 hello 권한 있는 NS 레코드입니다. 즉, hello DNS 표준 위반 하지 않고 hello 영역 루트에 CNAME 레코드를 만들 수 없습니다.

트래픽 관리자 DNS CNAME 레코드 toomap hello 베 니 티 DNS 이름이 필요 합니다. 예를 들어 www.contoso.com toohello 트래픽 관리자 프로필의 DNS 이름 contoso.trafficmanager.net을 매핑할 수 있습니다. 또한 hello 트래픽 관리자 프로필 끝점 hello 클라이언트에 연결 해야 하는 두 번째 DNS CNAME tooindicate를 반환 합니다.

이 문제를 해결 toowork, hello naked 도메인 이름 tooa 다른 URL에서 트래픽 관리자를 사용 하 여 수 HTTP 리디렉션 toodirect 트래픽을 사용 하는 것이 좋습니다. 예를 들어 hello naked 도메인 '만든 contoso.com' 리디렉션할 수 사용자 toohello 'www.contoso.com' toohello 트래픽 관리자 DNS 이름을 가리키는 CNAME 합니다.

트래픽 관리자에서 naked 도메인에 대한 전체 지원은 기능 백로그에서 추적됩니다. [커뮤니티 피드백 사이트에서 투표](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly)하여 이 기능 요청에 지원을 등록할 수 있습니다.

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>DNS 쿼리를 처리할 때 트래픽 관리자 hello 클라이언트 서브넷 주소 고려? 
아니요, 현재 트래픽 관리자만 hello의 원본 IP 주소 hello DNS 쿼리가 수신, 지리 및 성능 라우팅 방법에 대해 조회를 수행할 때 일반적으로 hello DNS 해결 프로그램의 hello IP 주소를 고려 합니다.  
특히, [RFC 7871 – DNS 쿼리에 클라이언트 서브넷](https://tools.ietf.org/html/rfc7871) 를 제공 하는 [EDNS0 (DNS)에 대 한 확장 메커니즘](https://tools.ietf.org/html/rfc2671) tooDNS 서버 지원 해결 프로그램에서 hello 클라이언트 서브넷 주소에 전달할 수 있는 현재 트래픽 관리자에서 지원 되지 않습니다. [커뮤니티 피드백 사이트](https://feedback.azure.com/forums/217313-networking)를 통해 이 기능 요청에 대한 지원을 받도록 등록할 수 있습니다.


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>DNS TTL이란 무엇이며 사용자에게 어떤 영향을 주나요?

트래픽 관리자는 DNS 쿼리에 처음 삽입, 활성 시간 (TTL)를 호출 하는 hello 응답에서 값을 설정 합니다. 이 값을 가진 단위는 초, 시간 toocache에 tooDNS 확인자를 다운스트림이 응답을 나타냅니다. DNS 확인자 toocache 되지 않을 때 저장 한 다음이 결과 tooTraffic 관리자 DNS 서버를 이동 하지 않고도 hello 캐시 오프 toorespond tooany 후속 쿼리가 있습니다. 영향을 주는 hello 응답 다음과 같습니다.
- 더 높은 TTL hello 제공 하는 쿼리 수는 청구 가능 사용량 고객에 대 한 hello 비용을 줄일 수는 트래픽 관리자 DNS 서버가 hello에 도착 하는 쿼리 수를 줄입니다.
- 더 높은 TTL toodo DNS 조회를 걸리는 hello 시간을 줄일 수 있습니다.
- 더 높은 TTL 데이터 hello 최신 상태 정보를 트래픽 관리자는 검색 에이전트를 통해 가져온 반영 하지 않는 의미 하기도 합니다.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>상위 또는 하위 방법 있습니까 트래픽 관리자 응답에 대 한 hello TTL을 설정할 수 있습니까?

설정할 수 있습니다에 개별 프로필 수준으로 0 초도 낮은 임계값과 같이 높은 2147483647 초 DNS TTL toobe hello (최대 범위 준수 hello [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). 0은 쿼리 응답을 캐시 하지 않음 다운스트림 DNS 확인자 및 모든 쿼리는 TTL 확인용 tooreach hello 트래픽 관리자 DNS 서버가 필요 합니다.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Traffic Manager 지리적 트래픽 라우팅 방법

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>지리적 라우팅이 유용한 사용 사례에는 어떤 것이 있습니까? 
지리적 라우팅 유형은 Azure 고객 해야 하는 toodistinguish 지리적 지역에 따라 사용자가 모든 시나리오에서 사용할 수 있습니다. 예를 들어 hello 지리적 트래픽 라우팅 방법을 사용 하 여, 사용자 제공할 수 있습니다 특정 지역에서 다른 지역에서 하는 것 보다는 다른 사용자 경험을 합니다. 또 다른 예는 특정 지역의 해당 사용자들이 해당 지역의 끝점에서만 제공받도록 하는 로컬 데이터 독립성 지침을 준수하는 것입니다.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>지원 되는 트래픽 관리자에서 지리적 라우팅에 대 한 hello 지역 이란? 
트래픽 관리자에서 사용 되는 hello 국가/지역 계층 있습니다 [여기](traffic-manager-geographic-regions.md)합니다. 또한 프로그래밍 방식으로 검색할 수 있습니다이 페이지를 변경으로 최신 상태로 유지 하는 동안 hello를 사용 하 여 동일한 정보를 hello [Azure 트래픽 관리자 REST API](https://docs.microsoft.com/rest/api/trafficmanager/)합니다. 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Traffic Manager는 어떻게 사용자가 쿼리하는 위치를 결정합니까? 
트래픽 관리자 (대부분이 hello hello 사용자를 대신 하 여 쿼리를 수행 하는 로컬 DNS 확인자) hello 쿼리의 hello 원본 IP 보고 하는 내부 IP tooregion 맵 toodetermine hello 위치를 사용 합니다. 이 맵에서 지속적으로 tooaccount hello에서 변경 내용을 업데이트 될 인터넷 합니다. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>트래픽 관리자 올바르게 hello hello 모든 경우에는 사용자의 정확한 지리적 위치를 결정할 수 있도록 보장은 것?
아니요, 트래픽 관리자 DNS 쿼리 hello 원본 IP 주소에서 유추 म 해당 hello 지리적 지역의 toohello 다음 인해 toohello 사용자의 위치를 해당 항상 됩니다 보장할 수 없습니다 이유: 

- 첫째, 이전 FAQ hello와 같이 hello는 hello 사용자를 대신 하 여 hello 조회를 수행 하는 DNS 해결 프로그램의 원본 IP 주소입니다. Hello DNS 확인자의 지리적 위치 hello hello hello 사용자의 지리적 위치에 대 한 좋은 프록시 이지만, 또한 수 hello DNS 확인자 서비스 및 hello 특정 DNS 확인자 서비스의 고객 선택 했습니다. 메모리 사용량이 hello에 다른 따라 toouse 합니다. 예를 들어 말레이시아에 있는 고객 싱가포르에서 DNS 서버를 얻을 수 있습니다 DNS 확인자 서비스 선택 toohandle 해당 사용자/장치에 대 한 hello 쿼리 해상도 장치 설정에 사용에 지정할 수 있습니다. 트래픽 관리자의 경우 hello 해결 프로그램의 IP 주소를 볼 수 있다는 점에서 toohello 싱가포르 위치에 해당 합니다. 이 페이지에서 지 원하는 클라이언트 서브넷 주소에 대 한 이전 FAQ hello를 참조 하십시오.

- 둘째, 트래픽 관리자는 내부 맵 toodo hello IP 주소 toogeographic 지역 번역을 사용합니다. 이 맵은 유효성이 검사 되 고 업데이트 하는 동안 해당 정확성과의 특성을 통해 진화 하는 hello에 대 한 계정 hello 인터넷에서 지속적으로 tooincrease는 여전히 hello 가능성을 받으려면 정보 hello 지리적 위치 모두의 정확한 나타내지는 않습니다. hello IP 주소입니다.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>가에 물리적으로 배치 하는 끝점 필요 toobe hello hello와 같은 지역의 지리적 라우팅에 사용 하는 하나? 
아니요, hello 끝점의 hello 위치에서는 영역은에 매핑된 tooit 수 수 제한이 적용 됩니다. 예를 들어 미국 중부 Azure 지역에 끝점에 전송 인도 tooit의 모든 사용자가 있을 수 있습니다.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>지리적 지역 할당할 수 없는 프로필에 tooendpoints toodo 지리적 라우팅 구성? 

예, hello 프로필의 라우팅 메서드를 지리적 없는 경우 사용할 수 있습니다 hello [Azure 트래픽 관리자 REST API](https://docs.microsoft.com/rest/api/trafficmanager/) tooassign 지리적 지역 tooendpoints 프로필에 있습니다. Hello 지리적 라우팅 유형 프로필의 경우에서이 구성은 무시 됩니다. 나중에 이러한 프로필 toogeographic 라우팅 유형을 변경 하면 트래픽 관리자는 이러한 매핑을 사용할 수 있습니다.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>이유는 무엇입니까 오류가 toochange hello 라우팅 메서드는 기존 프로필 tooGeographic 때?

지리적 라우팅을 사용 하 여 프로필 아래에서 모든 hello 끝점 toohave 필요 하나 이상의 영역 tooit 매핑됩니다. 기존 프로필 toogeographic 라우팅 유형 tooconvert 먼저 tooassociate 지리적 지역 tooall hello를 사용 하는 끝점 [Azure 트래픽 관리자 REST API](https://docs.microsoft.com/rest/api/trafficmanager/) 라우팅 hello를 변경 하기 전에 toogeographic 입력 합니다. Hello 끝점을 삭제 먼저 포털을 사용 하 여 hello hello 프로필 toogeographic의 라우팅 방법을 변경 하 고 지리적 지역 매핑 함께 hello 끝점을 추가 합니다. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>고객에게 지리적 라우팅이 활성화된 프로필의 끝점보다 중첩 프로필을 만드는 것을 권장하는 이유는 무엇입니까? 

영역 할당 될 수 있습니다 하나 tooonly 끝점 프로필 내에서 경우 해당 지리적 라우팅 유형을 사용 하 여 합니다. 해당 끝점이 없는 경우 자식 연결 된 프로필이 tooit 된 중첩된 형식을 비정상 이동 트래픽 관리자 끝점에 트래픽을 전혀 없는 하나 더를 보내지 않으면 hello 다른 방법도 이후 toosend 트래픽 tooit 계속 합니다. 할당 된 hello 지역이 "부모" hello 영역의 toohello 끝점 (예를 들어 되더라도 지역 스페인을 가진 끝점을 장애 조치 tooanother 없습니다 것 비정상 비정상를 할당 된 경우에 트래픽 관리자는 장애 조치 tooanother 끝점 하지 hello 지역 유럽을 가진 끝점을 할당 tooit). 이 트래픽 관리자 측면 hello 지리적 경계 고객에 게는 자신의 프로필에 설정 tooensure를 수행 됩니다. tooanother 끝점 끝점 비정상이 되 면 장애 조치할 tooget hello 혜택 지리적 지역 대신 개별 끝점 내에서 여러 끝점을 사용 하 여 toonested 프로필에 할당할 수 있음을 것이 좋습니다. 이러한 방식으로 중첩 hello 자식 프로필 실패 트래픽에서에서 끝점 hello 내의 장애 조치 tooanother 끝점 수 있는 경우 같은 중첩 된 자식 프로필입니다.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>이 라우팅 형식을 지 원하는 hello API 버전에 대 한 제한을 있습니까?

예. API 버전 2017-03-01 및 최신 지원 hello 지리적 라우팅 유형에 합니다. 오래 된 API 버전 지리적 라우팅 유형의 프로필을 사용 하는 toocreated 수 하거나 지리적 지역 tooendpoints를 할당할 수 없습니다. Azure 구독에서 사용 되는 tooretrieve 프로필 이전 API 버전을 사용 하는 경우에 지리적 라우팅 형식이 모든 프로필 반환 되지 않습니다. 또한 이전 API 버전을 사용하는 경우, 지리적 지역 할당을 사용하는 끝점이 있는 반환된 프로필에서 지리적 지역 할당이 표시되지 않습니다.



## <a name="traffic-manager-endpoints"></a>Traffic Manager 끝점

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>여러 구독에서 끝점으로 Traffic Manager를 사용할 수 있습니까?

Azure Web Apps의 경우 여러 구독에서 끝점을 사용하는 것은 가능하지 않습니다. Azure Web Apps은 Web Apps와 함께 사용되는 모든 사용자 지정 도메인 이름을 단일 구독 내에서만 사용할 것을 요구합니다. Hello로 여러 구독에서 웹 응용 프로그램을 가능한 toouse 없으면 동일한 도메인 이름입니다.

다른 끝점 유형에 끝점이 하나 이상의 구독에서 가능한 toouse 트래픽 관리자 리소스 관리자의 구독 으로부터의 끝점 추가할 수 있습니다 tooTraffic 관리자 hello 트래픽 관리자 프로필을 구성 하는 hello 사람에 대 한 읽기 액세스 toohello 끝점. 이러한 권한은 [Azure Resource Manager 역할 기반 액세스 제어(RBAC)](../active-directory/role-based-access-control-configure.md)를 사용하여 부여될 수 있습니다.


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>클라우드 서비스 '스테이징' 슬롯으로 Traffic Manager를 사용할 수 있습니까?

예. 클라우드 서비스 '스테이징' 슬롯은 외부 끝점으로 Traffic Manager에서 구성될 수 있습니다. 상태 검사는 hello Azure 끝점 속도로 계속 청구 됩니다. 외부 끝점 유형이 hello 사용 중에서 이므로 변경 toohello 기본 서비스 자동으로 선택 되지 않습니다. 트래픽 관리자는 외부 끝점과 함께 hello 클라우드 서비스를 중지 하거나 삭제할 때를 감지할 수 없습니다. 따라서 hello 트래픽 관리자는 hello 끝점이 비활성화 되었거나 삭제 될 때까지 상태 검사에 대 한 청구를 계속 합니다.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Traffic Manager는 IPv6 끝점을 지원하나요?

Traffic Manager는 현재 IPv6으로 주소 지정이 가능한 이름 서버를 제공하지 않습니다. 그러나 트래픽 관리자는 tooIPv6 끝점을 연결 하는 IPv6 클라이언트에 계속 사용 수 있습니다. 클라이언트를 만들지 않습니다 DNS를 tooTraffic 관리자 직접 요청 합니다. 대신, hello 클라이언트는 재귀 DNS 서비스를 사용합니다. IPv6 전용 클라이언트는 i p v 6 통해 toohello 재귀 DNS 서비스 요청을 보냅니다. 그런 다음 hello 재귀 서비스는 i p v 4를 사용 하 여 수 toocontact hello 트래픽 관리자 이름 서버 여야 합니다.

트래픽 관리자 hello 끝점의 DNS 이름을 hello 사용 하 여 응답 합니다. toosupport IPv6 끝점 DNS AAAA 기록 포인팅 hello 끝점 DNS 이름 toohello IPv6 주소가 있어야 합니다. Traffic Manager 상태 검사는 IPv4 주소만 지원합니다. hello 서비스가 필요한 tooexpose IPv4 끝점 hello에 동일한 DNS 이름입니다.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>트래픽 관리자 hello에 둘 이상의 웹 응용 프로그램을 사용할 수 있습니까 동일한 지역?

일반적으로 트래픽 관리자는 사용 되는 toodirect 트래픽 tooapplications 서로 다른 지역에 배포 합니다. 그러나도 사용할 수 있는 응용 프로그램에 둘 이상의 배포가 hello에 동일한 지역입니다. hello Azure 트래픽 관리자 끝점 허용 하지 않는 여러 웹 응용 프로그램 끝점 hello에서 동일한 Azure 지역 toobe 추가 toohello 같은 트래픽 관리자 프로필.

##  <a name="traffic-manager-endpoint-monitoring"></a>Traffic Manager 끝점 모니터링

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>트래픽 관리자 탄력적인 tooAzure 영역 장애 인지 확인 합니다.

트래픽 관리자는 Azure에서 항상 사용 가능한 응용 프로그램의 hello 배달의 핵심 구성 요소입니다.
toodeliver 고가용성을 트래픽 관리자는 매우 높은 수준의 가용성 및 복원 력 있는 tooregional 실패 수 있어야 합니다.

기본적으로 트래픽 관리자 구성 요소에는 어떠한 Azure 지역의 복원 력이 tooa 전체 오류는 합니다. 이 복원 력을 적용 tooall 트래픽 관리자 구성 요소: hello DNS 이름 서버, hello API, hello 저장소 계층 및 hello 끝점 서비스를 모니터링 합니다.

전체 Azure 지역의 중단의 흔하지을 hello, 트래픽 관리자는 예상된 toocontinue toofunction 일반적으로 합니다. 트래픽 관리자 toodirect 트래픽 tooan 응용 프로그램의 사용 가능한 인스턴스 여러 Azure 지역에 배포 된 응용 프로그램 사용 수 있습니다.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Hello 다양 한 리소스 그룹 위치에 주는 영향은 트래픽 관리자?

Traffic Manager는 단일 전역 서비스입니다. 지역에 영향을 받지 않습니다. hello 리소스 그룹 위치 선택 하면 해당 리소스 그룹에 배포 된 차이 tooTraffic 관리자 프로필이 없습니다.

Azure 리소스 관리자는 모든 리소스 그룹 toospecify 해당 리소스 그룹에 배포 된 리소스에 대 한 hello 기본 위치를 결정 하는 위치를 필요 합니다. Traffic Manager 프로필을 만들면 리소스 그룹에 만들어집니다. 모든 트래픽 관리자 프로필 사용 **글로벌** 으로 해당 위치를 hello 리소스 그룹 기본값을 재정의 합니다.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>각 끝점의 hello 현재 상태를 확인 하려면 어떻게 해야 합니까?

hello 현재 각 끝점의 상태를 모니터링 합니다. 또한 toohello 전체 프로필에에서 표시 됩니다 hello Azure 포털입니다. 이 정보를 제공 hello 트래픽 모니터 [REST API](https://msdn.microsoft.com/library/azure/mt163667.aspx), [PowerShell cmdlet](https://msdn.microsoft.com/library/mt125941.aspx), 및 [플랫폼 간 Azure CLI](../cli-install-nodejs.md)합니다.

Azure 지난 끝점에 대 한 기록 정보 tooendpoint 상태 변경에 대 한 상태 또는 hello 기능 tooraise 알림을 제공 하지 않습니다.

### <a name="can-i-monitor-https-endpoints"></a>HTTPS 끝점을 모니터링할 수 있나요?

예. Traffic Manager는 HTTPS를 통한 검색을 지원합니다. 구성 **HTTPS** hello 프로토콜로 hello 모니터링 구성 합니다.

Traffic Manager는 다음을 포함하는 인증서 유효성 검사를 제공할 수 없습니다.

* 서버 쪽 인증서의 유효성이 검사되지 않습니다.
* SNI 서버 쪽 인증서가 지원되지 않습니다.
* 클라이언트 인증서는 지원되지 않습니다.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>응용 프로그램에 HTTP 또는 HTTPS에 대한 지원이 없는 경우에도 Traffic Manager를 사용할 수 있나요?

예. TCP 프로토콜 및 트래픽 관리자 모니터링 hello 수의 TCP 연결을 시작 하 고 hello 끝점에서 응답을 대기 지정할 수 있습니다. Hello 끝점 응답 tooestablish hello 연결과 toohello 연결 요청에 응답, hello 시간 제한 내 기간 후 해당 끝점으로 표시 됩니다 정상으로.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>어떤 특정 응답은 TCP 모니터링을 사용 하는 경우 hello 끝점에서 필요한?

TCP 모니터링 사용 되는 경우 SYN 전송 하 여 3 방향 TCP 핸드셰이크 요청에서 tooendpoint 트래픽 관리자 시작 hello 지정 된 포트입니다. 그런 다음 hello 끝점의에서 응답에 대 한 hello 제한 시간 설정에 지정) (된 시간 동안 대기합니다. Hello 끝점 응답 toohello SYN SYN ACK 응답으로 hello 모니터링 설정을 hello에 지정 된 시간 제한 내 요청 후 해당 끝점 정상인 상태로 간주 됩니다. Hello SYN ACK 응답을 받으면 hello 트래픽 관리자는 RST 다시 응답 하 여 hello 연결 다시 설정 합니다.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>Traffic Manager는 사용자를 비정상 끝점에서 얼마나 빨리 이동하나요?

트래픽 관리자 수 있는 트래픽 관리자 프로필의 toocontrol hello 장애 조치 동작이 다음과 같은 여러 설정을 제공 합니다.
- hello 트래픽 관리자는 프로브 hello 끝점을 설정 하 여 더 자주 10 초 후에 검색 간격을 hello를 지정할 수 있습니다. 이렇게 하면 비정상 상태로 전환되는 끝점을 가능한 한 빨리 검색할 수 있습니다. 
- 상태 검사 요청 전에 toowait 시간 초과 기간을 지정할 수 있습니다 (최소 제한 시간 값은 5 초)입니다.
- 발생 한 오류 수는 hello 끝점이 비정상으로 표시 되기 전에 발생할 수 있습니다를 지정할 수 있습니다. 첫 번째 상태 확인에 사례 hello 끝점 hello 실패 하는 즉시 비정상 표시 되,이 값을 0으로 낮은 수 있습니다. 그러나 hello 허용 실패 수에 대 한 hello 최소 값이 0 사용 하 여 tooendpoints tooany 검색이 hello 시 발생할 수 있는 일시적인 문제로 인해 회전에서 제거 되 고 발생할 수 있습니다.
- hello DNS 응답 toobe 낮은 0에 대 한 hello 활성 시간 (TTL)을 지정할 수 있습니다. 이렇게 하면 DNS 확인자 hello 응답을 캐시할 수 없으며 및 각 쿼리에 가져오는 hello 최신 상태 정보를 통합 하는 응답 트래픽 관리자는 hello 있음을 의미 합니다.

이러한 설정을 사용 하 여 10 초 내 끝점 비정상 들어가고 hello 해당 프로필에 대 한 DNS 쿼리를 실행 하는 후 트래픽 관리자 장애 조치를 제공할 수 있습니다.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>프로필의 끝점마다 다른 모니터링 설정을 지정하려면 어떻게 하나요?

Traffic Manager 모니터링 설정은 프로필 수준별로 지정됩니다. 하나의 끝점에 대 한 다른 모니터링 설정을 toouse 해야 할 경우 해당 끝점으로 하 여 수행할 수 있습니다는 [중첩 프로필](traffic-manager-nested-profiles.md) 모니터링 설정 되어 있는 부모 프로필 hello와에서 다릅니다.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>끝점 상태 검사에 어떤 호스트 헤더가 사용되나요?

Traffic Manager는 HTTP 및 HTTPS 상태 검사에서 호스트 헤더를 사용합니다. 트래픽 관리자에서 사용 하는 hello 호스트 헤더에는 hello 프로필에 구성 된 hello 끝점 대상 hello 이름입니다. hello 대상 속성에서 hello 호스트 헤더에서 사용 하는 hello 값을 별도로 지정할 수 없습니다.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Hello 상태를 발생을 검사 하는 hello IP 주소는 무엇입니까?

hello 다음 목록은 hello IP 주소를 트래픽 관리자 상태 검사 제공 될 수 있습니다. 이 목록 tooensure를 사용할 수 있습니다 상태 이러한 IP 주소 로부터 들어오는 연결 hello 끝점 toocheck에서 허용 됩니다.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>개수 상태 검사 toomy 끝점 트래픽 관리자에서 기대할 수 있습니까?

트래픽 관리자 상태 수가 hello hello 다음에 따라 달라 집니다 끝점에 도달을 확인 합니다.
- hello hello 모니터링 간격에 대해 설정 된 값 (작은 간격은 주어진된 시간 동안에서 끝점에서 시작 되 고 더 많은 요청을 의미 하는 데 사용).
- hello 상태 확인 (hello IP 주소에서 이러한 검사 hello FAQ 앞에 나열 되어 있을 수 있는) 발생 한 위치에서 위치 hello 수입니다.

## <a name="traffic-manager-nested-profiles"></a>Traffic Manager 중첩 프로필

### <a name="how-do-i-configure-nested-profiles"></a>중첩 프로필을 구성하려면 어떻게 해야 하나요?

중첩 된 트래픽 관리자 프로필 모두 hello Azure 리소스 관리자를 사용 하 여 구성할 수 있으며 hello 클래식 Azure REST Api, Azure PowerShell cmdlet 및 크로스 플랫폼 Azure CLI 명령입니다. Hello 새 Azure 포털을 통해도 지원 됩니다. Hello 클래식 포털에서 지원 되지 않습니다.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>트래픽 관리자가 지원하는 중첩 계층 수는 얼마나 되나요?

프로필 too10 수준 깊이를 중첩할 수 있습니다. '루프'는 허용되지 않습니다.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>함께 사용할 수 있습니까 다른 끝점 형식을 중첩 된 자식 프로필로 같은 트래픽 관리자 프로필 hello?

예. 프로필 내에서 서로 다른 유형의 끝점을 결합하는 방법에는 제한이 없습니다.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>중첩 된 프로필에 대 한 청구 모델 hello 적용 하는 방법

중첩 프로필을 사용한다고 해서 가격이 더 부과되지는 않습니다.

Traffic Manager 요금 청구는 끝점 상태 검사 및 수백만 개의 DNS 쿼리로 구성됩니다.

* 끝점 상태 검사: 부모 프로필에서 끝점으로 구성된 자식 프로필에 대해서는 요금이 부과되지 않습니다. Hello 자식 프로필의 hello 끝점 모니터링 hello에 대 한 요금이 청구 일반적인 방법입니다.
* DNS 쿼리: 각 쿼리는 한 번만 계산됩니다. 자식 프로필에서 끝점을 반환 하는 부모 프로필에 대 한 쿼리는만 hello 부모 프로필에 대해 계산 됩니다.

전체 세부 정보에 대 한 참조 hello [트래픽 관리자 가격 책정 페이지](https://azure.microsoft.com/pricing/details/traffic-manager/)합니다.

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>중첩 프로필이 성능에 영향을 미치나요?

아니요. 중첩 프로필을 사용해도 성능에 미치는 영향은 없습니다.

트래픽 관리자 이름 서버 hello 각 DNS 쿼리를 처리할 때 내부적으로 hello 프로필 계층 구조를 통과 합니다. DNS 쿼리 tooa 부모 프로필이 자식 프로필에서 끝점 포함 된 DNS 응답을 받을 수 있습니다. 단일 CNAME 레코드는 단일 프로필이나 중첩 프로필을 사용하는 경우 사용합니다. Hello 계층 구조에서 각 프로필에 대 한 CNAME 레코드는 필요 toocreate 없습니다.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>트래픽 관리자는 부모 프로필에서 중첩 된 끝점의 hello 상태를 계산 하는 방법

hello 부모 프로필 직접 hello 자식에 대해 상태 검사를 수행 하지 않습니다. 대신 hello 자식 프로필의 끝점의 hello 상태가 사용 되는 toocalculate hello hello 자식 프로필의 전반적인 상태입니다. 이 정보는 중첩 된 hello 끝점의 중첩 된 hello 프로필 계층 toodetermine hello 상태를 전파 됩니다. hello 부모 프로필 hello 트래픽 directed toohello 자식일 수 있는지 여부를이 집계 상태 toodetermine를 사용 합니다.

hello 다음 표에서 설명 hello 동작의 트래픽 관리자는 중첩 된 끝점에 대 한 상태를 확인 합니다.

| 자식 프로필 모니터 상태 | 부모 끝점 모니터 상태 | 참고 사항 |
| --- | --- | --- |
| Disabled. hello 자식 프로필에 사용할 수 없습니다. |중지됨 |hello 부모 끝점 상태가 중지 되 면 사용 하지 않도록 설정 합니다. hello 사용 안 함 상태로 hello 부모 프로필에서 끝점 hello를 사용할 수 없음을 나타내는 예약 되어 있습니다. |
| Degraded. 하나 이상의 자식 프로필 끝점이 Degraded 상태입니다. |온라인: hello hello 자식 프로필의 Online 끝점 수가 이상 hello 수가 MinChildEndpoints 값입니다.<BR>CheckingEndpoint: hello hello 자식 프로필의 Online + checkingendpoint Endpoints 끝점 수가 적어도 hello 수가 MinChildEndpoints 값입니다.<BR>Degraded: 그렇지 않은 경우 |트래픽이는 CheckingEndpoint 상태의 끝점 라우트된 tooan 됩니다. MinChildEndpoints를 너무 높게 설정 하면 hello 끝점 항상 저하 됩니다. |
| Online. 하나 이상의 하위 프로필 끝점이 온라인 상태입니다. 끝점이에 hello Degraded 상태입니다. |위 내용을 참조하세요. | |
| CheckingEndpoints. 하나 이상의 하위 프로필 끝점이 'CheckingEndpoint'입니다. '온라인' 또는 '성능이 저하'된 끝점이 없습니다. |위와 동일합니다. | |
| Inactive. 모든 하위 프로필 끝점이 사용 안 함 또는 중지됨이거나 끝점이 없는 프로필입니다. |중지됨 | |

## <a name="next-steps"></a>다음 단계:
- 트래픽 관리자 [끝점 모니터링 및 자동 장애 조치(failover)](../traffic-manager/traffic-manager-monitoring.md)에 대해 자세히 알아봅니다.
- 트래픽 관리자 [트래픽 라우팅 방법](../traffic-manager/traffic-manager-routing-methods.md)에 대해 자세히 알아봅니다.