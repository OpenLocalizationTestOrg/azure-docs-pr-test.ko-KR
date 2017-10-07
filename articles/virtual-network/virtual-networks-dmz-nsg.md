---
title: "DMZ 예 – aaaAzure 빌드 Nsg와 단순 DMZ | Microsoft Docs"
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
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="e4bcd-103">예 1 – Azure Resource Manager 템플릿으로 NSG를 사용하여 간단한 DMZ 빌드</span><span class="sxs-lookup"><span data-stu-id="e4bcd-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="e4bcd-104">[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4bcd-105">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4bcd-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="e4bcd-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4bcd-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="e4bcd-107">이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="e4bcd-108">이 예에서는 각 hello 관련 템플릿 섹션 tooprovide 각 단계에 대 한 깊은 이해가 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="e4bcd-109">이기도 트래픽 시나리오 섹션 tooprovide 단계별 자세히 배우려면 hello DMZ에에서는 심층적인 방어의 hello 계층을 통해 트래픽을 처리할 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="e4bcd-110">마지막으로 hello references 섹션에는 hello 완전 한 템플릿 코드와 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="e4bcd-111">![NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="e4bcd-112">환경 설명</span><span class="sxs-lookup"><span data-stu-id="e4bcd-112">Environment description</span></span>
<span data-ttu-id="e4bcd-113">이 예에서 구독 리소스를 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="e4bcd-114">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="e4bcd-114">A single resource group</span></span>
* <span data-ttu-id="e4bcd-115">두 서브넷 “프런트 엔드” 및 “백 엔드”를 사용하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="e4bcd-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="e4bcd-116">적용 된 tooboth 서브넷은 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="e4bcd-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="e4bcd-117">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="e4bcd-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="e4bcd-118">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="e4bcd-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="e4bcd-119">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="e4bcd-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="e4bcd-120">Hello 응용 프로그램 웹 서버와 관련 된 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e4bcd-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="e4bcd-121">Hello references 섹션에는이 예제에서 설명 하는 hello 환경 구축 하 링크 tooan Azure 리소스 관리자 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="e4bcd-122">건물 hello Vm 및 가상 네트워크를 hello 예제 서식 파일에서 수행 되지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="e4bcd-123">**toobuild이이 환경** (자세한 지침은이 문서의 hello references 섹션에는);</span><span class="sxs-lookup"><span data-stu-id="e4bcd-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="e4bcd-124">배포 시 Azure 리소스 관리자 템플릿을 hello: [Azure 빠른 시작 템플릿][Template]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="e4bcd-125">시 hello 샘플 응용 프로그램 설치: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="e4bcd-126">이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="e4bcd-127">첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="e4bcd-128">또는 공용 IP는 보다 쉬운 RDP를 위해 각 서버 NIC와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="e4bcd-129">hello 다음 섹션에서는 hello 네트워크 보안 그룹 및 Azure 리소스 관리자 템플릿을 hello 키 줄을 살펴보는 방법으로이 예제에 대 한 작동 방식이 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="e4bcd-130">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="e4bcd-131">이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="e4bcd-132">일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="e4bcd-133">우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="e4bcd-134">트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="e4bcd-135">NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="e4bcd-136">선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:</span><span class="sxs-lookup"><span data-stu-id="e4bcd-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="e4bcd-137">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="e4bcd-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="e4bcd-138">RDP 트래픽 (포트 3389 hello 인터넷 tooany VM에서 에서) 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="e4bcd-139">Hello 인터넷 tooweb 서버 (IIS01)에서 HTTP 트래픽 (포트 80)가 허용</span><span class="sxs-lookup"><span data-stu-id="e4bcd-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="e4bcd-140">(모든 포트) IIS01 tooAppVM1에서 모든 트래픽을 허용합니다</span><span class="sxs-lookup"><span data-stu-id="e4bcd-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="e4bcd-141">전체 VNet (두 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="e4bcd-142">Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="e4bcd-143">이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청 hello 인터넷 toohello 웹 서버 로부터 언바운드 하지 않은 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것을 히 규칙 3 보다 우선 순위가 규칙 5는 하지 고려해 야 하 고 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="e4bcd-144">따라서 toohello 웹 서버 hello HTTP 요청 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="e4bcd-145">동일한 트래픽이 해당 tooreach hello DNS01 서버를 시도 하 고, 규칙 5 (거부) hello 첫 번째 tooapply 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="e4bcd-146">규칙 6 (거부) hello 프런트 엔드 서브넷 통하게 (규칙 1 및 4에서에서 허용 된 트래픽)를 제외한 toohello 백 엔드 서브넷의 차단,이 규칙 집합 hello 백 엔드 네트워크를 보호는 공격자가 손상 hello에서 웹 응용 프로그램 hello 프런트 엔드, hello 공격자가 경우 백 엔드 "보호" (만 hello AppVM01 서버에서 노출 tooresources) 네트워크 액세스 toohello를 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="e4bcd-147">Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="e4bcd-148">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="e4bcd-149">양방향에서 tooapply 보안 정책 tootraffic, 사용자 정의 된 라우팅 필수 이며 hello에 "예 3"에 대해서는 [보안 경계 모범 사례 페이지][HOME]합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="e4bcd-150">각 규칙은 다음과 같이 더 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="e4bcd-151">네트워크 보안 그룹 리소스 인스턴스화된 toohold hello 규칙 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

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

2. <span data-ttu-id="e4bcd-152">이 예에서 첫 번째 규칙 hello hello 백 엔드 서브넷에 있는 모든 내부 네트워크 toohello DNS 서버 간의 DNS 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="e4bcd-153">hello 규칙에 몇 가지 중요 한 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="e4bcd-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="e4bcd-154">이러한 태그는 쉽게 tooaddress 주소 접두사의 더 큰 범주를 허용 하는 시스템 제공 식별자를 "destinationAddressPrefix"-규칙 주소 접두사 "기본 태그" 라는 특수 한 유형의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="e4bcd-155">이 규칙을 사용 하 여 기본 태그 "Internet" hello toosignify hello VNet 외부에서 모두 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="e4bcd-156">다른 접두사 레이블은 VirtualNetwork 및 AzureLoadBalancer입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="e4bcd-157">"Direction"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="e4bcd-158">hello 방향은 (에 따라이 NSG 바인딩되는) hello 서브넷 또는 가상 컴퓨터의 hello 관점에서입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="e4bcd-159">따라서 경우 방향은 "Inbound" 및 트래픽 hello 서브넷을 시작 하는, hello 규칙 적용 및이 규칙에 의해 내보내는 hello 서브넷을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="e4bcd-160">"Priority" 트래픽 흐름을 확인 하는 hello 순서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="e4bcd-161">hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="e4bcd-162">Tooa 특정 트래픽 흐름을 적용 하는 규칙을 더 이상 규칙이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="e4bcd-163">따라서 우선 순위 1의 규칙이 트래픽이 우선 순위가 2 인 규칙 트래픽을, 거부 및 규칙이 모두 적용 tootraffic 경우 hello 트래픽 tooflow 것은 허용 (규칙 1 한 우선 순위가 높은 이후 효과 데 걸린 및 적용 된 규칙이 더 이상 없음).</span><span class="sxs-lookup"><span data-stu-id="e4bcd-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="e4bcd-164">"Access"는 이 규칙의 영향을 받는 트래픽을 차단("Deny")하거나 허용("Allow")할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="e4bcd-165">이 규칙은 모든 서버 hello에 hello toohello RDP 포트를 인터넷에서 RDP 트래픽 tooflow 바인딩된 서브넷 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

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

4. <span data-ttu-id="e4bcd-166">이 규칙은 toohit hello 웹 서버에 대 한 인바운드의 인터넷 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="e4bcd-167">이 규칙 hello 라우팅 동작을 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="e4bcd-168">hello 규칙 IIS01 toopass 향하는 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="e4bcd-169">따라서이 규칙은 허용 하 고 규칙은 추가 처리를 중지 대상으로 hello 인터넷 트래픽만 hello 웹 서버를 갖는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="e4bcd-170">(우선 순위에서 hello 규칙에 140 모든 다른 인바운드 인터넷 트래픽을 차단).</span><span class="sxs-lookup"><span data-stu-id="e4bcd-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="e4bcd-171">이 규칙 HTTP 트래픽을 처리 하는 경우 추가 될 수 제한 tooonly 대상 포트 80을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
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

5. <span data-ttu-id="e4bcd-172">이 규칙은 toohello AppVM01 서버 트래픽을 toopass hello IIS01 서버에서 허용, 이후 규칙은 다른 모든 프런트 엔드 tooBackend 트래픽을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="e4bcd-173">tooimprove hello 포트를 식별 하는 경우이 규칙을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="e4bcd-174">예를 들어 hello IIS 서버 AppVM01에 SQL Server 작업 부하는 hello 대상 포트 범위 변경 해야에서 "*" (모두) too1433 (hello SQL 포트) 되므로 AppVM01에서 더 작은 인바운드 공격 노출 해야 hello 웹 응용 프로그램 적이 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
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

6. <span data-ttu-id="e4bcd-175">이 규칙 hello 인터넷 tooany 서버 hello 네트워크에서에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="e4bcd-176">110 및 120 우선 순위에서 hello 규칙을 사용 hello 효과 tooallow만 인바운드 인터넷 트래픽 toohello 방화벽 및 서버 모두에서 RDP 포트 이며 다른 모든 것을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="e4bcd-177">이 규칙은 "유사시 대기" 규칙 tooblock 모든 예기치 않은 흐름.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
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

7. <span data-ttu-id="e4bcd-178">hello 최종 규칙 hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="e4bcd-179">이 규칙에만 인바운드 규칙 이므로 (hello 백 엔드 toohello 프런트 엔드)에서 역방향 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
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

## <a name="traffic-scenarios"></a><span data-ttu-id="e4bcd-180">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="e4bcd-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="e4bcd-181">(*허용*) 인터넷 tooweb 서버</span><span class="sxs-lookup"><span data-stu-id="e4bcd-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="e4bcd-182">인터넷 사용자 hello hello IIS01 NIC와 관련 된 NIC의 hello 공용 IP 주소에서 HTTP 페이지 요청</span><span class="sxs-lookup"><span data-stu-id="e4bcd-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="e4bcd-183">공용 IP 주소 hello 전달 트래픽 toohello IIS01 쪽으로 VNet (hello 웹 서버)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="e4bcd-184">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-185">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="e4bcd-186">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="e4bcd-187">NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="e4bcd-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e4bcd-188">트래픽 (10.0.1.5) hello 웹 서버의 IIS01 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="e4bcd-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="e4bcd-189">IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다</span><span class="sxs-lookup"><span data-stu-id="e4bcd-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="e4bcd-190">IIS01 정보 AppVM01에 SQL Server hello를 요청</span><span class="sxs-lookup"><span data-stu-id="e4bcd-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="e4bcd-191">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="e4bcd-192">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="e4bcd-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-193">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="e4bcd-194">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="e4bcd-195">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="e4bcd-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="e4bcd-196">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="e4bcd-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="e4bcd-197">AppVM01 hello SQL 쿼리를 받아 응답</span><span class="sxs-lookup"><span data-stu-id="e4bcd-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="e4bcd-198">Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우</span><span class="sxs-lookup"><span data-stu-id="e4bcd-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="e4bcd-199">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-200">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="e4bcd-201">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="e4bcd-202">hello IIS 서버 hello SQL 응답 및 hello HTTP 응답을 완료를 주고받는 toohello 요청자</span><span class="sxs-lookup"><span data-stu-id="e4bcd-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="e4bcd-203">Hello 프런트 엔드 서브넷에 아웃 바운드 규칙이 있기 때문에 hello 응답이 허용 하 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="e4bcd-204">(*허용*) RDP tooIIS 서버</span><span class="sxs-lookup"><span data-stu-id="e4bcd-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="e4bcd-205">인터넷에서 서버 관리자는 RDP 세션 tooIIS01 hello hello IIS01 NIC (이 공용 IP 주소 hello 포털 또는 PowerShell을 통해 찾을 수 있습니다)와 연결 된 NIC는 hello 공용 IP 주소에서 요청</span><span class="sxs-lookup"><span data-stu-id="e4bcd-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="e4bcd-206">공용 IP 주소 hello 전달 트래픽 toohello IIS01 쪽으로 VNet (hello 웹 서버)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="e4bcd-207">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-208">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="e4bcd-209">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e4bcd-210">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="e4bcd-211">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-211">RDP session is enabled</span></span>
6. <span data-ttu-id="e4bcd-212">Hello 사용자 이름 및 암호에 대 한 IIS01 프롬프트</span><span class="sxs-lookup"><span data-stu-id="e4bcd-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="e4bcd-213">이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="e4bcd-214">첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="e4bcd-215">(*허용*) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="e4bcd-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="e4bcd-216">웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="e4bcd-217">hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="e4bcd-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="e4bcd-218">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="e4bcd-219">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="e4bcd-220">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="e4bcd-221">DNS 서버 hello 요청 수신</span><span class="sxs-lookup"><span data-stu-id="e4bcd-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="e4bcd-222">DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷</span><span class="sxs-lookup"><span data-stu-id="e4bcd-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="e4bcd-223">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="e4bcd-224">이 세션은 내부적으로 시작 된 이후 인터넷 DNS 서버 응답을 hello 응답이 허용</span><span class="sxs-lookup"><span data-stu-id="e4bcd-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="e4bcd-225">DNS 서버 hello 응답을 캐시 및 toohello 초기 요청 백 tooIIS01 이벤트에 응답</span><span class="sxs-lookup"><span data-stu-id="e4bcd-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="e4bcd-226">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="e4bcd-227">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-228">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="e4bcd-229">hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용</span><span class="sxs-lookup"><span data-stu-id="e4bcd-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="e4bcd-230">IIS01은 DNS01에서 hello 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="e4bcd-231">(*허용*) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="e4bcd-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="e4bcd-232">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="e4bcd-233">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="e4bcd-234">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="e4bcd-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-235">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="e4bcd-236">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="e4bcd-237">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooIIS01) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="e4bcd-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="e4bcd-238">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="e4bcd-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e4bcd-239">AppVM01은 hello 요청을 받아 파일 (액세스 권한이 부여 가정)를 사용 하 여 응답</span><span class="sxs-lookup"><span data-stu-id="e4bcd-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="e4bcd-240">Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우</span><span class="sxs-lookup"><span data-stu-id="e4bcd-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="e4bcd-241">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-242">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="e4bcd-243">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="e4bcd-244">hello IIS 서버 hello 파일 수신</span><span class="sxs-lookup"><span data-stu-id="e4bcd-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="e4bcd-245">(*Denied*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="e4bcd-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="e4bcd-246">인터넷 사용자가 tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="e4bcd-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="e4bcd-247">이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="e4bcd-248">그러나 어떤 이유로 공용 IP 주소가 활성화된 경우 NSG 규칙 2(RP)는 이 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="e4bcd-249">이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="e4bcd-250">첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="e4bcd-251">(*Denied*) 웹 toobackend 서버</span><span class="sxs-lookup"><span data-stu-id="e4bcd-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="e4bcd-252">인터넷 사용자가 tooaccess AppVM01에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="e4bcd-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="e4bcd-253">이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="e4bcd-254">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 공용 IP 주소를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="e4bcd-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="e4bcd-255">(*거부*) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="e4bcd-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="e4bcd-256">인터넷 사용자가 toolook DNS01에는 내부 DNS 레코드를</span><span class="sxs-lookup"><span data-stu-id="e4bcd-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="e4bcd-257">이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="e4bcd-258">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 공용 IP 주소를 사용 하는 경우 (참고: 인터넷 hello 및 toohello 규칙 1에만 적용 됩니다는 규칙 1 (DNS) hello 소스 주소를 요청 하기 때문에 적용 되지 않습니다 hello 소스로 지역 VNet)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="e4bcd-259">(*Denied*) hello 웹 서버에 대 한 SQL 액세스</span><span class="sxs-lookup"><span data-stu-id="e4bcd-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="e4bcd-260">인터넷 사용자가 IIS01에서 SQL 데이터를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="e4bcd-261">이 서버 NIC와 관련 된 공용 IP 주소가 없는 있을 경우이 VNet hello 입력할 수 없고 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="e4bcd-262">몇 가지 이유로 공용 IP 주소를 사용 하는 경우 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="e4bcd-263">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="e4bcd-264">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="e4bcd-265">NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="e4bcd-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="e4bcd-266">트래픽 (10.0.1.5) hello IIS01의 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="e4bcd-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="e4bcd-267">IIS01 하지 않게 응답 toohello 요청 포트 1433에서 수신 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="e4bcd-268">결론</span><span class="sxs-lookup"><span data-stu-id="e4bcd-268">Conclusion</span></span>
<span data-ttu-id="e4bcd-269">이 예제는 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 쉽고 명확한 방법.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="e4bcd-270">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="e4bcd-271">참조</span><span class="sxs-lookup"><span data-stu-id="e4bcd-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="e4bcd-272">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4bcd-272">Azure Resource Manager template</span></span>
<span data-ttu-id="e4bcd-273">이 예제는 Microsoft에서 관리 하는 GitHub 리포지토리에 미리 정의 된 Azure 리소스 관리자 템플릿을 사용 하 고 toohello 커뮤니티를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="e4bcd-274">이 템플릿은 GitHub에서 배포할 수 있습니다 또는 다운로드 하 고 toofit 요구에 맞게 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="e4bcd-275">hello 기본 서식 파일은 "azuredeploy.json." 라는 hello 파일에</span><span class="sxs-lookup"><span data-stu-id="e4bcd-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="e4bcd-276">이 서식 파일 (hello 관련된 "azuredeploy.parameters.json" 파일)와 PowerShell 또는 CLI를 통해 제출할 수 toodeploy이 서식이 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="e4bcd-277">I 찾을 hello 가장 쉬운 방법은 toouse hello GitHub에서 hello README.md 페이지에서 "배포 tooAzure" 단추 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="e4bcd-278">toodeploy hello 템플릿을 GitHub 및 hello Azure 포털에서이 예제를 작성 하는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="e4bcd-279">브라우저에서 탐색 toohello [서식 파일][Template]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="e4bcd-280">Hello "배포 tooAzure" 단추 (또는 hello "시각화" 단추 toosee이 서식이 파일의 그래픽 표현)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="e4bcd-281">Hello 매개 변수 블레이드에서 hello 저장소 계정, 사용자 이름 및 암호를 입력 한 다음 클릭 **확인**</span><span class="sxs-lookup"><span data-stu-id="e4bcd-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="e4bcd-282">이 배포에 대한 리소스 그룹을 만듭니다.(기존 것을 사용할 수 있지만 최상의 결과를 위해 새 것을 권장합니다.)</span><span class="sxs-lookup"><span data-stu-id="e4bcd-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="e4bcd-283">필요한 경우 VNet에 대 한 hello 구독 및 위치 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="e4bcd-284">클릭 **약관을 검토**hello 조건을 읽고 클릭 **구매** tooagree 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="e4bcd-285">클릭 **만들기** 이 서식 파일의 toobegin hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="e4bcd-286">Hello 배포 성공적으로 완료 되 면 리소스 그룹 내에 구성할이 배포 toosee hello 리소스에 대해 생성 toohello를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="e4bcd-287">이 템플릿을 사용 하 여 RDP toohello IIS01 서버만 (찾기 hello IIS01에 대 한 공용 IP hello 포털에).</span><span class="sxs-lookup"><span data-stu-id="e4bcd-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="e4bcd-288">이 경우 IIS 서버 hello tooRDP tooany 백 엔드 서버 "점프 상자입니다."로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="e4bcd-289">첫 번째 RDP toohello IIS 서버 hello IIS 서버 RDP toohello 백 엔드 서버에서 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="e4bcd-290">tooremove 배포, delete hello이 리소스 그룹 및 모든 자식 리소스가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="e4bcd-291">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="e4bcd-291">Sample application scripts</span></span>
<span data-ttu-id="e4bcd-292">Hello 템플릿을 성공적으로 실행 되 면이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 hello 웹 서버 및 응용 프로그램 서버를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4bcd-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="e4bcd-293">이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 제공 된다는 링크 hello에: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="e4bcd-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4bcd-294">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4bcd-294">Next steps</span></span>

* <span data-ttu-id="e4bcd-295">이 예제 배포</span><span class="sxs-lookup"><span data-stu-id="e4bcd-295">Deploy this example</span></span>
* <span data-ttu-id="e4bcd-296">Hello 샘플 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="e4bcd-296">Build hello sample application</span></span>
* <span data-ttu-id="e4bcd-297">이 DMZ를 통해 다양한 트래픽 흐름 테스트</span><span class="sxs-lookup"><span data-stu-id="e4bcd-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "NSG와 인바운드 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md