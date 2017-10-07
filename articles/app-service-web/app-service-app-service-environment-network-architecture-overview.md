---
title: "앱 서비스 환경의 아키텍처 개요의 aaaNetwork"
description: "앱 서비스 환경의 네트워크 토폴로지의 아키텍처 개요입니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 3cbc86883f5687a9ada35a3ab2f577a450a3fa0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a>앱 서비스 환경의 네트워크 아키텍처 개요
## <a name="introduction"></a>소개
앱 서비스 환경을 만드는 데는 항상의 서브넷 내에서 한 [가상 네트워크] [ virtualnetwork] -앱 서비스 환경에서 실행 중인 앱 전용와 통신할 수 끝점 내에 있는 hello 가상 동일 네트워크 토폴로지입니다.  고객은 해당 가상 네트워크 인프라의 일부를 잠글 수 있습니다, 이므로 중요 toounderstand hello 형식의 앱 서비스 환경에서 발생 하는 네트워크 통신 흐름.

## <a name="general-network-flow"></a>일반 네트워크 흐름
ASE(앱 서비스 환경)가 앱에 공용 VIP(가상 IP 주소)를 사용하는 경우 모든 인바운드 트래픽이 해당 공용 VIP에 도착합니다.  여기에는 FTP에 대한 다른 트래픽, 원격 디버깅 기능, Azure 관리 작업과 마찬가지로 앱의 HTTP와 HTTPS 트래픽이 포함됩니다.  전체 목록은 hello에 대 한 hello 공용 VIP에서 사용할 수 있는 특정 포트 (필수 및 선택적)에 hello 문서를 참조 [인바운드 트래픽을 제어] [ controllinginboundtraffic] tooan 앱 서비스 환경입니다. 

앱 서비스 환경도 실행을 지원 tooa 가상 네트워크 내부 주소에만 연결 된 앱 ILB (내부 부하 분산 장치) 주소 tooas 라고도 합니다.  ILB는에서 응용 프로그램과 원격 디버깅 호출에 대 한 활성화 된 ASE, HTTP 및 HTTPS 트래픽을 hello ILB 주소에 도착 합니다.  가장 일반적인 ASE ILB 구성에 대 한 FTP/FTPS 트래픽의 hello ILB 주소에 도착도 됩니다.  그러나 Azure 관리 작업에는 여전히 받는 ILB의 hello 공용 VIP에 454/455 tooports 흘러 ASE를 사용할 수 있습니다.

아래 hello 다이어그램 hello 앱 바인딩된 tooa 공용 가상 IP 주소에 있는 앱 서비스 환경에 대 한 hello에 대 한 개요 다양 한 인바운드 및 아웃 바운드 네트워크 흐름 보여 줍니다.

![일반 네트워크 흐름][GeneralNetworkFlows]

앱 서비스 환경은 다양한 개인 고객 끝점과 통신할 수 있습니다.  예를 들어, 앱 서비스 환경에서 IaaS 가상 컴퓨터에서 실행 중인 toodatabase 서버에 연결할 수는 hello에서 실행 되는 앱에 동일한 가상 네트워크 토폴로지를 hello 합니다.

