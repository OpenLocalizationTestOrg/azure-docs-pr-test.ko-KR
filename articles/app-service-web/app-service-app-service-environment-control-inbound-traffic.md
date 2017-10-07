---
title: "aaaHow tooControl 인바운드 트래픽 tooan 앱 서비스 환경"
description: "어떻게 tooconfigure 네트워크 보안 규칙 toocontrol 인바운드 트래픽을 tooan 앱 서비스 환경에 알아봅니다."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>어떻게 tooControl 인바운드 트래픽 tooan 앱 서비스 환경
## <a name="overview"></a>개요
App Service Environment를 Azure Resource Manager 가상 네트워크에서 **만들 수도 있고** 클래식 배포 모델 [가상 네트워크][virtualnetwork]에서 **만들 수도 있습니다**.  앱 서비스 환경을 만드는 hello 시 새 가상 네트워크와 새 서브넷을 정의할 수 있습니다.  또는 기존 가상 네트워크 및 기존 서브넷에 앱 서비스 환경을 만들 수 있습니다.  2016년 6월에 적용된 변경 내용에 따르면 공용 주소 범위 또는 RFC1918 주소 공간(즉, 개인 주소) 중 하나를 사용하는 가상 네트워크에 ASE를 배포할 수도 있습니다.  앱 서비스 환경을 만드는 방법에 대 한 자세한 내용은 참조 [어떻게 tooCreate 앱 서비스 환경][HowToCreateAnAppServiceEnvironment]합니다.

앱 서비스 환경 항상 만들어야 할 한 서브넷 내에서 서브넷은 HTTP 및 HTTPS 트래픽을 구체적인 정보부터 사용할 수 있도록 사용 되는 toolock 업스트림 장치 및 서비스의 데이터로 인바운드 트래픽 다운 될 수 있는 네트워크 경계를 제공 하기 때문에 업스트림 IP 주소입니다.

서브넷의 인바운드 및 아웃바운드 네트워크 트래픽은 [네트워크 보안 그룹][NetworkSecurityGroups]을 사용하여 제어합니다. 네트워크 보안 그룹에 네트워크 보안 규칙을 만들고 hello 네트워크 보안 그룹 hello 서브넷 포함 hello 앱 서비스 환경에 할당 한 다음 필요 인바운드 트래픽을 제어 합니다.

네트워크 보안 그룹은 tooa 서브넷 할당 되 면 앱 서비스 환경이입니다 허용/차단 hello에 따라 hello에 tooapps 인바운드 트래픽 허용 하 고 hello 네트워크 보안 그룹에 정의 된 규칙을 거부 합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>App Service 환경에서 사용하는 인바운드 네트워크 포트
네트워크 보안 그룹과 인바운드 네트워크 트래픽을 잠그는 하기 전에 것은 중요 한 tooknow hello 집합 앱 서비스 환경에서 사용 하는 필수 및 선택적 네트워크 포트입니다.  실수로 트래픽이 toosome 포트 오프 닫는 앱 서비스 환경에서 기능 손실 될 수 있습니다.

hello 다음은 앱 서비스 환경에서 사용 하는 포트 목록입니다. 명확하게 언급이 없는 한 모든 포트는 **TCP**입니다.

