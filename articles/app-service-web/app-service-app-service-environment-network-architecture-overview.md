---
title: "앱 서비스 환경의 네트워크 아키텍처 개요"
description: "앱 서비스 환경의 네트워크 토폴로지의 아키텍처 개요입니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 13d03a37-1fe2-4e3e-9d57-46dfb330ba52
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: b2afe86d8774b449a257312d4e60b5f6125336ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="network-architecture-overview-of-app-service-environments"></a><span data-ttu-id="ced83-103">앱 서비스 환경의 네트워크 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="ced83-103">Network Architecture Overview of App Service Environments</span></span>
## <a name="introduction"></a><span data-ttu-id="ced83-104">소개</span><span class="sxs-lookup"><span data-stu-id="ced83-104">Introduction</span></span>
<span data-ttu-id="ced83-105">App Service 환경은 [가상 네트워크][virtualnetwork]의 서브넷에서 항상 만들어지고, App Service 환경에서 실행되는 앱은 동일한 가상 네트워크 토폴로지 내에 위치한 개인 끝점과 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-105">App Service Environments are always created within a subnet of a [virtual network][virtualnetwork] - apps running in an App Service Environment can communicate with private endpoints located within the same virtual network topology.</span></span>  <span data-ttu-id="ced83-106">고객은 그들의 가상 네트워크 일부를 잠글 수 있기 때문에 앱 서비스 환경에서 일어나는 네트워크 통신 흐름의 유형을 이해하는 것은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-106">Since customers may lock down parts of their virtual network infrastructure, it is important to understand the types of network communication flows that occur with an App Service Environment.</span></span>

## <a name="general-network-flow"></a><span data-ttu-id="ced83-107">일반 네트워크 흐름</span><span class="sxs-lookup"><span data-stu-id="ced83-107">General Network Flow</span></span>
<span data-ttu-id="ced83-108">ASE(앱 서비스 환경)가 앱에 공용 VIP(가상 IP 주소)를 사용하는 경우 모든 인바운드 트래픽이 해당 공용 VIP에 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-108">When an App Service Environment (ASE) uses a public virtual IP address (VIP) for apps, all inbound traffic arrives on that public VIP.</span></span>  <span data-ttu-id="ced83-109">여기에는 FTP에 대한 다른 트래픽, 원격 디버깅 기능, Azure 관리 작업과 마찬가지로 앱의 HTTP와 HTTPS 트래픽이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-109">This includes HTTP and HTTPS traffic for apps, as well as other traffic for FTP, remote debugging functionality, and Azure management operations.</span></span>  <span data-ttu-id="ced83-110">공용 VIP에서 사용할 수 있는 특정 포트(필수 및 선택적)의 전체 목록은 App Service 환경의 [인바운드 트래픽 제어][controllinginboundtraffic] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ced83-110">For a full list of the specific ports (both required and optional) that are available on the public VIP see the article on [controlling inbound traffic][controllinginboundtraffic] to an App Service Environment.</span></span> 

<span data-ttu-id="ced83-111">또한 앱 서비스 환경은 ILB(내부 부하 분산 장치) 주소라고도 하는 가상 네트워크 내부 주소에만 바인딩되는 앱 실행을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-111">App Service Environments also support running apps that are bound only to a virtual network internal address, also referred to as an ILB (internal load balancer) address.</span></span>  <span data-ttu-id="ced83-112">ILB 지원 ASE에서 앱에 대한 HTTP 및 HTTPS 트래픽과 원격 디버깅 호출은 ILB 주소에 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-112">On an ILB enabled ASE, HTTP and HTTPS traffic for apps as well as remote debugging calls, arrive on the ILB address.</span></span>  <span data-ttu-id="ced83-113">가장 일반적인 ILB-ASE 구성에서는 FTP/FTPS 트래픽도 ILB 주소에 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-113">For most common ILB-ASE configurations, FTP/FTPS traffic will also arrive on the ILB address.</span></span>  <span data-ttu-id="ced83-114">그러나 Azure 관리 작업은 여전히 ILB 지원 ASE의 공용 VIP에 있는 포트 454/455로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-114">However Azure management operations will still flow to ports 454/455 on the public VIP of an ILB enabled ASE.</span></span>

