---
title: "Azure DMZ 예제 – NSG를 사용하여 간단한 DMZ 빌드| Microsoft Docs"
description: "NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: ec29e6b250f927a3a4a94ffdf83d6c7c0e325722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="19694-103">예 1 – Azure Resource Manager 템플릿으로 NSG를 사용하여 간단한 DMZ 빌드</span><span class="sxs-lookup"><span data-stu-id="19694-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="19694-104">[보안 경계 모범 사례 페이지로 돌아가기][HOME]</span><span class="sxs-lookup"><span data-stu-id="19694-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="19694-105">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="19694-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="19694-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="19694-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="19694-107">이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="19694-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="19694-108">이 예제는 각 단계를 자세히 이해할 수 있도록 각각의 관련 템플릿 섹션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="19694-109">트래픽 시나리오 섹션에서는 DMZ에서 방어 계층을 진행하는 방법에 대한 심층적인 단계별 설명도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="19694-110">마지막으로, 참조 섹션에서는 다양한 시나리오를 사용하여 테스트 및 실험하기 위한 환경을 구축하는 전체 템플릿 코드와 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="19694-111">![NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="19694-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="19694-112">환경 설명</span><span class="sxs-lookup"><span data-stu-id="19694-112">Environment description</span></span>
<span data-ttu-id="19694-113">이 예에서 구독은 다음 리소스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="19694-114">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="19694-114">A single resource group</span></span>
* <span data-ttu-id="19694-115">두 서브넷 “프런트 엔드” 및 “백 엔드”를 사용하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="19694-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="19694-116">서브넷 모두에 적용되는 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="19694-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="19694-117">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="19694-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="19694-118">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="19694-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="19694-119">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="19694-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="19694-120">응용 프로그램 웹 서버에 연결된 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="19694-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="19694-121">참조 섹션에서 이 예제에서 설명된 환경을 구축하는 Azure Resource Manager 템플릿에 대한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="19694-122">VM 및 가상 네트워크 구축은 예제 템플릿으로 수행하지만 이 문서에서는 자세히 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="19694-123">**이 환경을 구축하려면**(자세한 지침은 이 문서의 참조 섹션에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="19694-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="19694-124">Azure Resource Manager 템플릿 배포: [Azure 빠른 시작 템플릿][Template]</span><span class="sxs-lookup"><span data-stu-id="19694-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="19694-125">샘플 응용 프로그램 설치: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="19694-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="19694-126">이 인스턴스의 백 엔드 서버에 RDP하려면 IIS 서버는 "점프 상자"로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-126">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="19694-127">먼저 RDP에서 IIS 서버로 그 다음에 IIS 서버 RDP에서 백 엔드 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-127">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span> <span data-ttu-id="19694-128">또는 공용 IP는 보다 쉬운 RDP를 위해 각 서버 NIC와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="19694-129">다음 섹션에서는 네트워크 보안 그룹을 설명하고 Azure Resource Manager 템플릿의 핵심 줄을 살펴보는 방법으로 이 예제의 작동 방식을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="19694-130">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="19694-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="19694-131">이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="19694-132">일반적으로 특정 "허용" 규칙을 먼저 만든 후 보다 일반적인 "거부" 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-132">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="19694-133">할당된 우선순위에 따라 먼저 평가할 규칙이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-133">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="19694-134">특정 규칙에 적용할 트래픽이 발견되면 규칙을 더 이상 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-134">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="19694-135">NSG 규칙은 인바운드 또는 아웃바운드 방향으로 적용할 수 있습니다(서브넷 관점에서).</span><span class="sxs-lookup"><span data-stu-id="19694-135">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
>
>

<span data-ttu-id="19694-136">선언적으로 인바운드 트래픽에 대해 다음 규칙이 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="19694-137">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="19694-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="19694-138">인터넷에서 모든 VM으로 RDP 트래픽(포트 3389) 허용됨</span><span class="sxs-lookup"><span data-stu-id="19694-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="19694-139">인터넷에서 웹 서버(IIS01)로 HTTP 트래픽(포트 80) 허용됨</span><span class="sxs-lookup"><span data-stu-id="19694-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="19694-140">IIS01에서 AppVM1로 모든 트래픽(모든 포트) 허용됨</span><span class="sxs-lookup"><span data-stu-id="19694-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="19694-141">인터넷에서 전체 VNet(두 서브넷)으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="19694-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="19694-142">프런트 엔드 서브넷에서 백 엔드 서브넷으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="19694-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="19694-143">각 서브넷에 바인딩된 이러한 규칙에서는 HTTP 요청이 인터넷에서 웹 서버로 인바운드되는 경우 규칙 3(허용) 및 5(거부)가 모두 적용되지만 규칙 3이 우선순위가 높기 때문에 규칙 3만 적용되고 규칙 5는 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="19694-144">따라서 웹 서버에 대해 HTTP 요청이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="19694-145">동일한 트래픽이 DNS01 서버에 도달하려고 시도하는 경우 규칙 5(거부)는 가장 먼저 적용되며 트래픽을 서버에 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="19694-146">규칙 6(거부)은 프런트 엔드 서브넷이 백 엔드 서브넷과 통신하는 것을 차단(규칙 1 및 4에서 허용된 트래픽 제외)하여 공격자가 프런트 엔드에서 웹 응용 프로그램을 손상시키는 경우 공격자의 "보호된" 백 엔드 네트워크(AppVM01 서버에서 노출되는 리소스만)에 대한 액세스가 제한되므로 이 규칙 집합은 백 엔드 네트워크를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="19694-147">인터넷으로 트래픽을 허용하는 기본 아웃바운드 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="19694-148">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="19694-149">양방향에서 트래픽에 보안 정책을 적용하려면 사용자 정의 라우팅이 필요하며 [보안 경계 모범 사례 페이지][HOME]의 "예제 3"에서 이에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="19694-150">각 규칙은 다음과 같이 더 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="19694-151">규칙을 저장하도록 네트워크 보안 그룹 리소스를 인스턴스화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="19694-152">이 예의 첫 번째 규칙에서는 백 엔드 서브넷에서 DNS 서버에 대해 모든 내부 네트워크 간 DNS 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="19694-153">규칙은 몇 가지 중요한 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="19694-154">"destinationAddressPrefix" - 규칙은 "기본 태그"라는 특수한 주소 유형의 접두사를 사용할 수 있습니다. 이러한 태그는 더 큰 범주의 주소 접두사를 해결하는 쉬운 방법을 허용하는 시스템 제공 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="19694-155">이 규칙은 기본 태그 “Internet"을 사용하여 VNet 외의 모든 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="19694-156">다른 접두사 레이블은 VirtualNetwork 및 AzureLoadBalancer입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="19694-157">"Direction"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="19694-158">방향은 서브넷 또는 가상 컴퓨터의 관점에서 옵니다(이 NSG가 바인딩되는 위치에 따라).</span><span class="sxs-lookup"><span data-stu-id="19694-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="19694-159">따라서 Direction이 "Inbound"이고 트래픽이 서브넷에 들어가는 경우 규칙이 적용되고 서브넷에서 나가는 트래픽에는 이 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="19694-160">"Priority"는 트래픽 흐름이 평가되는 순서를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="19694-161">번호가 낮을수록 우선순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="19694-162">특정 트래픽 흐름에 규칙이 적용되는 경우 더 이상 규칙이 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="19694-163">따라서 우선순위 1인 규칙에서는 트래픽을 허용하고 우선순위 2인 규칙에서는 트래픽을 거부하고 두 규칙 모두 트래픽에 적용된다면 트래픽 흐름이 허용됩니다(규칙 1의 우선순위가 높으므로 해당 규칙이 적용되고 다른 규칙은 적용되지 않음).</span><span class="sxs-lookup"><span data-stu-id="19694-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="19694-164">"Access"는 이 규칙의 영향을 받는 트래픽을 차단("Deny")하거나 허용("Allow")할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="19694-165">이 규칙은 RDP 트래픽이 인터넷에서 바인딩된 서브넷에 있는 모든 서버의 RDP 포트로 흐르도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="19694-166">이 규칙은 웹 서버를 호출하기 위해 인바운드 인터넷 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="19694-167">이 규칙은 라우팅 동작을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="19694-168">규칙은 IIS01을 대상으로 하는 트래픽만을 전달하도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="19694-169">따라서 인터넷에서 트래픽이 이 규칙에서 허용하는 대상으로 웹 서버를 포함하는 경우 추가 규칙의 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="19694-170">(우선순위 140의 규칙에서 모든 다른 인바운드 인터넷 트래픽이 차단됩니다.)</span><span class="sxs-lookup"><span data-stu-id="19694-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="19694-171">HTTP 트래픽만 처리하는 경우 대상 포트 80만 허용하도록 이 규칙을 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="19694-172">이 규칙은 IIS01 서버에서 AppVM01 서버로 트래픽 전달을 허용합니다. 이후 규칙은 백 엔드 트래픽에 대한 모든 다른 프런트엔드를 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="19694-173">추가해야 할 포트를 알고 있다면 이 규칙을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="19694-174">예를 들어, IIS 서버가 AppVM01에서 SQL Server만 연결하는 경우 대상 포트 범위를 "*"(모두)에서 1433(SQL 포트)으로 변경해야 하므로 AppVM01에서 웹 응용 프로그램이 손상될 수 있는 인바운드 공격에 대한 취약성을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="19694-175">이 규칙은 네트워크 상의 모든 서버에 인터넷에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="19694-176">우선순위 110 및 120의 규칙을 사용하여 방화벽에 대한 인바운드 인터넷 트래픽 및 서버의 RDP 포트만 허용하고 다른 모든 항목은 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="19694-177">이 규칙은 모든 예기치 않은 흐름을 차단하는 "유사 시 대기" 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="19694-178">마지막 규칙은 프런트엔드 서브넷에서 백 엔드 서브넷으로 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="19694-179">이 규칙은 인바운드 전용 규칙이므로 역방향 트래픽이 허용됩니다(백 엔드에서 프런트 엔드로).</span><span class="sxs-lookup"><span data-stu-id="19694-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="19694-180">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="19694-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="19694-181">(*허용*) 인터넷에서 웹 서버</span><span class="sxs-lookup"><span data-stu-id="19694-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="19694-182">인터넷 사용자는 IIS01 NIC와 연결된 NIC의 공용 IP 주소에서 HTTP 페이지를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="19694-183">공용 IP 주소는 IIS01 쪽으로 VNet에 트래픽을 전달합니다(웹 서버).</span><span class="sxs-lookup"><span data-stu-id="19694-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="19694-184">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-185">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="19694-186">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="19694-187">NSG 규칙 3(인터넷에서 IIS01로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="19694-188">트래픽이 웹 서버 IIS01의 내부 IP 주소를 호출합니다(10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="19694-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="19694-189">IIS01이 웹 트래픽을 수신 대기하고 이 요청을 수신하며 요청 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="19694-190">IIS01은 AppVM01에서 SQL Server에 정보를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="19694-191">프런트엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="19694-192">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-193">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="19694-194">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="19694-195">NSG 규칙 3(인터넷에서 방화벽으로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="19694-196">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="19694-197">AppVM01은 SQL 쿼리를 수신하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="19694-198">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="19694-199">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-200">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="19694-201">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="19694-202">IIS 서버는 SQL 응답을 수신하고 HTTP 응답을 완료하여 요청자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="19694-203">응답이 허용되는 프런트 엔드 서브넷에 아웃바운드 규칙이 없으므로 인터넷 사용자는 요청된 웹 페이지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="19694-204">(*허용*) RDP에서 IIS 서버</span><span class="sxs-lookup"><span data-stu-id="19694-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="19694-205">인터넷에서 서버 관리자는 IIS01 NIC와 연결된 NIC의 공용 IP 주소에서 IIS01에 대한 RDP 세션을 요청합니다(이 공용 IP 주소는 포털 또는 PowerShell을 통해 찾을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="19694-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="19694-206">공용 IP 주소는 IIS01 쪽으로 VNet에 트래픽을 전달합니다(웹 서버).</span><span class="sxs-lookup"><span data-stu-id="19694-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="19694-207">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-208">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="19694-209">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="19694-210">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="19694-211">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-211">RDP session is enabled</span></span>
6. <span data-ttu-id="19694-212">IIS01에서 사용자 이름과 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
><span data-ttu-id="19694-213">이 인스턴스의 백 엔드 서버에 RDP하려면 IIS 서버는 "점프 상자"로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-213">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="19694-214">먼저 RDP에서 IIS 서버로 그 다음에 IIS 서버 RDP에서 백 엔드 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-214">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="19694-215">(*허용*) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="19694-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="19694-216">웹 서버인 IIS01은 www.data.gov에서 데이터 피드를 요구하지만 주소를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="19694-217">VNet에 대한 네트워크 구성에서 DNS01(백 엔드 서브넷에서 10.0.2.4)을 주 DNS 서버로 나열하며 IIS01은 DNS01로 DNS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="19694-218">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="19694-219">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="19694-220">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="19694-221">DNS 서버는 요청을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-221">DNS server receives the request</span></span>
6. <span data-ttu-id="19694-222">DNS 서버에는 캐시된 주소가 없고 인터넷에서 루트 DNS 서버를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="19694-223">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="19694-224">이 세션은 내부적으로 시작되었으므로 인터넷 DNS 서버가 응답하고 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="19694-225">DNS 서버는 응답을 캐시하고 IIS01에 대한 초기 요청에 다시 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="19694-226">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="19694-227">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-228">백 엔드 서브넷에서 프런트 엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="19694-229">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙에서 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="19694-230">IIS01이 DNS01에서 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="19694-231">(*허용*) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="19694-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="19694-232">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="19694-233">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="19694-234">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-235">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="19694-236">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="19694-237">NSG 규칙 3(인터넷에서 IIS01로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="19694-238">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="19694-239">AppVM01이 요청을 받아 파일로 응답합니다(액세스 권한이 부여된 것으로 가정).</span><span class="sxs-lookup"><span data-stu-id="19694-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="19694-240">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="19694-241">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-242">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="19694-243">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="19694-244">IIS 서버가 파일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="19694-245">(*거부*) RDP - 백 엔드</span><span class="sxs-lookup"><span data-stu-id="19694-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="19694-246">인터넷 사용자가 서버 AppVM01로 RDP하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="19694-247">이 서버 NIC와 연결된 공용 IP 주소가 없으므로 이 트래픽은 VNet을 입력할 수 없고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="19694-248">그러나 어떤 이유로 공용 IP 주소가 활성화된 경우 NSG 규칙 2(RP)는 이 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="19694-249">이 인스턴스의 백 엔드 서버에 RDP하려면 IIS 서버는 "점프 상자"로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-249">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="19694-250">먼저 RDP에서 IIS 서버로 그 다음에 IIS 서버 RDP에서 백 엔드 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-250">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="19694-251">(*거부*) 웹 - 백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="19694-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="19694-252">인터넷 사용자가 AppVM01에 있는 파일에 액세스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="19694-253">이 서버 NIC와 연결된 공용 IP 주소가 없으므로 이 트래픽은 VNet을 입력할 수 없고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="19694-254">어떤 이유로 공용 IP 주소가 활성화된 경우 NSG 규칙 5(인터넷에서 VNet으로)는 이 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="19694-255">(*거부*) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="19694-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="19694-256">인터넷 사용자가 DNS01에 있는 내부 DNS 레코드를 조회하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="19694-257">이 서버 NIC와 연결된 공용 IP 주소가 없으므로 이 트래픽은 VNet을 입력할 수 없고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="19694-258">어떤 이유로 공용 IP 주소가 활성화된 경우 NSG 규칙 5(인터넷에서 VNet으로)는 이 트래픽을 차단합니다.(참고: 요청 원본 주소는 인터넷이며 규칙 1은 원본으로 로컬 VNet에만 적용되므로 해당 규칙 1(DNS)은 적용되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="19694-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="19694-259">(*거부*) 웹 서버에서 SQL 액세스</span><span class="sxs-lookup"><span data-stu-id="19694-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="19694-260">인터넷 사용자가 IIS01에서 SQL 데이터를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="19694-261">이 서버 NIC와 연결된 공용 IP 주소가 없으므로 이 트래픽은 VNet을 입력할 수 없고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="19694-262">어떤 이유로 공용 IP 주소가 활성화된 경우 프런트 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="19694-263">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="19694-264">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="19694-265">NSG 규칙 3(인터넷에서 IIS01로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="19694-266">트래픽이 IIS01의 내부 IP 주소를 호출합니다(10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="19694-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="19694-267">IIS01이 포트 1433에서 수신 대기하지 않으므로 요청에 대한 응답이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="19694-268">결론</span><span class="sxs-lookup"><span data-stu-id="19694-268">Conclusion</span></span>
<span data-ttu-id="19694-269">이 예제는 백 엔드 서브넷을 인바운드 트래픽과 격리하는 비교적 간단하고 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="19694-270">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="19694-271">참조</span><span class="sxs-lookup"><span data-stu-id="19694-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="19694-272">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="19694-272">Azure Resource Manager template</span></span>
<span data-ttu-id="19694-273">이 예제는 Microsoft에서 유지 관리하는 GitHub 리포지토리에서 미리 정의된 Azure Resource Manager 템플릿을 사용하고 해당 커뮤니티를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="19694-274">이 템플릿은 GitHub에서 바로 배포하거나 다운로드한 후 필요에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="19694-275">기본 템플릿은 “azuredeploy.json”이라는 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="19694-276">이 템플릿을 배포하도록 PowerShell 또는 CLI를 통해 제출할 수 있습니다(연결된 "azuredeploy.parameters.json" 파일과 함께).</span><span class="sxs-lookup"><span data-stu-id="19694-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="19694-277">가장 쉬운 방법은 GitHub에서 README.md 페이지의 "Azure에 배포" 단추를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="19694-278">GitHub 및 Azure Portal에서 이 예제를 작성하는 템플릿을 배포하려면 이 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="19694-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="19694-279">브라우저에서 [템플릿][Template]으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="19694-280">"Azure에 배포" 단추(또는 이 템플릿의 그래픽 표시를 보려면 "시각화" 단추)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="19694-281">매개 변수 블레이드에서 저장소 계정, 사용자 이름 및 암호를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="19694-282">이 배포에 대한 리소스 그룹을 만듭니다.(기존 것을 사용할 수 있지만 최상의 결과를 위해 새 것을 권장합니다.)</span><span class="sxs-lookup"><span data-stu-id="19694-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="19694-283">필요한 경우 VNet에 맞게 구독 및 위치 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="19694-284">**약관 검토**를 클릭하고 약관을 읽은 후 **구입**을 클릭하여 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="19694-285">**만들기**를 클릭하여 이 템플릿의 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="19694-286">배포가 성공적으로 완료되면 내부에서 구성된 리소스를 보기 위해 이 배포에 대해 만든 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="19694-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="19694-287">이 템플릿을 통해 IIS01 서버로 RDP할 수 있습니다(포털에서 IIS01에 대한 공용 IP 찾기).</span><span class="sxs-lookup"><span data-stu-id="19694-287">This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal).</span></span> <span data-ttu-id="19694-288">이 인스턴스의 백 엔드 서버에 RDP하려면 IIS 서버는 "점프 상자"로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-288">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="19694-289">먼저 RDP에서 IIS 서버로 그 다음에 IIS 서버 RDP에서 백 엔드 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="19694-289">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

<span data-ttu-id="19694-290">이 배포를 제거하려면 리소스 그룹을 삭제합니다. 모든 자식 리소스도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="19694-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="19694-291">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="19694-291">Sample application scripts</span></span>
<span data-ttu-id="19694-292">템플릿이 성공적으로 실행되면 간단한 웹 응용 프로그램을 사용하는 웹 서버와 앱 서버를 설정하여 이 DMZ 구성을 이용한 테스트를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19694-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="19694-293">이에 대한 샘플 응용 프로그램 및 기타 DMZ 예제를 설치하는 방법은 다음 링크를 통해 제공됩니다. [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="19694-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="19694-294">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19694-294">Next steps</span></span>

* <span data-ttu-id="19694-295">이 예제 배포</span><span class="sxs-lookup"><span data-stu-id="19694-295">Deploy this example</span></span>
* <span data-ttu-id="19694-296">샘플 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="19694-296">Build the sample application</span></span>
* <span data-ttu-id="19694-297">이 DMZ를 통해 다양한 트래픽 흐름 테스트</span><span class="sxs-lookup"><span data-stu-id="19694-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="19694-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "NSG와 인바운드 DMZ"</span><span class="sxs-lookup"><span data-stu-id="19694-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md