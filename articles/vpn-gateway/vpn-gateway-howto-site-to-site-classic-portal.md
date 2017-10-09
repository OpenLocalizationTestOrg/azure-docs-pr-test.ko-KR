---
title: "온-프레미스 네트워크 tooan Azure 가상 네트워크 연결: 사이트 간 VPN (클래식): 포털 | Microsoft Docs"
description: "온-프레미스에서 IPsec 연결을 통해 Azure 가상 네트워크 tooan 네트워크 단계 toocreate hello 공용 인터넷 합니다. 다음이 단계를 사용 하면 hello 포털을 사용 하는 크로스-프레미스 사이트 간 VPN 게이트웨이 연결을 만들 수 있습니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Hello Azure 포털 (클래식)를 사용 하 여 사이트 간 연결 만들기

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

이 문서에서는 어떻게 toouse hello Azure 포털 toocreate 온-프레미스 네트워크 toohello VNet에서에서 사이트 간 VPN 게이트웨이 연결 합니다. 이 문서의 단계 hello toohello 클래식 배포 모델을 적용합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

사이트 간 VPN 게이트웨이 연결에 사용 되는 tooconnect는 온-프레미스 IPsec/IKE (IKEv1 또는 IKEv2) VPN 터널을 통해 Azure 가상 네트워크 tooan 네트워크입니다. 이러한 종류의 연결에는 VPN 장치에 있는 온-프레미스 외부와 접한 공용 IP 주소 할당 tooit가 필요 합니다. VPN Gateway에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

