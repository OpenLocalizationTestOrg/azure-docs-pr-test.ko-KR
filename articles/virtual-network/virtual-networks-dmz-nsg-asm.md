---
title: "Azure DMZ 예제 – NSG를 사용하여 간단한 DMZ 빌드| Microsoft Docs"
description: "NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="1da5c-103">예제 1 – 클래식 PowerShell로 NSG를 사용하여 간단한 DMZ 빌드</span><span class="sxs-lookup"><span data-stu-id="1da5c-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="1da5c-104">[보안 경계 모범 사례 페이지로 돌아가기][HOME]</span><span class="sxs-lookup"><span data-stu-id="1da5c-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1da5c-105">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="1da5c-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="1da5c-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1da5c-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="1da5c-107">이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="1da5c-108">이 예제는 각 단계를 자세히 이해할 수 있도록 각각의 관련 PowerShell 명령을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="1da5c-109">트래픽 시나리오 섹션에서는 DMZ에서 방어 계층을 진행하는 방법에 대한 심층적인 단계별 설명도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="1da5c-110">마지막으로, 참조 섹션에서는 다양한 시나리오를 사용하여 테스트 및 실험하기 위한 환경을 구축하는 전체 코드와 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="1da5c-111">![NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="1da5c-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="1da5c-112">환경 설명</span><span class="sxs-lookup"><span data-stu-id="1da5c-112">Environment description</span></span>
<span data-ttu-id="1da5c-113">이 예에서 구독은 다음 리소스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="1da5c-114">두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="1da5c-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="1da5c-115">"FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"</span><span class="sxs-lookup"><span data-stu-id="1da5c-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="1da5c-116">서브넷 모두에 적용되는 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="1da5c-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="1da5c-117">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="1da5c-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="1da5c-118">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="1da5c-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="1da5c-119">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="1da5c-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="1da5c-120">참조 섹션에는 이 예제에서 설명한 대부분의 환경을 빌드하는 PowerShell 스크립트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="1da5c-121">VM 및 가상 네트워크 구축은 예제 스크립트로 수행하지만 이 문서에서는 자세히 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="1da5c-122">환경을 구축하려면</span><span class="sxs-lookup"><span data-stu-id="1da5c-122">To build the environment;</span></span>

1. <span data-ttu-id="1da5c-123">참조 섹션에 포함된 네트워크 구성 xml 파일 저장(지정된 시나리오에 맞게 이름, 위치, IP 주소로 업데이트됨)</span><span class="sxs-lookup"><span data-stu-id="1da5c-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="1da5c-124">스크립트의 사용자 변수를 스크립트를 실행할 환경에 맞게 업데이트(구독, 서비스 이름 등)</span><span class="sxs-lookup"><span data-stu-id="1da5c-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="1da5c-125">PowerShell에서 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="1da5c-125">Execute the script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="1da5c-126">PowerShell 스크립트에 표시된 영역은 네트워크 구성 xml 파일에 표시된 영역과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-126">The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>
>
>

<span data-ttu-id="1da5c-127">스크립트가 성공적으로 실행되면 추가로 선택적 단계를 수행할 수 있는데, 참조 섹션의 두 스크립트를 사용하여 간단한 웹 응용 프로그램을 사용하는 웹 서버와 앱 서버를 설정하여 이 DMZ 구성을 이용한 테스트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="1da5c-128">다음 섹션에서는 네트워크 보안 그룹을 설명하고 PowerShell 스크립트의 핵심 줄을 살펴보는 방법으로 이 예제의 작동 방식을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="1da5c-129">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="1da5c-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="1da5c-130">이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="1da5c-131">일반적으로 특정 "허용" 규칙을 먼저 만든 후 보다 일반적인 "거부" 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-131">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="1da5c-132">할당된 우선순위에 따라 먼저 평가할 규칙이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-132">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="1da5c-133">특정 규칙에 적용할 트래픽이 발견되면 규칙을 더 이상 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-133">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="1da5c-134">NSG 규칙은 인바운드 또는 아웃바운드 방향으로 적용할 수 있습니다(서브넷 관점에서).</span><span class="sxs-lookup"><span data-stu-id="1da5c-134">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="1da5c-135">선언적으로 인바운드 트래픽에 대해 다음 규칙이 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="1da5c-136">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="1da5c-137">인터넷에서 모든 VM으로 RDP 트래픽(포트 3389) 허용됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="1da5c-138">인터넷에서 웹 서버(IIS01)로 HTTP 트래픽(포트 80) 허용됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="1da5c-139">IIS01에서 AppVM1로 모든 트래픽(모든 포트) 허용됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="1da5c-140">인터넷에서 전체 VNet(두 서브넷)으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="1da5c-141">프런트 엔드 서브넷에서 백 엔드 서브넷으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="1da5c-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="1da5c-142">각 서브넷에 바인딩된 이러한 규칙에서는 HTTP 요청이 인터넷에서 웹 서버로 인바운드되는 경우 규칙 3(허용) 및 5(거부)가 모두 적용되지만 규칙 3이 우선순위가 높기 때문에 규칙 3만 적용되고 규칙 5는 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="1da5c-143">따라서 웹 서버에 대해 HTTP 요청이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="1da5c-144">동일한 트래픽이 DNS01 서버에 도달하려고 시도하는 경우 규칙 5(거부)는 가장 먼저 적용되며 트래픽을 서버에 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="1da5c-145">규칙 6(거부)은 프런트 엔드 서브넷이 백 엔드 서브넷과 통신하는 것을 차단(규칙 1 및 4에서 허용된 트래픽 제외)하여 공격자가 프런트 엔드에서 웹 응용 프로그램을 손상시키는 경우 공격자의 "보호된" 백 엔드 네트워크(AppVM01 서버에서 노출되는 리소스만)에 대한 액세스가 제한되므로 이 규칙 집합은 백 엔드 네트워크를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="1da5c-146">인터넷으로 트래픽을 허용하는 기본 아웃바운드 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="1da5c-147">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="1da5c-148">양방향에서 트래픽을 잠그려면 사용자 정의 라우팅이 필요하며 [보안 경계 모범 사례 페이지][HOME]의 "예제 3"에서 이에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="1da5c-149">다음과 같이 각 규칙을 보다 상세히 설명합니다.(**참고**: 달러 기호(예: $NSGName)로 시작하는 다음 목록에서 모든 항목은 이 문서의 참조 섹션에서 스크립트의 사용자 정의 변수입니다.)</span><span class="sxs-lookup"><span data-stu-id="1da5c-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="1da5c-150">먼저 규칙을 포함하도록 네트워크 보안 그룹을 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="1da5c-151">이 예의 첫 번째 규칙에서는 백 엔드 서브넷에서 DNS 서버에 대해 모든 내부 네트워크 간 DNS 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="1da5c-152">규칙은 몇 가지 중요한 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="1da5c-153">"Type"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="1da5c-154">방향은 서브넷 또는 가상 컴퓨터의 관점에서 옵니다(이 NSG가 바인딩되는 위치에 따라).</span><span class="sxs-lookup"><span data-stu-id="1da5c-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="1da5c-155">따라서 Type이 "Inbound"이고 트래픽이 서브넷에 들어가는 경우 규칙이 적용되고 서브넷에서 나가는 트래픽에는 이 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="1da5c-156">"Priority"는 트래픽 흐름이 평가되는 순서를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="1da5c-157">번호가 낮을수록 우선순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="1da5c-158">특정 트래픽 흐름에 규칙이 적용되는 경우 더 이상 규칙이 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="1da5c-159">따라서 우선순위 1인 규칙에서는 트래픽을 허용하고 우선순위 2인 규칙에서는 트래픽을 거부하고 두 규칙 모두 트래픽에 적용된다면 트래픽 흐름이 허용됩니다(규칙 1의 우선순위가 높으므로 해당 규칙이 적용되고 다른 규칙은 적용되지 않음).</span><span class="sxs-lookup"><span data-stu-id="1da5c-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="1da5c-160">"Action"은 이 규칙의 영향을 받는 트래픽을 차단하거나 허용할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="1da5c-161">이 규칙은 RDP 트래픽이 인터넷에서 바인딩된 서브넷에 있는 모든 서버의 RDP 포트로 흐르도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="1da5c-162">이 규칙은 "VIRTUAL_NETWORK" 및 "INTERNET"이라는 두 가지 특별한 주소 접두사 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="1da5c-163">이러한 태그는 주소 접두사로 더 큰 범주의 주소를 간편하게 지정하는 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="1da5c-164">이 규칙은 웹 서버를 호출하기 위해 인바운드 인터넷 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="1da5c-165">이 규칙은 라우팅 동작을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="1da5c-166">규칙은 IIS01을 대상으로 하는 트래픽만을 전달하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="1da5c-167">따라서 인터넷에서 트래픽이 이 규칙에서 허용하는 대상으로 웹 서버를 포함하는 경우 추가 규칙의 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="1da5c-168">(우선순위 140의 규칙에서 모든 다른 인바운드 인터넷 트래픽이 차단됩니다.)</span><span class="sxs-lookup"><span data-stu-id="1da5c-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="1da5c-169">HTTP 트래픽만 처리하는 경우 대상 포트 80만 허용하도록 이 규칙을 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="1da5c-170">이 규칙은 IIS01 서버에서 AppVM01 서버로 트래픽 전달을 허용합니다. 이후 규칙은 백 엔드 트래픽에 대한 모든 다른 프런트엔드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="1da5c-171">추가해야 할 포트를 알고 있다면 이 규칙을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="1da5c-172">예를 들어, IIS 서버가 AppVM01에서 SQL Server만 연결하는 경우 대상 포트 범위를 "*"(모두)에서 1433(SQL 포트)으로 변경해야 하므로 AppVM01에서 웹 응용 프로그램이 손상될 수 있는 인바운드 공격에 대한 취약성을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="1da5c-173">이 규칙은 네트워크 상의 모든 서버에 인터넷에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="1da5c-174">우선순위 110 및 120의 규칙을 사용하여 방화벽에 대한 인바운드 인터넷 트래픽 및 서버의 RDP 포트만 허용하고 다른 모든 항목은 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="1da5c-175">이 규칙은 모든 예기치 않은 흐름을 차단하는 "유사 시 대기" 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="1da5c-176">마지막 규칙은 프런트엔드 서브넷에서 백 엔드 서브넷으로 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="1da5c-177">이 규칙은 인바운드 전용 규칙이므로 역방향 트래픽이 허용됩니다(백 엔드에서 프런트 엔드로).</span><span class="sxs-lookup"><span data-stu-id="1da5c-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="1da5c-178">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="1da5c-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="1da5c-179">(*허용*) 인터넷에서 웹 서버</span><span class="sxs-lookup"><span data-stu-id="1da5c-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="1da5c-180">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="1da5c-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="1da5c-181">클라우드 서비스는 포트 80에서 열린 끝점을 통해 IIS01(웹 서버)로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="1da5c-182">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-183">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="1da5c-184">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="1da5c-185">NSG 규칙 3(인터넷에서 IIS01로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1da5c-186">트래픽이 웹 서버 IIS01의 내부 IP 주소를 호출합니다(10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="1da5c-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="1da5c-187">IIS01이 웹 트래픽을 수신 대기하고 이 요청을 수신하며 요청 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="1da5c-188">IIS01은 AppVM01에서 SQL Server에 정보를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="1da5c-189">프런트 엔드 서브넷에 아웃바운드 규칙이 없으므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="1da5c-190">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-191">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="1da5c-192">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="1da5c-193">NSG 규칙 3(인터넷에서 방화벽으로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="1da5c-194">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="1da5c-195">AppVM01은 SQL 쿼리를 수신하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="1da5c-196">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="1da5c-197">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="1da5c-198">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="1da5c-199">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="1da5c-200">IIS 서버는 SQL 응답을 수신하고 HTTP 응답을 완료하여 요청자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="1da5c-201">응답이 허용되는 프런트 엔드 서브넷에 아웃바운드 규칙이 없으므로 인터넷 사용자는 요청된 웹 페이지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="1da5c-202">(*허용*) RDP - 백 엔드</span><span class="sxs-lookup"><span data-stu-id="1da5c-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="1da5c-203">인터넷의 서버 관리자는 BackEnd001.CloudApp.Net:xxxxx에서 AppVM01에 대해 RDP 세션을 요청합니다.여기서 xxxxx는 RDP에 대해 AppVM01로 임의로 할당된 포트 번호입니다(할당된 포트는 Azure Portal 또는 PowerShell을 통해 확인할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="1da5c-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="1da5c-204">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-205">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="1da5c-206">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="1da5c-207">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="1da5c-208">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-208">RDP session is enabled</span></span>
5. <span data-ttu-id="1da5c-209">AppVM01에서 사용자 이름과 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="1da5c-210">(*허용*) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="1da5c-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="1da5c-211">웹 서버인 IIS01은 www.data.gov에서 데이터 피드를 요구하지만 주소를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="1da5c-212">VNet에 대한 네트워크 구성에서 DNS01(백 엔드 서브넷에서 10.0.2.4)을 주 DNS 서버로 나열하며 IIS01은 DNS01로 DNS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="1da5c-213">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="1da5c-214">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="1da5c-215">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="1da5c-216">DNS 서버는 요청을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-216">DNS server receives the request</span></span>
6. <span data-ttu-id="1da5c-217">DNS 서버에는 캐시된 주소가 없고 인터넷에서 루트 DNS 서버를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="1da5c-218">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="1da5c-219">이 세션은 내부적으로 시작되었으므로 인터넷 DNS 서버가 응답하고 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="1da5c-220">DNS 서버는 응답을 캐시하고 IIS01에 대한 초기 요청에 다시 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="1da5c-221">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="1da5c-222">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="1da5c-223">백 엔드 서브넷에서 프런트 엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="1da5c-224">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙에서 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="1da5c-225">IIS01이 DNS01에서 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="1da5c-226">(*허용*) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="1da5c-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="1da5c-227">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="1da5c-228">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="1da5c-229">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-230">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="1da5c-231">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="1da5c-232">NSG 규칙 3(인터넷에서 IIS01로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="1da5c-233">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1da5c-234">AppVM01이 요청을 받아 파일로 응답합니다(액세스 권한이 부여된 것으로 가정).</span><span class="sxs-lookup"><span data-stu-id="1da5c-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="1da5c-235">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="1da5c-236">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-237">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="1da5c-238">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="1da5c-239">IIS 서버가 파일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="1da5c-240">(*거부*) 웹 - 백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="1da5c-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="1da5c-241">인터넷 사용자가 BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에서 파일에 액세스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="1da5c-242">파일 공유를 위해 열린 끝점이 없으므로 이 트래픽은 클라우드 서비스를 전달하지 않고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="1da5c-243">어떤 이유로 끝점이 열린 경우 NSG 규칙 5(인터넷에서 VNet으로)가 이 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="1da5c-244">(*거부*) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="1da5c-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="1da5c-245">인터넷 사용자가 BackEnd001.CloudApp.Net 서비스를 통해 DNS01에서 내부 DNS 레코드를 조회하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="1da5c-246">DNS를 위해 열린 끝점이 없으므로 이 트래픽은 클라우드 서비스를 전달하지 않고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="1da5c-247">어떤 이유로 끝점이 열린 경우 NSG 규칙 5(인터넷에서 VNet으로)가 이 트래픽을 차단합니다.(참고: 규칙 1(DNS)은 두 가지 이유로 적용되지 않습니다. 첫째, 원본 주소가 인터넷입니다. 이 규칙은 로컬 VNet에만 원본으로 적용됩니다. 또한 이 규칙은 허용 규칙이므로 트래픽을 거부하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="1da5c-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="1da5c-248">(*거부*) 방화벽을 통해 웹에서 SQL 액세스</span><span class="sxs-lookup"><span data-stu-id="1da5c-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="1da5c-249">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="1da5c-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="1da5c-250">SQL을 위해 열린 끝점이 없으므로 이 트래픽은 클라우드 서비스를 전달하지 않고 방화벽에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="1da5c-251">어떤 이유로 끝점이 열린 경우 프런트엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1da5c-252">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="1da5c-253">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="1da5c-254">NSG 규칙 3(인터넷에서 IIS01로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1da5c-255">트래픽이 IIS01의 내부 IP 주소를 호출합니다(10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="1da5c-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="1da5c-256">IIS01이 포트 1433에서 수신 대기하지 않으므로 요청에 대한 응답이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="1da5c-257">결론</span><span class="sxs-lookup"><span data-stu-id="1da5c-257">Conclusion</span></span>
<span data-ttu-id="1da5c-258">이 예제는 백 엔드 서브넷을 인바운드 트래픽과 격리하는 비교적 간단하고 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="1da5c-259">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="1da5c-260">참조</span><span class="sxs-lookup"><span data-stu-id="1da5c-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="1da5c-261">기본 스크립트 및 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="1da5c-261">Main script and network config</span></span>
<span data-ttu-id="1da5c-262">PowerShell 스크립트 파일에 전체 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="1da5c-263">네트워크 구성을 "NetworkConf1.xml"이라는 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="1da5c-264">필요에 따라 사용자 정의 변수를 수정하고 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="1da5c-265">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="1da5c-265">Full script</span></span>
<span data-ttu-id="1da5c-266">이 스크립트는 사용자 정의 변수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="1da5c-267">Azure 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="1da5c-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="1da5c-268">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1da5c-268">Create a storage account</span></span>
3. <span data-ttu-id="1da5c-269">네트워크 구성 파일에 정의된 대로 VNet 및 두 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="1da5c-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="1da5c-270">4개의 Windows Server VM 빌드</span><span class="sxs-lookup"><span data-stu-id="1da5c-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="1da5c-271">다음을 포함하여 NSG를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-271">Configure NSG including:</span></span>
   * <span data-ttu-id="1da5c-272">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="1da5c-272">Creating an NSG</span></span>
   * <span data-ttu-id="1da5c-273">규칙으로 채우기</span><span class="sxs-lookup"><span data-stu-id="1da5c-273">Populating it with rules</span></span>
   * <span data-ttu-id="1da5c-274">적절한 서브넷에 대해 NSG 바인딩</span><span class="sxs-lookup"><span data-stu-id="1da5c-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="1da5c-275">이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1da5c-276">이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="1da5c-277">빨간색 오류 메시지만 심각한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer to New Storage Account
    Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="1da5c-278">네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="1da5c-278">Network config file</span></span>
<span data-ttu-id="1da5c-279">업데이트된 위치로 이 xml 파일을 저장하고 이 파일에 대한 링크를 앞의 스크립트에 있는 $NetworkConfigFile 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1da5c-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="1da5c-280">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="1da5c-280">Sample application scripts</span></span>
<span data-ttu-id="1da5c-281">이에 대한 샘플 응용 프로그램 및 기타 DMZ 예제를 설치하는 방법은 다음 링크를 통해 제공됩니다. [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="1da5c-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1da5c-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1da5c-282">Next steps</span></span>
* <span data-ttu-id="1da5c-283">업데이트 및 XML 파일 저장</span><span class="sxs-lookup"><span data-stu-id="1da5c-283">Update and save XML file</span></span>
* <span data-ttu-id="1da5c-284">PowerShell 스크립트를 실행하여 환경 구축</span><span class="sxs-lookup"><span data-stu-id="1da5c-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="1da5c-285">샘플 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="1da5c-285">Install the sample application</span></span>
* <span data-ttu-id="1da5c-286">이 DMZ를 통해 다양한 트래픽 흐름 테스트</span><span class="sxs-lookup"><span data-stu-id="1da5c-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="1da5c-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG와 인바운드 DMZ"</span><span class="sxs-lookup"><span data-stu-id="1da5c-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

