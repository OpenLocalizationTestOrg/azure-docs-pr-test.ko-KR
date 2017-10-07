---
title: "가상 네트워크와 aaaHow toouse Azure API 관리"
description: "어떻게 toosetup Azure API 관리 및 액세스 하는 웹에서 연결 tooa 가상 네트워크는이 통해을 서비스에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>어떻게 가상 네트워크와 toouse Azure API 관리
Azure 가상 네트워크 (Vnet)를 사용 하면 tooplace 액세스 하는 모든 사용자가 제어 하는 인터넷이 아닌 routeable 네트워크에 Azure 리소스가 있습니다. 이러한 네트워크 다양 한 VPN 기술을 사용 하 여 연결 된 tooyour 온-프레미스 네트워크 수 있습니다. 여기에 hello 정보로 시작 하는 Azure 가상 네트워크에 대 한 자세한 toolearn: [Azure 가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)합니다.

Hello 네트워크 내에서 백 엔드 서비스에 액세스할 수 있도록 hello 가상 네트워크 (VNET) 내의 azure API 관리를 배포할 수 있습니다. 개발자 포털 및 API 게이트웨이 hello, 구성 된 toobe hello 인터넷 또는 hello 가상 네트워크 내 에서만 액세스할 수 있습니다.

> [!NOTE]
> Azure API Management는 클래식 및 Azure Resource Manager Vnet을 모두 지원합니다.
>
>

## <a name="enable-vpn"> </a>VNET 연결 사용
> [!NOTE]
> VNET 연결 기능은 hello 사용할 **프리미엄** 및 **개발자** 계층입니다. hello 계층 간 tooswitch hello Azure 포털에서에서 API 관리 서비스를 연 다음 hello를 열어 **배율과 가격** 탭 합니다. Hello에서 **가격 책정 계층** 섹션 hello 개발자 또는 Premium 계층을 선택 하 고 저장을 클릭 합니다.
>

tooenable VNET 연결 hello Azure 포털에서에서 API 관리 서비스를 열고 hello 열고 **가상 네트워크** 페이지.

![API 관리의 가상 네트워크 메뉴][api-management-using-vnet-menu]

Hello 필요한 액세스 유형을 선택 합니다.

* **외부**: hello API 관리 게이트웨이 및 개발자 포털에서 액세스할 수 있는 공용 인터넷에서 외부 부하 분산 장치를 통해 hello 합니다. hello 게이트웨이 hello 가상 네트워크 내에서 리소스에 액세스할 수 있습니다.

![공용 피어링][api-management-vnet-public]

* **내부**: hello API 관리 게이트웨이 및 개발자 포털은 hello는 내부 부하 분산 장치를 통해 가상 네트워크 내 에서만 액세스할 수 있습니다. hello 게이트웨이 hello 가상 네트워크 내에서 리소스에 액세스할 수 있습니다.

![개인 피어링][api-management-vnet-private]

이제 API 관리 서비스가 프로비전되는 모든 지역 목록이 보입니다. VNET 및 모든 지역에 대한 서브넷을 선택합니다. hello 목록 기본 및 리소스 관리자 가상 네트워크를 구성 하는 hello 영역의 설정 되도록 하 여 Azure 구독에서 사용할 수 있는 채워집니다.

> [!NOTE]
> **서비스 끝점** hello 위의 다이어그램에서에서 게이트웨이/프록시, 게시자 포털, 개발자 포털, GIT, 및 hello 직접 관리 끝점이 포함 됩니다.
> **관리 끝점** hello 다이어그램 위의 Powershell 및 Azure 포털을 통해 hello 서비스 toomanage 구성에서 호스트 하는 hello 끝점입니다.
> 또한 사항에 유의 하십시오, hello 다이어그램에서는 다양 한 끝점, API 관리 서비스에 대 한 IP 주소를 보여 줍니다. 하더라도 **만** 해당 구성 된 호스트 이름에 대해 응답 합니다.

> [!IMPORTANT]
> Azure API 관리 인스턴스 tooa 리소스 관리자 VNET을 배포할 때는 hello 서비스 Azure API 관리 인스턴스를 제외 하 고 다른 리소스가 없는 포함 하는 전용된 서브넷에 있어야 합니다. Toodeploy 하려고 시도 하는 경우 Azure API 관리 인스턴스 tooa 다른 리소스, hello 배포를 포함 하는 리소스 관리자 VNET 서브넷 실패 합니다.
>
>

![VPN 선택][api-management-setup-vpn-select]

클릭 **저장** hello hello 화면 위쪽에 있습니다.

> [!NOTE]
> hello hello API 관리 인스턴스 VIP 주소는 VNET 사용 하거나 사용 하지 않도록 설정 될 때마다를 변경 됩니다.  
> API 관리에서 이동 하면 hello VIP 주소를 바뀌고 **외부** 너무**내부** 또는 그 반대
>


