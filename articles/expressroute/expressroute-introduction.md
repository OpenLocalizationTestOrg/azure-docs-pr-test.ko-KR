---
title: "ExpressRoute 개요: 개인 연결을 통해 온-프레미스 네트워크 tooAzure 확장 | Microsoft Docs"
description: "이 express 경로 기술 개요에서는 express 경로 연결 작동 원리 tooextend 온-프레미스 네트워크 tooAzure 개인 연결을 통해 설명 합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>ExpressRoute 개요
Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 통해 쉽게 처리 하는 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있습니다. ExpressRoute를 사용 등 Microsoft Azure, Office 365, Dynamics 365 연결 tooMicrosoft 클라우드 서비스를 설정할 수 있습니다.

공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다. ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다. 이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해. 방법에 대 한 내용은 tooconnect ExpressRoute를 사용 하 여 네트워크 tooMicrosoft 참조 [ExpressRoute 연결 모델](expressroute-connectivity-models.md)합니다.

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>주요 이점

* 계층 3 연결 하면 온-프레미스 네트워크와 연결 공급자를 통해 Microsoft 클라우드 hello 사이입니다. 임의의(IPVPN) 네트워크, 지점간 이더넷 연결, 이더넷 Exchange로 가상 간 연결을 통해 연결할 수 있습니다.
* Hello 지리적 지역에 모든 지역에 걸쳐 연결 tooMicrosoft 클라우드 서비스
* ExpressRoute premium 추가 기능으로 모든 지역에 걸쳐 전역 연결 tooMicrosoft 서비스입니다.
* 업계 표준 프로토콜을 통해 네트워크와 Microsoft 간의 동적 라우팅입니다.(BGP) 
* 높은 안정성을 위한 모든 피어링 위치의 기본 중복성입니다.
* 연결 가동 시간 [SLA](https://azure.microsoft.com/support/legal/sla/)입니다.
* 비즈니스용 Skype에 대한 QoS 지원.

자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.

## <a name="features"></a>기능

### <a name="layer-3-connectivity"></a>3계층 연결
Microsoft에서는 업계 표준 동적 라우팅 프로토콜 (BGP) tooexchange 공용 주소를 통해 인스턴스, Azure에서 온-프레미스 네트워크와 Microsoft 간에 라우팅합니다.  다른 트래픽 프로필에 네트워크를 사용하여 여러 BGP 세션을 설정합니다. 자세한 내용은 hello에서 확인할 수 있습니다 [express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md) 문서.

### <a name="redundancy"></a>중복
각 ExpressRoute 회로는 hello 연결 공급자에서 두 개의 연결 tootwo Microsoft Enterprise edge 라우터 (MSEEs) 구성 / 사용자 네트워크 가장자리입니다. Microsoft에서는 hello 연결 공급자에서 이중 BGP 연결 / 측면 – 하나의 tooeach MSEE 합니다. 중복 장치 하지 toodeploy를 선택할 수 있습니다 프로그램 끝 이더넷 회로 /입니다. 그러나 연결 공급자 연결 넘겨집니다 tooMicrosoft 중복 방식에서 중복 장치 tooensure를 사용 합니다. 중복 계층 3 연결 구성에 대 한 요구 사항은 우리의 [SLA](https://azure.microsoft.com/support/legal/sla/) toobe 유효 합니다.

### <a name="connectivity-toomicrosoft-cloud-services"></a>연결 tooMicrosoft 클라우드 서비스
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

ExpressRoute 연결 서비스를 다음 액세스 toohello 사용:

* Microsoft Azure 서비스
* Microsoft Office 365 서비스
* Microsoft Dynamics 365

Hello를 방문할 수 있는 [express 경로 FAQ](expressroute-faqs.md) 자세한 목록은 ExpressRoute를 통해 지원 되는 서비스에 대 한 페이지입니다.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>지리적 지역 내에서 연결 tooall 영역
TooMicrosoft 중 하나에 연결할 수 있습니다이 [피어 링 위치](expressroute-locations.md) 액세스 tooall 영역 hello 지리적 지역 내에 있어야 하 고 있습니다. 

예를 들어 암스테르담에서 tooMicrosoft ExpressRoute를 통해 연결한 있으면 유럽 북부 및 서 부 유럽에서 호스트 하는 액세스 tooall Microsoft 클라우드 서비스입니다. Hello 참조 [express 경로 파트너 및 피어 링 위치](expressroute-locations.md) hello 지리적 영역, 관련된 Microsoft 클라우드 영역 및 해당 express 경로 피어 링 위치에 대 한 개요 문서.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Express 경로 프리미엄 추가 기능으로 전역 연결
지리적 경계에 걸쳐 hello ExpressRoute 프리미엄 기능 tooextend 연결 추가 기능을 사용할 수 있습니다. 예를 들어 ExpressRoute 통해 암스테르담에 연결 된 tooMicrosoft 인 경우는 경우 액세스 tooall Microsoft 클라우드 서비스는 hello world를 통해 모든 지역에서 호스트 된 (national 클라우드 제외 됨). 남아메리카의 경우 나 오스트레일리아 hello 액세스할 때 동일한 방법으로 북쪽 hello 및 서 부 유럽 지역에 배포 된 서비스에 액세스할 수 있습니다.

### <a name="rich-connectivity-partner-ecosystem"></a>다양한 연결 파트너 에코시스템
Express 경로에서는 연결 공급자 및 SI 파트너의 에코시스템이 지속적으로 성장합니다. Toohello 참조할 수 있습니다 [ExpressRoute 공급자 및 위치](expressroute-locations.md) hello 최신 정보에 대 한 문서입니다.

### <a name="connectivity-toonational-clouds"></a>Toonational 클라우드에 연결
Microsoft는 특별한 지리학적 지역 및 고객 세그먼트에 격리된 클라우드 환경을 작동합니다. Toohello 참조 [ExpressRoute 공급자 및 위치](expressroute-locations.md) national 클라우드 및 공급자의 목록에 대 한 페이지입니다.

### <a name="bandwidth-options"></a>대역폭 옵션
다양한 범위의 대역폭에 대해 Express 경로 회로를 구입할 수 있습니다. 지원되는 대역폭 목록이 아래에 나열됩니다. 연결 공급자 toodetermine hello 목록의 지원 되는 대역폭을 제공 하는지 toocheck 수 있습니다.

* 50Mbps
* 100Mbps
* 200Mbps
* 500Mbps
* 1Gbps
* 2Gbps
* 5Gbps
* 10Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>대역폭의 동적 크기 조정
Hello ExpressRoute 회로 대역폭 (최상의 노력 방식)에 대 한 연결이 다운 tootear 필요 없이 늘릴 수 있습니다. 

### <a name="flexible-billing-models"></a>유연한 청구 모델
사용자에게 적합한 청구 모델을 선택할 수 있습니다. 아래에 나열 된 hello 청구 모델 간의 선택 합니다. 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.

* **무제한 데이터**입니다. ExpressRoute 회로 hello 월별 요금 청구 됩니다 및 모든 인바운드 및 아웃 바운드 데이터 전송 속도가 무료로 무료로 포함 합니다. 
* **데이터 요금**입니다. ExpressRoute 회로 hello 월별 요금 청구 됩니다. 모든 인바운드 데이터 전송은 무료로 제공됩니다. 아웃 바운드 데이터 전송은 데이터 전송량 GB 당 요금이 부과됩니다. 데이터 전송 속도는 지역에 따라 다릅니다.
* **Express 경로 프리미엄 추가 기능**입니다. hello ExpressRoute 프리미엄 hello ExpressRoute 회로 통해 추가 기능입니다. hello ExpressRoute premium 추가 기능 hello를 다음 기능을 제공 합니다. 
  * Azure 공용 및 Azure 개인 피어 링 용 경로 too10 4, 000, 000 경로에서 향상 된 경로 제한 합니다.
  * 서비스에 대한 전역 연결입니다. 모든 지역 (national 클라우드 제외)에서 만든 ExpressRoute 회로 hello world에서 다른 지역에 걸쳐 액세스 tooresources를 갖습니다. 예를 들어 서유럽에서 만든 가상 네트워크는 실리콘밸리에 프로비전된 Express 경로 회로를 통해 액세스될 수 있습니다.
  * Hello 회로의 hello 대역폭에 따라 10 tooa 큰 제한에서 express 경로 회로 당 VNet 링크의 횟수가 증가 합니다.

## <a name="faq"></a>FAQ

ExpressRoute에 대 한 자주 묻는 질문에 대 한 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.

## <a name="next-steps"></a>다음 단계

* [ExpressRoute 연결 모델](expressroute-connectivity-models.md)에 대해 알아봅니다.
* Express 경로 연결 및 라우팅 도메인에 대해 알아봅니다. [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.
* 서비스 공급자를 찾습니다. [Express 경로 파트너 및 피어링 위치](expressroute-locations.md)를 확인하세요.
* 모든 필수 조건이 충족되었는지 확인합니다. [ExpressRoute 필수 조건](expressroute-prerequisites.md)을 참조하세요.
* Toohello 요구 사항에 대 한 참조 [라우팅](expressroute-routing.md), [NAT](expressroute-nat.md), 및 [QoS](expressroute-qos.md)합니다.
* ExpressRoute 연결을 구성합니다.
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md)
  * [ExpressRoute 회로의 피어링 구성](expressroute-howto-routing-portal-resource-manager.md)
  * [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-portal-resource-manager.md)
* 일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.
