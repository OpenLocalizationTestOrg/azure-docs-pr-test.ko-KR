---
title: "DMZ 예제 - 방화벽 및 NSG로 응용 프로그램을 보호하는 DMZ 빌드 | Microsoft Docs"
description: "방화벽 및 NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc0e8a3fa749eb2e6f65ef92c2d3cb404cfc8bc0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="example-2--build-a-dmz-to-protect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="74a47-103">예 2 - 방화벽 및 NSG로 응용 프로그램을 보호하는 DMZ 빌드</span><span class="sxs-lookup"><span data-stu-id="74a47-103">Example 2 – Build a DMZ to protect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="74a47-104">[보안 경계 모범 사례 페이지로 돌아가기][HOME]</span><span class="sxs-lookup"><span data-stu-id="74a47-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="74a47-105">이 예에서는 방화벽, 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="74a47-106">또한 각 단계를 자세히 이해할 수 있도록 각각의 관련 명령에 대해 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="74a47-107">트래픽 시나리오 섹션에서는 DMZ에서 방어 계층을 진행하는 방법에 대한 심층적인 단계별 설명도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="74a47-108">마지막으로, 참조 섹션에서는 다양한 시나리오를 사용하여 테스트 및 실험하기 위한 환경을 구축하는 전체 코드와 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="74a47-109">![NVA NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="74a47-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="74a47-110">환경 설명</span><span class="sxs-lookup"><span data-stu-id="74a47-110">Environment Description</span></span>
<span data-ttu-id="74a47-111">이 예에서는 다음을 포함하는 구독이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="74a47-112">두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="74a47-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="74a47-113">"FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"</span><span class="sxs-lookup"><span data-stu-id="74a47-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="74a47-114">서브넷 모두에 적용되는 단일 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="74a47-114">A single Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="74a47-115">네트워크 가상 어플라이언스(이 예제의 경우 프런트 엔드 서브넷에 연결된 Barracuda NextGen Firewall)</span><span class="sxs-lookup"><span data-stu-id="74a47-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected to the Frontend subnet</span></span>
* <span data-ttu-id="74a47-116">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="74a47-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="74a47-117">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="74a47-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="74a47-118">DNS 서버("DNS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="74a47-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="74a47-119">이 예제에서는 Barracuda NextGen Firewall을 사용하지만 이 예제에 다른 네트워크 가상 어플라이언스를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-119">Although this example uses a Barracuda NextGen Firewall, many of the different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="74a47-120">아래 참조 섹션에는 위에서 설명한 대부분의 환경을 빌드할 PowerShell 스크립트가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-120">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="74a47-121">VM 및 가상 네트워크 구축은 예제 스크립트로 수행하지만 이 문서에서는 자세히 설명하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="74a47-122">환경을 구축하려면</span><span class="sxs-lookup"><span data-stu-id="74a47-122">To build the environment:</span></span>

1. <span data-ttu-id="74a47-123">참조 섹션에 포함된 네트워크 구성 xml 파일 저장(지정된 시나리오에 맞게 이름, 위치, IP 주소로 업데이트됨)</span><span class="sxs-lookup"><span data-stu-id="74a47-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="74a47-124">스크립트의 사용자 변수를 스크립트를 실행할 환경에 맞게 업데이트(구독, 서비스 이름 등)</span><span class="sxs-lookup"><span data-stu-id="74a47-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="74a47-125">PowerShell에서 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="74a47-125">Execute the script in PowerShell</span></span>

<span data-ttu-id="74a47-126">**참고**: PowerShell 스크립트에 표시된 영역은 네트워크 구성 xml 파일에 표시된 영역과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-126">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="74a47-127">스크립트를 성공적으로 실행하면 다음과 같은 사후 스크립트 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-127">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="74a47-128">방화벽 규칙을 설정합니다(아래 방화벽 규칙 섹션에서 설명).</span><span class="sxs-lookup"><span data-stu-id="74a47-128">Set up the firewall rules, this is covered in the section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="74a47-129">또는 참조 섹션의 두 스크립트를 사용하여 간단한 웹 응용 프로그램을 사용하는 웹 서버와 앱 서버를 설정하여 이 DMZ 구성을 이용한 테스트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-129">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="74a47-130">다음 섹션에서는 네트워크 보안 그룹과 관련된 대부분의 스크립트 문에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-130">The next section explains most of the scripts statements relative to Network Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="74a47-131">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="74a47-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="74a47-132">이 예에서는 NSG 그룹을 빌드한 후 6개의 규칙과 함께 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="74a47-133">일반적으로 특정 "허용" 규칙을 먼저 만든 후 보다 일반적인 "거부" 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-133">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="74a47-134">할당된 우선순위에 따라 먼저 평가할 규칙이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-134">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="74a47-135">특정 규칙에 적용할 트래픽이 발견되면 규칙을 더 이상 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-135">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="74a47-136">NSG 규칙은 인바운드 또는 아웃바운드 방향으로 적용할 수 있습니다(서브넷 관점에서).</span><span class="sxs-lookup"><span data-stu-id="74a47-136">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="74a47-137">선언적으로 인바운드 트래픽에 대해 다음 규칙이 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-137">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="74a47-138">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="74a47-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="74a47-139">인터넷에서 모든 VM으로 RDP 트래픽(포트 3389) 허용됨</span><span class="sxs-lookup"><span data-stu-id="74a47-139">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="74a47-140">인터넷에서 NVA(방화벽)로 HTTP 트래픽(포트 80) 허용됨</span><span class="sxs-lookup"><span data-stu-id="74a47-140">HTTP traffic (port 80) from the Internet to the NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="74a47-141">IIS01에서 AppVM1로 모든 트래픽(모든 포트) 허용됨</span><span class="sxs-lookup"><span data-stu-id="74a47-141">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="74a47-142">인터넷에서 전체 VNet(두 서브넷)으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="74a47-142">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="74a47-143">프런트 엔드 서브넷에서 백 엔드 서브넷으로 모든 트래픽(모든 포트) 거부됨</span><span class="sxs-lookup"><span data-stu-id="74a47-143">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="74a47-144">각 서브넷에 바인딩된 이러한 규칙에서는 HTTP 요청이 인터넷에서 웹 서버로 인바운드되는 경우 규칙 3(허용) 및 5(거부)가 모두 적용되지만 규칙 3이 우선순위가 높기 때문에 규칙 3만 적용되고 규칙 5는 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-144">With these rules bound to each subnet, if a HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="74a47-145">따라서 방화벽에 대해 HTTP 요청이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-145">Thus the HTTP request would be allowed to the firewall.</span></span> <span data-ttu-id="74a47-146">동일한 트래픽이 DNS01 서버에 도달하려고 시도하는 경우 규칙 5(거부)는 가장 먼저 적용되며 트래픽을 서버에 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-146">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="74a47-147">규칙 6(거부)은 프런트 엔드 서브넷이 백 엔드 서브넷과 통신을 차단합니다(규칙 1 및 4에서 허용된 트래픽 제외)하여 공격자가 프런트 엔드에서 웹 응용 프로그램을 손상시키는 경우 공격자의 "보호된" 백 엔드 네트워크(AppVM01 서버에서 노출되는 리소스만)에 대한 액세스가 제한되므로 백 엔드 네트워크를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-147">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="74a47-148">인터넷으로 트래픽을 허용하는 기본 아웃바운드 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-148">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="74a47-149">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="74a47-150">양방향에서 트래픽을 잠그려면 사용자 정의 라우팅이 필요하며 [기본 보안 경계 문서][HOME]에 있는 다양한 예에서 이에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-150">To lock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in the [main security boundary document][HOME].</span></span>

<span data-ttu-id="74a47-151">위에서 설명한 NSG 규칙은 [예 1 - NSG를 사용하여 간단한 DMZ 빌드][Example1]의 NSG 규칙과 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-151">The above discussed NSG rules are very similar to the NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="74a47-152">이 문서의 NSG 설명을 검토하여 각 NSG 규칙 및 해당 특성에 대해 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-152">Please review the NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="74a47-153">방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="74a47-153">Firewall Rules</span></span>
<span data-ttu-id="74a47-154">관리 클라이언트를 PC에 설치하여 방화벽을 관리하고 필요에 따라 구성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-154">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="74a47-155">장치를 관리하는 방법은 방화벽(또는 다른 NVA) 공급업체의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74a47-155">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="74a47-156">이 섹션의 나머지 부분에서는 공급업체 관리 클라이언트(예: Azure 포털 또는 PowerShell 아님)를 통한 방화벽 자체 구성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-156">The remainder of this section will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="74a47-157">이 예에 사용된 클라이언트 다운로드 및 Barracuda 연결에 대한 지침은 [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="74a47-157">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="74a47-158">방화벽에서 전달 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-158">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="74a47-159">이 예에서는 인터넷 트래픽 인바운드를 방화벽으로 라우팅한 후 웹 서버로 라우팅하므로 하나의 전달 NAT 규칙만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-159">Since this example only routes internet traffic in-bound to the firewall and then to the web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="74a47-160">이 예제에 사용된 Barracuda NextGen Firewall에서 규칙은 이 트래픽을 전달하기 위한 대상 NAT 규칙("Dst NAT")입니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-160">On the Barracuda NextGen Firewall used in this example the rule would be a Destination NAT rule (“Dst NAT”) to pass this traffic.</span></span>

<span data-ttu-id="74a47-161">다음 규칙을 만들거나 기존 기본 규칙을 확인하려면 Barracuda NG Admin 클라이언트 대시보드에서 시작하여 구성 탭으로 이동한 후 작동 구성 섹션에서 규칙 집합을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-161">To create the following rule (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="74a47-162">"Main Rules"라는 그리드에 방화벽에 대해 기존 활성 및 비활성화된 규칙이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-162">A grid called, “Main Rules” will show the existing active and deactivated rules on the firewall.</span></span> <span data-ttu-id="74a47-163">이 그리드의 오른쪽 위 모서리에 작은 녹색 "+" 단추를 클릭하여 새 규칙을 만듭니다(참고: 방화벽은 변경에 대해 "잠금" 상태일 수 있으며 "잠금" 단추가 표시되고 규칙을 만들거나 편집할 수 없는 경우 이 단추를 클릭하여 규칙 집합을 "잠금 해제"하고 편집을 허용합니다).</span><span class="sxs-lookup"><span data-stu-id="74a47-163">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the ruleset and allow editing).</span></span> <span data-ttu-id="74a47-164">기존 규칙을 편집하려는 경우 해당 규칙을 선택하고 마우스 오른쪽 단추를 클릭한 후 규칙 편집을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-164">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="74a47-165">새 규칙을 만들고 "WebTraffic"과 같은 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="74a47-166">대상 NAT 규칙 아이콘은 다음과 같습니다: ![대상 NAT 아이콘][2]</span><span class="sxs-lookup"><span data-stu-id="74a47-166">The Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="74a47-167">규칙 자체는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-167">The rule itself would look something like this:</span></span>

