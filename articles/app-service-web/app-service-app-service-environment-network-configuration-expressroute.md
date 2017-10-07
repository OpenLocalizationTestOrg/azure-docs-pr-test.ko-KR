---
title: "Express 경로 사용 하기 위한 aaaNetwork 구성 세부 정보"
description: "가상 네트워크에서 앱 서비스 환경을 실행 하기 위한 네트워크 구성 세부 정보 tooan ExpressRoute 회로 연결 합니다."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>Express 경로를 사용하는 앱 서비스 환경에 대한 네트워크 구성 세부 정보
## <a name="overview"></a>개요
고객 연결할 수는 [Azure express 경로] [ ExpressRoute] 회로 tootheir 가상 네트워크 인프라를 해당 온-프레미스 네트워크 tooAzure 기능을 확장할 합니다.  App Service Environment는 이 [가상 네트워크][virtualnetwork] 인프라의 서브넷에서 만들 수 있습니다.  그런 다음 hello 앱 서비스 환경에서 실행 되는 앱 hello ExpressRoute 연결을 통해서만 액세스할 수 있는 보안 연결 tooback 최종 리소스를 설정할 수 있습니다.  

App Service Environment를 Azure Resource Manager 가상 네트워크에서 **만들 수도 있고** 클래식 배포 모델 가상 네트워크에서 **만들 수도 있습니다**.  최근인 2016년 6월의 변경 내용에 따르면 이제 공용 주소 범위 또는 RFC1918 주소 공간(즉, 개인 주소) 중 하나를 사용하는 가상 네트워크에 ASE를 배포할 수도 있습니다. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>필요한 네트워크 연결
앱 서비스 환경에 연결 된 가상 네트워크 tooan ExpressRoute 처음 충족 하지 않을 수 있습니다에 대 한 네트워크 연결 요구 사항이 있습니다.  앱 서비스 환경을 순서 toofunction에서 hello 다음의 모든 제대로 필요:

* 아웃 바운드 네트워크 연결 tooAzure 저장소 끝점 전 세계 두 포트 80 및 443입니다.  여기에 hello에 있는 끝점으로 앱 서비스 환경 hello와 동일한 지역에 있는 저장소 끝점 **다른** Azure 지역입니다.  Azure 저장소 끝점 hello 다음 DNS 도메인에서 해결: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* 및 *file.core.windows.net*합니다.  
* 아웃 바운드 네트워크 연결 toohello 포트 445에서 Azure 파일 서비스
* Hello에 아웃 바운드 네트워크 연결 tooSql DB 끝점 있는 동일한 앱 서비스 환경 hello 지역의 합니다.  Sql DB 끝점 도메인 다음 hello 아래 해결: *database.windows.net*합니다.  이 액세스 tooports 11000 11999 및 14000 14999 1433을 열지 필요 합니다.  자세한 내용은 [이 문서에서 SQL 데이터베이스 V12 포트 사용](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md)을 참조하세요.
* 아웃 바운드 네트워크 연결 toohello Azure 관리 평면 끝점 (ASM 및 ARM 모두 끝점).  여기에 아웃 바운드 연결 tooboth *management.core.windows.net* 및 *management.azure.com*합니다. 
* 아웃 바운드 네트워크 연결이 너무*ocsp.msocsp.com*, *mscrl.microsoft.com* 및 *crl.microsoft.com*합니다.  이것이 필요한 toosupport SSL 기능입니다.
* hello 가상 네트워크에 대 한 DNS 구성을 hello 모든 hello 끝점 확인 가능한 수 있어야 하며 도메인에 언급 된 hello 이전 포인트입니다.  이러한 끝점을 해결할 수 없으면 앱 서비스 환경 만들기 시도는 실패하고 기존 앱 서비스 환경도 비정상으로 표시됩니다.
* DNS 서버와의 통신을 위해서는 포트 53에서 아웃바운드 액세스가 필요합니다.
* 사용자 지정 DNS 서버에 있는 경우 VPN 게이트웨이의 다른 쪽 끝 hello, DNS 서버 hello hello 앱 서비스 환경을 포함 하는 hello 서브넷에서 연결할 수 있어야 합니다. 
* hello 아웃 바운드 네트워크 경로 내부 회사 프록시를 통과할 수 없습니다도 강제 터널링 tooon 온-프레미스 방식일 수 없습니다.  이렇게 하면 변경 내용이 hello hello 앱 서비스 환경에서에서 아웃 바운드 네트워크 트래픽의 효과적인 NAT 주소입니다.  앱 서비스 환경의 아웃 바운드 네트워크 트래픽의 hello NAT 주소를 변경 하면 위에 나열 된 오류 toomany hello 끝점 연결 합니다.  실패한 앱 서비스 환경 만들기 시도라는 결과로 나타날 뿐만 아니라 이전의 정상 앱 서비스 환경도 비정상으로 표시됩니다.  
* 이에 설명 된 대로 앱 서비스 환경을 허용 해야 네트워크 액세스 toorequired 포트를 인바운드 [문서][requiredports]합니다.

