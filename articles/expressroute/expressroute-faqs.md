---
title: "express 경로 FAQ aaaAzure | Microsoft Docs"
description: "express 경로 FAQ hello Azure 서비스 지원, 비용, 데이터 및 연결, SLA, 공급자 및 위치, 대역폭 및 추가 기술 세부 정보에 대 한 정보를 포함합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>ExpressRoute FAQ

## <a name="what-is-expressroute"></a>ExpressRoute란?

ExpressRoute는 온-프레미스 또는 공동 장소 환경의 Microsoft 데이터 센터와 인프라 사이에 개인 연결을 만들 수 있게 해 주는 서비스입니다. ExpressRoute 연결은 공용 인터넷 및 보안을 강화 하는 제품 신뢰성 hello 보다 내려가지 않는지, 속도와 일반 연결 보다 대기 시간이 hello 인터넷을 통해입니다.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>ExpressRoute 및 개인 네트워크 연결을 사용 하 여 hello 장점은 무엇입니까?

ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 보안, 안정성 및 속도 일관 된 대기 시간이 hello 인터넷을 통한 일반 연결 보다 더 높은 제공합니다. 경우에 따라 간에 ExpressRoute 연결 tootransfer 데이터를 사용 하 여 온-프레미스 장치 및 Azure 상당한 비용 혜택을 얻을 수 있습니다.

### <a name="where-is-hello-service-available"></a>Hello 서비스는 사용할 수 있는 어디 입니까?

서비스 위치 및 가용성은 [ExpressRoute 파트너 및 위치](expressroute-locations.md)페이지를 참조하세요.

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Hello ExpressRoute 통신 업체 중 하 나와 파트너 관계 없는 경우 tooconnect tooMicrosoft ExpressRoute를 사용 하는 방법

지역 통신 업체를 선택할 수 있으며 이더넷 연결 tooone 지원 hello exchange 공급자 위치를 배치 합니다. 그러면 hello 공급자 위치에서 microsoft 피어 링 수 있습니다. 마지막 부분 hello [express 경로 파트너 및 위치](expressroute-locations.md) toosee 서비스 공급자 hello exchange 위치 중 하나에 있는 경우. 그런 다음 서비스 공급자 tooconnect tooAzure hello 통해 ExpressRoute 회로 주문할 수 있습니다.

### <a name="how-much-does-expressroute-cost"></a>Express 경로 비용

