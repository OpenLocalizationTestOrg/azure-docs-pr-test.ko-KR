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
# <a name="introduction-tooapp-service-environments"></a><span data-ttu-id="4e952-103">소개 tooApp 서비스 환경</span><span class="sxs-lookup"><span data-stu-id="4e952-103">Introduction tooApp Service environments</span></span> #
 
## <a name="overview"></a><span data-ttu-id="4e952-104">개요</span><span class="sxs-lookup"><span data-stu-id="4e952-104">Overview</span></span> ##

<span data-ttu-id="4e952-105">Azure App Service Environment는 App Service 앱을 매우 높은 확장성으로 안전하게 실행하기 위해 완전히 격리된 전용 환경을 제공하는 Azure App Service 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-105">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="4e952-106">이 기능은 [웹앱][webapps], [모바일 앱][mobileapps], [API 앱][APIapps] 및 [함수][Functions]를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-106">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIapps], and [functions][Functions].</span></span>

<span data-ttu-id="4e952-107">ASE(App Service Environment)는 다음을 필요로 하는 응용 프로그램 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-107">App Service environments (ASEs) are appropriate for application workloads that require:</span></span>

- <span data-ttu-id="4e952-108">매우 높은 확장성</span><span class="sxs-lookup"><span data-stu-id="4e952-108">Very high scale.</span></span>
- <span data-ttu-id="4e952-109">격리 및 보안된 네트워크 액세스</span><span class="sxs-lookup"><span data-stu-id="4e952-109">Isolation and secure network access.</span></span>
- <span data-ttu-id="4e952-110">높은 메모리 사용률</span><span class="sxs-lookup"><span data-stu-id="4e952-110">High memory utilization.</span></span>

<span data-ttu-id="4e952-111">고객은 단일 Azure 지역 내 또는 여러 Azure 지역에 걸쳐서 여러 ASE를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-111">Customers can create multiple ASEs within a single Azure region or across multiple Azure regions.</span></span> <span data-ttu-id="4e952-112">따라서 ASE는 높은 RPS 워크로드를 지원하여 상태 비저장 응용 프로그램 계층을 수평적으로 크기 조정하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-112">This flexibility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="4e952-113">ASEs toorunning 격리 된 응용 프로그램에 단일 고객의만 되며 가상 네트워크에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-113">ASEs are isolated toorunning only a single customer's applications and are always deployed into a virtual network.</span></span> <span data-ttu-id="4e952-114">고객은 인바운드 및 아웃바운드 응용 프로그램 네트워크 트래픽을 세부적으로 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-114">Customers have fine-grained control over inbound and outbound application network traffic.</span></span> <span data-ttu-id="4e952-115">응용 프로그램 Vpn tooon 온-프레미스 회사 리소스에 대해 고속 보안 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-115">Applications can establish high-speed secure connections over VPNs tooon-premises corporate resources.</span></span>

<span data-ttu-id="4e952-116">Hello에서 사용할 수 있는 모든 문서 및 ASEs에 대 한 방법 tooinstructions [앱 서비스 환경에 대 한 추가 정보][ASEReadme]:</span><span class="sxs-lookup"><span data-stu-id="4e952-116">All articles and how-tooinstructions about ASEs are available in hello [README for App Service environments][ASEReadme]:</span></span>