* 454: Azure 인프라에서 SSL을 통해 App Service 환경을 관리 및 유지 보수하는 데 사용되는 **필수 포트** 입니다.  트래픽 toothis 포트를 차단 하지 않습니다.  이 포트는 항상 ASE의 바인딩된 toohello 공용 VIP입니다.
* 455: Azure 인프라에서 SSL을 통해 App Service 환경을 관리 및 유지 보수하는 데 사용되는 **필수 포트** 입니다.  트래픽 toothis 포트를 차단 하지 않습니다.  이 포트는 항상 ASE의 바인딩된 toohello 공용 VIP입니다.
* 80: 기본에 대 한 인바운드 HTTP 트래픽 tooapps 앱 서비스 환경에 앱 서비스 계획에서 실행 되는 포트입니다.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ILB 주소 hello ASE입니다.
* 443: 기본에 대 한 인바운드 SSL 트래픽 tooapps 앱 서비스 환경에 앱 서비스 계획에서 실행 되는 포트입니다.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ILB 주소 hello ASE입니다.
* 21: FTP에 대한 컨트롤 채널입니다.  FTP를 사용하지 않는 경우 이 포트를 안전하게 차단할 수 있습니다.  이 포트는 ILB 사용이 가능한 ASE ASE에 대 한 바운드 toohello ILB 주소 수 있습니다.
* 990: FTPS에 대한 컨트롤 채널입니다.  FTPS를 사용하지 않는 경우 이 포트를 안전하게 차단할 수 있습니다.  이 포트는 ILB 사용이 가능한 ASE ASE에 대 한 바운드 toohello ILB 주소 수 있습니다.
* 10001~10020: FTP에 대한 데이터 채널입니다.  으로 hello 컨트롤 채널에서 이러한 포트 차단 될 수 안전 하 게 FTP를 사용 하는 경우.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ASE의 ILB 주소일 수 있습니다.
* 4016: Visual Studio 2012를 통한 원격 디버깅에 사용됩니다.  Hello 기능은 사용 되지 않는 경우이 포트 안전 하 게 차단 될 수 있습니다.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ILB 주소 hello ASE입니다.
* 4018: Visual Studio 2013을 통한 원격 디버깅에 사용됩니다.  Hello 기능은 사용 되지 않는 경우이 포트 안전 하 게 차단 될 수 있습니다.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ILB 주소 hello ASE입니다.
* 4020: Visual Studio 2015를 통한 원격 디버깅에 사용됩니다.  Hello 기능은 사용 되지 않는 경우이 포트 안전 하 게 차단 될 수 있습니다.  ILB 사용이 가능한 ASE에이 포트는 바인딩된 toohello ILB 주소 hello ASE입니다.

## <a name="outbound-connectivity-and-dns-requirements"></a>아웃 바운드 연결 및 DNS 요구 사항
앱 서비스 환경 toofunction에 대 한 제대로 것도 아웃 바운드 액세스 toovarious 끝점이 필요합니다. ASE에서 사용 하는 hello 외부 끝점의 전체 목록은 "필요한 네트워크 연결" 섹션의 hello hello 중인 [ExpressRoute에 대 한 네트워크 구성을](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) 문서.

앱 서비스 환경 hello 가상 네트워크에 구성 된 유효한 DNS 인프라가 필요 합니다.  모든 이유 hello에 대 한 앱 서비스 환경을 만든 후에 DNS 구성이 변경 되 면 개발자는 앱 서비스 환경 toopick hello 새 DNS 구성을 강제로 수 있습니다.  Hello hello에 hello 앱 서비스 환경 관리 블레이드 위쪽에 hello "다시 시작" 아이콘을 사용 하 여 롤링 환경 재부팅 트리거 [Azure 포털] [ NewPortal] hello 환경 toopick 하면 DNS 구성을 새는 hello 합니다.

또한 모든 사용자 지정 DNS 서버 hello vnet에 시간 이전 toocreating 앱 서비스 환경 미리 설치 된다는 것이 좋습니다.  앱 서비스 환경을 만드는 동안 가상 네트워크의 DNS 구성이 변경 되 면 hello 앱 서비스 환경 만들기 프로세스 실패 발생 하 합니다.  비슷한에서 사용자 지정 DNS 서버 hello에 있는 경우 VPN 게이트웨이 및 DNS 서버 hello의 다른 쪽 끝은 연결할 수 없거나 사용할 수 없거나, hello 앱 서비스 환경 만들기 프로세스가 실패 합니다.

## <a name="creating-a-network-security-group"></a>네트워크 보안 그룹 만들기
전체 네트워크 보안 그룹의 작동 방법을 참조 hello 다음 [정보][NetworkSecurityGroups]합니다.  네트워크 보안 그룹 구성 및 적용 한 앱 서비스 환경에 포함 된 네트워크 보안 그룹 tooa 서브넷에 중점을 둔의 hello Azure 서비스 관리 예제에서 터치 아래 강조 표시 합니다.

