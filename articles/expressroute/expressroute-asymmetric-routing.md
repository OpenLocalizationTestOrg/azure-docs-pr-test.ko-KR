---
title: "aaaAsymmetric 라우팅 | Microsoft Docs"
description: "이 문서에서는 고객이 여러 개의 링크 tooa 대상이 있는 네트워크에 있는 비대칭 라우팅을 사용 하 여 발생할 수 hello 문제를 안내 합니다."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>여러 네트워크 경로를 포함한 비대칭 라우팅
이 문서에서는 네트워크 원본과 대상 간에 여러 경로를 사용할 수 있을 때 전달 및 반환 네트워크 트래픽에서 다른 경로를 사용하는 방법을 설명합니다.

중요 한 toounderstand 두 개념 toounderstand 비대칭 라우팅입니다. 하나는 여러 네트워크 경로의 hello 효과입니다. 다른 hello는 방화벽 같은 장치 상태를 유지 하는 방법입니다. 이러한 종류의 장치는 상태 저장 장치라고 합니다. 이러한 두 가지 요인의 조합이 만듭니다 시나리오는 네트워크에서 트래픽을 상태 저장 장치에 의해 때문에 삭제 된 트래픽을 채널이 hello 장치 자체는 hello 상태 저장 장치를 검색할 수 없습니다.

## <a name="multiple-network-paths"></a>여러 네트워크 경로
엔터프라이즈 네트워크에 경우 인터넷 서비스 공급자의 인터넷 hello에서 모든 트래픽 tooand 통해 인터넷 이동 하는 하나의 링크 toohello hello 동일한 경로만 합니다. 종종 회사 중복 경로 tooimprove 네트워크 가동 시간으로 여러 회로 구입합니다. 이 경우의 가능한 hello 네트워크, 인터넷 toohello 외부로 이동 하는 트래픽 hello 및 링크를 통해 전달 되는 트래픽이 다른 링크 통과 반환 합니다. 이를 일반적으로 비대칭 라우팅이라고 합니다. 비대칭 라우팅에 역방향 네트워크 트래픽이 hello 원래 흐름에서 다른 경로 사용 합니다.