* <span data-ttu-id="4e952-117">ASE를 통해 보안 네트워크 액세스 권한이 있는 확장성이 뛰어난 앱 호스팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-117">ASEs enable high-scale app hosting with secure network access.</span></span> <span data-ttu-id="4e952-118">자세한 내용은 참조 hello [AzureCon 심층 분석](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) ASEs에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-118">For more information, see hello [AzureCon Deep Dive](https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/) on ASEs.</span></span>
* <span data-ttu-id="4e952-119">여러 ASEs 사용된 tooscale를 가로로 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-119">Multiple ASEs can be used tooscale horizontally.</span></span> <span data-ttu-id="4e952-120">자세한 내용은 참조 [어떻게 지리적으로 분산 응용 프로그램 공간만 사용 tooset](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-120">For more information, see [how tooset up a geo-distributed app footprint](https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/).</span></span>
* <span data-ttu-id="4e952-121">ASEs는 hello AzureCon 심층 분석에에서 나와 있는 것 처럼 사용 되는 tooconfigure 보안 아키텍처를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-121">ASEs can be used tooconfigure security architecture, as shown in hello AzureCon Deep Dive.</span></span> <span data-ttu-id="4e952-122">hello AzureCon 심층 분석에에서 표시 된 hello 보안 아키텍처 구성 방법 toosee 참조 hello [방법에 대 한 문서 tooimplement 계층화 된 보안 아키텍처](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) 앱 서비스 환경을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-122">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello [article on how tooimplement a layered security architecture](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-layered-security) with App Service environments.</span></span>
* <span data-ttu-id="4e952-123">ASE에서 실행 중인 앱은 WAF(웹 응용 프로그램 방화벽) 등의 업스트림 장치에서 제어된 액세스를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-123">Apps running on ASEs can have their access gated by upstream devices, such as web application firewalls (WAFs).</span></span> <span data-ttu-id="4e952-124">자세한 내용은 [App Service Environment에 대한 WAF 구성](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e952-124">For more information, see [Configure a WAF for App Service environments](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-app-service-environment-web-application-firewall).</span></span>

## <a name="dedicated-environment"></a><span data-ttu-id="4e952-125">전용 환경</span><span class="sxs-lookup"><span data-stu-id="4e952-125">Dedicated environment</span></span> ##

<span data-ttu-id="4e952-126">ASE는 단독으로 tooa 단일 구독 전용 및 인스턴스 수가 100을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-126">An ASE is dedicated exclusively tooa single subscription and can host 100 instances.</span></span> <span data-ttu-id="4e952-127">hello 범위는 단일 앱 서비스 계획 too100 단일 인스턴스 응용 프로그램 서비스 계획 및 사이 있는 모든 항목에 인스턴스 수가 100을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-127">hello range can span 100 instances in a single App Service plan too100 single-instance App Service plans, and everything in between.</span></span>

<span data-ttu-id="4e952-128">ASE는 프런트 엔드 및 작업자로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-128">An ASE is composed of front ends and workers.</span></span> <span data-ttu-id="4e952-129">프런트 엔드는 ASE 내의 앱 요청에 대한 자동 부하 분산 및 HTTP/HTTPS 종료를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-129">Front ends are responsible for HTTP/HTTPS termination and automatic load balancing of app requests within an ASE.</span></span> <span data-ttu-id="4e952-130">프런트 엔드 hello ASE에 앱 서비스 계획 하 여 확장 되어 hello로 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-130">Front ends are automatically added as hello App Service plans in hello ASE are scaled out.</span></span>

<span data-ttu-id="4e952-131">작업자는 고객 앱을 호스트하는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-131">Workers are roles that host customer apps.</span></span> <span data-ttu-id="4e952-132">작업자는 3가지 고정된 크기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-132">Workers are available in three fixed sizes:</span></span>

* <span data-ttu-id="4e952-133">1 코어/3.5GB RAM</span><span class="sxs-lookup"><span data-stu-id="4e952-133">One core/3.5 GB RAM</span></span>
* <span data-ttu-id="4e952-134">2 코어/7GB RAM</span><span class="sxs-lookup"><span data-stu-id="4e952-134">Two core/7 GB RAM</span></span>
* <span data-ttu-id="4e952-135">4 코어/14GB RAM</span><span class="sxs-lookup"><span data-stu-id="4e952-135">Four core/14 GB RAM</span></span>