> [!IMPORTANT]
> VNET에서 API 관리를 제거 하거나 하나에 배포 된 hello를 변경할 경우 too4 시간 이전에 사용한 VNET 남아 있을 수 있는 hello에 대 한 잠깁니다. 이 기간 동안 것은 가능한 toodelete hello VNET 또는 수 새 리소스 tooit 배포.

## <a name="enable-vnet-powershell"> </a>PowerShell cmdlet을 사용하여 VNET 연결 사용
Hello PowerShell cmdlet을 사용 하 여 VNET 연결을 설정할 수도 있습니다.

* **VNET 내 API 관리 서비스 만들기**: hello cmdlet을 사용 하 여 [새로 AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate VNET 내에 Azure API 관리 서비스입니다.

* **VNET 내 기존 API 관리 서비스를 배포**: hello cmdlet을 사용 하 여 [업데이트 AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove 가상 네트워크 내 기존 Azure API 관리 서비스입니다.

## <a name="connect-vnet"></a>가상 네트워크 내에서 호스팅되는 tooa 웹 서비스 연결
API 관리 서비스에 연결 된 VNET toohello 되 면 그 안에 백 엔드 서비스에 액세스 하는 공용 서비스에 액세스 차이가 없습니다. Hello에 hello 로컬 IP 주소 또는 hello의 호스트 이름 (DNS 서버 hello VNET에 대 한 구성 됨) 하는 경우 웹 서비스에만 입력 **웹 서비스 URL** 새로운 API를 만들 때 필드 하거나 기존 구성을 편집 합니다.

![VPN에서 API 추가][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"> </a>일반적인 네트워크 구성 문제
다음은 가상 네트워크로 API Management 서비스를 배포하는 동안 발생할 수 있는 일반적인 구성 오류의 목록입니다.

* **사용자 지정 DNS 서버 설치**: hello API 관리 서비스는 여러 Azure 서비스에 따라 달라 집니다. API 관리는 사용자 지정 DNS 서버를 통해 VNET에서 호스트 되는 경우에 Azure 서비스의 tooresolve hello 호스트 이름이 필요 합니다. 사용자 지정 DNS 설정에 대한 [이](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 지침을 따르세요. 아래 hello 포트 테이블 및 참조에 대 한 기타 네트워크 요구 사항을 참조 하십시오.

> [!IMPORTANT]
> VNET hello에 대 한 사용자 지정 DNS 서버를 사용 하는 경우 설정 하는 것이 좋습니다. **전에** API 관리 서비스를 배포 합니다. 그렇지 않으면 하면 필요한 너무 hello API 관리 서비스 (s) hello DNS 서버를 변경할 때마다 실행 하 여 업데이트 hello [네트워크 구성 연산 적용](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **API 관리에 필요한 포트**:를 사용 하 여 API 관리 배포 된 hello 서브넷으로 인바운드 및 아웃 바운드 트래픽을 제어할 수 [네트워크 보안 그룹][Network Security Group]합니다. 이러한 포트를 사용할 수 없는 경우 API Management가 정상적으로 작동하지 않고 액세스하지 못하게 될 수 있습니다. 이러한 포트가 하나 이상 차단되는 것은 VNET에서 API Management를 사용하는 경우 가장 일반적인 잘못된 구성 문제입니다.

API 관리 서비스 인스턴스는 VNET에서 호스트 되는 경우에 다음 표에 hello에 hello 포트 사용 됩니다.

| 소스/대상 포트 | 방향 | 전송 프로토콜 | 목적 | 원본 / 대상 | 액세스 유형 |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |인바운드 |TCP |클라이언트 통신 tooAPI 관리 |인터넷 / VIRTUAL_NETWORK |외부 |
| * / 3443 |인바운드 |TCP |Azure Portal 및 Powershell용 관리 끝점 |인터넷 / VIRTUAL_NETWORK |외부 및 내부 |
| * / 80, 443 |아웃바운드 |TCP |Azure 저장소 및 Azure Service Bus에 대한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| * / 1433 |아웃바운드 |TCP |Azure SQL에 대한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| * / 11000 - 11999 |아웃바운드 |TCP |Azure SQL V12에 대한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| * / 14000 - 14999 |아웃바운드 |TCP |Azure SQL V12에 대한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| * / 5671 |아웃바운드 |AMQP |로그 tooEvent 허브 정책 및 모니터링 에이전트에 대 한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| 6381 - 6383 / 6381 - 6383 |인바운드 및 아웃바운드 |UDP |Redis 캐시에 대한 종속성 |VIRTUAL_NETWORK / VIRTUAL_NETWORK |외부 및 내부 |-
| * / 445 |아웃바운드 |TCP |GIT의 Azure 파일 공유에 대한 종속성 |VIRTUAL_NETWORK / 인터넷 |외부 및 내부 |
| * / * | 인바운드 |TCP |Azure 인프라 부하 분산 장치 | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |외부 및 내부 |

* **SSL 기능**: tooenable SSL 인증서 체인 작성 및 유효성 검사 hello API 관리 서비스는 아웃 바운드 네트워크 연결 tooocsp.msocsp.com, mscrl.microsoft.com 및 crl.microsoft.com 필요 합니다. 관리 tooAPI 업로드 한 인증서 hello 전체 체인 toohello CA 루트를 포함 하는 경우에이 종속성 필요 하지 않습니다.

* **DNS 액세스**: DNS 서버와의 통신을 위해서는 53 포트에서 아웃바운드 액세스가 필요합니다. 사용자 지정 DNS 서버에 있는 경우 VPN 게이트웨이의 다른 쪽 끝 hello, DNS 서버 hello API 관리를 호스팅하는 hello 서브넷에서 연결할 수 있어야 합니다.

* **메트릭 및 상태 모니터링**: 아웃 바운드 네트워크 연결 tooAzure 모니터링 끝점을 다음 도메인 hello 아래 해결: global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net 합니다.

* **빠른 설치에 경로**: 일반적인 고객 구성 toodefine 자신의 기본 경로 (0.0.0.0/0) 아웃 바운드 인터넷 트래픽을 tooinstead 흐름 온-프레미스를 강제로 수행 됩니다. 이 트래픽 흐름 것을 중단 하지 Azure API 관리와의 연결을 hello 아웃 바운드 트래픽을 차단 된 온-프레미스, 되었거나 NAT tooan 인식할 수 없는 집합이 더 이상 작동 하지 다양 한 Azure 끝점 주소를 수신할 합니다. hello 솔루션은 toodefine 하나 이상의 사용자 정의 경로 ([UDRs][UDRs]) hello Azure API 관리를 포함 하는 hello 서브넷에 있습니다. UDR hello 기본 경로 대신 허용 되어야 하는 서브넷 별 경로 정의 합니다.
  가능 하면 같은 구성이 toouse hello를 좋습니다.
 * 0.0.0.0/0을 보급 하는 hello ExpressRoute 구성 하 고 기본적으로 강제 터널링 모든 아웃 바운드 트래픽을 온-프레미스 키를 누릅니다.
 * hello Azure API 관리를 포함 하는 hello 적용 UDR toohello 서브넷 0.0.0.0/0은 인터넷의 다음 홉 형식으로 정의 합니다.
 hello 결합 된 효과 이러한 단계는 hello 서브넷 수준은 UDR 우선 hello hello Azure API 관리에서에서 아웃 바운드 인터넷에 액세스 하는 데 ExpressRoute 강제 터널링 합니다.

>[!WARNING]  
>Azure API 관리 express 경로 구성은 지원 되지 않습니다는 **hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 경로 크로스-보급할 잘못**합니다. 구성된 공용 피어링이 있는 Express 경로 구성은 다양한 Microsoft Azure IP 주소 범위 집합에 대해 Microsoft에서 경로 보급을 받습니다. 이러한 주소 범위가 잘못 크로스-에 보급 hello 개인 피어 링 경로 hello 최종 결과 hello Azure API 관리 인스턴스 서브넷의 모든 아웃 바운드 네트워크 패킷이 됩니다 tooa 잘못 강제 터널링 된 고객의 온-프레미스 네트워크 인프라입니다. 이 네트워크 흐름은 Azure API Management를 중단합니다. hello 솔루션 toothis 문제는 hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 toostop 간 광고 경로입니다.


## <a name="troubleshooting"> </a>문제 해결
변경 내용을 tooyour 네트워크를 만들 때 참조 너무[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate hello API 관리 서비스를 손실 하지 않은 액세스 tooany hello의 중요 한 리소스에 따라 달라 지는 경우. hello 연결 상태는 15 분 마다 업데이트 되어야 합니다.

## <a name="limitations"> </a>제한 사항
* API 관리 인스턴스가 포함된 서브넷은 다른 Azure 리소스 종류를 포함할 수 없습니다.
* hello 서브넷 및 API 관리 서비스에 있어야 합니다. hello hello 동일한 구독 합니다.
* API 관리 인스턴스가 포함된 서브넷은 구독 간에 이동할 수 없습니다.
* Hello 범위에 명시 된 내부 IP 주소에서 사용할 수는 내부 가상 네트워크를 사용 하는 경우 [RFC 1918](https://tools.ietf.org/html/rfc1918), 공용 IP 주소를 제공할 수 없습니다.
* 를 구성 하는 내부 가상 네트워크와 다중 지역 API 관리 배포에 대 한 사용자가 자신의 부하 hello DNS을 소유 분산을 관리 합니다.


## <a name="related-content"> </a>관련 콘텐츠
* [Vpn 게이트웨이 사용 하 여 가상 네트워크 toobackend 연결](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [다양한 배포 모델에서 가상 네트워크 연결](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Azure API 관리에서 toouse hello API 검사기 tootrace 호출 하는 방법](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
