---
title: "Azure App Service Environment 소개"
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
ms.openlocfilehash: e21c4c3e2c212d86a0dbe2211564c2e3a1acf819
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environments"></a><span data-ttu-id="47256-103">App Service Environment 소개</span><span class="sxs-lookup"><span data-stu-id="47256-103">Introduction to App Service environments</span></span> #
 
## <a name="overview"></a><span data-ttu-id="47256-104">개요</span><span class="sxs-lookup"><span data-stu-id="47256-104">Overview</span></span> ##

<span data-ttu-id="47256-105">Azure App Service Environment는 App Service 앱을 매우 높은 확장성으로 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공하는 Azure App Service 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-105">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="47256-106">이 기능은 [웹앱][webapps], [모바일 앱][mobileapps], [API 앱][APIapps] 및 [함수][Functions]를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-106">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIapps], and [functions][Functions].</span></span>

<span data-ttu-id="47256-107">ASE(App Service Environment)는 다음을 필요로 하는 응용 프로그램 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-107">App Service environments (ASEs) are appropriate for application workloads that require:</span></span>

- <span data-ttu-id="47256-108">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="47256-108">Very high scale.</span></span>
- <span data-ttu-id="47256-109">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="47256-109">Isolation and secure network access.</span></span>
- <span data-ttu-id="47256-110">높은 메모리 사용률</span><span class="sxs-lookup"><span data-stu-id="47256-110">High memory utilization.</span></span>

<span data-ttu-id="47256-111">고객은 단일 Azure 지역 내 또는 여러 Azure 지역에 걸쳐서 여러 ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-111">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span></span> <span data-ttu-id="47256-112">따라서 ASE는 높은 RPS 워크로드를 지원하여 상태 비저장 응용 프로그램 계층을 수평적으로 크기 조정하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-112">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="47256-113">ASE는 단일 고객의 응용 프로그램만을 실행하도록 격리되며 항상 가상 네트워크에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-113">ASEs are isolated to running only a single customer's applications and are always deployed into a virtual network.</span></span> <span data-ttu-id="47256-114">고객은 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽을 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-114">Customers have fine-grained control over inbound and outbound application network traffic.</span></span> <span data-ttu-id="47256-115">응용 프로그램은 온-프레미스 회사 리소스에 VPN을 통한 고속 보안 연결을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-115">Applications can establish high-speed secure connections over VPNs to on-premises corporate resources.</span></span>

<span data-ttu-id="47256-116">ASE에 대한 모든 문서와 지침은 [App Service Environment의 추가 정보][ASEReadme]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-116">All articles and how-to instructions about ASEs are available in the [README for App Service environments][ASEReadme]:</span></span>

* <span data-ttu-id="47256-117">ASE를 통해 보안 네트워크 액세스 권한이 있는 확장성이 뛰어난 앱 호스팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-117">ASEs enable high-scale app hosting with secure network access.</span></span> <span data-ttu-id="47256-118">자세한 내용은 ASE의 [AzureCon 심층 분석](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-118">For more information, see the [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) on ASEs.</span></span>
* <span data-ttu-id="47256-119">여러 ASE를 수평적 크기 조정에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-119">Multiple ASEs can be used to scale horizontally.</span></span> <span data-ttu-id="47256-120">자세한 내용은 [지리적으로 분산된 앱 설치 공간 설정 방법](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-120">For more information, see [how to set up a geo-distributed app footprint](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).</span></span>
* <span data-ttu-id="47256-121">AzureCon 심층 분석에 표시된 대로 ASE는 보안 아키텍처를 구성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-121">ASEs can be used to configure security architecture, as shown in the AzureCon Deep Dive.</span></span> <span data-ttu-id="47256-122">AzureCon 심층 분석에 표시된 보안 아키텍처가 어떻게 구성되었는지 확인하려면 App Service Environment를 사용하여 [계층화된 보안 아키텍처를 구현하는 방법에 대한 문서](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-122">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the [article on how to implement a layered security architecture](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) with App Service environments.</span></span>
* <span data-ttu-id="47256-123">ASE에서 실행 중인 앱은 WAF(웹 응용 프로그램 방화벽) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-123">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span></span> <span data-ttu-id="47256-124">자세한 내용은 [App Service Environment에 대한 WAF 구성](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-124">For more information, see [Configure a WAF for App Service environments](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).</span></span>

