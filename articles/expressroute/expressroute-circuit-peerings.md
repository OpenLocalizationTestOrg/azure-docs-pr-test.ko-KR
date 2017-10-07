---
title: "aaaAzure express 경로 회로 및 라우팅 도메인 | Microsoft Docs"
description: "이 페이지는 express 경로 회로 및 라우팅 도메인 hello에 대 한 개요를 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Express 경로 회로 및 라우팅 도메인
 주문 해야는 *ExpressRoute 회로* tooconnect 연결 공급자를 통해 온-프레미스 인프라 tooMicrosoft 프로그램입니다. 아래 hello 그림 WAN와 Microsoft 간의 연결의 논리적 표현을 제공합니다.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Express 경로 회로
*Express 경로 회로* 는 연결 공급자를 통한 온-프레미스 인프라와 Microsoft 클라우드 서비스 간의 논리적 연결을 나타냅니다. 여러 Express 경로 회로를 주문할 수 있습니다. 각 회로 수에 같거나 다른 지역 hello 및 다른 연결 공급자를 통해 연결 된 tooyour 프레미스 될 수 있습니다. 

ExpressRoute 회로 tooany 물리적 엔터티 매핑되지 않습니다. 회로는 서비스 키(S 키)라고 하는 표준 GUID를 통해 고유하게 식별됩니다. hello 서비스 키가 hello 뿐 Microsoft hello 연결 공급자와 사용자 사이 주고받는 정보입니다. hello s 키가 보안을 위해 암호. Express 경로 회로 및 hello 간에 1:1 매핑이 s 키입니다.

Toothree 독립적인 피어 링 최대 ExpressRoute 회로 보유할 수: Azure 공용, Azure 개인 큐 및 Microsoft 합니다. 각 피어링은 한 쌍의 독립 BGP 세션으로, 각각 고가용성을 위해 중복 구성됩니다. Express 경로 회로와 라우팅 도메인 사이에는 1:N(1 <= N <= 3) 매핑이 있습니다. Express 경로 회로는 Express 경로 회로마다 1개, 2개 또는 3개의 피어링을 모두 사용할 수 있습니다.

각 회로 (50mbps, 100mbps, 200mbps, 500mbps, 1gbps, 10gbps) 고정된 대역폭 고 매핑된 tooa 연결 공급자 및 피어 링 위치입니다. 선택한 hello 대역폭 hello 회로 대 한 모든 hello 피어 링 공유 됩니다. 

### <a name="quotas-limits-and-limitations"></a>할당량, 제한 및 제약 조건
모든 Express 경로 회로에는 기본 할당량 및 제한이 적용됩니다. Toohello 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md) 할당량에 대 한 최신 정보에 대 한 페이지입니다.

## <a name="expressroute-routing-domains"></a>Express 경로 라우팅 도메인
Express 경로 회로에는 Azure 공용, Azure 개인 및 Microsoft와 연결된 여러 라우팅 도메인이 있습니다. 라우터 쌍에 동일 하 게 구성 된 각 라우팅 도메인 hello (로드 공유 또는 액티브-액티브 구성) 고가용성에 대 한 합니다. Azure 서비스는 네트워크로 분류 *Azure 공용* 및 *Azure 전용* toorepresent hello IP 주소 지정 구성표입니다.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>개인 피어링
Azure 계산 서비스, 즉 가상 컴퓨터 (IaaS) 및 클라우드 서비스 (PaaS), 가상 네트워크 내에 배포 된 hello 개인 피어 링 도메인을 통해 연결 될 수 있습니다. 개인 피어 링 도메인 hello를 Microsoft Azure로 toobe 핵심 네트워크의 신뢰할 수 있는 확장으로 간주 됩니다. 핵심 네트워크 및 Azure Vnet(가상 네트워크) 간의 양방향 연결을 설정할 수 있습니다. 이 피어 링 toovirtual 컴퓨터를 연결 하 고 클라우드 서비스는 개인 IP 주소에서 직접 수 있습니다.  

둘 이상의 가상 네트워크 toohello 개인 피어 링 도메인을 연결할 수 있습니다. 검토 hello [FAQ 페이지](expressroute-faqs.md) 제한 및 제한 사항에 대 한 내용은 합니다. Hello를 방문할 수 있는 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md) 제한에 대 한 최신 정보에 대 한 페이지입니다.  Toohello 참조 [라우팅](expressroute-routing.md) 라우팅 구성에 대 한 자세한 정보에 대 한 페이지입니다.

### <a name="public-peering"></a>공용 피어링
Azure Storage, SQL 데이터베이스 및 웹사이트와 같은 서비스는 공용 IP 주소에 제공됩니다. Hello 공용 피어 링 라우팅 도메인을 통해, 클라우드 서비스의 Vip를 포함 하 여 공용 IP 주소에 호스팅된 tooservices 개인적으로 연결할 수 있습니다. Hello 공용 피어 링 도메인 tooyour DMZ를 연결 하 고 Azure tooall 연결 수를 통해 tooconnect 필요 없이 WAN에서 공용 IP 주소에서 서비스 hello 인터넷 합니다. 

