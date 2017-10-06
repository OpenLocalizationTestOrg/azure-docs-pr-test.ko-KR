---
title: "클래식 가상 네트워크 tooAzure 리소스 관리자 Vnet 연결: 포털 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 클래식 Vnet 및 VPN 게이트웨이와 hello 포털을 사용 하 여 리소스 관리자 Vnet 간의 VPN 연결"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Hello 포털을 사용 하 여 다양 한 배포 모델에 있는 가상 네트워크에 연결

이 문서 tooconnect 클래식 Vnet tooResource 관리자 Vnet tooallow 서로 hello 별도 배포 모델 toocommunicate에 배치 된 리소스를 hello 하는 방법을 보여 줍니다. 이 문서의 단계 hello 주로 hello Azure 포털을 사용 하지만 PowerShell hello를 사용 하 여 hello 문서가이 목록에서 선택 하 여이 구성을 만들 수도 있습니다.

> [!div class="op_single_selector"]
> * [포털](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

비슷한 tooconnecting VNet tooan 온-프레미스 사이트 위치는 클래식 VNet tooa 리소스 관리자 VNet를 연결 합니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다. 다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다. 으로 구성 된 hello 게이트웨이 동적 또는 경로 기반으로 연결 tooon 온-프레미스 네트워크에 이미 있는 Vnet을 연결할 수도 있습니다. VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다. 

Vnet hello에 있는 경우 동일한 지역 경우가 있습니다 tooinstead VNet 피어 링을 사용 하 여 연결을 것입니다. VNet 피어링은 VPN Gateway를 사용하지 않습니다. 자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요. 

### <a name="prerequisites"></a>필수 조건

* 이 단계에서는 두 VNet이 이미 만들어졌다고 가정합니다. 이 문서를 사용 하는 연습으로 Vnet이 없는 경우 링크 가지 hello 단계 toohelp에서 만드는지에 합니다.
* Vnet이 서로 겹치지 않을 hello에 대 한 hello 주소 범위 또는 해당 hello 게이트웨이에 연결할 수 있습니다 다른 연결에 대 한 hello를 사용 하 여 겹치는 범위를 확인 합니다.
* 리소스 관리자와 서비스 관리 (클래식)에 대 한 hello 최신 PowerShell cmdlet을 설치 합니다. 이 문서에서는 Azure 포털 hello 및 PowerShell을 모두 사용합니다. PowerShell은 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 필요한 toocreate hello 연결입니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 

### <a name="values"></a>예제 설정

이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.

**클래식 VNet**

VNet 이름 = ClassicVNet <br>
Address space = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
Resource Group = ClassicRG <br>
Location = West US <br>
GatewaySubnet = 10.0.0.32/28 <br>
Local site = RMVNetLocal <br>

**Resource Manager VNet**

VNet 이름 = RMVNet <br>
Address space = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Resource Group = RG1 <br>
Location = East US <br>
Virtual network gateway name = RMGateway <br>
Gateway type = VPN <br>
VPN type = Route-based <br>
게이트웨이 공용 IP 주소 이름 = rmgwpip <br>
Local network gateway = ClassicVNetLocal <br>
연결 이름 = RMtoClassic

### <a name="connection-overview"></a>연결 개요

이 구성에 대 한 hello 가상 네트워크 간에 IPsec/IKE VPN 터널을 통해 VPN 게이트웨이 연결을 만듭니다. 또는 로컬 네트워크에 연결 하는 hello 사용 하 여 겹치는 VNet 범위 중 있는지 확인 합니다.

hello 다음 표에서 hello 예제 Vnet 및 로컬 사이트 정의 하는 방법의 예:

| 가상 네트워크 | 주소 공간 | 지역 | Toolocal 네트워크 사이트에 연결 |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |미국 서부 | RMVNetLocal(192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |미국 동부 |ClassicVNetLocal(10.0.0.0/24) |

## <a name="classicvnet"></a>1. Hello 클래식 VNet 설정 구성

이 섹션에서는 만들 hello 로컬 네트워크 (사이트 로컬 사이트) 및 클래식 VNet에 대 한 가상 네트워크 게이트웨이 hello 합니다. 클래식 VNet이 없는 연습으로 다음이 단계를 실행 하는 경우 사용 하 여 VNet을 만들 수 있습니다 [이 여기서](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) 및 hello [예제](#values) 위에서 설정 값입니다.

Hello 포털 toocreate 클래식 가상 네트워크를 사용할 때는 hello hello 옵션 toocreate 클래식 가상 네트워크 나타나지 않으면 그렇지 않으면 다음 단계를 사용 하 여 toohello 가상 네트워크 블레이드를 이동 해야 합니다.

1. Hello 클릭 tooopen hello 'New' 블레이드 '+'.
2. ' 가상 네트워크 ' hello 'hello 마켓플레이스' 필드에 입력 합니다. 네트워킹을 대신 선택-> 가상 네트워크를 가져올 수 없습니다 hello 옵션 toocreate 클래식 VNet 합니다.
3. ' 가상 네트워크 ' hello 반환 된 목록에서에서 찾은 tooopen hello 가상 네트워크 블레이드를 클릭 합니다. 
4. 가상 네트워크 블레이드에서 hello '클래식' toocreate 클래식 VNet을 선택 합니다. 

VNet VPN 게이트웨이 통해 이미 있는 경우 해당 hello 게이트웨이 동적 확인 합니다. 정적 이면 먼저 hello VPN 게이트웨이 삭제 하십시오 계속 진행 합니다.

스크린샷은 예제로 제공됩니다. 있는지 tooreplace hello 사용 하 여 값을 직접 수행 하거나 사용할 hello [예제](#values) 값입니다.

### <a name="part-1---configure-hello-local-site"></a>1 부-hello 로컬 사이트를 구성 합니다.

열기 hello [Azure 포털](https://ms.portal.azure.com) Azure 계정으로 로그인 합니다.

1. 너무 이동**모든 리소스** hello 찾습니다 **ClassicVNet** hello 목록에 있습니다.
2. Hello에 **개요** 블레이드 hello **VPN 연결** 섹션에서 hello **게이트웨이** 그래픽 toocreate 게이트웨이 합니다.

    ![VPN 게이트웨이 구성](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "VPN 게이트웨이 구성")
3. Hello에 **새 VPN 연결** 블레이드에서 대 한 **연결 유형**선택, **사이트 간**합니다.
4. **로컬 사이트**로 **필요한 설정 구성**을 클릭합니다. Hello 열립니다 **로컬 사이트** 블레이드입니다.
5. Hello에 **로컬 사이트** 블레이드에서 이름 toorefer toohello 리소스 관리자 VNet을 만듭니다. 예: 'RMVNetLocal'.
6. 리소스 관리자 VNet hello에 대 한 hello VPN 게이트웨이 공용 IP 주소를 이미 있으면 hello 값을 사용 하 여 hello에 대 한 **VPN 게이트웨이 IP 주소** 필드입니다. 이 단계를 연습으로 수행하는 경우 또는 아직 Resource Manager VNet에 대한 가상 네트워크 게이트웨이가 없는 경우 자리 표시자 IP 주소를 만들 수 있습니다. Hello 자리 표시자 IP 주소는 유효한 형식의 사용 하는지 확인 합니다. 이상에서는 hello hello 리소스 관리자 가상 네트워크 게이트웨이의 공용 IP 주소와 hello 자리 표시자 IP 주소를 대체합니다.
7. 에 대 한 **클라이언트 주소 공간**, 리소스 관리자 VNet hello에 대 한 hello 가상 네트워크 IP 주소 공간에 대 한 hello 값을 사용 합니다. 이 설정은 사용 되는 toospecify hello 주소 공간 tooroute toohello 리소스 관리자 가상 네트워크입니다.
8. 클릭 **확인** toosave 값 hello 돌아와 toohello **새 VPN 연결** 블레이드입니다.

### <a name="part-2---create-hello-virtual-network-gateway"></a>2 부-hello 가상 네트워크 게이트웨이 만들기

1. Hello에 **새 VPN 연결** 블레이드, 선택 hello **게이트웨이 즉시 만들기** 확인란을 클릭 하 고 **선택적 게이트웨이 구성** tooopen hello  **게이트웨이 구성** 블레이드입니다. 

    ![게이트웨이 구성 블레이드 열기](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "게이트웨이 구성 블레이드 열기")
2. 클릭 **서브넷-필요한 설정 구성** tooopen hello **서브넷 추가** 블레이드입니다. hello **이름** hello 필요한 값으로 이미 구성 되어 **GatewaySubnet**합니다.
3. hello **주소 범위** toohello 범위 hello 게이트웨이 서브넷에 대 한 참조입니다. 게이트웨이 서브넷을 /29 주소 범위(주소 3개)로 만들 수 있지만 더 많은 IP 주소를 포함하는 게이트웨이 서브넷을 만드는 것이 좋습니다. 그러면 사용 가능한 IP 주소가 필요할 수 있는 향후 구성을 수용하게 됩니다. 가능하면 /27 또는 /28을 사용합니다. 다음이 단계를 연습으로 사용 하는 경우에 toohello을 참조할 수 있습니다 [예제](#values) 값입니다. 클릭 **확인** toocreate hello 게이트웨이 서브넷입니다.
4. Hello에 **게이트웨이 구성** 블레이드에서 **크기** toohello 게이트웨이 SKU를 참조 합니다. VPN 게이트웨이에 대 한 hello 게이트웨이 SKU를 선택 합니다.
5. Hello 확인 **라우팅 유형** 은 **동적**, 클릭 **확인** tooreturn toohello **새 VPN 연결** 블레이드입니다.
6. Hello에 **새 VPN 연결** 블레이드에서 클릭 **확인** toobegin VPN 게이트웨이 만들기. VPN 게이트웨이 만들기 too45 분 toocomplete 차지할 수 있습니다.

### <a name="ip"></a>-3 부 복사 hello 가상 네트워크 게이트웨이 공용 IP 주소

Hello 가상 네트워크 게이트웨이 만든 후에 hello 게이트웨이 IP 주소를 볼 수 있습니다. 

1. Tooyour 이동 클래식 VNet 및 클릭 **개요**합니다.
2. 클릭 **VPN 연결** tooopen hello VPN 연결 블레이드입니다. Hello VPN 연결 블레이드에서 hello 공용 IP 주소를 볼 수 있습니다. Tooyour 가상 네트워크 게이트웨이 할당 하는 hello 공용 IP 주소입니다. 
3. 적어 두거나 hello IP 주소를 복사 합니다. 나중 단계에서 Resource Manager 로컬 네트워크 게이트웨이 구성 설정 관련 작업을 수행할 때 사용합니다. 게이트웨이 연결의 hello 상태를 볼 수 있습니다. 사용자가 만든 공지 hello 로컬 네트워크 사이트 '연결'로 표시 됩니다. 연결을 만든 후 hello 상태가 변경 됩니다.
4. Hello 게이트웨이 IP 주소를 복사한 후 hello 블레이드를 닫습니다.

## <a name="rmvnet"></a>2. Hello 리소스 관리자 VNet 설정 구성

이 섹션에서는 가상 네트워크 게이트웨이 hello와 만들어야 hello 로컬 네트워크 게이트웨이 리소스 관리자 VNet에 대 한 합니다. 리소스 관리자 VNet이 없는 연습으로 다음이 단계를 실행 하는 경우 사용 하 여 VNet을 만들 수 있습니다 [이 여기서](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 및 hello [예제](#values) 위에서 설정 값입니다.

스크린샷은 예제로 제공됩니다. 있는지 tooreplace hello 사용 하 여 값을 직접 수행 하거나 사용할 hello [예제](#values) 값입니다.

### <a name="part-1---create-a-gateway-subnet"></a>1부 - 게이트웨이 서브넷 만들기

가상 네트워크 게이트웨이 만들기 전에 먼저 toocreate hello 게이트웨이 서브넷을 해야 합니다. CIDR 개수가 /28 이상인 게이트웨이 서브넷을 만듭니다. (/27, /26 등)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>2부 - 가상 네트워크 게이트웨이 만들기

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>3부 - 로컬 네트워크 게이트웨이 만들기

로컬 네트워크 게이트웨이 hello hello 주소 범위 및 클래식 VNet 및 해당 가상 네트워크 게이트웨이에 연결 된 hello 공용 IP 주소를 지정 합니다.

다음이 단계를 연습으로 수행 하는 경우에 toothese 설정을 참조 합니다.

| 가상 네트워크 | 주소 공간 | 지역 | Toolocal 네트워크 사이트에 연결 |게이트웨이 공용 IP 주소|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |미국 서부 | RMVNetLocal(192.168.0.0/16) |hello toohello ClassicVNet 게이트웨이에 할당 된 공용 IP 주소|
| RMVNet | (192.168.0.0/16) |미국 동부 |ClassicVNetLocal(10.0.0.0/24) |hello toohello RMVNet 게이트웨이에 할당 된 공용 IP 주소입니다.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Hello 클래식 VNet 로컬 사이트 설정 수정

이 섹션에서는 hello 리소스 관리자 VPN 게이트웨이 IP 주소를 사용 하 여 hello 로컬 사이트 설정을 지정 하는 때 사용한 hello 자리 표시자 IP 주소를 대체 합니다. 이 섹션에서는 hello 클래식 (SM) PowerShell cmdlet을 사용 합니다.

1. Azure 포털 hello toohello 클래식 가상 네트워크를 이동 합니다.
2. 가상 네트워크에 대 한 hello 블레이드에서 클릭 **개요**합니다.
3. Hello에 **VPN 연결** 섹션에서 hello 그래픽에 로컬 사이트의 hello 이름을 클릭 합니다.

    ![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN 연결")
4. Hello에 **사이트 간 VPN 연결** 블레이드에서 hello hello 사이트 이름을 클릭 합니다.

    ![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "로컬 사이트 이름")
5. 로컬 사이트에 대 한 연결 블레이드에서 hello hello 로컬 사이트 tooopen hello의 hello 이름을 클릭 **로컬 사이트** 블레이드입니다.

    ![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "로컬 사이트 열기")
6. Hello에 **로컬 사이트** 블레이드, replace hello **VPN 게이트웨이 IP 주소** hello 리소스 관리자 게이트웨이의 hello IP 주소를 사용 합니다.

    ![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "게이트웨이 IP 주소")
7. 클릭 **확인** tooupdate hello IP 주소입니다.

## <a name="RMtoclassic"></a>4. 리소스 관리자 tooclassic 연결 만들기

리소스 관리자 VNet hello에서 hello 연결을 구성 하면이 단계에서는 Azure 포털 hello toohello 클래식 VNet 사용 합니다.

1. **모든 리소스**, hello 로컬 네트워크 게이트웨이 찾습니다. 이 예에서 hello 로컬 네트워크 게이트웨이 **ClassicVNetLocal**합니다.
2. 클릭 **구성** hello에 대 한 hello VPN 게이트웨이 IP 주소 값을 hello 인지 확인 클래식 VNet입니다. 필요한 경우 업데이트하고 **저장**을 클릭합니다. 닫기 hello 블레이드입니다.
3. **모든 리소스**, hello 로컬 네트워크 게이트웨이 클릭 합니다.
4. 클릭 **연결** tooopen hello 연결 블레이드입니다.
5. Hello에 **연결** 블레이드에서 클릭  **+**  tooadd 연결 합니다.
6. Hello에 **연결 추가** 블레이드, 이름 hello 연결 합니다. 예: 'RMtoClassic'.
7. **사이트 간**이 블레이드에 이미 선택되어 있습니다.
8. 이 사이트와 tooassociate 원하는 hello 가상 네트워크 게이트웨이 선택 합니다.
9. **공유 키**를 만듭니다. 이 키는 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 만든 hello 연결에도 사용 됩니다. Hello 키를 생성 하거나 하나 만들 수 있습니다. 이 예제에서는 'abc123'을 사용했지만 좀 더 복잡한 항목을 사용할 수 있고 사용해야 합니다.
10. 클릭 **확인** toocreate hello 연결 합니다.

##<a name="classictoRM"></a>5. 클래식 tooResource에 대 한 연결 관리자 만들기

이 단계에서는 hello 연결 hello 클래식 VNet toohello 리소스 관리자 VNet을에서 구성합니다. 이러한 단계에는 PowerShell이 필요합니다. Hello 포털에서이 연결을 만들 수 없습니다. 다운로드 하 고 hello 클래식 (SM)와 관리자 RM (리소스) PowerShell cmdlet은 모두 설치 되어 있는지 확인 합니다.

### <a name="1-connect-tooyour-azure-account"></a>1. Tooyour Azure 계정 연결

관리자 권한을 가진 hello PowerShell 콘솔을 열고 tooyour Azure 계정에에서 로그인 합니다. hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다. 로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정은 다운로드 됩니다.

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

프로그램 Azure 계정 toouse hello 클래식 PowerShell cmdlet (SM)를 추가 합니다. toodo 따라서 hello 다음 명령을 사용할 수 있습니다.

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. 보기 hello 네트워크 구성 파일 값

Hello Azure 포털에서에서 VNet을 만들 때 Azure를 사용 하는 hello 전체 이름을 hello Azure 포털에에서 표시 되지 않습니다. 예를 들어 hello Azure 포털에에서 'ClassicVNet' 라는 toobe 나타나는 VNet 있을 수는 훨씬 더 긴 이름을 hello 네트워크 구성 파일에서. hello 이름이 같을 수 있습니다: ' 그룹 ClassicRG ClassicVNet'. 이 단계에서는 hello 네트워크 구성 파일, 보기 hello 값 다운로드합니다.

컴퓨터에 디렉터리를 만들고 hello 네트워크 구성 파일 toohello 디렉터리를 내보냅니다. 이 예제에서는 hello 네트워크 구성 파일에는 내보낸된 tooC:\AzureNet은 합니다.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

클래식 VNet에 대 한 텍스트 편집기 및 보기 hello 이름으로 hello 파일을 엽니다. PowerShell cmdlet을 실행 하는 경우 hello 이름을 hello 네트워크 구성 파일에서 사용 합니다.

- VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.
- 사이트 이름은 **LocalNetworkSite name =**으로 나열됩니다.

### <a name="3-create-hello-connection"></a>3. Hello 연결 만들기

Hello 공유 키를 설정 하 고 hello 클래식 VNet toohello 리소스 관리자 VNet에서에서 hello 연결을 만듭니다. Hello 포털을 사용 하 여 hello 공유 키를 설정할 수 없습니다. Hello 클래식 버전의 hello PowerShell cmdlet 사용 하 여 로그인 하는 동안 다음이 단계를 실행 해야 합니다. toodo를 사용 하 여 **Add-azureaccount**합니다. 이렇게 하지 않으면 됩니다 수 tooset hello '-AzureVNetGatewayKey'.

- 이 예제에서는 **-VNetName** hello 이름인 hello의 클래식 VNet으로 네트워크 구성 파일에서 발견 합니다. 
- hello **-LocalNetworkSiteName** 네트워크 구성 파일에서 발견 하 hello 이름으로 hello 로컬 사이트에 대 한 지정 합니다.
- hello **-에서 SharedKey** 생성 하 고 지정 하는 값입니다. 이 예제에서는 *abc123*을 사용했으나 좀 더 복잡한 항목을 생성할 수 있습니다. 중요 한 점은 여기에서 지정한 hello 값 hello hello 같은 리소스 관리자 tooclassic 연결을 만들 때 지정한 값 이어야 합니다.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. 연결 확인

사용 하 여 연결 hello Azure 포털 또는 PowerShell을 확인할 수 있습니다. 을 확인할 때 할 수 있습니다 toowait 2 분 정도로 hello 연결을 만들 때. 연결이 성공적 '연결' too'Connected에서 hello 연결 상태가 변경 '.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>프로그램 클래식 VNet tooyour 리소스 관리자 VNet에서에서 tooverify hello 연결

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>리소스 관리자 VNet tooyour에서 tooverify hello 연결 클래식 VNet

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>VNet 간 FAQ

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
