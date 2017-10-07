---
title: "aaaSecurely 연결 tooBackEnd 앱 서비스 환경에서 리소스"
description: "Toosecurely 앱 서비스 환경에서 toobackend 리소스를 연결 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a>연결 tooBackend 앱 서비스 환경에서 리소스를 안전 하 게
## <a name="overview"></a>개요
앱 서비스 환경에 항상 만들어집니다 이후 **어느** 은 Azure 리소스 관리자 가상 네트워크를 **또는** 클래식 배포 모델 [가상 네트워크] [ virtualnetwork], 앱 서비스 환경 tooother 백엔드 리소스의 아웃 바운드 연결 hello 가상 네트워크를 통해 배타적으로 전달 될 수 있습니다.  최근인 2016년 6월의 변경 내용에 따르면 이제 공용 주소 범위 또는 RFC1918 주소 공간(즉, 개인 주소) 중 하나를 사용하는 가상 네트워크에 ASE를 배포할 수도 있습니다.  

예를 들어 잠긴 포트 1433을 통해 가상 컴퓨터의 클러스터에서 실행되는 SQL Server가 있을 수 있습니다.  hello 끝점에 다른 리소스의 액세스를 허용 하는 tooonly ACLd 수 hello 동일한 가상 네트워크입니다.  

또 다른 예로, 중요 한 끝점 실행 온-프레미스 하 고 하나를 사용 하는 연결 된 tooAzure 수 [사이트 간] [ SiteToSite] 또는 [Azure express 경로] [ ExpressRoute] 연결 합니다.  결과적으로, 가상 네트워크에만 리소스 toohello 사이트 간 연결 또는 express 경로 터널 수 tooaccess 온-프레미스 끝점이 됩니다.

모든이 시나리오에 대 한 앱 서비스 환경에서 실행 되는 앱은 될 수 toosecurely 연결 toohello 다양 한 서버 및 리소스 합니다.  아웃 바운드 트래픽을 hello에는 앱 서비스 환경 tooprivate 끝점에서 실행 중인 앱에서 동일한 가상 네트워크 (toohello 연결 또는 동일한 가상 네트워크), 흐름만 hello 가상 네트워크를 통해 됩니다.  공용 인터넷 hello 하는 아웃 바운드 트래픽을 tooprivate 끝점을 통해 이동 하지 것입니다.

한 가지 주의할 점은 앱 서비스 환경 tooendpoints 가상 네트워크 내에서 toooutbound 트래픽에 적용 됩니다.  앱 서비스 환경 hello에 있는 가상 컴퓨터의 끝점에 도달할 수 없는 **동일한** hello 앱 서비스 환경으로 서브넷입니다.  이 정상적으로 아니어야 문제가으로 앱 서비스 환경 hello 앱 서비스 환경에서 배타적으로 사용 하도록 예약 된 서브넷에 배포 됩니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a>아웃 바운드 연결 및 DNS 요구 사항
앱 서비스 환경 toofunction 제대로 필요한 아웃 바운드 액세스 toovarious 끝점입니다. ASE에서 사용 하는 hello 외부 끝점의 전체 목록은 "필요한 네트워크 연결" 섹션의 hello hello 중인 [ExpressRoute에 대 한 네트워크 구성을](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) 문서.

앱 서비스 환경 hello 가상 네트워크에 구성 된 유효한 DNS 인프라가 필요 합니다.  모든 이유 hello에 대 한 앱 서비스 환경을 만든 후에 DNS 구성이 변경 되 면 개발자는 앱 서비스 환경 toopick hello 새 DNS 구성을 강제로 수 있습니다.  앱 서비스 환경 hello hello 위쪽에 있는 hello "다시 시작" 아이콘을 사용 하 여 롤링 환경 재부팅을 트리거하는 hello 포털에서 관리 블레이드 hello 환경 toopick hello 새 DNS 구성을 발생 합니다.

