---
title: "DMZ 예 – aaaAzure 빌드 Nsg와 단순 DMZ | Microsoft Docs"
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
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="3761d-103">예제 1 – 클래식 PowerShell로 NSG를 사용하여 간단한 DMZ 빌드</span><span class="sxs-lookup"><span data-stu-id="3761d-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="3761d-104">[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]</span><span class="sxs-lookup"><span data-stu-id="3761d-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3761d-105">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3761d-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="3761d-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="3761d-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="3761d-107">이 예에서는 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 기본 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="3761d-108">이 예에서는 각 hello 관련 PowerShell 명령 tooprovide 각 단계에 대 한 깊은 이해가 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="3761d-109">이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="3761d-110">마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="3761d-111">![NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="3761d-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="3761d-112">환경 설명</span><span class="sxs-lookup"><span data-stu-id="3761d-112">Environment description</span></span>
<span data-ttu-id="3761d-113">이 예에서 구독 리소스를 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="3761d-114">두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="3761d-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="3761d-115">"FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"</span><span class="sxs-lookup"><span data-stu-id="3761d-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="3761d-116">적용 된 tooboth 서브넷은 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="3761d-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="3761d-117">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="3761d-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="3761d-118">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="3761d-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="3761d-119">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="3761d-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="3761d-120">Hello references 섹션에는 PowerShell 스크립트의이 예제에서 설명 하는 hello 환경 대부분 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="3761d-121">건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="3761d-122">toobuild hello 환경</span><span class="sxs-lookup"><span data-stu-id="3761d-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="3761d-123">Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장</span><span class="sxs-lookup"><span data-stu-id="3761d-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="3761d-124">Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행</span><span class="sxs-lookup"><span data-stu-id="3761d-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="3761d-125">PowerShell에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="3761d-126">hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="3761d-127">Hello 스크립트 실행이 성공적으로 추가 되 면 선택적 단계를 수행 합니다, 그리고 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.</span><span class="sxs-lookup"><span data-stu-id="3761d-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="3761d-128">hello 다음 섹션에서는 네트워크 보안 그룹 및이 예제에 대 한 키 줄의 hello PowerShell 스크립트를 통해 탐색 하 여 작동 방식을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="3761d-129">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="3761d-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="3761d-130">이 예제에서는 NSG 그룹을 빌드한 후 6개의 규칙을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="3761d-131">일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="3761d-132">우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="3761d-133">트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="3761d-134">NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="3761d-135">선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:</span><span class="sxs-lookup"><span data-stu-id="3761d-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="3761d-136">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="3761d-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="3761d-137">RDP 트래픽 (포트 3389 hello 인터넷 tooany VM에서 에서) 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="3761d-138">Hello 인터넷 tooweb 서버 (IIS01)에서 HTTP 트래픽 (포트 80)가 허용</span><span class="sxs-lookup"><span data-stu-id="3761d-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="3761d-139">(모든 포트) IIS01 tooAppVM1에서 모든 트래픽을 허용합니다</span><span class="sxs-lookup"><span data-stu-id="3761d-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="3761d-140">전체 VNet (두 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)</span><span class="sxs-lookup"><span data-stu-id="3761d-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="3761d-141">Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="3761d-142">이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청 hello 인터넷 toohello 웹 서버 로부터 언바운드 하지 않은 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것을 히 규칙 3 보다 우선 순위가 규칙 5는 하지 고려해 야 하 고 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="3761d-143">따라서 toohello 웹 서버 hello HTTP 요청 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="3761d-144">동일한 트래픽이 해당 tooreach hello DNS01 서버를 시도 하 고, 규칙 5 (거부) hello 첫 번째 tooapply 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="3761d-145">규칙 6 (거부) hello 프런트 엔드 서브넷 통하게 (규칙 1 및 4에서에서 허용 된 트래픽)를 제외한 toohello 백 엔드 서브넷의 차단,이 규칙 집합 hello 백 엔드 네트워크를 보호는 공격자가 손상 hello에서 웹 응용 프로그램 hello 프런트 엔드, hello 공격자가 경우 백 엔드 "보호" (만 hello AppVM01 서버에서 노출 tooresources) 네트워크 액세스 toohello를 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="3761d-146">Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="3761d-147">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="3761d-148">양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅 필수 이며 hello에 "예 3"에 대해서는 [보안 경계 모범 사례 페이지][HOME]합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="3761d-149">다음과 같이 각 규칙에서 자세히 설명 되어 (**참고**: hello 달러 기호로 시작 하는 목록 다음의 모든 항목 (예: $NSGName)는이 문서의 hello 참조 섹션에 hello 스크립트에서 사용자 정의 변수):</span><span class="sxs-lookup"><span data-stu-id="3761d-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="3761d-150">먼저 네트워크 보안 그룹 toohold hello 규칙 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="3761d-151">이 예에서 첫 번째 규칙 hello hello 백 엔드 서브넷에 있는 모든 내부 네트워크 toohello DNS 서버 간의 DNS 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="3761d-152">hello 규칙에 몇 가지 중요 한 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="3761d-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="3761d-153">"Type"은 이 규칙이 적용되는 트래픽 흐름의 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="3761d-154">hello 방향은 (에 따라이 NSG 바인딩되는) hello 서브넷 또는 가상 컴퓨터의 hello 관점에서입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="3761d-155">따라서 경우 형식이 "Inbound" 및 트래픽 hello 서브넷을 시작 하는, hello 규칙이 적용 되 고이 규칙에 의해 내보내는 hello 서브넷을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="3761d-156">"Priority" 트래픽 흐름을 확인 하는 hello 순서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="3761d-157">hello 낮은 hello 숫자 hello 더 높은 hello 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="3761d-158">Tooa 특정 트래픽 흐름을 적용 하는 규칙을 더 이상 규칙이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="3761d-159">따라서 우선 순위 1의 규칙이 트래픽이 우선 순위가 2 인 규칙 트래픽을, 거부 및 규칙이 모두 적용 tootraffic 경우 hello 트래픽 tooflow 것은 허용 (규칙 1 한 우선 순위가 높은 이후 효과 데 걸린 및 적용 된 규칙이 더 이상 없음).</span><span class="sxs-lookup"><span data-stu-id="3761d-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="3761d-160">"Action"은 이 규칙의 영향을 받는 트래픽을 차단하거나 허용할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="3761d-161">이 규칙은 모든 서버 hello에 hello toohello RDP 포트를 인터넷에서 RDP 트래픽 tooflow 바인딩된 서브넷 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="3761d-162">이 규칙은 "VIRTUAL_NETWORK" 및 "INTERNET"이라는 두 가지 특별한 주소 접두사 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="3761d-163">이러한 태그는 쉽게 tooaddress 주소 접두사의 더 큰 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="3761d-164">이 규칙은 toohit hello 웹 서버에 대 한 인바운드의 인터넷 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="3761d-165">이 규칙 hello 라우팅 동작을 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="3761d-166">hello 규칙 IIS01 toopass 향하는 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="3761d-167">따라서이 규칙은 허용 하 고 규칙은 추가 처리를 중지 대상으로 hello 인터넷 트래픽만 hello 웹 서버를 갖는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="3761d-168">(우선 순위에서 hello 규칙에 140 모든 다른 인바운드 인터넷 트래픽을 차단).</span><span class="sxs-lookup"><span data-stu-id="3761d-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="3761d-169">이 규칙 HTTP 트래픽을 처리 하는 경우 추가 될 수 제한 tooonly 대상 포트 80을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="3761d-170">이 규칙은 toohello AppVM01 서버 트래픽을 toopass hello IIS01 서버에서 허용, 이후 규칙은 다른 모든 프런트 엔드 tooBackend 트래픽을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="3761d-171">tooimprove hello 포트를 식별 하는 경우이 규칙을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="3761d-172">예를 들어 hello IIS 서버 AppVM01에 SQL Server 작업 부하는 hello 대상 포트 범위 변경 해야에서 "*" (모두) too1433 (hello SQL 포트) 되므로 AppVM01에서 더 작은 인바운드 공격 노출 해야 hello 웹 응용 프로그램 적이 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="3761d-173">이 규칙 hello 인터넷 tooany 서버 hello 네트워크에서에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="3761d-174">110 및 120 우선 순위에서 hello 규칙을 사용 hello 효과 tooallow만 인바운드 인터넷 트래픽 toohello 방화벽 및 서버 모두에서 RDP 포트 이며 다른 모든 것을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="3761d-175">이 규칙은 "유사시 대기" 규칙 tooblock 모든 예기치 않은 흐름.</span><span class="sxs-lookup"><span data-stu-id="3761d-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="3761d-176">hello 최종 규칙 hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 트래픽을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="3761d-177">이 규칙에만 인바운드 규칙 이므로 (hello 백 엔드 toohello 프런트 엔드)에서 역방향 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="3761d-178">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="3761d-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="3761d-179">(*허용*) 인터넷 tooweb 서버</span><span class="sxs-lookup"><span data-stu-id="3761d-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="3761d-180">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="3761d-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="3761d-181">서비스 전달 트래픽을 IIS01 쪽으로 포트 80에 대 한 열린 끝점을 통해 클라우드 (hello 웹 서버)</span><span class="sxs-lookup"><span data-stu-id="3761d-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="3761d-182">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-183">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="3761d-184">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="3761d-185">NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="3761d-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3761d-186">트래픽 (10.0.1.5) hello 웹 서버의 IIS01 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="3761d-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="3761d-187">IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다</span><span class="sxs-lookup"><span data-stu-id="3761d-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="3761d-188">IIS01 정보 AppVM01에 SQL Server hello를 요청</span><span class="sxs-lookup"><span data-stu-id="3761d-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="3761d-189">프런트 엔드 서브넷에 아웃바운드 규칙이 없으므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="3761d-190">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="3761d-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-191">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="3761d-192">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="3761d-193">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="3761d-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="3761d-194">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="3761d-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="3761d-195">AppVM01 hello SQL 쿼리를 받아 응답</span><span class="sxs-lookup"><span data-stu-id="3761d-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="3761d-196">Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우</span><span class="sxs-lookup"><span data-stu-id="3761d-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="3761d-197">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="3761d-198">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="3761d-199">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="3761d-200">hello IIS 서버 hello SQL 응답을 수신 하 고 hello HTTP 응답을 완료 및 toohello 요청자에 게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="3761d-201">아웃 바운드 규칙 hello 프런트 엔드 서브넷에 있기 때문 hello 응답 허용 되 고 hello 인터넷 사용자에 게 요청 된 hello 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="3761d-202">(*허용*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="3761d-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="3761d-203">인터넷에서 서버 관리자 요청 BackEnd001.CloudApp.Net:xxxxx 여기서 xxxxx는 RDP tooAppVM01 hello 임의로 할당 된 포트 번호에서 RDP 세션 tooAppVM01 (hello 할당 된 포트를 찾을 수 hello Azure 포털에서 또는 PowerShell을 통해)</span><span class="sxs-lookup"><span data-stu-id="3761d-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="3761d-204">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-205">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="3761d-206">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="3761d-207">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="3761d-208">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-208">RDP session is enabled</span></span>
5. <span data-ttu-id="3761d-209">Hello 사용자 이름 및 암호에 대 한 AppVM01 프롬프트</span><span class="sxs-lookup"><span data-stu-id="3761d-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="3761d-210">(*허용*) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="3761d-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="3761d-211">웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="3761d-212">hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="3761d-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="3761d-213">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="3761d-214">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="3761d-215">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="3761d-216">DNS 서버 hello 요청 수신</span><span class="sxs-lookup"><span data-stu-id="3761d-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="3761d-217">DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷</span><span class="sxs-lookup"><span data-stu-id="3761d-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="3761d-218">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="3761d-219">이 세션은 내부적으로 시작 된 이후 인터넷 DNS 서버 응답을 hello 응답이 허용</span><span class="sxs-lookup"><span data-stu-id="3761d-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="3761d-220">DNS 서버 hello 응답을 캐시 및 toohello 초기 요청 백 tooIIS01 이벤트에 응답</span><span class="sxs-lookup"><span data-stu-id="3761d-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="3761d-221">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="3761d-222">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="3761d-223">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="3761d-224">hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용</span><span class="sxs-lookup"><span data-stu-id="3761d-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="3761d-225">IIS01은 DNS01에서 hello 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="3761d-226">(*허용*) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="3761d-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="3761d-227">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="3761d-228">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="3761d-229">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="3761d-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-230">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="3761d-231">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="3761d-232">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooIIS01) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="3761d-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="3761d-233">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="3761d-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3761d-234">AppVM01은 hello 요청을 받아 파일 (액세스 권한이 부여 가정)를 사용 하 여 응답</span><span class="sxs-lookup"><span data-stu-id="3761d-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="3761d-235">Hello 응답이 허용 hello 백 엔드 서브넷에 없는 아웃 바운드 규칙이 있을 경우</span><span class="sxs-lookup"><span data-stu-id="3761d-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="3761d-236">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-237">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="3761d-238">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="3761d-239">hello IIS 서버 hello 파일 수신</span><span class="sxs-lookup"><span data-stu-id="3761d-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="3761d-240">(*Denied*) 웹 toobackend 서버</span><span class="sxs-lookup"><span data-stu-id="3761d-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="3761d-241">인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="3761d-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="3761d-242">파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3761d-243">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우</span><span class="sxs-lookup"><span data-stu-id="3761d-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="3761d-244">(*거부*) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="3761d-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="3761d-245">인터넷 사용자 시도 하는 hello BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드를 toolook</span><span class="sxs-lookup"><span data-stu-id="3761d-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="3761d-246">DNS에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="3761d-247">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 있던 경우 (참고: 규칙 1 (DNS) 같은 두 가지 이유로 적용 되지 않습니다, 첫 번째 hello 소스 주소는 인터넷을 hello,이 규칙은 toohello 적용 됩니다. 또한 지역 VNet으로 hello 원본 이 규칙 허용 규칙 이므로 트래픽을 거부 하지 않습니다 것)</span><span class="sxs-lookup"><span data-stu-id="3761d-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="3761d-248">(*Denied*) 웹 방화벽을 통해 tooSQL 액세스</span><span class="sxs-lookup"><span data-stu-id="3761d-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="3761d-249">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="3761d-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="3761d-250">SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 트래픽과 hello 방화벽에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="3761d-251">어떤 이유로 끝점 열려 있던 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="3761d-252">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="3761d-253">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="3761d-254">NSG 규칙 3 (인터넷 tooIIS01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="3761d-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="3761d-255">트래픽 (10.0.1.5) hello IIS01의 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="3761d-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="3761d-256">IIS01 하지 않게 응답 toohello 요청 포트 1433에서 수신 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="3761d-257">결론</span><span class="sxs-lookup"><span data-stu-id="3761d-257">Conclusion</span></span>
<span data-ttu-id="3761d-258">이 예제는 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 쉽고 명확한 방법.</span><span class="sxs-lookup"><span data-stu-id="3761d-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="3761d-259">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="3761d-260">참조</span><span class="sxs-lookup"><span data-stu-id="3761d-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="3761d-261">기본 스크립트 및 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="3761d-261">Main script and network config</span></span>
<span data-ttu-id="3761d-262">PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="3761d-263">Hello 네트워크 구성 "NetworkConf1.xml." 라는 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="3761d-264">필요 하 고 실행할 hello 스크립트로 hello 사용자 정의 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="3761d-265">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="3761d-265">Full script</span></span>
<span data-ttu-id="3761d-266">이 스크립트는 사용자 정의 변수를 hello; 기반</span><span class="sxs-lookup"><span data-stu-id="3761d-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="3761d-267">Tooan Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="3761d-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="3761d-268">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3761d-268">Create a storage account</span></span>
3. <span data-ttu-id="3761d-269">VNet 및 hello 네트워크 구성 파일에 정의 된 대로 두 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="3761d-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="3761d-270">4개의 Windows Server VM 빌드</span><span class="sxs-lookup"><span data-stu-id="3761d-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="3761d-271">다음을 포함하여 NSG를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-271">Configure NSG including:</span></span>
   * <span data-ttu-id="3761d-272">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="3761d-272">Creating an NSG</span></span>
   * <span data-ttu-id="3761d-273">규칙으로 채우기</span><span class="sxs-lookup"><span data-stu-id="3761d-273">Populating it with rules</span></span>
   * <span data-ttu-id="3761d-274">바인딩 hello NSG toohello 적절 한 서브넷</span><span class="sxs-lookup"><span data-stu-id="3761d-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="3761d-275">이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3761d-276">이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="3761d-277">빨간색 오류 메시지만 심각한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-277">Only error messages in red are cause for concern.</span></span>
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
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

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
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
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

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

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
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="3761d-278">네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="3761d-278">Network config file</span></span>
<span data-ttu-id="3761d-279">업데이트 된 위치와이 xml 파일을 저장 하 고 hello 스크립트 앞에 hello 링크 toothis 파일 toohello $NetworkConfigFile 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3761d-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="3761d-280">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="3761d-280">Sample application scripts</span></span>
<span data-ttu-id="3761d-281">Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="3761d-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3761d-282">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3761d-282">Next steps</span></span>
* <span data-ttu-id="3761d-283">업데이트 및 XML 파일 저장</span><span class="sxs-lookup"><span data-stu-id="3761d-283">Update and save XML file</span></span>
* <span data-ttu-id="3761d-284">Hello PowerShell 스크립트 toobuild hello 환경 실행</span><span class="sxs-lookup"><span data-stu-id="3761d-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="3761d-285">Hello 샘플 응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="3761d-285">Install hello sample application</span></span>
* <span data-ttu-id="3761d-286">이 DMZ를 통해 다양한 트래픽 흐름 테스트</span><span class="sxs-lookup"><span data-stu-id="3761d-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG와 인바운드 DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