유효한 DNS 인프라를 구성 하 고 hello 가상 네트워크에 대 한 유지 관리 되도록 하 여 hello DNS 요구 사항은 충족할 수 있습니다.  모든 이유 hello에 대 한 앱 서비스 환경을 만든 후에 DNS 구성이 변경 되 면 개발자는 앱 서비스 환경 toopick hello 새 DNS 구성을 강제로 수 있습니다.  Hello hello에 hello 앱 서비스 환경 관리 블레이드 위쪽에 hello "다시 시작" 아이콘을 사용 하 여 롤링 환경 재부팅 트리거 [Azure 포털] [ NewPortal] hello 환경 toopick 하면 DNS 구성을 새는 hello 합니다.

hello 인바운드 네트워크 액세스 요구 사항을 충족할 수 있습니다를 구성 하 여 한 [네트워크 보안 그룹] [ NetworkSecurityGroups] 이 에설명된대로hello앱서비스환경서브넷tooallowhello필요한액세스[문서][requiredports]합니다.

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>앱 서비스 환경에 대한 아웃바운드 네트워크 연결을 사용하도록 설정
기본적으로, 새로 생성된 Express Route 회로는 아웃바운드 인터넷 연결을 허용하는 기본 경로를 알립니다.  앱 서비스 환경에서이 구성을 사용 하 여 수 tooconnect tooother Azure 끝점이 됩니다.

일반적인 사용자 구성을 toodefine은 아웃 바운드 인터넷 트래픽을 tooinstead 흐름을 강제로 수행 하는 자신의 기본 경로 (0.0.0.0/0) 온-프레미스입니다.  이 트래픽 흐름 것을 중단 하지 앱 서비스 환경 hello 아웃 바운드 트래픽을 차단 된 온-프레미스, 되었거나 NAT tooan 인식할 수 없는 집합이 더 이상 작동 하지 다양 한 Azure 끝점 주소를 수신할 합니다.

hello 솔루션은 앱 서비스 환경 hello이 포함 된 hello 서브넷에서 toodefine 하나 이상의 사용자 정의 경로 (UDRs)입니다.  UDR hello 기본 경로 대신 허용 되어야 하는 서브넷 별 경로 정의 합니다.

가능 하면 같은 구성이 toouse hello를 좋습니다.

* 0.0.0.0/0을 보급 하는 hello ExpressRoute 구성 하 고 기본적으로 강제 터널링 모든 아웃 바운드 트래픽을 온-프레미스 키를 누릅니다.
* hello 앱 서비스 환경에 포함 된 hello 적용 UDR toohello 서브넷 0.0.0.0/0 (이 예는이 문서의 맨 아래로)는 인터넷의 다음 홉 형식으로 정의 합니다.

hello 결합 된 효과 이러한 단계는 hello 서브넷 수준 UDR 우선 hello ExpressRoute 강제 터널링, hello 앱 서비스 환경에서에서 아웃 바운드 인터넷에 액세스할 수 있도록 합니다.

> [!IMPORTANT]
> UDR에 정의 된 경로 hello **해야** 수 있을 만큼 구체적 너무 ExpressRoute 구성 hello에서 보급 모든 경로 보다 우선 합니다.  아래 예제에서는 hello hello 광범위 한 0.0.0.0/0 주소 범위를 사용 하 여 있으며 따라서 경로 알림이 더 구체적인 주소 범위를 사용 하 여 실수로 재정의할 잠재적으로 수 있습니다.
> 
> 앱 서비스 환경 ExpressRoute 구성이 지원 되지 않습니다는 **간 알릴 안녕 공용 피어 링 경로 toohello 개인 피어 링 경로에서 경로**합니다.  구성된 공용 피어링이 있는 Express 경로 구성은 다양한 Microsoft Azure IP 주소 범위 집합에 대해 Microsoft에서 경로 보급을 받습니다.  이 주소 범위 hello 개인 피어 링 경로에 크로스 보급을 hello 최종 결과 hello 앱 서비스 환경 서브넷의 모든 아웃 바운드 네트워크 패킷이 tooa 강제 터널링 된 고객의 온-프레미스 네트워크 인프라 된다는 것입니다.  이 네트워크 흐름은 현재 App Service Environment에서 지원되지 않습니다.  하나의 솔루션 toothis 문제는 hello 공용 피어 링 경로 toohello 개인 피어 링 경로에서 toostop 간 광고 경로입니다.
> 
> 

사용자 정의 경로에 대한 배경 정보는 [개요][UDROverview]를 참조하세요.  

