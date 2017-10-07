---
title: "ExpressRoute 회로 대 한 요구 사항 aaaNAT | Microsoft Docs"
description: "이 페이지는 Express 경로 회로에 NAT를 구성하고 관리하는 자세한 요구 사항을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Express 경로 NAT 요구 사항
ExpressRoute를 사용 하 여 tooconnect tooMicrosoft 클라우드 서비스, tooset 필요한 하 Nat를 관리 합니다. 일부 연결 공급자는 NAT을 관리 서비스로 설치하고 관리해 줍니다. 이러한 서비스를 제공 하는 경우 연결 공급자 toosee 확인 하십시오. 파일이 없으면 아래에 설명 된 toohello 요구 사항을 준수 해야 합니다. 

검토 hello [express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md) 다양 한 라우팅 도메인 tooget hello의 개요 페이지입니다. toomeet hello 공용 IP 주소 요구 사항은 공용 Azure 및 Microsoft 피어 링에 대 한, 네트워크와 Microsoft 간에 NAT를 설정 하는 두는 것이 좋습니다. 이 섹션에서는 필요한 tooset hello NAT 인프라에 대 한 자세한 설명을 제공 합니다.

## <a name="nat-requirements-for-azure-public-peering"></a>Azure 공용 피어링에 대한 NAT 요구 사항
hello Azure 공용 피어 링 경로 있습니다 tooconnect tooall Azure에서 호스팅된 서비스를 공용 IP 주소를 통해 수 있습니다. 여기에 hello에 나열 된 서비스가 [ExpessRoute FAQ](expressroute-faqs.md) 및 isv Microsoft Azure에서 호스트 되는 모든 서비스입니다. 

> [!IMPORTANT]
> 연결 tooMicrosoft Azure 서비스에 공용 피어 링 항상 초기화 네트워크에서 Microsoft 네트워크 hello로 합니다. 따라서 세션 ExpressRoute를 통해 Microsoft Azure 서비스 tooyour 네트워크에서 시작 될 수 없습니다. 전송 된 패킷과 toothese Ip 보급 하려고 시도 하면 ´ ֲ ExpressRoute 대신 인터넷 hello 합니다.
> 

공용 피어 링에 트래픽이 tooMicrosoft Azure SNATed toovalid hello Microsoft 네트워크를 입력 하기 전까지 공용 IPv4 주소 여야 합니다. 아래 hello 그림 요구 사항 위에 toomeet hello를 hello NAT 수 설정 하는 방법의 한 높은 수준의 그림을 제공 합니다.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>NAT IP 풀 및 경로 광고
트래픽 hello 유효한 공용 IPv4 주소와 Azure 공용 피어 링 경로 입력 하는 있는지 확인 해야 합니다. Microsoft는 hello 국가별 라우팅 인터넷 레지스트리 (RIR) 또는 인터넷 라우팅 레지스트리 (IRR)에 대해 IPv4 NAT 주소 풀의 수 toovalidate hello 소유권 이어야 합니다. 확인을 대로 수행 됩니다 hello에 따라 번호와 겹치기 되 고 hello NAT. hello에 대 한 사용 되는 IP 주소 Toohello 참조 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md) 라우팅 레지스트리에 대 한 정보에 대 한 페이지입니다.

이 피어 링을 통해 보급 hello NAT IP 접두사 길이 hello 제한은 없습니다. Hello NAT 풀을 모니터링 하 고 NAT 세션 중단 하지는 확인 해야 합니다.

