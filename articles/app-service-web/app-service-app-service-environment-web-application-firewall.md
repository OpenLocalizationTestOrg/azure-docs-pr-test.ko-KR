---
title: "앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성"
description: "앱 서비스 환경의 앞에 웹 응용 프로그램 방화벽을 구성하는 방법에 알아봅니다."
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
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="2d51f-103">앱 서비스 환경에 대한 웹 응용 프로그램 방화벽(WAF) 구성</span><span class="sxs-lookup"><span data-stu-id="2d51f-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="2d51f-104">개요</span><span class="sxs-lookup"><span data-stu-id="2d51f-104">Overview</span></span>
<span data-ttu-id="2d51f-105">[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/)에서 사용 가능한 [Azure용 Barracuda WAF](https://www.barracuda.com/programs/azure)와 같은 웹 응용 프로그램 방화벽은 SQL 주입, 교차 사이트 스크립팅, 맬웨어 업로드와 DDos 응용 프로그램 및 다른 공격을 막는 인바운드 웹트래 픽을 검사하여 웹 응용 프로그램 보안을 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="2d51f-106">데이터 손실 방지 DLP (Data Loss Prevention)에 대한 백엔드 웹 서버로부터의 응답도 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="2d51f-107">앱 서비스 환경은 격리와 추가 확장의 조합을 제공합니다. 이 조합은 악의적인 요청과 고용량 트래픽을 견뎌야 하는 호스트 비즈니스 중요한 웹 응용 프로그램에 이상적인 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="2d51f-108">설정</span><span class="sxs-lookup"><span data-stu-id="2d51f-108">Setup</span></span>
<span data-ttu-id="2d51f-109">이 문서에서는 Barracuda WAF의 다중 부하 분산 인스턴스 뒤의 앱 서비스 환경을 구성하여 WAF의 트래픽만이 앱 서비스 환경에 도달할 수 있게 하고 DMZ로부터는 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="2d51f-110">Azure 트래픽 관리자를 Azure 데이터 센터와 지역 간의 작업 부하를 위해 Barracuda WAF 앞에 놓겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="2d51f-111">설치 프로그램의 높은 수준의 다이어그램은 아래와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Architecture][Architecture] 