<span data-ttu-id="ced83-115">아래 다이어그램은 앱이 공용 가상 IP 주소에 바인딩되는 앱 서비스 환경에 대한 다양한 인바운드 및 아웃바운드 네트워크 흐름을 대략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-115">The diagram below shows an overview of the various inbound and outbound network flows for an App Service Environment where the apps are bound to a public virtual IP address:</span></span>

![일반 네트워크 흐름][GeneralNetworkFlows]

<span data-ttu-id="ced83-117">앱 서비스 환경은 다양한 개인 고객 끝점과 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-117">An App Service Environment can communicate with a variety of private customer endpoints.</span></span>  <span data-ttu-id="ced83-118">예를들어, 앱 서비스 환경에서 실행 중인 앱은 동일한 가상 네트워크 토폴로지 안의 Iaas 가상 컴퓨터에서 실행되는 데이터베이스 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-118">For example, apps running in the App Service Environment can connect to database server(s) running on IaaS virtual machines in the same virtual network topology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ced83-119">네트워크 다이어그램을 보면 "다른 컴퓨터 리소스"는 앱 서비스 환경에서 다른 서브넷에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-119">Looking at the network diagram, the "Other Compute Resources" are deployed in a different Subnet from the App Service Environment.</span></span> <span data-ttu-id="ced83-120">ASE와 동일한 서브넷에 리소스를 배포하면 (특정 ASE 내 라우팅을 제외하고) ASE에서 해당 리소스로 연결을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-120">Deploying resources in the same Subnet with the ASE will block connectivity from ASE to those resources (except for specific intra-ASE routing).</span></span> <span data-ttu-id="ced83-121">대신 (동일한 VNET에서) 다른 서브넷에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-121">Deploy to a different Subnet instead (in the same VNET).</span></span> <span data-ttu-id="ced83-122">앱 서비스 환경에 연결할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-122">The App Service Environment will then be able to connect.</span></span> <span data-ttu-id="ced83-123">추가 구성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-123">No additional configuration is necessary.</span></span>
> 
> 

<span data-ttu-id="ced83-124">앱 서비스 환경 역시 관리 및 운영에 필요한 sql DB 및 Azure 저장소와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-124">App Service Environments also communicate with Sql DB and Azure Storage resources necessary for managing and operating an App Service Environment.</span></span>  <span data-ttu-id="ced83-125">앱 서비스 환경과 통신하는 일부 SQL 및 저장소 리소스는 앱 서비스 환경과 같은 지역에 위치해 있는 반면, 나머지는 Azure 지역과 멀리 위치해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-125">Some of the Sql and Storage resources that an App Service Environment communicates with are located in the same region as the App Service Environment, while others are located in remote Azure regions.</span></span>  <span data-ttu-id="ced83-126">결과적으로, 인터넷에 대한 아웃 바운드 연결은 항상 제대로 작동하는 앱 서비스 환경에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-126">As a result, outbound connectivity to the Internet is always required for an App Service Environment to function properly.</span></span> 

<span data-ttu-id="ced83-127">서브넷에 배포된 앱 서비스 환경 때문에, 네트워크 보안 그룹은 서브넷에 인바운드 트래픽을 제어할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-127">Since an App Service Environment is deployed in a subnet, network security groups can be used to control inbound traffic to the subnet.</span></span>  <span data-ttu-id="ced83-128">App Service 환경에 대한 인바운드 트래픽을 제어하는 방법에 대한 자세한 내용은 다음 [문서][controllinginboundtraffic]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ced83-128">For details on how to control inbound traffic to an App Service Environment, see the following [article][controllinginboundtraffic].</span></span>