## <a name="dedicated-environment"></a><span data-ttu-id="47256-125">전용 환경</span><span class="sxs-lookup"><span data-stu-id="47256-125">Dedicated environment</span></span> ##

<span data-ttu-id="47256-126">ASE는 단일 구독에 단독으로 전용되어 100개 인스턴스를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-126">An ASE is dedicated exclusively to a single subscription and can host 100 instances.</span></span> <span data-ttu-id="47256-127">단일 App Service 계획의 100개 인스턴스부터 100개의 단일 인스턴스 App Service 계획까지 가능하며 모든 항목은 이 두 계획 사이에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-127">The range can span 100 instances in a single App Service plan to 100 single-instance App Service plans, and everything in between.</span></span>

<span data-ttu-id="47256-128">ASE는 프런트 엔드 및 작업자로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-128">An ASE is composed of front ends and workers.</span></span> <span data-ttu-id="47256-129">프런트 엔드는 ASE 내의 앱 요청에 대한 자동 부하 분산 및 HTTP/HTTPS 종료를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-129">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span></span> <span data-ttu-id="47256-130">프런트 엔드는 ASE의 App Service 계획이 스케일 아웃됨에 따라 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-130">Front ends are automatically added as the App Service plans in the ASE are scaled out.</span></span>

<span data-ttu-id="47256-131">작업자는 고객 앱을 호스트하는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-131">Workers are roles that host customer apps.</span></span> <span data-ttu-id="47256-132">작업자는 3가지 고정된 크기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-132">Workers are available in three fixed sizes:</span></span>

* <span data-ttu-id="47256-133">1 코어/3.5GB RAM</span><span class="sxs-lookup"><span data-stu-id="47256-133">One core/3.5 GB RAM</span></span>
* <span data-ttu-id="47256-134">2 코어/7GB RAM</span><span class="sxs-lookup"><span data-stu-id="47256-134">Two core/7 GB RAM</span></span>
* <span data-ttu-id="47256-135">4 코어/14GB RAM</span><span class="sxs-lookup"><span data-stu-id="47256-135">Four core/14 GB RAM</span></span>

<span data-ttu-id="47256-136">고객은 프런트 엔드와 작업자를 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-136">Customers do not need to manage front ends and workers.</span></span> <span data-ttu-id="47256-137">모든 인프라는 고객이 App Service 계획을 스케일 아웃함에 따라 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-137">All infrastructure is automatically added as customers scale out their App Service plans.</span></span> <span data-ttu-id="47256-138">ASE에서 App Service 계획을 생성하거나 규모를 변경함에 따라 필요한 인프라가 적절하게 추가되거나 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-138">As App Service plans are created or scaled in an ASE, the required infrastructure is added or removed as appropriate.</span></span>

<span data-ttu-id="47256-139">인프라에 대해 대금을 지급하고 ASE 크기에 따라 변경되지 않는 ASE의 월정액이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-139">There is a flat monthly rate for an ASE that pays for the infrastructure and doesn't change with the size of the ASE.</span></span> <span data-ttu-id="47256-140">거기에 App Service 계획 코어당 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-140">In addition, there is a cost per App Service plan core.</span></span> <span data-ttu-id="47256-141">ASE에 호스트되는 모든 앱은 격리 가격 책정 SKU에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-141">All apps hosted in an ASE are in the Isolated pricing SKU.</span></span> <span data-ttu-id="47256-142">ASE에 대한 가격 책정에 대한 정보는 [App Service 가격 책정][Pricing] 페이지를 참조하고 ASE에 대한 사용 가능한 옵션을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-142">For information on pricing for an ASE, see the [App Service pricing][Pricing] page and review the available options for ASEs.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="47256-143">가상 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="47256-143">Virtual network support</span></span> ##

