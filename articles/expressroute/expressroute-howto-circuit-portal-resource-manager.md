---
title: "ExpressRoute 회로 만들기 및 수정: Azure Portal | Microsoft Docs"
description: "이 문서에서는 어떻게 toocreate, 프로 비전, 확인, 업데이트, 삭제 및 ExpressRoute 회로 프로 비전 해제를 설명 합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Express 경로 회로 만들기 및 수정
> [!div class="op_single_selector"]
> * [Azure 포털](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell(클래식)](expressroute-howto-circuit-classic.md)
>

이 문서에서는 toocreate Azure ExpressRoute 회로 사용 하 여 Azure 포털 및 hello Azure 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다. 다음 단계도 hello hello 회로의 toocheck hello 상태를 업데이트 또는 삭제 및 프로 비전 해제 방법을 보여 줍니다.


## <a name="before-you-begin"></a>시작하기 전에
* 검토 hello [필수 구성 요소](expressroute-prerequisites.md) 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 액세스 toohello 갖추어야 [Azure 포털](https://portal.azure.com)합니다.
* 사용 권한을 toocreate 새로운 네트워킹 리소스 가졌는지 확인 합니다. Hello 적절 한 사용 권한이 없는 경우 계정 관리자를 게 문의 하십시오.
* 할 수 있습니다 [비디오를 보려면](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) toobetter 순서로 시작 하기 전에 hello 단계를 파악 합니다.

## <a name="create-and-provision-an-expressroute-circuit"></a>Express 경로 회로 만들기 및 프로비전
### <a name="1-sign-in-toohello-azure-portal"></a>1. Azure 포털 toohello에 로그인
브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) Azure 계정으로 로그인 합니다.

### <a name="2-create-a-new-expressroute-circuit"></a>2. 새 Express 경로 회로 만들기
> [!IMPORTANT]
> ExpressRoute 회로 서비스 키를 발급 하는 hello 순간부터 요금이 청구 됩니다. Hello 연결 공급자가 준비 tooprovision hello 회로이 작업을 수행할 수 있는지 확인 합니다.
> 
> 

