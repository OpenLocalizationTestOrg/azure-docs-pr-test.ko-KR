---
title: "Azure 가상 네트워크 tooanother VNet 연결: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure 리소스 관리자 및 PowerShell을 사용하여 가상 네트워크를 함께 연결하는 과정을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>PowerShell을 사용하여 VNet-VNet VPN Gateway 연결 구성

이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다. hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다. Hello 구독이 다른 구독에서 연결 Vnet toobe hello와 관련 된 필요 하지 않는 경우 동일한 Active Directory 테 넌 트. 

이 문서의 단계 hello toohello 리소스 관리자 배포 모델을 적용 하 고 PowerShell을 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [다양한 배포 모델 간 연결 - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [다양한 배포 모델 간 연결 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. Vnet hello에 있는 경우 동일한 지역 VNet 피어 링을 사용 하 여 연결 tooconsider 할 수 있습니다. VNet 피어링은 VPN Gateway를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.

VNet-VNet 통신을 다중 사이트 구성과 결합할 수 있습니다. 이렇게 하면 hello 다음 다이어그램에에서 나와 있는 것 처럼 가상 네트워크 간 연결 되 면 크로스-프레미스 연결을 결합 하는 네트워크 토폴로지를 설정할 수 있습니다.

![연결 정보](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>가상 네트워크에 연결하는 이유

다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.

* **지역 간 지리적 중복 및 지리적 상태**

  * 인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.
  * Azure Traffic Manager 및 부하 분산 장치를 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다. 한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.
* **분리 또는 관리 경계를 가진 지역별 다중 계층 응용 프로그램**

  * 내 동일한 hello 영역을 설정할 수 있습니다 다층 계층 응용 프로그램 기한 tooisolation 또는 관리 요구를 함께 연결 하는 여러 가상 네트워크가 됩니다.

VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

## <a name="which-set-of-steps-should-i-use"></a>어느 단계 집합을 사용해야 합니까?

이 문서에서는 서로 다른 두 집합의 단계를 볼 수 있습니다. 일련의 절차에 대 한 [Vnet에 상주 하는 동일한 구독 hello](#samesub), 용이고 다른 하나는 [서로 다른 구독에 있는 Vnet](#difsub)합니다. hello hello 집합 간의 주요 차이점은 만들어 hello 내의 모든 가상 네트워크 및 게이트웨이 리소스를 구성 하는 여부 같은 PowerShell 세션입니다.

hello 단계가이 문서에서 사용 하 여 각 섹션의 hello 시작 부분에 선언 된 변수입니다. 이미 사용 하는 기존 Vnet을 하는 경우에 사용자 환경에 hello 변수 tooreflect hello 설정을 수정 합니다. 가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.

## <a name="samesub"></a>어떻게 tooconnect Vnet에에서 있는 hello 동일한 구독

![v2v 다이어그램](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>시작하기 전에

시작 하기 전에, tooinstall hello 최신 버전의 hello Azure 리소스 관리자 PowerShell cmdlet, 적어도 4.0 이상 필요 합니다. Hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

### <a name="Step1"></a>1단계 - IP 주소 범위 계획

다음 단계는 hello, 두 가상 네트워크와 해당 게이트웨이 서브넷 및 구성을 만듭니다. Hello 간의 VPN 연결이 두 Vnet 다음 만듭니다. 네트워크 구성에 대 한 중요 한 tooplan hello IP 주소 범위는 따라서 VNet 범위 또는 로컬 네트워크 범위가 겹치지 않는지 확인해야 합니다. 이 예에서는 DNS 서버를 포함하지 않습니다. 가상 네트워크의 이름 확인을 원하는 경우 [이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.

다음 hello 예제에는 값에는 hello를 사용 합니다.

**TestVNet1에 대한 값:**

* VNet 이름: TestVNet1
* 리소스 그룹: TestRG1
* 위치: 미국 동부
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* 프런트 엔드: 10.11.0.0/24
* 백 엔드: 10.12.0.0/24
* 게이트웨이 서브넷 = 10.12.255.0/27
* 게이트웨이 이름: VNet1GW
* 공용 IP: VNet1GWIP
* VpnType: 경로 기반
* 연결(1 대 4): VNet1 대 VNet4
* 연결(1 대 5): VNet1 대 VNet5
* 연결 유형: VNet 간

**TestVNet4에 대한 값:**

* VNet 이름: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* 프런트 엔드: 10.41.0.0/24
* 백 엔드: 10.42.0.0/24
* 게이트웨이 서브넷: 10.42.255.0/27
* 리소스 그룹: TestRG4
* 위치: 미국 서부
* 게이트웨이 이름: VNet4GW
* 공용 IP: VNet4GWIP
* VpnType: 경로 기반
* 연결: VNet4 대 VNet1
* 연결 유형: VNet 간


### <a name="Step2"></a>2단계 - TestVNet1 만들기 및 구성

1. 변수 선언. 이 예제에서는이 연습에 대 한 hello 값을 사용 하는 hello 변수를 선언 합니다. 대부분의 경우에서 자신의 hello 값 바꿔야 합니다. 그러나 이러한 유형의 구성에 잘 알고 hello 단계 toobecome를 통해 실행 하는 경우에 이러한 변수를 사용할 수 있습니다. 필요한 경우 hello 변수를 수정 복사 및 PowerShell 콘솔에 붙여 넣습니다.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Tooyour 계정을 연결 하세요. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  Hello 계정에 대 한 hello 구독을 확인 합니다.

  ```powershell
  Get-AzureRmSubscription
  ```

  Toouse hello 구독을 지정 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. 새 리소스 그룹을 만듭니다.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Hello TestVNet1에 대 한 서브넷 구성을 만듭니다. 이 예제에서는 TestVNet1이라는 가상 네트워크와 GatewaySubnet, FrontEnd 및 Backend라는 세 개의 서브넷을 만듭니다. 값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다. 다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.

  hello 다음 예제에서는 이전에 설정 하는 hello 변수. 이 예제에서는 hello 게이트웨이 서브넷에 / 27을 사용 중입니다. 가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, 적어도/28 또는/27 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다. 이렇게 하면 충분 한 주소 tooaccommodate 가능한 추가 되는 구성에 만한 hello 이후 있습니다.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. TestVNet1 만들기.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. 공용 IP 주소 toobe 할당 된 toohello 게이트웨이 만들려는 VNet에 대 한 요청 합니다. 해당 hello AllocationMethod 동적 점에 유의 하십시오. 원하는 toouse hello IP 주소를 지정할 수 없습니다. 그는 동적으로 할당 된 tooyour 게이트웨이입니다. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Hello 게이트웨이 구성을 만듭니다. hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다. Hello 예제 toocreate 게이트웨이 구성을 사용 합니다.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. TestVNet1에 대 한 hello 게이트웨이 만듭니다. 이 단계에서는 TestVNet1 프로그램에 대 한 hello 가상 네트워크 게이트웨이 만듭니다. VNet-VNet 구성에는 RouteBased VpnType이 필요합니다. 게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>3단계 - TestVNet4 만들기 및 구성

TestVNet1 구성이 끝나면 TestVNet4를 만듭니다. 아래 레이블과 필요할 때 hello 값 대체 hello 단계를 수행 합니다. 이 단계를 수행할 수 hello 내에서 동일한 PowerShell 세션에 있기 때문에 hello 동일 구독 합니다.

1. 변수 선언. 수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. 새 리소스 그룹을 만듭니다.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Hello TestVNet4에 대 한 서브넷 구성을 만듭니다.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. TestVNet4 만들기.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. 공용 IP 주소를 요청합니다.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Hello 게이트웨이 구성을 만듭니다.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Hello TestVNet4 게이트웨이 만듭니다. 게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>4 단계-hello 연결 만들기

1. 두 개의 가상 네트워크 게이트웨이 모두 가져오기. Hello 게이트웨이 둘 다 hello에 하는 경우 동일한 구독 hello에이 단계를 완료 하려면 hello 예제에 있는 것 처럼 동일한 PowerShell 세션입니다.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Hello TestVNet1 tooTestVNet4 연결을 만듭니다. 이 단계에서 TestVNet1 tooTestVNet4 hello 연결을 만듭니다. Hello 예제에서 참조 하는 공유 키를 볼 수 있습니다. Hello 공유 키에 대 한 사용자 지정 값을 사용할 수 있습니다. 두 연결에 대 한 중요 한 점은 그 hello 공유 키 hello 일치 해야 합니다. 연결 만들기 toocomplete 잠시를 걸릴 수 있습니다.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Hello TestVNet4 tooTestVNet1 연결을 만듭니다. 이 단계에서 TestVNet4 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다. Hello 공유 키와 일치 하는지 확인 합니다. 몇 분 후 hello 연결이 설정 됩니다.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. 연결을 확인합니다. Hello 섹션을 참조 [어떻게 tooverify 연결](#verify)합니다.

## <a name="difsub"></a>어떻게 tooconnect Vnet에에서 있는 서로 다른 구독

![v2v 다이어그램](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

이 시나리오에서는 TestVNet1 및 TestVNet5를 연결합니다. TestVNet1 및 TestVNet5는 다른 구독에 상주합니다. hello 구독 hello와 관련 된 toobe 불필요 동일한 Active Directory 테 넌 트입니다. 이러한 단계 및 hello 이전 집합의 hello 차이점 hello 두 번째 구독의 hello 컨텍스트에서 별도 PowerShell 세션에서 수행 하는 toobe hello 구성 단계 중 일부에 필요 하다는 것입니다. 특히 때 hello 두 구독 속해 toodifferent 조직 합니다.

### <a name="step-5---create-and-configure-testvnet1"></a>5단계 - TestVNet1 만들기 및 구성

완료 해야 [1 단계](#Step1) 및 [2 단계](#Step2) 이전 hello에서 toocreate 섹션 TestVNet1를 구성 하 고 TestVNet1에 대 한 VPN 게이트웨이 hello 합니다. 이 구성에 대 한 하지 않으므로 필요한 toocreate TestVNet4 hello 이전 섹션에서 다음이 단계와 충돌을 만들지 않는 경우 하지 않지만. 6 단계 toocreate TestVNet5 단계 1 및 2 단계를 완료 한 후 계속 합니다. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>6 단계-hello IP 주소 범위를 확인 합니다.

것이 중요 한 toomake hello 새 가상 네트워크를 TestVNet5의 hello IP 주소 공간 VNet 범위 또는 로컬 네트워크 게이트웨이 범위와 겹치지 않습니다. 이 예제에서는 가상 네트워크 hello toodifferent 조직 속할 수 있습니다. 이 연습에서는 다음 TestVNet5 hello에 대 한 값에는 hello를 사용할 수 있습니다.

**TestVNet5에 대한 값:**

* VNet 이름: TestVNet5
* 리소스 그룹: TestRG5
* 위치: 일본 동부
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* 프런트 엔드: 10.51.0.0/24
* 백 엔드: 10.52.0.0/24
* 게이트웨이 서브넷: 10.52.255.0.0/27
* 게이트웨이 이름: VNet5GW
* 공용 IP: VNet5GWIP
* VpnType: 경로 기반
* 연결: VNet5 대 VNet1
* 연결 유형: VNet 간

### <a name="step-7---create-and-configure-testvnet5"></a>7단계 - TestVNet5 만들기 및 구성

이 단계는 새 구독 hello의 hello 컨텍스트에서 수행 되어야 합니다. Hello 구독을 소유 하는 다른 조직의 관리자에 게가이 부분을 수행할 수 있습니다.

1. 변수 선언. 수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Toosubscription 5를 연결 합니다. PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다. 다음 샘플 toohelp 연결한 hello를 사용 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  Hello 계정에 대 한 hello 구독을 확인 합니다.

  ```powershell
  Get-AzureRmSubscription
  ```

  Toouse hello 구독을 지정 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. 새 리소스 그룹을 만듭니다.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Hello TestVNet5에 대 한 서브넷 구성을 만듭니다.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. TestVNet5 만들기.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. 공용 IP 주소를 요청합니다.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Hello 게이트웨이 구성을 만듭니다.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Hello TestVNet5 게이트웨이 만듭니다.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>8 단계-hello 연결 만들기

이 예제에서는 hello 게이트웨이 hello 서로 다른 구독에 있기 때문에 म 했습니다 분할할이 단계 두 [구독 1]로 표시 된 PowerShell 세션 및 [구독 5].

1. **[1 구독]**  Hello 구독 1에 대 한 가상 네트워크 게이트웨이 가져오기. 로그인 하 고 hello 다음 예제를 실행 하기 전에 tooSubscription 1을 연결 합니다.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Hello 요소 다음의 hello 출력 복사한 구독 5 이러한 toohello 관리자 전자 메일 또는 다른 방법을 통해 보냅니다.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  이 두 요소 값 비슷한 toohello 예제 출력 다음에 적용 됩니다.

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[구독 5]**  Hello 5 구독에 대 한 가상 네트워크 게이트웨이 가져오기. 로그인 하 고 hello 다음 예제를 실행 하기 전에 5 tooSubscription 연결:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Hello 요소 다음의 hello 출력 복사한 구독 1 이러한 toohello 관리자 전자 메일 또는 다른 방법을 통해 보냅니다.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  이 두 요소 값 비슷한 toohello 예제 출력 다음에 적용 됩니다.

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[1 구독]**  Hello TestVNet1 tooTestVNet5 연결을 만듭니다. 이 단계에서 TestVNet1 tooTestVNet5 hello 연결을 만듭니다. hello 차이점은 다른 구독에 있기 때문에 해당 $vnet5gw 직접 가져올 수 없습니다. 위의 hello 단계에서 구독 1에서 통신 하는 hello 값으로 toocreate 새 PowerShell 개체가 필요 합니다. 다음 예제에서는 hello를 사용 합니다. Hello 이름, Id 및 공유 키를 원하는 값으로 대체 합니다. 두 연결에 대 한 중요 한 점은 그 hello 공유 키 hello 일치 해야 합니다. 연결 만들기 toocomplete 잠시를 걸릴 수 있습니다.

  다음 예제는 hello를 실행 하기 전에 tooSubscription 1을 연결 합니다.

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[구독 5]**  Hello TestVNet5 tooTestVNet1 연결을 만듭니다. 이 단계에서 TestVNet5 tooTestVNet1 hello 연결을 만드는 점을 제외 하 고 위에 나온 비슷한 toohello 것입니다. 구독 1에서 얻은 hello 값을 기반으로 하는 PowerShell 개체를 만드는 동일한 과정도 적용 됩니다 여기 번호입니다. 이 단계에서는 공유 hello 키와 일치 해야 합니다.

  다음 예제는 hello를 실행 하기 전에 tooSubscription 5를 연결 합니다.

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>어떻게 tooverify 연결

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>VNet 간 FAQ

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>다음 단계

* 연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. Hello 참조 [가상 컴퓨터 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) 자세한 정보에 대 한 합니다.
* BGP에 대 한 정보를 참조 hello [BGP 개요](vpn-gateway-bgp-overview.md) 및 [어떻게 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)합니다.