<span data-ttu-id="74a47-168">![방화벽 규칙][3]</span><span class="sxs-lookup"><span data-stu-id="74a47-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="74a47-169">여기서 HTTP(포트 80 또는 HTTPS인 경우 443)에 도달하려고 시도하는 방화벽을 호출하는 모든 인바운드 주소는 방화벽의 "DHCP1 로컬 IP" 인터페이스로 전송되고 IP 주소 10.0.1.5의 웹 서버로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-169">Here any inbound address that hits the Firewall trying to reach HTTP (port 80 or 443 for HTTPS) will be sent out the Firewall’s “DHCP1 Local IP” interface and redirected to the Web Server with the IP Address of 10.0.1.5.</span></span> <span data-ttu-id="74a47-170">트래픽이 포트 80에서 들어오고 포트 80에서 웹 서버로 나가므로 포트 변경이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-170">Since the traffic is coming in on port 80 and going to the web server on port 80 no port change was needed.</span></span> <span data-ttu-id="74a47-171">그러나 웹 서버가 포트 8080을 수신 대기하는 경우 대상 목록은 10.0.1.5:8080일 수 있으므로 방화벽에서 인바운드 포트 80을 웹 서버에서 인바운드 포트 8080으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-171">However, the Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating the inbound port 80 on the firewall to inbound port 8080 on the web server.</span></span>

