---
title: "컴퓨터 tooan 지점-사이트를 사용 하 여 Azure 가상 네트워크를 연결 하 고 인증 인증서: PowerShell | Microsoft Docs"
description: "인증서 인증을 사용 하는 지점-사이트 VPN 게이트웨이 연결을 생성 하 여 컴퓨터 tooyour 가상 네트워크를 안전 하 게 연결 합니다. 이 문서 toohello 리소스 관리자 배포 모델을 적용 하 고는 PowerShell을 사용 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: PowerShell

이 문서에서는 PowerShell을 사용 하 여 toocreate hello 리소스 관리자 배포에서 지점 및 사이트 연결 VNet을 모델링 하는 방법을 보여 줍니다. 이 구성은 인증서 tooauthenticate hello 클라이언트 연결을 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다. 지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다. P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다.

P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다. Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.

![컴퓨터 tooan 지점 및 사이트 연결 다이어그램-Azure VNet를 연결 합니다.](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

지점 및 사이트 인증서 인증 연결 hello 다음에 필요 합니다.

* RouteBased VPN 게이트웨이입니다.
* hello tooAzure 업로드 된 루트 인증서에 대 한 공개 (키.cer 파일) 키입니다. Hello 인증서를 업로드 한 후 인증서를 신뢰할 수 있는 것으로 간주 됩니다 하 고 인증을 위해 사용 됩니다.
* Hello 루트 인증서에서 생성 되 고 toohello VNet 연결 하는 각 클라이언트 컴퓨터에 설치 되는 클라이언트 인증서입니다. 클라이언트 인증에 사용됩니다.
* VPN 클라이언트 구성 패키지. hello VPN 클라이언트 구성 패키지 hello hello 클라이언트 tooconnect toohello VNet에 대 한 필요한 정보를 포함합니다. hello 패키지 hello 기존 VPN 클라이언트는 네이티브 toohello Windows 운영 체제를 구성 합니다. 연결 하는 각 클라이언트 hello 구성 패키지를 사용 하 여 구성 되어야 합니다.

지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다. VPN 연결 hello SSTP (Secure Socket Tunneling Protocol)를 통해 생성 됩니다. Hello 서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2 지원합니다. 클라이언트 hello 어떤 버전 toouse를 결정합니다. Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다. 

지점 및 사이트 간 연결에 대 한 자세한 내용은 참조 hello [지점 및 사이트 간 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

## <a name="before-beginning"></a>시작하기 전에

* Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.
* Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다. PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

### <a name="example"></a>예제 값

Hello 예제 값 toocreate 테스트 환경을 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해 합니다. 섹션의 hello 변수 설정 [1](#declare) hello 문서의 합니다. 연습으로 hello 단계를 사용 하 고 변경 없이 hello 값을 사용 하거나 tooreflect 변경할 사용자 환경입니다. 

* **이름: VNet1**
* **주소 공간: 192.168.0.0/16** 및 **10.254.0.0/16**<br>이 예제에서는이 구성을 여러 주소 공간을 사용 하는 둘 이상의 주소 공간이 tooillustrate를 사용 합니다. 하지만 이 구성에 여러 주소 공간이 반드시 필요한 것은 아닙니다.
* **서브넷 이름: FrontEnd**
  * **서브넷 주소 범위: 192.168.1.0/24**
* **서브넷 이름: BackEnd**
  * **서브넷 주소 범위: 10.254.1.0/24**
* **서브넷 이름: GatewaySubnet**<br>hello 서브넷 이름 *GatewaySubnet* hello VPN 게이트웨이 toowork 필수 항목입니다.
  * **GatewaySubnet 주소 범위: 192.168.200.0/24** 
* **VPN 클라이언트 주소 풀: 172.16.201.0/24**<br>Toohello VNet이 지점 및 사이트 연결을 사용 하 여 연결 하는 VPN 클라이언트 hello VPN 클라이언트 주소 풀에서에서 IP 주소를 받습니다.
* **구독:** 사용 하 고 있는지 확인 하는 둘 이상의 구독이 있는 경우 hello 올바르다는 것입니다.
* **리소스 그룹: TestRG**
* **위치: 미국 동부**
* **DNS 서버: IP 주소** hello DNS 서버의 이름 확인을 위해 toouse 되도록 합니다.
* **GW 이름: Vnet1GW**
* **공용 IP 이름: VNet1GWPIP**
* **VpnType: RouteBased** 

## <a name="declare"></a>1. 로그인 및 변수 설정

이 섹션에서는 로그인 하 고이 구성에 사용 되는 hello 값을 선언 합니다. hello 선언 값 hello 예제 스크립트에 사용 됩니다. 사용자가 자신의 환경 hello 값 tooreflect를 변경 합니다. 또는 값을 선언 하는 hello를 사용 하 고 실행으로 hello 단계를 진행할 수 있습니다.

1. 상승 된 권한으로 PowerShell 콘솔을 열고 tooyour Azure 계정에에서 로그인 합니다. 이 cmdlet hello 로그인 자격 증명을 묻습니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.

  ```powershell
  Login-AzureRmAccount
  ```
2. Azure 구독 목록을 가져옵니다.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Toouse hello 구독을 지정 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. 원하는 toouse hello 변수를 선언 합니다. 다음 샘플, 필요한 경우 직접에 대 한 hello 값으로 대체 hello를 사용 합니다.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. VNet 구성

1. 리소스 그룹을 만듭니다.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Hello 명명 하 hello 가상 네트워크의 서브넷 구성 만들기 *프런트 엔드*, *백 엔드*, 및 *GatewaySubnet*합니다. 이러한 접두사 hello VNet 주소 공간에서 선언한의 일부 여야 합니다.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Hello 가상 네트워크를 만듭니다.

  이 예제에서는 hello DNS 서버는 선택 사항입니다. 값을 지정하더라도 새 DNS 서버를 만들지 않습니다. hello DNS 서버 IP 주소 지정 하는 DNS 서버가 있어야에 연결 하는 hello 리소스에 대 한 hello 이름을 확인할 수 있는 합니다. 이 예에서는 개인 IP 주소를 사용 하지만 DNS 서버의 IP 주소 hello 아닌지 가능성이 쉽습니다. 있는지 toouse 고유한 값 이어야 합니다.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. 앞에서 만든 가상 네트워크 hello에 대 한 hello 변수를 지정 합니다.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. VPN Gateway에는 공용 IP 주소가 있어야 합니다. 먼저 hello IP 주소 리소스를 요청 하 고 가상 네트워크 게이트웨이 만들 때 tooit를 참조 하십시오. hello IP 주소를 사용 hello VPN 게이트웨이 만들 때 toohello 리소스를 동적으로 할당 됩니다. 현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다. 고정 공용 IP 주소 할당을 요청할 수 없습니다. 그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에 하는 것은 아닙니다. hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다. VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.

  동적으로 할당된 공용 IP 주소를 요청합니다.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Hello VPN 게이트웨이 만들기

구성 하 고 VNet에 대 한 hello 가상 네트워크 게이트웨이 만듭니다.

* hello *-GatewayType* 해야 **Vpn** hello 및 *-VpnType* 해야 **RouteBased**합니다.
* Hello에 따라 too45 분 toocomplete을 사용할 수 있으며 VPN 게이트웨이 [게이트웨이 sku](vpn-gateway-about-vpn-gateway-settings.md) 선택 합니다.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Hello VPN 클라이언트 주소 풀이 추가

Hello VPN 게이트웨이 만들기를 완료 한 후에 hello VPN 클라이언트 주소 풀을 추가할 수 있습니다. hello VPN 클라이언트 주소 풀이 있는 hello VPN 클라이언트가 IP 주소를 받을 연결할 때 hello 범위입니다. , 연결 하는 hello 온-프레미스 위치와 또는 VNet tooconnect을 hello로 중복 되지 않는 개인 IP 주소 범위를 사용 합니다. 이 예제에서는 VPN 클라이언트 주소 풀이 hello로 선언 되는 [변수](#declare) 1 단계에서에서 합니다.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. 인증서 생성

인증서는 지점-사이트 Vpn에 대 한 Azure tooauthenticate VPN 클라이언트에 의해 사용 됩니다. Hello hello 루트 인증서 tooAzure의 공개 키 정보를 업로드 합니다. 공개 키 hello는 '신뢰할 수 있는'으로 간주 됩니다. 클라이언트 인증서 hello 신뢰할 수 있는 루트 인증서에서 생성 하 고 hello 인증서-현재 사용자/개인 인증서 저장소에서 각 클라이언트 컴퓨터에 설치 해야 합니다. 연결 toohello VNet을 시작할 때 hello 인증서는 사용 되는 tooauthenticate hello 클라이언트입니다. 

자체 서명된 인증서를 사용하는 경우 특정 매개 변수를 사용하여 만들어야 합니다. 에 대 한 hello 지침을 사용 하 여 자체 서명 된 인증서를 만들 수 있습니다 [PowerShell 및 Windows 10](vpn-gateway-certificates-point-to-site.md), Windows 10를 설정 하지 않은 경우 사용할 수 있습니다 또는 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)합니다. 자체 서명 된 루트 인증서 및 클라이언트 인증서를 생성할 때 hello 지침에 설명 된 hello 단계를 수행 합니다. 그렇지 않으면 hello 인증서 생성 P2S 연결와 호환 되지 않으며 연결 오류가 발생 합니다.

### <a name="cer"></a>1. Hello 루트 인증서에 대 한 hello.cer 파일을 가져오려면

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. 클라이언트 인증서 생성

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Hello 루트 인증서 공개 키 정보를 업로드 합니다.

VPN 게이트웨이에서 만들기가 완료되었는지 확인합니다. 완료 되 면 신뢰할 수 있는 루트 인증서 tooAzure에 대 한 (을 hello 공개 키 정보를 포함) hello.cer 파일을 업로드할 수 있습니다. A.cer 파일이 업로드 되 면 Azure 사용할 수 tooauthenticate 클라이언트 hello 신뢰할 수 있는 루트 인증서에서 생성 된 클라이언트 인증서를 설치 합니다. 필요한 경우-tooa 총 20-나중를 신뢰할 수 있는 루트 인증서 파일을 업로드할 수 있습니다.

1. 사용자 고유의 hello 값 대체에 인증서 이름에 대 한 hello 변수를 선언 합니다.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. 고유의으로 hello 파일 경로 대체 하 고 hello cmdlet을 실행 하십시오.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. 공개 키 정보 tooAzure hello를 업로드 합니다. Hello 인증서 정보를 업로드 한 후 Azure에서는 신뢰할 수 있는 루트 인증서를이 toobe에 게 고려 합니다.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Hello VPN 클라이언트 구성 패키지를 다운로드 합니다.

hello 설정을 사용 하 여 hello 기본 VPN 클라이언트를 구성 하는 클라이언트 구성 패키지와 파일은 필요한 tooconnect toohello 가상 네트워크 tooconnect tooa VNet 지점-사이트 VPN을 사용 하 여 각 클라이언트를 설치 해야 합니다. hello 네이티브 Windows VPN 클라이언트를 구성 하는 hello VPN 클라이언트 구성 패키지, 다른 또는 새로운 VPN 클라이언트를 설치 하지 않습니다. 

클라이언트 hello에 대 한 hello 아키텍처를 일치 하는 hello 버전으로 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지 hello를 사용할 수 있습니다. 지원 되는 클라이언트 운영 체제의 hello 목록 참조 hello [지점 및 사이트 연결 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

1. Hello 게이트웨이 만든 후에 생성 및 hello 클라이언트 구성 패키지를 다운로드할 수 있습니다. 이 예제에서는 64 비트 클라이언트에 대 한 hello 패키지를 다운로드합니다. Toodownload hello 32 비트 클라이언트 하려는 경우 'Amd64를'를 'x86' 바꿉니다. 또한 hello Azure 포털을 사용 하 여 hello VPN 클라이언트를 다운로드할 수 있습니다.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. 복사한 tooa 웹 브라우저 toodownload hello 패키지 hello 링크 주변 tooremove hello 따옴표 처리를 반환 하는 hello 링크를 붙여 넣습니다. 
3. 다운로드 하 고 hello 패키지 hello 클라이언트 컴퓨터에 설치 합니다. SmartScreen 팝업이 표시되면 **자세한 정보**, **실행**을 차례로 클릭합니다. Hello 패키지 tooinstall 다른 클라이언트 컴퓨터에 저장할 수도 있습니다.
4. Hello 클라이언트 컴퓨터에서 이동 너무**네트워크 설정** 클릭 **VPN**합니다. hello VPN 연결에 연결 하는 hello 가상 네트워크의 hello 이름을 보여 줍니다.

## <a name="clientcertificate"></a>8. 내보낸 클라이언트 인증서 설치

Hello 아닌 클라이언트 컴퓨터에서 toogenerate hello 클라이언트 인증서를 사용 하는 P2S toocreate 연결 tooinstall 클라이언트 인증서를 해야 합니다. 클라이언트 인증서를 설치할 때 클라이언트 인증서 hello을 내보낼 때 만든 hello 암호가 필요 합니다. 일반적으로의 hello 인증서를 두 번 클릭 하 고 설치 합니다.

Hello 클라이언트 인증서 hello 전체 인증서 체인 (즉, hello 기본값)와 함께.pfx로 내보낸 있는지 확인 합니다. 그렇지 않으면 hello 루트 인증서 정보를 hello 클라이언트 컴퓨터에 존재 하지 않는 및 hello 클라이언트 수 tooauthenticate를 제대로 수 없습니다. 자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요. 

## <a name="connect"></a>9. TooAzure 연결

1. hello 클라이언트 컴퓨터에서 tooconnect tooyour VNet tooVPN 연결 이동한 만든 hello VPN 연결을 찾습니다. 가상 네트워크 이름이 hello를 라고 합니다. **Connect**를 클릭합니다. 팝업 메시지 toousing hello 인증서 참조 나타날 수 있습니다. 클릭 **계속** toouse 상승 된 권한을 합니다. 
2. Hello에 **연결** 상태 페이지 클릭 **연결** toostart hello 연결 합니다. 표시 되 면 한 **인증서 선택** 화면에서 클라이언트 인증서 표시 된 hello toouse tooconnect 원하는 hello 하나 인지 확인 합니다. 없는 경우 hello 드롭 다운 화살표 tooselect hello 올바른 인증서를 사용 하 고 클릭 **확인**합니다.

  ![VPN 클라이언트가 tooAzure 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. 연결이 설정되었습니다.

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S 연결 문제 해결

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. 연결 확인

1. VPN 연결을 활성 상태 인지 tooverify 관리자 명령 프롬프트를 열고 실행 *ipconfig/all*합니다.
2. Hello 결과 확인 합니다. 받은 hello IP 주소가 구성에 지정 된 hello 지점-사이트 VPN 클라이언트 주소 풀 내의 hello 주소 중 하나 인지 확인 합니다. hello 결과 비슷한 toothis 예제.

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Tooa 가상 컴퓨터에 연결

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="addremovecert"></a>루트 인증서 추가 또는 제거

Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다. 루트 인증서를 제거 하면 hello 루트 인증서에서 생성 된 인증서가 있는 클라이언트를 인증할 수 없습니다 및 수 tooconnect 수 없습니다. 클라이언트 tooauthenticate 원하는 연결 하는 경우 tooinstall 루트 인증서를 신뢰할 수 있는 (업로드) tooAzure에서 새 클라이언트 인증서를 생성 해야 합니다.

### <a name="addtrustedroot"></a>tooadd 신뢰할 수 있는 루트 인증서

Too20 루트 인증서.cer 파일 tooAzure를 추가할 수 있습니다. hello 다음 단계에서는 루트 인증서를 추가 합니다.

#### <a name="certmethod1"></a>방법 1

이 hello 가장 효율적인 방법 tooupload 루트 인증서입니다.

1. .Cer 파일 tooupload hello를 준비 합니다.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Hello 파일을 업로드 합니다. 한 번에 하나의 파일만 업로드할 수 있습니다.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify 해당 hello 인증서 파일을 업로드 합니다.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>방법 2

방법 1 보다 더 많은 단계를가지고 있지만이 메서드는 동일한 결과 hello 합니다. Tooview hello 인증서 데이터를 필요한 경우에 포함 되어 있습니다.

1. 만들고 hello 새 루트 인증서 tooadd tooAzure를 준비 합니다. E-64로 인코딩된 X.509 대로 hello 공개 키를 내보냅니다 (합니다. CER) 하 고 텍스트 편집기로 엽니다. 다음 예제는 hello와 같이 hello 값을 복사 합니다.

  ![인증서](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Hello 인증서 데이터를 복사할 때 캐리지 리턴 또는 줄 바꿈 없이 한 연속 줄으로 hello 텍스트를 복사 해야 합니다. Toomodify hello 텍스트 편집기 too'Show 기호/표시 모든 문자 toosee hello 캐리지 리턴 및 줄에서 보기를 할 수 있습니다.
  >
  >

2. 변수로 hello 인증서 이름 및 키 정보를 지정 합니다. 다음 예제에서는 사용자 고유의 hello에서와 같이 hello 정보를 바꿉니다.

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Hello 새 루트 인증서를 추가 합니다. 한번에 하나의 인증서만 추가할 수 있습니다.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. 다음 예제는 hello를 사용 하 여 해당 hello 새 인증서가 올바르게에 추가 하는 것을 확인할 수 있습니다.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove 루트 인증서

1. Hello 변수를 선언 합니다.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Hello 인증서를 제거 합니다.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. 사용 하 여 hello 인증서 hello 예제 tooverify 다음를 제거 했습니다.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>클라이언트 인증서 해지

클라이언트 인증서를 해지할 수 있습니다. hello 인증서 해지 목록을 통해 tooselectively 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 연결을 거부 합니다. 이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다. Azure에서 신뢰할 수 있는 루트 인증서.cer를 제거 하면 모든 클라이언트 인증서를 서명 생성/된 hello 해지 된 루트 인증서에 의해 hello 액세스 권한을 취소 합니다. 클라이언트 인증서를 해지 hello 루트 인증서를 대신 허용 hello 인증에 사용 하는 hello 루트 인증서 toocontinue toobe에서 생성 된 다른 인증서입니다.

hello 일반적으로 개별 사용자에 대 한 세분화 된 액세스 제어에 대 한 해지 된 클라이언트 인증서를 사용 하는 동안 팀 또는 조직 수준에서 toouse hello 루트 인증서 toomanage 액세스가 됩니다.

### <a name="revokeclientcert"></a>toorevoke 클라이언트 인증서

1. Hello 클라이언트 인증서 지문을 검색 합니다. 자세한 내용은 참조 [어떻게 tooretrieve hello 인증서의 지문을](https://msdn.microsoft.com/library/ms734695.aspx)합니다.
2. Hello 정보 tooa 텍스트 편집기를 복사 하 고 모든 공백을 제거 하는 연속 문자열. 이 문자열은 hello 다음 단계에서 변수로 선언 합니다.
3. Hello 변수를 선언 합니다. 검색 있는지 toodeclare hello 지문 hello 이전 단계에서 확인 하십시오.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. 해지 된 인증서의 hello 지문 toohello 목록을 추가 합니다. Hello 지문을 추가 될 때 "Succeeded"를 참조 하십시오.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. 해당 hello 지문 toohello 인증서 해지 목록에 추가 되었는지 확인

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Hello 지문을 추가 된 후 hello 인증서 사용된 tooconnect를 더 이상 수 없습니다. Tooconnect이이 인증서를 사용 하 여 시도 하는 클라이언트 hello 인증서를 더 이상 사용할 수 없다는 메시지를 수신 합니다.

### <a name="reinstateclientcert"></a>tooreinstate 클라이언트 인증서

Hello 지문 hello 해지 된 클라이언트 인증서 목록에서 제거 하 여 클라이언트 인증서를 복원할 수 있습니다.

1. Hello 변수를 선언 합니다. Tooreinstate hello 인증서에 대 한 올바른 지문을 hello를 선언 해야 합니다.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Hello 인증서 지문을 hello 인증서 해지 목록에서 제거 합니다.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Hello 지문 hello 해지 목록에서 제거 되 면 확인 합니다.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>지점 및 사이트 간 FAQ

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>다음 단계
연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요. 네트워킹 및 가상 컴퓨터에 대해 자세히 toounderstand 참조 [Azure와 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)합니다.