<span data-ttu-id="4e952-136">고객은 toomanage 프런트 엔드 및 작업 자가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-136">Customers do not need toomanage front ends and workers.</span></span> <span data-ttu-id="4e952-137">모든 인프라는 고객이 App Service 계획을 스케일 아웃함에 따라 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-137">All infrastructure is automatically added as customers scale out their App Service plans.</span></span> <span data-ttu-id="4e952-138">앱 서비스 계획 생성 되거나 ASE에 수평으로 hello 인프라 추가 또는 제거를 적절 하 게 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-138">As App Service plans are created or scaled in an ASE, hello required infrastructure is added or removed as appropriate.</span></span>

<span data-ttu-id="4e952-139">편평한 월정액 hello 인프라에 대 한 대금을 지급 한다는 및 hello ASE hello 크기가 변경 되지 않습니다는 ASE에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-139">There is a flat monthly rate for an ASE that pays for hello infrastructure and doesn't change with hello size of hello ASE.</span></span> <span data-ttu-id="4e952-140">거기에 App Service 계획 코어당 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-140">In addition, there is a cost per App Service plan core.</span></span> <span data-ttu-id="4e952-141">Hello에 ASE에 호스트 되는 모든 앱은 SKU 가격을 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-141">All apps hosted in an ASE are in hello Isolated pricing SKU.</span></span> <span data-ttu-id="4e952-142">ASE에 대 한 가격 책정에 대 한 내용은 hello 참조 [앱 서비스 가격 책정] [ Pricing] 페이지 및 hello ASEs에 대 한 사용 가능한 옵션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-142">For information on pricing for an ASE, see hello [App Service pricing][Pricing] page and review hello available options for ASEs.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="4e952-143">가상 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="4e952-143">Virtual network support</span></span> ##

