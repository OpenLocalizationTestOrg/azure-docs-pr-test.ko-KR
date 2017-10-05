---
title: "앱 서비스 환경에서 백 엔드 리소스에 안전하게 연결"
description: "앱 서비스 환경에서 백 엔드 리소스에 안전하게 연결하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="318f0-103">앱 서비스 환경에서 백 엔드 리소스에 안전하게 연결</span><span class="sxs-lookup"><span data-stu-id="318f0-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="318f0-104">개요</span><span class="sxs-lookup"><span data-stu-id="318f0-104">Overview</span></span>
<span data-ttu-id="318f0-105">App Service 환경은 **항상** Azure Resource Manager 가상 네트워크 **또는** 클래식 배포 모델 [가상 네트워크][virtualnetwork]의 서브넷에 만들어지므로 App Service 환경에서 다른 백 엔드 리소스로의 아웃바운드 연결은 가상 네트워크를 통해서만 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="318f0-106">최근에 수행된 2016년 6월 변경 내용에 따르면 공용 주소 범위 또는 RFC1918 주소 공간(즉, 개인 주소) 중 하나를 사용하는 가상 네트워크에 ASE를</span><span class="sxs-lookup"><span data-stu-id="318f0-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="318f0-107">배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-107">private addresses).</span></span>  

<span data-ttu-id="318f0-108">예를 들어 잠긴 포트 1433을 통해 가상 컴퓨터의 클러스터에서 실행되는 SQL Server가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="318f0-109">끝점은 동일한 가상 네트워크에 있는 다른 리소스의 액세스만 허용하도록 ACL에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="318f0-110">또 다른 예로, 중요한 끝점은 온-프레미스에서 실행되고 [사이트 간][SiteToSite] 또는 [Azure ExpressRoute][ExpressRoute] 연결을 통해 Azure에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="318f0-111">따라서 사이트 간 또는 ExpressRoute 터널에 연결된 가상 네트워크의 리소스만 온-프레미스 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="318f0-112">이 모든 시나리오에 대해 앱 서비스 환경에서 실행되는 앱은 다양한 서버 및 리소스에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="318f0-113">앱 서비스 환경에서 실행되는 앱에서 동일한 가상 네트워크에 있는(또는 동일한 가상 네트워크에 연결된) 개인 끝점으로의 아웃바운드 트래픽은 가상 네트워크를 통해서만 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="318f0-114">개인 끝점으로의 아웃바운드 트래픽은 공용 인터넷을 통해 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="318f0-115">한 가지 주의 사항은 앱 서비스 환경과 가상 네트워크 내 끝점 간의 아웃바운드 트래픽에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="318f0-116">앱 서비스 환경은 앱 서비스 환경과 **동일한** 서브넷에 있는 가상 컴퓨터의 끝점에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="318f0-117">이는 앱 서비스 환경이 앱 서비스 환경 전용으로 예약된 서브넷에 배포된 경우에는 일반적으로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="318f0-118">아웃 바운드 연결 및 DNS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="318f0-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="318f0-119">앱 서비스 환경이 제대로 작동하려면 다양한 끝점에 대한 아웃바운드 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="318f0-120">ASE에서 사용하는 외부 끝점의 전체 목록은 [Express 경로에 대한 네트워크 구성](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) 문서의 "필수 네트워크 연결" 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="318f0-121">앱 서비스 환경에는 가상 네트워크에 대해 구성된 유효한 DNS 인프라가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="318f0-122">앱 서비스 환경을 만든 후에 어떤 이유로든 DNS 구성이 변경되면 개발자는 앱 서비스 환경을 강제하여 새 DNS 구성을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="318f0-123">포털에서 앱 서비스 환경 관리 블레이드의 상단에 있는 "다시 시작" 아이콘을 사용하여 롤링 환경 다시 부팅을 트리거하면 환경에서 새 DNS 구성을 선택하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="318f0-124">Vnet의 모든 사용자 지정 DNS 서버는 앱 서비스 환경 생성보다 미리 설치하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="318f0-125">앱 서비스 환경이 만들어질 때 가상 네트워크의 DNS 구성이 변경될 경우, 앱 서비스 환경 생성 과정에 장애가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="318f0-126">이와 비슷하게, 사용자 지정 DNS 서버가 VPN 게이트웨이의 반대쪽 끝에 있고 DNS 서버를 연결하거나 사용할 수 없는 경우 앱 서비스 환경을 만드는 프로세스도 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="318f0-127">SQL Server 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="318f0-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="318f0-128">일반적인 SQL Server 구성에는 포트 1433에서 수신 대기하는 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server 끝점][SqlServerEndpoint]

