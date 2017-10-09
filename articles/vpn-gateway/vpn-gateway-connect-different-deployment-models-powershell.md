---
title: "클래식 가상 네트워크 tooAzure 리소스 관리자 Vnet 연결: PowerShell | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 클래식 Vnet 및 VPN 게이트웨이 및 PowerShell을 사용 하 여 리소스 관리자 Vnet 간의 VPN 연결"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>PowerShell을 사용하여 다양한 배포 모델에서 가상 네트워크 연결



이 문서 tooconnect 클래식 Vnet tooResource 관리자 Vnet tooallow 서로 hello 별도 배포 모델 toocommunicate에 배치 된 리소스를 hello 하는 방법을 보여 줍니다. 이 문서의 단계 hello PowerShell을 사용 하지만 hello 문서가이 목록에서 선택 하 여 hello Azure 포털을 사용 하 여이 구성을 만들 수도 있습니다.

> [!div class="op_single_selector"]
> * [포털](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

비슷한 tooconnecting VNet tooan 온-프레미스 사이트 위치는 클래식 VNet tooa 리소스 관리자 VNet를 연결 합니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. 다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다. 으로 구성 된 hello 게이트웨이 동적 또는 경로 기반으로 연결 tooon 온-프레미스 네트워크에 이미 있는 Vnet을 연결할 수도 있습니다. VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다. 

Vnet hello에 있는 경우 동일한 지역 경우가 있습니다 tooinstead VNet 피어 링을 사용 하 여 연결을 것입니다. VNet 피어링은 VPN Gateway를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요. 

## <a name="before-beginning"></a>시작하기 전에

hello 다음 단계 과정을 단계별로 hello 설정 필요한 tooconfigure 동적 또는 경로 기반 게이트웨이 각 VNet에 대 한 고 hello 게이트웨이 간에 VPN 연결을 만듭니다. 이 구성은 고정 또는 정책 기반 게이트웨이를 지원하지 않습니다.

### <a name="prerequisites"></a>필수 조건

* 두 VNet이 이미 생성되었습니다.
* Vnet을 서로 중첩 하지 않거나 겹치는 hello에 대 한 주소 범위 hello hello 게이트웨이에 연결할 수 있습니다 하는 다른 연결에 대 한 hello 범위를 사용 하 여입니다.
* Hello 최신 PowerShell cmdlet을 설치 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다. 서비스 관리 (SM) hello와 hello 관리자 RM (리소스) cmdlet 설치 해야 합니다. 

### <a name="exampleref"></a>예제 설정

이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.

**클래식 VNet 설정**

VNet 이름 = ClassicVNet  <br>
Location = West US <br>
Virtual Network Address Spaces = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
GatewaySubnet = 10.0.0.32/29 <br>
Local Network Name = RMVNetLocal <br>
GatewayType = DynamicRouting

**Resource Manager VNet 설정**

VNet 이름 = RMVNet  <br>
Resource Group = RG1 <br>
Virtual Network IP Address Spaces = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Location = East US <br>
Gateway public IP name = gwpip <br>
Local Network Gateway = ClassicVNetLocal <br>
Virtual Network Gateway name = RMGateway <br>
게이트웨이 IP 주소 구성 = gwipconfig

## <a name="createsmgw"></a>섹션 1-구성 클래식 VNet hello
### <a name="part-1---download-your-network-configuration-file"></a>1부 - 네트워크 구성 파일 다운로드
1. 관리자 권한을 가진 hello PowerShell 콘솔에서 Azure 계정 tooyour에 로그인 합니다. hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다. 이 부분의 hello 구성 SM PowerShell cmdlet toocomplete hello를 사용합니다.

  ```powershell
  Add-AzureAccount
  ```
2. Hello 다음 명령을 실행 하 여 Azure 네트워크 구성 파일을 내보냅니다. Hello 위치의 hello tooexport tooa 다른 필요한 경우 파일 위치를 변경할 수 있습니다.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. 열기 hello.xml 파일 tooedit 다운로드 하는 것입니다. 예를 보려면 hello 네트워크 구성 파일 참조 hello [네트워크 구성 스키마](https://msdn.microsoft.com/library/jj157100.aspx)합니다.

### <a name="part-2--verify-hello-gateway-subnet"></a>파트 2-hello 게이트웨이 서브넷을 확인
Hello에 **VirtualNetworkSites** 요소를 하나 아직 만들어지지 않은 경우 게이트웨이 서브넷 tooyour VNet을 추가 합니다. Hello 네트워크 구성 파일에서 작업할 때는 hello 게이트웨이 서브넷 이름을 지정 해야 "GatewaySubnet" 또는 Azure에서 인식 하 고 게이트웨이 서브넷으로 사용할 수 없습니다.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**예제:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>3 부-hello 로컬 네트워크 사이트를 추가 합니다.
hello 로컬 네트워크 사이트를 추가 하면 tooconnect 원하는 RM VNet toowhich hello를 나타냅니다. 추가 **LocalNetworkSites** 요소 toohello 파일이 존재 하지 않는 경우. 이 시점에서 hello 구성에서 hello VPNGatewayAddress 수 때문일 모든 유효한 공용 IP 주소 아직 리소스 관리자 VNet hello에 대 한 hello 게이트웨이 만들지 않았습니다. Hello 게이트웨이 작성 하는 것이 자리 표시자 IP 주소를 hello 올바른 공용 IP 주소와 toohello RM 게이트웨이에 할당 된 바꿉니다.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>-4 부 hello 로컬 네트워크 사이트와 연결할 hello VNet
이 섹션에서는 원하는 tooconnect hello 로컬 네트워크 사이트 지정 VNet 대 hello 합니다. 이 경우 이전에 참조 되는 리소스 관리자 VNet hello 됩니다. 있는지 hello 이름을 일치를 확인 합니다. 이 단계에서는 게이트웨이를 만들지 않습니다. Hello 로컬 네트워크 게이트웨이 hello에에 연결을 지정 합니다.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>5 부-hello 파일을 저장 하 고, 업로드
Hello 파일을 저장 한 후 hello 다음 명령을 실행 하 여 tooAzure을 가져옵니다. 사용자 환경의 필요에 따라 hello 파일 경로 변경 해야 합니다.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Hello 가져오기 성공 했는지 보여 주는 비슷한 결과 확인할 수 있습니다.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>6 단계-hello 게이트웨이 만들기

이 예제를 실행 하기 전에 toohello 참조 hello 정확한 이름을 해당 Azure에 대 한 다운로드 한 네트워크 구성 파일에서는 toosee 합니다. 클래식 가상 네트워크에 대 한 hello 값을 포함 하는 hello 네트워크 구성 파일입니다. 경우에 따라 클래식에서 클래식 VNet 설정을 만들 때 Vnet hello 네트워크 구성 파일에서 변경 된에 대 한 hello 이름을 hello hello 배포 모델의 toohello 차이 때문에 Azure 포털입니다. 예를 들어 Azure 포털 toocreate 클래식 VNet 라는 ' 클래식 VNet' 및 'ClassicRG' 라는 리소스 그룹에서 만든 hello를 사용 하는 hello 네트워크 구성 파일에 포함 된 hello 이름이 변환된 too'Group ClassicRG 클래식 VNet 되었습니다 '. 공백이 포함 된 VNet의 hello 이름을 지정할 때 hello 값 주위에 따옴표를 사용 합니다.


다음 예제에서는 toocreate 동적 라우팅 게이트웨이 hello를 사용 합니다.

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Hello를 사용 하 여 hello 게이트웨이의 hello 상태를 확인할 수 있습니다 **Get AzureVNetGateway** cmdlet.

## <a name="creatermgw"></a>섹션 2: hello RM VNet 게이트웨이 구성 합니다.
toocreate hello RM VNet에 대 한 VPN 게이트웨이 hello 다음 지침을 따릅니다. Hello hello 클래식 VNet 게이트웨이 공용 IP 주소를 검색 한 후 hello 설명 하는 단계를 시작 하지 마십시오. 

1. Hello PowerShell 콘솔에서 Azure 계정 tooyour에 로그인 합니다. hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정은 다운로드 됩니다.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  둘 이상의 구독이 있는 경우 Azure 구독 목록을 가져옵니다.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Toouse hello 구독을 지정 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. 로컬 네트워크 게이트웨이를 만듭니다. 가상 네트워크에서 로컬 네트워크 게이트웨이 hello 일반적으로 tooyour 온-프레미스 위치를 나타냅니다. 이 경우 로컬 네트워크 게이트웨이 hello tooyour 클래식 VNet을 참조합니다. Azure 수 tooit를 참조 하 고으로 hello 주소 공간 접두사를 지정 이름을 지정 합니다. Azure는 tooidentify 어떤 트래픽 toosend tooyour 온-프레미스 위치를 지정 하는 hello IP 주소 접두사를 사용 합니다. 게이트웨이 만들기 전에 여기에서 tooadjust hello 정보 이상 필요한 경우 수정할 수 있습니다 hello 값과 실행된 hello 샘플 다시.
   
   **-이름** tooassign toorefer toohello 로컬 네트워크 게이트웨이 원하는 hello 이름입니다.<br>
   **-AddressPrefix** 는 hello 클래식 VNet에 대 한 주소 공간입니다.<br>
   **-GatewayIpAddress** 는 hello hello 클래식 VNet 게이트웨이의 공용 IP 주소입니다. Toochange hello 다음 샘플 tooreflect hello 올바른 IP 주소로 확인 해야 합니다.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. 에 대 한 공용 IP 주소 toobe toohello 할당 된 가상 네트워크 게이트웨이 리소스 관리자 VNet hello 요청 합니다. 원하는 toouse hello IP 주소를 지정할 수 없습니다. hello IP 주소 toohello 가상 네트워크 게이트웨이 동적으로 할당 됩니다. 그러나이이 hello IP 주소 변경 내용을 의미 하지 않습니다. hello 유일한 시간 hello 가상 네트워크 게이트웨이 IP 주소 변경 내용을 게이트웨이 hello 경우는 삭제 하 고 다시 됩니다. 크기 조정, 다시 설정, 또는 기타 내부 유지 관리/업그레이드 hello 게이트웨이의 바뀌지 않습니다.

  이 단계에서는 이후 단계에 사용되는 변수도 설정합니다.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. 가상 네트워크에 게이트웨이 서브넷이 있는지 확인합니다. 게이트웨이 서브넷이 없다면 추가합니다. Hello 게이트웨이 서브넷 이름이 있는지 확인 *GatewaySubnet*합니다.
5. Hello 다음 명령을 실행 하 여 hello 게이트웨이에 사용 하는 hello 서브넷을 검색 합니다. 이 단계에서는 hello 다음 단계에서 사용 되는 변수 toobe도 설정 합니다.
   
   **-이름** 리소스 관리자 VNet의 hello 이름입니다.<br>
   **-ResourceGroupName** VNet 연결 된 해당 hello hello 리소스 그룹입니다. hello 게이트웨이 서브넷이이 VNet에 이미 존재 해야 하며 이름은 *GatewaySubnet* toowork 제대로 합니다.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Hello 게이트웨이 IP 주소 지정 구성을 만듭니다. hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다. 다음 샘플 toocreate hello 게이트웨이 구성을 사용 합니다.

  이 단계에서는 hello **-SubnetId** 및 **-PublicIpAddressId** 매개 변수에 전달 해야 hello id 속성 hello 서브넷 및 IP 주소 개체의 각각. 간단한 문자열을 사용할 수 없습니다. 이러한 변수는 공용 IP hello 단계 toorequest에 설정 되 고 hello 단계 tooretrieve hello 서브넷.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Hello 다음 명령을 실행 하 여 hello 리소스 관리자 가상 네트워크 게이트웨이 만듭니다. hello `-VpnType` 해야 *RouteBased*합니다. Hello 게이트웨이 toocreate 45 분 이상 걸릴 수 있습니다.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Hello VPN 게이트웨이 만든 후 hello 공용 IP 주소를 복사 합니다. 클래식 VNet에 대 한 hello 로컬 네트워크 설정을 구성 하는 경우 해당 사용 합니다. Hello 다음 cmdlet tooretrieve hello 공용 IP 주소를 사용할 수 있습니다. hello 공용 IP 주소에에서 나열 된 hello로 반환 *IpAddress*합니다.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>섹션 3: hello 클래식 VNet 로컬 사이트 설정 수정

이 섹션에서는 작업할 hello 클래식 VNet입니다. Hello 자리 표시자 IP 주소를 사용 하는 tooconnect toohello 리소스 관리자 VNet 게이트웨이 될 hello 로컬 사이트 설정을 지정할 때 사용 되는 바꿀 있습니다. 

1. Hello 네트워크 구성 파일을 내보냅니다.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. 텍스트 편집기를 사용 하 여 VPNGatewayAddress를 hello 값을 수정 합니다. Hello hello 리소스 관리자 게이트웨이의 공용 IP 주소와 hello 자리 표시자 IP 주소를 바꾼 다음 hello 변경 내용을 저장 합니다.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. 가져오기 hello 네트워크 구성 파일 tooAzure 수정 합니다.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>섹션 4: hello 게이트웨이 간의 연결 만들기
Hello 게이트웨이 간의 연결을 만드는 PowerShell이 필요 합니다. Hello PowerShell cmdlet의 Azure 계정 toouse hello 클래식 버전 tooadd를 할 수 있습니다. toodo를 사용 하 여 **Add-azureaccount**합니다.

1. Hello PowerShell 콘솔에서 공유 키를 설정 합니다. 참조 toohello hello cmdlet을 실행 하기 전에 hello 정확한 이름을 해당 Azure에 대 한 다운로드 한 네트워크 구성 파일에서는 toosee 합니다. 공백이 포함 된 VNet의 hello 이름을 지정할 때 hello 값에 단일 따옴표를 사용 합니다.<br><br>다음 예에서 **-VNetName** hello의 hello 이름인 클래식 VNet 및 **-LocalNetworkSiteName** hello 로컬 네트워크 사이트에 대해 지정한 hello 이름입니다. hello **-에서 SharedKey** 생성 하 고 지정 하는 값입니다. Hello 예에서 'abc123' 사용 하지만 생성 하 고 조금 더 복잡 한 사용할 수 있습니다. 중요 한 점은 여기에서 지정한 hello 값 hello hello 연결을 만들 때 hello 다음 단계에서 지정 하는 같은 값 이어야 합니다. hello 반환 표시할지 **상태: 성공**합니다.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Hello 다음 명령을 실행 하 여 hello VPN 연결을 만듭니다.
   
  Hello 변수를 설정 합니다.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Hello 연결을 만듭니다. 해당 hello 확인 **-ConnectionType** ipsec, Vnet2Vnet 없습니다.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>섹션 5: 연결 확인

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>프로그램 클래식 VNet tooyour 리소스 관리자 VNet에서에서 tooverify hello 연결

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure portal

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>리소스 관리자 VNet tooyour에서 tooverify hello 연결 클래식 VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure 포털

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>VNet 간 FAQ

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