<span data-ttu-id="4e952-144">ASE는 Azure Resource Manager 가상 네트워크에서만 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-144">An ASE can be created only in an Azure Resource Manager virtual network.</span></span> <span data-ttu-id="4e952-145">Azure 가상 네트워크에 대해 자세히 toolearn 참조 hello [Azure 가상 네트워크 FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-145">toolearn more about Azure virtual networks, see hello [Azure virtual networks FAQ](https://azure.microsoft.com/documentation/articles/virtual-networks-faq/).</span></span> <span data-ttu-id="4e952-146">ASE는 항상 가상 네트워크 내 존재하며, 더 정확하게는 가상 네트워크의 서브넷 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-146">An ASE always exists in a virtual network, and more precisely, within a subnet of a virtual network.</span></span> <span data-ttu-id="4e952-147">가상 네트워크 toocontrol 인바운드 및 아웃 바운드의 hello 보안 기능을 사용 하려면 앱에 대 한 통신 네트워크.</span><span class="sxs-lookup"><span data-stu-id="4e952-147">You can use hello security features of virtual networks toocontrol inbound and outbound network communications for your apps.</span></span>

<span data-ttu-id="4e952-148">ASE는 공개 IP 주소가 있는 인터넷 연결이거나 Azure ILB(내부 부하 분산 장치) 주소만 있는 내부 연결일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-148">An ASE can be either internet-facing with a public IP address or internal-facing with only an Azure internal load balancer (ILB) address.</span></span>

<span data-ttu-id="4e952-149">[네트워크 보안 그룹] [ NSGs] ASE 있는 인바운드 네트워크 통신 toohello 서브넷을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-149">[Network Security Groups][NSGs] restrict inbound network communications toohello subnet where an ASE resides.</span></span> <span data-ttu-id="4e952-150">업스트림 장치 및 WAFs 및 네트워크 SaaS 공급자와 같은 서비스의 데이터로 Nsg toorun 앱을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-150">You can use NSGs toorun apps behind upstream devices and services such as WAFs and network SaaS providers.</span></span>

<span data-ttu-id="4e952-151">앱은 tooaccess 내부 데이터베이스 및 웹 서비스와 같은 회사 리소스를 자주 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-151">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span> <span data-ttu-id="4e952-152">VPN 연결 toohello 온-프레미스 네트워크에 있는 가상 네트워크의 hello ASE를 배포 하는 경우 hello ASE에에서 hello 앱 hello 온-프레미스 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-152">If you deploy hello ASE in a virtual network that has a VPN connection toohello on-premises network, hello apps in hello ASE can access hello on-premises resources.</span></span> <span data-ttu-id="4e952-153">이 기능은 hello VPN 인지에 관계 없이 true는 [사이트 간](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) 또는 [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span><span class="sxs-lookup"><span data-stu-id="4e952-153">This capability is true regardless of whether hello VPN is a [site-to-site](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/) or [Azure ExpressRoute](http://azure.microsoft.com/services/expressroute/) VPN.</span></span>

<span data-ttu-id="4e952-154">ASE가 가상 네트워크 및 온-프레미스 네트워크와 함께 어떻게 작동하는지에 대한 자세한 내용은 [App Service Environment 네트워크 고려 사항][ASENetwork]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e952-154">For more information on how ASEs work with virtual networks and on-premises networks, see [App Service Environment network considerations][ASENetwork].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="4e952-155">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="4e952-155">App Service Environment v1</span></span> ##

<span data-ttu-id="4e952-156">App Service Environment에는 두 가지 버전(ASEv1 및 ASEv2)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-156">App Service Environment has two versions: ASEv1 and ASEv2.</span></span> <span data-ttu-id="4e952-157">앞에 정보 hello ASEv2 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-157">hello preceding information was based on ASEv2.</span></span> <span data-ttu-id="4e952-158">이 섹션 ASEv1와 ASEv2 차이점 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-158">This section shows you hello differences between ASEv1 and ASEv2.</span></span> 

<span data-ttu-id="4e952-159">Toomanage ASEv1에 필요한 리소스를 수동으로 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-159">In ASEv1, you need toomanage all of hello resources manually.</span></span> <span data-ttu-id="4e952-160">Hello 프런트 엔드, 작업자 및 IP 기반 SSL에 사용 되는 IP 주소를 포함 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-160">That includes hello front ends, workers, and IP addresses used for IP-based SSL.</span></span> <span data-ttu-id="4e952-161">앱 서비스 계획을 확장할 수 있습니다, 먼저 toofirst toohost 원하는 hello 작업자 풀 아웃 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-161">Before you can scale out your App Service plan, you need toofirst scale out hello worker pool where you want toohost it.</span></span>

<span data-ttu-id="4e952-162">ASEv1은 ASEv2와는 다른 가격 책정 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-162">ASEv1 uses a different pricing model from ASEv2.</span></span> <span data-ttu-id="4e952-163">ASEv1에서는 할당된 각 코어에 대한 비용을 지불해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-163">In ASEv1, you pay for each core allocated.</span></span> <span data-ttu-id="4e952-164">여기에는 워크로드를 호스트하지 않는 프런트 엔드 또는 작업자에 사용된 코어가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-164">That includes cores used for front ends or workers that aren't hosting any workloads.</span></span> <span data-ttu-id="4e952-165">ASEv1에서 hello 기본 최대 규모의 ASE 크기가 55 총 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-165">In ASEv1, hello default maximum-scale size of an ASE is 55 total hosts.</span></span> <span data-ttu-id="4e952-166">여기에는 작업자 및 프런트 엔드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-166">That includes workers and front ends.</span></span> <span data-ttu-id="4e952-167">한 이점은 tooASEv1은 클래식 가상 네트워크와 리소스 관리자 가상 네트워크에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-167">One advantage tooASEv1 is that it can be deployed in a classic virtual network and a Resource Manager virtual network.</span></span> <span data-ttu-id="4e952-168">toolearn ASEv1에 대 한 자세한 참조 [앱 서비스 환경 v1 소개][ASEv1Intro]합니다.</span><span class="sxs-lookup"><span data-stu-id="4e952-168">toolearn more about ASEv1, see [App Service Environment v1 introduction][ASEv1Intro].</span></span>

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