<span data-ttu-id="ced83-129">App Service 환경으로부터 아웃바운드 인터넷 연결을 허용하는 방법에 대한 세부 정보는 [Express 경로][ExpressRoute]로 작업하는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ced83-129">For details on how to allow outbound Internet connectivity from an App Service Environment, see the following article about working with [Express Route][ExpressRoute].</span></span>  <span data-ttu-id="ced83-130">사이트와 사이트를 연결 및 강제 터널링을 사용할 때는 문서에 설명된 동일한 방법을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-130">The same approach described in the article applies when working with Site-to-Site connectivity and using forced tunneling.</span></span>

## <a name="outbound-network-addresses"></a><span data-ttu-id="ced83-131">아웃 바운드 네트워크 주소</span><span class="sxs-lookup"><span data-stu-id="ced83-131">Outbound Network Addresses</span></span>
<span data-ttu-id="ced83-132">앱 서비스 환경이 아웃바운드를 호출하는 경우, IP 주소는 항상 아웃바운드 호출과 연관이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-132">When an App Service Environment makes outbound calls, an IP Address is always associated with the outbound calls.</span></span>  <span data-ttu-id="ced83-133">특정 IP 주소는 끝점 호출이 이 가상 네트워크 토폴로지 내에 있는지 혹은 밖에 있는지에 따라서 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-133">The specific IP address that is used depends on whether the endpoint being called is located within the virtual network topology, or outside of the virtual network topology.</span></span>

<span data-ttu-id="ced83-134">끝점이 가상 네트워크 토폴로지 **외부** 에서 호출된 경우, 아웃바운드 주소(즉, 아웃바운드 NAT 주소)는 앱 서비스 환경의 공용 VIP로 사용된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-134">If the endpoint being called is **outside** of the virtual network topology, then the outbound address (aka the outbound NAT address) that is used is the public VIP of the App Service Environment.</span></span>  <span data-ttu-id="ced83-135">속성 블레이드의 앱 서비스 환경에 대한 포털 사용자 인터페이스에서 이 주소를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-135">This address can be found in the portal user interface for the App Service Environment in Properties blade.</span></span>

![아웃 바운드 IP 주소][OutboundIPAddress]

<span data-ttu-id="ced83-137">앱 서비스 환경에서 앱을 만든 다음 앱 주소에 대해 *nslookup* 을 수행하여 공용 VIP만 있는 ASE에 대해 이 주소를 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-137">This address can also be determined for ASEs that only have a public VIP by creating an app in the App Service Environment, and then performing an *nslookup* on the app's address.</span></span> <span data-ttu-id="ced83-138">결과 IP 주소는 공용 VIP, 앱 서비스 환경의 아웃바운드 NAT 주소 둘 다 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-138">The resultant IP address is both the public VIP, as well as the App Service Environment's outbound NAT address.</span></span>

<span data-ttu-id="ced83-139">끝점이 가상 네트워크 토폴리지 **내** 에서 호출된 경우,  호출한 응용 프로그램의 아웃바운드 주소는 개별 계산 리소스의 내부 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-139">If the endpoint being called is **inside** of the virtual network topology, the outbound address of the calling app will be the internal IP address of the individual compute resource running the app.</span></span>  <span data-ttu-id="ced83-140">그러나 앱에 내부 IP 주소를 가상 네트워크의 지속적으로 매핑하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-140">However there is not a persistent mapping of virtual network internal IP addresses to apps.</span></span>  <span data-ttu-id="ced83-141">앱은 다른 계산 리소스에 걸쳐 이동할 수 있고, 앱 서비스 환경의 사용 가능한 계산 리소스의 풀은 크기 조정 때문에 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-141">Apps can move around across different compute resources, and the pool of available compute resources in an App Service Environment can change due to scaling operations.</span></span>