<span data-ttu-id="318f0-130">이 끝점으로 트래픽을 제한하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="318f0-131">[네트워크 액세스 제어 목록][NetworkAccessControlLists](네트워크 ACL)</span><span class="sxs-lookup"><span data-stu-id="318f0-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="318f0-132">[네트워크 보안 그룹][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="318f0-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="318f0-133">네트워크 ACL을 사용하여 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="318f0-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="318f0-134">네트워크 액세스 제어 목록을 사용하여 포트 1433의 보안을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="318f0-135">아래 예제에서는 가상 네트워크 내부에서 시작되는 클라이언트 주소는 허용하고 다른 모든 클라이언트에 대한 액세스는 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![네트워크 액세스 제어 목록 예][NetworkAccessControlListExample]

<span data-ttu-id="318f0-137">SQL Server와 동일한 가상 네트워크의 앱 서비스 환경에서 실행되는 모든 응용 프로그램은 SQL Server 가상 컴퓨터에 대한 **VNet 내부** IP 주소를 사용하여 SQL Server 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="318f0-138">아래 예제 연결 문자열은 해당 개인 IP 주소를 사용하여 SQL Server를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="318f0-139">가상 컴퓨터에 공용 끝점도 있지만 공용 IP 주소를 사용한 연결 시도는 네트워크 ACL 때문에 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="318f0-140">네트워크 보안 그룹을 사용하여 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="318f0-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="318f0-141">액세스를 보호하는 또 다른 방법은 네트워크 보안 그룹을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="318f0-142">개별 가상 컴퓨터 또는 가상 컴퓨터가 포함된 서브넷에 네트워크 보안 그룹을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="318f0-143">먼저 네트워크 보안 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="318f0-144">VNet 내부 트래픽으로만 액세스를 제한하는 작업은 네트워크 보안 그룹을 사용할 경우 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="318f0-145">네트워크 보안 그룹의 기본 규칙은 동일한 가상 네트워크에 있는 다른 네트워크 클라이언트의 액세스만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="318f0-146">따라서 SQL Server에 대한 액세스를 잠그는 것은 SQL Server를 실행하는 가상 컴퓨터 또는 가상 컴퓨터가 포함된 서브넷에 네트워크 보안 그룹을 해당 기본 규칙으로 적용하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="318f0-147">아래 샘플에서는 서브넷에 네트워크 보안 그룹을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="318f0-148">최종 결과는 VNet 내부 액세스는 허용하는 반면, 외부 액세스는 차단하는 보안 규칙 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![기본 네트워크 보안 규칙][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="318f0-150">시작</span><span class="sxs-lookup"><span data-stu-id="318f0-150">Getting started</span></span>
<span data-ttu-id="318f0-151">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318f0-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="318f0-152">App Service 환경을 시작하려면 [App Service 환경 소개][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="318f0-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="318f0-153">App Service 환경으로의 인바운드 트래픽을 제어하는 방법에 대한 자세한 내용은 [App Service 환경으로의 인바운드 트래픽 제어][ControlInboundASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="318f0-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="318f0-154">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service][AzureAppService]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="318f0-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