가격 정보는 [가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 를 참조하세요.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>가 지정된 된 대역폭의 ExpressRoute 회로 내 네트워크 서비스 공급자 로부터 구매 하는 VPN 연결을 hello에 대 한 비용을 지불할 경우 toobe hello 동일한 속도?

아니요. 서비스 공급자로부터 모든 속도의 VPN 연결을 구입할 수 있습니다. 그러나 연결 tooAzure 제한 toohello ExpressRoute 회로 대역폭을 구입할 됩니다.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>비용을 지불할 경우 지정된 된 대역폭의 ExpressRoute 회로 필요에 따라 toohigher 속도를 hello 기능 tooburst 있습니까?

예. ExpressRoute 회로 구성 된 tooallow tootwo 시간 tooburst hello에 대 한 추가 비용 없이 확보 하는 대역폭 제한입니다. 이 기능을 지원 하는 경우 서비스 공급자 toosee 확인 하십시오.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>사용할 수 있습니까 hello 동일한 개인 가상 네트워크 및 기타 Azure 서비스와의 연결을 동시에 네트워크?

예. ExpressRoute 회로 한 번 설정 하면 가상 네트워크 내에서 tooaccess 서비스 및 다른 Azure 서비스가 동시에. 개인 피어 링 경로 hello 및 tooother 서비스를 통해 hello 공용 피어 링 경로 통해 toovirtual 네트워크를 연결합니다.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute는 SLA(서비스 수준 계약)을 제공하나요?

내용은 hello를 참조 하십시오. [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) 페이지.

## <a name="supported-services"></a>지원되는 서비스

ExpressRoute는 다양한 유형의 서비스에 대해 [세 개의 라우팅 도메인](expressroute-circuit-peerings.md)을 지원합니다.

### <a name="private-peering"></a>개인 피어링

* 모든 가상 컴퓨터 및 클라우드 서비스를 포함한 가상 네트워크

### <a name="public-peering"></a>공용 피어링

* Power BI
* Dynamics 365 for Finance and Operations(이전의 Dynamics AX Online)
* 대부분 hello Azure의 hello 다음 몇 가지 예외를 사용 하 여 서비스:
  * CDN
  * Visual Studio Team Services 부하 테스트
  * Multi-Factor 인증
  * Traffic Manager

### <a name="microsoft-peering"></a>Microsoft 피어링

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 Customer Engagement 응용 프로그램(이전의 CRM Online)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service

## <a name="data-and-connections"></a>데이터 및 연결

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>ExpressRoute를 사용 하 여 전송할 수 있습니까 하는 데이터 양 hello에 대 한 제한 사항이 있습니까?

Hello 데이터 전송 양에 대 한 제한의 설정 하지 마십시오 했습니다. 너무 참조[가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 대역폭 속도에 대 한 내용은 합니다.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>ExpressRoute에서 지원되는 연결 속도는 무엇인가요?

지원되는 대역폭은 다음을 제공합니다.

50Mbps, 100Mbps, 200Mbps, 500Mbps, 1Gbps, 2Gbps, 5Gbps, 10Gbps

### <a name="which-service-providers-are-available"></a>어떤 서비스 공급자를 사용할 수 있나요?

참조 [express 경로 파트너 및 위치](expressroute-locations.md) hello 목록은 서비스 공급자 및 위치입니다.

## <a name="technical-details"></a>기술 세부 정보

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>내 온-프레미스 위치 tooAzure 연결 하기 위한 hello 기술 요구 사항은 무엇입니까?

요구 사항은 [ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md)를 참조하세요.

### <a name="are-connections-tooexpressroute-redundant"></a>중복 연결 tooExpressRoute?

예. 각 ExpressRoute 회로 구성 된 연결 tooprovide 고가용성 크로스 중복 쌍 있습니다.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>내 ExpressRoute 링크 중 하나가 실패하면 연결이 끊어지나요?

한 경우 연결이 손실 되지 것입니다의 hello 교차 연결 실패 합니다. 네트워크의 사용 가능한 toosupport hello 부하 중복 연결이합니다. 또한 다른 피어 링 위치 tooachieve 오류 복구에 여러 회로 만들 수 있습니다.

### <a name="onep2plink"></a>클라우드 교환에서 같은 위치에 배치 하지 않겠습니다 내 서비스 공급자 지점 간 연결을 제공 하는 경우 내 온-프레미스 네트워크와 Microsoft tooorder 두 개의 실제 연결 해야 합니까?

서비스 공급자를 설정 하려면 두 이더넷 가상 회로 hello 물리적 연결을 통해 경우 하나의 실제 연결을 하면 됩니다. hello 물리적 연결 (예를 들어 광학 파이버)에서 종료 되는 계층 (L1) 장치 1 개 (hello 이미지 참조). hello 2 이더넷 가상 회로 hello 기본 회로 대 한 서로 다른 VLAN Id로 태그가 지정 하 고 보조 hello에 대 한 합니다. Hello 외부 802.1 q 이더넷 헤더에 해당 VLAN Id가 있습니다. hello 내부 802.1 q 이더넷 헤더 (표시 되지 않음)은 특정 매핑된 tooa [ExpressRoute 라우팅 도메인](expressroute-circuit-peerings.md)합니다.

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>확장할 수 있습니까 ExpressRoute를 사용 하 여 내 Vlan tooAzure 중?

아니요. Azure까지의 계층 2 연결 확장을 지원하지 않습니다.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>내 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있나요?

예. 사용자 구독에 둘 이상의 ExpressRoute 회로가 있을 수 있습니다. hello 기본 제한은 too10을 설정 됩니다. 필요한 경우 Microsoft 지원 tooincrease hello 제한을 문의할 수 있습니다.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>다른 서비스 공급자의 ExpressRoute 회로를 사용할 수 있나요?

예. 여러 서비스 공급자의 ExpressRoute 회로가 있을 수 있습니다. 각 ExpressRoute 회로마다 하나의 서비스 공급자와만 연결됩니다. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Hello에 여러 개의 ExpressRoute 회로 있을 수 같은 위치?

예. 동일 hello, 여러 개의 ExpressRoute 회로 라도 보유할 수 있습니다 또는 다른 서비스 공급자에서 동일한 위치를 환영 합니다. 그러나 둘 이상의 ExpressRoute 회로 toohello를 연결할 수 없습니다 동일한 가상 네트워크 hello에서 동일 위치 합니다.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>내 가상 네트워크 tooan ExpressRoute 회로 연결 어떻게 하나요

hello 기본 단계입니다.

* ExpressRoute 회로 설정 하 고 hello 서비스 공급자를 사용 하도록 설정 합니다.
* 또는 hello 공급자 hello BGP 피어 링 (s)를 구성 해야 합니다.
* Hello 가상 네트워크 toohello ExpressRoute 회로 연결 합니다.

자세한 내용은 [회로 프로비전 및 회로 상태에 대한 ExpressRoute 워크플로](expressroute-workflows.md)를 참조하세요.

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>내 ExpressRoute 회로에 대한 연결 경계가 있나요?

예. hello [express 경로 파트너 및 위치](expressroute-locations.md) 문서 ExpressRoute 회로 대 한 hello 연결 경계에 대 한 개요를 제공 합니다. ExpressRoute 회로 대 한 연결에는 제한 된 tooa 단일 지리적 영역입니다. 연결은 hello ExpressRoute premium 기능을 사용 하 여 확장 된 toocross 지리적 영역을 수 있습니다.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>ExpressRoute 회로 하나의 가상 네트워크 tooan 보다 toomore를 연결할 수 있습니까?

예. 표준 ExpressRoute 회로 too10 가상 네트워크 연결을 및 too100 드릴업에 있을 수 있습니다는 [프리미엄 ExpressRoute 회로](#expressroute-premium)합니다. 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>가상 네트워크를 포함하는 여러 Azure 구독을 가지고 있습니다. 별도 구독 tooa 단일 ExpressRoute 회로에 있는 가상 네트워크를 연결할 수 있습니까?

예. Too10를 권한을 부여할 수 있습니다 다른 Azure 구독에 단일 ExpressRoute 회로 toouse 합니다. Hello ExpressRoute premium 기능을 사용 하 여이 한도 늘릴 수 있습니다.

자세한 내용은 [여러 구독에서 ExpressRoute 회로 공유](expressroute-howto-linkvnet-arm.md)를 참조하세요.

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>각 가상 네트워크 연결 된 toohello 동일한 회로 격리?

아니요. 큐브 뷰, 모든 가상 네트워크 연결 된 toohello 라우팅에서 동일한 ExpressRoute 회로의 일부인 hello 동일한 라우팅 도메인 및 서로 분리 되지 않습니다. 격리를 라우팅할 필요한 별도 ExpressRoute 회로 toocreate를 해야 합니다.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>하나의 ExpressRoute 회로 보다 하나의 연결 된 가상 네트워크 toomore 있습니까?

예. Toofour ExpressRoute 회로를 단일 가상 네트워크와 연결할 수 있습니다. 4개의 다른 [ExpressRoute 위치](expressroute-locations.md)를 통해 순서를 지정해야 합니다.

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>내 가상 네트워크 연결 된 tooExpressRoute 회로에서 hello 인터넷에 액세스할 수 있습니까?

예. 기본 경로 (0.0.0.0/0) 또는 hello BGP 세션을 통해 인터넷 경로 접두사를 보급 하지 않았다면, 경우에 연결 된 가상 네트워크 tooan ExpressRoute 회로를 toohello 인터넷을 연결할 수 있습니다.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>인터넷 연결 toovirtual 네트워크 연결 된 tooExpressRoute 회로 차단할 수 있나요?

예. 기본 경로 (0.0.0.0/0) tooblock 모든 인터넷 연결 toovirtual 컴퓨터 가상 네트워크 내에 배포 되며 hello ExpressRoute 회로 통해 모든 트래픽을 밖 라우팅할 광고할 수도 있습니다.

기본 경로 보급 하는 경우 (예: Azure 저장소 및 SQL DB) 피어 링 공용 백 tooyour 프레미스를 통해 제공 되는 트래픽 tooservices를 수행 합니다. Tooconfigure hello 공용 피어 링 경로 통해 또는 hello 인터넷을 통해 프로그램 라우터 tooreturn 트래픽 tooAzure 해야 합니다.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>가상 네트워크에 연결 된 toohello 수 있습니다. 동일한 ExpressRoute 회로 통신 tooeach 다른?

예. 동일한 ExpressRoute 회로 서로 통신할 수 있는 연결 된 toohello를 가상 네트워크에 배포 된 가상 컴퓨터.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>ExpressRoute와 함께 가상 네트워크에 대한 사이트 간 연결을 사용할 수 있나요?

예. ExpressRoute는 사이트 간 VPN과 공존할 수 있습니다.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>사이트 간 / 지점 및 사이트 구성 toouse ExpressRoute에서에서 가상 네트워크를 이동할 수 있습니까?

예. 가상 네트워크 내에서 express 경로 게이트웨이 toocreate를 해야 합니다. Hello 프로세스와 관련 된 작은 가동 중지 시간이 있습니다.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>연결 된 가상 네트워크에 hello express 경로 게이트웨이 공용 IP 주소 있는 이유는 무엇입니까?

공용 IP 주소 hello만 내부 관리에 사용 됩니다. 이 공용 IP 주소 인터넷에 노출 된 toohello 아니며 가상 네트워크의 보안 노출을 것을 구성 하지 않습니다.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>무엇을 ExpressRoute를 통해 tooconnect tooAzure 저장소가 필요 합니까?

ExpressRoute 회로를 설정하고 공용 피어링에 대한 경로를 구성해야 합니다.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>보급할 수 있는 I 경로 hello 수에 대 한 제한 사항이 있습니까?

예. 개인 피어 링 용 경로 접두사 too4000와 각 200 공용 피어 링 및 Microsoft 피어 링에 대 한를 수락합니다. 이 too10 hello ExpressRoute 고급 기능을 사용 하는 경우 개인 피어 링 용 000 경로 늘릴 수 있습니다.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>I hello BGP 세션을 통해 보급할 수 있는 IP 범위에 대 한 제한 사항이 있습니까?

공용 hello 개인 접두사 (RFC1918) 및 Microsoft 피어 링 BGP 세션을 허용 하지 않습니다.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Hello BGP 제한을 초과한 경우 어떻게 되나요?

BGP 세션이 삭제됩니다. Hello 접두사 횟수가 hello 제한 아래로 되 면 재설정 됩니다.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Express 경로 BGP 보유 시간 hello 이란? 조정할 수 있나요?

hello 대기 시간은 180입니다. hello 연결 유지 메시지 60 초 마다 전송 됩니다. 설정은 변경할 수 없는 Microsoft의 hello에 수정이 되었습니다. Tooconfigure 다른 타이머 있습니다 되며 hello BGP 세션 매개 변수를 적절 하 게 협상 됩니다.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Hello 기본 경로 (0.0.0.0/0) toomy 가상 네트워크를 보급 I 후 Azure Vm 내에서 실행 되는 Windows를 활성화할 수 없습니다 I. 어떻게 tooI이 문제 해결?

단계를 수행 하는 hello Azure hello 정품 인증 요청을 인식 도움이 됩니다.

1. Hello 공용 피어 링 express 경로 회로 대 한 설정 합니다.
2. DNS 조회를 수행 하 고 hello IP 주소를 찾을 **kms.core.windows.net**
3. hello 키 관리 서비스 인식 해야 Azure와 honor hello에서 hello 정품 인증 요청에 해당 하는 요청입니다. Hello 다음 세 가지 작업 중 하나를 수행 합니다.

   * 온-프레미스 네트워크에 경로 hello 트래픽을 보내는 hello에 대 한 공용 피어 링 hello를 통해 백 tooAzure 2 단계에서에서 가져온 IP 주소 합니다.
   * 프로그램 NSP 공급자 머리 핀 hello 트래픽이 백 tooAzure hello 공용 피어 링을 통해 있어야 합니다.
   * 사용자 정의 경로 다음 홉으로 인터넷에 있는 해당 지점 hello IP를 만들고 이러한 가상 컴퓨터는 여기서 toohello ब 적용 합니다.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Hello 대역폭의 ExpressRoute 회로 변경할 수 있나요?

예, tooincrease hello 대역폭의 ExpressRoute 회로 hello Azure 포털 또는 PowerShell을 사용 하 여 시작할 수 있습니다. 회로가 만들어진 hello 실제 포트에 사용할 수 있는 용량이 있으면, 변경 내용을 성공 합니다. 

Hello 현재 포트에 남아 있는 충분 한 용량이 없는 고 toocreate hello 더 높은 대역폭을 새 ExpressRoute 회로 또는 해당 위치에서 추가 용량이 있는,이 경우 없게 필요 중 하나 있음을 의미 프로그램 변경에 실패 하는 경우 tooincrease hello 대역폭입니다. 

수 제공 됩니다 toofollow 연결 공급자 tooensure와 해당 네트워크 toosupport hello 대역폭 증가 내 hello 스로틀을 업데이트 합니다. 그러나 hello 대역폭의 ExpressRoute 회로 줄일 수는 없습니다. Toocreate 낮은 대역폭 새 ExpressRoute 회로 있고 hello 이전 회로 삭제 합니다.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Hello 대역폭의 ExpressRoute 회로 변경 하려면 어떻게 해야 합니까?

Hello hello REST API 또는 PowerShell cmdlet을 사용 하 여 hello ExpressRoute 회로 대역폭을 업데이트할 수 있습니다.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>ExpressRoute 프리미엄이란?

ExpressRoute premium에는 같은 기능 hello의 컬렉션입니다.

* 개인 피어 링 용 000 경로 4000 경로 too10에서 라우팅 테이블 한도 증가합니다.
* 연결 된 toohello ExpressRoute 회로 될 수 있는 Vnet 수가 증가 (기본값은 10). 자세한 내용은 참조 hello [ExpressRoute 제한](#limits) 테이블입니다.
* 연결 tooOffice 365 및 Dynamics 365 합니다.
* Hello Microsoft 핵심 네트워크를 통해 전역 연결 합니다. 이제 한 지리적 지역의 VNet을 다른 지역의 ExpressRoute 회로와 연결할 수 있습니다.<br>
    **예제:**

    *  서유럽 tooan Silicon Valley에 만든 ExpressRoute 회로에 만든 VNet을 연결할 수 있습니다. 
    *  공용 피어 링 hello에 Silicon Valley에 회로에서 인도 서 부 유럽 예를 들어 SQL Azure에 연결할 수 있도록 다른 지리적 지역에서 접두사는 보급 합니다.


### <a name="limits"></a>개수 Vnet을 연결 하는 tooan ExpressRoute 회로 ExpressRoute premium을 사용 합니까?

hello 다음 표에서 보여 hello ExpressRoute 제한 및 express 경로 회로 당 Vnet의 hello 수 있습니다:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>ExpressRoute Premium을 사용하려면 어떻게 하나요?

ExpressRoute 프리미엄 기능 hello 기능을 사용 하는 경우 사용할 수 있습니다 및 hello 회로 상태를 업데이트 하 여 종료할 수 있습니다. 회로가 만들어질 때 ExpressRoute 프리미엄을 활성화 수 또는 hello REST API를 호출할 수 / PowerShell cmdlet.

### <a name="how-do-i-disable-expressroute-premium"></a>ExpressRoute Premium을 사용하지 않도록 하려면 어떻게 하나요?

ExpressRoute 프리미엄 hello REST API 또는 PowerShell cmdlet을 호출 하 여 해제할 수 있습니다. ExpressRoute premium을 사용 하지 않도록 설정 하기 전에 연결 요구 toomeet hello 기본 제한을 조정 했 있는지 확인 해야 합니다. Hello 기본도 넘어 확장 하면 사용률 hello 요청 toodisable ExpressRoute 프리미엄 실패 합니다.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>I 선택할 수 hello 프리미엄 기능 집합에서 원하는 hello 기능이 있습니까?

아니요. Hello 기능을 선택할 수 없습니다. ExpressRoute Premium을 켜면 모든 기능을 사용합니다.

### <a name="how-much-does-expressroute-premium-cost"></a>ExpressRoute Premium 비용

너무 참조[가격 정보](https://azure.microsoft.com/pricing/details/expressroute/) 비용에 대 한 합니다.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>납부 ExpressRoute 프리미엄에 대 한 또한 toostandard ExpressRoute 요금?

예. Express 경로 회로 요금과 hello 연결 공급자에 필요한 요금이 위에 ExpressRoute 프리미엄 요금이 부과 됩니다.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>Office 365 및 Dynamics 365에 대한 ExpressRoute

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>어떻게 만드나요 ExpressRoute 회로 tooconnect tooOffice 365 서비스 및 Dynamics 365?

1. 검토 hello [ExpressRoute 필수 구성 요소 페이지](expressroute-prerequisites.md) toomake hello 요구 사항을 충족 하는지 합니다.
2. 충족 하 고 연결 tooensure, 서비스 공급자 및 위치 hello에 hello 목록을 검토 [express 경로 파트너 및 위치](expressroute-locations.md) 문서.
3. [Office 365에 대한 네트워크 계획 및 성능 튜닝](http://aka.ms/tune/)을 검토하여 용량 요구 사항을 계획합니다.
4. 연결을 워크플로 tooset hello에에서 나열 된 hello 단계에 따라 [회선 프로비저닝 및 회선 상태에 대 한 express 경로 워크플로](expressroute-workflows.md)합니다.

> [!IMPORTANT]
> 연결 tooOffice 365 서비스 및 Dynamics 365 구성할 때 ExpressRoute premium 추가 기능을 설정 했는지 확인 합니다.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>해야 Azure tooenable tooconnect tooOffice 365 서비스와 Dynamics 365 피어 링 공용?

아니요, Microsoft 피어 링 tooenable만 필요 합니다. 인증 트래픽 tooAzure AD Microsoft 피어 링을 통해 전송 됩니다. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>연결 tooOffice 365 서비스 및 Dynamics 365 내 기존 express 경로 회로 지원할 수 있습니까?

예. 기존 express 경로 회로 구성 된 toosupport 연결 tooOffice 365 서비스 일 수 있습니다. 충분 한 용량 tooconnect tooOffice 365 서비스가 하며 premium 추가 기능을 설정 했는지 확인 합니다. [Office 365의 네트워크 계획 및 성능 조정](http://aka.ms/tune/)을 참조하면 연결 요구 사항을 계획할 수 있습니다. [ExpressRoute 회로 만들기 및 수정](expressroute-howto-circuit-classic.md)도 참조하세요.

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>ExpressRoute 연결을 통해 어느 Office 365 서비스에 액세스할 수 있나요?

너무 참조[Office 365 Url 및 IP 주소 범위](http://aka.ms/o365endpoints) ExpressRoute를 통해 지원 되는 서비스의 최신 목록에 대 한 페이지입니다.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Office 365 서비스 및 Dynamics 365용 ExpressRoute 비용은 얼마인가요?

Office 365 서비스와 Dynamics 365 premium 추가 기능 toobe 활성화 필요 합니다. Hello 참조 [가격 책정 세부 정보 페이지](https://azure.microsoft.com/pricing/details/expressroute/) 비용에 대 한 합니다.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Office 365용 ExpressRoute가 지원하는 영역

[ExpressRoute 파트너 및 위치](expressroute-locations.md)를 참조하세요.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>에 액세스할 수 Office 365 hello 인터넷을 통해 ExpressRoute 내 조직에 대해 구성 된 경우에?

예. Office 365 서비스 끝점은 네트워크에 대 한 express 경로 구성한 경우에 hello 인터넷을 통해 연결할 수 있는입니다. ExpressRoute 통해 구성 된 tooconnect tooOffice 365 서비스에 있는 위치에 있는 경우 ExpressRoute를 통해 연결 됩니다.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Azure 미국 정부 ExpressRoute 회로를 통해 Office 365 미국 정부 커뮤니티(GCC) 서비스에 액세스할 수 있나요?

예. Office 365 GCC 서비스 끝점은 Azure 미국 정부 ExpressRoute hello를 통해 연결할 수 있습니다. 그러나 하면 첫 번째 필요 tooopen 지원 티켓에 hello tooadvertise tooMicrosoft를 만들려는 경우 Azure 포털 tooprovide hello 접두사입니다. 사용자 연결 tooOffice 365 GCC 서비스는 hello 지원 티켓 해결 된 후 설정 됩니다. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>ExpressRoute 연결을 통해 Dynamics 365 for Operations(이전의 Dynamics AX Online)에 액세스할 수 있나요?

예. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations)가 Azure에서 호스팅됩니다. Azure 공용 피어 링 express 경로 회로 tooconnect tooit 프로그램에서 사용할 수 있습니다.

## <a name="route-filters-for-microsoft-peering"></a>Microsoft 피어링용 경로 필터

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>처음으로 hello에 대 한 피어 링 Microsoft 켜기, 어떤 경로 얼마나?

경로는 표시되지 않습니다. Tooattach는 경로 필터 tooyour 회로 toostart 접두사 알림을 만들어야합니다. 자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>필자는 Microsoft 피어 링에 있고 Exchange Online 동안 tooselect 저는 걸리지만 것은 me는 없는 권한이 부여 된 toodo 오류가 이제 것입니다.

경로 필터를 사용하면 모든 고객이 Microsoft 피어링을 설정할 수 있습니다. 그러나 Office 365 서비스를 사용 하 고에 대 한 보내야 tooget Office 365에 권한을 부여 합니다.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Microsoft 피어 링을 통해 Dynamics 365 켜는 tooget 권한 부여 필요 합니까?

아니요, Dynamics 365에 대해 권한을 부여받을 필요가 없습니다. 규칙을 만든 다음, 권한을 부여받지 않고 Dynamics 365 커뮤니티를 선택하면 됩니다.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Microsoft 피어링을 이미 사용하고 있습니다. 경로 필터를 사용하려면 어떻게 해야 하나요?

선택 hello 서비스를 toouse, 연결 hello 필터 tooyour Microsoft 피어 링, 경로 필터를 만들 수 있습니다. 자세한 내용은 [Microsoft 피어링용 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>이제 tooenable 려 한 위치에서 피어 링 하는 Microsoft가 다른 위치에서 모든 접두사가 표시 되지 않는 한 합니다.

* 이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다.

* Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다. 접두사는 기본적으로 표시되지 않습니다.
