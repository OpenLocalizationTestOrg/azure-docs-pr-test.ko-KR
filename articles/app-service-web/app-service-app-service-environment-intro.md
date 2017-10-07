---
title: "aaaIntroduction tooApp 서비스 환경 v1"
description: "모든 앱을 실행 하기 위한 보안, VNet에 가입 된, 전용 배율 단위를 제공 하는 hello 앱 서비스 환경 v1 기능에 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>소개 tooApp 서비스 환경 v1

> [!NOTE]
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다.  최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
> 

## <a name="overview"></a>개요
App Service 환경은 Azure App Service의 [프리미엄][PremiumTier] 서비스 계획 옵션으로, [웹앱][WebApps], [Mobile Apps][MobileApps] 및 [API 앱][APIApps]을 포함하여 높은 확장성에서 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공합니다.  

앱 서비스 환경은 다음을 필요로 하는 응용 프로그램 작업에 적합합니다.

* 매우 높은 확장성
* 격리 및 보안된 네트워크 액세스

고객은 단일 Azure 지역 내뿐만 아니라 여러 Azure 지역에 걸쳐서 여러 앱 서비스 환경을 만들 수 있습니다.  따라서 앱 서비스 환경은 높은 RPS 작업을 지원하여 상태가 없는 응용 프로그램 계층을 수평적으로 확장하는 데 적합합니다.

앱 서비스 환경은 격리 된 toorunning만 단일 고객의 응용 프로그램 및 가상 네트워크에 배포 됩니다.  고객 모두 인바운드 및 아웃 바운드 응용 프로그램 네트워크 트래픽 세부적으로 제어 해야 하 고 응용 프로그램 가상 네트워크 tooon 온-프레미스 회사 리소스에 대해 고속 보안 연결을 설정할 수 있습니다.

모든 문서와 방법을-에 대 한의 하려면 앱 서비스 환경 hello에서 사용할 수 있는 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

앱 서비스 환경을 확장할 수 있습니다. 사용 하도록 설정 하 고 보호 하는 방법에 대 한 개요에 대 한 네트워크 액세스를 참조 하십시오 hello [AzureCon 심층 분석] [ AzureConDeepDive] 앱 서비스 환경에!

여러 앱 서비스 환경 방법에 hello 문서 참조를 사용 하 여 수평 확장에 심층적에 대 한 toosetup는 [지리적으로 분산 응용 프로그램 메모리 사용량이][GeodistributedAppFootprint]합니다.

구현에 hello 문서를 참조 하는 hello AzureCon 심층 분석에에서 표시 된 hello 보안 아키텍처 구성 방법 toosee는 [보안 아키텍처를 계층화](app-service-app-service-environment-layered-security.md) 앱 서비스 환경을 사용 하 여 합니다.

앱 서비스 환경에서 실행 중인 앱은 웹 응용 프로그램 방화벽 (WAF) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다.  hello 문서 [는 WAF 앱 서비스 환경에 대 한 구성](app-service-app-service-environment-web-application-firewall.md) 이 시나리오에 설명 합니다. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>전용 계산 리소스
앱 서비스 환경으로 구성할 수 있습니다에 배타적으로 사용 (50) toofifty 계산 리소스를 한 응용 프로그램 및 독점적으로 tooa 단일 구독 전용 모든 앱 서비스 환경에서 리소스는 hello 계산 합니다.

앱 서비스 환경으로 프런트 엔드 계산 리소스 풀 하나 toothree 작업자 계산 리소스 풀으로 구성 됩니다. 

hello 프런트 엔드 풀도 자동 부하 분산을 앱 서비스 환경 내에서 응용 프로그램 요청으로 SSL 종료를 담당 하는 계산 리소스를 포함 합니다. 

