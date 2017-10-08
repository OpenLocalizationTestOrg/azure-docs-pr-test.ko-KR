---
title: "aaaConfigure 가상 네트워크 및 게이트웨이에서 ExpressRoute에 대 한 hello 클래식 포털 | Microsoft Docs"
description: "이 문서에서는 hello 클래식 배포 모델 및 hello 클래식 포털을 사용 하 여 ExpressRoute에 대 한 가상 네트워크를 설정 하는 과정을 안내 합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Hello 클래식 포털의 ExpressRoute에 대 한 가상 네트워크 만들기
이 문서의 hello 단계에서는 hello 클래식 배포 모델 및 hello 클래식 포털을 사용 하 여 ExpressRoute와 가상 네트워크 및 사용 하기 위해 가상 네트워크 게이트웨이 구성 하는 과정을 안내 합니다.

다음 문서는 hello hello 리소스 관리자 배포 모델에 대 한 지침을 원하는 경우 사용할 수 있습니다: [PowerShell을 사용 하 여 가상 네트워크를 만드는](../virtual-network/virtual-networks-create-vnet-arm-ps.md) 및 [VPN 게이트웨이 tooa 리소스 관리자 VNet 추가 대 한 ExpressRoute](expressroute-howto-add-gateway-resource-manager.md)합니다.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>클래식 VNet 및 게이트웨이 만들기
hello 다음 단계를 만들고 클래식 VNet 가상 네트워크 게이트웨이. 클래식 VNet 이미 있는 경우 참조 hello [는 기존 클래식 VNet 구성](#config) 이 문서의 섹션.

1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com)합니다.
2. Hello 왼쪽 아래 모퉁이의 hello 화면을 클릭 **새로**합니다. Hello 탐색 창에서 클릭 **네트워크 서비스**, 클릭 하 고 **가상 네트워크**합니다. 클릭 **사용자 지정 만들기** toobegin hello 구성 마법사.
3. Hello에 **가상 네트워크 세부 정보** 페이지 hello 다음을 입력 합니다.
   
   * **이름** : 가상 네트워크 이름을 지정합니다. Toomake hello 이름을 너무 복잡 하지 못하게 하려는 하므로 Vm 및 PaaS 인스턴스를 배포할 때이 가상 네트워크 이름을 사용 합니다.
   * **위치** – hello 위치는 리소스 (Vm) tooreside 저장할 실제 직접적인 관련된은 toohello 위치 (지역). 예를 들어 hello Vm을 toothis 가상 네트워크 toobe 미국 동부에 물리적으로 배치를 배포 하려는 경우 해당 위치를 선택 합니다. 만든 후 가상 네트워크와 관련 된 hello 지역을 변경할 수 없습니다.
4. Hello에 **DNS 서버 및 VPN 연결** 페이지 hello 다음 정보를 입력 한 다음 hello hello 오른쪽 아래에서 다음 화살표를 클릭 합니다. 
   
   * **DNS 서버** -hello DNS 서버 이름 및 IP 주소를 입력 하거나 hello 바로 가기 메뉴에서 이전에 등록 된 DNS 서버를 선택 합니다. 이 설정은 DNS 서버를 만들지 않습니다. 이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 toospecify hello DNS 서버가 있습니다.
   * **사이트 간 연결** -선택에 대 한 확인란 hello **사이트 간 VPN 구성**합니다.
   * **ExpressRoute** – 확인란 hello **ExpressRoute 사용**합니다. **사이트간 VPN 구성**을 선택한 경우에 이 옵션만이 나타납니다
   * **로컬 네트워크** -필수 toohave ExpressRoute에 대 한 로컬 네트워크 사이트를 됩니다. 그러나, ExpressRoute 연결의 hello 경우 hello 주소 접두사에 대해 지정 hello 로컬 네트워크 사이트는 무시 됩니다. 대신, hello 주소 접두사 보급 hello ExpressRoute 회로 통해 tooMicrosoft 라우팅 목적에 사용 됩니다.<BR>ExpressRoute 연결에 대해 만든 로컬 네트워크를 이미 있는 경우에 hello 드롭다운에서 선택할 수 있습니다. 없는 경우 **새 로컬 네트워크 지정**을 선택합니다.
5. hello **사이트 간 연결** hello 이전 단계에서 toospecify 새 로컬 네트워크를 선택한 경우 페이지가 나타납니다. tooconfigure 로컬 네트워크 hello 다음 정보를 입력 한 후 hello 다음 화살표를 클릭 합니다. 
   
   * **이름** -hello 이름을 toocall 로컬 네트워크 사이트 (온-프레미스).
   * **주소 공간** - 시작 IP 및 CIDR(주소 수)를 포함합니다. 가상 네트워크에 대 한 hello 주소 범위와 겹치지 않는으로 임의의 주소 범위를 지정할 수 있습니다. 일반적으로 온-프레미스 네트워크에 대 한 hello 주소 범위 지정이 있지만 ExpressRoute의 hello 경우에서 이러한 설정은 사용 되지 않습니다. 그러나, hello 클래식 포털을 사용 하는 경우 순서 toocreate hello에 대 한 로컬 네트워크에이 설정은 필수입니다.
   * **주소 공간 추가** -이 설정은 Express 경로와 관련이 없습니다.
