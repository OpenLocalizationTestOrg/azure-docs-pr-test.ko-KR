---
title: "앱 서비스 환경에 대 한 웹 응용 프로그램 방화벽 (WAF) aaaConfiguring"
description: "앱 서비스 환경 앞에 tooconfigure 웹 응용 프로그램 방화벽 하는 방법에 대해 알아봅니다."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성
## <a name="overview"></a>개요
Hello와 같은 응용 프로그램 방화벽 웹 [Azure에 대 한 Barracuda WAF](https://www.barracuda.com/programs/azure) hello에서 확인 가능한 [Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) 사용 하면 인바운드 웹 트래픽 tooblock SQL를 검사 하 여 웹 응용 프로그램을 보호 삽입, 사이트 간 스크립팅, 맬웨어 업로드 & DDoS 응용 프로그램 및 기타 공격입니다. Hello 백 엔드 웹 서버에서 응답 hello에 대 한 데이터 손실 방지 (DLP)도 검사합니다. Hello 격리 및 앱 서비스 환경에서 제공 되는 추가 확장을 함께 제공 이상적인 환경 toowithstand 악의적인 요청 및 고용량 트래픽이 필요로 하는 toohost 비즈니스 중요 한 웹 응용 프로그램 합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>설정
자동으로 구성할이 문서에 대 한 앱 서비스 환경 뒤에 여러 부하 균형을 Barracuda WAF 인스턴스의 hello DMZ에서에서 액세스할 수 없는 고 hello WAF 트래픽만 hello 앱 서비스 환경에 연결할 수 있도록 합니다. Azure 데이터 센터 및 지역에서 Azure 트래픽 관리자 우리의 Barracuda WAF 인스턴스 tooload 균형 앞에 해야 합니다. Hello 설치 프로그램의 높은 수준의 다이어그램은 아래에 표시 되는 내용을 같습니다.

![아키텍처][Architecture] 

> 참고: hello 도입 되면서 [ILB 앱 서비스 환경에 대 한 지원](app-service-environment-with-internal-load-balancer.md), hello ASE toobe hello DMZ에서에서 액세스할 수를 구성 하 고만 사용할 수 있는 toohello 개인 네트워크를 수 있습니다. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>앱 서비스 환경 구성
앱 서비스 환경 tooconfigure 너무 참조[설명서](app-service-web-how-to-create-an-app-service-environment.md) hello 주제에 있습니다. 만들 수 있으면 만든 앱 서비스 환경, [웹 앱](app-service-web-overview.md), [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md) 및 [모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md) 모든 hello WAF 뒤 보호 될이 환경에서 했습니다 hello 다음 섹션에서 구성 합니다.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Barracuda WAF 클라우드 서비스를 구성합니다.
Barracuda에는 Azure의 가상 컴퓨터에 WAF를 배포하는 방법에 대한 [자세한 문서](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) 가 있습니다. 하지만 중복 원하는 하 고 단일 실패 지점이 발생 하지, 때문에 2 개 이상 toodeploy WAF 인스턴스 Vm hello로 이러한 지침을 진행 하는 경우 동일한 클라우드 서비스입니다.

### <a name="adding-endpoints-toocloud-service"></a>끝점 tooCloud 서비스 추가
더 많은 WAF VM 클라우드 서비스에서 인스턴스 또는 2를 사용 하 여 hello [Azure 포털](https://portal.azure.com/) hello 이미지 아래에 나와 있는 것 처럼 응용 프로그램에서 사용 되는 tooadd HTTP 및 HTTPS 끝점입니다.

![끝점 구성][ConfigureEndpoint]

응용 프로그램에서 다른 끝점을 사용 하는 경우 이러한 toothis 목록도 tooadd 있는지 확인 합니다. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>해당 관리 포털을 통해 WAF Barracuda 구성
해당 관리 포털을 통해 Barracuda WAF를 사용하여 TCP Port 8000에 대해 구성합니다. Hello WAF Vm의 여러 인스턴스 개 있으므로 각 VM 인스턴스에 대 한 toorepeat hello 여기에 나오는 단계를 해야 합니다. 

> 참고: WAF 구성 했으면 hello TCP/8000 끝점에서에서 제거 하면 모든 WAF Vm tookeep 프로그램 WAF 보안 합니다.
> 
> 

그림과 같이 hello tooconfigure 아래 Barracuda WAF hello 관리 끝점을 추가 합니다.

![관리 끝점 추가][AddManagementEndpoint]

클라우드 서비스에 브라우저 toobrowse toohello 관리 끝점을 사용 합니다. 클라우드 서비스는 test.cloudapp.net를 호출 하는 경우 액세스 하는 것이 끝점 toohttp://test.cloudapp.net:8000 이동 하 여 합니다. 로그인 페이지가 표시 되어야 아래와 같은 hello WAF VM 설치 단계에서 지정한 자격 증명을 사용 하 여 로그인 할 수 있습니다.

![관리 로그인 페이지][ManagementLoginPage]

한 번 로그인 hello로 대시보드에 나타납니다 hello WAF 보호에 대 한 기본 통계를 제공 합니다 hello 이미지 아래에서 하나.

![관리 대시보드][ManagementDashboard]

Hello 서비스 탭을 클릭 하 여 WAF, 보호 하는 서비스에 대 한 구성할 수 있습니다. Barracuda WAF를 구성하는 방법에 대한 자세한 내용은 [해당 설명서](https://techlib.barracuda.com/waf/getstarted1)를 참조하세요. Azure 웹 앱 아래 hello 예제에서에서 HTTP 및 HTTPS 트래픽을 처리 구성 되었습니다.

![관리 서비스를 추가 합니다.][ManagementAddServices]

> 참고: 응용 프로그램 구성 방법 및 앱 서비스 환경에서 어떤 기능을 사용 하는 따라 tooforward 트래픽을에 필요한 TCP 포트 80 및 443 이외의 포트 예를 들어 웹 응용 프로그램에 대 한 IP SSL 설정 되어 있는 경우. 앱 서비스 환경에서 사용 되는 네트워크 포트의 목록은 참조 하십시오 너무[제어 인바운드 트래픽을 설명서](app-service-app-service-environment-control-inbound-traffic.md) 네트워크 포트 섹션.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Microsoft Azure 트래픽 관리자를 구성합니다. (선택 사항)
응용 프로그램은 여러 지역에서 사용할 수 있는 경우 tooload 균형 원하는 뒤에 [Azure 트래픽 관리자](../traffic-manager/traffic-manager-overview.md)합니다. hello에 끝점을 추가할 수 있도록 toodo [Azure 클래식 포털](https://manage.azure.com) hello 이미지 아래에 나와 있는 것 처럼 hello 트래픽 관리자 프로필에서 프로그램 WAF hello 클라우드 서비스 이름을 사용 하 여 합니다. 

![트래픽 관리자 끝점][TrafficManagerEndpoint]

응용 프로그램에 인증이 필요한 경우 응용 프로그램의 가용성을 hello에 대 한 트래픽 관리자 tooping에 대 한 인증이 필요 하지 않은 일부 리소스를 사용할 확인 합니다. Hello에 hello 구성 섹션에서 hello URL을 구성할 수 있습니다 [Azure 클래식 포털](https://manage.azure.com) 다음과 같이 합니다.

![트래픽 관리자를 구성하는 방법][ConfigureTrafficManager]

tooforward hello 트래픽 관리자 WAF tooyour 응용 프로그램에서 ping, 응용 프로그램에 Barracuda WAF tooforward 트래픽 tooyour 아래 hello 예에 나와 있는 것 처럼 toosetup 웹 사이트 번역 할 수 있습니다.

![웹사이트 번역][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>서비스 환경을 사용 하 여 보안 그룹 NSG (네트워크) 트래픽을 tooApp 보안 설정
Hello에 따라 [제어 인바운드 트래픽을 설명서](app-service-app-service-environment-control-inbound-traffic.md) 제한에 대 한 내용은 클라우드 서비스의 hello VIP 주소를 사용 해야만 tooyour 앱 서비스 환경 hello WAF에서에서 트래픽을 대 한 합니다. TCP 포트 80에 대한 작업을 수행 하기 위한 샘플 Powershell 명령은 다음과 같습니다.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Hello SourceAddressPrefix hello WAF의 클라우드 서비스의 가상 IP 주소 (VIP)로 대체 합니다.

> 참고: 클라우드 서비스의 hello VIP를 삭제 하 고 다시 hello 클라우드 서비스를 만들 때 변경 됩니다. 확인 되었는지 tooupdate hello IP 주소를 이렇게 하면 hello 네트워크 리소스 그룹입니다. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
