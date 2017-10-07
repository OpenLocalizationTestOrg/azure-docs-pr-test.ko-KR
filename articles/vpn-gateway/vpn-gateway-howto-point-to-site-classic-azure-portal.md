---
title: "지점 및 사이트 및 인증서 인증을 사용 하 여 컴퓨터 tooa 가상 네트워크에 연결: 기본 Azure 포털 | Microsoft Docs"
description: "안전 하 게 연결 tooyour hello Azure 포털을 사용 하 여 지점-사이트 VPN 게이트웨이 연결을 만들어 클래식 Azure 가상 네트워크입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>지점 및 사이트 연결 tooa VNet 구성 인증서 인증 (클래식)를 사용 하 여: Azure 포털

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

이 문서에서는 방법을 사용 하 여 hello 클래식 배포 모델에서 지점 및 사이트 연결 VNet toocreate hello Azure 포털을 보여 줍니다. 이 구성은 인증서 tooauthenticate hello 클라이언트 연결을 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다. 지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다. P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다. 

P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다. Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.


![지점 및 사이트 간 다이어그램](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


지점 및 사이트 인증서 인증 연결 hello 다음에 필요 합니다.

* 동적 VPN 게이트웨이
* hello tooAzure 업로드 된 루트 인증서에 대 한 공개 (키.cer 파일) 키입니다. 신뢰할 수 있는 인증서로 간주되며 인증에 사용됩니다.
* Hello 루트 인증서에서 생성 되 고 연결 하는 각 클라이언트 컴퓨터에 설치 된 클라이언트 인증서입니다. 클라이언트 인증에 사용됩니다.
* 연결하는 모든 클라이언트 컴퓨터에 VPN 클라이언트 구성 패키지를 생성하여 설치해야 합니다. hello 클라이언트 구성 패키지 hello 필요한 정보 tooconnect toohello VNet hello 운영 체제에 이미 있는 hello 기본 VPN 클라이언트를 구성 합니다.

지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다. VPN 연결 hello SSTP (Secure Socket Tunneling Protocol)를 통해 생성 됩니다. Hello 서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2 지원합니다. 클라이언트 hello 어떤 버전 toouse를 결정합니다. Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다. 

지점 및 사이트 간 연결에 대 한 자세한 내용은 참조 hello [지점 및 사이트 간 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

### <a name="example-settings"></a>예제 설정

값 toocreate 테스트 환경에 따라 hello를 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해:

* **이름: VNet1**
* **주소 공간: 192.168.0.0/16**<br>이 예제에서는 하나의 주소 공간만 사용합니다. VNet에는 둘 이상의 주소 공간을 포함할 수 있습니다.
* **서브넷 이름: FrontEnd**
* **서브넷 주소 범위: 192.168.1.0/24**
* **구독:** 사용 하 고 있는지 확인 하는 둘 이상의 구독이 있는 경우 hello 올바르다는 것입니다.
* **리소스 그룹: TestRG**
* **위치: 미국 동부**
* **연결 형식: 지점 및 사이트 간**
* **클라이언트 주소 공간: 172.16.201.0/24**. 이 지점 및 사이트 연결을 사용 하 여 VNet IP 주소에서 수신 toohello 연결 하는 VPN 클라이언트 hello 지정한 풀입니다.
* **GatewaySubnet: 192.168.200.0/24**. hello 게이트웨이 서브넷 hello 이름 'GatewaySubnet'를 사용 해야 합니다.
* **크기:** 선택 hello 게이트웨이 SKU toouse 되도록 합니다.
* **라우팅 유형: 동적**

## <a name="vnetvpn"></a>1. 가상 네트워크 및 VPN Gateway 만들기

시작하기 전에 Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.

### <a name="createvnet"></a>1부: 가상 네트워크 만들기

가상 네트워크가 아직 없는 경우 만듭니다. 스크린샷은 예제로 제공됩니다. 자신의 있는지 tooreplace hello 값 수입니다. 사용 하 여 VNet toocreate hello Azure 포털을 사용 하 여 hello 단계를 수행 합니다.

1. 브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.
2. **새로 만들기**를 클릭합니다. Hello에 **hello 마켓플레이스** 필드 ' 가상 네트워크 '를 입력 합니다. 찾을 **가상 네트워크** 에서 반환 하는 hello 목록 이동한 tooopen hello 클릭 **가상 네트워크** 페이지.

  ![가상 네트워크 검색 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Hello 아래 근처의 hello 가상 네트워크 페이지에서 hello **배포 모델 선택** 목록에서 선택 **클래식**, 클릭 하 고 **만들기**합니다.

  ![배포 모델 선택](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Hello에 **가상 네트워크 만들기** 페이지 hello VNet 설정을 구성 합니다. 이 페이지에서 첫 번째 주소 공간과 단일 서브넷 주소 범위를 추가합니다. Hello VNet 만들기를 마친 후에 다시 이동 하 고 주소 공간 및 서브넷을 더 추가할 수 있습니다.

  ![가상 네트워크 만들기 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. 해당 hello 확인 **구독** 는 hello 올바르다는 것입니다. Hello 드롭 다운을 사용 하 여 구독을 변경할 수 있습니다.
6. **리소스 그룹** 을 클릭하고 기존 리소스 그룹을 선택하거나 새 리소스 그룹에 대한 이름을 입력하여 새로 만듭니다. 새 리소스 그룹을 만드는 경우 tooyour에 따라 이름 hello 리소스 그룹 구성 값을 계획 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
7. 다음으로, 선택 hello **위치** VNet에 대 한 설정입니다. hello 위치 toothis VNet을 배포 하는 hello 리소스 상주할 위치를 결정 합니다.
8. 선택 **Pin toodashboard** toobe 수 toofind hello 대시보드에 쉽게 VNet을 클릭 하는 경우 **만들기**합니다.

  ![Pin toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. 만들기를 클릭 한 후 타일은 VNet의 hello 진행 상태를 반영 하 여 대시보드에 나타납니다. hello와 hello 타일 변경 사항이 VNet은 만드는 중입니다.

  ![가상 네트워크 만들기 타일](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. 가상 네트워크를 만든 후 참조 **Created** 아래에 나열 **상태** hello Azure 클래식 포털의에서 네트워크 페이지 hello 합니다.
11. DNS 서버를 추가합니다(선택 사항). 가상 네트워크를 만든 후에 이름 확인에 DNS 서버의 hello IP 주소를 추가할 수 있습니다. hello 지정 하는 DNS 서버 IP 주소에는 VNet의 hello 리소스에 대 한 hello 이름을 확인할 수 있는 DNS 서버 hello 주소 여야 합니다.<br>가상 네트워크에 대 한 hello 설정을 열고 DNS 서버를 클릭 toouse 원하는 hello DNS 서버의 hello IP 주소를 추가 하는 tooadd DNS 서버를 합니다.

### <a name="gateway"></a>2부: 게이트웨이 서브넷 및 동적 라우팅 게이트웨이 만들기

이 단계에서는 게이트웨이 서브넷 및 동적 라우팅 게이트웨이를 만듭니다. Hello hello 클래식 배포 모델에 대 한 Azure 포털에서에서 hello 게이트웨이 서브넷을 만들고 hello 게이트웨이 통해 수행할 수 있습니다 hello 동일한 구성 페이지입니다.

1. Hello 포털에서 게이트웨이 toocreate 원하는 toohello 가상 네트워크를 이동 합니다.
2. Hello에 가상 네트워크에 대 한 hello 페이지 **개요** 페이지 hello VPN 연결 섹션에서 클릭 **게이트웨이**합니다.

  ![Toocreate 게이트웨이 클릭 합니다.](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Hello에 **새 VPN 연결** 페이지에서 **지점-사이트**합니다.

  ![지점 및 사이트 간 연결 형식](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. 에 대 한 **클라이언트 주소 공간**, hello IP 주소 범위를 추가 합니다. Hello 범위가 있는 hello VPN 클라이언트가 IP 주소를 받을 연결할 때 되었습니다. 연결 하려는 hello 온-프레미스 위치와 또는 VNet tooconnect을 hello로 중복 되지 않는 개인 IP 주소 범위를 사용 합니다. Hello 개인 IP 주소 범위 추가 toouse 되도록 다음 hello 자동으로 채워진 범위를 삭제할 수 있습니다.

  ![클라이언트 주소 공간](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. 선택 hello **게이트웨이 즉시 만들기** 확인란을 선택 합니다.

  ![게이트웨이 즉시 만들기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. 클릭 **선택적 게이트웨이 구성** tooopen hello **게이트웨이 구성** 페이지.

  ![선택적 게이트웨이 구성 클릭](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. 클릭 **필요한 서브넷 구성 설정** tooadd hello **게이트웨이 서브넷**합니다. 가능한 toocreate/29 수신자로 게이트웨이 서브넷 이지만, 적어도/28 또는/27 선택 하 여 더 많은 주소를 포함 하는 큰 서브넷을 만들어야 하는 것이 좋습니다. 이렇게 하면 충분 한 주소 tooaccommodate 가능한 추가 되는 구성에 만한 hello 이후 있습니다. 게이트웨이 서브넷에서 작업할 때는 네트워크 보안 그룹 (NSG) toohello 게이트웨이 서브넷에 연결 하지 마십시오. 네트워크 보안 그룹 toothis 서브넷 연결 예상 대로 작동 하 여 VPN 게이트웨이 toostop을 발생할 수 있습니다.

  ![GatewaySubnet 추가](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. 선택 hello 게이트웨이 **크기**합니다. hello 크기는 가상 네트워크 게이트웨이에 대 한 hello 게이트웨이 SKU입니다. Hello 포털에서 hello 기본 SKU가 **기본**합니다. 게이트웨이 SKU에 대한 자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.

  ![게이트웨이 크기](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. 선택 hello **라우팅 유형** 게이트웨이에 대 한 합니다. P2S 구성에는 **동적** 라우팅 유형이 필요합니다. 이 페이지 구성을 완료했으면 **확인**을 클릭합니다.

  ![라우팅 유형 구성](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Hello에 **새 VPN 연결** 페이지 **확인** 가상 네트워크 게이트웨이 만들기 hello 페이지 toobegin hello 맨 아래에 있습니다. VPN 게이트웨이 선택 하는 hello 게이트웨이 sku에 따라 too45 분 toocomplete 차지할 수 있습니다.

## <a name="generatecerts"></a>2. 인증서 만들기

인증서는 지점-사이트 Vpn에 대 한 Azure tooauthenticate VPN 클라이언트에 의해 사용 됩니다. Hello hello 루트 인증서 tooAzure의 공개 키 정보를 업로드 합니다. 공개 키 hello는 '신뢰할 수 있는'으로 간주 됩니다. 클라이언트 인증서 hello 신뢰할 수 있는 루트 인증서에서 생성 하 고 hello 인증서-현재 사용자/개인 인증서 저장소에서 각 클라이언트 컴퓨터에 설치 해야 합니다. 연결 toohello VNet을 시작할 때 hello 인증서는 사용 되는 tooauthenticate hello 클라이언트입니다. 

자체 서명된 인증서를 사용하는 경우 특정 매개 변수를 사용하여 만들어야 합니다. 에 대 한 hello 지침을 사용 하 여 자체 서명 된 인증서를 만들 수 있습니다 [PowerShell 및 Windows 10](vpn-gateway-certificates-point-to-site.md), 또는 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)합니다. 자체 서명 된 루트 인증서를 hello에서 클라이언트 인증서를 생성 및 자체 서명 된 루트 인증서를 사용 하는 경우 이러한 지침에 설명 된 hello 단계를 수행 합니다. 그렇지 않은 경우 만든 hello 인증서 P2S 연결와 호환 되지 않으며 연결 오류가 발생 합니다.

### <a name="cer"></a>1 부: hello 루트 인증서에 대 한 hello 공개 키 (.cer)를 가져올

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>2부: 클라이언트 인증서 생성

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Hello 루트 인증서.cer 파일 업로드

Hello 게이트웨이 만든 후에 신뢰할 수 있는 루트 인증서 tooAzure에 대 한 (을 hello 공개 키 정보를 포함) hello.cer 파일을 업로드할 수 있습니다. 루트 인증서 tooAzure hello에 대 한 hello 개인 키를 업로드 하지 마세요. A.cer 파일이 업로드 되 면 Azure 사용할 수 tooauthenticate 클라이언트 hello 신뢰할 수 있는 루트 인증서에서 생성 된 클라이언트 인증서를 설치 합니다. 필요한 경우-tooa 총 20-나중를 신뢰할 수 있는 루트 인증서 파일을 업로드할 수 있습니다.  

1. Hello에 **VPN 연결** 섹션 VNet에 대 한 hello 페이지의 클릭 hello **클라이언트** 그래픽 tooopen hello **지점 및 사이트 간 VPN 연결** 페이지.

  ![클라이언트](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Hello에 **지점 및 사이트 연결** 페이지 **인증서 관리** tooopen hello **인증서** 페이지.<br>

  ![인증서 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Hello에 **인증서** 페이지 **업로드** tooopen hello **인증서 업로드** 페이지.<br>

    ![인증서 업로드 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Hello 그래픽 toobrowse hello.cer 파일에 대 한 폴더를 클릭 합니다. Hello 파일을 선택한 다음 클릭 **확인**합니다. Hello에 새로 고침 hello 페이지 toosee 업로드 hello 인증서 **인증서** 페이지.

  ![인증서 업로드](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Hello 클라이언트 구성

tooconnect tooa VNet 지점-사이트 VPN을 사용 하 여 각 클라이언트 패키지 tooconfigure hello 네이티브 Windows VPN 클라이언트를 설치 해야 합니다. hello 구성 패키지 hello 설정 필요한 tooconnect toohello 가상 네트워크와 hello 네이티브 Windows VPN 클라이언트를 구성합니다.

클라이언트 hello에 대 한 hello 아키텍처를 일치 하는 hello 버전으로 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지 hello를 사용할 수 있습니다. 지원 되는 클라이언트 운영 체제의 hello 목록 참조 hello [지점 및 사이트 연결 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

### <a name="generateconfigpackage"></a>1 부: 생성 및 hello VPN 클라이언트 구성 패키지를 설치 합니다.

1. Hello hello에서 Azure 포털에서에서 **개요** VNet을에 대 한 페이지에 **VPN 연결**, hello 클라이언트 그래픽 tooopen hello 클릭 **지점 및 사이트 간 VPN 연결** 페이지.
2. Hello의 hello 위쪽 **지점 및 사이트 간 VPN 연결** 페이지 toohello 클라이언트 운영 체제에 설치 됩니다 해당 하는 hello 다운로드 패키지를 클릭 합니다.

  * 64비트 클라이언트인 경우 **VPN 클라이언트(64비트)**를 선택합니다.
  * 32비트 클라이언트인 경우 **VPN 클라이언트(32비트)**를 선택합니다.

  ![VPN 클라이언트 구성 패키지 다운로드](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. 다운로드 패키지 hello 생성 되 면 클라이언트 컴퓨터에 설치 합니다. SmartScreen 팝업이 표시되면 **자세한 정보**, **실행**을 차례로 클릭합니다. Hello 패키지 tooinstall 다른 클라이언트 컴퓨터에 저장할 수도 있습니다.

### <a name="installclientcert"></a>2 부: hello 클라이언트 인증서 설치

Hello 아닌 클라이언트 컴퓨터에서 toogenerate hello 클라이언트 인증서를 사용 하는 P2S toocreate 연결 tooinstall 클라이언트 인증서를 해야 합니다. 클라이언트 인증서를 설치할 때 클라이언트 인증서 hello을 내보낼 때 만든 hello 암호가 필요 합니다. 일반적으로 hello 인증서를 두 번 클릭 하 고 설치 하는 것 만으로입니다. 자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요.

## <a name="connect"></a>5. TooAzure 연결

### <a name="connect-tooyour-vnet"></a>Tooyour VNet 연결

1. hello 클라이언트 컴퓨터에서 tooconnect tooyour VNet tooVPN 연결 이동한 만든 hello VPN 연결을 찾습니다. 가상 네트워크 이름이 hello를 라고 합니다. **Connect**를 클릭합니다. 팝업 메시지 toousing hello 인증서 참조 나타날 수 있습니다. 이 경우 클릭 **계속** toouse 상승 된 권한을 합니다.
2. Hello에 **연결** 상태 페이지 클릭 **연결** toostart hello 연결 합니다. 표시 되 면 한 **인증서 선택** 화면에서 클라이언트 인증서 표시 된 hello toouse tooconnect 원하는 hello 하나 인지 확인 합니다. 없는 경우 hello 드롭 다운 화살표 tooselect hello 올바른 인증서를 사용 하 고 클릭 **확인**합니다.

  ![VPN 클라이언트 연결](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. 연결이 설정되었습니다.

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S 연결 문제 해결

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Hello VPN 연결 확인

1. VPN 연결을 활성 상태 인지 tooverify 관리자 명령 프롬프트를 열고 실행 *ipconfig/all*합니다.
2. Hello 결과 확인 합니다. 받은 hello IP 주소가 VNet을 만들 때 지정한 hello 지점 및 사이트 간 연결 주소 범위 내의 hello 주소 중 하나 인지 확인 합니다. hello 결과 비슷한 예는 toothis 됩니다.

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Tooa 가상 컴퓨터에 연결

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>신뢰할 수 있는 루트 인증서 추가 또는 제거

Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다. 루트 인증서를 제거 하면 해당 루트에서 생성 된 인증서가 클라이언트 수 tooauthenticate 됩니다 하 고 따라서 수 tooconnect 되지 않습니다. 클라이언트 tooauthenticate 원하는 연결 하는 경우 tooinstall 루트 인증서를 신뢰할 수 있는 (업로드) tooAzure에서 새 클라이언트 인증서를 생성 해야 합니다.

### <a name="addtrustedroot"></a>tooadd 신뢰할 수 있는 루트 인증서

Too20 신뢰할 수 있는 루트 인증서.cer 파일 tooAzure를 추가할 수 있습니다. 자세한 내용은 [섹션 3-업로드 hello 루트 인증서.cer 파일](#upload)합니다.

### <a name="removetrustedroot"></a>tooremove 신뢰할 수 있는 루트 인증서

1. Hello에 **VPN 연결** 섹션 VNet에 대 한 hello 페이지의 클릭 hello **클라이언트** 그래픽 tooopen hello **지점 및 사이트 간 VPN 연결** 페이지.

  ![클라이언트](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Hello에 **지점 및 사이트 연결** 페이지 **인증서 관리** tooopen hello **인증서** 페이지.<br>

  ![인증서 페이지](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Hello에 **인증서** 페이지에서 hello 줄임표 다음 toohello 인증서 tooremove, 원하는 다음 클릭 있습니다 **삭제**합니다.

  ![루트 인증서 삭제](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>클라이언트 인증서 해지

클라이언트 인증서를 해지할 수 있습니다. hello 인증서 해지 목록을 통해 tooselectively 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 연결을 거부 합니다. 이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다. Azure에서 신뢰할 수 있는 루트 인증서.cer를 제거 하면 모든 클라이언트 인증서를 서명 생성/된 hello 해지 된 루트 인증서에 의해 hello 액세스 권한을 취소 합니다. 클라이언트 인증서를 해지 hello 루트 인증서를 대신 허용 hello hello 루트 인증서 toocontinue toobe hello 지점 및 사이트 간 연결에 대 한 인증에 사용 되는에서 생성 된 다른 인증서입니다.

hello 일반적으로 개별 사용자에 대 한 세분화 된 액세스 제어에 대 한 해지 된 클라이언트 인증서를 사용 하는 동안 팀 또는 조직 수준에서 toouse hello 루트 인증서 toomanage 액세스가 됩니다.

### <a name="revokeclientcert"></a>toorevoke 클라이언트 인증서

Hello 지문 toohello 해지 목록에 추가 하 여 클라이언트 인증서를 해지할 수 있습니다.

1. Hello 클라이언트 인증서 지문을 검색 합니다. 자세한 내용은 참조 [하는 방법: 인증서의 지문 검색 hello](https://msdn.microsoft.com/library/ms734695.aspx)합니다.
2. Hello 정보 tooa 텍스트 편집기를 복사 하 고 모든 공백을 제거 하는 연속 문자열.
3. Toohello 이동 **'클래식 가상 네트워크 이름' > 지점-사이트 VPN 연결 > 인증서** 페이지 한 다음 클릭 **해지 목록** tooopen hello 해지 목록 페이지. 
4. Hello에 **해지 목록** 페이지 **+ 인증서 추가** tooopen hello **추가 인증서 toorevocation 목록** 페이지.
5. Hello에 **추가 인증서 toorevocation 목록** 페이지, hello 인증서 지문을 공백 없이 한 연속 줄의 텍스트를 붙여 넣습니다. 클릭 **확인** hello hello 페이지 맨 아래에 있습니다.
6. 업데이트 완료 되 면 hello 인증서 사용된 tooconnect를 더 이상 수 없습니다. Tooconnect이이 인증서를 사용 하 여 시도 하는 클라이언트 hello 인증서를 더 이상 사용할 수 없다는 메시지를 수신 합니다.

## <a name="faq"></a>지점 및 사이트 간 FAQ

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>다음 단계
연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요. 네트워킹 및 가상 컴퓨터에 대해 자세히 toounderstand 참조 [Azure와 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)합니다.