> [!IMPORTANT]
> NAT IP 풀 hello 보급 tooMicrosoft 보급된 toohello 인터넷 수 없습니다. 이 연결 tooother Microsoft 서비스 연결이 끊어집니다.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Microsoft 피어링에 대한 NAT 요구 사항
hello Microsoft 피어 링 경로 사용 하면 hello Azure 공용 피어 링 경로 통해 지원 되지 않는 tooMicrosoft 클라우드 서비스를 연결할 수 있습니다. Exchange Online, SharePoint Online, 비즈니스용 Skype를 및 Dynamics 365 등의 Office 365 서비스를 포함 하는 서비스의 hello 목록이 나타납니다. Microsoft는 hello Microsoft 피어 링에 toosupport 양방향 연결을 예상합니다. 전송 트래픽을 tooMicrosoft 클라우드 서비스 SNATed toovalid hello Microsoft 네트워크를 입력 하기 전까지 공용 IPv4 주소 여야 합니다. Microsoft 클라우드 서비스에서 전송 트래픽을 tooyour 네트워크 인터넷 가장자리 tooprevent SNATed 있어야 [비대칭 라우팅](expressroute-asymmetric-routing.md)합니다. 아래 hello 그림 어떻게 hello NAT 설정할 것인지 Microsoft 피어 링 용의 상위 수준 그림을 제공 합니다.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>대상이 지정 되었으며 네트워크 tooMicrosoft에서 생성 되는 트래픽
* 트래픽의 hello Microsoft 피어 링 경로 유효한 공용 IPv4 주소로 시작 하는 확인 해야 합니다. Microsoft는 hello hello 국가별 라우팅 인터넷 레지스트리 (RIR)에 대해 IPv4 NAT 주소 풀의 수 toovalidate hello 소유자 또는 인터넷 라우팅 레지스트리 (IRR) 이어야 합니다. 확인을 대로 수행 됩니다 hello에 따라 번호와 겹치기 되 고 hello NAT. hello에 대 한 사용 되는 IP 주소 Toohello 참조 [ExpressRoute 라우팅 요구 사항](expressroute-routing.md) 라우팅 레지스트리에 대 한 정보에 대 한 페이지입니다.
* IP 주소 사용 hello Azure 공용 피어 링 설정 하 고 다른 ExpressRoute 회로 hello BGP 세션을 통해 보급된 tooMicrosoft을 사용 하지 않아야 합니다. 이 피어 링을 통해 보급 hello NAT IP 접두사의 hello 길이에 제한이 있습니다.
  
  > [!IMPORTANT]
  > NAT IP 풀 hello 보급 tooMicrosoft 보급된 toohello 인터넷 수 없습니다. 이 연결 tooother Microsoft 서비스 연결이 끊어집니다.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>대상이 지정 되었으며 tooyour 네트워크 트래픽 Microsoft에서 생성
* 특정 시나리오에는 Microsoft tooinitiate 연결 tooservice 끝점 네트워크 내에서 호스트 해야 합니다. Office 365에서 네트워크에서 호스트 되는 연결 tooADFS 서버 hello 시나리오의 일반적인 예는 것입니다. 이러한 경우 hello Microsoft 피어 링에 네트워크에서 적절 한 접두사를 누수 해야 있습니다. 
* 네트워크 tooprevent 내에서 서비스 끝점에 대 한 인터넷 가장자리 hello에서 SNAT Microsoft 트래픽을 해야 [비대칭 라우팅](expressroute-asymmetric-routing.md)합니다. 대상 IP가 ExpressRoute를 통해 받은 경로와 일치하는 요청 **및 회신**은 항상 ExpressRoute를 통해 전송됩니다. Hello로 hello 인터넷을 통해 hello 요청을 수신 하는 경우 존재 비대칭 라우팅 ExpressRoute를 통해 보낸 회신 합니다. Hello 인터넷 가장자리에서 SNATing hello 들어오는 Microsoft 트래픽을 강제로 회신 트래픽이 백 toohello 인터넷 경계 면 hello 문제를 해결 합니다.

![Express 경로를 포함한 비대칭 라우팅](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>다음 단계
* Toohello 요구 사항에 대 한 참조 [라우팅](expressroute-routing.md) 및 [QoS](expressroute-qos.md)합니다.
* 워크플로 정보는 [Express 경로 회로 프로비전 워크플로 및 회로 상태](expressroute-workflows.md)를 참조하세요.
* Express 경로 연결을 구성합니다.
  
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md)
  * [라우팅 구성](expressroute-howto-routing-classic.md)
  * [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)

