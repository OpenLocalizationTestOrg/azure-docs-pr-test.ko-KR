---
title: "클래식 tooResource 관리자에서에서 aaaMoving ExpressRoute 회로 | Microsoft Docs"
description: "이 페이지에서는 필요한 간략하게 tooknow 브리징 클래식 hello 및 hello 리소스 관리자 배포 모델에 대 한 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>ExpressRoute 회로 hello 클래식 toohello 리소스 관리자 배포 모델에서 이동
이 문서는 hello 클래식 toohello Azure 리소스 관리자 배포 모델에서에서 Azure ExpressRoute 회로 toomove 의미에 대 한 개요를 제공 합니다.

클래식 hello 및 hello 리소스 관리자 배포 모델 모두에서 배포 되는 단일 express 경로 회로 tooconnect toovirtual 네트워크를 사용할 수 있습니다. ExpressRoute 회로 만드는 방법과 상관 없이 두 가지 경우 모두에서 이제 toovirtual 네트워크를 연결할 수 있습니다.

![두 가지 경우 모두에서 toovirtual 네트워크를 연결 하는 ExpressRoute 회로](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Hello 클래식 배포 모델에서 만들어진 ExpressRoute 회로
ExpressRoute 회로 hello 클래식 배포 모델에서 만든 이동 toobe toohello 리소스 관리자 배포 모델 첫 번째 tooenable 연결 tooboth hello 클래식 및 hello 리소스 관리자 배포 모델을 필요 합니다. 연결을 이동하는 경우 연결 손실 또는 중단은 없습니다. Hello 클래식 배포 모델에 있는 모든 회로를 가상 네트워크 연결 (내 hello 동일한 구독 및 구독 간) 유지 됩니다.

Hello 이동 된 후 성공적으로 완료 hello ExpressRoute 회로, 수행, 모양과 느낌 hello 리소스 관리자 배포 모델에서 만든 ExpressRoute 회로와 동일 하 게 합니다. 이제 연결을 만들 수 toovirtual 네트워크 hello 리소스 관리자 배포 모델에서.

ExpressRoute 회로 대 한 이동된 toohello 리소스 관리자 배포 모델을 수행한 후에 hello 리소스 관리자 배포 모델을 사용 하 여 hello ExpressRoute 회로의 hello 수명 주기를 관리할 수 있습니다. 이 회로 속성 (예: 대역폭, SKU 및 청구 유형), 업데이트 및 hello 리소스 관리자 배포 모델에만 회로 삭제 피어 링 추가/업데이트/삭제와 같은 작업을 수행할 수 있다는 것을 의미 합니다. 액세스 tooboth 배포 모델을 관리 하는 방법에 대 한 자세한 hello 리소스 관리자 배포 모델에서 만들어진 회로에 아래의 toohello 섹션을 참조 하십시오.

사용자 연결 공급자 tooperform hello 이동 tooinvolve를 않아도 됩니다.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Hello 리소스 관리자 배포 모델에서 만들어진 ExpressRoute 회로
에서 만든 hello 리소스 관리자 배포 모델 toobe 두 가지 경우 모두에서 액세스할 수 있는 ExpressRoute 회로 사용할 수 있습니다. 구독에서 모든 ExpressRoute 회로 사용된 toobe 두 가지 경우 모두에서 액세스할 수 있습니다.

* ExpressRoute 회로 hello 리소스 관리자 배포 모델에서 생성 된 기본적으로 액세스 toohello 클래식 배포 모델을 갖지 않습니다.
* Hello 클래식 배포 모델 toohello 리소스 관리자 배포 모델에서 이동 된 ExpressRoute 회로 기본적으로 모두 배포 모델에서 액세스할 수 있습니다.
* ExpressRoute 회로 항상 hello 리소스 관리자 또는 클래식 배포 모델에서 생성 된 여부에 관계 없이 액세스 toohello 리소스 관리자 배포 모델을 갖습니다. 이 즉, toovirtual 네트워크에서 만든 연결을 만들 수는 지침에 따라 리소스 관리자 배포 모델에 hello [어떻게 toolink 가상 네트워크](expressroute-howto-linkvnet-arm.md)합니다.
* 액세스 toohello 클래식 배포 모델 hello에 의해 제어 됩니다 **allowClassicOperations** hello ExpressRoute 회로에 대 한 매개 변수입니다.

> [!IMPORTANT]
> Hello에 설명 된 모든 할당량 [제한 서비스](../azure-subscription-service-limits.md) 페이지 적용 합니다. 예를 들어 표준 회로 hello 리소스 관리자 배포 모델 및 hello 클래식에서 최대 10 개의 가상 네트워크 연결/연결 있을 수 있습니다.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>액세스 toohello 클래식 배포 모델을 제어합니다.
Hello 설정 하 여 두 배포 모델에는 단일 express 경로 회로 toolink toovirtual 네트워크를 사용 하도록 설정할 수 **allowClassicOperations** hello ExpressRoute 회로의 매개 변수입니다.

설정 **allowClassicOperations** tooTRUE toolink 가상 네트워크를 ExpressRoute 회로 모두 배포 모델 toohello에서을 수 있습니다. 다음과 같은 지침으로 hello 클래식 배포 모델에서 toovirtual 네트워크를 연결할 수 있습니다 [toolink 가상 네트워크에 클래식 배포 모델을 hello 어떻게](expressroute-howto-linkvnet-classic.md)합니다. 다음과 같은 지침으로 hello 리소스 관리자 배포 모델에서 toovirtual 네트워크를 연결할 수 있습니다 [toolink에서 가상 네트워크의 리소스 관리자 배포 모델 hello 어떻게](expressroute-howto-linkvnet-arm.md)합니다.

설정 **allowClassicOperations** tooFALSE 블록 hello 클래식 배포 모델에서 toohello 회로 액세스 합니다. 그러나 hello 클래식 배포 모델에 있는 모든 가상 네트워크 연결 유지 됩니다. 이 경우 hello ExpressRoute 회로 hello 클래식 배포 모델에 표시 되지 않습니다.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Hello 클래식 배포 모델에서 작업 지원
클래식 작업을 수행 하는 hello는 express 경로에서 지원 될 때 회로 **allowClassicOperations** tooTRUE 설정:

* Express 경로 회로 정보 가져오기
* 가상 네트워크 만들기/업데이트/get/삭제 tooclassic 가상 네트워크에 연결
* 구독 간 연결에 대한 가상 네트워크 연결 권한 부여 만들기/업데이트/가져오기/삭제

Hello 다음 클래식 작업을 수행할 수 없을 때 **allowClassicOperations** tooTRUE 설정 됩니다.

* Azure 개인, Azure 공용 및 Microsoft 피어링에 대한 BGP(Border Gateway Protocol) 피어링 만들기/업데이트/가져오기/삭제
* Express 경로 회로 삭제

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>클래식 hello와 hello 리소스 관리자 배포 모델 간의 통신
ExpressRoute 회로 hello 클래식 hello와 hello 리소스 관리자 배포 모델 간의 다리 역할을 합니다. 두 가상 네트워크가 연결 된 toohello 경우 hello 클래식 배포 모델의 가상 네트워크에 가상 컴퓨터 및 가상 네트워크를 ExpressRoute 통해 hello 리소스 관리자 배포 모델 흐름에 있는 간의 트래픽이 동일한 ExpressRoute 회로 합니다.

동시에 집계 처리량 hello 가상 네트워크 게이트웨이의 hello 처리 용량으로 제한 됩니다. 트래픽 이러한 경우에 hello 연결 공급자 네트워크 또는 네트워크를 입력 하지 않습니다. Hello 가상 네트워크 간의 트래픽 흐름 hello Microsoft 네트워크 완벽 하 게 포함 되어 있습니다.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>TooAzure 공용 액세스 및 Microsoft 피어 링 리소스
일반적으로 Azure 공용 피어 링 및 중단 없이 Microsoft 피어 링을 통해 액세스할 수 있는 tooaccess 리소스를 계속할 수 있습니다.  

## <a name="whats-supported"></a>지원되는 내용
이 섹션에서는 Express 경로 회로에 지원되는 내용을 설명합니다.

* 단일 express 경로 회로 tooaccess 가상 네트워크 클래식 hello 및 hello 리소스 관리자 배포 모델에 배포 되는 사용할 수 있습니다.
* Hello 클래식 toohello 리소스 관리자 배포 모델에서에서 ExpressRoute 회로 이동할 수 있습니다. 이동한 후 hello ExpressRoute 회로, 느낌을 찾아서 hello 리소스 관리자 배포 모델에서 생성 된 다른 ExpressRoute 회로 동일 합니다.
* ExpressRoute 회로 hello만 이동할 수 있습니다. 회로 링크, 가상 네트워크 및 VPN 게이트웨이는 이 작업을 통해 이동될 수 없습니다.
* ExpressRoute 회로 대 한 이동된 toohello 리소스 관리자 배포 모델을 수행한 후에 hello 리소스 관리자 배포 모델을 사용 하 여 hello ExpressRoute 회로의 hello 수명 주기를 관리할 수 있습니다. 이 회로 속성 (예: 대역폭, SKU 및 청구 유형), 업데이트 및 hello 리소스 관리자 배포 모델에만 회로 삭제 피어 링 추가/업데이트/삭제와 같은 작업을 수행할 수 있다는 것을 의미 합니다.
* ExpressRoute 회로 hello 클래식 hello와 hello 리소스 관리자 배포 모델 간의 다리 역할을 합니다. 두 가상 네트워크가 연결 된 toohello 경우 hello 클래식 배포 모델의 가상 네트워크에 가상 컴퓨터 및 가상 네트워크를 ExpressRoute 통해 hello 리소스 관리자 배포 모델 흐름에 있는 간의 트래픽이 동일한 ExpressRoute 회로 합니다.
* 구독 간 연결 클래식 hello 및 hello 리소스 관리자 배포 모델 모두에서 지원 됩니다.
* Hello 클래식 모델 toohello Azure 리소스 관리자 모델에서 ExpressRoute 회로 이동한 후 다음을 할 수 있습니다 [hello 가상 네트워크 연결 된 toohello ExpressRoute 회로 마이그레이션하려면](expressroute-migration-classic-resource-manager.md)합니다.

## <a name="whats-not-supported"></a>지원 되지않는 사항
이 섹션에서는 Express 경로 회로에 지원되지 않는 내용을 설명합니다.

* Hello 클래식 배포 모델에서 ExpressRoute 회로의 hello 수명 주기를 관리 합니다.
* Hello 클래식 배포 모델에 대 한 역할 기반 액세스 제어 (RBAC) 지원 Hello 클래식 배포 모델에서 RBAC 컨트롤 tooa 회로 수행할 수 없습니다. Hello 구독의 모든 관리자/coadministrator 연결 하거나 가상 네트워크 toohello 회로 연결을 해제할 수 있습니다.

## <a name="configuration"></a>구성
에 설명 된 hello 지침에 따라 [hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](expressroute-howto-move-arm.md)합니다.

## <a name="next-steps"></a>다음 단계
* [Hello 가상 네트워크 연결 된 toohello ExpressRoute 회로 hello 클래식 모델 toohello Azure 리소스 관리자 모델에서 마이그레이션](expressroute-migration-classic-resource-manager.md)
* 워크플로 정보는 [Express 경로 회로 프로비전 워크플로 및 회로 상태](expressroute-workflows.md)를 참조하세요.
* tooconfigure ExpressRoute 연결:
  
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md)
  * [라우팅 구성](expressroute-howto-routing-arm.md)
  * [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)

