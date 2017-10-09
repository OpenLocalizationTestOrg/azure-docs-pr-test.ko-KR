---
title: "Azure 가상 네트워크 tooanother VNet 연결: 포털 | Microsoft Docs"
description: "리소스 관리자를 사용 하 여 Vnet 간의 VPN 게이트웨이 연결을 만들고 Azure 포털 hello 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a7015cfc-764b-46a1-bfac-043d30a275df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: a529f90d976bee0f50403947d06e9da8a6c05349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 VNet 대 VNet VPN 게이트웨이 연결 구성

이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다. hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다. Hello 구독이 다른 구독에서 연결 Vnet toobe hello와 관련 된 필요 하지 않는 경우 동일한 Active Directory 테 넌 트. 

이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용 하 고 hello Azure 포털을 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [다양한 배포 모델 간 연결 - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [다양한 배포 모델 간 연결 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![v2v 다이어그램](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v2vrmps.png)

가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. Vnet hello에 있는 경우 동일한 지역 VNet 피어 링을 사용 하 여 연결 tooconsider 할 수 있습니다. VNet 피어링은 VPN Gateway를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.

VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다. 이렇게 하면 hello 다음 다이어그램에에서 나와 있는 것 처럼 가상 네트워크 간 연결 되 면 크로스-프레미스 연결을 결합 하는 네트워크 토폴로지를 설정할 수 있습니다.

![연결 정보](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/aboutconnections.png "About connections")

### <a name="why-connect-virtual-networks"></a>가상 네트워크에 연결하는 이유

다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.

* **지역 간 지리적 중복 및 지리적 상태**
  
  * 인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.
  * Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다. 한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.
* **분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**
  
  * 내 동일한 hello 영역을 설정할 수 있습니다 다층 계층 응용 프로그램 기한 tooisolation 또는 관리 요구를 함께 연결 하는 여러 가상 네트워크가 됩니다.

VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다. Vnet 서로 다른 구독에 있는 경우 hello 포털에서 hello 연결을 만들 수 없다는 참고 합니다. [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 또는 [CLI](vpn-gateway-howto-vnet-vnet-cli.md)를 사용할 수 있습니다.

### <a name="values"></a>예제 설정

연습으로 이러한 단계를 사용 하는 경우에 hello 예제 설정 값을 사용할 수 있습니다. 예제에서는 각 VNet에 대한 여러 주소 공간을 사용합니다. 그러나 VNet 간 구성에는 여러 개의 주소 공간이 필요하지 않습니다.

**TestVNet1에 대한 값:**

* VNet 이름: TestVNet1
* 주소 공간: 10.11.0.0/16
  * 서브넷 이름: FrontEnd
  * 서브넷 주소 범위: 10.11.0.0/24
* 리소스 그룹: TestRG1
* 위치: 미국 동부
* 주소 공간: 10.12.0.0/16
  * 서브넷 이름: BackEnd
  * 서브넷 주소 범위: 10.12.0.0/24
* 게이트웨이 서브넷 이름: GatewaySubnet (hello 포털에서 자동 채우기 됩니다)
  * 게이트웨이 서브넷 주소 범위: 10.11.255.0/27
* DNS 서버의 IP 주소를 hello를 사용 하는 DNS 서버:
* Virtual Network 게이트웨이 이름: TestVNet1GW
* 게이트웨이 유형: VPN
* VPN 유형: 경로 기반
* SKU: hello toouse 게이트웨이 SKU를 선택 합니다.
* 공용 IP 주소 이름: TestVNet1GWIP
* 연결 값:
  * 이름: TestVNet1toTestVNet4
  * 공유 키: hello 공유 키를 직접 만들 수 있습니다. 이 예제에서는 abc123을 사용합니다. hello 중요 한 점은 hello Vnet 간의 hello 연결을 만들 때 hello 값 일치 해야 합니다.

**TestVNet4에 대한 값:**

* VNet 이름: TestVNet4
* 주소 공간: 10.41.0.0/16
  * 서브넷 이름: FrontEnd
  * 서브넷 주소 범위: 10.41.0.0/24
* 리소스 그룹: TestRG1
* 위치: 미국 서부
* 주소 공간: 10.42.0.0/16
  * 서브넷 이름: BackEnd
  * 서브넷 주소 범위: 10.42.0.0/24
* GatewaySubnet 이름: GatewaySubnet (hello 포털에서 자동 채우기 됩니다)
  * 게이트웨이 서브넷 주소 범위: 10.41.255.0/27
* DNS 서버의 IP 주소를 hello를 사용 하는 DNS 서버:
* Virtual Network 게이트웨이 이름: TestVNet4GW
* 게이트웨이 유형: VPN
* VPN 유형: 경로 기반
* SKU: hello toouse 게이트웨이 SKU를 선택 합니다.
* 공용 IP 주소 이름: TestVNet4GWIP
* 연결 값:
  * 이름: TestVNet4toTestVNet1
  * 공유 키: hello 공유 키를 직접 만들 수 있습니다. 이 예제에서는 abc123을 사용합니다. hello 중요 한 점은 hello Vnet 간의 hello 연결을 만들 때 hello 값 일치 해야 합니다.

## <a name="CreatVNet"></a>1. TestVNet1 만들기 및 구성
VNet 이미 있는 경우 hello 설정이 VPN 게이트웨이 설계와 호환 되는지 확인 합니다. 특히 주의 tooany 서브넷이 다른 네트워크와 겹칠 수 있습니다. 겹치는 서브넷에 있으면 연결이 제대로 작동하지 않습니다. VNet을 hello 올바른 설정으로 구성 된 경우 hello의 hello 단계를 시작할 수 있습니다 [DNS 서버 지정](#dns) 섹션.

### <a name="toocreate-a-virtual-network"></a>toocreate 가상 네트워크
[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-rm-portal-include.md)]

## <a name="subnets"></a>2. 다른 주소 공간 추가 및 서브넷 만들기
VNet이 만들어지면 여기에 다른 주소 공간을 추가하고 서브넷을 만들 수 있습니다.

[!INCLUDE [vpn-gateway-additional-address-space](../../includes/vpn-gateway-additional-address-space-include.md)]

## <a name="gatewaysubnet"></a>3. 게이트웨이 서브넷 만들기
가상 네트워크 tooa 게이트웨이 연결 하기 전에 먼저 toocreate hello 게이트웨이 서브넷 tooconnect 원하는 가상 네트워크 toowhich hello에 대 한 합니다. 가능 하면 것 최상의 toocreate 순서 tooprovide에 CIDR 블록/28/27 등의 사용 하는 게이트웨이 서브넷 충분 한 IP tooaccommodate 앞으로 추가 구성 요구 사항을 충족 합니다.

연습으로이 구성을 만드는 경우 참조 toothese [설정 예](#values) 게이트웨이 서브넷을 만들 때.

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="toocreate-a-gateway-subnet"></a>게이트웨이 서브넷 toocreate
[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

## <a name="dns"></a>4. DNS 서버 지정(선택 사항)
DNS는 VNet 간 연결에 필요하지 않습니다. 그러나 tooyour 배포 된 가상 네트워크 리소스에 대 한 toohave 이름 확인 하려는 경우에 DNS 서버를 지정 해야 합니다. 이 설정을 사용 하면이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 hello DNS 서버를 지정할 수 있습니다. DNS 서버를 만들지 않습니다.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="VNetGateway"></a>5. 가상 네트워크 게이트웨이 만들기
이 단계에서는 VNet에 대 한 hello 가상 네트워크 게이트웨이 만듭니다. 게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다. 연습으로이 구성을 만드는 경우 toohello 참조할 수 있습니다 [설정 예](#values)합니다.

### <a name="toocreate-a-virtual-network-gateway"></a>가상 네트워크 게이트웨이 toocreate
[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

## <a name="CreateTestVNet4"></a>6. TestVNet4 만들기 및 구성
TestVNet1 구성한 경우 TestVNet4 TestVNet4의 hello 값을 대체 하는 hello 이전 단계를 반복 하 여 만듭니다. TestVNet1에 대 한 가상 네트워크 게이트웨이 hello TestVNet4 구성 하기 전에 만들기 끝날 때까지 toowait이 필요는 없습니다. 사용자가 직접 값을 사용 하는 hello 주소 공간을 tooconnect 원하는 Vnet hello를 사용 하 여 겹치지 않는지 확인 합니다.

## <a name="TestVNet1Connection"></a>7. Hello TestVNet1 연결 구성
Hello 가상 네트워크 게이트웨이 TestVNet1 및 TestVNet4 모두 완료 했을 때 게이트웨이 연결 가상 네트워크를 만들 수 있습니다. 이 섹션에서는 VNet1 tooVNet4에서 연결을 만듭니다. 다음이 단계 동일 하 게 작동 hello에 Vnet에 대해서만 구독 합니다. Vnet 서로 다른 구독에 있는 경우 PowerShell toomake hello 연결을 사용 해야 합니다. Hello 참조 [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md) 문서.

1. **모든 리소스**, VNet에 대 한 toohello 가상 네트워크 게이트웨이 이동 합니다. 예를 들어 **TestVNet1GW**로 이동합니다. 클릭 **TestVNet1GW** tooopen hello 가상 네트워크 게이트웨이 블레이드입니다.
   
    ![연결 블레이드](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/settings_connection.png "Connections blade")
2. 클릭 **+ 추가** tooopen hello **연결 추가** 블레이드입니다.
3. Hello에 **연결 추가** 블레이드에서 hello 이름 필드에 입력 한 연결에 대 한 이름입니다. 예를 들어, **TestVNet1toTestVNet4**를 입력합니다.
   
    ![연결 이름](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/v1tov4.png "Connection name")
4. **연결 형식**은 선택 **VNet 대 VNet** hello 드롭다운에서 합니다.
5. hello **첫 번째 가상 네트워크 게이트웨이** 이 연결을 작성 하는 hello 지정 된 가상 네트워크 게이트웨이에서 자동으로 필드 값은 채워집니다.
6. hello **두 번째 가상 네트워크 게이트웨이** 필드는 hello VNet의 가상 네트워크 게이트웨이 hello 되도록 toocreate에 대 한 연결 합니다. 클릭 **다른 가상 네트워크 게이트웨이 선택** tooopen hello **가상 네트워크 게이트웨이 선택** 블레이드입니다.
   
    ![연결 추가](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/add_connection.png "Add a connection")
7. 이 블레이드에 나열 된 보기 hello 가상 네트워크 게이트웨이 구독에 있는 가상 네트워크 게이트웨이만 나열되어 있는지 확인합니다. 구독에 있지 않은 tooconnect tooa 가상 네트워크 게이트웨이 원하는 경우 hello를 사용 하십시오 [PowerShell 문서](vpn-gateway-vnet-vnet-rm-ps.md)합니다. 
8. Hello 가상 네트워크 게이트웨이를 tooconnect를 클릭 합니다.
9. Hello에 **공유 키** 필드 연결에 대 한 공유 키를 입력 합니다. 이 키를 생성하거나 직접 만들 수 있습니다. 사이트 간 연결에 사용 되는 hello 키가 수 정확히 hello 온-프레미스 장치 및 가상 네트워크 게이트웨이 연결에 대 한 동일한 합니다. hello 개념은 비슷하지만 여기에서 점을 제외 하 고 tooanother 가상 네트워크 게이트웨이 연결 하려는 연결 tooa VPN 장치를 대신 합니다.
   
    ![공유 키](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/sharedkey.png "Shared key")
10. 클릭 **확인** 에 hello hello 블레이드 toosave 맨 변경 내용을 합니다.

## <a name="TestVNet4Connection"></a>8. Hello TestVNet4 연결 구성
다음으로 TestVNet4 tooTestVNet1에서 연결을 만듭니다. 사용 하 여 hello 동일 toocreate hello 연결 TestVNet1 tooTestVNet4에서 사용 되는 방법입니다. Hello를 사용 하면 동일한 키를 공유 합니다.

## <a name="VerifyConnection"></a>9. 연결 확인
Hello 연결을 확인 합니다. 각 가상 네트워크 게이트웨이에 대 한 않습니다 hello를 수행 합니다.

1. Hello 가상 네트워크 게이트웨이에 대 한 hello 블레이드를 찾습니다. 예를 들어 **TestVNet4GW**를 찾습니다. 
2. Hello 가상 네트워크 게이트웨이 블레이드에서 클릭 **연결** tooview hello 연결 블레이드 hello 가상 네트워크 게이트웨이에 대 한 합니다.

Hello 연결을 표시 하 고 hello 상태를 확인 합니다. Hello 연결을 만들고 나타납니다 **Succeeded** 및 **연결 됨** hello 상태 값으로.

![성공](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connected.png "Succeeded")

개별적으로 각 연결을 두 번 수 tooview hello 연결에 대 한 자세한 정보.

![Essentials](./media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/essentials.png "Essentials")

## <a name="faq"></a>VNet 간 FAQ
VNet 대 VNet 연결에 대 한 추가 정보에 대 한 hello FAQ 정보를 봅니다.

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>다음 단계
연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. Hello 참조 [가상 컴퓨터 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) 자세한 정보에 대 한 합니다.