너무 할당 된 계산 리소스를 포함 하는 각 작업자 풀[앱 서비스 계획][AppServicePlan], 하나 이상의 Azure 앱 서비스 앱에 포함 하는 합니다.  수 있으므로 toothree 다른 작업자 풀을 앱 서비스 환경에서 각 작업자 풀에 대 한 hello 유연성 toochoose 다른 계산 리소스 해야 합니다.  

예를 들어이 있습니다 성능이 낮은 계산 리소스가 포함 된 하나의 작업자 풀을 toocreate 개발 또는 테스트 앱을 위한 앱 서비스 계획에 대 한.  두 번째(또는 세 번째) 작업자 풀은 프로덕션 앱을 실행하는 앱 서비스 계획에 성능이 보다 뛰어난 계산 리소스를 사용할 수 있습니다.

계산 리소스 사용 가능한 toohello 프런트 엔드 및 작업자 풀의 hello 수량에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooConfigure 앱 서비스 환경][HowToConfigureanAppServiceEnvironment]합니다.  

앱 서비스 환경에서 지원 되는 리소스 크기를 계산 하는 사용 가능한 hello에 대 한 세부 정보에 대 한 참조 hello [앱 서비스 가격 책정] [ AppServicePricing] 페이지 hello 앱 서비스 환경에 대 한 사용 가능한 옵션을 검토 하 고 hello 프리미엄 가격 책정 계층

## <a name="virtual-network-support"></a>가상 네트워크 지원
App Service 환경을 Azure Resource Manager 가상 네트워크에서 **만들 수도 있고** 클래식 배포 모델 가상 네트워크에서 **만들 수도 있습니다**([가상 네트워크에 대한 추가 정보][MoreInfoOnVirtualNetworks] 참조).  앱 서비스 환경 내 가상 네트워크의 서브넷에서 보다 정확 하 게 하 고 가상 네트워크에 항상 존재 하므로 인바운드 및 아웃 바운드 네트워크 통신의 두 가상 네트워크 toocontrol의 보안 기능 hello를 활용할 수 있습니다.  

App Service Environment는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.

사용할 수 있습니다 [네트워크 보안 그룹] [ NetworkSecurityGroups] toorestrict 인바운드 네트워크 통신 toohello 서브넷 앱 서비스 환경 상주 합니다.  이렇게 하면 업스트림 장치 및 웹 응용 프로그램 방화벽 및 네트워크 SaaS 공급자와 같은 서비스의 데이터로 toorun 앱 있습니다.

앱은 tooaccess 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스를 자주 필요 합니다.  일반적인 접근 방식은 toomake 이러한 끝점 사용 가능한 유일한 toointernal 네트워크 트래픽 Azure 가상 네트워크 내에서 흐름은 합니다.  앱 서비스 환경에 가입된 toohello 되 면 hello 환경에서 실행 되는 앱 hello 내부 서비스와 동일한 가상 네트워크를 통해 연결할 수 있는 끝점을 포함 하 여 액세스할 수 [사이트 간] [ SiteToSite]및 [Azure express 경로] [ ExpressRoute] 연결 합니다.

앱 서비스 환경 온-프레미스 네트워크 및 가상 네트워크와 작동 하는 방식에 대 한 자세한 내용은 참조 문서에 나오는에 hello에 대 한 [네트워크 아키텍처][NetworkArchitectureOverview], [인바운드 제어 트래픽][ControllingInboundTraffic], 및 [안전 하 게 연결 tooBackends][SecurelyConnectingToBackends]합니다. 

## <a name="getting-started"></a>시작
앱 서비스 환경 시작 tooget 참조 [어떻게 tooCreate An 앱 서비스 환경][HowToCreateAnAppServiceEnvironment]

모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.

Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.

Hello 앱 서비스 환경 네트워크 아키텍처의 개요를 참조 hello [네트워크 아키텍처 개요] [ NetworkArchitectureOverview] 문서.

ExpressRoute를 사용 앱 서비스 환경을 사용 하 여 참조 다음 문서 hello [Express 경로 및 앱 서비스 환경][NetworkConfigDetailsForExpressRoute]합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


