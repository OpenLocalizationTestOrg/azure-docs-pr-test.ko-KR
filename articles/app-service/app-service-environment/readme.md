---
title: "Azure App Service Environment 추가 정보"
description: "Azure App Service Environment에 대해 설명하는 설명서를 소개합니다."
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 5b1362854dbc3b0098718bd2ea3cffb06366000c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="4a0f6-103">App Service Environment 설명서</span><span class="sxs-lookup"><span data-stu-id="4a0f6-103">App Service environment documentation</span></span>
 <span data-ttu-id="4a0f6-104">Azure App Service Environment는 Azure App Service 앱을 매우 높은 확장성으로 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공하는 Azure App Service 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="4a0f6-105">이 기능은 [웹앱][webapps], [모바일 앱][mobileapps], [API 앱][APIApps] 및 [함수][Functions]를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="4a0f6-106">ASE(App Service Environment)는 다음을 필요로 하는 응용 프로그램 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="4a0f6-107">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="4a0f6-107">Very high scale.</span></span>
* <span data-ttu-id="4a0f6-108">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="4a0f6-108">Isolation and secure network access.</span></span>

<span data-ttu-id="4a0f6-109">고객은 단일 Azure 지역 내에서, 그리고 여러 Azure 지역에 걸쳐서 여러 ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="4a0f6-110">이처럼 다용도로 활용 가능한 ASE는 대량의 RPS 작업을 지원하는 상태 비저장 응용 프로그램 계층을 수평적으로 크기 조정하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="4a0f6-111">ASE는 단일 고객의 응용 프로그램만을 실행하도록 격리되며 항상 Azure Virtual Network에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-111">ASEs are isolated to running only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="4a0f6-112">고객은 [네트워크 보안 그룹][NSGs]을 사용하여 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽을 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="4a0f6-113">응용 프로그램은 온-프레미스 회사 리소스에 가상 네트워크를 통한 고속 보안 연결을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-113">Applications can also establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="4a0f6-114">앱에서는 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스에 자주 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-114">Apps frequently need to access corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="4a0f6-115">ASE에서 실행되는 앱은 [사이트 간][SiteToSite] VPN 및 [Azure ExpressRoute][ExpressRoute] 연결을 통해 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="4a0f6-116">[App Service Environment란?][Intro]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="4a0f6-117">[App Service Environment 만들기][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="4a0f6-118">[내부 부하 분산 장치 App Service Environment 만들기][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="4a0f6-119">[App Service Environment 사용][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="4a0f6-120">[네트워킹 고려 사항과 App Service Environment][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-120">[Networking considerations and the App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="4a0f6-121">[템플릿에서 App Service Environment 만들기][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="4a0f6-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="4a0f6-122">비디오</span><span class="sxs-lookup"><span data-stu-id="4a0f6-122">Videos</span></span>
<span data-ttu-id="4a0f6-123">Azure App Service를 사용하는 Enterprise에 대한 최신 PaaS 마스터</span><span class="sxs-lookup"><span data-stu-id="4a0f6-123">Master Modern PaaS for the Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="4a0f6-124">확장성이 매우 높으며 안전한 앱 배포</span><span class="sxs-lookup"><span data-stu-id="4a0f6-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="4a0f6-125">Azure App Service에서 Enterprise 웹 및 Mobile Apps 실행</span><span class="sxs-lookup"><span data-stu-id="4a0f6-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="4a0f6-126">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="4a0f6-126">App Service Environment v1</span></span> ##
<span data-ttu-id="4a0f6-127">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="4a0f6-128">ASEv1에 대한 자세한 내용은 [App Service Environment v1 설명서][ASEv1README]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a0f6-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


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
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
