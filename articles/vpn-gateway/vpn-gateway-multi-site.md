---
title: "VPN 게이트웨이 및 PowerShell을 사용 하 여 가상 네트워크 toomultiple 사이트 연결: 클래식 | Microsoft Docs"
description: "이 문서에서는 여러 로컬 온-프레미스 사이트 tooa 가상 네트워크 VPN 게이트웨이 사용 하 여 hello 클래식 배포 모델에 연결 하는 과정을 안내 합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>사이트 간 연결 tooa VNet (클래식) 기존 VPN 게이트웨이 연결 된 추가

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell(클래식)](vpn-gateway-multi-site.md)
>
>

이 문서의 PowerShell tooadd 사이트 및 사이트 간 (S2S) 연결 tooa VPN 게이트웨이 기존 연결이 있는 사용 하 여 안내 합니다. 이 연결의 형식은 종종 참조 tooas "멀티 사이트" 구성 합니다. hello이 문서의 단계 적용 toovirtual 네트워크 hello 클래식 배포 모델 (서비스 관리 라고 함)를 사용 하 여 생성 됩니다. 이러한 단계는 tooExpressRoute /-사이트 공존할 연결 구성 적용 되지 않습니다.

### <a name="deployment-models-and-methods"></a>배포 모델 및 메서드

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

새 문서 및 추가 도구를 이 구성에 사용할 수 있게 되었으므로 다음 표를 업데이트합니다. 문서를 사용할 수 있는이 테이블에서 tooit을 연결 직접 합니다.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>연결 정보

여러 온-프레미스 사이트 tooa 단일 가상 네트워크를 연결할 수 있습니다. 이 방식은 하이브리드 클라우드 솔루션을 구축하는 경우 특히 유용합니다. 다중 사이트 연결 tooyour Azure 가상 네트워크 게이트웨이 만들기는 비슷한 toocreating 다른 사이트 간 연결입니다. 실제로 hello 게이트웨이 동적으로 기존 Azure VPN 게이트웨이 사용할 수 있습니다 (경로 기반).

정적 게이트웨이에 연결 된 tooyour 가상 네트워크를 이미 있는 경우 순서 tooaccommodate 다중 사이트에 toorebuild hello 가상 네트워크 필요 없이 게이트웨이 유형 toodynamic hello를 변경할 수 있습니다. Hello 라우팅 유형을 변경 하기 전에 온-프레미스 VPN 게이트웨이 경로 기반 VPN 구성을 지원 하는지 확인 합니다.

![다중 사이트 다이어그램](./media/vpn-gateway-multi-site/multisite.png "다중 사이트")

## <a name="points-tooconsider"></a>포인트 tooconsider

**수 toouse hello 포털 toomake 변경 toothis 가상 네트워크 수 없습니다.** Hello 포털을 사용 하는 대신 toomake 변경 toohello 네트워크 구성 파일이 필요 합니다. Hello 포털에서 변경한 경우이 가상 네트워크에 대 한 다중 사이트 참조 설정을 덮어씁니다.

잘 알고 hello 시간별 hello 네트워크 구성 파일을 사용 하 여 hello 다중 사이트 절차를 완료 했습니다. 그러나 네트워크 구성에 사용 하는 여러 사용자를 설정한 경우이 모두 알고 있어야이 대 한 toomake를 해야 합니다. Hello 포털을 전혀 사용할 수 없다는 의미 아닙니다. 구성 변경 내용을 toothis 특정 가상 네트워크 만들기를 제외 하 고 다른 모든 항목에 사용할 수 있습니다.

## <a name="before-you-begin"></a>시작하기 전에

구성을 시작 하기 전에 hello 다음 항목이 있는지 확인 합니다.

* 각 온-프레미스 위치에서 호환되는 VPN 하드웨어. 확인 [VPN 장치에 대 한 가상 네트워크 연결을 위한](vpn-gateway-about-vpn-devices.md) toobe 호환 알려진 tooverify toouse hello 장치 됩니다.
* 각 VPN 장치에 대한 외부 연결 공용 IPv4 IP 주소. NAT 뒤 hello IP 주소를 찾을 수 없습니다. 이는 필수 요구 사항입니다.
* Tooinstall hello 최신 버전의 hello Azure PowerShell cmdlet 필요 합니다. 또한 toohello 리소스 관리자 버전에 hello 서비스 관리 (SM) 버전을 설치 해야 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.
* VPN 하드웨어 구성에 능숙한 사용자. Toohave 방법 완전히 이해 해야 tooconfigure VPN 장치 또는 아는 사람과 함께 작업 합니다.
* hello IP 주소 범위 (아직 만들지 않은 하나) 하는 경우 가상 네트워크에 대 한 toouse 되도록 합니다.
* 각 hello 로컬 네트워크 사이트에 연결 하는 hello IP 주소 범위입니다. 각 tooconnect toodo 겹치지 원하는 hello 로컬 네트워크 사이트에 hello IP 주소 범위는 있는지 toomake가 필요 합니다. 그렇지 않으면 hello 포털 또는 REST API hello hello 구성 되 고 업로드를 거부 합니다.<br>예를 들어 hello IP 주소 범위 10.2.3.0/24 모두 포함 하 고 대상 주소가 10.2.3.3 인 패키지에 있는 두 개의 로컬 네트워크 사이트가 있는 경우 Azure를 알 수 없습니다 toosend hello 패키지 toobecause hello 주소 범위는 원하는 어떤 사이트 겹칩니다. tooprevent 라우팅 문제 Azure 허용 하지 않습니다 tooupload 범위가 겹치는 구성 파일.

