---
title: "서비스 환경을 aaaApp | Microsoft Docs"
description: "Azure App 서비스 환경이란? 소개 tooApp 서비스 환경입니다."
keywords: "Azure App 서비스 환경, 가상 네트워크, 보안 네트워킹"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="c5d75-105">앱 서비스 환경 설명서</span><span class="sxs-lookup"><span data-stu-id="c5d75-105">App Service Environment Documentation</span></span>
<span data-ttu-id="c5d75-106">App Service 환경은 Azure App Service의 [프리미엄][PremiumTier] 서비스 계획 옵션으로, [웹앱][WebApps], [Mobile Apps][MobileApps] 및 [API 앱][APIApps]을 포함하여 높은 확장성에서 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="c5d75-107">앱 서비스 환경은 다음을 필요로 하는 응용 프로그램 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="c5d75-108">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="c5d75-108">Very high scale</span></span>
* <span data-ttu-id="c5d75-109">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="c5d75-109">Isolation and secure network access</span></span>

<span data-ttu-id="c5d75-110">고객은 단일 Azure 지역 내뿐만 아니라 여러 Azure 지역에 걸쳐서 여러 앱 서비스 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="c5d75-111">따라서 앱 서비스 환경은 높은 RPS 작업을 지원하여 상태가 없는 응용 프로그램 계층을 수평적으로 확장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="c5d75-112">앱 서비스 환경은 격리 된 toorunning만 단일 고객의 응용 프로그램 및 가상 네트워크에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="c5d75-113">고객은 [네트워크 보안 그룹][NetworkSecurityGroups]을 사용하여 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽을 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="c5d75-114">응용 프로그램은 가상 네트워크 tooon 온-프레미스 회사 리소스에 대해 고속 보안 연결을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="c5d75-115">앱은 tooaccess 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스를 자주 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="c5d75-116">App Service 환경에서 실행 중인 앱은 [사이트 간][SiteToSite] VPN 및 [Azure ExpressRoute][ExpressRoute] 연결을 통해 접근 가능한 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d75-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="c5d75-117">앱 서비스 환경이란?</span><span class="sxs-lookup"><span data-stu-id="c5d75-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="c5d75-118">앱 서비스 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="c5d75-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="c5d75-119">앱 서비스 환경에서 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c5d75-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="c5d75-120">앱 서비스 환경에서 내부 부하 분산 장치 생성 및 사용</span><span class="sxs-lookup"><span data-stu-id="c5d75-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="c5d75-121">앱 서비스 환경 구성</span><span class="sxs-lookup"><span data-stu-id="c5d75-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="c5d75-122">앱 서비스 환경에서 앱 확장</span><span class="sxs-lookup"><span data-stu-id="c5d75-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="c5d75-123">네트워크 보안 및 아키텍처</span><span class="sxs-lookup"><span data-stu-id="c5d75-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="c5d75-124">방법</span><span class="sxs-lookup"><span data-stu-id="c5d75-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="c5d75-125">비디오</span><span class="sxs-lookup"><span data-stu-id="c5d75-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
