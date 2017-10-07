---
title: "ExpressRoute 라우팅 최적화: Azure | Microsoft Docs"
description: "이 페이지는 Microsoft와 회사 네트워크 사이의 연결 방법을 toooptimize 라우팅 있으면 둘 이상의 ExpressRoute 회로 대 한 세부 정보를 제공 합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Express 경로 라우팅 최적화
ExpressRoute 회로 여러 개 있는 경우 둘 이상의 경로 tooconnect tooMicrosoft 해야 합니다. 결과적으로 만족 스 럽 지 라우팅 발생할 수 있습니다-즉, 트래픽이 걸릴 수 있습니다 더 긴 경로 tooreach Microsoft, 및 Microsoft tooyour 네트워크입니다. hello 긴 hello 네트워크 경로 hello hello 대기 합니다. 대기 시간은 응용 프로그램 성능 및 사용자 환경에 직접적인 영향을 줍니다. 이 문서는 이러한 문제를 설명 하 고 방법을 사용 하 여 라우팅 toooptimize hello 라우팅의 표준 기술을 설명 합니다.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>고객 tooMicrosoft에서 라우팅 만족 스 럽 지
예제를 hello 라우팅 문제를 자세히 검토를 보겠습니다. Hello 미국, 로스앤젤레스와 뉴욕에 각각 하나씩 두 개의 본사가 있다고 가정해 보겠습니다. 사무실은 고유한 백본 네트워크 또는 서비스 공급자의 IP VPN에 연결할 수 있는 WAN(광역 네트워크)에 연결됩니다. 두 개의 ExpressRoute 회로, 미국 서 부와 WAN hello에도 연결 되어 있는 미국 동부에 각각 하나씩 해야 합니다. 물론, 두 개의 경로 tooconnect toohello Microsoft 네트워크를 해야합니다. 이제 미국 서부와 동부 모두에서 Azure 배포(예: Azure App Service)가 있다고 가정해 보겠습니다. 의도 이므로 tooconnect 로스앤젤레스 tooAzure 미국 서 부에 있는 사용자 및 뉴욕 tooAzure 미국 동부에서에서 사용자가 최적의 경험에 대 한 Azure 서비스 근처에 있는 각 office access에서 사용자가 hello를 보급 하는 서비스 관리자. 그러나 hello 계획 hello 서 부 해안 사용자가 아니라 hello 동부 사용자에 대해 작동합니다. hello hello 문제의 원인은 hello 다음입니다. 각 ExpressRoute 회로에 म tooyou 모두 Azure 미국 동부의 (23.100.0.0/16) hello 접두사 및 보급 Azure 미국 서 부 (13.100.0.0/16)에서 hello 접두사입니다. 접두사는 어떤 영역에서 알 수 없는 경우 없는 수 tootreat 것 다르게 합니다. 미국 서 부 보다 자세히 tooUS 동부 이며 따라서 미국 동부의 모두 office 사용자 toohello ExpressRoute 회로 라우팅할 hello 접두사 둘 다 WAN 네트워크 생각할 수 있습니다. Hello 끝 hello 로스앤젤레스 사무실의에서 여러 불만이 생겼습니다 사용자가 해야 합니다.

