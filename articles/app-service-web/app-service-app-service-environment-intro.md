---
title: "App Service Environment v1 소개"
description: "모든 앱을 실행하기 위한 안전한 VNet 가입 전용 배율 단위를 제공하는 App Service Environment v1 기능을 알아봅니다."
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="d2804-103">App Service Environment v1 소개</span><span class="sxs-lookup"><span data-stu-id="d2804-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="d2804-104">이 문서는 ASE(App Service Environment) v1에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="d2804-105">사용하기가 더 쉽고 더 강력한 인프라에서 실행되는 최신 버전의 App Service Environment가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="d2804-106">새 버전에 대한 자세한 내용은 [App Service Environment 소개](../app-service/app-service-environment/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="d2804-107">개요</span><span class="sxs-lookup"><span data-stu-id="d2804-107">Overview</span></span>
<span data-ttu-id="d2804-108">App Service 환경은 Azure App Service의 [프리미엄][PremiumTier] 서비스 계획 옵션으로, [웹앱][WebApps], [Mobile Apps][MobileApps] 및 [API 앱][APIApps]을 포함하여 높은 확장성에서 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="d2804-109">앱 서비스 환경은 다음을 필요로 하는 응용 프로그램 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="d2804-110">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="d2804-110">Very high scale</span></span>
* <span data-ttu-id="d2804-111">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="d2804-111">Isolation and secure network access</span></span>

