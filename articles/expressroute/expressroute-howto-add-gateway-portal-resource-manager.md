---
title: "ExpressRoute에 대 한 가상 네트워크 게이트웨이 tooa VNet 추가: 포털: Azure | Microsoft Docs"
description: "이 문서에서는 이미 ExpressRoute에 대 한 리소스 관리자 VNet을 만든 가상 네트워크 게이트웨이 tooan를 추가 하는 과정을 안내 합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 ExpressRoute에 대 한 가상 네트워크 게이트웨이 구성 합니다.
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [클래식 - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

이 문서에서는 기존 VNet에 대 한 hello 단계 tooadd 가상 네트워크 게이트웨이를 안내 합니다. 이 문서 단계별로 hello 단계 tooadd, 크기 조정 및 기존 VNet에 대 한 가상 네트워크 (VNet) 게이트웨이 제거 합니다. 이 구성에 대 한 hello 단계 ExpressRoute 구성에 사용할 hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vnet에 대 한 구체적으로 합니다. 가상 네트워크 게이트웨이 및 ExpressRoute의 게이트웨이 구성 설정에 대한 자세한 내용은 [ExpressRoute에 대한 가상 네트워크 게이트웨이 정보](expressroute-about-virtual-network-gateways.md)를 참조하세요. 


## <a name="before-beginning"></a>시작하기 전에

이 작업 사용 하 여 VNet에 대 한 hello 단계 hello 구성 참조 목록 다음의 hello 값에 기반 합니다. 예제 단계에서 이 목록을 사용합니다. 자신의 hello 값 대체를 참조로 hello 목록 toouse을 복사할 수 있습니다.

**구성 참조 목록**

* 가상 네트워크 이름 = "TestVNet"
* 가상 네트워크 주소 공간: 192.168.0.0/16
* 서브넷 이름= “FrontEnd” 
    * 서브넷 주소 공간 = “192.168.1.0/24”
* 리소스 그룹: "TestRG"
* 위치 = “미국 동부”
* 게이트웨이 서브넷 이름: "GatewaySubnet" 게이트웨이 서브넷의 이름을 항상 *GatewaySubnet*으로 지정해야 합니다.
    * 게이트웨이 서브넷 주소 공간 = "192.168.200.0/26"
* 게이트웨이 이름 = “ERGW”
* 게이트웨이 IP 이름 = "MyERGWVIP"
* 게이트웨이 유형 = “ExpressRoute” Express 경로 구성에 이 유형이 필요합니다.
* 게이트웨이 공용 IP 이름 = “MyERGWVIP”

구성을 시작하기 전에 이러한 단계의 [비디오](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)를 시청하십시오.

## <a name="create-hello-gateway-subnet"></a>Hello 게이트웨이 서브넷 만들기

1. Hello에 [포털](http://portal.azure.com), 가상 네트워크 게이트웨이 toocreate 원하는 toohello 리소스 관리자 가상 네트워크를 이동 합니다.
2. Hello에 **설정** 섹션 VNet 블레이드의 클릭 **서브넷** tooexpand hello 서브넷 블레이드입니다.
3. Hello에 **서브넷** 블레이드에서 클릭 **+ 게이트웨이 서브넷** tooopen hello **서브넷 추가** 블레이드입니다. 
   
    ![Hello 게이트웨이 서브넷 추가](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "hello 게이트웨이 서브넷 추가")


4. hello **이름** 값 'GatewaySubnet' 서브넷에 자동으로 hello를 사용 하 여 채워집니다. 이 값은 Azure toorecognize hello 서브넷에 대 한 순서 대로 hello 게이트웨이 서브넷으로 필요 합니다. 자동으로 채워진 hello 조정 **주소 범위** 값 toomatch 사용자 구성 요구 사항입니다. /27 이상의 게이트웨이 서브넷을 만드는 것이 좋습니다(/26, /25, 등). 클릭 **확인** toosave 값 hello 및 hello 게이트웨이 서브넷을 만듭니다.

    ![Hello 서브넷 추가](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "hello 서브넷 추가")

## <a name="create-hello-virtual-network-gateway"></a>Hello 가상 네트워크 게이트웨이 만들기

1. Hello 왼쪽에 hello 포털에서 클릭  **+**  검색에 ' 가상 네트워크 게이트웨이 '를 입력 합니다. 찾을 **가상 네트워크 게이트웨이** hello 검색에서 반환 하 고 hello 항목을 클릭 합니다. Hello에 **가상 네트워크 게이트웨이** 블레이드에서 클릭 **만들기** hello hello 블레이드 맨 아래에 있습니다. Hello 열립니다 **가상 네트워크 게이트웨이 만들기** 블레이드입니다.
2. Hello에 **가상 네트워크 게이트웨이 만들기** 블레이드, 가상 네트워크 게이트웨이에 대 한 hello 값을 입력 합니다.

    ![가상 네트워크 게이트웨이 만들기 블레이드의 필드](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "가상 네트워크 게이트웨이 만들기 블레이드의 필드")
3. **이름**: 게이트웨이 이름을 지정합니다. 이 게이트웨이 서브넷 이름 지정과 동일 hello 없습니다. 만들려는 hello 게이트웨이 개체의 hello 이름의 것입니다.
4. **게이트웨이 유형**: **ExpressRoute**를 선택합니다.
5. **SKU**: hello 드롭다운에서 선택 hello 게이트웨이 SKU입니다.
6. **위치**: hello 조정 **위치** 가상 네트워크가 있는 toopoint toohello 위치 필드입니다. Hello 위치 toohello 지역 가상 네트워크가 있는 위치를 가리키지 않습니다, 가상 네트워크 hello hello 'Choose 가상 네트워크' 드롭다운에 표시 되지 않습니다.
7. 가상 네트워크 toowhich hello 선택 tooadd이이 게이트웨이 선택 합니다. 클릭 **가상 네트워크** tooopen hello **가상 네트워크를 선택** 블레이드입니다. Hello VNet을 선택 합니다. VNet 보이지 않으면 확인 되었는지 hello **위치** 필드 toohello 지역 가상 네트워크의 위치를 가리키는 가리키고 합니다.
9. 공용 IP 주소를 선택합니다. 클릭 **공용 IP 주소** tooopen hello **공용 IP 주소 선택** 블레이드입니다. 클릭 **+ 새로 만들기** tooopen hello **만들기 공용 IP 주소 블레이드**합니다. 공용 IP 주소의 이름을 입력합니다. 이 블레이드는 공용 IP 주소를 동적으로 할당 되도록 하는 공용 IP 주소 개체 toowhich를 만듭니다. 클릭 **확인** toosave 변경 toothis 블레이드입니다.
10. **구독**: 해당 hello 올바른 구독이 선택 되었는지 확인 합니다.
11. **리소스 그룹**:이 설정을 선택 하는 가상 네트워크 hello에 의해 결정 됩니다.
12. Hello를 조정 하지 않을 **위치** hello 이전 설정을 지정한 후 합니다.
13. Hello 설정을 확인 합니다. 선택할 수 있습니다 프로그램 게이트웨이 tooappear hello 대시보드에서 하려는 경우 **Pin toodashboard** hello hello 블레이드 맨 아래에 있습니다.
14. 클릭 **만들기** toobegin hello 게이트웨이 만들기. hello 설정 유효성을 검사 하 고 hello 게이트웨이 배포 합니다. 가상 네트워크 게이트웨이 만들기 too45 분 toocomplete 차지할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Hello VNet 게이트웨이 만든 후에 VNet tooan ExpressRoute 회로 연결할 수 있습니다. 참조 [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-portal-resource-manager.md)합니다.