또한 모든 사용자 지정 DNS 서버 hello vnet에 시간 이전 toocreating 앱 서비스 환경 미리 설치 된다는 것이 좋습니다.  앱 서비스 환경을 만드는 동안 가상 네트워크의 DNS 구성이 변경 되 면 hello 앱 서비스 환경 만들기 프로세스 실패 발생 하 합니다.  비슷한에서 사용자 지정 DNS 서버 hello에 있는 경우 VPN 게이트웨이 및 DNS 서버 hello의 다른 쪽 끝은 연결할 수 없거나 사용할 수 없거나, hello 앱 서비스 환경 만들기 프로세스가 실패 합니다.

## <a name="connecting-tooa-sql-server"></a>SQL Server tooa 연결
일반적인 SQL Server 구성에는 포트 1433에서 수신 대기하는 끝점이 있습니다.

![SQL Server 끝점][SqlServerEndpoint]

트래픽 toothis 끝점을 제한 하는 방법은 두 가지가 있습니다.

* [네트워크 액세스 제어 목록][NetworkAccessControlLists](네트워크 ACL)
* [네트워크 보안 그룹][NetworkSecurityGroups]

## <a name="restricting-access-with-a-network-acl"></a>네트워크 ACL을 사용하여 액세스 제한
네트워크 액세스 제어 목록을 사용하여 포트 1433의 보안을 유지할 수 있습니다.  허용 목록 클라이언트 아래 hello 예제에서는 가상 네트워크 내에서 시작 및 블록 tooall 다른 클라이언트에 액세스 합니다.

![네트워크 액세스 제어 목록 예][NetworkAccessControlListExample]

앱 서비스 환경에서 실행 중인 모든 응용 프로그램으로 SQL Server hello hello를 사용 하 여 수 tooconnect toohello SQL Server 인스턴스에 동일한 가상 네트워크 hello **내부 VNet** hello SQL Server 가상 컴퓨터에 대 한 IP 주소입니다.  

hello 참조 아래 연결 문자열의 예에는 해당 개인 IP 주소를 사용 하 여 SQL Server hello 합니다.

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

Hello 가상 컴퓨터에 공용 끝점으로 연결 시도 hello 공용 IP 주소를 사용 하 여 hello 네트워크 ACL 때문에 거부 됩니다. 

## <a name="restricting-access-with-a-network-security-group"></a>네트워크 보안 그룹을 사용하여 액세스 제한
액세스를 보호하는 또 다른 방법은 네트워크 보안 그룹을 사용하는 것입니다.  네트워크 보안 그룹에는 적용 된 tooindividual 가상 컴퓨터 또는 가상 컴퓨터를 포함 하는 tooa 서브넷 수 있습니다.

먼저 네트워크 보안 그룹에는 만든 toobe 항목이 필요 합니다.

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

액세스 tooonly VNet 내부 트래픽을 제한 하는 것은 네트워크 보안 그룹과 매우 간단 합니다.  네트워크 보안 그룹의 hello 기본 규칙에서 다른 네트워크 클라이언트 hello에 대 한 액세스만 허용 동일한 가상 네트워크입니다.

결과적으로 잠그는 기능이 액세스 tooSQL 서버가 하기만 하면 해당 기본 규칙 tooeither hello 가상 컴퓨터와 SQL Server 또는 hello 서브넷 hello 가상 컴퓨터가 포함 된 실행 네트워크 보안 그룹을 적용 합니다.

아래 hello 샘플 네트워크 보안 그룹 toohello 포함 된 서브넷이 적용 됩니다.

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

hello 최종 결과 VNet 내부 액세스를 허용 하면서 외부 액세스를 차단 하는 보안 규칙의 집합:

![기본 네트워크 보안 규칙][DefaultNetworkSecurityRules]

## <a name="getting-started"></a>시작
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경][IntroToAppServiceEnvironment]

제어 하는 인바운드 트래픽 tooyour 앱 서비스 환경 자세한 내용은 참조 하세요. [인바운드 트래픽을 tooan 앱 서비스 환경 제어][ControlInboundASE]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
