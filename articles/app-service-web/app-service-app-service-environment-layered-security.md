---
title: "앱 서비스 환경으로 계층화된 보안 아키텍처"
description: "앱 서비스 환경으로 계층화된 보안 아키텍처 구현"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="17f9b-103">앱 서비스 환경으로 계층화된 보안 아키텍처 구현</span><span class="sxs-lookup"><span data-stu-id="17f9b-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="17f9b-104">개요</span><span class="sxs-lookup"><span data-stu-id="17f9b-104">Overview</span></span>
<span data-ttu-id="17f9b-105">앱 서비스 환경이 가상 네트워크에 배포된 격리된 런타임 환경을 제공하므로 개발자는 실제 응용 프로그램 계층 각각에 서로 다른 수준으로 네트워크 액세스를 제공하는 계층화된 보안 아키텍처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="17f9b-106">일반적으로 일반 인터넷 액세스로부터 API 백 엔드를 숨기거나 API가 업스트림 웹앱에서 호출될 수 있도록 하기 원합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="17f9b-107">[네트워크 보안 그룹(NSG)][NetworkSecurityGroups]은 App Service 환경을 포함하는 서브넷에서 사용되어 API 응용 프로그램에 대한 공용 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="17f9b-108">아래 다이어그램은 앱 서비스 환경에 배포된 Web API 기반 앱을 사용한 예제 아키텍처를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="17f9b-109">3개의 별도 앱 서비스 환경에 배포된 3개의 별도 웹앱 인스턴스는 동일한 Web API 앱에 백 엔드 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![개념적 아키텍처][ConceptualArchitecture] 

<span data-ttu-id="17f9b-111">녹색 더하기 기호는 "apiase"를 포함하는 서브넷의 네트워크 보안 그룹이 자체에서 호출 뿐만 아니라 업스트림 웹앱에서 인바운드 호출을 허용한다는 사실을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="17f9b-112">그러나 동일한 네트워크 보안 그룹은 인터넷에서 일반 인바운드 트래픽에 대한 액세스를 명시적으로 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="17f9b-113">이 항목의 나머지 부분에서는 "apiase"를 포함하는 서브넷에 네트워크 보안 그룹을 구성하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="17f9b-114">네트워크 동작 확인</span><span class="sxs-lookup"><span data-stu-id="17f9b-114">Determining the Network Behavior</span></span>
<span data-ttu-id="17f9b-115">어떤 네트워크 보안 규칙이 필요한지 알기 위해 어떤 네트워크 클라이언트가 API 앱을 포함하는 앱 서비스 환경에 연결할 수 있고 어떤 클라이언트를 차단할지 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="17f9b-116">[네트워크 보안 그룹(NSG)][NetworkSecurityGroups]이 서브넷에 적용되고 App Service 환경이 서브넷에 배포되기 때문에 NSG에 포함된 규칙은 App Service 환경에서 실행하는 **모든** 앱에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="17f9b-117">네트워크 보안 그룹이 "apiase"를 포함하는 서브넷에 적용되면 이 문서에 대한 샘플 아키텍처를 사용하여 "apiase" 앱 서비스 환경에서 실행되는 모든 앱은 동일한 집합의 보안 규칙에 의해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="17f9b-118">**업스트림 호출자의 아웃 바운드 IP 주소 확인:** IP 주소 또는 업스트림 호출자의 주소는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="17f9b-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="17f9b-119">이러한 주소는 NSG에서 명시적으로 액세스하도록 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="17f9b-120">앱 서비스 환경 간의 호출이 "Internet" 호출을 고려하기 때문에 각 세 업스트림 응용 프로그램 서비스 환경에 할당된 아웃 바운드 IP 주소는 "apiase" 서브넷에 대한 NSG에서 액세스하도록 허용해야 한다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="17f9b-121">App Service 환경에서 실행되는 앱에 대한 아웃 바운드 IP 주소를 확인하는 데 대한 자세한 내용은 [네트워크 아키텍처][NetworkArchitecture] 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17f9b-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="17f9b-122">**백 엔드 API 앱 자체를 호출해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="17f9b-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="17f9b-123">때로는 간과되고 미묘한 점은 백 엔드 응용 프로그램이 자신을 호출해야 한다는 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="17f9b-124">또한 앱 서비스 환경에서 백 엔드 API 응용 프로그램이 자신을 호출하는 경우 "인터넷" 호출로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="17f9b-125">샘플 아키텍처에서는 "apiase" 앱 서비스 환경의 아웃 바운드 IP 주소에서 액세스하도록 허락이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="17f9b-126">네트워크 보안 그룹 설치</span><span class="sxs-lookup"><span data-stu-id="17f9b-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="17f9b-127">아웃 바운드 IP 주소 집합을 모두 알고 나면 다음 단계에서 네트워크 보안 그룹을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="17f9b-128">클래식 가상 네트워크뿐만 아니라 가상 네트워크를 기반으로 하는 두 Resource Manager에 네트워크 보안 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="17f9b-129">아래 예제에서는 Powershell을 사용하여 기존 가상 네트워크에 NSG를 만들고 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="17f9b-130">샘플 아키텍처의 경우 환경은 미국 중남부에 있으므로 빈 NSG는 해당 지역에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="17f9b-131">먼저 명시적 허용 규칙은App Service 환경에 대한 [인바운드 트래픽][InboundTraffic] 문서에서 설명한 대로 Azure 관리 인프라에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="17f9b-132">다음으로 첫 번째 업스트림 앱 서비스 환경("fe1ase")에서 HTTP 및 HTTPS 호출을 허용하도록 두 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="17f9b-133">두 번째 및 세 번째 업스트림 앱 서비스 환경("fe2ase" 및 "fe3ase")을 다듬고 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="17f9b-134">마지막으로 백 엔드 API의 앱 서비스 환경의 아웃 바운드 IP 주소에 대한 액세스를 부여하므로 자신에 다시 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="17f9b-135">모든 NSG에 기본적으로 인터넷에서 인바운드 액세스를 차단하는 기본 규칙의 집합이 있기 때문에 다른 네트워크 보안 규칙은 구성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="17f9b-136">네트워크 보안 그룹에 있는 규칙의 전체 목록은 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="17f9b-137">강조 표시된 마지막 규칙이 명시적으로 액세스를 부여한 호출자를 제외한 모든 호출자에서 인바운드 액세스를 차단하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG 구성][NSGConfiguration] 

<span data-ttu-id="17f9b-139">마지막 단계는 "apiase" 앱 서비스 환경에 포함된 서브넷에 NSG를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="17f9b-140">서브넷에 적용된 NSG를 사용하여 3개의 업스트림 앱 서비스 환경 및 API 백 엔드를 포함하는 앱 서비스 환경은 "apiase" 환경으로 호출하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="17f9b-141">추가 링크 및 정보</span><span class="sxs-lookup"><span data-stu-id="17f9b-141">Additional Links and Information</span></span>
<span data-ttu-id="17f9b-142">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17f9b-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="17f9b-143">[네트워크 보안 그룹](../virtual-network/virtual-networks-nsg.md)에 대한 정보.</span><span class="sxs-lookup"><span data-stu-id="17f9b-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="17f9b-144">[아웃바운드 IP 주소][NetworkArchitecture] 및 App Service 환경 이해.</span><span class="sxs-lookup"><span data-stu-id="17f9b-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="17f9b-145">App Service 환경에서 사용되는 [네트워크 포트][InboundTraffic].</span><span class="sxs-lookup"><span data-stu-id="17f9b-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