<span data-ttu-id="74a47-172">연결 방법을 나타내야 하며 인터넷의 대상 규칙에 대해 "동적 SNAT"가 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-172">A Connection Method should also be signified, for the Destination Rule from the Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="74a47-173">하나의 규칙만 만들어지지만 우선순위가 바르게 설정되는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="74a47-174">방화벽의 모든 규칙에 대한 그리드에서 이 새로운 규칙은 맨 아래("BLOCKALL" 규칙 아래)에 있으며 진행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-174">If in the grid of all rules on the firewall this new rule is on the bottom (below the "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="74a47-175">웹 트래픽에 대해 새로 만든 규칙이 BLOCKALL 규칙 위에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-175">Ensure the newly created rule for web traffic is above the BLOCKALL rule.</span></span>

<span data-ttu-id="74a47-176">규칙을 만들었으면 방화벽에 푸시한 후 활성화해야 합니다. 이 작업을 수행하지 않으면 규칙 변경이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-176">Once the rule is created, it must be pushed to the firewall and then activated, if this is not done the rule change will not take effect.</span></span> <span data-ttu-id="74a47-177">푸시 및 활성화 프로세스는 다음 섹션에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-177">The push and activation process is described in the next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="74a47-178">규칙 활성화</span><span class="sxs-lookup"><span data-stu-id="74a47-178">Rule Activation</span></span>
<span data-ttu-id="74a47-179">이 규칙을 추가하도록 규칙 집합을 수정하고 규칙 집합을 방화벽에 업로드하고 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-179">With the ruleset modified to add this rule, the ruleset must be uploaded to the firewall and activated.</span></span>

<span data-ttu-id="74a47-180">![방화벽 규칙 활성화][4]</span><span class="sxs-lookup"><span data-stu-id="74a47-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="74a47-181">관리 클라이언트의 오른쪽 위 모서리에 단추 클러스터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-181">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="74a47-182">"변경 내용 보내기" 단추를 클릭하여 규칙을 방화벽으로 전송한 다음 "활성화" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-182">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="74a47-183">방화벽 규칙 집합을 활성화하면 이 예제 환경 빌드가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-183">With the activation of the firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="74a47-184">필요에 따라 참조 섹션의 빌드 후 스크립트를 실행하여 응용 프로그램을 이 환경에 추가하고 아래 트래픽 시나리오를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-184">Optionally, the post build scripts in the References section can be run to add an application to this environment to test the below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74a47-185">웹 서버를 직접 호출하지 않는다는 것을 깨닫는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-185">It is critical to realize that you will not hit the web server directly.</span></span> <span data-ttu-id="74a47-186">브라우저가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청하면 HTTP 끝점(포트 80)이 이 트래픽을 웹 서버가 아닌 방화벽에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, the HTTP endpoint (port 80) passes this traffic to the firewall not the web server.</span></span> <span data-ttu-id="74a47-187">방화벽 다음에는 위에서 만든 규칙에 따라 웹 서버로 요청을 NAT합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-187">The firewall then, according to the rule created above, NATs that request to the Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="74a47-188">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="74a47-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-to-web-server-through-firewall"></a><span data-ttu-id="74a47-189">(허용) 방화벽을 통해 웹 - 웹 서버</span><span class="sxs-lookup"><span data-stu-id="74a47-189">(Allowed) Web to Web Server through Firewall</span></span>
1. <span data-ttu-id="74a47-190">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="74a47-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="74a47-191">클라우드 서비스는 포트 80에서 열린 끝점을 통해 10.0.1.4:80에서 방화벽 로컬 인터페이스로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-191">Cloud service passes traffic through open endpoint on port 80 to firewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="74a47-192">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-193">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="74a47-194">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="74a47-195">NSG 규칙 3(인터넷에서 방화벽으로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-195">NSG Rule 3 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="74a47-196">트래픽이 방화벽의 내부 IP 주소를 호출합니다(10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="74a47-196">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="74a47-197">방화벽 전달 규칙은 이것이 포트 80 트래픽인 것을 확인하고 웹 서버 IIS01로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-197">Firewall forwarding rule see this is port 80 traffic, redirects it to the web server IIS01</span></span>
6. <span data-ttu-id="74a47-198">IIS01이 웹 트래픽을 수신 대기하고 이 요청을 수신하며 요청 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-198">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
7. <span data-ttu-id="74a47-199">IIS01은 AppVM01에서 SQL Server에 정보를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-199">IIS01 asks the SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="74a47-200">프런트엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="74a47-201">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-201">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-202">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-202">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="74a47-203">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-203">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="74a47-204">NSG 규칙 3(인터넷에서 방화벽으로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-204">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="74a47-205">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-205">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="74a47-206">AppVM01은 SQL 쿼리를 수신하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-206">AppVM01 receives the SQL Query and responds</span></span>
11. <span data-ttu-id="74a47-207">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-207">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
12. <span data-ttu-id="74a47-208">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="74a47-209">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-209">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="74a47-210">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-210">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
13. <span data-ttu-id="74a47-211">IIS 서버는 SQL 응답을 수신하고 HTTP 응답을 완료하여 요청자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-211">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
14. <span data-ttu-id="74a47-212">방화벽으로부터 NAT 세션이므로 응답 대상(처음)은 방화벽을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-212">Since this is a NAT session from the firewall, the response destination (initially) is for the Firewall</span></span>
15. <span data-ttu-id="74a47-213">방화벽은 웹 서버로부터 응답을 받아 인터넷 사용자에게 다시 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-213">The firewall receives the response from the Web Server and forwards back to the Internet User</span></span>
16. <span data-ttu-id="74a47-214">응답이 허용되는 프런트엔드 서브넷에 아웃바운드 규칙이 없으므로 인터넷 사용자는 요청된 웹 페이지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-214">Since there are no outbound rules on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="74a47-215">(허용) RDP - 백 엔드</span><span class="sxs-lookup"><span data-stu-id="74a47-215">(Allowed) RDP to Backend</span></span>
1. <span data-ttu-id="74a47-216">인터넷의 서버 관리자는 BackEnd001.CloudApp.Net:xxxxx에서 AppVM01에 대해 RDP 세션을 요청합니다.여기서 xxxxx는 RDP에 대해 AppVM01로 임의로 할당된 포트 번호입니다(할당된 포트는 Azure 포털 또는 PowerShell을 통해 확인할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="74a47-216">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="74a47-217">방화벽은 FrontEnd001.CloudApp.Net 주소만 수신 대기하므로 이 트래픽 흐름에는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-217">Since the Firewall is only listening on the FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="74a47-218">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-219">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-219">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="74a47-220">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="74a47-221">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="74a47-222">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-222">RDP session is enabled</span></span>
6. <span data-ttu-id="74a47-223">AppVM01에서 사용자 이름과 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="74a47-224">(허용) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="74a47-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="74a47-225">웹 서버인 IIS01은 www.data.gov에서 데이터 피드를 요구하지만 주소를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="74a47-226">VNet에 대한 네트워크 구성에서 DNS01(백 엔드 서브넷에서 10.0.2.4)을 주 DNS 서버로 나열하며 IIS01은 DNS01로 DNS 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-226">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="74a47-227">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="74a47-228">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-229">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="74a47-230">DNS 서버는 요청을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-230">DNS server receives the request</span></span>
6. <span data-ttu-id="74a47-231">DNS 서버에는 캐시된 주소가 없고 인터넷에서 루트 DNS 서버를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-231">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="74a47-232">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="74a47-233">이 세션은 내부적으로 시작되었으므로 인터넷 DNS 서버가 응답하고 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-233">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="74a47-234">DNS 서버는 응답을 캐시하고 IIS01에 대한 초기 요청에 다시 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-234">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="74a47-235">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="74a47-236">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="74a47-237">백 엔드 서브넷에서 프런트 엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="74a47-238">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙에서 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="74a47-239">IIS01은 DNS01에서 응답을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-239">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="74a47-240">(허용) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="74a47-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="74a47-241">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="74a47-242">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="74a47-243">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-243">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-244">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-244">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="74a47-245">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-245">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="74a47-246">NSG 규칙 3(인터넷에서 방화벽으로)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-246">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="74a47-247">NSG 규칙 4(IIS01에서 AppVM01로)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-247">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="74a47-248">AppVM01이 요청을 받아 파일로 응답합니다(액세스 권한이 부여된 것으로 가정).</span><span class="sxs-lookup"><span data-stu-id="74a47-248">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="74a47-249">백 엔드 서브넷에 아웃바운드 규칙이 없으므로 응답이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-249">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
6. <span data-ttu-id="74a47-250">프런트엔드 서브넷은 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-251">백 엔드 서브넷에서 프런트엔드 서브넷으로 인바운드 트래픽에 적용되는 NSG 규칙이 없으므로 NSG 규칙이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-251">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="74a47-252">서브넷 간의 트래픽을 허용하는 기본 시스템 규칙이 이 트래픽을 허용하므로 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-252">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="74a47-253">IIS 서버가 파일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-253">The IIS server receives the file</span></span>

#### <a name="denied-web-direct-to-web-server"></a><span data-ttu-id="74a47-254">(거부) 웹에서 웹 서버로 직접</span><span class="sxs-lookup"><span data-stu-id="74a47-254">(Denied) Web direct to Web Server</span></span>
<span data-ttu-id="74a47-255">웹 서버인 IIS01과 방화벽은 동일한 클라우드 서비스에 있으므로 동일한 공용 연결 IP 주소를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-255">Since the Web Server, IIS01, and the Firewall are in the same Cloud Service they share the same public facing IP address.</span></span> <span data-ttu-id="74a47-256">따라서 HTTP 트래픽은 방화벽에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-256">Thus any HTTP traffic would be directed to the firewall.</span></span> <span data-ttu-id="74a47-257">요청은 성공적으로 처리되지만 웹 서버로 직접 이동할 수 없으며 지정된 대로 방화벽을 통해 먼저 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-257">While the request would be successfully served, it cannot go directly to the Web Server, it passed, as designed, through the Firewall first.</span></span> <span data-ttu-id="74a47-258">트래픽 흐름은 이 섹션의 첫 번째 시나리오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="74a47-258">See the first Scenario in this section for the traffic flow.</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="74a47-259">(거부) 웹 - 백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="74a47-259">(Denied) Web to Backend Server</span></span>
1. <span data-ttu-id="74a47-260">인터넷 사용자가 BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에서 파일에 액세스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-260">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="74a47-261">파일 공유를 위해 열린 끝점이 없으므로 클라우드 서비스를 전달하지 않고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-261">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="74a47-262">어떤 이유로 끝점이 열린 경우 NSG 규칙 5(인터넷에서 VNet으로)가 이 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-262">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="74a47-263">(거부) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="74a47-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="74a47-264">인터넷 사용자가 BackEnd001.CloudApp.Net 서비스를 통해 DNS01에서 내부 DNS 레코드를 조회하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-264">Internet user tries to lookup an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="74a47-265">DNS를 위해 열린 끝점이 없으므로 클라우드 서비스를 전달하지 않고 서버에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-265">Since there are no endpoints open for DNS, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="74a47-266">어떤 이유로 끝점이 열린 경우 NSG 규칙 5(인터넷에서 VNet으로)가 이 트래픽을 차단합니다(참고: 규칙 1(DNS)은 두 가지 이유로 적용되지 않습니다. 첫째, 원본 주소가 인터넷입니다. 이 규칙은 로컬 VNet에만 원본으로 적용됩니다. 또한 이는 허용 규칙이므로 트래픽을 거부하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="74a47-266">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="74a47-267">(거부) 방화벽을 통해 웹에서 SQL 액세스</span><span class="sxs-lookup"><span data-stu-id="74a47-267">(Denied) Web to SQL access through Firewall</span></span>
1. <span data-ttu-id="74a47-268">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="74a47-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="74a47-269">SQL을 위해 열린 끝점이 없으므로 클라우드 서비스를 전달하지 않고 방화벽에 도달하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-269">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="74a47-270">어떤 이유로 끝점이 열린 경우 프런트엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-270">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="74a47-271">NSG 규칙 1(DNS)이 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-271">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="74a47-272">NSG 규칙 2(RDP)가 적용되지 않고 다음 규칙으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-272">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="74a47-273">NSG 규칙 2(인터넷에서 방화벽으로)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-273">NSG Rule 2 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="74a47-274">트래픽이 방화벽의 내부 IP 주소를 호출합니다(10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="74a47-274">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="74a47-275">방화벽에는 SQL에 대한 전달 규칙이 없고 트래픽을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-275">Firewall has no forwarding rules for SQL and drops the traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="74a47-276">결론</span><span class="sxs-lookup"><span data-stu-id="74a47-276">Conclusion</span></span>
<span data-ttu-id="74a47-277">이 방법은 방화벽으로 응용 프로그램을 보호하고 백 엔드 서브넷을 인바운드 트래픽과 격리하는 비교적 직접적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-277">This is a relatively straight forward way of protecting your application with a firewall and isolating the back end subnet from inbound traffic.</span></span>

<span data-ttu-id="74a47-278">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="74a47-279">참조</span><span class="sxs-lookup"><span data-stu-id="74a47-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="74a47-280">기본 스크립트 및 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="74a47-280">Main Script and Network Config</span></span>
<span data-ttu-id="74a47-281">PowerShell 스크립트 파일에 전체 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-281">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="74a47-282">네트워크 구성을 "NetworkConf2.xml"이라는 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-282">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="74a47-283">필요에 따라 사용자 정의 변수를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-283">Modify the user defined variables as needed.</span></span> <span data-ttu-id="74a47-284">스크립트를 실행한 다음 위의 방화벽 규칙 설정 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-284">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="74a47-285">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="74a47-285">Full Script</span></span>
<span data-ttu-id="74a47-286">이 스크립트는 사용자 정의 변수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-286">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="74a47-287">Azure 구독에 연결</span><span class="sxs-lookup"><span data-stu-id="74a47-287">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="74a47-288">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="74a47-288">Create a new storage account</span></span>
3. <span data-ttu-id="74a47-289">네트워크 구성 파일에 정의된 대로 새 VNet 및 두 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="74a47-289">Create a new VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="74a47-290">4개의 Windows Server VM 빌드</span><span class="sxs-lookup"><span data-stu-id="74a47-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="74a47-291">다음을 포함하여 NSG 구성</span><span class="sxs-lookup"><span data-stu-id="74a47-291">Configure NSG including:</span></span>
   * <span data-ttu-id="74a47-292">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="74a47-292">Creating a NSG</span></span>
   * <span data-ttu-id="74a47-293">규칙으로 채우기</span><span class="sxs-lookup"><span data-stu-id="74a47-293">Populating it with rules</span></span>
   * <span data-ttu-id="74a47-294">적절한 서브넷에 대해 NSG 바인딩</span><span class="sxs-lookup"><span data-stu-id="74a47-294">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="74a47-295">이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74a47-296">이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="74a47-297">빨간색 오류 메시지만 심각한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on the FrontEnd Subnet (plus the NVA on the FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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

    # User Defined Global Variables
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
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: To ensure proper NSG Rule creation later in this script:
        #       - The Web Server must be VM 1
        #       - The AppVM1 Server must be VM 2
        #       - The DNS server must be VM 4
        #
        #       Otherwise the NSG rules in the last section of this
        #       script will need to be changed to match the modified
        #       VM array numbers ($i) so the NSG Rule IP addresses
        #       are aligned to the associated VM IP addresses.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
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
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all the EndPoints we'll need once we're up and running
                # Note: Web traffic goes through the firewall, so we'll need to set up a HTTP endpoint.
                #       Also, the firewall will be redirecting web traffic to a new IP and Port in a
                #       forwarding rule, so the HTTP endpoint here will have the same public and local
                #       port and the firewall will do the NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) to $($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="74a47-298">네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="74a47-298">Network Config File</span></span>
<span data-ttu-id="74a47-299">업데이트된 위치로 이 xml 파일을 저장하고 이 파일에 대한 링크를 위의 스크립트에 있는 $NetworkConfigFile 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74a47-299">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="74a47-300">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="74a47-300">Sample Application Scripts</span></span>
<span data-ttu-id="74a47-301">이에 대한 샘플 응용 프로그램 및 기타 DMZ 예제를 설치하는 방법은 다음 링크를 통해 제공됩니다. [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="74a47-301">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="74a47-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "NSG와 인바운드 DMZ"</span><span class="sxs-lookup"><span data-stu-id="74a47-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inbound DMZ with NSG"</span></span>
<span data-ttu-id="74a47-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "대상 NAT 아이콘"</span><span class="sxs-lookup"><span data-stu-id="74a47-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Destination NAT Icon"</span></span>
<span data-ttu-id="74a47-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "방화벽 규칙"</span><span class="sxs-lookup"><span data-stu-id="74a47-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewall Rule"</span></span>
<span data-ttu-id="74a47-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "방화벽 규칙 활성화"</span><span class="sxs-lookup"><span data-stu-id="74a47-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
