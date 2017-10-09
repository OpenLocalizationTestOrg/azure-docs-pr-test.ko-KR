---
title: "여러 VPN 사이트 간 게이트웨이 연결 tooa VNet 추가: Azure 포털: 리소스 관리자 | Microsoft Docs"
description: "다중 사이트 S2S 연결 tooa VPN 게이트웨이 추가 하는 기존 연결"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>기존 VPN 게이트웨이 연결에는 사이트 간 연결 tooa VNet 추가

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell(클래식)](vpn-gateway-multi-site.md)
>
> 

이 문서 hello Azure 포털 tooadd 사이트 및 사이트 간 (S2S) 연결 tooa VPN 게이트웨이 기존 연결이 있는 사용 하 여 안내 합니다. 이 연결의 형식은 종종 참조 tooas "멀티 사이트" 구성 합니다. S2S 연결 tooa S2S 연결, 지점 및 사이트 연결 또는 VNet 대 VNet 연결을 이미 있는 VNet을 추가할 수 있습니다. 연결을 추가하는 데 몇 가지 제한이 있습니다. Hello 확인 [시작 하기 전에](#before) 섹션에서 구성을 시작 하기 전에이 문서 tooverify 합니다. 

이 문서 RouteBased VPN 게이트웨이가 있는 hello 리소스 관리자 배포 모델을 사용 하 여 만든 tooVNets 적용 됩니다. 이러한 단계는 tooExpressRoute /-사이트 공존할 연결 구성 적용 되지 않습니다. 공존 연결에 대한 자세한 내용은 [xpress 경로/S2S 공존 연결](../expressroute/expressroute-howto-coexist-resource-manager.md)을 참조하세요.

### <a name="deployment-models-and-methods"></a>배포 모델 및 메서드
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다. 문서를 사용할 수 있는이 테이블에서 tooit을 연결 직접 합니다.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>시작하기 전에
Hello 다음 항목을 확인 합니다.

* ExpressRoute/S2S 공존 연결을 만들지 않습니다.
* 기존에 연결 되어 있는 hello 리소스 관리자 배포 모델을 사용 하 여 만든 가상 네트워크를 해야 합니다.
* VNet에 대 한 가상 네트워크 게이트웨이 hello RouteBased입니다. PolicyBased VPN 게이트웨이 사용 하도록 설정한 경우에 hello 가상 네트워크 게이트웨이 삭제 하 고 RouteBased로 새 VPN 게이트웨이 만들 해야 합니다.
* Hello 주소 범위가 겹치지 Vnet이이 VNet에 연결 하는 hello에 대 한 합니다.
* 호환 VPN 장치 및 사용자 수 tooconfigure가 있는 것입니다. [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요. VPN 장치 구성에 익숙하지 않은 익숙하지 않은 hello IP 주소 범위를 온-프레미스 네트워크 구성에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate가 필요 합니다.
* VPN 장치에 대한 외부 연결 공용 IP 주소가 있습니다. 이 IP 주소는 NAT 뒤에 배치할 수 없습니다.

## <a name="part1"></a>1부 - 연결 구성
1. 브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.
2. 클릭 **모든 리소스** 찾습니다 프로그램 **가상 네트워크 게이트웨이** hello 리소스 목록에서 클릭 합니다.
3. Hello에 **가상 네트워크 게이트웨이** 블레이드에서 클릭 **연결**합니다.
   
    ![연결 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")<br>
4. Hello에 **연결** 블레이드에서 클릭 **+ 추가**합니다.
   
    ![추가 연결 단추](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "추가 연결 단추")<br>
5. Hello에 **연결 추가** 블레이드에서 hello 필드에 다음 내용을 입력 합니다.
   
   * **이름:** toogive toohello 사이트 hello 연결을 만들면 원하는 hello 이름입니다.
   * **연결 형식:** **사이트 간(IPSec)**을 선택합니다.
     
     ![추가 연결 블레이드](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "추가 연결 블레이드")<br>

## <a name="part2"></a>2부 - 로컬 네트워크 게이트웨이 추가
1. **로컬 네트워크 게이트웨이**를 클릭하고 ***로컬 네트워크 게이트웨이를 선택 합니다***. Hello 열립니다 **로컬 네트워크 게이트웨이 선택** 블레이드입니다.
   
    ![로컬 네트워크 게이트웨이 선택](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "로컬 네트워크 게이트웨이 선택")<br>
2. 클릭 **새로 만들기** tooopen hello **로컬 네트워크 게이트웨이 만들기** 블레이드입니다.
   
    ![로컬 네트워크 게이트웨이 블레이드 만들기](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "로컬 네트워크 게이트웨이 만들기")<br>
3. Hello에 **로컬 네트워크 게이트웨이 만들기** 블레이드에서 hello 필드에 다음 내용을 입력 합니다.
   
   * **이름:** toogive toohello 로컬 네트워크 게이트웨이 리소스 hello 이름입니다.
   * **IP 주소:** hello tooconnect를 원하는 hello 사이트에 대 한 hello VPN 장치의 공용 IP 주소입니다.
   * **주소 공간:** toobe 원하는 hello 주소 공간 toohello 새 로컬 네트워크 사이트를 라우팅됩니다.
4. 클릭 **확인** hello에 **로컬 네트워크 게이트웨이 만들기** 블레이드 toosave hello 변경 합니다.

## <a name="part3"></a>3 부-hello 공유 키를 추가 하 고 hello 연결 만들기
1. Hello에 **연결 추가** 블레이드에서 원하는 toouse toocreate 연결 hello 공유 키를 추가 합니다. 중 하나 가져와서 hello 공유 키 VPN 장치에서 또는 여기 하나를 수행 하 여 VPN 장치 toouse hello를 구성 합니다 동일한 키를 공유 합니다. hello hello 키 정확 하 게 되는 중요 한 hello 동일 합니다.
   
    ![공유 키](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")<br>
2. Hello 블레이드의 hello 아래쪽 클릭 **확인** toocreate hello 연결 합니다.

## <a name="part4"></a>4 부-hello VPN 연결 확인


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>다음 단계

연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. Hello 가상 컴퓨터를 참조 하십시오. [학습 경로](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) 자세한 정보에 대 한 합니다.
