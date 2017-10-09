---
title: "aaaLayered 앱 서비스 환경을 사용 하 여 보안 아키텍처"
description: "앱 서비스 환경으로 계층화된 보안 아키텍처 구현"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a>앱 서비스 환경으로 계층화된 보안 아키텍처 구현
## <a name="overview"></a>개요
앱 서비스 환경이 가상 네트워크에 배포된 격리된 런타임 환경을 제공하므로 개발자는 실제 응용 프로그램 계층 각각에 서로 다른 수준으로 네트워크 액세스를 제공하는 계층화된 보안 아키텍처를 만들 수 있습니다.

일반적인 desire toohide API 백 엔드가 일반 인터넷 액세스 로부터 이며 Api toobe 업스트림 웹 응용 프로그램에 의해 호출을 허용 합니다.  [네트워크 보안 그룹 (Nsg)] [ NetworkSecurityGroups] 앱 서비스 환경 toorestrict 공용 액세스 tooAPI 응용 프로그램이 포함 된 서브넷에서 사용할 수 있습니다.

아래 hello 다이어그램와 앱 서비스 환경에 배포 된 WebAPI 기반 응용 프로그램 예제 아키텍처를 보여 줍니다.  세 가지 별도 앱 서비스 환경에 배포 된 세 개의 별도 웹 앱 인스턴스 확인 백 엔드 호출 toohello 동일한 WebAPI 앱.

![개념적 아키텍처][ConceptualArchitecture] 

hello 녹색 더하기 기호 나타냅니다 해당 hello "apiase"를 포함 하는 hello 서브넷에 네트워크 보안 그룹 인바운드의 호출을 허용 hello 업스트림 웹 응용 프로그램, 자신에 게 서도 호출 합니다.  하지만 동일한 네트워크 보안 그룹을 명시적으로 거부 하는 hello toogeneral에 액세스 트래픽을 hello 인터넷에서에서 인바운드 합니다. 

이 항목의 나머지 부분에서는 hello "apiase"를 포함 하는 hello 서브넷에 hello 단계 필요한 tooconfigure hello 네트워크 보안 그룹을 안내 합니다.

## <a name="determining-hello-network-behavior"></a>Hello 네트워크 동작 결정
순서 tooknow 네트워크 보안 규칙이 필요한 해야 toodetermine tooreach hello 앱 서비스 환경 포함 hello API 앱과 차단 될 어떤 클라이언트 네트워크 클라이언트 허용 됩니다.

이후 [네트워크 보안 그룹 (Nsg)] [ NetworkSecurityGroups] 적용된 toosubnets 되며 앱 서비스 환경에 배포 된 서브넷에 NSG에 포함 된 hello 규칙이 적용 너무**모든** 앱 서비스 환경에서 실행 되는 앱입니다.  보안 규칙 집합를 네트워크 보안 그룹에 적용 된 toohello 서브넷 "apiase" hello "apiase" hello 하 여 보호 될 앱 서비스 환경에서 실행 되는 모든 앱을 포함 하 되 면이 문서에 대 한 hello 샘플 아키텍처를 사용 하 여 동일 합니다. 

* **Hello 업스트림 호출자의 아웃 바운드 IP 주소 확인:** hello 업스트림 호출자의 hello IP 주소 또는 주소 란?  이러한 주소 toobe NSG hello에 대 한 액세스를 명시적으로 허용 해야 합니다.  앱 서비스 환경 간의 호출 "Internet" 호출 고려 하는 경우이 hello 세 업스트림 앱 서비스 환경 요구 toobe hello "apiase" 서브넷에 NSG hello에 대 한 액세스가 허용의 hello 아웃 바운드 IP 주소가 할당 tooeach를 의미 합니다.   앱 서비스 환경에서 실행 되는 앱 참조 hello에 대 한 hello 아웃 바운드 IP 주소를 결정 하는 대 한 자세한 내용은 [네트워크 아키텍처] [ NetworkArchitecture] 개요 문서.
* **Hello 백 엔드 API 앱 자체 toocall 필요 한가요?**  경우에 따라 간과 하 고 미묘한 지점은 hello 시나리오는 hello 백 엔드 응용 프로그램이 해야 toocall 자체입니다.  앱 서비스 환경에 있는 백 엔드 API 응용 프로그램 자체 toocall 경우,이 처리도 "Internet" 호출으로 합니다.  필요 hello 샘플 아키텍처의 hello "apiase" 앱 서비스 환경도 hello 아웃 바운드 IP 주소에서 액세스할 수 있도록 합니다.

## <a name="setting-up-hello-network-security-group"></a>네트워크 보안 그룹 hello 설정
hello 설정 되 면 아웃 바운드 IP 주소 알려진, hello 다음 단계는 tooconstruct 네트워크 보안 그룹입니다.  클래식 가상 네트워크뿐만 아니라 가상 네트워크를 기반으로 하는 두 Resource Manager에 네트워크 보안 그룹을 만들 수 있습니다.  hello 아래 예와 만들기 및 Powershell을 사용 하 여 클래식 가상 네트워크에 NSG를 구성 합니다.

Hello 샘플 아키텍처에 대 한 빈 NSG 되어 해당 지역에서 만들어 hello 환경 남 중앙 미국에 있습니다.

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

먼저 명시적 허용 hello Azure 관리 인프라에는 hello 문서에서 설명한 대로 대 한 규칙은 추가 [트래픽 인바운드] [ InboundTraffic] 앱 서비스 환경에 대 한 합니다.

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

다음으로, 두 개의 규칙이 tooallow HTTP를 추가 하 고 HTTPS 호출에서 hello 첫 번째 업스트림 앱 서비스 환경 ("fe1ase").

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

고 및 반복에 대 한 hello 두 번째 및 세 번째 업스트림 앱 서비스 환경 ("fe2ase" 및 "fe3ase").

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

마지막으로, 자신으로 다시 호출할 수 있도록 hello 백 엔드 API의 앱 서비스 환경을 액세스 toohello 아웃 바운드 IP 주소를 부여 합니다.

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

다른 네트워크 보안 규칙이 기본적으로 모든 NSG에 hello 인터넷에서에서 인바운드 액세스를 차단 하는 기본 규칙 집합이 구성 toobe가 필요 합니다.

hello hello 네트워크 보안 그룹의 규칙의 전체 목록은 다음과 같습니다.  Note 강조 표시 되어 있는 hello 마지막 규칙에서 명시적으로 부여 된 액세스 된 것과 다른 모든 호출자가에서 인바운드 액세스를 차단 하는 방법입니다.

![NSG 구성][NSGConfiguration] 

hello 마지막 단계는 hello "apiase" 앱 서비스 환경에 포함 된 tooapply hello NSG toohello 서브넷입니다.  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

Hello 적용할 NSG toohello 서브넷과만 hello 세 업스트림 앱 서비스 환경 및 hello 앱 서비스 환경 포함 hello API 백 엔드는 허용 toocall hello "apiase" 환경에.

## <a name="additional-links-and-information"></a>추가 링크 및 정보
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

[네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)에 대한 정보. 

[아웃바운드 IP 주소][NetworkArchitecture] 및 App Service 환경 이해.

App Service 환경에서 사용되는 [네트워크 포트][InboundTraffic].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