![사이트 간 VPN Gateway 크로스-프레미스 연결 다이어그램](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>시작하기 전에

Hello 조건을 구성을 시작 하기 전에 다음을 충족 하는지 확인 합니다.

* Hello 클래식 배포 모델에서 toowork 것임을 확인 합니다. Hello 리소스 관리자 배포 모델에서 toowork 참조 [사이트 간 연결 (리소스 관리자)을 만들](vpn-gateway-howto-site-to-site-resource-manager-portal.md)합니다. 가능 하면 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다.
* 호환 되는 VPN 장치 및 수 tooconfigure 장애가 있는 사용자를 완료 했는지 확인 것입니다. 호환되는 VPN 장치 및 장치 구성에 대한 자세한 내용은 [VPN 장치 정보](vpn-gateway-about-vpn-devices.md)를 참조하세요.
* VPN 장치에 대한 외부 연결 공용 IPv4 주소가 있는지 확인합니다. 이 IP 주소는 NAT 뒤에 배치할 수 없습니다.
* 온-프레미스 네트워크 구성을 잘 모르는 hello IP 주소 범위에 있는 경우 해당 세부 정보를 제공할 수 있는 사용자와 toocoordinate를 해야 합니다. 이 구성을 만들 때 Azure tooyour 온-프레미스 위치를 라우팅하는 hello IP 주소 범위 접두사를 지정 해야 합니다. 온-프레미스 네트워크의 hello 서브넷 중 랩 tooconnect를 원하는 hello 가상 네트워크 서브넷을 통해 할 수 있습니다.
* 현재 PowerShell은 필요한 toospecify hello에 대 한 공유 키와 hello VPN 게이트웨이 연결을 만듭니다. Hello hello Azure 서비스 관리 (SM) PowerShell cmdlet의 최신 버전을 설치 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 이 구성에 PowerShell을 사용할 때 관리자 권한으로 실행되고 있는지 확인합니다. 

### <a name="values"></a>이 연습에 대한 샘플 구성 값

이 문서의 hello 예제는 다음 값에는 hello를 사용 합니다. 이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.

* **VNet 이름:** TestVNet1
* **주소 공간:** 
  * 10.11.0.0/16
  * 10.12.0.0/16(이 연습의 선택 사항)
* **서브넷:**
  * 프런트 엔드: 10.11.0.0/24
  * 백 엔드: 10.12.0.0/24(이 연습의 선택 사항)
* **게이트웨이 서브넷:** 10.11.255.0/27
* **리소스 그룹:** TestRG1
* **위치:** 미국 동부
* **DNS 서버:** 10.11.0.3(이 연습의 선택 사항)
* **로컬 사이트 이름:** Site2
* **클라이언트 주소 공간:** hello 온-프레미스 사이트에 있는 주소 공간입니다.

## <a name="CreatVNet"></a>1. 가상 네트워크 만들기

S2S 연결에 대 한 가상 네트워크 toouse을 만들 때 지정 하는 hello 주소 공간에 tooconnect 원하는 hello 로컬 사이트에 대 한 클라이언트 주소 공간 hello 사용 하 여 겹치지 않는 toomake를 해야 합니다. 겹치는 서브넷에 있으면 연결이 제대로 작동하지 않습니다.

* VNet 이미 있는 경우 hello 설정이 VPN 게이트웨이 설계와 호환 되는지 확인 합니다. 특히 주의 tooany 서브넷이 다른 네트워크와 겹칠 수 있습니다. 

* 가상 네트워크가 아직 없는 경우 만듭니다. 스크린샷은 예제로 제공됩니다. 자신의 있는지 tooreplace hello 값 수입니다.

### <a name="toocreate-a-virtual-network"></a>toocreate 가상 네트워크

1. 브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.
2. 페이지 맨 아래에 있는 **+**를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다. Hello에 **hello 마켓플레이스** 필드 ' 가상 네트워크 '를 입력 합니다. 찾을 **가상 네트워크** 에서 반환 하는 hello 목록 이동한 tooopen hello 클릭 **가상 네트워크** 페이지.

  ![가상 네트워크 검색 페이지](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Hello 아래 근처의 hello 가상 네트워크 페이지에서 hello **배포 모델 선택** 드롭다운 목록에서 선택 **클래식**, 클릭 하 고 **만들기**합니다.

  ![배포 모델 선택](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Hello에 **가상 network(classic) 만들** 페이지 hello VNet 설정을 구성 합니다. 이 페이지에서 첫 번째 주소 공간과 단일 서브넷 주소 범위를 추가합니다. Hello VNet 만들기를 마친 후에 다시 이동 하 고 주소 공간 및 서브넷을 더 추가할 수 있습니다.

  ![가상 네트워크 만들기 페이지](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "가상 네트워크 만들기 페이지")
5. 해당 hello 확인 **구독** 는 hello 올바르다는 것입니다. Hello 드롭 다운을 사용 하 여 구독을 변경할 수 있습니다.
6. **리소스 그룹**을 클릭하고 기존 리소스 그룹을 선택하거나 이름을 입력하여 새로 만듭니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
7. 다음으로, 선택 hello **위치** VNet에 대 한 설정입니다. hello 위치 toothis VNet을 배포 하는 hello 리소스 상주할 위치를 결정 합니다.
8. Hello 대시보드에 쉽게 VNet toobe 수 toofind 하려는 경우 선택 **Pin toodashboard**합니다. 클릭 **만들기** toocreate VNet입니다.

  ![Pin toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "Pin toodashboard")
9. '만들기'를 클릭 한 후 타일은 VNet의 hello 진행 상태를 반영 하는 hello 대시보드에 나타납니다. hello와 hello 타일 변경 사항이 VNet은 만드는 중입니다.

  ![가상 네트워크 타일 만들기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "가상 네트워크 만들기")

참조 하 여 가상 네트워크를 만든 후 **Created** 나열 **상태** hello Azure 클래식 포털의에서 네트워크 페이지 hello 합니다.

## <a name="additionaladdress"></a>2. 다른 주소 공간 추가

가상 네트워크를 만든 후에 다른 주소 공간을 추가할 수 있습니다. 다른 주소 공간 추가 S2S 구성의 필요한 부분 지 않으며 단계를 수행 하는 hello를 사용 하 여 여러 개의 주소 공간을 필요한 경우:

1. Hello 포털에서 hello 가상 네트워크를 찾습니다.
2. Hello 아래에서 가상 네트워크에 대 한 hello 페이지 **설정** 섹션에서 클릭 **주소 공간**합니다.
3. Hello 주소 공간 페이지에서 클릭 **+ 추가** 추가 주소 공간을 입력 합니다.

## <a name="dns"></a>3. DNS 서버 지정

DNS 설정이 S2S 구성의 일부가 아니지만 이름을 확인하려는 경우 DNS가 필요합니다. 값을 지정하더라도 새 DNS 서버를 만들지 않습니다. hello DNS 서버 IP 주소 지정 하는 DNS 서버가 있어야에 연결 하는 hello 리소스에 대 한 hello 이름을 확인할 수 있는 합니다. Hello 예제 설정에 대 한 개인 IP 주소를 사용 했습니다. hello IP 주소를 사용 하 여 DNS 서버의 IP 주소 hello 하지 못할 경우 있는지 toouse 고유한 값 이어야 합니다.

가상 네트워크를 만든 후에 DNS 서버 toohandle 이름 확인의 hello IP 주소를 추가할 수 있습니다. 가상 네트워크에 대 한 hello 설정을 열고 DNS 서버를 클릭 한 다음 이름 확인을 위해 toouse 되도록 hello DNS 서버의 IP 주소 hello를 추가 합니다.

1. Hello 포털에서 hello 가상 네트워크를 찾습니다.
2. Hello 아래에서 가상 네트워크에 대 한 hello 페이지 **설정** 섹션에서 클릭 **DNS 서버**합니다.
3. DNS 서버를 추가합니다.
4. toosave 설정을 클릭 **저장** hello hello 페이지 위쪽에 있습니다.

## <a name="localsite"></a>4. Hello 로컬 사이트를 구성 합니다.

일반적으로 로컬 사이트 hello tooyour 온-프레미스 위치를 나타냅니다. Hello hello VPN 게이트웨이 toohello VPN 장치를 통해 라우팅되는 hello IP 주소 범위 및는 연결을 만듭니다는 VPN 장치 toowhich의 hello IP 주소를 포함 합니다.

1. Hello 포털에서 게이트웨이 toocreate 원하는 toohello 가상 네트워크를 이동 합니다.
2. Hello에 가상 네트워크에 대 한 hello 페이지 **개요** 페이지 hello VPN 연결 섹션에서 클릭 **게이트웨이** tooopen hello **새 VPN 연결** 페이지.

  ![Tooconfigure 게이트웨이 설정을 클릭](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "tooconfigure 게이트웨이 설정을 클릭 합니다.")
3. Hello에 **새 VPN 연결** 페이지에서 **사이트 간**합니다.
4. 클릭 **로컬 사이트-필요한 설정 구성** tooopen hello **로컬 사이트** 페이지. Hello 설정을 구성 하 고 클릭 **확인** toosave hello 설정 합니다.
  - **이름:** 로컬 사이트 toomake에 대 한 이름을 만들 있습니다 tooidentify 한 것을 쉽게 합니다.
  - **VPN 게이트웨이 IP 주소:** hello 온-프레미스 네트워크에 대 한 hello VPN 장치의 공용 IP 주소입니다. hello VPN 장치는 IPv4 공용 IP 주소가 필요합니다. VPN 장치 toowhich tooconnect 원하는 hello에 대 한 유효한 공용 IP 주소를 지정 합니다. NAT 뒤에 있을 수 없습니다 하 고 Azure에서 연결할 수 toobe 했습니다. 알 수 없는 경우 hello VPN 장치 IP 주소에서는 수 항상에 자리 표시자 값 (으로 유효한 공용 IP 주소 hello 형식으로 되어) 넣은 다음 나중에 변경 합니다.
  - **클라이언트 주소 공간:** 목록 hello IP 주소 범위를이 게이트웨이 통해 로컬 온-프레미스 네트워크 toohello 라우팅됩니다. 주소 공간 범위를 여러 개 추가할 수 있습니다. 가상 네트워크가 연결 하는 다른 네트워크의 범위와 또는 자체 hello 가상 네트워크의 주소 범위 hello와 여기에서 지정한 hello 범위가 겹치지 않는 있는지 확인 합니다.

  ![로컬 사이트](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "로컬 사이트 구성")

## <a name="gatewaysubnet"></a>5. Hello 게이트웨이 서브넷을 구성 합니다.

VPN Gateway의 게이트웨이 서브넷을 만들어야 합니다. hello 게이트웨이 서브넷 hello VPN 게이트웨이 서비스를 사용 하는 hello IP 주소를 포함 합니다.

1. Hello에 **새 VPN 연결** 페이지, 확인란 선택 hello **게이트웨이 즉시 만들기**합니다. '선택적 게이트웨이 구성' hello 페이지가 나타납니다. Hello 확인란을 선택 하지 않은 경우에 hello 페이지 tooconfigure hello 게이트웨이 서브넷을 볼 수 없습니다.

  ![게이트웨이 구성 - 서브넷, 크기, 라우팅 유형](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "게이트웨이 구성 - 서브넷, 크기, 라우팅 유형")
2. tooopen hello **게이트웨이 구성** 페이지 **선택적 게이트웨이 구성-서브넷, 크기 및 라우팅 유형**합니다.
3. Hello에 **게이트웨이 구성** 페이지 **서브넷-필요한 설정 구성** tooopen hello **서브넷 추가** 페이지.

  ![게이트웨이 구성 - 게이트웨이 서브넷](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "게이트웨이 구성 - 게이트웨이 서브넷")
4. Hello에 **서브넷 추가** 페이지 hello 게이트웨이 서브넷을 추가 합니다. 지정 하는 hello 게이트웨이 서브넷의 hello 크기에 따라 달라 집니다 hello VPN 게이트웨이 구성 toocreate 되도록 합니다. 가능한 toocreate/29 수신자로 게이트웨이 서브넷 상태인 동안에 / 27 또는/28를 사용 하는 것이 좋습니다. 이렇게 하면 더 많은 주소를 포함하는 큰 서브넷이 만들어집니다. 더 큰 게이트웨이 서브넷을 사용 하 여 구성에 대 한 충분 한 IP 주소 tooaccommodate 가능한 이후 수 있습니다.

  ![게이트웨이 서브넷 추가](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "게이트웨이 서브넷 추가")

## <a name="sku"></a>6. Hello SKU 및 VPN 유형을 지정 합니다.

1. 선택 hello 게이트웨이 **크기**합니다. Hello 게이트웨이 사용 하는 toocreate 가상 네트워크 게이트웨이 SKU입니다. Hello 포털에서 ' 기본 SKU' hello = **기본**합니다. 클래식 VPN 게이트웨이 hello 이전 (레거시) 게이트웨이 Sku를 사용합니다. Hello 레거시 게이트웨이 Sku에 대 한 자세한 내용은 참조 [가상 네트워크 게이트웨이 Sku (이전 Sku) 작업](vpn-gateway-about-skus-legacy.md)합니다.

  ![SKUL 및 VPN 유형 선택](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "SKU 및 VPN 유형 선택")
2. 선택 hello **라우팅 유형** 게이트웨이에 대 한 합니다. 이 hello VPN 유형을 라고도 합니다. 한 형식 tooanother에서 hello 게이트웨이 변환할 수 없습니다 중요 tooselect hello 올바른 게이트웨이 형식입니다. VPN 장치는 선택한 hello 라우팅 유형에 호환 되어야 합니다. VPN 유형에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#vpntype)를 참조하세요. 문서 참조 too'RouteBased 표시 될 수 있습니다 ' 및 'PolicyBased' VPN 형식입니다. ' Dynamic 'too'RouteBased 해당', 'PolicyBased'에 'Static' 해당 합니다.
3. 클릭 **확인** toosave hello 설정 합니다.
4. Hello에 **새 VPN 연결** 페이지 **확인** 가상 네트워크 게이트웨이 만들기 hello 페이지 toobegin hello 맨 아래에 있습니다. 선택한 SKU hello에 따라 too45 분 toocreate까지 가상 네트워크 게이트웨이 걸릴 수 있으므로 합니다.

## <a name="vpndevice"></a>7. VPN 장치 구성

사이트 간 연결 tooan 온-프레미스 네트워크는 VPN 장치가 필요 합니다. 이 단계에서는 VPN 장치를 구성합니다. VPN 장치를 구성할 때 hello 다음이 필요 합니다.

- 공유 키 - 동일한 공유 hello은이 사이트 간 VPN 연결을 만들 때 지정한 키입니다. 이 예제에서는 기본적인 공유 키를 사용합니다. 더 복잡 한 키 toouse를 생성 하는 것이 좋습니다.
- 가상 네트워크 게이트웨이의 공용 IP 주소 번호입니다. Hello Azure 포털, PowerShell 또는 CLI를 사용 하 여 hello 공용 IP 주소를 볼 수 있습니다.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Hello 연결 만들기
이 단계에서는 hello 공유 키를 설정 하 고 hello 연결을 만듭니다. hello 설정한 hello 키가 있어야 VPN 장치 구성에 사용 된 동일한 키입니다.

> [!NOTE]
> 현재,이 단계는 hello Azure 포털에서에서 사용할 수 없습니다. Hello 서비스 관리 (SM) 버전의 hello Azure PowerShell cmdlet 사용 해야 합니다.
>

### <a name="step-1-connect-tooyour-azure-account"></a>1단계. Tooyour Azure 계정 연결

1. 관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

  ```powershell
  Add-AzureAccount
  ```
2. Hello 계정에 대 한 hello 구독을 확인 합니다.

  ```powershell
  Get-AzureSubscription
  ```
3. 둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>2단계. Hello 공유 키를 설정 하 고 hello 연결 만들기

PowerShell 및 hello 클래식 배포 모델에서 작업할 때는 때로는 hello의 이름이 hello 포털에서 리소스 되지 않습니다 hello 이름 hello Azure PowerShell을 사용 하는 경우 toosee 필요 합니다. hello 다음 단계 쉽게 hello 네트워크 구성 파일 tooobtain hello 정확한 값 hello 이름에 대 한를 내보낼 수 있습니다.

1. 컴퓨터에 디렉터리를 만들고 hello 네트워크 구성 파일 toohello 디렉터리를 내보냅니다. 이 예제에서는 hello 네트워크 구성 파일에는 내보낸된 tooC:\AzureNet은 합니다.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Xml 편집기와 hello 네트워크 구성 파일을 열고 'LocalNetworkSite name' 및 'VirtualNetworkSite 이름'에 대 한 hello 값을 확인 합니다. Hello 예제 tooreflect hello 필요한 값을 수정 합니다. 공백이 포함 된 이름을 지정할 때 hello 값에 단일 따옴표를 사용 합니다.

3. Hello 공유 키를 설정 하 고 hello 연결을 만듭니다. hello '-에서 SharedKey'를 생성 하 고 지정 하는 값입니다. 생성할 수 있습니다 하지만 hello 예에서는 'abc123' 사용 해야 할 더 복잡 한 항목을 사용 합니다. 중요 한 점은 여기에서 지정한 hello 값 hello hello VPN 장치를 구성할 때 지정한 같은 값 이어야 합니다.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Hello 결과 hello 연결을 만들면: **상태: 성공**합니다.

## <a name="verify"></a>9. 연결 확인

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

연결 하는 문제를 발생 하는 경우 참조 hello **문제 해결** hello 목차 hello 왼쪽된 창에서 항목의 섹션입니다.

## <a name="reset"></a>어떻게 tooreset VPN 게이트웨이

Azure VPN Gateway 재설정은 하나 이상의 사이트 간 VPN 터널에서 크로스-프레미스 VPN 연결이 손실되는 경우에 유용합니다. 이 경우 온-프레미스 VPN 장치는 모든 정상적으로 작동 하지만 수 없습니다. tooestablish IPsec 터널 hello Azure VPN 게이트웨이 사용 합니다. 자세한 단계는 [VPN 게이트웨이 다시 설정](vpn-gateway-resetgw-classic.md)을 참조하세요.

## <a name="changesku"></a>어떻게 toochange 게이트웨이 SKU

Hello 게이트웨이 SKU toochange를 단계에 대 한 참조 [게이트웨이 SKU 크기를 조정](vpn-gateway-about-SKUS-legacy.md)합니다.

## <a name="next-steps"></a>다음 단계

* 연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.
* 강제 터널링에 대한 내용은 [강제 터널링 정보](vpn-gateway-about-forced-tunneling.md)를 참조하세요.