1. 만들 수 있습니다 ExpressRoute 회로 hello 옵션 toocreate를 선택 하 여 새 리소스. 클릭 **새로** > **네트워킹** > **ExpressRoute**hello 다음 이미지에에서 나타난 것 처럼:
   
    ![Express 경로 회로 만들기](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. 클릭 한 후 **ExpressRoute**, hello 표시 **만들 ExpressRoute 회로** 블레이드입니다. 이 블레이드를 hello 값에서 데이터를 입력할 때 올바른 SKU 계층 hello 및 계량 데이터를 지정 하는 있는지 확인 합니다.
   
   * **계층** 은 Express 경로 표준 또는 Express 경로 Premium 추가 기능이 사용되는지 여부를 결정합니다. 지정할 수 있습니다 **표준** tooget hello 표준 SKU 또는 **프리미엄** hello premium 추가 기능에 대 한 합니다.
   * **데이터 계량이** hello 청구 유형을 결정 합니다. 데이터 요금제의 경우 **Metered**를 선택하고 무제한 데이터 요금제의 경우 **Unlimited**를 선택할 수 있습니다. hello 청구 유형을 변경할 수 **Metered** 너무**무제한**에서 hello 형식은 변경할 수 있지만 **무제한** 너무**Metered**.
     
     ![Hello SKU 계층 및 데이터 계량을 구성 합니다.](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> 해당 hello 피어 링 위치 나타냅니다 hello 온 [물리적 위치](expressroute-locations.md) microsoft 피어 링는 위치입니다. 이 **하지** 너무 연결 toohello geography hello Azure 네트워크 리소스 공급자의 위치를 가리키는 "위치" 속성입니다. 관련 되지 않은 것은 좋습니다 toochoose 네트워크 리소스 공급자 지리적으로 닫기 toohello hello 회로의 피어 링 위치 합니다. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. 보기 hello 회로 및 속성
**모든 hello 회로 보려면**

선택 하 여 만든 모든 hello 회로 볼 수 있습니다 **모든 리소스** hello 왼쪽 메뉴에서 합니다.

![회로 보기](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Hello 속성 보기**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![보기 속성](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Hello 서비스 키 tooyour 연결 공급자를 프로 비전에 대 한 보내기
이 블레이드에서 **공급자 상태** hello hello 서비스 공급자 쪽에 프로 비전의 현재 상태에 대해 설명 합니다. **상태 회로** Microsoft의 hello에 hello 상태를 제공 합니다. 상태를 프로 비전 하는 회로 대 한 자세한 내용은 참조 hello [워크플로](expressroute-workflows.md#expressroute-circuit-provisioning-states) 문서.

새 ExpressRoute 회로 만들 때 다음 상태 hello hello 회로가 됩니다.

공급자 상태: 프로비전되지 않음<BR>
회로 상태: 활성화됨

![프로비전 프로세스 시작](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

hello 회로 toohello hello 연결 공급자를 사용 하면 hello 진행 중인 경우 뒤에 상태를 변경 합니다.

공급자 상태: 프로비전 중<BR>
회로 상태: 활성화됨

하면 toobe 수 toouse ExpressRoute 회로 hello 상태 뒤에 있어야 합니다.

공급자 상태: 프로비전됨<BR>
회로 상태: 활성화됨

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Hello 상태 및 hello 회로 키의 hello 상태를 주기적으로 확인
선택 하 여 관심이 있는 hello 회로의 hello 속성을 볼 수 있습니다. Hello 확인 **공급자 상태** 너무 이동 했습니다 확인**프로 비전 됨** 계속 하기 전에.

![회로 및 공급자 상태](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. 라우팅 구성 만들기
단계별 지침에 대 한 참조 toohello [ExpressRoute 회로 라우팅 구성을](expressroute-howto-routing-portal-resource-manager.md) toocreate 문서 및 회로 피어 링을 수정 합니다.

> [!IMPORTANT]
> 이러한 지침은 계층 2 연결 서비스를 제공 하는 서비스 공급자를 사용 하 여 만든 toocircuits만 적용 됩니다. 관리된 3계층 서비스(일반적으로 MPLS와 같은 IP VPN)를 제공하는 서비스 공급자를 사용하는 경우 연결 공급자는 사용자를 위해 라우팅을 구성하고 관리합니다.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. 가상 네트워크 tooan ExpressRoute 회로 연결
다음으로, 가상 네트워크 tooyour ExpressRoute 회로 연결 합니다. 사용 하 여 hello [tooExpressRoute 회로 네트워크 연결 가상](expressroute-howto-linkvnet-arm.md) hello 리소스 관리자 배포 모델을 사용 하 여 작업할 때 문서입니다.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>ExpressRoute 회로의 hello 상태를 가져오기
선택 하 여 회로의 hello 상태를 볼 수 있습니다. 

![Express 경로 회로의 상태](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Express 경로 회로 수정
연결에 미치는 영향 없이 Express 경로 회로의 특정 속성을 수정할 수 있습니다.

할 수 있는 가동 중지 시간 없이 사용 다음과 같습니다. hello:

* Express 경로 회로에 대해 Express 경로 프리미엄 추가 기능을 사용하거나 사용하지 않을 수 있습니다.
* 증가 hello 대역폭의 ExpressRoute 회로 제공 된 hello 포트에서 용량입니다. 참고는 회로의 대역폭 hello 다운 그레이드는 지원 되지 않습니다. 
* 데이터 요금 tooUnlimited 데이터에서에서 계획을 계량 hello를 변경 합니다. Note 변경 hello 계량 계획에서 무제한 데이터 요금 tooMetered 데이터가 지원 되지 않습니다.
* *Allow Classic Operations*을 활성화하거나 비활성화할 수 있습니다.

제한 및 제한 사항에 대 한 자세한 내용은 참조 toohello [express 경로 FAQ](expressroute-faqs.md)합니다.

ExpressRoute 회로 toomodify hello 클릭 **구성** 아래 hello 그림에 나와 있는 것 처럼 합니다.

![회로 수정](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Hello 대역폭, SKU, 요금 청구 모델을 수정 하 고 hello 구성 블레이드 내 기존 작업을 허용 수 있습니다.

> [!IMPORTANT]
> Hello 기존 포트에서 부적절 한 용량이 있으면 toorecreate hello ExpressRoute 회로 할 수 있습니다. 해당 위치에서 사용할 수 없는 추가 용량 있으면 hello 회로 업그레이드할 수 없습니다.
>
> Hello 중단 없이 ExpressRoute 회로 대역폭을 줄일 수 없습니다. 대역폭을 다운 그레이드 toodeprovision hello ExpressRoute 회로 해야 하 고 새 ExpressRoute 회로 다시 프로 비전 합니다.
> 
> Premium 추가 기능을 사용 하지 않도록 설정 hello 표준 회로 대 한 허용 되는 기능 보다 큰 리소스를 사용 중인 경우 작업이 실패할 수 있습니다.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Express 경로 회로 프로비전 해제 및 삭제
Hello를 선택 하 여 ExpressRoute 회로 삭제할 수 있습니다 **삭제** 아이콘입니다. 참고 hello 다음.

* ExpressRoute 회로 hello에서 모든 가상 네트워크 연결을 해제 해야 합니다. 이 작업이 실패 하는 경우에 가상 네트워크가 연결 되어 있는지 여부를 확인 toohello 회로 합니다.
* Hello ExpressRoute 회로 서비스 공급자의 프로비저닝 상태 이면 **프로 비전** 또는 **프로 비전 됨** 편인 서비스 공급자 toodeprovision hello 회로 사용 해야 합니다. Tooreserve 리소스를 계속 하 고 hello 서비스 공급자 프로 비전 해제 hello 회로 완료 하 고 알려주는 될 때까지 사용자를 청구 합니다.
* Hello 서비스 공급자가 회로 hello를 프로 비전 해제 하는 경우 (hello 서비스 공급자 프로 비전 상태가 너무 설정 되어**프로 비전 되지**) hello 회로 삭제할 수 있습니다. 이렇게 되 면 hello 회로 대 한 청구

## <a name="next-steps"></a>다음 단계
회로 만든 후 다음 hello 수행 해야 합니다.

* [Express 경로 회로의 라우팅 만들기 및 수정](expressroute-howto-routing-portal-resource-manager.md)
* [가상 네트워크 tooyour ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)

