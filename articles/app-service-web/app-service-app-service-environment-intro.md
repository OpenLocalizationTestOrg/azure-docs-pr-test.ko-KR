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
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="2da15-103">소개 tooApp 서비스 환경 v1</span><span class="sxs-lookup"><span data-stu-id="2da15-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="2da15-104">앱 서비스 환경 v1 hello에 대 한이 문서는입니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="2da15-105">최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="2da15-106">hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="2da15-107">개요</span><span class="sxs-lookup"><span data-stu-id="2da15-107">Overview</span></span>
<span data-ttu-id="2da15-108">App Service 환경은 Azure App Service의 [프리미엄][PremiumTier] 서비스 계획 옵션으로, [웹앱][WebApps], [Mobile Apps][MobileApps] 및 [API 앱][APIApps]을 포함하여 높은 확장성에서 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="2da15-109">앱 서비스 환경은 다음을 필요로 하는 응용 프로그램 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="2da15-110">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="2da15-110">Very high scale</span></span>
* <span data-ttu-id="2da15-111">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="2da15-111">Isolation and secure network access</span></span>

<span data-ttu-id="2da15-112">고객은 단일 Azure 지역 내뿐만 아니라 여러 Azure 지역에 걸쳐서 여러 앱 서비스 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="2da15-113">따라서 앱 서비스 환경은 높은 RPS 작업을 지원하여 상태가 없는 응용 프로그램 계층을 수평적으로 확장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="2da15-114">앱 서비스 환경은 격리 된 toorunning만 단일 고객의 응용 프로그램 및 가상 네트워크에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="2da15-115">고객 모두 인바운드 및 아웃 바운드 응용 프로그램 네트워크 트래픽 세부적으로 제어 해야 하 고 응용 프로그램 가상 네트워크 tooon 온-프레미스 회사 리소스에 대해 고속 보안 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="2da15-116">모든 문서와 방법을-에 대 한의 하려면 앱 서비스 환경 hello에서 사용할 수 있는 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="2da15-117">앱 서비스 환경을 확장할 수 있습니다. 사용 하도록 설정 하 고 보호 하는 방법에 대 한 개요에 대 한 네트워크 액세스를 참조 하십시오 hello [AzureCon 심층 분석] [ AzureConDeepDive] 앱 서비스 환경에!</span><span class="sxs-lookup"><span data-stu-id="2da15-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="2da15-118">여러 앱 서비스 환경 방법에 hello 문서 참조를 사용 하 여 수평 확장에 심층적에 대 한 toosetup는 [지리적으로 분산 응용 프로그램 메모리 사용량이][GeodistributedAppFootprint]합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="2da15-119">구현에 hello 문서를 참조 하는 hello AzureCon 심층 분석에에서 표시 된 hello 보안 아키텍처 구성 방법 toosee는 [보안 아키텍처를 계층화](app-service-app-service-environment-layered-security.md) 앱 서비스 환경을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="2da15-120">앱 서비스 환경에서 실행 중인 앱은 웹 응용 프로그램 방화벽 (WAF) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="2da15-121">hello 문서 [는 WAF 앱 서비스 환경에 대 한 구성](app-service-app-service-environment-web-application-firewall.md) 이 시나리오에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="2da15-122">전용 계산 리소스</span><span class="sxs-lookup"><span data-stu-id="2da15-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="2da15-123">앱 서비스 환경으로 구성할 수 있습니다에 배타적으로 사용 (50) toofifty 계산 리소스를 한 응용 프로그램 및 독점적으로 tooa 단일 구독 전용 모든 앱 서비스 환경에서 리소스는 hello 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="2da15-124">앱 서비스 환경으로 프런트 엔드 계산 리소스 풀 하나 toothree 작업자 계산 리소스 풀으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="2da15-125">hello 프런트 엔드 풀도 자동 부하 분산을 앱 서비스 환경 내에서 응용 프로그램 요청으로 SSL 종료를 담당 하는 계산 리소스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="2da15-126">너무 할당 된 계산 리소스를 포함 하는 각 작업자 풀[앱 서비스 계획][AppServicePlan], 하나 이상의 Azure 앱 서비스 앱에 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="2da15-127">수 있으므로 toothree 다른 작업자 풀을 앱 서비스 환경에서 각 작업자 풀에 대 한 hello 유연성 toochoose 다른 계산 리소스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="2da15-128">예를 들어이 있습니다 성능이 낮은 계산 리소스가 포함 된 하나의 작업자 풀을 toocreate 개발 또는 테스트 앱을 위한 앱 서비스 계획에 대 한.</span><span class="sxs-lookup"><span data-stu-id="2da15-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="2da15-129">두 번째(또는 세 번째) 작업자 풀은 프로덕션 앱을 실행하는 앱 서비스 계획에 성능이 보다 뛰어난 계산 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="2da15-130">계산 리소스 사용 가능한 toohello 프런트 엔드 및 작업자 풀의 hello 수량에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooConfigure 앱 서비스 환경][HowToConfigureanAppServiceEnvironment]합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="2da15-131">앱 서비스 환경에서 지원 되는 리소스 크기를 계산 하는 사용 가능한 hello에 대 한 세부 정보에 대 한 참조 hello [앱 서비스 가격 책정] [ AppServicePricing] 페이지 hello 앱 서비스 환경에 대 한 사용 가능한 옵션을 검토 하 고 hello 프리미엄 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="2da15-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="2da15-132">가상 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="2da15-132">Virtual Network Support</span></span>
<span data-ttu-id="2da15-133">App Service 환경을 Azure Resource Manager 가상 네트워크에서 **만들 수도 있고** 클래식 배포 모델 가상 네트워크에서 **만들 수도 있습니다**([가상 네트워크에 대한 추가 정보][MoreInfoOnVirtualNetworks] 참조).</span><span class="sxs-lookup"><span data-stu-id="2da15-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="2da15-134">앱 서비스 환경 내 가상 네트워크의 서브넷에서 보다 정확 하 게 하 고 가상 네트워크에 항상 존재 하므로 인바운드 및 아웃 바운드 네트워크 통신의 두 가상 네트워크 toocontrol의 보안 기능 hello를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="2da15-135">App Service Environment는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="2da15-136">사용할 수 있습니다 [네트워크 보안 그룹] [ NetworkSecurityGroups] toorestrict 인바운드 네트워크 통신 toohello 서브넷 앱 서비스 환경 상주 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="2da15-137">이렇게 하면 업스트림 장치 및 웹 응용 프로그램 방화벽 및 네트워크 SaaS 공급자와 같은 서비스의 데이터로 toorun 앱 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="2da15-138">앱은 tooaccess 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스를 자주 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="2da15-139">일반적인 접근 방식은 toomake 이러한 끝점 사용 가능한 유일한 toointernal 네트워크 트래픽 Azure 가상 네트워크 내에서 흐름은 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="2da15-140">앱 서비스 환경에 가입된 toohello 되 면 hello 환경에서 실행 되는 앱 hello 내부 서비스와 동일한 가상 네트워크를 통해 연결할 수 있는 끝점을 포함 하 여 액세스할 수 [사이트 간] [ SiteToSite]및 [Azure express 경로] [ ExpressRoute] 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="2da15-141">앱 서비스 환경 온-프레미스 네트워크 및 가상 네트워크와 작동 하는 방식에 대 한 자세한 내용은 참조 문서에 나오는에 hello에 대 한 [네트워크 아키텍처][NetworkArchitectureOverview], [인바운드 제어 트래픽][ControllingInboundTraffic], 및 [안전 하 게 연결 tooBackends][SecurelyConnectingToBackends]합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="2da15-142">시작</span><span class="sxs-lookup"><span data-stu-id="2da15-142">Getting started</span></span>
<span data-ttu-id="2da15-143">앱 서비스 환경 시작 tooget 참조 [어떻게 tooCreate An 앱 서비스 환경][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="2da15-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="2da15-144">모든 문서와 방법을-hello에서 사용할 수 있는 앱 서비스 환경에 대 한의 하려면 [응용 프로그램 서비스 환경에 대 한 추가 정보](../app-service/app-service-app-service-environments-readme.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="2da15-145">Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스][AzureAppService]합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="2da15-146">Hello 앱 서비스 환경 네트워크 아키텍처의 개요를 참조 hello [네트워크 아키텍처 개요] [ NetworkArchitectureOverview] 문서.</span><span class="sxs-lookup"><span data-stu-id="2da15-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="2da15-147">ExpressRoute를 사용 앱 서비스 환경을 사용 하 여 참조 다음 문서 hello [Express 경로 및 앱 서비스 환경][NetworkConfigDetailsForExpressRoute]합니다.</span><span class="sxs-lookup"><span data-stu-id="2da15-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


