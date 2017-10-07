---
title: "aaaIntroduction tooAzure 앱 서비스 환경"
description: "Azure App Service Environment에 대한 간략한 개요"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 3c7eaefa-1850-4643-8540-428e8982b7cb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 9261041333cf59374974a039edf89c4983c45cdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environments"></a>소개 tooApp 서비스 환경 #
 
## <a name="overview"></a>개요 ##

Azure App Service Environment는 App Service 앱을 매우 높은 확장성으로 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공하는 Azure App Service 기능입니다. 이 기능은 [웹앱][webapps], [모바일 앱][mobileapps], [API 앱][APIapps] 및 [함수][Functions]를 호스트할 수 있습니다.

ASE(App Service Environment)는 다음을 필요로 하는 응용 프로그램 워크로드에 적합합니다.

- 매우 높은 확장성
- 격리 및 보안된 네트워크 액세스
- 높은 메모리 사용률

고객은 단일 Azure 지역 내 또는 여러 Azure 지역에 걸쳐서 여러 ASE를 만들 수 있습니다. 따라서 ASE는 높은 RPS 워크로드를 지원하여 상태 비저장 응용 프로그램 계층을 수평적으로 크기 조정하는 데 적합합니다.

ASEs toorunning 격리 된 응용 프로그램에 단일 고객의만 되며 가상 네트워크에 배포 됩니다. 고객은 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽을 세부적으로 제어할 수 있습니다. 응용 프로그램 Vpn tooon 온-프레미스 회사 리소스에 대해 고속 보안 연결을 설정할 수 있습니다.

Hello에서 사용할 수 있는 모든 문서 및 ASEs에 대 한 방법 tooinstructions [앱 서비스 환경에 대 한 추가 정보][ASEReadme]:

* ASE를 통해 보안 네트워크 액세스 권한이 있는 확장성이 뛰어난 앱 호스팅을 사용할 수 있습니다. 자세한 내용은 참조 hello [AzureCon 심층 분석](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) ASEs에 있습니다.
* 여러 ASEs 사용된 tooscale를 가로로 될 수 있습니다. 자세한 내용은 참조 [어떻게 지리적으로 분산 응용 프로그램 공간만 사용 tooset](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)합니다.
* ASEs는 hello AzureCon 심층 분석에에서 나와 있는 것 처럼 사용 되는 tooconfigure 보안 아키텍처를 수 있습니다. hello AzureCon 심층 분석에에서 표시 된 hello 보안 아키텍처 구성 방법 toosee 참조 hello [방법에 대 한 문서 tooimplement 계층화 된 보안 아키텍처](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) 앱 서비스 환경을 사용 하 여 합니다.
* ASE에서 실행 중인 앱은 WAF(웹 응용 프로그램 방화벽) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다. 자세한 내용은 [App Service Environment에 대한 WAF 구성](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)을 참조하세요.

## <a name="dedicated-environment"></a>전용 환경 ##

ASE는 단독으로 tooa 단일 구독 전용 및 인스턴스 수가 100을 호스팅할 수 있습니다. hello 범위는 단일 앱 서비스 계획 too100 단일 인스턴스 응용 프로그램 서비스 계획 및 사이 있는 모든 항목에 인스턴스 수가 100을 확장할 수 있습니다.

ASE는 프런트 엔드 및 작업자로 구성됩니다. 프런트 엔드는 ASE 내의 앱 요청에 대한 자동 부하 분산 및 HTTP/HTTPS 종료를 담당합니다. 프런트 엔드 hello ASE에 앱 서비스 계획 하 여 확장 되어 hello로 자동으로 추가 됩니다.

작업자는 고객 앱을 호스트하는 역할입니다. 작업자는 3가지 고정된 크기로 사용할 수 있습니다.

* 1 코어/3.5GB RAM
* 2 코어/7GB RAM
* 4 코어/14GB RAM

고객은 toomanage 프런트 엔드 및 작업 자가 필요 하지 않습니다. 모든 인프라는 고객이 App Service 계획을 스케일 아웃함에 따라 자동으로 추가됩니다. 앱 서비스 계획 생성 되거나 ASE에 수평으로 hello 인프라 추가 또는 제거를 적절 하 게 필요 합니다.

편평한 월정액 hello 인프라에 대 한 대금을 지급 한다는 및 hello ASE hello 크기가 변경 되지 않습니다는 ASE에 있습니다. 거기에 App Service 계획 코어당 비용이 발생합니다. Hello에 ASE에 호스트 되는 모든 앱은 SKU 가격을 격리 합니다. ASE에 대 한 가격 책정에 대 한 내용은 hello 참조 [앱 서비스 가격 책정] [ Pricing] 페이지 및 hello ASEs에 대 한 사용 가능한 옵션에 설명 합니다.

## <a name="virtual-network-support"></a>가상 네트워크 지원 ##

ASE는 Azure Resource Manager 가상 네트워크에서만 만들 수 있습니다. Azure 가상 네트워크에 대해 자세히 toolearn 참조 hello [Azure 가상 네트워크 FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)합니다. ASE는 항상 가상 네트워크 내 존재하며, 더 정확하게는 가상 네트워크의 서브넷 내에 있습니다. 가상 네트워크 toocontrol 인바운드 및 아웃 바운드의 hello 보안 기능을 사용 하려면 앱에 대 한 통신 네트워크.

ASE는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.

[네트워크 보안 그룹] [ NSGs] ASE 있는 인바운드 네트워크 통신 toohello 서브넷을 제한 합니다. 업스트림 장치 및 WAFs 및 네트워크 SaaS 공급자와 같은 서비스의 데이터로 Nsg toorun 앱을 사용할 수 있습니다.

앱은 tooaccess 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스를 자주 필요 합니다. VPN 연결 toohello 온-프레미스 네트워크에 있는 가상 네트워크의 hello ASE를 배포 하는 경우 hello ASE에에서 hello 앱 hello 온-프레미스 리소스에 액세스할 수 있습니다. 이 기능은 hello VPN 인지에 관계 없이 true는 [사이트 간](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) 또는 [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.

ASE가 가상 네트워크 및 온-프레미스 네트워크와 함께 어떻게 작동하는지에 대한 자세한 내용은 [App Service Environment 네트워크 고려 사항][ASENetwork]을 참조하세요.

## <a name="app-service-environment-v1"></a>App Service 환경 v1 ##

App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다. 앞에 정보 hello ASEv2 기반 합니다. 이 섹션 ASEv1와 ASEv2 차이점 hello를 표시 합니다. 

Toomanage ASEv1에 필요한 리소스를 수동으로 hello 모든 합니다. Hello 프런트 엔드, 작업자 및 IP 기반 SSL에 사용 되는 IP 주소를 포함 하 합니다. 앱 서비스 계획을 확장할 수 있습니다, 먼저 toofirst toohost 원하는 hello 작업자 풀 아웃 확장 합니다.

ASEv1은 ASEv2와는 다른 가격 책정 모델을 사용합니다. ASEv1에서는 할당된 각 코어에 대한 비용을 지불해야 합니다. 여기에는 워크로드를 호스트하지 않는 프런트 엔드 또는 작업자에 사용된 코어가 포함됩니다. ASEv1에서 hello 기본 최대 규모의 ASE 크기가 55 총 호스트입니다. 여기에는 작업자 및 프런트 엔드가 포함됩니다. 한 이점은 tooASEv1은 클래식 가상 네트워크와 리소스 관리자 가상 네트워크에 배포할 수 있습니다. toolearn ASEv1에 대 한 자세한 참조 [앱 서비스 환경 v1 소개][ASEv1Intro]합니다.

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
