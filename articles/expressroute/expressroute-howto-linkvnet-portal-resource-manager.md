---
title: "가상 네트워크 tooan ExpressRoute 회로 연결: Azure 포털 | Microsoft Docs"
description: "이 문서는 어떻게 toolink 가상 네트워크 (Vnet) tooExpressRoute 회로의 개요를 제공 합니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>가상 네트워크 tooan ExpressRoute 회로 연결
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-linkvnet-classic.md)
> 

이 문서를 사용 하면 hello 리소스 관리자 배포 모델을 사용 하 여 가상 네트워크 (Vnet) tooAzure ExpressRoute 회로 연결 하 고 Azure 포털 hello 있습니다. 가상 네트워크 수 hello에 동일한 구독 또는 있습니다 수의 일부가 될 다른 구독 합니다.

## <a name="before-you-begin"></a>시작하기 전에
* 검토 hello [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 활성화된 Express 경로 회로가 있어야 합니다.
  
  * 너무 hello 지침에 따라[ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) 있고 hello 회로 연결 공급자가 사용 하도록 설정 합니다.
  * 회로에 구성된 Azure 개인 피어링이 있는지 확인합니다. Hello 참조 [구성 라우팅](expressroute-howto-routing-portal-resource-manager.md) 라우팅 지침에 대 한 문서입니다.
  * 구성 된 Azure 개인 피어 링 및 종단 간 연결을 사용 하도록 설정할 수 있도록 중일 hello 네트워크와 Microsoft 간에 BGP 피어 링을 확인 합니다.
  * 가상 네트워크 및 가상 네트워크 게이트웨이를 만들어서 완전히 프로비전해야 합니다. 너무 hello 지침에 따라[ExpressRoute에 대 한 가상 네트워크 게이트웨이 만들](expressroute-howto-add-gateway-resource-manager.md)합니다. ExpressRoute에 대 한 가상 네트워크 게이트웨이 hello GatewayType 'ExpressRoute' 하지 VPN을 사용합니다.

* Too10 가상 네트워크 tooa 표준 ExpressRoute 회로를 연결할 수 있습니다. 모든 가상 네트워크 hello에 있어야 합니다. 동일한 지리적 지역 표준 ExpressRoute 회로 사용 하는 경우. 
* Hello ExpressRoute 회로의 hello 지리적 영역 외부의 가상 네트워크 연결 또는 hello ExpressRoute premium 추가 기능을 사용 하는 경우 많은 수의 가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다. Hello 확인 [FAQ](expressroute-faqs.md) hello premium 추가 기능에 대 한 자세한 내용은 합니다.
* 할 수 있습니다 [비디오를 보려면](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) 전에 시작 toobetter hello 단계를 파악 합니다.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Hello의 가상 네트워크 연결 동일한 구독 tooa 회로

### <a name="toocreate-a-connection"></a>toocreate 연결

> [!NOTE]
> BGP 구성 정보는 표시 되지 hello 계층 3 공급자에 피어 링을 구성 하는 경우. 회로 프로 비전 된 상태에 있으면 수 toocreate 연결 해야 합니다.
>

1. Express 경로 회로 및 Azure 개인 피어링이 성공적으로 구성되었는지 확인합니다. Hello 지침에 따라 [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md) 및 [구성 라우팅](expressroute-howto-routing-arm.md)합니다. ExpressRoute 회로 hello 다음 이미지와 같습니다.

    ![Express 경로 회로 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. 이제 연결 toolink 가상 네트워크 게이트웨이 tooyour ExpressRoute 회로 프로 비전을 시작할 수 있습니다. 클릭 **연결** > **추가** tooopen hello **연결 추가** 블레이드에서 hello 값을 구성 합니다.

    ![연결 추가 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. 연결이 성공적으로 구성 된 후 연결 개체에는 hello 연결에 대 한 hello 정보가 표시 됩니다.

     ![연결 개체 스크린샷](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete 연결
Hello를 선택 하 여 연결을 삭제할 수 **삭제** 연결에 대 한 hello 블레이드에서 아이콘입니다.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>다른 구독 tooa 회로에 가상 네트워크에 연결
여러 구독에서 Express 경로 회로를 공유할 수 있습니다. 아래 hello 그림 간단한 계통도 나와의 ExpressRoute 회로 대 한 일정 공유 works 여러 구독에서.

![구독 간 연결](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- 사용 되는 toorepresent 속하는 구독에 조직 내의 toodifferent 부서는 각각 hello 작은 구름 hello 큰 구름 안에 있습니다.
- 해당 서비스를 배포 각각 hello 부서 hello 조직 내에서 자체 구독 사용할 수 있지만 단일 express 경로 회로 tooconnect 백 tooyour 온-프레미스 네트워크를 공유할 수 있습니다.
- 단일 부서 (이 예제의: IT) hello ExpressRoute 회로 소유할 수 있습니다. Hello 조직 내에서 다른 구독 hello ExpressRoute 회로 사용할 수 있습니다.

    > [!NOTE]
    > Hello 전용 회로 대 한 연결 및 대역폭 요금은 적용된 toohello ExpressRoute 회로 소유자 됩니다. Hello를 공유 하는 모든 가상 네트워크 대역폭이 동일 합니다.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>관리 - 회로 소유자 및 회로 사용자

'회로 소유자' hello는 hello ExpressRoute 회로 리소스의 인증된 된 전원 사용자입니다. hello 회로 소유자는 '회로 사용자'가 교환할 수 있는 권한 부여를 만들 수 있습니다. 회로 사용자 가상 네트워크의 소유자가 없는 내 게이트웨이 ExpressRoute 회로 hello으로 동일한 구독 hello 합니다. 회로 사용자는 가상 네트워크당 하나의 권한 부여를 사용할 수 있습니다.

hello 회로 소유자는 언제 든 지 hello 전원 toomodify 및 revoke 권한을 가집니다. 액세스가 해지 된 hello 구독에서 삭제 되 고 모든 링크 연결에는 권한 부여 결과 취소 합니다.

### <a name="circuit-owner-operations"></a>회로 소유자 작업

**toocreate 연결 권한 부여**

hello 회로 소유자는 권한 부여를 만듭니다. 이 인해 hello 생성 될 수 있는 권한 부여 키의 해당 가상 네트워크 게이트웨이 toohello ExpressRoute 회로 회로 사용자 tooconnect에서 사용 합니다. 권한 부여는 하나의 연결에만 유효합니다.

1. Hello ExpressRoute 블레이드에서 클릭 **권한 부여** 한 다음를 입력 한 **이름** hello 권한 부여 및 클릭에 대 한 **저장**합니다.

    ![권한 부여](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Hello 구성이 저장 되 고 나면 복사 hello **리소스 ID** 및 hello **인증 키**합니다.

    ![인증 키](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete 연결 권한 부여**

Hello를 선택 하 여 연결을 삭제할 수 **삭제** 연결에 대 한 hello 블레이드에서 아이콘입니다.

### <a name="circuit-user-operations"></a>회로 사용자 작업

hello 회로 사용자는 hello 리소스 ID 및 권한 부여 키 hello 회로 소유자 로부터 필요합니다. 

**tooredeem 연결 권한 부여**

1.  Hello 클릭 **+ 새로 만들기** 단추입니다.

    ![새로 만들기 클릭](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  검색할 **"연결"** 마켓플레이스 hello에서 선택 하 고 클릭 **만들기**합니다.

    ![연결 검색](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  있는지 hello 확인 **연결 유형** 너무 설정 된 "express 경로"입니다.


4.  Hello 세부 정보를 입력 한 다음 클릭 **확인** hello 기본 사항 블레이드에서 합니다.

    ![기본 사항 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  Hello에 **설정** 블레이드, 선택 hello **가상 네트워크 게이트웨이** hello를 확인 하 고 **권한 부여 교환** 확인란 합니다.

6.  Hello 입력 **인증 키** 및 hello **회로 URI 피어** hello 연결 이름을 지정 합니다. **확인**을 클릭합니다.

    ![설정 블레이드](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Hello hello 정보를 검토 **요약** 블레이드에 대 한 클릭 **확인**합니다.


**toorelease 연결 권한 부여**

Hello ExpressRoute 회로 toohello 가상 네트워크를 연결 하는 hello 연결을 삭제 하 여 권한 부여를 해제할 수 있습니다.

## <a name="next-steps"></a>다음 단계
ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