> <span data-ttu-id="2d51f-113">참고: [App Service 환경에 대한 ILB 지원](app-service-environment-with-internal-load-balancer.md)의 도입으로 DMZ에서 ASE에 액세스할 수 없고 개인 네트워크에만 사용할 수 있도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="2d51f-114">앱 서비스 환경 구성</span><span class="sxs-lookup"><span data-stu-id="2d51f-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="2d51f-115">앱 서비스 환경을 구성하려면 해당 제목의 [설명서](app-service-web-how-to-create-an-app-service-environment.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d51f-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="2d51f-116">App Service Environment를 만들면 [웹앱](app-service-web-overview.md), [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md) 및 [Mobile App](../app-service-mobile/app-service-mobile-value-prop.md)을 다음에 섹션에서 구성할 WAF로 모두 보호 받는 환경에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="2d51f-117">Barracuda WAF 클라우드 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="2d51f-118">Barracuda에는 Azure의 가상 컴퓨터에 WAF를 배포하는 방법에 대한 [자세한 문서](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) 가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="2d51f-119">이 설명서를 따라할 때 중복성을 원하고 단일 실패 지점을 도입하지 않는 것뿐만 아니라, 동일한 클라우드 서비스 안에 최소 2개의 WAF 인스턴스 VM을 배포하는 것을 원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="2d51f-120">클라우드 서비스에 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="2d51f-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="2d51f-121">클라우드 서비스 내에 2개 이상의 WAF VM이 있다면 [Azure 포털](https://portal.azure.com/) 을 사용하여 아래의 이미지처럼 응용 프로그램에서 사용하는 HTTP와 HTTPS 끝점을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![끝점 구성][ConfigureEndpoint]

<span data-ttu-id="2d51f-123">응용 프로그램에서 다른 끝점을 사용하는 경우 이 목록에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="2d51f-124">해당 관리 포털을 통해 WAF Barracuda 구성</span><span class="sxs-lookup"><span data-stu-id="2d51f-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="2d51f-125">해당 관리 포털을 통해 Barracuda WAF를 사용하여 TCP Port 8000에 대해 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="2d51f-126">WAF VM의 여러 인스턴스가 있기 때문에 각 VM에 이 단계를 반복해서 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="2d51f-127">참고: WAF 구성이 끝났다면, WAF 보안을 유지하기 위해 모든 WAF VM에서 TCP/8000 끝점을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="2d51f-128">아래의 그림처럼 관리 끝점을 추가하여 Barracuda WAF를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![관리 끝점 추가][AddManagementEndpoint]

<span data-ttu-id="2d51f-130">브라우저를 사용하여 클라우드 서비스에서 관리 끝점으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="2d51f-131">클라우드 서비스 이름이 test.cloudapp.net 이라면 http://test.cloudapp.net:8000 로 이동하여 이 끝점에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="2d51f-132">로그인 페이지를 참조해야 아래와 같은 WAF VM 설치 단계에서 지정한 자격 증명을 사용하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![관리 로그인 페이지][ManagementLoginPage]

<span data-ttu-id="2d51f-134">로그인 하면 아래 그림 안의 1처럼 대시보드를 참조해야 WAF 보호에 관한 기본 통계를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![관리 대시보드][ManagementDashboard]

<span data-ttu-id="2d51f-136">서비스 탭을 클릭하여 WAF가 보호하는 서비스에 대해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="2d51f-137">Barracuda WAF를 구성하는 방법에 대한 자세한 내용은 [해당 설명서](https://techlib.barracuda.com/waf/getstarted1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d51f-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="2d51f-138">아래 예제는 Azure 웹앱이 구성된 HTTP 및 HTTPS로 트래픽을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![관리 서비스를 추가 합니다.][ManagementAddServices]

> <span data-ttu-id="2d51f-140">참고: 응용 프로그램이 어떻게 구성되었는지, 앱 서비스 환경에서 어떤 기능들이 쓰이고 있는지에 따라서 트래픽을 80 및 443이 아닌 TCP 포트로 전달해야 합니다(예: 웹앱에 대한 IP SSL을 설치한 경우).</span><span class="sxs-lookup"><span data-stu-id="2d51f-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="2d51f-141">앱 서비스 환경에서 사용되는 네트워크 포트의 목록은 [인바운드 트래픽을 제어 설명서](app-service-app-service-environment-control-inbound-traffic.md) 의 네트워크 포트 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d51f-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="2d51f-142">Microsoft Azure 트래픽 관리자를 구성합니다. (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="2d51f-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="2d51f-143">응용 프로그램이 여러 지역에서 사용할 수 있는 경우, [Azure 트래픽 관리자](../traffic-manager/traffic-manager-overview.md)를 사용하여 부하 분산하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="2d51f-144">이 작업을 수행하려면 아래 그림처럼 트래픽 관리자 프로필의 WAF 클라우드 서비스 이름을 이용하여 [Azure 클래식 포털](https://manage.azure.com) 에서 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![트래픽 관리자 끝점][TrafficManagerEndpoint]

<span data-ttu-id="2d51f-146">응용 프로그램에 대해 인증이 필요한 경우, 응용 프로그램의 가용성에 대해 ping하는 트리팩 관리자에 대한 어떤 자격 증명도 필요하지 않는 리소스가 남아 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="2d51f-147">아래 그림처럼 [Azure 클래식 포털](https://manage.azure.com) 의 구성 섹션에서 URL을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![트래픽 관리자를 구성하는 방법][ConfigureTrafficManager]

<span data-ttu-id="2d51f-149">아래의 예가 보여주는 것처럼 WAF에서 응용 프로그램으로 트래픽 관리자 Ping을 전송하려면, 웹 사이트 번역을 Barracuda WAF에 설치하여 트래픽을 응용 프로그램으로 전송하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![웹사이트 번역][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="2d51f-151">NSG(네트워크 보안 그룹)을 사용하여 앱 서비스 환경에 대한 트래픽 보안</span><span class="sxs-lookup"><span data-stu-id="2d51f-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="2d51f-152">클라우드 서비스의 VIP 주소만 사용하여 WAF에서 앱 서비스 환경으로 들어오는 트래픽을 제한하는 방법에 대한 자세한 내용은 [인바운드 트래픽 제어 설명서](app-service-app-service-environment-control-inbound-traffic.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2d51f-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="2d51f-153">TCP 포트 80에 대한 작업을 수행 하기 위한 샘플 Powershell 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="2d51f-154">프로그램 WAF 클라우드 서비스의 가상 IP 주소 (VIP)는 SourceAddres Prefix를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="2d51f-155">참고: 클라우드 서비스의 VIP는 클라우드 서비스를 삭제하고 다시  만들 때 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="2d51f-156">이렇게 하면 네트워크 리소스 그룹의 IP 주소를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d51f-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
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