## <a name="1-create-a-site-to-site-vpn"></a>1. 사이트 간 VPN 만들기
동적 라우팅 게이트웨이를 사용한 사이트 간 VPN이 이미 있으면 좋습니다. 너무 진행할 수[hello 가상 네트워크 구성 설정 내보내기](#export)합니다. 그렇지 않은 경우 다음 hello지 않습니다.

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>사이트 간 가상 네트워크가 이미 있지만 정적(정책 기반) 라우팅 게이트웨이가 있는 경우:
1. 게이트웨이 유형 toodynamic 라우팅 변경 합니다. 다중 사이트 VPN에는 동적(경로 기반이라고도 함) 라우팅 게이트웨이가 필요합니다. toochange 게이트웨이 입력, 필요한 toofirst delete hello 기존 게이트웨이 만든 후 새로 만들 합니다. 자세한 내용은 [어떻게 toochange hello VPN 게이트웨이 라우팅 유형을](vpn-gateway-configure-vpn-gateway-mp.md)합니다.  
2. 새 게이트웨이를 구성하고 VPN 터널을 만듭니다. 자세한 내용은 [hello Azure 클래식 포털에서에서 VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)합니다. 먼저, 게이트웨이 유형 toodynamic 라우팅 변경 합니다.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>사이트 간 가상 네트워크 사이트가 없는 경우:
1. 이러한 지침을 사용 하 여 사이트 간 가상 네트워크를 만든: [hello Azure 클래식 포털에서에서 사이트 간 VPN 연결을 가진 가상 네트워크 만들기](vpn-gateway-site-to-site-create.md)합니다.  
2. [VPN 게이트웨이 구성](vpn-gateway-configure-vpn-gateway-mp.md)을 참조하여 동적 라우팅 게이트웨이를 구성하십시오. 수 있는지 tooselect **동적 라우팅** 게이트웨이 형식에 대 한 합니다.

## <a name="export"></a>2. 내보내기 hello 네트워크 구성 파일
Hello 다음 명령을 실행 하 여 Azure 네트워크 구성 파일을 내보냅니다. Hello 위치의 hello tooexport tooa 다른 필요한 경우 파일 위치를 변경할 수 있습니다.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. 열기 hello 네트워크 구성 파일
Hello 마지막 단계에서 다운로드 한 hello 네트워크 구성 파일을 엽니다. 원하는 xml 편집기를 사용합니다. hello 파일에는 비슷한 toohello 다음과 같아야 합니다.

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. 여러 사이트 참조 추가
구성 변경 내용을 추가 하거나 제거 하면 사이트 참조 정보를 지정 toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef 합니다. 새 로컬 사이트 참조를 추가할 새 터널을 Azure toocreate 트리거합니다. Hello 아래의 예제에서는 hello 네트워크 구성은 단일 사이트 연결입니다. 프로그램의 변경을 완료 되 면 hello 파일을 저장 합니다.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

(멀티 사이트 구성 만들기) tooadd 추가 사이트 참조를 아래 hello 예에 나와 있는 것 처럼 추가 "LocalNetworkSiteRef" 줄을 추가 합니다.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Hello 네트워크 구성 파일 가져오기
Hello 네트워크 구성 파일을 가져옵니다. Hello 변경 내용으로이 파일을 가져올 때 hello 새 터널이 추가 됩니다. hello 터널 hello 앞에서 만든 동적 게이트웨이 사용 합니다. Hello 클래식 포털 또는 PowerShell tooimport hello 파일을 사용할 수 있습니다.

## <a name="6-download-keys"></a>6. 키 다운로드
새 터널을 추가한 후 각 터널용에 대 한 hello PowerShell cmdlet ' Get AzureVNetGatewayKey' tooget hello IPsec/IKE 사전 공유 키를 사용 합니다.

예:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

원하는 경우 사용할 수도 있습니다 hello *가상 네트워크 게이트웨이 공유 키 가져오기* REST API tooget hello 사전 공유 키.

## <a name="7-verify-your-connections"></a>7. 연결 확인
Hello 다중 사이트 터널 상태를 확인 합니다. Hello 각 터널용 키를 다운로드 한 후 tooverify 연결 합니다. 아래 hello 예에 나와 있는 것 처럼 ' Get AzureVnetConnection' tooget 가상 네트워크의 목록이 터널링을 사용 합니다. VNet1에는 VNet hello hello 이름입니다.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

예제는 다음을 반환합니다.

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>다음 단계

VPN 게이트웨이에 대 한 자세한 정보는 toolearn 참조 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md)합니다.