![ExpressRoute 사례 1 문제-고객 tooMicrosoft에서 라우팅 만족 스 럽 지](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>해결 방법: BGP 커뮤니티 사용
toooptimize tooknow Azure 미국 동부에서 Azure 미국 서 부에서 어떤 접두사는 필요한 사용자 모두에 대 한 라우팅입니다. 이 정보는 [BGP 커뮤니티 값](expressroute-routing.md)을 사용하여 인코딩합니다. 예를 들어 고유 BGP 커뮤니티 값 tooeach Azure 지역 할당 되어 미국 동부는 "12076:51004"를, 미국 서부는 "12076:51006"을 할당했습니다. 이제 어떤 접두사가 어떤 Azure 지역의 것인지 알았으므로 어떤 Express 경로를 기본 설정할지 구성할 수 있습니다. Hello BGP tooexchange 라우팅 정보를 사용 하므로 BGP의 로컬 기본 설정 tooinfluence 라우팅을 사용할 수 있습니다. 예제에서는 미국 동부의 보다 미국 서 부에 더 높은 로컬 기본 설정 값 too13.100.0.0/16와 마찬가지로, 미국 서 부에 보다 미국 동부의 높은 로컬 기본 설정 값 too23.100.0.0/16를 할당할 수 있습니다. 이 구성 즉, 두 경로 tooMicrosoft을 사용할 수 로스앤젤레스에서 사용자가 걸립니다 hello ExpressRoute 회로 미국 서 부 tooconnect tooAzure 미국 서 부에에서 뉴욕에 있는 사용자 미국 동부 tooAzure 미국 동부에에서 hello ExpressRoute를 사용 하는 반면 있는지 확인 합니다. . 라우팅이 양쪽 모두에서 최적화됩니다. 

![ExpressRoute 사례 1 솔루션 - BGP 커뮤니티 사용](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> 동일한 기법을 로컬 기본 설정을 사용 하 여 hello, 고객 tooAzure 가상 네트워크에서에서 적용 된 toorouting 될 수 있습니다. म Azure tooyour 네트워크에서 보급 한 BGP 커뮤니티 값 toohello 접두사 태그를 지정 하지 않습니다. 그러나 가상 네트워크 배포 중 사무실 닫기 toowhich를 알고 있으므로 구성할 수 있습니다 라우터에서 적절 하 게 하나의 ExpressRoute 회로 tooanother tooprefer 합니다.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Microsoft toocustomer에서 라우팅 만족 스 럽 지
다음은 Microsoft에서 연결 어디로 긴 경로 tooreach 네트워크 또 다른 예입니다. 이 경우 [하이브리드 환경](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx)에서 온-프레미스 Exchange Server와 Exchange Online을 사용합니다. 사무실 연결된 tooa WAN 됩니다. 두 프로그램 사무실 tooMicrosoft hello 두 ExpressRoute 회로 통해 온-프레미스 서버 hello 접두사 알립니다. Exchange Online 사서함 마이그레이션 등의 경우에서 toohello 온-프레미스 서버 연결을 시작 합니다. 그러나 hello 연결 tooyour 로스앤젤레스 office hello 전체 continent 백 toohello 서 부 해안 통과 하기 전에 라우트된 toohello 미국 동부의 ExpressRoute 회로 않습니다. hello hello 문제의 원인은 비슷한 toohello 첫 번째 항목이 있습니다. 모든 힌트 없이 hello Microsoft 네트워크는 고객 접두사 닫기 tooUS 동부 이며 tooUS 서쪽 닫습니다는 어떤 것을 알 수 없습니다. 로스앤젤레스 toopick hello, 잘못 된 경로 tooyour office 자주 발생 합니다.

![ExpressRoute 사례 2-Microsoft toocustomer에서 라우팅 만족 스 럽 지](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>해결 방법: AS PATH 앞에 추가 사용
두 솔루션 toohello 문제가 있습니다. hello 먼저 하나는 단순히 로스앤젤레스 사무실, 미국 서 부에 hello ExpressRoute 회로에 177.2.0.0/31 온-프레미스 접두사를 보급할 온-프레미스 뉴욕 사무실, 177.2.0.2/31 미국 동부의 hello ExpressRoute 회로에 대 한 접두사입니다. 결과적으로, Microsoft tooconnect tooeach 사무실에 하나의 경로만이 있습니다. 최적화된 모호성과 라우팅이 없습니다. 이 디자인에서는 장애 조치 전략에 대 한 toothink이 필요 합니다. Hello에 이벤트를 통해 ExpressRoute 경로 tooMicrosoft hello 끊어지면 toomake Exchange Online 연결할 수 있는지 계속 tooyour 온-프레미스 서버를 해야 합니다. 

hello 두 번째 해결 방법은 tooadvertise hello 접두사의 두 ExpressRoute 회로에 계속 또한 제공 해 힌트는 접두사의 사무실 닫기 toowhich 하나입니다. BGP AS 경로 앞에 추가 지원 하므로 접두사 tooinfluence 라우팅에 대 한 hello AS 경로 구성할 수 있습니다. 이 예제에서는 우리는 것이 좋습니다 (으로 네트워크는 hello 경로 toothis 접두사 짧으면 hello 서쪽)이이 접두사에 대 한 대상으로 하는 트래픽에 대 한 미국 서 부에 hello ExpressRoute 회로 미국 동부의 172.2.0.0/31에 대 한 hello AS 경로 길게 할 수 있습니다. 마찬가지로 미국 동부의 hello ExpressRoute 회로 선호 합니다 म 있도록 172.2.0.2/31 미국 서 부에 대 한 hello AS 경로 길게 할 수 있습니다. 두 사무소 모두에 대해 라우팅이 최적화됩니다. 이 디자인에서 한 Express 경로 회로가 중단되면 Exchange Online에서 다른 Express 경로 회로 및 WAN을 통해 계속 연결할 수 있습니다. 

> [!IMPORTANT]
> Hello 접두사에 대 한 hello AS 경로에 숫자 Microsoft 피어 링에서 수신할 때 개인을 제거 합니다. Tooappend 필요한 AS 번호에 대 한 Microsoft 피어 링 AS 경로 tooinfluence 라우팅 hello에 공개 합니다.
> 
> 

![ExpressRoute 사례 2 솔루션 - AS PATH 접두사 사용](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Microsoft 및 공용 피어 링에 대 한 여기에 나와 hello 예 이지만,이 지원 hello hello 개인 피어 링에 대 한 동일한 기능입니다. 또한 하나의 단일 ExpressRoute 회로 hello 기본 및 보조 경로 tooinfluence hello 선택 영역 내에서 작동 hello AS 경로 앞에 추가 합니다.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>가상 네트워크 간에 최적이 아닌 라우팅
ExpressRoute를 가상 네트워크 tooVirtual 네트워크 ("VNet"이 라고도 함)을 사용할 수 있습니다 tooan ExpressRoute 회로 연결 하 여 통신 합니다. 연결할 때 해당 toomultiple ExpressRoute 회로 만족 스 럽 지 라우팅 hello Vnet 간의 발생할 수 있습니다. 예제를 살펴보겠습니다. 두 개의 ExpressRoute 회로가 하나는 미국 서부에, 하나는 미국 동부에 있습니다. 각 지역에는 두 개의 VNet이 있습니다. 웹 서버 하나 VNet에 배포 된 및 다른 응용 프로그램 서버 hello 합니다. 중복성을 링크 하면 각 지역 tooboth hello 로컬 ExpressRoute 회로에 두 개의 Vnet hello 하 고 원격 ExpressRoute 회로 hello 합니다. 아래 볼 수 있듯이 각 VNet에는 두 개의 경로 toohello 다른 VNet 있습니다. ExpressRoute 회로 로컬 고 어떤 단추가 원격 Vnet hello 알 수 없습니다. 따라서 tooload 균형 VNet 간 트래픽 라우팅 같은 비용-다중 경로 ECMP ()은 에서처럼 일부 트래픽 흐름은 hello 긴 경로 걸리며 hello 원격 ExpressRoute 회로에 라우팅됩니다.

![ExpressRoute 사례 3 - 가상 네트워크 간에 최적이 아닌 라우팅](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>높은 가중치 toolocal 연결을 할당 하는 해결 방법:
hello 솔루션은 간단 합니다. 여기서는 hello Vnet 및 hello 회로 알고 있으므로 각 VNet 높여야 경로 알 수 있습니다. 이 예제에 맞게 toohello 원격 연결 보다 더 높은 가중치 toohello 로컬 연결 할당 (hello 구성 예제에서는 참조 [여기](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). 선택 하면 VNet hello 가장 높은 가중치 toosend 트래픽이 해당 접두사의 대상이 hello 연결을 선호 하는 여러 연결에 다른 VNet의 hello hello 접두사를 받습니다.

![ExpressRoute 사례 3 솔루션-할당 높은 가중치 toolocal 연결](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> AS 경로 앞에 추가, 위의 hello 두 번째 시나리오에 설명 된 기술을 적용 하는 대신 연결의 hello 가중치를 구성 하 여 여러 개의 ExpressRoute 회로 설정한 경우 VNet tooyour 온-프레미스 네트워크에서 라우팅 적용할 수 있습니다. 각 접두사에 대해 항상 살펴보도록 하겠습니다 hello AS 경로 길이 하기 전에 hello 연결 가중치를 결정할 때 어떻게 toosend 트래픽입니다.
>
>
