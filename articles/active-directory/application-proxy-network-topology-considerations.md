---
title: "Azure Active Directory 응용 프로그램 프록시를 사용 하는 경우 aaaNetwork 토폴로지 고려 사항 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항을 다룹니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Azure Active Directory 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항

이 문서에서는 응용 프로그램을 원격으로 게시 및 액세스하기 위해 Azure AD(Azure Active Directory) 응용 프로그램 프록시를 사용할 때 네트워크 토폴로지 고려 사항을 설명합니다.

## <a name="traffic-flow"></a>트래픽 흐름

응용 프로그램은 Azure AD 응용 프로그램 프록시를 통해 게시 되 면 트래픽 hello 사용자 toohello 응용 프로그램에서 3 개의 연결을 통해 전달 됩니다.

1. hello 사용자가 Azure에서 toohello Azure AD 응용 프로그램 프록시 서비스 공용 끝점 연결
2. 응용 프로그램 프록시 서비스 hello toohello 응용 프로그램 프록시 커넥터 연결
3. hello 응용 프로그램 프록시 커넥터 toohello 대상 응용 프로그램에 연결

![사용자 tootarget 응용 프로그램에서 트래픽 흐름을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>테넌트 위치 및 응용 프로그램 프록시 서비스

Azure AD 테 넌 트에 가입 하면 테 넌 트의 hello 영역 지정 hello 국가별로 결정 됩니다. 테 넌 트에 대 한 hello 응용 프로그램 프록시 서비스 인스턴스는 선택 하거나 동일한 hello에서 만든 응용 프로그램 프록시를 사용 하도록 설정 하면 Azure AD 테 넌 트 또는 가장 가까운 지역 tooit hello와 지역입니다.

예를 들어, EU (유럽 연합) hello Azure AD 테 넌 트의 영역을 사용 하는 경우 모든 응용 프로그램 프록시 커넥터 hello EU에서에서 Azure 데이터 센터에서 서비스 인스턴스를 사용 합니다. 사용자가 액세스 응용 프로그램을 게시할 때는 트래픽을이 위치에 hello 응용 프로그램 프록시 서비스 인스턴스를 거칩니다.

## <a name="considerations-for-reducing-latency"></a>대기 시간 단축을 위한 고려 사항

모든 프록시 솔루션은 네트워크 연결에 대기 시간을 발생시킵니다. 프록시 또는 VPN 솔루션을 설정 하면 원격 액세스 솔루션으로에 관계 없이 항상 지 원하는 서버 hello 연결 tooinside 회사 네트워크의 집합을 포함 합니다.

조직은 일반적으로 자신의 경계 네트워크에 서버 끝점을 포함합니다. 그러나 Azure AD 응용 프로그램 프록시 트래픽 흐름 hello 클라우드에서 hello 프록시 서비스를 통해 hello 커넥터 회사 네트워크에 있는 동안 합니다. 경계 네트워크는 필요하지 않습니다.

hello 다음 섹션에는 대기 시간을 더욱 줄일 추가 제안 toohelp을 포함 합니다. 

### <a name="connector-placement"></a>커넥터 배치

응용 프로그램 프록시는 테 넌 트의 현재 위치에 따라 인스턴스 hello 위치를 선택 합니다. 그러나 얻게 toodecide tooinstall hello 커넥터를 제공 전원 toodefine hello 대기 시간 특징의 네트워크 트래픽 hello 위치.

Hello 응용 프로그램 프록시 서비스를 설정할 때 다음 질문 hello를 요청 합니다.

* Hello 앱 어디에 있습니까?
* 대부분의 사용자가 있는 hello 앱에 액세스 하는 어디 입니까?
* Hello 응용 프로그램 프록시 인스턴스 어디에 있습니까?
* 이미 Azure express 경로 또는 유사한 VPN과 같은 설정 하는 전용된 네트워크 연결 tooAzure 센터?

hello 커넥터와가 모두 Azure 응용 프로그램 (2 단계와 3 단계에서 hello 트래픽 흐름 다이어그램) toocommunicate, 하므로 hello 커넥터 영향을 줌 hello 대기 시간의 두 가지 연결의 배치를 hello 지정 됩니다. Hello 커넥터의 hello 배치를 평가할 때는 유의 hello 지점 다음에 유의 하십시오.

* Single sign on에 대 한 Kerberos 제한 위임 toouse KCD ()를 원하는 경우 hello 커넥터 시야 tooa 데이터 센터가 필요 합니다. 또한 hello 커넥터 서버 toobe 도메인에 가입 되어 있어야 합니다.  
* 의심에서 hello 커넥터 자세히 toohello 응용 프로그램을 설치 합니다.

### <a name="general-approach-toominimize-latency"></a>일반적인 방법 toominimize 대기 시간

각 네트워크 연결을 최적화 하 여 hello 종단 간 트래픽의 hello 대기 시간을 최소화할 수 있습니다. 각 연결은 다음을 통해 최적화할 수 있습니다.

* Hello 홉의 양쪽 hello hello 간격을 줄입니다.
* 적합 한 네트워크 tootraverse hello를 선택 합니다. 예를 들어 hello 아닌 개인 네트워크를 통과 공용 인터넷 빠를 수 있습니다, 때문 toodedicated 링크.

회사 네트워크와 Azure 간 VPN 또는 express 경로 전용된 링크를 설정한 경우 toouse입니다.

## <a name="focus-your-optimization-strategy"></a>최적화 전략에 집중

거의 사용자와 응용 프로그램 프록시 서비스 hello 간의 toocontrol hello 연결을 수행할 수 있습니다. 사용자는 홈 네트워크, 인터넷 카페 또는 다른 국가에서 앱에 액세스할 수 있습니다. 대신, hello 응용 프로그램 프록시 서비스 toohello 응용 프로그램 프록시 커넥터 toohello 앱의 hello 연결을 최적화할 수 있습니다. 사용자 환경에서 패턴을 따른 hello를 통합 하는 것이 좋습니다.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>패턴 1: Put hello 커넥터 닫기 toohello 응용 프로그램

현재 위치 hello 커넥터 닫기 toohello에서에서 대상 응용 프로그램 hello 고객 네트워크입니다. 이 구성은 hello 커넥터와 응용 프로그램 닫기 있으므로 hello 토폴로지 다이어그램에서 3 단계를 최소화 합니다. 

커넥터 시야 toohello 도메인 컨트롤러를 필요한 경우이 패턴은 것이 좋습니다. 대부분의 시나리오에 적합하기 때문에 대부분의 고객이 이 패턴을 사용합니다. 이 패턴 hello 서비스 사이 hello 커넥터 패턴 2 toooptimize 트래픽을와 함께 사용할 수도 있습니다.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>패턴 2: 공용 피어링이 있는 ExpressRoute 활용

ExpressRoute를 사용 하 여 공용 피어 링 설정를 설정한 경우에 응용 프로그램 프록시 커넥터 hello 사이의 트래픽에 대 한 hello 더 빠른 ExpressRoute 연결을 사용할 수 있습니다. 닫기 toohello 응용 프로그램 네트워크에 여전히 hello 커넥터는입니다.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>패턴 3: 개인 피어링이 있는 ExpressRoute 활용

Azure 및 회사 네트워크 간에 개인 피어링이 있는 전용 VPN 또는 ExpressRoute를 설정한 경우 다른 옵션이 있습니다. 이 구성에서는 Azure의 hello 가상 네트워크 hello 회사 네트워크의 확장 기능으로 일반적으로 간주 됩니다. 따라서 hello Azure 데이터 센터에에서 hello 커넥터를 설치 하 고 여전히 hello 커넥터 응용 프로그램 연결의 hello 짧은 대기 시간 요구 사항을 충족 수 있습니다.

트래픽은 전용 연결을 통해 전송되므로 대기 시간에 나쁜 영향을 주지 않습니다. 또한 hello 커넥터 Azure 데이터 센터 닫기 tooyour Azure AD 테 넌 트 위치에에서 설치 되어 향상 된 응용 프로그램 프록시 커넥터에 서비스 대기 시간을 가져옵니다.

![Azure 데이터 센터 내에 설치된 커넥터를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>다른 방법

이 문서의 hello 핵심은 커넥터 배치를 hello 응용 프로그램 tooget 더 나은 대기 시간 특성의 hello 배치를 변경할 수도 있습니다.

조직은 더욱 더 네트워크를 호스티드 환경으로 이동하고 있습니다. 이렇게 하면 사용자 tooplace 자신의 회사 네트워크의 일부 이기도 고 여전히 hello 도메인 내에서 호스트 된 환경에서 응용 프로그램입니다. 이 경우 hello 이전 섹션에서에서 설명한 hello 패턴에 적용 된 toohello 새 응용 프로그램 위치 수 있습니다. 이 옵션을 고려하는 경우 [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md)를 참조하세요.

또한, 커넥터를 사용 하 여 구성 고려 [커넥터 그룹](active-directory-application-proxy-connectors.md) 다른 위치와 네트워크에 있는 tootarget 앱입니다. 

## <a name="common-use-cases"></a>일반 사용 예

이 섹션에서는 몇 가지 일반적인 시나리오를 살펴봅니다. Azure AD 테 넌 트 해당 hello 가정 (및 그에 따른 프록시 서비스 끝점) hello United States (US)에 있습니다. hello 설명에서 이러한 고려 사항을 사용 사례 hello 전 세계 tooother 영역에도 적용 합니다.

이러한 시나리오에서는 각 연결을 "홉"으로 지칭하고 보다 쉬운 이해를 위해 번호를 매깁니다.

- **1 홉**: 사용자 toohello 응용 프로그램 프록시 서비스
- **2 홉**: 응용 프로그램 프록시 서비스 toohello 응용 프로그램 프록시 커넥터
- **3 홉**: 응용 프로그램 프록시 커넥터 toohello 대상 응용 프로그램 

### <a name="use-case-1"></a>사용 사례 1

**시나리오:** hello 앱은 hello에서 조직의 네트워크에서 US, hello에 있는 사용자와 동일한 지역입니다. Express 경로 또는 VPN 없습니다 hello Azure 데이터 센터 및 회사 네트워크 hello 사이 있습니다.

**권장 사항:** 수행 패턴 1, hello 이전 섹션에서 설명 합니다. 대기 시간 개선을 위해 필요한 경우 ExpressRoute를 사용하는 것이 좋습니다.

이것은 단순한 패턴입니다. Hello 커넥터 hello 앱 근처에 배치 하 여 3 홉을 최적화 합니다. 일반적으로 hello 커넥터 시야 toohello 앱과 toohello datacenter tooperform KCD 작업에 설치 되어 있으므로 자연 스러운 선택 이기도 합니다.

![사용자, 프록시, 커넥터 및 응용 프로그램은 모두 hello US를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>사용 사례 2

**시나리오:** hello 앱은 hello에서 조직의 네트워크에서 US, 전역적으로 분산 된 사용자와 합니다. Express 경로 또는 VPN 없습니다 hello Azure 데이터 센터 및 회사 네트워크 hello 사이 있습니다.

**권장 사항:** 수행 패턴 1, hello 이전 섹션에서 설명 합니다. 

다시 hello 일반적인 방법은 toooptimize 홉 3, hello 커넥터 hello 앱 근처에 배치 하는 위치입니다. 홉 3 일반적으로 비용이 많이 들지 않습니다, 내에서 동일한 hello 경우 영역입니다. 그러나 hello 전 세계 사용자 hello 미국에서에서 hello 응용 프로그램 프록시 인스턴스에 액세스 해야 하기 때문에 1 홉 hello 사용자가 인지에 따라 비용이 수 있습니다. 모든 프록시 솔루션은 전 세계에 분산된 사용자에 따라 유사한 특성을 포함한다는 것에 주목해야 합니다.

![사용자가 전역으로 분산 되어 하지만 hello 프록시 커넥터를 앱에에서는, 및 hello US를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>사용 사례 3

**시나리오:** hello에서 조직 네트워크의 hello 앱은 US입니다. 회사 네트워크를 Azure와 hello 사이 공용 피어 링 express 경로 있습니다.

**권장 사항:** 1 및 2를 hello 이전 섹션에서 설명한 패턴을 따릅니다.

먼저, 가능한 toohello 응용 프로그램으로 가까운 hello 커넥터를 배치 합니다. 그런 다음 hello 시스템 홉 2에 대 한 express 경로 자동으로 사용 합니다. 

Hello ExpressRoute 연결을 사용 하는 공용 피어 링 하는 경우 해당 링크를 통해 hello 트래픽 hello 프록시와 hello 커넥터 간에 이동 합니다. 홉 2는 대기 시간을 최적화하게 됩니다.

![Hello 프록시 사이의 커넥터 express 경로 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>사용 사례 4

**시나리오:** hello에서 조직 네트워크의 hello 앱은 US입니다. 회사 네트워크를 Azure와 hello 사이 개인 피어 링 express 경로 있습니다.

**권장 사항:** 수행 패턴 3, hello 이전 섹션에서 설명 합니다.

Hello 커넥터 hello 개인 피어 링 express 경로 통해 연결 된 toohello 회사 네트워크를 Azure 데이터 센터에에서 배치 합니다. 

hello 커넥터 hello Azure 데이터 센터에에서 배치할 수 있습니다. Hello 커넥터 여전히에 있으므로 시야 toohello 응용 프로그램 및 hello 개인 네트워크를 통해 데이터 센터 hello 홉 3 최적화 된 상태로 유지 됩니다. 또한 홉 2는 더욱 최적화됩니다.

![Hello 커넥터와 응용 프로그램 간에 Azure 데이터 센터 및 express 경로에 hello 커넥터를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>사용 사례 5

**시나리오:** hello 응용 프로그램 프록시 인스턴스와 사용자가 대부분 hello 사용 하 여 hello EU에서에서 조직 네트워크의 hello 앱은 US입니다.

**권장 사항:** hello 앱 가까운 곳 hello 커넥터입니다. 미국 사용자가 toobe hello에서 발생 하는 응용 프로그램 프록시 인스턴스를 액세스 하기 때문에 동일한 지역 홉 1 가격이 너무 비쌉니다. 홉 3이 최적화됩니다. ExpressRoute toooptimize 홉 2를 사용 하는 것이 좋습니다. 

![Hello, 미국 hello 커넥터와 hello EU에서에서 응용 프로그램에서에서 사용자와 프록시를 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

이 상황에서 다른 한 가지 변수를 사용하도록 고려할 수 있습니다. 대부분 조직의 사용자에 게 hello에 있는 경우 hello 우리 가능성을 네트워크 확장 toohello US도 합니다. Hello, 미국에에서 hello 커넥터를 배치 하 고 hello EU 전용 hello 내부 회사 네트워크 줄 toohello 응용 프로그램 사용 합니다. 이 방식으로 홉 2와 3이 최적화됩니다.

![Hello 미국, 유럽 hello에서 응용 프로그램에서에서 사용자, 프록시 및 연결선을 보여 주는 다이어그램](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>다음 단계

- [응용 프로그램 프록시 사용](active-directory-application-proxy-enable.md)
- [Single Sign-On 사용](active-directory-application-proxy-sso-using-kcd.md)
- [조건부 액세스 사용](active-directory-application-proxy-conditional-access.md)
- [응용 프로그램 프록시에서 발생한 문제 해결](active-directory-application-proxy-troubleshoot.md)