<span data-ttu-id="47256-144">ASE는 Azure Resource Manager 가상 네트워크에서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-144">An ASE can be created only in an Azure Resource Manager virtual network.</span></span> <span data-ttu-id="47256-145">Azure 가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-145">To learn more about Azure virtual networks, see the [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span></span> <span data-ttu-id="47256-146">ASE는 항상 가상 네트워크 내 존재하며, 더 정확하게는 가상 네트워크의 서브넷 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-146">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span></span> <span data-ttu-id="47256-147">가상 네트워크의 보안 기능을 사용하여 앱에 대한 인바운드 및 아웃바운드 네트워크 통신을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-147">You can use the security features of virtual networks to control inbound and outbound network communications for your apps.</span></span>

<span data-ttu-id="47256-148">ASE는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-148">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span></span>

<span data-ttu-id="47256-149">[네트워크 보안 그룹][NSGs]은 ASE가 있는 서브넷에 대한 인바운드 네트워크 통신을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-149">[Network Security Groups][NSGs] restrict inbound network communications to the subnet where an ASE resides.</span></span> <span data-ttu-id="47256-150">NSG를 사용하여 WAF 및 네트워크 SaaS 공급자와 같은 업스트림 장치 및 서비스 뒤에서 앱을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-150">You can use NSGs to run apps behind upstream devices and services such as WAFs and network SaaS providers.</span></span>

<span data-ttu-id="47256-151">또한 앱에서는 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스에 자주 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-151">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span> <span data-ttu-id="47256-152">온-프레미스 네트워크에 VPN이 연결되어 있는 가상 네트워크에 ASE를 배포하는 경우 ASE의 앱은 온-프레미스 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-152">If you deploy the ASE in a virtual network that has a VPN connection to the on-premises network, the apps in the ASE can access the on-premises resources.</span></span> <span data-ttu-id="47256-153">이 기능은 VPN이 [사이트 간](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/)이든 [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN이든 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-153">This capability is true regardless of whether the VPN is a [site-to-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span></span>

<span data-ttu-id="47256-154">ASE가 가상 네트워크 및 온-프레미스 네트워크와 함께 어떻게 작동하는지에 대한 자세한 내용은 [App Service Environment 네트워크 고려 사항][ASENetwork]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-154">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="47256-155">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="47256-155">App Service Environment v1</span></span> ##

<span data-ttu-id="47256-156">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47256-156">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="47256-157">위의 정보는 ASEv2를 기준으로 작성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-157">The preceding information was based on ASEv2.</span></span> <span data-ttu-id="47256-158">이 섹션은 ASEv1과 ASEv2의 차이를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="47256-158">This section shows you the differences between ASEv1 and ASEv2.</span></span> 

<span data-ttu-id="47256-159">ASEv1에서는 모든 리소스를 수동으로 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-159">In ASEv1, you need to manage all of the resources manually.</span></span> <span data-ttu-id="47256-160">여기에는 IP 기반 SSL에 사용된 프런트 엔드, 작업자 및 IP 주소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-160">That includes the front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="47256-161">App Service 계획을 스케일 아웃하기 전에 호스트할 작업자 풀을 먼저 스케일 아웃해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-161">Before you can scale out your App Service plan, you need to first scale out the worker pool where you want to host it.</span></span>

<span data-ttu-id="47256-162">ASEv1은 ASEv2와는 다른 가격 책정 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-162">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="47256-163">ASEv1에서는 할당된 각 코어에 대한 비용을 지불해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47256-163">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="47256-164">여기에는 워크로드를 호스트하지 않는 프런트 엔드 또는 작업자에 사용된 코어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-164">That includes cores used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="47256-165">ASEv1에서 ASE의 기본 최대 규모 크기는 총 55개의 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-165">In ASEv1, the default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="47256-166">여기에는 작업자 및 프런트 엔드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="47256-166">That includes workers and front ends.</span></span> <span data-ttu-id="47256-167">ASEv1의 한 가지 장점은 클래식 가상 네트워크 및 Resource Manager 가상 네트워크에 배포할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="47256-167">One advantage to ASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="47256-168">ASEv1에 대해 자세히 알아보려면 [App Service Environment v1 소개][ASEv1Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47256-168">To learn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

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