<span data-ttu-id="ced83-142">그러나 앱 서비스 환경은 항상 서브넷 내에 위치하므로, 앱을 실행하는 계산 리소스의 내부 IP 주소가 서브넷의 CIDR 범위에 놓인다는 점을 보장 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-142">However, since an App Service Environment is always located within a subnet, you are guaranteed that the internal IP address of a compute resource running an app will always lie within the CIDR range of the subnet.</span></span>  <span data-ttu-id="ced83-143">결과적으로 세분화 된 ACL 또는 네트워크 보안 그룹은 가상 네트워크 내의 다른 끝점의 액세스를 보호하는 데 사용되고, 앱 서비스 환경에 대한 서브넷 범위 조정은 액세스 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-143">As a result, when fine-grained ACLs or network security groups are used to secure access to other endpoints within the virtual network, the subnet range containing the App Service Environment needs to be granted access.</span></span>

<span data-ttu-id="ced83-144">다음 다이어그램에서는 이러한 개념을 자세히 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-144">The following diagram shows these concepts in more detail:</span></span>

![아웃 바운드 네트워크 주소][OutboundNetworkAddresses]

<span data-ttu-id="ced83-146">위의 다이어그램:</span><span class="sxs-lookup"><span data-stu-id="ced83-146">In the above diagram:</span></span>

* <span data-ttu-id="ced83-147">앱 서비스 환경의 공용 VIP가 192.23.1.2 이므로, "Internet" 끝점에 대한 호출을 만들 때 사용하는 아웃 바운드 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-147">Since the public VIP of the App Service Environment is 192.23.1.2, that is the outbound IP address used when making calls to "Internet" endpoints.</span></span>
* <span data-ttu-id="ced83-148">앱 서비스 환경에 대한 조정 서브넷을 포함하는 CIDR 범위가 10.0.1.0/26 입니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-148">The CIDR range of the containing subnet for the App Service Environment is 10.0.1.0/26.</span></span>  <span data-ttu-id="ced83-149">동일한 가상 네트워크 인프라 내에서 다른 끝점은 주소 범위 내에서 발생 한 것처럼 앱에서 호출을 보게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-149">Other endpoints within the same virtual network infrastructure will see calls from apps as originating from somewhere within this address range.</span></span>

## <a name="calls-between-app-service-environments"></a><span data-ttu-id="ced83-150">앱 서비스 환경 간의 호출</span><span class="sxs-lookup"><span data-stu-id="ced83-150">Calls Between App Service Environments</span></span>
<span data-ttu-id="ced83-151">동일 가상 네트워크의 여러 앱 서비스 환경에 배포하고 다른 앱 서비스 환경에서 다른 앱 서비스 환경으로 아웃바운드 호출을 작성하는 경우 더 복잡한 시나리오가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-151">A more complex scenario can occur if you deploy multiple App Service Environments in the same virtual network, and make outbound calls from one App Service Environment to another App Service Environment.</span></span>  <span data-ttu-id="ced83-152">이러한 종류의 크로스 앱 서비스 환경 호출은 "Internet" 호출로도 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-152">These types of cross App Service Environment calls will also be treated as "Internet" calls.</span></span>

<span data-ttu-id="ced83-153">다음 다이어그램은 두 번째 앱 서비스 환경(예: 인터넷에서 액세스할 수 없는 내부 백 엔드 API 앱)에서 앱을 호출하는 하나의 앱 서비스 환경(예: "프런트 도어" 웹앱)에서 앱으로 계층화된 아키텍처의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-153">The following diagram shows an example of a layered architecture with apps on one App Service Environment (e.g. "Front door" web apps) calling apps on a second App Service Environment (e.g. internal back-end API apps not intended to be accessible from the Internet).</span></span> 

![앱 서비스 환경 간의 호출][CallsBetweenAppServiceEnvironments] 