**참고:** 그래픽으로 hello를 사용 하 여 네트워크 보안 그룹을 구성할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 Azure PowerShell을 통해.

네트워크 보안 그룹은 먼저 구독과 연결된 독립 실행형 엔터티로 만들어집니다. 네트워크 보안 그룹은 Azure 지역에서 만들어지므로 해당 hello 네트워크 보안 그룹에에서 만들어져 있는지 확인 hello 동일한 앱 서비스 환경 hello 지역의 합니다.

hello 다음 네트워크 보안 그룹을 만들어 하는 방법을 보여 줍니다.

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

네트워크 보안 그룹을 만든 후 하나 이상의 네트워크 보안 규칙 tooit을 추가 됩니다.  규칙 집합이 hello 시간이 지남에 따라 변경 될 수 있습니다, 때문 번호 매기기 체계 hello 아웃 toospace 규칙 우선 순위 toomake에 대 한 것 쉽게 tooinsert 추가 규칙 시간이 지남에 따라 사용 하는 것이 좋습니다.

다음 예제에서는 hello 명시적으로 액세스 toohello 관리 포트 hello Azure 인프라 toomanage에 필요한 권한을 부여 하 고 앱 서비스 환경 유지 관리 하는 규칙을 보여 줍니다.  이때 모든 관리 트래픽 흐름 SSL을 통해 지정 하 고 Azure 관리 인프라 이외의 모든 엔터티에 의해 액세스할 수 없는 hello 포트가 열려 있는 경우에 있으므로 클라이언트 인증서에 의해 보안 됩니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


잠그는 경우 80 및 443 액세스 tooport 너무 "숨기기" 업스트림 장치 또는 서비스 뒤에 있는 앱 서비스 환경, tooknow hello 업스트림 IP 주소가 필요 합니다.  예를 들어 웹 응용 프로그램 방화벽 (WAF)를 사용 하는 hello WAF 경우에 자체 IP 주소 (또는 주소) 하는 데 사용 될 때 프록시 트래픽 tooa 다운스트림 앱 서비스 환경입니다.  Toouse hello에이 IP 주소가 필요 *SourceAddressPrefix* 네트워크 보안 규칙의 매개 변수입니다.

아래 hello 예제에서 업스트림 특정 IP 주소에서 인바운드 트래픽은 명시적으로 허용 됩니다.  주소 hello *1.2.3.4* 업스트림 WAF의 hello IP 주소에 대 한 자리 표시자로 사용 됩니다.  업스트림 장치 또는 서비스에서 사용 하는 hello 값 toomatch hello 주소를 변경 합니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

FTP 지원 기능을 사용할 경우 서식 파일 toogrant 액세스 toohello FTP 제어 포트 및 데이터 채널 포트 규칙에 따라 hello는 사용할 수 있습니다.  FTP 상태 저장 프로토콜 이기 때문에 기존의 HTTP/HTTPS 방화벽 또는 프록시 장치를 통해 트래픽을 수 tooroute FTP 설치할 수 없습니다.  이 경우 해야 tooset hello *SourceAddressPrefix* tooa 다른 값-예를 들어 hello IP 주소는 FTP 클라이언트를 실행 하는 개발자 또는 배포 컴퓨터의 범위. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**참고:** hello 데이터 채널 포트 범위 hello 미리 보기 기간 동안 변경 될 수 있습니다.)