<span data-ttu-id="d2804-112">고객은 단일 Azure 지역 내뿐만 아니라 여러 Azure 지역에 걸쳐서 여러 앱 서비스 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="d2804-113">따라서 앱 서비스 환경은 높은 RPS 작업을 지원하여 상태가 없는 응용 프로그램 계층을 수평적으로 확장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="d2804-114">앱 서비스 환경은 단일 고객의 응용 프로그램만을 실행하도록 격리되며 항상 가상 네트워크에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="d2804-115">고객은 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽 둘 다에 대해 세밀하게 제어할 수 있고 응용 프로그램은 가상 네트워크를 통해 온-프레미스 회사 리소스에 고속 보안 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="d2804-116">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d2804-117">App Service 환경이 어떻게 높은 확장성을 사용하고 네트워크 액세스를 보호할 수 있는지에 대한 개요는 App Service 환경에서 [AzureCon 심층 분석][AzureConDeepDive]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="d2804-118">여러 App Service 환경을 사용하는 수평 확장에 대한 심층 분석은 [지역 분산 앱 메모리 공간][GeodistributedAppFootprint]을 설정하는 방법에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="d2804-119">AzureCon 심층 분석에 표시된 보안 아키텍처를 구성하는 방법을 보려면 앱 서비스 환경을 사용하여 [계층화된 보안 아키텍처](app-service-app-service-environment-layered-security.md) 를 구현하는데 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="d2804-120">앱 서비스 환경에서 실행 중인 앱은 웹 응용 프로그램 방화벽 (WAF) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="d2804-121">[앱 서비스 환경에 대한 WAF 구성](app-service-app-service-environment-web-application-firewall.md) 의 문서는 이 시나리오에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="d2804-122">전용 계산 리소스</span><span class="sxs-lookup"><span data-stu-id="d2804-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="d2804-123">앱 서비스 환경의 모든 컴퓨터 리소스는 전적으로 단일 구독 전용이며 앱 서비스 환경은 단일 응용 프로그램 전용으로 최대 50개 계산 리소스로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="d2804-124">앱 서비스 환경은 1~3개 작업자 계산 리소스 풀뿐만 아니라 프런트 엔드 계산 리소스 풀로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="d2804-125">프런트 엔드 풀에는 앱 서비스 환경 내의 앱 요청에 대한 자동 부하 분산뿐 아니라 SSL 종료를 담당하는 계산 리소스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="d2804-126">각 작업자 풀에는 하나 이상의 Azure App Service 앱을 포함하는 [App Service 계획][AppServicePlan]에 할당된 계산 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="d2804-127">앱 서비스 환경에는 최대 세 가지 작업자 풀을 둘 수 있으므로 작업자 풀마다 다른 계산 리소스를 유연하게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="d2804-128">예를 들어 앱 개발 또는 테스트용 앱 서비스 계획에 사용하기 위해 성능이 낮은 계산 리소스가 포함된 하나의 작업자 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="d2804-129">두 번째(또는 세 번째) 작업자 풀은 프로덕션 앱을 실행하는 앱 서비스 계획에 성능이 보다 뛰어난 계산 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="d2804-130">프런트 엔드 및 작업자 풀에 사용할 수 있는 계산 리소스의 양에 대한 자세한 내용은 [App Service 환경을 구성하는 방법][HowToConfigureanAppServiceEnvironment]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="d2804-131">App Service 환경에서 지원되는 사용 가능한 계산 리소스 크기에 대한 자세한 내용은 [App Service 가격][AppServicePricing] 페이지에서 프리미엄 가격 책정 계층의 App Service 환경에 사용 가능한 옵션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="d2804-132">가상 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="d2804-132">Virtual Network Support</span></span>
<span data-ttu-id="d2804-133">App Service 환경을 Azure Resource Manager 가상 네트워크에서 **만들 수도 있고** 클래식 배포 모델 가상 네트워크에서 **만들 수도 있습니다**([가상 네트워크에 대한 추가 정보][MoreInfoOnVirtualNetworks] 참조).</span><span class="sxs-lookup"><span data-stu-id="d2804-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="d2804-134">앱 서비스 환경은 항상 가상 네트워크, 더 정확히 말하자면 가상 네트워크의 서브넷 내에 존재하므로 가상 네트워크의 보안 기능을 활용하여 인바운드 및 아웃바운드 네트워크 통신을 모두 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="d2804-135">App Service Environment는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="d2804-136">[네트워크 보안 그룹][NetworkSecurityGroups]을 사용하여 App Service 환경이 있는 서브넷에 대한 인바운드 네트워크 통신을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="d2804-137">이 옵션을 통해 웹 응용 프로그램 방화벽 및 SaaS 공급자와 같은 업스트림 장치 및 서비스 뒤에서 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="d2804-138">또한 앱에서는 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스에 자주 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="d2804-139">일반적인 접근 방법은 Azure 가상 네트워크 내에서 이동하는 내부 네트워크 트래픽에만 이러한 끝점을 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="d2804-140">App Service 환경이 내부 서비스와 동일한 가상 네트워크에 가입되면 해당 환경에서 실행되는 앱은 [사이트 간][SiteToSite] 및 [Azure ExpressRoute][ExpressRoute] 연결을 통해 도달할 수 있는 끝점을 비롯하여 내부 서비스에 액세스할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="d2804-141">App Service 환경이 가상 네트워크 및 온-프레미스 네트워크와 함께 작동하는 방법에 대한 자세한 내용은 [네트워크 아키텍처][NetworkArchitectureOverview], [인바운드 트래픽 제어][ControllingInboundTraffic] 및 [백 엔드에 안전하게 연결][SecurelyConnectingToBackends]에 대한 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="d2804-142">시작</span><span class="sxs-lookup"><span data-stu-id="d2804-142">Getting started</span></span>
<span data-ttu-id="d2804-143">App Service 환경을 시작하려면 [App Service 환경을 만드는 방법][HowToCreateAnAppServiceEnvironment]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="d2804-144">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2804-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d2804-145">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service][AzureAppService]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="d2804-146">App Service 환경 네트워크 아키텍처의 개요는 [네트워크 아키텍처 개요][NetworkArchitectureOverview] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="d2804-147">ExpressRoute로 App Service 환경을 사용하는 방법에 대한 자세한 내용은 [Express 경로 및 App Service 환경][NetworkConfigDetailsForExpressRoute]에 대한 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2804-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