> [!IMPORTANT]
> Hello 네트워크 다이어그램을 살펴보면 hello 다른 계산 "리소스" hello 앱 서비스 환경에서에서 다른 서브넷에 배포 됩니다. Hello의 리소스를 배포 hello ASE 동일한 서브넷에서 특정 내부 ASE 라우팅) (제외 ASE toothose 리소스 연결을 차단 합니다. 배포 tooa 다른 서브넷 대신 (에서 동일한 VNET hello). 앱 서비스 환경 hello tooconnect 수 있게 됩니다. 추가 구성은 필요하지 않습니다.
> 
> 

앱 서비스 환경 역시 관리 및 운영에 필요한 sql DB 및 Azure 저장소와 통신할 수 있습니다.  Hello에 있는 앱 서비스 환경와 통신 하는 hello Sql 및 저장소 리소스의 일부 다른 원격 Azure 지역에 있는 동안 앱 서비스 환경 hello와 동일한 영역입니다.  결과적으로, 아웃 바운드 연결 toohello 인터넷이 항상 필요 앱 서비스 환경 toofunction 제대로 합니다. 

앱 서비스 환경 서브넷에 배포 된 네트워크 보안 그룹 사용된 toocontrol이 될 수 있습니다 하는 인바운드 트래픽 toohello 서브넷입니다.  어떻게 toocontrol 인바운드 트래픽을 tooan 앱 서비스 환경에 대 한 세부 정보를 hello 다음을 참조 하십시오. [문서][controllinginboundtraffic]합니다.

방법에 대 한 자세한 내용은 앱 서비스 환경에서 아웃 바운드 인터넷 연결 tooallow hello 다음 작업에 대 한 문서를 참조 하세요. [Express 경로][ExpressRoute]합니다.  사이트 간 연결을 사용 하 고 사용 하 여 hello 문서에 설명 된 동일한 방법을 적용 하는 hello 강제 터널링 합니다.

## <a name="outbound-network-addresses"></a>아웃 바운드 네트워크 주소
앱 서비스 환경에서는 아웃 바운드 호출을 하는 경우에 IP 주소는 hello 아웃 바운드 통화 연관 항상 합니다.  사용 되는 hello 특정 IP 주소는 hello 끝점 호출 되 고 hello 가상 네트워크 토폴로지 또는 hello 가상 네트워크 토폴로지 외부에 있는 인지에 따라 다릅니다.

호출 되 고 hello 끝점이 경우 **외부** hello 가상 네트워크 토폴로지, 아니면 hello 사용 되는 아웃 바운드 주소 (즉, hello 아웃 바운드 NAT 주소)는 hello 공용 VIP의 hello 앱 서비스 환경입니다.  이 주소 속성 블레이드에서 hello 앱 서비스 환경에 대 한 hello 포털 사용자 인터페이스에 있습니다.

![아웃 바운드 IP 주소][OutboundIPAddress]

이 주소는 hello 앱 서비스 환경에서에서 응용 프로그램을 만들고 다음을 수행 하 여 공용 VIP를 하나만 ASEs도 확인할 수 있습니다는 *nslookup* hello 응용 프로그램의 주소입니다. hello 결과 IP 주소는 모두 hello 공용 VIP를 뿐만 아니라 아웃 바운드 NAT 주소 hello 앱 서비스 환경입니다.

호출 되 고 hello 끝점이 경우 **내** hello 가상 네트워크 토폴로지의 hello 호출 응용 프로그램의 아웃 바운드 주소 hello hello hello 앱을 실행 하는 hello 개별 계산 리소스의 내부 IP 주소 됩니다.  그러나 가상 네트워크 내부 IP 주소 tooapps의 지속적으로 매핑하는 하지 않습니다.  앱이 서로 다른 계산 리소스 간에 이동할 수 및 앱 서비스 환경에서 사용 가능한 컴퓨팅 리소스의 hello 풀 tooscaling 작업 인해 변경할 수 있습니다.

그러나 앱 서비스 환경 서브넷 내에 항상 이므로 응용 프로그램을 실행 하는 계산 리소스의 내부 IP 주소 hello hello 서브넷의 hello CIDR 범위 내에 항상은 보장 됩니다.  결과적으로, 세분화 된 Acl 또는 네트워크 보안 그룹 사용 toosecure hello 가상 네트워크 내에서 끝점에 tooother 액세스, hello hello 앱 서비스 환경 요구 toobe 액세스 권한이 부여를 포함 하는 서브넷 범위입니다.

hello 다음 다이어그램에서는 이러한 개념을 자세히:

![아웃 바운드 네트워크 주소][OutboundNetworkAddresses]

다이어그램 위에 hello:

* 앱 서비스 환경 hello의 hello 공용 VIP 192.23.1.2 이므로, 하는 hello 아웃 바운드 IP 주소가 너무 호출할 때 사용 되는 "Internet" 끝점입니다.
* CIDR 범위 hello 앱 서비스 환경에 대 한 서브넷을 포함 하는 hello hello 10.0.1.0/26입니다.  다른 끝점 hello 내에서 동일한 가상 네트워크 인프라 나타납니다 호출 응용 프로그램에서이 주소 범위 내의 특정 위치에서 발생 한 것으로 합니다.

## <a name="calls-between-app-service-environments"></a>앱 서비스 환경 간의 호출
더 복잡 한 시나리오는 여러 앱 서비스 환경에 배포 하는 경우에 발생할 수 있습니다에 동일한 가상 네트워크를 hello 하 고 한 앱 서비스 환경 tooanother 앱 서비스 환경에서에서 아웃 바운드 호출을 확인 합니다.  이러한 종류의 크로스 앱 서비스 환경 호출은 "Internet" 호출로도 처리됩니다.

다음 다이어그램 hello 예를 보여 줍니다 앱과 계층화 된 아키텍처의 한 앱 서비스 환경에 (예: "프런트 도어" 웹 앱) (예: 내부 백 엔드 API 앱이 아니며 toobe hello 인터넷에서에서 액세스할 수 있는)는 두 번째 앱 서비스 환경에서 앱을 호출 합니다. 

![앱 서비스 환경 간의 호출][CallsBetweenAppServiceEnvironments] 

Hello 앱 서비스 환경 "ASE 하나" hello 위의 예제에는 192.23.1.2 아웃 바운드 IP 주소가 있습니다.  이 앱 서비스 환경에서 실행 되는 앱에서는 아웃 바운드 호출 tooan 앱 환경에서 실행 한 두 번째 응용 프로그램 서비스 ("ASE 두") 동일한 가상 네트워크, hello hello에 아웃 바운드 호출 처리 됩니다 "Internet" 호출으로 합니다.  따라서 hello에 도착 하는 hello 네트워크 트래픽은 두 번째 앱 서비스 환경이 표시 됩니다 192.23.1.2에서 발생 한 것으로 (즉, 하지 hello 서브넷의 주소 범위 hello 첫 번째 앱 서비스 환경)입니다.

앱 서비스 환경 모두 동일한 Azure 지역 hello 네트워크 hello 지역 Azure 네트워크에 그대로 남아 있게 됩니다 트래픽과 물리적으로 흐르지 hello에 있는 경우 다양 한 앱 서비스 환경 간의 호출 "Internet" 호출으로 처리 됩니다 하는 경우에 통해 공용 인터넷 hello 합니다.  네트워크 보안 그룹을 사용할 수는 결과적으로 hello의 hello 서브넷에 두 번째 앱 서비스 환경에서 인바운드 호출을 허용 하는 tooonly hello 첫 번째 앱 서비스 환경 (아웃 바운드 IP 주소가 192.23.1.2는 하는 데 사용), hello 간의 보안 통신 하는 데 앱 서비스 환경입니다.

## <a name="additional-links-and-information"></a>추가 링크 및 정보
모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

에 대 한 내용은 앱 서비스 환경에 의해 사용 되는 포트를 인바운드 및 네트워크 보안 그룹 toocontrol를 사용 하 여 인바운드 트래픽을 ´ ï ´ [여기][controllinginboundtraffic]합니다.

사용자 정의 경로 toogrant 아웃 바운드 인터넷 액세스 tooApp 서비스 환경 사용에 대 한 세부 정보는이 사용할 수 있는 [문서][ExpressRoute]합니다. 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