Visual Studio를 사용 하 여 원격 디버깅 사용 되는 경우 규칙에 따라 hello toogrant 액세스 하는 방법을 보여 줍니다.  버전마다 다른 포트를 원격 디버깅에 사용하기 때문에 지원되는 각 버전의 Visual Studio에 대한 별도의 규칙이 있습니다.  FTP 액세스와 마찬가지로 원격 디버깅 트래픽은 기존 WAF 또는 프록시 장치를 통해 제대로 흐르지 않을 수 있습니다.  hello *SourceAddressPrefix* 대신 Visual Studio를 실행 하는 개발자 컴퓨터의 IP 주소 범위 toohello 설정할 수 있습니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>네트워크 보안 그룹 tooa 서브넷 할당
네트워크 보안 그룹에 대 한 액세스 tooall 외부 트래픽이 거부 하는 기본 보안 규칙을 있습니다.  위에서 설명한 hello 네트워크 보안 규칙 결합 결과 hello 및 인바운드 트래픽을 차단 하 고 기본 보안 규칙 hello, 소스 주소 범위에서 트래픽만 연관 되는 *허용* 작업 수 없게 됩니다. toosend 트래픽 tooapps 앱 서비스 환경에서 실행 합니다.

네트워크 보안 그룹 보안 규칙을 채운 다음 hello 앱 서비스 환경에 포함 된 할당 toobe toohello 서브넷이 필요 합니다.  hello 할당 명령에는 앱 서비스 환경 hello 만들어진 hello 서브넷의 hello 이름 뿐만 아니라 앱 서비스 환경 hello 있는 hello 가상 네트워크의 두 hello 이름을 참조 합니다.  

다음 예제에서는 hello tooa 서브넷과 가상 네트워크에 할당 되는 네트워크 보안 그룹을 보여 줍니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Hello 네트워크 보안 그룹 할당 성공 (hello 할당 장기 실행 작업을 몇 분 toocomplete 걸릴 수 있습니다)만 일치 하는 트래픽 인바운드 *허용* 규칙 hello 응용 프로그램에서에서 응용 프로그램을 성공적으로 도달 합니다 서비스 환경입니다.

다음 예제에서는 완결성 hello에 대 한 tooremove 및 dis-연결 hello 네트워크 보안 hello 서브넷에서 그룹화 하는 방법을 보여 줍니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>명시적 IP-SSL에 대한 특별 고려 사항
응용 프로그램에서는 명시적 IP SSL 주소로 구성 됩니다 (적용 가능한 *만* 공용 VIP는 tooASEs), HTTP 및 HTTPS 모두 트래픽 흐름 hello 서브넷에 앱 서비스 환경 hello의 hello 기본 IP 주소를 사용 하는 대신 다른 세트에 대 한 포트 80 및 443 이외의 포트입니다.

각 IP SSL 주소에서 사용 되는 포트의 개별 쌍 hello hello 앱 서비스 환경 세부 정보 UX 블레이드에서 hello 포털 사용자 인터페이스에서 찾을 수 있습니다.  "모든 설정" > "lP 주소"를 선택합니다.  "IP 주소" hello 블레이드 표시 되는 테이블의 hello 앱 서비스 환경에 대 한 모든 명시적으로 구성 된 IP SSL 주소 사용 되는 tooroute hello 특수 포트 쌍과 함께 HTTP 및 HTTPS 트래픽이 연결 된 각 IP SSL 주소입니다.  그는 필요한 toobe hello DestinationPortRange 매개 변수에 대 한 네트워크 보안 그룹에서 규칙을 구성할 때 사용 되는이 포트 쌍입니다.

IP SSL 구성된 toouse ASE에 앱을 사용 하는 경우 외부 고객 되지 표시 되 고 tooworry hello 특수 포트 쌍 매핑에 대 한 필요는 없습니다.  트래픽 toohello 앱 구성 toohello IP SSL 주소 정상적으로 흐릅니다.  hello 번역 toohello 특수 포트 쌍 자동으로 발생 하는 내부적으로 트래픽 라우팅의 최종 레그 hello 하는 동안 hello 서브넷 포함 hello ASE에 있습니다. 

## <a name="getting-started"></a>시작
앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경][IntroToAppServiceEnvironment]

모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경에서 toobackend 리소스를 안전 하 게 연결 하는 앱 주위 세부 정보를 참조 하십시오. [앱 서비스 환경에서 tooBackend 리소스를 안전 하 게 연결][SecurelyConnecttoBackend]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

