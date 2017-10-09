---
title: "VNet: 클래식: Azure Portal 사이의 연결 만들기 | Microsoft Docs"
description: "어떻게 함께 tooconnect Azure 가상 네트워크 및 PowerShell을 사용 하 여 hello Azure 클래식 포털입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>VNet-VNet 연결(클래식) 구성

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

이 문서에서는 어떻게 toocreate 가상 네트워크 간의 VPN 게이트웨이 연결 합니다. hello 가상 네트워크 수 같거나 다른 지역 hello와에서 동일 hello 또는 서로 다른 구독 합니다. 이 문서의 단계 hello toohello 클래식 배포 모델 및 hello Azure 포털에 적용 됩니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [다양한 배포 모델 간 연결 - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [다양한 배포 모델 간 연결 - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![TooVNet VNet 연결 다이어그램](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>VNet 간 연결 정보

가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) VPN 게이트웨이 사용 하 여 hello 클래식 배포 모델에 연결 하는 유사한 tooconnecting 가상 네트워크 tooan 온-프레미스 사이트 위치입니다. 두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.

다른 구독 및 지역 hello Vnet에 연결할 수 있습니다. 다중 사이트 구성과 VNet tooVNet 통신을 결합할 수 있습니다. 이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.

![VNet tooVNet 연결](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>가상 네트워크에 연결하는 이유

다음 이유로 hello에 대 한 tooconnect 가상 네트워크를 사용할 수 있습니다.

* **지역 간 지리적 중복 및 지리적 상태**

  * 인터넷 연결 끝점으로 이동하지 않고도 보안 연결을 통해 지역에서 복제 또는 동기화를 직접 설정할 수 있습니다.
  * Azure 부하 분산 장치 및 Microsoft 또는 타사 클러스터링 기술을 사용하여 여러 Azure 지역 간의 지리적 중복을 통해 워크로드의 가용성을 높게 설정할 수 있습니다. 한 가지 중요 한 예는 SQL Always On 가용성 그룹이 여러 Azure 지역에 분산을 tooset 합니다.
* **분리 경계가 뚜렷한 지역별 다중 계층 응용 프로그램**

  * 내 동일한 hello 영역 강력한 격리 및 보안 계층 간 통신을 함께 연결 된 여러 Vnet으로 다중 계층 응용 프로그램을 설치할 수 없다.
* **Azure의 구독 간/조직 간 통신**

  * Azure 구독이 여러 개인 경우 이제 가상 네트워크 간에 여러 구독의 작업을 안전하게 연결할 수 있습니다.
  * 엔터프라이즈 또는 서비스 공급자의 경우 이제 Azure 내의 보안 VPN 기술을 사용하여 조직 간 통신을 사용하도록 설정할 수 있습니다.

VNet 대 VNet 연결에 대 한 자세한 내용은 참조 [VNet 대 VNet 고려 사항](#faq) hello이이 문서의 뒷부분에 있습니다.

### <a name="before-you-begin"></a>시작하기 전에

이 연습을 시작 하기 전에 다운로드 하 여 hello hello Azure 서비스 관리 (SM) PowerShell cmdlet의 최신 버전을 설치 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. 대부분의 hello 단계를 위해 hello 포털을 사용 하지만 hello Vnet 간의 PowerShell toocreate hello 연결을 사용 해야 합니다. Azure 포털 hello를 사용 하 여 hello 연결을 만들 수 없습니다.

## <a name="plan"></a>1단계 - IP 주소 범위 계획

것은 중요 한 toodecide hello 범위 수를 사용 하는 tooconfigure 가상 네트워크입니다. 이 구성에 대 한 서로 또는 로컬 네트워크에 연결 하는 hello 사용 하 여 겹치는 VNet 범위 중 선택 되어 있는지 확인 해야 합니다.

hello 다음 표에서 방법의 예 toodefine Vnet입니다. 지침 으로만 참고 hello 범위를 사용 합니다. 가상 네트워크에 대 한 hello 범위를 적어 둡니다. 이 정보는 이후 단계에서 필요합니다.

**예제**

| Virtual Network | 주소 공간 | 지역 | Toolocal 네트워크 사이트에 연결 |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |미국 동부 |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |미국 서부 |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>2 단계-hello 가상 네트워크 만들기

두 개의 가상 네트워크를에서 만들고 hello [Azure 포털](https://portal.azure.com)합니다. Hello 단계 toocreate 클래식 가상 네트워크에 대 한 참조 [클래식 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다. 

Hello 포털 toocreate 클래식 가상 네트워크를 사용할 때는 hello hello 옵션 toocreate 클래식 가상 네트워크 나타나지 않으면 그렇지 않으면 다음 단계를 사용 하 여 toohello 가상 네트워크 블레이드를 이동 해야 합니다.

1. Hello 클릭 tooopen hello 'New' 블레이드 '+'.
2. ' 가상 네트워크 ' hello 'hello 마켓플레이스' 필드에 입력 합니다. 네트워킹을 대신 선택-> 가상 네트워크를 가져올 수 없습니다 hello 옵션 toocreate 클래식 VNet 합니다.
3. ' 가상 네트워크 ' hello 반환 된 목록에서에서 찾은 tooopen hello 가상 네트워크 블레이드를 클릭 합니다. 
4. 가상 네트워크 블레이드에서 hello '클래식' toocreate 클래식 VNet을 선택 합니다. 

이 문서의 연습으로을 사용 하는 경우 다음 예제에서는 값에는 hello를 사용할 수 있습니다.

**TestVNet1에 대한 값**

이름: TestVNet1<br>
주소 공간: 10.11.0.0/16, 10.12.0.0/16(선택 사항)<br>
서브넷 이름: 기본값<br>
서브넷 주소 범위: 10.11.0.1/24<br>
리소스 그룹: ClassicRG<br>
위치: 미국 동부<br>
게이트웨이 서브넷: 10.11.1.0/27

**TestVNet4에 대한 값**

이름: TestVNet4<br>
주소 공간: 10.41.0.0/16, 10.42.0.0/16(선택 사항)<br>
서브넷 이름: 기본값<br>
서브넷 주소 범위: 10.41.0.1/24<br>
리소스 그룹: ClassicRG<br>
위치: 미국 서부<br>
게이트웨이 서브넷: 10.41.1.0/27

**Vnet을 만들 때 주의 hello 설정을 다음에 유의 하십시오.**

* **가상 네트워크 주소 공간** – hello 가상 네트워크 주소 공간 페이지에서 가상 네트워크에 대 한 toouse 되도록 hello 주소 범위를 지정 합니다. 이들은 toohello Vm 및 toothis 가상 네트워크를 배포 하는 다른 역할 인스턴스에 할당할 수 있는 hello 동적 IP 주소입니다.<br>이 VNet에 연결 하는 다른 Vnet 또는 온-프레미스 위치 hello 하는 hello 주소 공간 선택에 대 한 hello 주소 공간과 겹칠 수 없습니다.

* **위치** – 가상 네트워크를 만들 때 Azure 위치(지역)와 연결합니다. 예를 들어 있는 Vm에 배포 tooyour 가상 네트워크 toobe West US에 물리적으로 배치 하려면 해당 위치를 선택 합니다. 만든 후 가상 네트워크와 연결 된 hello 위치를 변경할 수 없습니다.

**Vnet을 만든 후에 다음 설정을 hello를 추가할 수 있습니다.**

* **주소 공간** – 추가 주소 공간이이 구성에 필요 하지 않습니다. 하지만 hello VNet을 만든 후 다른 주소 공간을 추가할 수 있습니다.

* **서브넷** – 추가 서브넷이이 구성에 필요 하지 않습니다. 하지만 다른 역할 인스턴스와 별도의 서브넷에 Vm toohave를 할 수 있습니다.

* **DNS 서버** – hello DNS 서버 이름 및 IP 주소를 입력 합니다. 이 설정은 DNS 서버를 만들지 않습니다. 이 가상 네트워크에 대 한 이름 확인을 위해 toouse 되도록 toospecify hello DNS 서버가 있습니다.

이 섹션에서는 hello 연결 유형, hello 로컬 사이트를 구성 하 고 hello 게이트웨이 만듭니다.

## <a name="localsite"></a>3 단계-hello 로컬 사이트를 구성 합니다.

Hello Vnet 간의 tooroute 트래픽이 하는 방법을 각 로컬 네트워크 사이트 toodetermine에 지정 된 hello 설정을 azure 사용 합니다. 각 VNet toohello 각 로컬 네트워크에 대 한 트래픽을 tooroute 원하는 가리켜야 합니다. Toouse toorefer tooeach 로컬 네트워크 사이트를 원하는 hello 이름을 확인할 수 있습니다. 것이 가장 좋은 toouse 다른 설명적인 이름입니다.

예를 들어 TestVNet1 tooa 로컬 네트워크 사이트를 만들면 'VNet4Local' 라는 연결 합니다. VNet4Local에 대 한 hello 설정을 TestVNet4에 대 한 hello 주소 접두사를 포함 합니다.

hello 로컬 각 VNet은 다른 VNet을 hello에 대 한 사이트입니다. 다음 예에서는 값에는 hello에서는 구성에 사용 됩니다.

| 가상 네트워크 | 주소 공간 | 지역 | Toolocal 네트워크 사이트에 연결 |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |미국 동부 |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |미국 서부 |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Hello Azure 포털에서에서 TestVNet1를 찾습니다. Hello에 **VPN 연결** 섹션 hello 블레이드의 클릭 **게이트웨이**합니다.

    ![게이트웨이 없음](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Hello에 **새 VPN 연결** 페이지에서 **사이트 간**합니다.
3. 클릭 **로컬 사이트** tooopen 로컬 사이트 페이지 hello 및 hello 설정을 구성 합니다.
4. Hello에 **로컬 사이트** 페이지에서 로컬 사이트 이름을 지정 합니다. 예제에서는 이름을 hello 로컬 사이트 'VNet4Local' 합니다.
5. **VPN 게이트웨이 IP 주소**의 경우 IP 주소가 올바른 형식이기만 하면 무엇이든 사용할 수 있습니다. 일반적으로 VPN 장치에 대 한 hello 실제 외부 IP 주소를 사용 합니다. 하지만 클래식 VNet 대 VNet 구성의 경우 toohello 게이트웨이 VNet에 대 한 할당 된 hello 공용 IP 주소를 사용 합니다. 아직 hello 가상 네트워크 게이트웨이 만든 있다고 가정 자리 표시자로 모든 유효한 공용 IP 주소를 지정 합니다.<br>이 구성에서는 선택 사항이 아니므로 이 항목은 비워두면 안 됩니다. 이후 단계에서이 설정으로 다시 이동 하 고 Azure에서 생성 되 면 hello 해당 가상 네트워크 게이트웨이 IP 주소와 구성 합니다.
6. 에 대 한 **클라이언트 주소 공간**, 다른 VNet의 hello hello 주소 공간을 사용 합니다. Tooyour 계획 예를 참조 하십시오. 클릭 **확인** toosave 설정 및 반환 백 toohello **새 VPN 연결** 블레이드입니다.

    ![로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>4 단계-hello 가상 네트워크 게이트웨이 만들기

각 가상 네트워크에는 가상 네트워크 게이트웨이가 있어야 합니다. hello 가상 네트워크 게이트웨이 라우팅하고 트래픽을 암호화 합니다.

1. Hello에 **새 VPN 연결** 블레이드, 확인란 선택 hello **게이트웨이 즉시 만들기**합니다.
2. **서브넷, 크기 및 라우팅 유형**을 클릭합니다. Hello에 **게이트웨이 구성** 블레이드에서 클릭 **서브넷**합니다.
3. hello 게이트웨이 서브넷 이름이 자동으로 채워집니다 'GatewaySubnet' hello 필요한 이름을 가진 합니다. hello **주소 범위** toohello VPN 게이트웨이 서비스에 할당 되는 hello IP 주소가 포함 되어 있습니다. 일부 구성은/27 또는 / 28/29, 하지만 최상의 toouse의 게이트웨이 서브넷을 허용 tooaccommodate 이후 구성을 hello 게이트웨이 서비스에 대 한 더 많은 IP 주소를 할 수도 있습니다. 여기의 예제에서는 10.11.1.0/27을 사용합니다. Hello 주소 공간을 조정 하 고 클릭 **확인**합니다.
4. Hello 구성 **게이트웨이 크기**합니다. 이 설정은 참조 toohello [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다.
5. Hello 구성 **라우팅 유형**합니다. 이 구성에 대해 라우팅 유형을 hello **동적**합니다. Hello 게이트웨이 종료 하 고 새로 만들 하지 않으면 hello 라우팅 유형을 나중에 변경할 수 없습니다.
6. **확인**을 클릭합니다.
7. Hello에 **새 VPN 연결** 블레이드에서 클릭 **확인** toobegin hello 가상 네트워크 게이트웨이 만들기. 게이트웨이 만들기 45 분에 따라 이상 hello 선택한 게이트웨이 SKU 종종 걸릴 수 있습니다.

## <a name="vnet4settings"></a>5단계 - TestVNet4 설정 구성

 ° ט hello 너무[로컬 사이트를 만들](#localsite) 및 [hello 가상 네트워크 게이트웨이 만들기](#gw) tooconfigure TestVNet4, 필요한 경우 hello 값으로 대체 합니다. 이렇게 하는 연습으로, 하는 경우 사용 하 여 hello [예제 값](#vnetvalues)합니다.

## <a name="updatelocal"></a>6 단계-hello 로컬 사이트 업데이트

Hello 로컬 사이트를 조정 해야 두 Vnet에 대 한 가상 네트워크 게이트웨이 만든 후 **VPN 게이트웨이 IP 주소** 값입니다.

|VNet 이름|연결된 사이트|게이트웨이 IP 주소|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|TestVNet4의 VPN 게이트웨이 IP 주소|
|TestVNet4|VNet1Local|TestVNet1의 VPN 게이트웨이 IP 주소|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>-1 부 Get hello 가상 네트워크 게이트웨이 공용 IP 주소

1. Hello Azure 포털에서에서 가상 네트워크를 찾습니다.
2. Tooopen hello VNet 클릭 **개요** 블레이드입니다. Hello 블레이드에서 **VPN 연결**, 가상 네트워크 게이트웨이에 대 한 hello IP 주소를 볼 수 있습니다.

  ![공용 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Hello IP 주소를 복사 합니다. Hello 다음 섹션에 사용 합니다.
4. TestVNet4에 대해 이들 단계를 반복합니다.

### <a name="part-2---modify-hello-local-sites"></a>2 부-hello 로컬 사이트 수정

1. Hello Azure 포털에서에서 가상 네트워크를 찾습니다.
2. Hello VNet에 **개요** 블레이드에서 hello 로컬 사이트를 클릭 합니다.

  ![생성된 로컬 사이트](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Hello에 **사이트 간 VPN 연결** 블레이드에서 원하는 toomodify hello 로컬 사이트의 hello 이름을 클릭 합니다.

  ![로컬 사이트 열기](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Hello 클릭 **로컬 사이트** toomodify 되도록 합니다.

  ![사이트 수정](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. 업데이트 hello **VPN 게이트웨이 IP 주소** 클릭 **확인** toosave hello 설정 합니다.

  ![게이트웨이 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. 다른 블레이드를 닫고 hello 합니다.
7. TestVNet4에 대해 이들 단계를 반복합니다.

## <a name="getvalues"></a>단계 7-hello 네트워크 구성 파일에서 값 검색

Hello Azure 포털에서에서 기존 Vnet을 만들 때 볼 수 있는 hello 이름은 PowerShell을 사용 하는 hello 전체 이름이 아닙니다. 예를 들어 라는 toobe 나타나는 VNet **TestVNet1** hello 포털에 있을 수는 훨씬 더 긴 이름을 hello 네트워크 구성 파일에 있습니다. hello 이름이 같을 수 있습니다: **그룹 ClassicRG TestVNet1**합니다. 사용자 연결을 만드는 경우는 hello 네트워크 구성 파일에서 볼 수 있는 중요 한 toouse hello 값입니다.

단계를 수행 하는 hello, tooyour Azure 계정을 연결 하는 데 하 고 다운로드 및 hello 네트워크 구성 파일 tooobtain hello 있는 값이 보기는 연결에 필요 합니다.

1. 다운로드 하 여 hello hello Azure 서비스 관리 (SM) PowerShell cmdlet의 최신 버전을 설치 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

2. 관리자 권한으로 PowerShell 콘솔을 열고 및 tooyour 계정을 연결 합니다. 다음 예제에서는 toohelp 연결한 hello를 사용 합니다.

  ```powershell
  Login-AzureRmAccount
  ```

  Hello 계정에 대 한 hello 구독을 확인 합니다.

  ```powershell
  Get-AzureRmSubscription
  ```

  둘 이상의 구독을 보유 하는 경우 toouse hello 구독을 선택 합니다.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  를 사용 하 여 다음 cmdlet tooadd hello Azure 구독 tooPowerShell hello 클래식 배포 모델에 대 한 합니다.

  ```powershell
  Add-AzureAccount
  ```
3. 내보낸 hello 네트워크 구성 파일을 확인 합니다. 컴퓨터에 디렉터리를 만들고 hello 네트워크 구성 파일 toohello 디렉터리를 내보냅니다. 이 예제에서는 hello 네트워크 구성 파일을 내보내려면 너무**C:\AzureNet**합니다.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. 표시 되는 텍스트 편집기 및 보기 hello 이름이 Vnet 및 사이트에 대 한 hello 파일을 엽니다. 이러한 연결을 만들 때 사용 하는 hello 이름이 됩니다.<br>VNet 이름은 **VirtualNetworkSite name =**으로 나열됩니다.<br>사이트 이름은 **LocalNetworkSiteRef name =**으로 나열됩니다.

## <a name="createconnections"></a>8 단계-hello VPN 게이트웨이 연결 만들기

Hello 위의 모든 단계를 모두 완료 되 면 hello IPsec/IKE 사전 공유 키를 설정할 수 있으며 hello 연결을 만듭니다. 이번 단계에서는 PowerShell을 사용합니다. VNet 대 VNet 연결 hello 클래식 배포 모델에 대 한 hello Azure 포털에서에서 구성할 수 없습니다.

Hello 예에서 hello 공유 키에 정확 하 게 hello 동일 합니다. 공유 키 hello 항상 일치 해야 합니다. 있는지 tooreplace hello Vnet 및 로컬 네트워크 사이트에 대 한 정확한 이름으로 이러한 예에서 hello 값 수입니다.

1. Hello TestVNet1 tooTestVNet4 연결을 만듭니다.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Hello TestVNet4 tooTestVNet1 연결을 만듭니다.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Hello 연결 tooinitialize 될 때까지 기다립니다. Hello 게이트웨이 초기화 되 면 hello 상태는 '성공'입니다.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>클래식 VNet에 대한 VNet-VNet 고려 사항
* hello에 hello 가상 네트워크 수 동일 하거나 다른 구독 합니다.
* hello에 hello 가상 네트워크 수 같거나 다른 Azure 지역 (위치).
* 클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.
* 여러 가상 네트워크를 연결할 때 VPN 장치는 필요하지 않습니다.
* VNet 간 연결은 Azure 가상 네트워크 연결을 지원합니다. 가상 컴퓨터 연결을 지원 하지 않습니다 또는 tooa 가상 네트워크를 배포 하지 않은 클라우드 서비스입니다.
* VNet-VNet을 위해서는 동적 라우팅 게이트웨이가 필요합니다. Azure 정적 라우팅 게이트웨이는 지원되지 않습니다.
* 가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다. 10 개의 VPN 터널이 다른 가상 네트워크 또는 온-프레미스 사이트 tooeither를 연결할 가상 네트워크 VPN 게이트웨이 최대가 있습니다.
* hello 주소 공간 hello 가상 네트워크와 온-프레미스 로컬 네트워크 사이트는 겹치지 않아야 합니다. 겹치는 주소 공간의 가상 네트워크 또는 업로드 netcfg 구성 파일 toofail hello 작성을 하면 됩니다.
* 가상 네트워크 한 쌍 간의 중복 터널은 지원되지 않습니다.
* VPN 터널 hello P2S Vpn을 포함 하 여 VNet에 대 한 모든 hello VPN 게이트웨이에 대 한 사용 가능한 대역폭 hello를 공유 하며 Azure에서 동일한 VPN 게이트웨이 작동 시간 SLA hello 합니다.
* VNet 대 VNet 트래픽이 hello Azure backbone 통과 합니다.

## <a name="next-steps"></a>다음 단계
연결을 확인합니다. [VPN Gateway 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.
