---
title: "어떻게 tooconfigure (피어 링)에 대 한 라우팅 ExpressRoute 회로: 리소스 관리자: Azure | Microsoft Docs"
description: "이 문서를 만들고 hello private, public 및 Microsoft 피어 링 express 경로 회로 프로 비전에 대 한 hello 단계를 안내 합니다. 또한이 문서를 보면 toocheck hello 상태 업데이트 또는 회로 대 한 피어 링 삭제 방법을 알 수 있습니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>ExpressRoute 회로의 피어링 만들기 및 수정

이 문서를 사용 하 여 만들고 hello Azure 포털을 사용 하 여 hello 리소스 관리자를 배포 하는 모델의 ExpressRoute 회로 대 한 라우팅 구성을 관리할 수 있습니다. Hello 상태, 업데이트 또는 삭제를 확인 하 고 피어 링 express 경로 회로 대 한 프로 비전을 해제할 수도 있습니다. 다른 방법 toowork toouse 회로 사용 하려는 경우 hello 다음 목록에서에서 아티클을 선택 합니다.


## <a name="configuration-prerequisites"></a>필수 구성 요소

* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md) 페이지 hello [라우팅 요구 사항](expressroute-routing.md) 페이지 및 hello [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에 페이지입니다.
* 활성화된 Express 경로 회로가 있어야 합니다. 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 계속 hello 회로 하기 전에 연결 공급자가 사용 하도록 설정 합니다. ExpressRoute 회로 hello hello 다음 섹션의 toobe 수 toorun hello cmdlet을 가능 하 고 프로 비전 된 상태에 있어야 합니다.
* Toouse 공유 키/MD5 해시를 사용 하도록 하려는 경우 수 있는지 toouse이 문자 tooa 최대 25의 hello 터널 및 제한 hello 번호의 양쪽 모두에 있습니다.

이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IPVPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다. 

> [!IMPORTANT]
> 에서는 현재 보급 되지 않고 피어 링 hello 서비스 관리 포털을 통해 서비스 공급자가 구성 합니다. 이 기능을 곧 사용할 수 있도록 개발 중입니다. BGP 피어링을 구성하기 전에 서비스 공급자에게 확인하세요.
> 
> 

ExpressRoute 회로에 한 가지, 두 가지 또는 세 가지 피어링을 구성할 수 있습니다.(개인, Azure 공용 Azure 및 Microsoft) 선택한 순서로 피어링을 구성할 수 있습니다. 그러나 한 번에 하나씩 피어 링의 hello 구성을 완료 되었는지 확인 해야 합니다.

## <a name="azure-private-peering"></a>Azure 개인 피어링

이 섹션을 사용 하면 만들기, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 개인 피어 링 구성을 Azure 있습니다.

### <a name="toocreate-azure-private-peering"></a>Azure 개인 피어 링 toocreate

1. Hello ExpressRoute 회로 구성 합니다. 계속 하기 전에 hello 회로 hello 연결 공급자에 의해 제공 완벽 하 게 되 확인 합니다.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Azure 개인 피어 링 hello 회로 대 한 구성 합니다. Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. hello 서브넷에 가상 네트워크에 대 한 예약 된 모든 주소 공간의 일부가 아니어야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다. 이 피어링에 개인 AS 숫자를 사용할 수 있습니다. 65515를 사용하지 않는지 확인합니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.
3. 다음 예제는 hello와 같이 hello Azure 개인 피어 링 행을 선택 합니다.

  ![개인](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. 개인 피어링을 구성합니다. 다음 이미지는 hello 구성 예를 보여 줍니다.

  ![개인 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. 모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다. Hello 구성이 성공적으로 수락 하는 후에 다음 예제는 다음과 유사한 toohello를 표시 됩니다.

  ![개인 피어링 저장](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>세부 정보를 피어 링 개인 Azure tooview

Azure 개인 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.

![개인 피어링 보기](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 개인 피어 링 구성

피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.

![개인 피어링 업데이트](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>Azure 개인 피어 링 toodelete

Hello 다음 이미지와 같이 hello 삭제 아이콘을 선택 하 여 피어 링 구성을 제거할 수 있습니다.

![개인 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Azure 공용 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Azure 공용 피어 링 구성이 있습니다.

### <a name="toocreate-azure-public-peering"></a>Azure 공용 피어 링 toocreate

1. ExpressRoute 회로를 구성합니다. Hello 회로 완벽 하 게 비전 되도록 hello 연결 공급자가 추가 되었는지를 확인 합니다.

  ![공용 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Azure 공용 피어 링 hello 회로 대 한 구성 합니다. Hello 다음 단계를 진행 하기 전에 다음 항목 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. 유효한 공용 IPv4 접두사여야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.
3. 다음 이미지는 hello와 같이 hello Azure 공용 피어 링 행을 선택 합니다.

  ![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. 공용 피어링을 구성합니다. 다음 이미지는 hello 구성 예를 보여 줍니다.

  ![공용 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. 모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다. Hello 구성이 성공적으로 수락 하는 후에 다음 예제는 다음과 유사한 toohello를 표시 됩니다.

  ![공용 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>세부 정보를 피어 링 공용 Azure tooview

Azure 공용 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.

![공용 피어 링 속성 보기](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 공용 피어 링 구성

피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.

![공용 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>Azure 공용 피어 링 toodelete

다음 예제는 hello와 같이 hello 삭제 아이콘을 선택 하 여 구성에 피어 링을 제거할 수 있습니다.

![공용 피어링 삭제](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Microsoft 피어링

이 섹션을 사용 하면 생성, 가져오기, 업데이트 및 삭제 hello ExpressRoute 회로 대 한 Microsoft 피어 링 구성이 있습니다.

> [!IMPORTANT]
> 이전 tooAugust 1에 구성 된 ExpressRoute 회로의 Microsoft 피어 링, 경로 필터 정의 되어 있지 않은 경우에 2017 hello Microsoft 피어 링을 통해 보급 되는 모든 서비스 접두사를 갖습니다. Microsoft 또는 그 이후에 2017 년 8 월 1 구성한 ExpressRoute 회로의 피어 링 수는 없습니다 모든 접두사 필터는 연결 될 때까지 보급 toohello 회로 합니다. 자세한 내용은 [Microsoft 피어링에 경로 필터 구성](how-to-routefilter-powershell.md)을 참조하세요.
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 피어 링

1. ExpressRoute 회로를 구성합니다. Hello 회로 완벽 하 게 비전 되도록 hello 연결 공급자가 추가 되었는지를 확인 합니다.

  ![Microsoft 피어링 나열](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Microsoft hello 회로 대 한 피어 링을 구성 합니다. 계속 하기 전에 정보 다음 hello 했는지 확인 합니다.

  * / 30 서브넷 hello 기본 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
  * / 30 서브넷 hello 보조 링크에 대 한 합니다. 사용자가 소유하고 RIR/IRR에 등록된 유효한 공용 IPv4 접두사여야 합니다.
  * 유효한 VLAN ID tooestablish이 피어 링을 합니다. 없는 다른 피어 링 되도록 hello 회로에 사용 하 여 hello 동일한 VLAN ID
  * 피어링에 대한 AS 숫자입니다. 2바이트 및 4바이트 AS 번호를 모두 사용할 수 있습니다.
  * 접두사를 보급: 목록을 제공 해야 모든 접두사의 hello BGP 세션을 통해 tooadvertise 계획 합니다. 공용 IP 주소 접두사만 수락됩니다. Toosend 접두사를 사용 하도록 하려는 경우 쉼표로 구분 된 목록을 보낼 수 있습니다. 이 접두사는 RIR에 등록 된 tooyou 여야 / IRR입니다.
  * **선택 사항-** 고객 ASN: 광고 접두사 수로 등록 된 toohello 피어 링 되지 않은 경우 등록 된 숫자 toowhich로 hello를 지정할 수 있습니다.
  * 라우팅 레지스트리 이름을: hello RIR 지정할 수 있습니다는 hello에 대 한 번호 매기기로이 앞에 추가 IRR를 등록 합니다.
  * **선택 사항-** toouse 하나를 선택 하는 경우 MD5 해시입니다.
3. Hello 피어 링 tooconfigure, 원하는 hello 다음 예와 같이 선택할 수 있습니다 예제입니다. Hello Microsoft 피어 링 행을 선택 합니다.

  ![Microsoft 피어링 행 선택](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Microsoft 피어링을 구성합니다. 다음 이미지는 hello 구성 예를 보여 줍니다.

  ![Microsoft 피어링 구성](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. 모든 매개 변수를 지정 했으면 hello 구성을 저장 합니다.

  회로 가져오면 tooa '유효성 검사 필요' (그림과 같이 hello) 상태 이면 hello 접두사 tooour 지원 팀 소유권 증명 지원 티켓 tooshow 열어야 합니다.

  ![Microsoft 피어링 구성 저장](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  다음 예제는 hello와 같이 hello 포털에서 직접 지원 티켓을 열 수 있습니다.

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Hello 구성이 성공적으로 수락 하는 후 다음 이미지는 다음과 유사한 toohello를 표시 됩니다.

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft 피어 링 세부 정보

Azure 공용 피어 링 hello 피어 링을 선택 하 여의 hello 속성을 볼 수 있습니다.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 피어 링 구성

피어 링 용 hello 행을 선택 하 고 hello 피어 링 속성을 수정할 수 있습니다.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 피어 링

Hello 다음 이미지와 같이 hello 삭제 아이콘을 선택 하 여 피어 링 구성을 제거할 수 있습니다.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>다음 단계

다음 단계 [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-portal-resource-manager.md)
* Express 경로 워크플로에 대한 자세한 내용은 [Express 경로 워크플로](expressroute-workflows.md)를 참조하세요.
* 회로 피어링에 대한 자세한 내용은 [Express 경로 회로 및 라우팅 도메인](expressroute-circuit-peerings.md)을 참조하세요.
* 가상 네트워크 작업에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.