작성 및 사용자 정의 경로 구성에 대 한 세부 정보는이 사용할 수 있는 [어떻게 tooGuide][UDRHowTo]합니다.

## <a name="example-udr-configuration-for-an-app-service-environment"></a>앱 서비스 환경에 대한 UDR 구성 예
**필수 구성 요소**

1. Hello에서 Azure Powershell 설치 [Azure 다운로드 페이지] [ AzureDownloads] (2015 이상이 년 6 월에 발표).  "명령줄 도구" hello 최신 Powershell cmdlet을 설치 하는 "Windows Powershell"에서 "설치" 링크는 있습니다.
2. 앱 서비스 환경에 의해 배타적 사용으로 만들어진 고유한 서브넷을 권장합니다.  이렇게 하면 해당 hello 적용 UDRs toohello 서브넷은 hello 앱 서비스 환경에 대 한 아웃 바운드 트래픽을 엽니다.
3. **중요 한**: 배포 하지 않는 앱 서비스 환경까지 hello **후** hello 다음 구성 단계를 수행 합니다.  이렇게 하면 앱 서비스 환경 toodeploy 시도 하기 전에 아웃 바운드 네트워크 연결을 사용할 수 있습니다.

**1 단계: 명명된 경로 테이블 만들기**

hello 다음 코드 조각 경로 이라는 테이블을 만들어 "DirectInternetRouteTable" hello 서쪽 미국 Azure 지역에서:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**2 단계: hello 경로 테이블에 하나 이상의 경로 만들기**

Tooadd 하나 필요 합니다 또는 순서 tooenable 아웃 바운드 인터넷 액세스에 더 많은 경로 toohello 경로 테이블입니다.  

hello 아웃 바운드 액세스 toohello 인터넷은 toodefine 아래 그림과 같이 0.0.0.0/0에 대 한 경로 구성 하기 위한 방법을 권장 합니다.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

해당 0.0.0.0/0은 광범위 한 주소 범위 및 따라서 hello ExpressRoute에서 보급 하는 보다 구체적인 주소 범위를 기준으로 재정의 될 수는 것이 중요 합니다.  toore-hello 반복 0.0.0.0/0은 경로와 UDR 이전 권장 구성만도 0.0.0.0/0을 알리는 ExressRoute 구성와 함께에서 사용 해야 합니다. 

대신 Azure에서 사용하는 CIDR 범위의 포괄적이고 업데이트된 목록을 다운로드할 수 있습니다.  hello 모든 hello Azure IP 주소 범위를 포함 하는 Xml 파일은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터][DownloadCenterAddressRanges]합니다.  

이러한 범위는 시간이 지나도 변경, toohello 수동는 정기적으로 업데이트 하기 때문 하며 사용자 정의 경로 tookeep 동기화 하지만 note 합니다.  또한 위 기본값 이므로 단일 UDR에 100 경로의 있습니다 필요한 너무 "요약" hello Azure IP 주소 제한을 toofit hello 100 경로 제한 내에서 범위를 해당 UDR 염두에서에 두고 정의 된 경로에서 알릴 안녕 경로 보다 구체적인 toobe 필요 하면 Express 경로입니다.  

**3 단계: hello 경로 테이블 toohello 서브넷 포함 hello 앱 서비스 환경에 연결**

hello 마지막 구성 단계는 tooassociate hello 경로 테이블 toohello 서브넷 hello 앱 서비스 환경 배포 될 위치입니다.  hello 다음 명령이 연결 결국 앱 서비스 환경에 들어갈 "ASESubnet" hello "DirectInternetRouteTable" toohello 합니다.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**4단계: 최종 단계**

Hello 경로 테이블에 바인딩된 toohello 서브넷이 되 면 toofirst 테스트 좋습니다 하 고 hello 의도 효과 확인 합니다.  예를 들어 hello 서브넷에 가상 컴퓨터를 배포 하 고 있는지 확인:

* 아웃 바운드 트래픽 tooboth Azure 및 비 Azure 끝점 언급에서 이전에이 문서는 **하지** hello ExpressRoute 회로 아래로 이동 합니다.  이 반드시 tooverify hello 서브넷에서 아웃 바운드 트래픽이 되는 경우 강제 여전히 온-프레미스, 앱 서비스 환경을 만들 터널링 된 이후이 문제는 항상 실패 합니다. 
* Hello 끝점에 대 한 DNS 조회가 앞에서 언급 한는 모두 적절 하 게 확인 합니다. 

Hello 단계는 확인 되 면 hello 서브넷 toobe "empty" hello 시간 hello 앱 서비스 환경을 만들 때 필요 하므로 toodelete hello 가상 컴퓨터가 필요 합니다.

그런 다음 앱 서비스 환경을 계속 만듭니다!

## <a name="getting-started"></a>시작
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경 시작 tooget 참조 [소개 tooApp 서비스 환경][IntroToAppServiceEnvironment]

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