<span data-ttu-id="ced83-155">위의 예제에서 앱 서비스 환경 "ASE One"에는 192.23.1.2의 아웃 바운드 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-155">In the example above the App Service Environment "ASE One" has an outbound IP address of 192.23.1.2.</span></span>  <span data-ttu-id="ced83-156">앱 서비스 환경에서 실행되는 앱이 동일한 가상 네트워크에 위치한 두 번째 앱 서비스 환경("ASE Two")에서 실행 중인 앱에 아웃 바운드 호출을 하면 아웃 바운드 호출은 "인터넷" 호출로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-156">If an app running on this App Service Environment makes an outbound call to an app running on a second App Service Environment ("ASE Two") located in the same virtual network, the outbound call will be treated as an "Internet" call.</span></span>  <span data-ttu-id="ced83-157">결과적으로 두 번째 앱 서비스 환경에 도착하는 네트워크 트래픽은 192.23.1.2에서 만들어진 것입니다.(즉, 첫 번째 앱 서비스 환경의 서브넷 주소 범위가 아님)</span><span class="sxs-lookup"><span data-stu-id="ced83-157">As a result the network traffic arriving on the second App Service Environment will show as originating from 192.23.1.2 (i.e. not the subnet address range of the first App Service Environment).</span></span>

<span data-ttu-id="ced83-158">다른 앱 서비스 환경 간의 호출이 "Internet" 호출로 처리되더라도, 두 앱 서비스 환경이 모두 동일한 Azure 지역에 있으면 네트워크 트래픽은 지역 Azure 네트워크에 그대로 유지되며 물리적으로 공용 인터넷을 통해 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-158">Even though calls between different App Service Environments are treated as "Internet" calls, when both App Service Environments are located in the same Azure region the network traffic will remain on the regional Azure network and will not physically flow over the public Internet.</span></span>  <span data-ttu-id="ced83-159">결과적으로 첫 번째 앱 서비스 환경(아웃바운드 IP 주소는 192.23.1.2임)에서의 인바운드 호출을 허용하도록 두번째 앱 서비스 환경의 서브넷에서 네트워크 보안 그룹을 사용하여, 앱 서비스 환경 간의 보안 통신을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-159">As a result you can use a network security group on the subnet of the second App Service Environment to only allow inbound calls from the first App Service Environment (whose outbound IP address is 192.23.1.2), thus ensuring secure communication between the App Service Environments.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="ced83-160">추가 링크 및 정보</span><span class="sxs-lookup"><span data-stu-id="ced83-160">Additional Links and Information</span></span>
<span data-ttu-id="ced83-161">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-161">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="ced83-162">App Service 환경에서 사용된 인바운드 포트의 세부 정보 및 인바운드 트래픽 제어를 위한 네트워크 보안 그룹 사용은 [여기][controllinginboundtraffic]에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-162">Details on inbound ports used by App Service Environments and using network security groups to control inbound traffic is available [here][controllinginboundtraffic].</span></span>

<span data-ttu-id="ced83-163">App Service 환경에 아웃바운드 인터넷 액세스 권한을 부여하는 사용자 정의 경로 사용에 대한 자세한 세부 정보는 이 [문서][ExpressRoute]에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ced83-163">Details on using user defined routes to grant outbound Internet access to App Service Environments is available in this [article][ExpressRoute].</span></span> 

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[controllinginboundtraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[ExpressRoute]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/

<!-- IMAGES -->
[GeneralNetworkFlows]: ./media/app-service-app-service-environment-network-architecture-overview/NetworkOverview-1.png
[OutboundIPAddress]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundIPAddress-1.png
[OutboundNetworkAddresses]: ./media/app-service-app-service-environment-network-architecture-overview/OutboundNetworkAddresses-1.png
[CallsBetweenAppServiceEnvironments]: ./media/app-service-app-service-environment-network-architecture-overview/CallsBetweenEnvironments-1.png