연결 프로그램 WAN tooMicrosoft Azure에서에서 항상 초기화 서비스입니다. Microsoft Azure 서비스는이 라우팅 도메인을 통해 네트워크에 수 tooinitiate 연결 되지 않습니다. 수 tooconnect tooall Azure 공용 피어 링 활성화 되 면 됩니다 서비스입니다. म 없도록 tooselectively 선택 서비스 경로를 라우터에 보급할 것입니다. 접두사 tooyou hello에 피어 링이 통해 보급 म hello 목록을 검토할 수 있습니다 [Microsoft Azure 데이터 센터 IP 범위](http://www.microsoft.com/download/details.aspx?id=41653) 페이지. hello 페이지 매주 업데이트 됩니다.

사용자 네트워크 tooconsume 유일한 hello 경로 필요한 내에서 사용자 지정 경로 필터를 정의할 수 있습니다. Toohello 참조 [라우팅](expressroute-routing.md) 라우팅 구성에 대 한 자세한 정보에 대 한 페이지입니다. 

Hello 참조 [FAQ 페이지](expressroute-faqs.md) hello 공용 피어 링 라우팅 도메인을 통해 지원 되는 서비스에 대 한 자세한 내용은 합니다. 

### <a name="microsoft-peering"></a>Microsoft 피어링
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

연결 tooall hello Microsoft 피어 링을 통해 다른 Microsoft 온라인 서비스 (예: Office 365 서비스) 됩니다. Hello Microsoft 피어 링 라우팅 도메인을 통해 WAN 및 Microsoft 클라우드 서비스 간의 양방향 연결을 설정합니다. TooMicrosoft 클라우드 서비스 또는 연결 공급자가 소유 하는 공용 IP 주소에 대해서만 연결 해야 하 고 tooall hello 정의 된 규칙을 준수 해야 합니다. Hello 참조 [ExpressRoute 필수 구성 요소](expressroute-prerequisites.md) 자세한 내용을 보려면 페이지입니다.

Hello 참조 [FAQ 페이지](expressroute-faqs.md) 지원 되는 서비스에 대 한 정보, 비용 및 구성 세부 정보에 대 한 합니다. Hello 참조 [ExpressRoute 위치](expressroute-locations.md) hello 목록에 Microsoft 피어 링 지원 제공 하는 연결 공급자의 정보에 대 한 페이지입니다.

## <a name="routing-domain-comparison"></a>라우팅 도메인 비교
hello 표에서 hello 3 개의 라우팅 도메인을 비교합니다.

|  | **개인 피어링** | **공용 피어링** | **Microsoft 피어링** |
| --- | --- | --- | --- |
| **피어링당 지원되는 최대값 # 접두사** |기본적으로 4000, Express 경로 프리미엄으로 10,000 |200 |200 |
| **지원되는 IP 주소 범위** |WAN 내에서 모든 유효한 IPv4 주소. |사용자 또는 연결 공급자가 소유한 공용 IPv4 주소. |사용자 또는 연결 공급자가 소유한 공용 IPv4 주소. |
| **AS 번호 요구 사항** |개인 및 공용 AS 번호. 자신이 소유한 hello 공용 toouse 하나를 선택 하는 경우에 숫자입니다. |개인 및 공용 AS 번호. 하지만, 공용 IP 주소의 소유권을 증명해야 합니다. |개인 및 공용 AS 번호. 하지만, 공용 IP 주소의 소유권을 증명해야 합니다. |
| **라우팅 인터페이스 IP 주소** |RFC1918 및 공용 IP 주소 |공용 IP 라우팅 레지스트리에 등록된 tooyou을 해결합니다. |공용 IP 라우팅 레지스트리에 등록된 tooyou을 해결합니다. |
| **MD5 해시 지원** |예 |예 |예 |

ExpressRoute 회로의 일부로 tooenable 하나 이상의 hello 라우팅 도메인을 선택할 수 있습니다. 모든 hello 라우팅 도메인에 toohave를 선택할 수 있습니다 toocombine 하려는 경우 같은 VPN hello 단일 라우팅 도메인에 해당 합니다. 서로 다른 라우팅 도메인 비슷한 toohello 다이어그램에 해당를 전환할 수도 있습니다. hello 권장 하는 해당 개인 피어 링 연결 되었으며 직접 toohello 핵심 네트워크 hello 공용 이며 Microsoft 피어 링 링크는 연결 된 tooyour DMZ 구성 합니다.

Toohave 모든 세 피어 링 세션을 선택 하면 세 쌍의 BGP 세션 (각 피어 링 형식에 대 한 한 쌍) 있어야 합니다. hello BGP 세션 쌍에는 항상 사용 가능한 링크를 제공 합니다. 계층 2 연결 공급자를 통해 연결하는 경우, 사용자가 라우팅을 구성하고 관리합니다. Hello를 검토 하 여 자세히 알아볼 수 있습니다 [워크플로](expressroute-workflows.md) express 경로를 설정 합니다.

## <a name="next-steps"></a>다음 단계
* 서비스 공급자를 찾습니다. [Express 경로 서비스 공급자 및 위치](expressroute-locations.md)를 참조하세요.
* 모든 필수 조건이 충족되었는지 확인합니다. [Express 경로 필수 조건](expressroute-prerequisites.md)을 참조하세요.
* Express 경로 연결을 구성합니다.
  * [ExpressRoute 회로 만들기 및 관리](expressroute-howto-circuit-portal-resource-manager.md)
  * [ExpressRoute 회로에 대한 라우팅(피어링) 구성](expressroute-howto-routing-portal-resource-manager.md)