![여러 경로가 포함된 네트워크](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Hello 인터넷에서 주로 이루어지지만, 비대칭 라우팅도 경로가 여러 개 tooother 조합 적용 됩니다. 해당 예를 들어 tooan 인터넷 경로 toohello 이동 하는 전용 경로 모두 동일한 대상 및 toomultiple 개인 경로 toohello 이동 하는 동일한 대상입니다.

각 소스 toodestination에서 hello 방법 라우터 hello 최상의 경로 tooreach 대상을 계산합니다. hello 최상의 가능한 경로 라우터의 결정 기준으로 두 가지 주요 요소 합니다.

* 외부 네트워크 간의 라우팅은 BGP(경계 게이트웨이 프로토콜), 라우팅 프로토콜을 기반으로 합니다. BGP 광고 네트워크 환경에서 실행 하는 이러한 일련의 단계 toodetermine hello 최상의 경로 toohello 의도 한 대상입니다. 라우팅 테이블에 hello 최상의 경로 저장합니다.
* 경로와 연결 된 서브넷 마스크의 hello 길이 라우팅 경로 영향을 줍니다. 라우터 수신 하는 경우 동일한 IP 주소를 hello에 대 한 보급 알림이 여러 개 있지만 다른 서브넷 마스크와 hello 라우터 선호 서브넷 마스크는 긴 hello 광고는 보다 구체적인 경로 것으로 간주 하기 때문에 있습니다.

## <a name="stateful-devices"></a>상태 저장 장치
라우터 라우팅 용도로 패킷의 IP 헤더 hello 살펴봅니다. 일부 장치 hello 패킷에 깊은 확인합니다. 일반적으로 이러한 장치는 Layer4(전송 제어 프로토콜 또는 TCP; 또는 사용자 데이터그램 프로토콜 또는 UDP) 또는 심지어 Layer7(응용 프로그램 계층) 헤더를 확인합니다. 이러한 종류의 장치는 보안 장치 또는 대역폭 최적화 장치입니다. 

방화벽은 상태 저장 장치의 일반적인 예입니다. 방화벽을 허용 하거나 프로토콜, TCP/UDP 포트 및 URL 헤더와 같은 다양 한 필드를 기반으로 하는 인터페이스를 통해 패킷을 toopass를 거부 합니다. 이 수준의 패킷 검사 hello 장치에서 처리 부하가 넣습니다. tooimprove 성능 hello 방화벽 흐름의 첫 번째 패킷이 hello를 검사합니다. Hello 패킷 tooproceed, 허용 되는 경우 상태 테이블에 hello 흐름 정보를 유지 합니다. Hello 초기 결정에 따라 모든 후속 패킷이 관련된 toothis 흐름이 허용 됩니다. Hello 방화벽에서 패킷을 기존 흐름의 일부인 도착할 수 있습니다. Hello 방화벽에 대 한 이전 상태 정보가 없습니다 있으면 hello 방화벽 hello 패킷을 삭제 합니다.

## <a name="asymmetric-routing-with-expressroute"></a>Express 경로를 포함한 비대칭 라우팅
Azure ExpressRoute를 통해 tooMicrosoft를 연결 하면 네트워크 변경 내용을 다음과 같이:

* 여러 링크 tooMicrosoft 해야합니다. 하나의 링크가 기존 인터넷 연결을 있고 다른 hello ExpressRoute를 통해. 일부 트래픽 tooMicrosoft hello 인터넷을 통해 이동 수도 있지만 ExpressRoute를 통해 또는 그 반대로 돌아옵니다.
* Express 경로를 통해 구체적인 IP 주소를 수신합니다. 따라서 ExpressRoute를 통해 제공 되는 서비스에 대 한 네트워크 tooMicrosoft 프로그램에서 트래픽용 라우터 항상 선호 ExpressRoute 합니다.

toounderstand hello 효과 네트워크에 이러한 두 가지 변경가지고 몇 가지 시나리오를 생각해 봅시다. 예를 들어, 하나의 회로 toohello 인터넷 있고 hello 인터넷을 통해 모든 Microsoft 서비스를 사용 합니다. hello 트래픽만 네트워크 tooMicrosoft 및 뒤로 트래버스하여 같은 인터넷 연결과 hello 방화벽을 통해 전달 hello 합니다. hello 방화벽 레코드 hello 첫 번째 패킷이 게 표시 하 고 hello 흐름 hello 상태 테이블에 존재 하기 때문에 패킷 수를 반환 하는 대로 흐름을 hello 합니다.

![Express 경로를 포함한 비대칭 라우팅](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

그런 다음 Express 경로를 켜고 Express 경로를 통해 Microsoft에서 제공하는 서비스를 사용합니다. Microsoft의 다른 모든 서비스는 hello 인터넷을 통해 사용 됩니다. 연결 된 tooExpressRoute 있는 가장자리에 별도 방화벽을 배포 합니다. Microsoft는 특정 서비스에 대 한 ExpressRoute를 통해 더 구체적인 접두사 tooyour 네트워크를 알립니다. 라우팅 인프라 해당 접두사에 대 한 기본 경로 hello 서 express 경로 선택합니다. ExpressRoute를 통해 공용 IP 주소 tooMicrosoft 프로그램을 한 하지 배포 하는 경우 Microsoft hello 인터넷을 통해 공용 IP 주소와 통신 합니다. 네트워크 tooMicrosoft의 정방향 트래픽이 ExpressRoute를 사용 하 고 Microsoft에서 역방향 트래픽 인터넷 hello를 사용 합니다. Hello 상태 테이블에서 찾을 수 없는 하는 흐름에 대 한 응답 패킷의 인식 하는 hello 가장자리에 hello 방화벽 hello 반환 트래픽을 삭제 합니다.

Toouse hello 동일한 네트워크 주소 변환 (NAT) hello 인터넷 및 express 경로 대 한 풀을 선택 하면 개인 IP 주소에 네트워크의 hello 클라이언트와 유사한 문제를 표시 됩니다. 이러한 서비스에 대 한 IP 주소는 ExpressRoute를 통해 보급 하지 때문에 Windows 업데이트와 같은 서비스에 대 한 요청 hello 인터넷을 통해 이동 합니다. 그러나 hello 반환 트래픽을 ExpressRoute를 통해 반환 됩니다. Microsoft와 IP 주소를 수신 하는 경우 동일한 hello 인터넷에서에서 서브넷 마스크 및 ExpressRoute를 hello hello 인터넷을 통해 ExpressRoute를 선호 합니다. ExpressRoute 연결 및 네트워크 경계에 있는 다른 상태 저장 장치 또는 방화벽 hello 흐름에 대 한 이전 비워진 있으면 toothat 흐름 속하는 hello 패킷에 삭제 합니다.

## <a name="asymmetric-routing-solutions"></a>비대칭 라우팅 솔루션
비대칭 라우팅의 두 가지 기본 옵션 toosolve hello 문제가 있을 있습니다. 하나 라우팅을 통해 고 hello 다른 소스 기반 NAT (SNAT)를 사용 하는 것입니다.

### <a name="routing"></a>라우팅
공용 IP 주소 보급된 tooappropriate 광역 네트워크 (WAN) 링크 되는지 확인 합니다. 예를 들어 메일 사용량에 대 한 인증 트래픽 및 express 경로 대 한 인터넷 toouse hello를 원하는 ExpressRoute를 통해 Active Directory Federation Services (AD FS) 공용 IP 주소 하지 광고할 해야 있습니다. 마찬가지로, 반드시 온-프레미스에서 tooexpose 하지 ExpressRoute를 통해 라우터 hello AD FS 서버 tooIP 주소를 받습니다. ExpressRoute를 통해 받는 경로 보다 구체적인 않으므로 ExpressRoute hello에 대 한 인증 트래픽 tooMicrosoft 기본 경로 확인 합니다. 이렇게 하면 비대칭 라우팅이 생겨납니다.

인증을 위해 toouse ExpressRoute를 원하는 경우 NAT. 없이 ExpressRoute를 통해 AD FS는 공용 IP 주소 알릴 있는지 확인 이러한 방식으로 tooan 나타나고 Microsoft에서 제공 되는 트래픽 온-프레미스 AD FS 서버 ExpressRoute를 통해 이동 합니다. Hello 인터넷을 통해 hello 기본 경로 이기 때문에 고객 tooMicrosoft에서 반환 트래픽을 ExpressRoute를 사용 합니다.

### <a name="source-based-nat"></a>원본 기반 NAT
비대칭 라우팅 문제를 해결하는 다른 방법은 SNAT를 사용하는 것입니다. 예를 들어를 보급 하지 않았다면 hello 공용 IP 주소는 온-프레미스 SMTP Simple Mail Transfer Protocol () 서버의 ExpressRoute를 통해 이러한 유형의 통신에 대 한 인터넷 toouse hello 만들 예정 이므로 합니다. Microsoft와 시작 되 고 다음 tooyour를 이동 하는 요청을 온-프레미스 SMTP 서버 hello 인터넷 통과 합니다. 들어오는 요청 tooan 내부 IP 주소를 안녕 SNAT 있습니다. Hello SMTP 서버에서 역방향 트래픽을 toohello 경계 면 방화벽 (nat 사용)를 대신 ExpressRoute 통해 이동 합니다. hello 반환 트래픽은 hello 인터넷을 통해 다시 전송 됩니다.

![원본 기반 NAT 네트워크 구성](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>비대칭 라우팅 감지
Traceroute는 hello 가장 좋은 방법은 toomake 있는지 네트워크 트래픽을 예상 하는 hello 경로 트래버스하는입니다. 온-프레미스 SMTP 서버 tooMicrosoft tootake hello 인터넷 경로에서 트래픽이 예상 하는 경우 hello traceroute hello SMTP 서버 tooOffice 365에서에서가 필요 합니다. hello 결과 트래픽을 네트워크 hello 인터넷 한 ExpressRoute 하지 나온다는 실제로 것을 확인 합니다.