6. Hello에 **가상 네트워크 주소 공간** 페이지 hello 다음 정보를 입력 한 다음 네트워크 hello 하단 오른쪽 tooconfigure에 hello 확인 표시를 클릭 합니다. 
   
   * **주소 공간** - 시작 IP 및 주소 수를 포함합니다. Hello 주소 공간을 지정 하면 로컬 네트워크에가지고 있는 hello 주소 공간 중 하나를 겹치지 않는지 확인 하십시오.
   * **서브넷 추가** - 시작 IP 및 주소 수를 포함합니다. 추가 서브넷은 필요하지 않습니다.
   * **게이트웨이 서브넷 추가** -tooadd hello 게이트웨이 서브넷을 클릭 합니다. hello 게이트웨이 서브넷은 hello 가상 네트워크 게이트웨이에 사용 되며이 구성에 필요 합니다.<BR>ExpressRoute/28 이어야 합니다. CIDR (주소 수) 게이트웨이 서브넷 hello 또는 더 큰 (27 일, / / 26 등.). 이렇게 하면 해당 서브넷 tooallow hello 구성 toowork의 IP 주소가 부족 합니다. Hello 클래식 포털의 hello 확인란 toouse ExpressRoute를 선택한 경우 hello 포털 지정 게이트웨이 서브넷/28 사용 합니다.  Hello 클래식 포털의 hello CIDR 주소 수를 조정할 수 없습니다. hello 게이트웨이 서브넷으로 나타납니다. **게이트웨이** hello 클래식 포털의 hello 만들어지는 hello 게이트웨이 서브넷의 실제 이름 이지만 실제로 **GatewaySubnet**합니다. Hello Azure 포털 또는 PowerShell을 사용 하 여이 이름을 볼 수 있습니다.
7. 클릭 하 여 hello hello 페이지 하단에 확인 표시를 hello 및 가상 네트워크가 toocreate 시작 됩니다. 완료 될 때, 나타납니다 **Created** 아래에 나열 **상태** hello에 **네트워크** hello 클래식 포털의 페이지입니다.

## <a name="gw"></a>Hello 게이트웨이 만들기
1. Hello에 **네트워크** 페이지 만들어지면 방금 hello 가상 네트워크를 클릭 한 다음 클릭 **대시보드** hello hello 페이지 위쪽에 있습니다.
2. Hello의 hello 아래쪽에 **대시보드** 페이지 **게이트웨이 만들기** 선택 **동적 라우팅**합니다. 클릭 **예** tooconfirm toocreate 게이트웨이 되도록 합니다.
3. Hello 게이트웨이 만들기 시작 될 때를 알리는 메시지가 해당 hello 게이트웨이가 시작 되었음을 볼 수 있습니다. Hello 게이트웨이 toocreate too45 분이 걸릴 수도 있습니다.
4. 네트워크 tooa 회로 연결 합니다. Hello hello 문서의 지침에 따라 [어떻게 toolink Vnet tooExpressRoute 회로](expressroute-howto-linkvnet-classic.md)합니다.

## <a name="config"></a>Express 경로에 대한 기존 클래식 VNet 구성
클래식 VNet이 이미 있으면 hello 클래식 포털에서 tooconnect tooExpressRoute 구성할 수 있습니다. hello 설정을 해당 섹션 toobecome hello 익숙한 통해 읽기 필요한 설정 하므로 위의 hello 섹션으로 동일 hello 됩니다. Express 경로 /-사이트 공존할 연결 toocreate 참조 [이 여기서](expressroute-howto-coexist-classic.md) hello 단계에 대 한 합니다. 이 문서의 단계를 hello 보다 서로 합니다.

1. VNet 설정의 hello 나머지 부분을 업데이트 하기 전에 toocreate hello 로컬 네트워크를 해야 합니다. toocreate이 필요한 hello 클래식 포털을 통해 ExpressRoute를 구성 하는 경우 새 로컬 네트워크를 클릭 하 여 **새로**  **>**  **네트워크 서비스**  **>**  **가상 네트워크**  **>**  **로컬 네트워크 추가**합니다. Hello 마법사 단계 toocreate hello 로컬 네트워크를 따릅니다.
2. 사용 하 여 **구성** VNet과 tooassociate hello VNet toohello 로컬 네트워크에 대 한 hello 설정 tooupdate hello 나머지 페이지입니다.
3. Hello 설정을 구성한 후 이동 toohello [hello 게이트웨이 만들기](#gw) 이 문서 toocreate hello 게이트웨이의 섹션입니다.

## <a name="next-steps"></a>다음 단계
* 가상 네트워크를 tooyour tooadd 가상 컴퓨터 참조 [가상 컴퓨터 경로 학습](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)합니다.
* ExpressRoute에 대 한 자세한 toolearn hello를 참조 하십시오 [ExpressRoute 개요](expressroute-introduction.md)합니다.

