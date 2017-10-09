---
title: "지점 및 사이트 및 인증서 인증을 사용 하 여 컴퓨터 tooa 가상 네트워크에 연결: Azure 포털 | Microsoft Docs"
description: "인증서 인증을 사용 하는 지점-사이트 VPN 게이트웨이 연결을 생성 하 여 컴퓨터 tooyour Azure 가상 네트워크를 안전 하 게 연결 합니다. 이 문서 toohello 리소스 관리자 배포 모델에 적용 하 고 hello Azure 포털을 사용 합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: Azure 포털

이 문서 toocreate hello 리소스 관리자 배포 사용 하 여 모델에서 지점 및 사이트 연결 VNet Azure 포털을 hello 하는 방법을 보여 줍니다. 이 구성은 인증서 tooauthenticate hello 클라이언트 연결을 사용 합니다. 또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.

> [!div class="op_single_selector"]
> * [Azure 포털](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal(클래식)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다. 지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다. P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다. 

P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다. Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.

![지점 및 사이트 간 다이어그램](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

지점 및 사이트 인증서 인증 연결 hello 다음에 필요 합니다.

* RouteBased VPN 게이트웨이입니다.
* hello tooAzure 업로드 된 루트 인증서에 대 한 공개 (키.cer 파일) 키입니다. Hello 인증서를 업로드 한 후 인증서를 신뢰할 수 있는 것으로 간주 됩니다 하 고 인증을 위해 사용 됩니다.
* Hello 루트 인증서에서 생성 되 고 toohello VNet 연결 하는 각 클라이언트 컴퓨터에 설치 되는 클라이언트 인증서입니다. 클라이언트 인증에 사용됩니다.
* VPN 클라이언트 구성 패키지. hello VPN 클라이언트 구성 패키지 hello hello 클라이언트 tooconnect toohello VNet에 대 한 필요한 정보를 포함합니다. hello 패키지 hello 기존 VPN 클라이언트는 네이티브 toohello Windows 운영 체제를 구성 합니다. 연결 하는 각 클라이언트 hello 구성 패키지를 사용 하 여 구성 되어야 합니다.

지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다. VPN 연결 hello SSTP (Secure Socket Tunneling Protocol)를 통해 생성 됩니다. Hello 서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2 지원합니다. 클라이언트 hello 어떤 버전 toouse를 결정합니다. Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다.

지점 및 사이트 간 연결에 대 한 자세한 내용은 참조 hello [지점 및 사이트 간 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

#### <a name="example"></a>예제 값

값 toocreate 테스트 환경에 따라 hello를 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해:

* **VNet 이름:** VNet1
* **주소 공간:** 192.168.0.0/16<br>이 예제에서는 하나의 주소 공간만 사용합니다. VNet에는 둘 이상의 주소 공간을 포함할 수 있습니다.
* **서브넷 이름:** FrontEnd
* **서브넷 주소 범위:** 192.168.1.0/24
* **구독:** 사용 하 고 있는지 확인 하는 둘 이상의 구독이 있는 경우 hello 올바르다는 것입니다.
* **리소스 그룹:** TestRG
* **위치:** 미국 동부
* **GatewaySubnet:** 192.168.200.0/24<br>
* **DNS 서버:** 이름 확인을 위해 toouse 되도록 hello DNS 서버의 IP 주소 (선택 사항).
* **가상 네트워크 게이트웨이 이름:** VNet1GW
* **게이트웨이 유형:** VPN
* **VPN 유형:** 경로 기반
* **공용 IP 주소 이름:** VNet1GWpip
* **연결 형식:** 지점 및 사이트 간
* **클라이언트 주소 풀:** 172.16.201.0/24<br>Toohello VNet이 지점 및 사이트 연결을 사용 하 여 연결 하는 VPN 클라이언트 hello 클라이언트 주소 풀에서 IP 주소를 받습니다.

## <a name="createvnet"></a>1. 가상 네트워크 만들기

시작하기 전에 Azure 구독이 있는지 확인합니다. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. 게이트웨이 서브넷 추가

가상 네트워크 tooa 게이트웨이 연결 하기 전에 먼저 toocreate hello 게이트웨이 서브넷 tooconnect 원하는 가상 네트워크 toowhich hello에 대 한 합니다. hello 게이트웨이 서비스는 hello 게이트웨이 서브넷에 지정 된 hello IP 주소를 사용 합니다. 가능 하면/28 또는/27 CIDR 블록을 사용 하 여 게이트웨이 서브넷을 만든 tooprovide 충분 한 IP tooaccommodate 앞으로 추가 구성 요구 사항을 충족 합니다.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. DNS 서버 지정(선택 사항)

가상 네트워크를 만든 후에 DNS 서버 toohandle 이름 확인의 hello IP 주소를 추가할 수 있습니다. hello DNS 서버는이 구성에 대 한 선택 사항 이지만 이름 확인 하려는 경우에 필요 합니다. 값을 지정하더라도 새 DNS 서버를 만들지 않습니다. hello DNS 서버 IP 주소 지정 하는 DNS 서버가 있어야에 연결 하는 hello 리소스에 대 한 hello 이름을 확인할 수 있는 합니다. 이 예에서는 개인 IP 주소를 사용 하지만 DNS 서버의 IP 주소 hello 아닌지 가능성이 쉽습니다. 있는지 toouse 고유한 값 이어야 합니다.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. 가상 네트워크 게이트웨이 만들기

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. 인증서 생성

인증서는 tooa VNet에 지점-사이트 VPN 연결을 통해 연결 하는 Azure tooauthenticate 클라이언트에서 사용 됩니다. 루트 인증서를 가져오고 나면 있습니다 [업로드](#uploadfile) 공개 키 정보 tooAzure hello 합니다. P2S toohello 가상 네트워크를 통해 hello 루트 인증서를 '신뢰할 수 있는' Azure에서 연결에 대 한 간주 다음 됩니다. 또한 hello 신뢰할 수 있는 루트 인증서에서 클라이언트 인증서를 생성 하 고 각 클라이언트 컴퓨터에 설치 합니다. hello 클라이언트 인증서 사용 되는 tooauthenticate hello 클라이언트 때 연결 toohello VNet을 시작 합니다. 

### <a name="getcer"></a>1. Hello 루트 인증서에 대 한 hello.cer 파일을 가져오려면

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. 클라이언트 인증서 생성

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Hello 클라이언트 주소 풀이 추가

hello 클라이언트 주소 풀이 지정 하는 개인 IP 주소 범위입니다. 지점-사이트 VPN을 통해 연결 하는 hello 클라이언트는이 범위에서 IP 주소를 받습니다. , 연결 하는 hello 온-프레미스 위치 또는 VNet tooconnect을 hello와 겹치지 않는 개인 IP 주소 범위를 사용 합니다.

1. Hello 가상 네트워크 게이트웨이 만든 후 이동 toohello **설정을** hello 가상 네트워크 게이트웨이 페이지의 섹션입니다. Hello에 **설정** 섹션에서 클릭 **지점-사이트 구성** tooopen hello **지점-에-사이트-구성** 페이지.

  ![지점 및 사이트 간 페이지](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Hello에 **지점-에-사이트-구성** 페이지 hello 개인 IP 주소 범위 추가 toouse 원하는 다음 hello 자동으로 채워진 범위를 삭제할 수 있습니다. 클릭 **저장** toovalidate hello 설정을 저장 합니다.

  ![클라이언트 주소 풀](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Hello 루트 인증서 공용 인증서 데이터를 업로드 합니다.

Hello 게이트웨이 만든 후 hello 루트 인증서 tooAzure hello에 대 한 공개 키 정보를 업로드 합니다. Hello 공용 인증서 데이터를 업로드 한 후 Azure 사용할 수 tooauthenticate 클라이언트 hello 신뢰할 수 있는 루트 인증서에서 생성 된 클라이언트 인증서를 설치 합니다. 신뢰할 수 있는 루트 인증서 접속 tooa 총 20 업로드할 수 있습니다.

1. Hello에 인증서를 추가 **지점-사이트 구성** hello에서 페이지 **루트 인증서** 섹션.  
2. E-64로 인코딩된 X.509 (.cer) 파일 처럼 hello 루트 인증서를 내보낸 있는지 확인 합니다. 텍스트 편집기로 hello 인증서를 열 수 있도록이 형식 tooexport hello 인증서를 필요 합니다.
3. Hello 인증서를 메모장과 같은 텍스트 편집기로 엽니다. Hello 인증서 데이터를 복사할 때 캐리지 리턴 또는 줄 바꿈 없이 한 연속 줄으로 hello 텍스트를 복사 해야 합니다. Toomodify hello 텍스트 편집기 too'Show 기호/표시 모든 문자 toosee hello 캐리지 리턴 및 줄에서 보기를 할 수 있습니다. 다음 섹션을 한 연속 줄으로만 hello를 복사 합니다.

  ![인증서 데이터](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Hello에 hello 인증서 데이터를 붙여 **공용 인증서 데이터** 필드입니다. **이름** hello 인증서를 클릭 하 고 **저장**합니다. Too20 신뢰할 수 있는 루트 인증서를 추가할 수 있습니다.

  ![인증서 업로드](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. 생성 하 고 hello VPN 클라이언트 구성 패키지를 설치 합니다.

hello 설정을 사용 하 여 hello 기본 VPN 클라이언트를 구성 하는 클라이언트 구성 패키지와 파일은 필요한 tooconnect toohello 가상 네트워크 tooconnect tooa VNet 지점-사이트 VPN을 사용 하 여 각 클라이언트를 설치 해야 합니다. hello 네이티브 Windows VPN 클라이언트를 구성 하는 hello VPN 클라이언트 구성 패키지, 다른 또는 새로운 VPN 클라이언트를 설치 하지 않습니다.

클라이언트 hello에 대 한 hello 아키텍처를 일치 하는 hello 버전으로 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지 hello를 사용할 수 있습니다. 지원 되는 클라이언트 운영 체제의 hello 목록 참조 hello [지점 및 사이트 연결 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>1 단계-생성 하 고 hello 클라이언트 구성 패키지를 다운로드 합니다.

1. Hello에 **지점-사이트 구성** 페이지 **다운로드 VPN 클라이언트** tooopen hello **다운로드 VPN 클라이언트** 페이지. 패키지 toogenerate hello에 대 일 분 정도 걸립니다.

  ![VPN 클라이언트 다운로드 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. 클라이언트에 대 한 hello 올바른 패키지를 선택한 다음 클릭 **다운로드**합니다. Hello 구성 패키지 파일을 저장 합니다. Toohello 가상 네트워크를 연결 하는 각 클라이언트 컴퓨터에서 hello VPN 클라이언트 구성 패키지를 설치 합니다.

  ![VPN 클라이언트 다운로드 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>2 단계-hello 클라이언트 구성 패키지 설치

1. Hello 구성 파일을 복사 toohello 컴퓨터 로컬로 tooconnect tooyour 가상 네트워크 되도록 합니다. 
2. Hello.exe 파일 tooinstall hello 패키지 hello 클라이언트 컴퓨터에서 두 번 클릭 합니다. Hello 구성 패키지에 만들어지므로, 서명 되지 않은 및 경고가 표시 될 수 있습니다. Windows SmartScreen 팝업을 발생 하면 클릭 **자세히** hello 왼쪽), (on 다음 **그래도 실행** tooinstall hello 패키지 합니다.
3. Hello 패키지 hello 클라이언트 컴퓨터에 설치 합니다. Windows SmartScreen 팝업을 발생 하면 클릭 **자세히** hello 왼쪽), (on 다음 **그래도 실행** tooinstall hello 패키지 합니다.
4. Hello 클라이언트 컴퓨터에서 이동 너무**네트워크 설정** 클릭 **VPN**합니다. hello VPN 연결에 연결 하는 hello 가상 네트워크의 hello 이름을 보여 줍니다.

## <a name="installclientcert"></a>9. 내보낸 클라이언트 인증서 설치

Hello 아닌 클라이언트 컴퓨터에서 toogenerate hello 클라이언트 인증서를 사용 하는 P2S toocreate 연결 tooinstall 클라이언트 인증서를 해야 합니다. 클라이언트 인증서를 설치할 때 클라이언트 인증서 hello을 내보낼 때 만든 hello 암호가 필요 합니다. 일반적으로의 hello 인증서를 두 번 클릭 하 고 설치 합니다.

Hello 클라이언트 인증서 hello 전체 인증서 체인 (즉, hello 기본값)와 함께.pfx로 내보낸 있는지 확인 합니다. 그렇지 않으면 hello 루트 인증서 정보를 hello 클라이언트 컴퓨터에 존재 하지 않는 및 hello 클라이언트 수 tooauthenticate를 제대로 수 없습니다. 자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요.

## <a name="connect"></a>10. TooAzure 연결

1. hello 클라이언트 컴퓨터에서 tooconnect tooyour VNet tooVPN 연결 이동한 만든 hello VPN 연결을 찾습니다. 가상 네트워크 이름이 hello를 라고 합니다. **Connect**를 클릭합니다. 팝업 메시지 toousing hello 인증서 참조 나타날 수 있습니다. 클릭 **계속** toouse 상승 된 권한을 합니다.

2. Hello에 **연결** 상태 페이지 클릭 **연결** toostart hello 연결 합니다. 표시 되 면 한 **인증서 선택** 화면에서 클라이언트 인증서 표시 된 hello toouse tooconnect 원하는 hello 하나 인지 확인 합니다. 없는 경우 hello 드롭 다운 화살표 tooselect hello 올바른 인증서를 사용 하 고 클릭 **확인**합니다.

  ![VPN 클라이언트가 tooAzure 연결](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. 연결이 설정되었습니다.

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S 연결 문제 해결

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. 연결 확인

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

## <a name="add"></a>신뢰할 수 있는 루트 인증서 추가 또는 제거

Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다. 루트 인증서를 제거 하면 해당 루트에서 생성 된 인증서가 클라이언트 수 tooauthenticate 됩니다 하 고 따라서 수 tooconnect 되지 않습니다. 클라이언트 tooauthenticate 원하는 연결 하는 경우 tooinstall 루트 인증서를 신뢰할 수 있는 (업로드) tooAzure에서 새 클라이언트 인증서를 생성 해야 합니다.

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd 신뢰할 수 있는 루트 인증서

Too20 신뢰할 수 있는 루트 인증서.cer 파일 tooAzure를 추가할 수 있습니다. Hello 섹션을 참조 하십시오 [신뢰할 수 있는 루트 인증서 업로드](#uploadfile) 이 문서의 내용입니다.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove 신뢰할 수 있는 루트 인증서

1. 신뢰할 수 있는 루트 인증서 tooremove 이동 toohello **지점-사이트 구성** 가상 네트워크 게이트웨이에 대 한 페이지입니다.
2. Hello에 **루트 인증서** 섹션 hello 페이지의 tooremove hello 인증서를 찾습니다.
3. Hello 줄임표 다음 toohello 인증서를 클릭 하 고 '제거'를 클릭 합니다.

## <a name="revokeclient"></a>클라이언트 인증서 해지

클라이언트 인증서를 해지할 수 있습니다. hello 인증서 해지 목록을 통해 tooselectively 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 연결을 거부 합니다. 이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다. Azure에서 신뢰할 수 있는 루트 인증서.cer를 제거 하면 모든 클라이언트 인증서를 서명 생성/된 hello 해지 된 루트 인증서에 의해 hello 액세스 권한을 취소 합니다. 클라이언트 인증서를 해지 hello 루트 인증서를 대신 허용 hello 인증에 사용 하는 hello 루트 인증서 toocontinue toobe에서 생성 된 다른 인증서입니다.

hello 일반적으로 개별 사용자에 대 한 세분화 된 액세스 제어에 대 한 해지 된 클라이언트 인증서를 사용 하는 동안 팀 또는 조직 수준에서 toouse hello 루트 인증서 toomanage 액세스가 됩니다.

### <a name="toorevoke-a-client-certificate"></a>toorevoke 클라이언트 인증서

Hello 지문 toohello 해지 목록에 추가 하 여 클라이언트 인증서를 해지할 수 있습니다.

1. Hello 클라이언트 인증서 지문을 검색 합니다. 자세한 내용은 참조 [어떻게 tooretrieve hello 인증서의 지문을](https://msdn.microsoft.com/library/ms734695.aspx)합니다.
2. Hello 정보 tooa 텍스트 편집기를 복사 하 고 모든 공백을 제거 하는 연속 문자열.
3. 가상 네트워크 게이트웨이 toohello 이동 **지점-에-사이트-구성** 페이지. 이 hello 너무 사용 되는 동일한 페이지[신뢰할 수 있는 루트 인증서 업로드](#uploadfile)합니다.
4. Hello에 **해지 된 인증서** 섹션, hello 인증서 (없어도 toobe hello 인증서 CN)에 사용할 이름을 입력 합니다.
5. 복사 및 붙여넣기 hello 지문 문자열 toohello **지문** 필드입니다.
6. hello 지문을 확인 하 고 toohello 해지 목록에 자동으로 추가 됩니다. 해당 hello hello 화면에 메시지가 표시 목록을 업데이트 하는 중입니다. 
7. 업데이트 완료 되 면 hello 인증서 사용된 tooconnect를 더 이상 수 없습니다. Tooconnect이이 인증서를 사용 하 여 시도 하는 클라이언트 hello 인증서를 더 이상 사용할 수 없다는 메시지를 수신 합니다.

## <a name="faq"></a>지점 및 사이트 간 FAQ

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>다음 단계
연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다. 자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요. 네트워킹 및 가상 컴퓨터에 대해 자세히 toounderstand 참조 [Azure와 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)합니다.
