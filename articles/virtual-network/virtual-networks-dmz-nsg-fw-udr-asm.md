---
title: "예 – aaaDMZ 빌드 DMZ tooProtect 네트워크 방화벽과 UDR, NSG를 | Microsoft Docs"
description: "방화벽, UDR(사용자 정의 라우팅), NSG(네트워크 보안 그룹)를 사용하여 DMZ 빌드"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="7a801-103">예제 3 – 빌드 DMZ tooProtect 네트워크 방화벽과 UDR, NSG를</span><span class="sxs-lookup"><span data-stu-id="7a801-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="7a801-104">[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]</span><span class="sxs-lookup"><span data-stu-id="7a801-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="7a801-105">이 예제에서는 방화벽이 포함된 DMZ, 4개의 Windows Server, 사용자 정의 라우팅, IP 전달, 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="7a801-106">그는 또한 안내 각각 hello 관련 명령 tooprovide의 각 단계에 대 한 깊은 이해가.</span><span class="sxs-lookup"><span data-stu-id="7a801-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="7a801-107">이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="7a801-108">마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="7a801-109">![NVA, NSG, UDR을 사용하는 양방향 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="7a801-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="7a801-110">환경 설정</span><span class="sxs-lookup"><span data-stu-id="7a801-110">Environment Setup</span></span>
<span data-ttu-id="7a801-111">이 예제는 hello 다음을 포함 하는 구독:</span><span class="sxs-lookup"><span data-stu-id="7a801-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="7a801-112">세 클라우드 서비스: "SecSvc001", "FrontEnd001", "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="7a801-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="7a801-113">"SecNet", "FrontEnd", "BackEnd"의 세 서브넷을 포함하는 가상 네트워크 "CorpNetwork"</span><span class="sxs-lookup"><span data-stu-id="7a801-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="7a801-114">이 예제는 방화벽에서 네트워크 가상 어플라이언스 toohello SecNet 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="7a801-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="7a801-115">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="7a801-116">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="7a801-117">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="7a801-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="7a801-118">아래 hello references 섹션에는 PowerShell 스크립트를 위에서 설명한 hello 환경의 대부분 빌드됩니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="7a801-119">건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="7a801-120">toobuild hello 환경:</span><span class="sxs-lookup"><span data-stu-id="7a801-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="7a801-121">Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장</span><span class="sxs-lookup"><span data-stu-id="7a801-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="7a801-122">Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행</span><span class="sxs-lookup"><span data-stu-id="7a801-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="7a801-123">PowerShell에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="7a801-124">**참고**: hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="7a801-125">Hello 스크립트가 성공적으로 실행 되 면 이후 스크립트 단계를 수행 하는 hello는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="7a801-126">이 이라는 hello 섹션에서 설명 되 hello 방화벽 규칙을 설정,: 방화벽 규칙을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="7a801-127">필요에 따라 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.</span><span class="sxs-lookup"><span data-stu-id="7a801-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="7a801-128">Hello 스크립트가 성공적으로 실행 되 면 hello 방화벽 규칙 toobe 완료 해야 합니다,이 내용은 hello 섹션에서 설명: 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="7a801-129">UDR(사용자 정의 라우팅)</span><span class="sxs-lookup"><span data-stu-id="7a801-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="7a801-130">기본적으로 시스템 경로 따라 hello로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="7a801-131">hello VNETLocal는 항상 정의 된 hello 주소 접두사가 (ie 것에서 변경 됩니다. 각 특정 VNet을 정의 하는 방법을 따라 VNet tooVNet) 해당 특정 네트워크에 대 한 hello VNet의입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="7a801-132">이 정적이 고 위와 같은 기본 hello 나머지 시스템 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="7a801-133">우선 순위와 hello 가장 긴 접두사 일치 (LPM) 메서드를 통해 처리 되는 경로, 따라서 hello hello 테이블에 가장 적합 한 경로 적용할 tooa 대상 주소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="7a801-134">따라서 hello 로컬 네트워크 (10.0.0.0/16) 하기 위한 트래픽 (예: toohello DNS01 서버를 10.0.2.4)는 toohello 10.0.0.0/16 경로 인해 hello VNet tooits 대상 간에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="7a801-135">즉, 10.0.2.4에 대 한 hello 10.0.0.0/16 경로가 hello 가장 구체적인 경로 hello 10.0.0.0/8 및 0.0.0.0/0도 적용할 수, 하지만이 트래픽을 영향을 하지 않는 덜 구체적인 되므로 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="7a801-136">따라서 hello 트래픽 too10.0.2.4 다음 홉의 지역 VNet hello 및 단순히 toohello 대상 라우팅하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="7a801-137">위한 트래픽이 10.1.1.1 예를 들어, hello 10.0.0.0/16 경로가 적용 하지 않지만 hello 10.0.0.0/8 hello 가장 구체적인 것이 hello 트래픽을 개이고 경우 hello 다음 홉은 Null ("블랙 숨어")는 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="7a801-138">Hello 대상 tooany hello Null 접두사 또는 hello VNETLocal 접두사를 적용 하지 않은 경우 hello 구체적인 따라가는, 0.0.0.0/0 라우팅하고 toohello hello 다음 홉으로 인터넷 아웃와 Azure의 인터넷 가장자리 아웃 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="7a801-139">Hello 경로 테이블에 두 개의 동일한 접두사 인 hello 다음은 hello 경로 "source" 특성에 따라 기본 설정의 hello 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="7a801-140">"Virtualappliance 인" = 사용자 정의 경로 수동으로 추가한 toohello 테이블</span><span class="sxs-lookup"><span data-stu-id="7a801-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="7a801-141">"VPNGateway" (BGP 하이브리드 네트워크와 함께 사용할 경우)에 대 한 동적 경로 = 동적 네트워크 프로토콜에 의해 추가, 이러한 경로로 변경 될 수 있습니다 시간이 지남에 따라 겹치기 네트워크의 변경 내용이 자동으로 반영 되 hello 동적 프로토콜</span><span class="sxs-lookup"><span data-stu-id="7a801-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="7a801-142">"Default" hello 시스템 경로 = 위의 hello 경로 테이블에 표시 된 대로 로컬 VNet과 hello 정적 항목 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="7a801-143">이제 ExpressRoute와 VPN 게이트웨이 tooforce 아웃 바운드 된 사용자 정의 라우팅 (UDR)를 사용할 수 있습니다 및 크로스-프레미스 인바운드 트래픽을 toobe 라우트된 tooa 네트워크 가상 어플라이언스 (NVA).</span><span class="sxs-lookup"><span data-stu-id="7a801-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="7a801-144">Hello 로컬 경로 만들기</span><span class="sxs-lookup"><span data-stu-id="7a801-144">Creating hello local routes</span></span>
<span data-ttu-id="7a801-145">이 예제에서는 두 개의 라우팅 테이블 필요한 마다 하나씩 hello 프런트 엔드 및 백 엔드 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="7a801-146">각 테이블은 서브넷을 지정 하는 hello에 대 한 적절 한 고정 경로로 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="7a801-147">이 예의 hello 목적으로 각 테이블에는 세 가지 경로:</span><span class="sxs-lookup"><span data-stu-id="7a801-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="7a801-148">정의 된 다음 홉 tooallow 로컬 서브넷 트래픽 toobypass hello 방화벽이 없는 로컬 서브넷 트래픽</span><span class="sxs-lookup"><span data-stu-id="7a801-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="7a801-149">지역 VNet 트래픽이 tooroute를 직접 허용 하는 hello 기본 규칙 재정의 한 다음 홉 방화벽으로 정의 된 가상 네트워크 트래픽</span><span class="sxs-lookup"><span data-stu-id="7a801-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="7a801-150">다음 홉 방화벽 hello로 정의 된 나머지 모든 트래픽 (0/0)</span><span class="sxs-lookup"><span data-stu-id="7a801-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="7a801-151">Hello 라우팅 테이블을 만들 바인딩된 tootheir 서브넷 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="7a801-152">Hello 프런트 엔드 서브넷 라우팅 테이블을 만든 후에 바인딩된 toohello 서브넷이 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="7a801-153">예를 들어 hello 다음 명령을 사용 하는 toobuild hello 경로 테이블은 사용자 정의 경로 추가 하 고 다음 hello 경로 테이블 tooa 서브넷을 바인딩합니다 (참고; 달러 기호로 시작 아래의 모든 항목 (예:: $BESubnet)는 hello 스크립트에서 사용자 정의 변수 hello 참조가 문서의 섹션):</span><span class="sxs-lookup"><span data-stu-id="7a801-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="7a801-154">첫 번째 hello 기본 라우팅 테이블을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-154">First hello base routing table must be created.</span></span> <span data-ttu-id="7a801-155">이 코드 조각 hello 백 엔드 서브넷에 대 한 hello 테이블 hello 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="7a801-156">Hello 스크립트에는 해당 테이블이 만들어집니다 hello 프런트 엔드 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="7a801-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="7a801-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="7a801-158">Hello 경로 테이블을 만든 후에 특정 사용자 정의 경로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="7a801-159">이 조각에서 모든 트래픽 (0.0.0.0/0) hello ($VMIP [0], 변수는 hello 가상 어플라이언스 hello 스크립트의 앞부분에 나오는 만들 떄 할당 hello IP 주소에 사용 되는 toopass은)는 가상 어플라이언스를 통해 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="7a801-160">Hello 스크립트에는 해당 규칙에에서도 만들어지는 hello 프런트 엔드 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="7a801-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="7a801-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="7a801-162">경로 항목 위에 hello 덮어씁니다 hello 기본 "0.0.0.0/0" 경로 하지만 여전히 있게 기존 hello 기본 10.0.0.0/16 규칙 트래픽 hello VNet tooroute 내에서 직접 toohello 대상과 toohello 네트워크 가상 어플라이언스 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="7a801-163">toocorrect이 동작 hello에 따라 규칙을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="7a801-164">이 시점에서 내용을 선택 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="7a801-165">두 경로 위에 hello로 모든 트래픽이 평가는 단일 서브넷 내에 트래픽에 대 한 toohello 방화벽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="7a801-166">하지만이 세 번째, 특정 규칙을 추가할 수 있습니다 hello 방화벽의 개입 하지 않고 로컬 서브넷 tooroute 내에서 트래픽을 tooallow 권장 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="7a801-167">이 경로의 모든 주소 destine hello 로컬 서브넷 just 수에 대 한 상태 라우팅할 있습니다 직접 (NextHopType VNETLocal =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="7a801-168">마지막으로 hello 라우팅 테이블과 함께 사용자 정의 경로가 채웁니다 hello 테이블 이제 해야 바인딩된 tooa 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="7a801-169">Hello 스크립트 hello 프런트 엔드 경로 테이블도 바인딩된 toohello 프런트 엔드 서브넷이입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="7a801-170">Hello 백 엔드 서브넷에 대 한 hello 바인딩 스크립트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="7a801-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="7a801-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="7a801-172">IP 전달</span><span class="sxs-lookup"><span data-stu-id="7a801-172">IP Forwarding</span></span>
<span data-ttu-id="7a801-173">도우미 기능 tooUDR IP 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="7a801-174">이 트래픽을 허용 하 고 tooreceive 특별히 가상 기기에서 설정을 toohello 기기 해결은 선택한 후 해당 트래픽을 tooits 최종 대상을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="7a801-175">예를 들어 AppVM01 트래픽만 인해 요청 toohello DNS01 서버, UDR 라우팅합니다이 toohello 방화벽을입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="7a801-176">IP 전달을 사용 하도록 설정와 hello DNS01 대상 (10.0.2.4)에 대 한 hello 트래픽은 hello 기기 (10.0.0.4)에서 허용 되며 tooits 최종 대상 (10.0.2.4)를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="7a801-177">없이 IP 전달 hello 방화벽에서 사용 하도록 설정, 트래픽 것에서 허용 되지 hello 기기 hello 경로 테이블에 hello 다음 홉으로 hello 방화벽이 있는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7a801-178">것이 사용자 정의 된 라우팅을와 함께에서 중요 한 tooremember tooenable IP 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="7a801-179">IP 전달 설정은 단일 명령이며 VM을 만들 때 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="7a801-180">Hello에 대 한이 예제에서는 hello 코드 조각의 흐름 hello hello 스크립트 끝에 반영 하 고 hello UDR 명령으로 그룹화:</span><span class="sxs-lookup"><span data-stu-id="7a801-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="7a801-181">Hello VM 인스턴스 가상 어플라이언스를 호출,이 경우 방화벽 hello 및 IP 전달 설정 (참고; 달러 기호로 시작 하는 빨간색의 모든 항목 (예:: $VMName[0]) hello이 문서의 hello 참조 섹션에는 스크립트에서 사용자 정의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="7a801-182">[0] 대괄호로 0 hello, 나타냅니다 hello 수정 하지 않고 예제 스크립트 toowork hello에 대 한 Vm의 hello 배열에서 첫 번째 VM, 첫 번째 VM (VM 0) 해야 하는 hello hello 방화벽):</span><span class="sxs-lookup"><span data-stu-id="7a801-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="7a801-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="7a801-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="7a801-184">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="7a801-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="7a801-185">이 예제에서는 NSG 그룹을 빌드한 후 단일 규칙을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="7a801-186">이 그룹은 다음 toohello 프런트 엔드 및 백 엔드 서브넷만 (하지 SecNet hello)를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="7a801-187">선언적 규칙을 따르는 hello 작성 중인:</span><span class="sxs-lookup"><span data-stu-id="7a801-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="7a801-188">전체 VNet (모든 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)</span><span class="sxs-lookup"><span data-stu-id="7a801-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="7a801-189">이 예제에서 NSG를 사용했지만 기본 목적은 수동 구성 시 실수가 발생할 경우를 대비하여 두 번째 방어 계층을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="7a801-190">프런트 엔드 hello 인터넷 tooeither hello에서 모든 인바운드 트래픽을 tooblock 원하는 또는 hello SecNet 서브넷 toohello 방화벽을 통해 백 엔드 서브넷 트래픽 흐름만 (및 서브넷 toohello 프런트 엔드 또는 백 엔드에 적절 한 경우).</span><span class="sxs-lookup"><span data-stu-id="7a801-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="7a801-191">또한 장소에 hello UDR 규칙과 함께 않은 쉽게 변환할 hello 프런트 엔드 또는 백 엔드 서브넷 하는 모든 트래픽은 전송 toohello 방화벽 (감사 tooUDR) 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="7a801-192">hello 표시 되는 것이 비대칭 흐름으로 방화벽과 hello 아웃 바운드 트래픽을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="7a801-193">있다는 3 계층의 보안 보호 hello 프런트 엔드 및 백 엔드 서브넷; 1) BackEnd001 클라우드 서비스, 2) Nsg 거부 없고 FrontEnd001 hello open 끝점에서 트래픽을 인터넷, 3) hello 방화벽 비대칭 트래픽을 삭제 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="7a801-194">이 예에서 hello 네트워크 보안 그룹에 대 한 흥미로운 사항이 하나 포함 한다는 것입니다 아래 표시 된 규칙이 하나만 있는 toodeny 인터넷 트래픽을 toohello 전체 가상 네트워크에 있는 hello 보안 서브넷을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="7a801-195">그러나 toohello 프런트 엔드 및 백 엔드 서브넷 hello NSG는만 바인딩되어 있으므로 hello 규칙 되지에서 처리 트래픽 인바운드 toohello 보안 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="7a801-196">결과적으로, hello NSG 규칙 처음이 NSG hello toohello 보안 서브넷 바인딩되기 때문에 인터넷 트래픽을 tooany 주소가 없습니다. VNet hello에 라는, 경우에 트래픽 toohello 보안 서브넷을 흐릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="7a801-197">방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="7a801-197">Firewall Rules</span></span>
<span data-ttu-id="7a801-198">Hello 방화벽에서 전달 규칙 toobe 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="7a801-199">Hello 방화벽 차단 또는 모든 인바운드, 아웃 바운드 전달 및 VNet 내 트래픽 이므로 많은 방화벽 규칙이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="7a801-200">또한 모든 인바운드 트래픽 hello 보안 서비스 공용 IP 주소를 적중지 것입니다 (서로 다른 포트의 경우)에서 toobe hello 방화벽에 의해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="7a801-201">가장 좋은 방법은 나중에 hello 서브넷 및 방화벽 규칙 tooavoid 재작업을 설정 하기 전에 toodiagram hello 논리 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="7a801-202">hello 다음 그림은이 예제에 대 한 hello 방화벽 규칙의 논리적 보기:</span><span class="sxs-lookup"><span data-stu-id="7a801-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="7a801-203">![Hello 방화벽 규칙의 논리적 보기][2]</span><span class="sxs-lookup"><span data-stu-id="7a801-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="7a801-204">Hello 관리 포트에 사용 되는 네트워크 가상 어플라이언스 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="7a801-205">이 예제에서는 포트 22, 801, 807을 사용하는 Barracuda NextGen 방화벽을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="7a801-206">Hello 어플라이언스 공급 업체 설명서 toofind hello 정확 하 게 사용 되는 포트를 사용 중인 hello 장치 관리를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7a801-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="7a801-207">논리적 규칙 설명</span><span class="sxs-lookup"><span data-stu-id="7a801-207">Logical Rule Description</span></span>
<span data-ttu-id="7a801-208">Hello 논리 위의 다이어그램에서 hello 방화벽 hello 해당 서브넷에만 리소스가 고 hello 방화벽 규칙 및 방법은 논리적으로 허용 하거나 거부할 트래픽 흐름이 고 hello 실제 라우트된 경로가 아닌이 다이어그램에 표시 되므로 hello 보안 서브넷 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="7a801-209">또한 hello RDP 트래픽이 높은 범위가 지정 된 포트 (8014 – 8026) 되며 hello로 정렬 된 선택한 toosomewhat에 대해 선택 하는 hello 외부 포트 마지막 두 개 8 진수가 동일한 hello 쉽게 가독성을 위해 로컬 IP 주소 (예: 로컬 서버 주소 10.0.1.4 연결 된 그러나 외부 포트 8014) 더 높은 모든 충돌 하지 않는 포트를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="7a801-210">이 예제에서는 7가지 유형의 규칙이 필요하며 아래에서 이러한 규칙 유형에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="7a801-211">외부 규칙(인바운드 트래픽용):</span><span class="sxs-lookup"><span data-stu-id="7a801-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="7a801-212">방화벽 관리 규칙:이 앱의 리디렉션 규칙 hello 네트워크 가상 어플라이언스의 트래픽이 toopass toohello 관리 포트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="7a801-213">(각 windows server) 용 RDP 규칙: (각 서버 마다 하나씩) 이러한 4 가지 규칙의 hello 관리 RDP 통해 개별 서버를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="7a801-214">Hello 사용 중인 네트워크 가상 어플라이언스의 hello 기능에 따라 하나의 규칙으로도 제공 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="7a801-215">응용 프로그램 트래픽 규칙: 두 응용 프로그램 트래픽 규칙을 hello 프런트 엔드 웹 트래픽에 대해 먼저 hello hello 백 엔드 트래픽 (예: 웹 서버 toodata 계층)에 대 한 두 번째 hello 가지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="7a801-216">이러한 규칙의 hello 구성 (서버 배치) hello 네트워크 아키텍처 및 트래픽 흐름 (어떤 방향이 hello 트래픽 흐름 및 사용 되는 포트)에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="7a801-217">첫 번째 규칙의 hello hello 실제 응용 프로그램 트래픽 tooreach hello 응용 프로그램 서버를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="7a801-218">Hello 다른 규칙 보안, 관리, 등을 허용 하는 동안 응용 프로그램 규칙 hello (가) 외부 사용자 또는 서비스 tooaccess 허용 작업은입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="7a801-219">이 예에서는 포트 80에서 단일 웹 서버인는, 따라서 단일 방화벽 응용 프로그램 규칙은 인바운드 트래픽을 toohello 외부 IP toohello 웹 서버의 내부 IP 주소를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="7a801-220">hello 리디렉션 트래픽 세션은 NAT 미치지 않을 toohello 내부 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="7a801-221">두 번째 응용 프로그램 트래픽 규칙은 hello 모든 포트를 통해 백 엔드 규칙 tooallow hello 웹 서버 tootalk toohello AppVM01 서버 (않음 하지 AppVM02) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="7a801-222">내부 규칙(인트라-VNet 트래픽용)</span><span class="sxs-lookup"><span data-stu-id="7a801-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="7a801-223">아웃 바운드 tooInternet 규칙:이 규칙을 사용 하면 모든 네트워크에서 트래픽을 toopass toohello 선택한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="7a801-224">이 규칙은 일반적으로 기본 규칙 요소가 hello 방화벽에 있지만 사용할 수 없는 상태에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="7a801-225">이 예제에서는 이 규칙을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="7a801-226">DNS 규칙:이 규칙에는 DNS (포트 53) 트래픽 toopass toohello DNS 서버 에서만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="7a801-227">Hello 프런트 엔드 toohello 백 엔드에서에서 대부분 트래픽을 차단 하는이 환경에 대 한이 규칙은 특히 DNS 모든 로컬 서브넷에서 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="7a801-228">서브넷 tooSubnet 규칙:이 규칙은 tooallow hello 프런트 엔드 서브넷에 서브넷 tooconnect tooany 서버 종료 (하지만 하지 역방향 hello)의 모든 서버 hello 백에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="7a801-229">유사 시 대기 (트래픽에 대 한 규칙 hello 위의 중 하나를 만족 하지 않는):</span><span class="sxs-lookup"><span data-stu-id="7a801-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="7a801-230">모든 트래픽 규칙 거부:이 hello 최종 규칙 (측면에서 우선 순위)은 항상 고 따라서 트래픽이 이동 하면 실패 toomatch hello 앞에이 규칙에 의해 삭제 됩니다 규칙의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="7a801-231">이 규칙은 기본 규칙으로 일반적으로 활성화되어 있으며 수정이 필요하지 않는 경우가 대부분입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="7a801-232">Hello 두 번째 응용 프로그램 트래픽 규칙 모든 포트가이 예제의 쉽게에 대 한 허용 됩니다에서 실제 시나리오 hello 가장 구체적인 포트와 주소 범위입니다.이 규칙의 사용된 tooreduce hello 공격 노출 영역 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="7a801-233">모든 규칙 위에 hello를 만든 후에 tooreview hello 각 규칙 tooensure 트래픽의 우선 순위 허용 하거나 필요에 따라 거부 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="7a801-234">예를 들어 hello 규칙은 우선 순위에 따라입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="7a801-235">쉽게 toobe toomis 정렬 규칙 기한 hello 방화벽 잠긴 경우</span><span class="sxs-lookup"><span data-stu-id="7a801-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="7a801-236">여기에 최소한 자체 hello 방화벽에 대 한 hello 관리는 항상 hello 절대 가장 높은 우선 순위 규칙을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="7a801-237">규칙 필수 조건</span><span class="sxs-lookup"><span data-stu-id="7a801-237">Rule Prerequisites</span></span>
<span data-ttu-id="7a801-238">Hello 가상 컴퓨터가 실행 중인 hello 방화벽에 대 한 필수 구성 요소 하나은 공용 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="7a801-239">Hello 방화벽 tooprocess 트래픽에 대 한 적절 한 공용 끝점 hello 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="7a801-240">세 가지 방법으로이 예에서; 트래픽 1) 관리 트래픽 toocontrol hello 방화벽 및 방화벽 규칙, 2) RDP 트래픽 toocontrol hello windows 서버 및 3) 응용 프로그램 트래픽이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="7a801-241">이들은 hello 위쪽에 있는 트래픽 형식의 hello 세 개의 열 위에 hello 방화벽 규칙의 논리 보기의 절반입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a801-242">키 takeway 여기는 tooremember 하 **모든** 트래픽이 hello 방화벽을 통해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="7a801-243">따라서 tooremote 데스크톱 toohello IIS01 서버 라고 하더라도 hello 프런트 엔드 서브넷에 tooaccess와 hello 프런트 엔드 클라우드 서비스에에서이 서버 tooRDP toohello 방화벽에 필요한 포트 8014, 사용 되 고 hello 방화벽 tooroute hello RDP 요청을 내부적으로 허용 toohello IIS01 RDP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="7a801-244">hello Azure 포털의 "연결" 단추 (관련해 서 hello 포털 참조 수) 없는 직접 RDP 경로 tooIIS01 있기 때문에 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="7a801-245">즉, 모든 연결 hello에서 toohello 보안 서비스 및 포트, secscv001.cloudapp.net:xxxx (외부 포트 및 내부 ip 주소 및 포트 매핑 hello에 대 한 다이어그램 위에서 참조 hello) 예: 인터넷 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="7a801-246">끝점 hello VM 생성 시 열 수 있습니다 또는 hello 예제 스크립트에서 수행 되며이 코드 조각에서는 아래 표시 된 대로 빌드를 게시할 (참고; 모든 항목 시작 부분에 달러 기호 (예:: $VMName[$i])는 hello referen의 hello 스크립트에서 사용자 정의 변수 이 문서의 섹션 ce입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="7a801-247">대괄호로 [$i] "$i" hello 나타내는 Vm의 배열에서 특정 VM의 hello 배열 번호):</span><span class="sxs-lookup"><span data-stu-id="7a801-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="7a801-248">하지 명확 하 게 여기에 표시 된 기한 않지만 변수 하지만 끝점의 toohello 사용은 **만** hello 보안 클라우드 서비스에서 열.</span><span class="sxs-lookup"><span data-stu-id="7a801-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="7a801-249">이 모든 인바운드 트래픽을 처리 하는 tooensure 라우팅되면 NAT를 생략 된 hello 방화벽에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="7a801-250">관리 클라이언트에서는 toobe PC toomanage hello 방화벽에 설치 되어 있어야 하 고 필요한 hello 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="7a801-251">어떻게 toomanage hello 장치에 hello 설명서 방화벽 (또는 다른 NVA)에서 공급 업체를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7a801-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="7a801-252">이 섹션 및 방화벽 규칙 만들기 hello 다음 섹션의 나머지 부분에서는 hello hello 공급 업체 관리 클라이언트 (즉, 하지 hello Azure 포털 또는 PowerShell)를 통해 자체 hello 방화벽의 hello 구성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="7a801-253">클라이언트 다운로드 및 연결 toohello Barracuda이 예에서 사용에 대 한 지침은 여기: [Barracuda NG 관리자](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="7a801-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="7a801-254">hello 규칙을 만들; 보다 쉽게 만들 수 있는 두 가지 필수 구성 요소 개체 클래스가 hello 방화벽에 있지만 방화벽 규칙을 만들기 전에 로그에 기록 되 면 네트워크 및 서비스 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="7a801-255">이 예제에서는 세 개의 명명 된 네트워크 개체 정의 (hello 프런트 엔드 서브넷 및 hello 백 엔드 서브넷에도 hello hello DNS 서버의 IP 주소에 대 한 네트워크 개체에 대해 각각 하나씩) 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="7a801-256">명명 된 네트워크; toocreate hello Barracuda NG 관리자 클라이언트 대시보드에서 부터는 toohello 구성 탭 이동, hello Operational 구성 섹션에서에서 규칙 집합을 클릭, 클릭 한 후 "네트워크" hello 방화벽 객체 메뉴에서 고 hello 네트워크 편집 메뉴에서 새로 만들기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="7a801-257">hello 네트워크 개체 hello 이름과 hello 접두사를 추가 하 여 만들 이제 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="7a801-258">![프런트 엔드 네트워크 개체 만들기][3]</span><span class="sxs-lookup"><span data-stu-id="7a801-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="7a801-259">이렇게 하면 hello 프런트 엔드 서브넷에 대 한 명명 된 네트워크 만들어집니다, 그리고 hello 백 엔드 서브넷에도 비슷한 개체를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="7a801-260">이제 hello 서브넷 hello 방화벽 규칙에 대 한 이름으로 보다 쉽게 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="7a801-261">에 대 한 DNS 서버 개체를 hello:</span><span class="sxs-lookup"><span data-stu-id="7a801-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="7a801-262">![DNS 서버 개체 만들기][4]</span><span class="sxs-lookup"><span data-stu-id="7a801-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="7a801-263">이 단일 IP 주소 참조가 hello 문서의 뒷부분에 나오는 DNS 규칙에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="7a801-264">hello 두 번째 필수 구성 요소 개체는 서비스 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="7a801-265">이 각 서버에 대 한 hello RDP 연결 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="7a801-266">Hello 기존 RDP 서비스 개체에 바인딩된 toohello 기본 RDP 포트 이므로 3389 새로운 서비스에서에서 만들 수 있습니다 tooallow 트래픽은 hello 외부 포트 (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="7a801-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="7a801-267">hello 새 포트 toohello 기존 RDP 서비스를 추가할 수도 있지만 설명의 편의 각 서버에 대해 개별 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="7a801-268">toocreate 서버;에 대 한 새 RDP 규칙 toohello 구성 탭을 탐색 hello Barracuda NG 관리 클라이언트 대시보드에서 시작, hello Operational 구성에서에서 섹션 클릭 규칙 집합을 다음 hello 서비스 hello 목록 아래로 스크롤하여 방화벽 개체 메뉴에서 "서비스"를 클릭 하 고 선택 hello "RDP" 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="7a801-269">마우스 오른쪽 단추로 복사를 클릭하여 선택한 다음 마우스 오른쪽 단추로 붙여넣기를 클릭하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="7a801-270">이제 RDP-Copy1 서비스 개체를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="7a801-271">RDP Copy1를 마우스 오른쪽 단추로 클릭 하 고 편집을 선택, 서비스 개체 편집 다음과 같이 창이 팝업 됩니다 hello:</span><span class="sxs-lookup"><span data-stu-id="7a801-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="7a801-272">![기본 RDP 규칙 복사본][5]</span><span class="sxs-lookup"><span data-stu-id="7a801-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="7a801-273">hello 값 편집된 toorepresent hello 특정 서버에 대 한 RDP 서비스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="7a801-274">기본 위에 AppVM01 hello에 대 한 RDP 규칙에는 수정 된 tooreflect 새 서비스 이름, 설명, 되어야 할지와 그림 8 다이어그램 hello에 외부 RDP 포트 사용 (참고: hello 포트가 hello RDP toohello 외부 포트 3389를 사용 하는이 기본값에서에서 변경 된 특정 서버 AppVM01 hello 외부 포트의 hello 경우에는 8025) hello 수정 된 서비스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="7a801-275">![AppVM01 규칙][6]</span><span class="sxs-lookup"><span data-stu-id="7a801-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="7a801-276">이 프로세스 반복된 toocreate 서버; 남은 hello에 대 한 RDP 서비스 여야 합니다. AppVM02, DNS01, 및 IIS01 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="7a801-277">이러한 서비스의 hello 생성을 하면 hello 규칙을 만드는 간단 하 고 더욱 명확 하 게 hello 다음 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="7a801-278">두 가지 이유로; hello 방화벽에 대 한는 RDP 서비스가 필요 하지 않습니다. 1) 첫 번째 hello 방화벽 VM은 Linux 기반 이미지 SSH 포트는 RDP, 2) 포트 22 대신 VM 관리에 대 한 22에서 사용 된 것과 다른 두 개의 관리 포트 관리 연결에 대 한 tooallow 아래에 설명 된 hello 첫 번째 관리 규칙 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="7a801-279">방화벽 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="7a801-279">Firewall Rules Creation</span></span>
<span data-ttu-id="7a801-280">이 예제에는 세 가지 유형의 방화벽 규칙을 사용하며 각각 고유한 아이콘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="7a801-281">응용 프로그램 리디렉션 규칙이 hello: ![응용 프로그램 리디렉션 아이콘][7]</span><span class="sxs-lookup"><span data-stu-id="7a801-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="7a801-282">hello 대상 NAT 규칙: ![대상 NAT 아이콘][8]</span><span class="sxs-lookup"><span data-stu-id="7a801-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="7a801-283">hello 통과 규칙: ![전달 아이콘][9]</span><span class="sxs-lookup"><span data-stu-id="7a801-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="7a801-284">이러한 규칙에 대 한 자세한 내용은 hello Barracuda 웹 사이트에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="7a801-285">toocreate 규칙에 따라 hello (또는 기존 기본 규칙 확인) hello Operational 구성 섹션에서 규칙 집합을 toohello 구성 탭 이동 hello Barracuda NG 관리 클라이언트 대시보드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="7a801-286">표 호출 하 여 "Main 규칙" hello이이 방화벽에 대 한 규칙 활성화 및 비활성화 된 기존 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="7a801-287">Hello 오른쪽 상단의이 눈금은 작은 녹색 "+" 단추를 클릭이 toocreate 새 규칙 (참고: 표시 단추에 "Lock"으로 표시는 없습니다 toocreate 또는 규칙을 편집,이 단추를 클릭 하는 경우 너무 "잠금 해제" hello 규칙 se, 방화벽 "잠겨" 변경에 대 한 t 편집).</span><span class="sxs-lookup"><span data-stu-id="7a801-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="7a801-288">기존 규칙 tooedit을 원한다 해당 규칙을 선택, 마우스 오른쪽 단추로 클릭 하 고 편집할 규칙을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="7a801-289">규칙은 생성 및/또는 수정, 일단 해야만 해당 toohello 방화벽 푸시되 며 다음 처리 되 고 활성화, 이렇게 하지 않으면 hello 규칙 변경 내용이 적용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="7a801-290">hello 세부 정보 규칙 설명은 아래 hello 푸시 및 활성화 프로세스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="7a801-291">각 규칙의 hello 비슷하므로이 예제는 다음과 같이 설명 toocomplete가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="7a801-292">**관리 규칙을 방화벽**:이 응용 프로그램 리디렉션 규칙이 toopass toohello 관리 포트가이 예에서 Barracuda NextGen 방화벽 hello 네트워크 가상 어플라이언스로의 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="7a801-293">hello 관리는 801, 807 필요에 따라 22입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="7a801-294">hello 외부 및 내부 포트 동일 (예: 포트 변환) hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="7a801-295">SETUP-MGMT-ACCESS가 기본 규칙이며 기본적으로 사용하도록 설정되어 있습니다(Barracuda NextGen Firewall 버전 6.1).</span><span class="sxs-lookup"><span data-stu-id="7a801-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="7a801-296">![방화벽 관리 규칙][10]</span><span class="sxs-lookup"><span data-stu-id="7a801-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="7a801-297">hello 소스 주소 공간이이 규칙에는 임의의 경우 hello 알려진 관리 IP 주소 범위,이 범위를 줄이는 hello 공격 노출 toohello 관리 포트가 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="7a801-298">**RDP 규칙**: 이러한 대상 NAT 규칙의 hello 관리 RDP 통해 개별 서버를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="7a801-299">이 규칙은 4 개의 필요한 중요 한 필드 toocreate:</span><span class="sxs-lookup"><span data-stu-id="7a801-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="7a801-300">소스 hello 원본 필드에 사용 되는 "Any" hello 참조 어디에서 든 RDP tooallow입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="7a801-301">Hello 외부 포트 리디렉션 toohello 서버 로컬 IP 주소와 tooport 3386 (hello 기본 RDP 포트)를 서비스 – 적절 한 서비스 개체는이 경우 "AppVM01 RDP" 앞에서 만든 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="7a801-302">이 특정 규칙 RDP 액세스 tooAppVM01입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="7a801-303">대상-hello 해야 *hello 방화벽에 로컬 포트*, "DCHP 1 로컬 IP" 또는 t h 0 고정 Ip를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7a801-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="7a801-304">hello 서 수 (eth0, e t h 1 등)는 네트워크 어플라이언스에 여러 로컬 인터페이스가 포함 하는 경우 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="7a801-305">이 hello 포트 hello 방화벽에서를 전송 (포트를 수신 하는 hello로 hello 동일)을 수 hello 실제 라우팅된 대상을 hello 대상 목록 필드에이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="7a801-306">리디렉션 –이 섹션에서는 설명 hello 가상 어플라이언스 tooultimately이이 트래픽을 리디렉션해야 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="7a801-307">hello 가장 간단한 리디렉션은 tooplace hello IP 및 hello 대상 목록 필드에 지정 된 포트 (선택 사항)입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="7a801-308">대상 포트 hello 인바운드 요청에 사용 되는 hello 포트가 없는 경우 됩니다 (ie 변환 없음), 포트 hello 포트를 지정 된 경우 사용 됩니다 NAT 함께 hello IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="7a801-309">![방화벽 RDP 규칙][11]</span><span class="sxs-lookup"><span data-stu-id="7a801-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="7a801-310">환경에서는 총 4 개의 RDP 규칙의 toobe 만든이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="7a801-311">규칙 이름</span><span class="sxs-lookup"><span data-stu-id="7a801-311">Rule Name</span></span> | <span data-ttu-id="7a801-312">서버</span><span class="sxs-lookup"><span data-stu-id="7a801-312">Server</span></span> | <span data-ttu-id="7a801-313">부여</span><span class="sxs-lookup"><span data-stu-id="7a801-313">Service</span></span> | <span data-ttu-id="7a801-314">대상 목록</span><span class="sxs-lookup"><span data-stu-id="7a801-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="7a801-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="7a801-315">RDP-to-IIS01</span></span> |<span data-ttu-id="7a801-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="7a801-316">IIS01</span></span> |<span data-ttu-id="7a801-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="7a801-317">IIS01 RDP</span></span> |<span data-ttu-id="7a801-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="7a801-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="7a801-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="7a801-319">RDP-to-DNS01</span></span> |<span data-ttu-id="7a801-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="7a801-320">DNS01</span></span> |<span data-ttu-id="7a801-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="7a801-321">DNS01 RDP</span></span> |<span data-ttu-id="7a801-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="7a801-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="7a801-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="7a801-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="7a801-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="7a801-324">AppVM01</span></span> |<span data-ttu-id="7a801-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="7a801-325">AppVM01 RDP</span></span> |<span data-ttu-id="7a801-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="7a801-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="7a801-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="7a801-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="7a801-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="7a801-328">AppVM02</span></span> |<span data-ttu-id="7a801-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="7a801-329">AppVm02 RDP</span></span> |<span data-ttu-id="7a801-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="7a801-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="7a801-331">Hello hello 소스 범위의 키와 서비스 필드 범위를 좁혀 hello 공격 노출 영역이 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="7a801-332">기능을 사용 하면 hello 가장 제한 된 범위를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="7a801-333">**응용 프로그램 트래픽 규칙**: 두 개의 응용 프로그램 트래픽 규칙, hello 프런트 엔드 웹 트래픽에 대해 먼저 hello 및 hello 백 엔드 트래픽 (예: 웹 서버 toodata 계층)에 대 한 두 번째 hello 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="7a801-334">이러한 규칙은 hello 네트워크 아키텍처 (위해 서버를 배치 하는 위치) 및 트래픽 흐름 (어떤 방향이 hello 트래픽 흐름 및 사용 되는 포트)에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="7a801-335">먼저 설명 하는 것은 웹 트래픽에 대해 hello 프런트 엔드 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="7a801-336">![방화벽 웹 규칙][12]</span><span class="sxs-lookup"><span data-stu-id="7a801-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="7a801-337">이 대상 NAT 규칙 hello 실제 응용 프로그램 트래픽 tooreach hello 응용 프로그램 서버를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="7a801-338">Hello 다른 규칙 보안, 관리, 등을 허용 하는 동안 응용 프로그램 규칙 hello (가) 외부 사용자 또는 서비스 tooaccess 허용 작업은입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="7a801-339">이 예에서는 포트 80 켜져 단일 웹 서버, 따라서 hello 단일 방화벽 응용 프로그램 규칙은 인바운드 트래픽을 toohello 외부 IP toohello 웹 서버의 내부 IP 주소를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="7a801-340">**참고**: hello 대상 목록 필드에 할당 된 포트는, 따라서 hello 인바운드 포트 80 (또는 hello 선택 되어 있는 서비스의 경우 443)에 사용할 hello 웹 서버의 hello 리디렉션.</span><span class="sxs-lookup"><span data-stu-id="7a801-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="7a801-341">Hello 웹 서버를 다른 포트에서 수신 하는 경우 예를 들어: 포트 8080, hello 대상 목록 필드도 hello 포트 리디렉션에 대 한 업데이트 된 too10.0.1.4:8080 tooallow 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="7a801-342">hello 다음 응용 프로그램 트래픽 규칙은 모든 서비스를 통해 백 엔드 규칙 tooallow hello 웹 서버 tootalk toohello AppVM01 서버 (않음 하지 AppVM02) hello:</span><span class="sxs-lookup"><span data-stu-id="7a801-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="7a801-343">![방화벽 AppVM01 규칙][13]</span><span class="sxs-lookup"><span data-stu-id="7a801-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="7a801-344">이 통과 규칙은 모든 IIS 서버에서 hello 프런트 엔드 서브넷 tooreach hello AppVM01 (IP 주소 10.0.2.5) 모든 포트에서 hello 웹 응용 프로그램에 필요한 프로토콜 tooaccess 데이터를 사용 하 여 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="7a801-345">이 화면에는 "\<명시적-dest\>" hello 대상 필드 toosignify 10.0.2.5에에서 hello 대상으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="7a801-346">일 수 명시적 표시 된 것 처럼 또는 명명 된 네트워크 개체 (값으로 DNS 서버 hello에 대 한 필수 구성 요소 hello에에서).</span><span class="sxs-lookup"><span data-stu-id="7a801-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="7a801-347">이 hello 방화벽의 toohello 관리자를 toowhich 메서드가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="7a801-348">Explict Desitnation,으로 10.0.2.5 tooadd hello 아래의 첫 번째 빈 행을 두 번 클릭 \<명시적-dest\> 팝업 되 hello 창의 hello 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="7a801-349">없는 NAT 때문에이 내부 트래픽이 너무 hello 연결 방법을 설정할 수 있도록이 전달 규칙을 사용 하면 필요한 "No SNAT"입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="7a801-350">**참고**:이 규칙에 hello 원본 네트워크는 모든 리소스 hello 프런트 엔드 서브넷에만, 또는 되기 알려진된 특정 수의 웹 서버, 리소스일 수 네트워크 개체를 만들 toobe 보다 구체적인 toothose 정확 하 게 IP 주소 대신 하는 경우 hello 전체 프런트 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="7a801-351">이 규칙에 "임의" toomake 샘플 응용 프로그램 보다 쉽게 toosetup hello 및 사용 하 여 hello 서비스 사용 하 여, 또한 이렇게 하면 ICMPv4 단일 규칙에서 (ping).</span><span class="sxs-lookup"><span data-stu-id="7a801-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="7a801-352">하지만 권장되는 방식은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="7a801-353">hello 포트 및 프로토콜 ("서비스")이이 경계를 넘어 응용 프로그램 작업 tooreduce hello 공격 노출 영역을 허용 하는 좁은 범위의 toohello 최소 가능 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="7a801-354">이 규칙을 사용 하 고는 dest 명시적 참조를 표시 하지만 전체 hello 방화벽 구성 일관적인 접근 방식을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="7a801-355">명명 된 네트워크 개체는 hello 쉽게 가독성 및 지원 가능성에 대 한 전체에서 사용 될 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="7a801-356">안녕하세요 명시적-dest 여기 사용 되는 유일한 tooshow 대체 참조 메서드이고 (특히 복잡 한 구성의 경우)에 일반적으로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="7a801-357">**아웃 바운드 tooInternet 규칙**:이 전달 규칙에는 모든 원본 네트워크 toopass toohello 선택한 대상 네트워크의 트래픽을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="7a801-358">이 규칙은 hello Barracuda NextGen 방화벽을 이미 일반적으로 기본 규칙을 않으며 사용할 수 없는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="7a801-359">이 규칙을 마우스 오른쪽 단추로 클릭 hello 규칙 활성화 명령에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="7a801-360">여기에 표시 된 hello 규칙 수정된 tooadd hello 로컬 서브넷인 hello이이 규칙의이 문서 toohello 원본 특성의 필수 구성 요소 섹션에 참조로 생성 된 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="7a801-361">![방화벽 아웃바운드 규칙][14]</span><span class="sxs-lookup"><span data-stu-id="7a801-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="7a801-362">**DNS 규칙**: 전달이 규칙은 DNS (포트 53) 트래픽 toopass toohello DNS 서버 에서만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="7a801-363">Hello 프런트 엔드 toohello 백 엔드에서에서 대부분 트래픽을 차단 하는이 환경에 대 한이 규칙은 특히 DNS 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="7a801-364">![방화벽 DNS 규칙][15]</span><span class="sxs-lookup"><span data-stu-id="7a801-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="7a801-365">**참고**:이 화면에서 발된 hello 라이선스 서버의 연결 방법이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="7a801-366">내부 IP toointernal IP 주소 트래픽에 대 한이 규칙 이기 때문에 없는 NATing가 필요 합니다이 hello이 연결 방법은 너무 설정 되어이 통과 규칙에 대 한 "No SNAT"입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="7a801-367">**서브넷 tooSubnet 규칙**: 전달이 규칙은 활성화 된 기본 규칙 및의 모든 서버에서 다시 hello에 서브넷 tooconnect tooany 서버를 종료 하는 수정 된 tooallow hello 프런트 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="7a801-368">이 규칙에는 모든 내부 트래픽 하므로 hello 라이선스 서버의 연결 방법이 tooNo SNAT를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="7a801-369">![방화벽 인트라-VNet 규칙][16]</span><span class="sxs-lookup"><span data-stu-id="7a801-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="7a801-370">**참고**: hello 양방향 확인란을 선택 하지 않으면 (아닙니다 대부분의 규칙에서 확인),이 기능은 "하나 방향" 규칙이 있다는 점에서이 규칙에 대 한 중요, hello 백 엔드 서브넷 toohello 프런트 엔드 네트워크에 대 한 연결을 시작할 수 있습니다 하지만 하지 역방향 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="7a801-371">이 확인란을 선택할 경우 이 규칙에서 양방향 트래픽이 허용되며 논리적 다이어그램에 따라 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="7a801-372">**모든 트래픽 규칙 거부**: hello 최종 규칙 (측면에서 우선 순위)와 항상를 이어야 하며 따라서 트래픽이 이동 실패 toomatch hello 규칙 앞에 하면 삭제 됩니다이 규칙에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="7a801-373">이 규칙은 기본 규칙으로 일반적으로 활성화되어 있으며 수정이 필요하지 않는 경우가 대부분입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="7a801-374">![방화벽 거부 규칙][17]</span><span class="sxs-lookup"><span data-stu-id="7a801-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a801-375">모든 규칙 위에 hello를 만든 후에 tooreview hello 각 규칙 tooensure 트래픽의 우선 순위 허용 하거나 필요에 따라 거부 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="7a801-376">예를 들어 hello 규칙 hello 전달 규칙 hello Barracuda 관리 클라이언트에서에서 주 눈금에에서 표시 되어야 하는 hello 순서로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="7a801-377">규칙 활성화</span><span class="sxs-lookup"><span data-stu-id="7a801-377">Rule Activation</span></span>
<span data-ttu-id="7a801-378">Hello 논리 다이어그램의 수정 된 ruleset toohello 사양 hello hello ruleset 이어야 toohello 방화벽을 업로드 하 고 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="7a801-379">![방화벽 규칙 활성화][18]</span><span class="sxs-lookup"><span data-stu-id="7a801-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="7a801-380">Hello 관리 클라이언트의 오른쪽 상단 모서리 hello 단추의 클러스터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="7a801-381">Hello "보낼 변경" 단추 toosend hello 수정 규칙 toohello 방화벽 클릭 hello "활성화" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="7a801-382">이 예에서는 환경 구축 hello 방화벽 규칙 집합의 정품 인증의 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="7a801-383">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="7a801-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7a801-384">키 takeway은 tooremember 하 **모든** 트래픽이 hello 방화벽을 통해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="7a801-385">따라서 tooremote 데스크톱 toohello IIS01 서버 라고 하더라도 hello 프런트 엔드 서브넷에 tooaccess와 hello 프런트 엔드 클라우드 서비스에에서이 서버 tooRDP toohello 방화벽에 필요한 포트 8014, 사용 되 고 hello 방화벽 tooroute hello RDP 요청을 내부적으로 허용 toohello IIS01 RDP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="7a801-386">hello Azure 포털의 "연결" 단추 (관련해 서 hello 포털 참조 수) 없는 직접 RDP 경로 tooIIS01 있기 때문에 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="7a801-387">즉, 모든 연결 hello에서 toohello 보안 서비스 및 포트, secscv001.cloudapp.net:xxxx 예: 인터넷 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="7a801-388">이러한 시나리오에 대 한 방화벽 규칙에 따라 hello 위치 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="7a801-389">방화벽 관리</span><span class="sxs-lookup"><span data-stu-id="7a801-389">Firewall Management</span></span>
2. <span data-ttu-id="7a801-390">RDP tooIIS01</span><span class="sxs-lookup"><span data-stu-id="7a801-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="7a801-391">RDP tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7a801-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="7a801-392">RDP tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="7a801-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="7a801-393">RDP tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="7a801-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="7a801-394">웹 앱 트래픽 toohello</span><span class="sxs-lookup"><span data-stu-id="7a801-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="7a801-395">앱 트래픽 tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="7a801-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="7a801-396">아웃 바운드 toohello 인터넷</span><span class="sxs-lookup"><span data-stu-id="7a801-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="7a801-397">프런트 엔드 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7a801-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="7a801-398">내 서브넷 간의 트래픽은 (백 엔드 toofront 끝에만 해당)</span><span class="sxs-lookup"><span data-stu-id="7a801-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="7a801-399">모두 거부</span><span class="sxs-lookup"><span data-stu-id="7a801-399">Deny All</span></span>

<span data-ttu-id="7a801-400">hello 실제 방화벽 규칙 집합 또한 toothese에서 여러 가지 규칙 줄 가능성이 큽니다, 지정 된 모든 방화벽 규칙 hello 서로 다른 우선 순위는 hello 여기에 나열 된 것 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="7a801-401">이 목록 및 연결 된 번호는 이러한 11 개의 규칙 및 적용 hello 상대적 우선 순위만 간의 tooprovide 관련성입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="7a801-402">즉; hello 실제 방화벽 "RDP tooIIS01" hello 규칙 번호 5, 수 있지만이 목록의 hello 의도가 맞게 hello "RDP tooDNS01" 규칙 이상 hello "방화벽 관리" 규칙 아래를 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="7a801-403">hello 목록 아래 시나리오를 간단 하 게 나타내기; 허용 hello에도 도움이 될 예: "FW Rule 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="7a801-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="7a801-404">간단한 설명을 위해 네 개의 RDP 규칙 통칭 됩니다 hello 라고도 함, "hello RDP 규칙" hello 트래픽 시나리오 관련 없는 tooRDP를가 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7a801-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="7a801-405">또한 네트워크 보안 그룹은 hello 프런트 엔드에 인바운드 인터넷 트래픽에 대해와 백 엔드 서브넷 점에 유의 하세요.</span><span class="sxs-lookup"><span data-stu-id="7a801-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="7a801-406">(사용 가능) 인터넷 tooWeb 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="7a801-407">인터넷 사용자가 SecSvc001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="7a801-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7a801-408">10.0.0.4:80에 포트 80 toofirewall 인터페이스에 대 한 열린 끝점을 통해 클라우드 서비스 전달 트래픽</span><span class="sxs-lookup"><span data-stu-id="7a801-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="7a801-409">없음 NSG tooSecurity 서브넷에 할당 하는 시스템 NSG 규칙에서 트래픽을 toofirewall 허용 되므로</span><span class="sxs-lookup"><span data-stu-id="7a801-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="7a801-410">트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="7a801-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="7a801-411">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7a801-412">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-413">FW 규칙 2-5 (RDP 규칙), 적용 하지 않는 toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7a801-414">FW 규칙 6 (응용 프로그램: 웹), 해당 방화벽 Nat 트래픽이 허용 것 too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="7a801-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="7a801-415">인바운드 규칙 처리를 시작 하는 hello 프런트 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7a801-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7a801-416">NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다 (이 트래픽은 NAT가 hello 방화벽에 의해 것, 따라서 hello 소스 주소는 이제 hello 보안 서브넷에는 hello 방화벽 NSG toobe "local" 트래픽 hello 프런트 엔드 서브넷에는 표시 있고 따라서 허용), toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="7a801-417">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="7a801-418">IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다</span><span class="sxs-lookup"><span data-stu-id="7a801-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="7a801-419">IIS01 백 엔드 서브넷에 FTP 세션 tooAppVM01 tooinitiates 시도</span><span class="sxs-lookup"><span data-stu-id="7a801-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="7a801-420">hello UDR 프런트 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉</span><span class="sxs-lookup"><span data-stu-id="7a801-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="7a801-421">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7a801-422">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="7a801-423">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-424">Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="7a801-425">FW 규칙 6 (응용 프로그램: 웹) toonext 규칙을 이동, 적용 하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="7a801-426">FW 규칙 7 (응용 프로그램: 백 엔드)를 적용 하는 트래픽을 허용, 방화벽 전달 트래픽 too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="7a801-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="7a801-427">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7a801-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7a801-428">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-429">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="7a801-430">AppVM01은 hello 요청을 수신 하 고 hello 세션 시작 및 응답</span><span class="sxs-lookup"><span data-stu-id="7a801-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="7a801-431">hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉</span><span class="sxs-lookup"><span data-stu-id="7a801-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="7a801-432">이어서 hello 백 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù</span><span class="sxs-lookup"><span data-stu-id="7a801-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="7a801-433">연결된 세션 hello 방화벽 hello 응답 백 toohello 웹 서버 (IIS01) 트래픽에서 반환이 때문에 통과</span><span class="sxs-lookup"><span data-stu-id="7a801-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="7a801-434">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7a801-435">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-436">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="7a801-437">이 HTTP 응답은 toohello 요청자에 게 전송 hello IIS 서버 hello 응답을 받은 AppVM01를 사용 하 여 hello 트랜잭션을 완료 하 고 건물 hello HTTP 응답을 요청한 후,</span><span class="sxs-lookup"><span data-stu-id="7a801-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="7a801-438">이어서 hello 프런트 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù</span><span class="sxs-lookup"><span data-stu-id="7a801-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="7a801-439">HTTP 응답 적중 hello 방화벽 hello 하며 NAT 세션은 hello 방화벽에 의해 허용 되는이 항목은 hello 응답 tooan 설정</span><span class="sxs-lookup"><span data-stu-id="7a801-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="7a801-440">hello 방화벽이 리디렉션합니다 hello 응답 백 toohello를 인터넷 사용자</span><span class="sxs-lookup"><span data-stu-id="7a801-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="7a801-441">아웃 바운드 NSG 규칙 또는 UDR 홉 없는지 이후 hello 프런트 엔드 서브넷에 hello 응답 허용 되 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="7a801-442">(사용 가능) 인터넷 RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="7a801-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="7a801-443">인터넷에서 서버 관리자 RDP 세션 tooAppVM01 SecSvc001.CloudApp.Net:8025, 8025 hello hello "RDP tooAppVM01" 방화벽 규칙에 대 한 포트 번호를 할당 하는 사용자가을 통해 요청</span><span class="sxs-lookup"><span data-stu-id="7a801-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="7a801-444">hello 클라우드 서비스 10.0.0.4:8025 8025 toofirewall 인터페이스 포트에 hello 열린 끝점을 통해 트래픽을 전달합니다</span><span class="sxs-lookup"><span data-stu-id="7a801-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="7a801-445">없음 NSG tooSecurity 서브넷에 할당 하는 시스템 NSG 규칙에서 트래픽을 toofirewall 허용 되므로</span><span class="sxs-lookup"><span data-stu-id="7a801-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="7a801-446">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7a801-447">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-448">Toonext 규칙 이동 FW 규칙 2 (RDP IIS) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7a801-449">Toonext 규칙 이동 FW 규칙 3 (RDP DNS01) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7a801-450">FW 규칙 4 (RDP AppVM01)은 적용, 방화벽 Nat 트래픽을 허용 하기 too10.0.2.5:3386 (AppVM01 RDP 포트)</span><span class="sxs-lookup"><span data-stu-id="7a801-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="7a801-451">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7a801-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7a801-452">NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다 (이 트래픽은 NAT가 hello 방화벽에 의해 것, 따라서 hello 소스 주소는 이제 hello 보안 서브넷에는 hello 방화벽 NSG toobe "local" 트래픽 hello 백 엔드 서브넷에는 표시 있고 따라서 허용), toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="7a801-453">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="7a801-454">AppVM01이 RDP 트래픽을 수신 대기하다 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="7a801-455">아웃바운드 NSG 규칙이 없으므로 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="7a801-456">Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽</span><span class="sxs-lookup"><span data-stu-id="7a801-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="7a801-457">연결된 세션 hello 방화벽 hello 응답 백 toohello 인터넷 사용자 트래픽을에서 반환이 때문에 통과</span><span class="sxs-lookup"><span data-stu-id="7a801-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="7a801-458">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-458">RDP session is enabled</span></span>
11. <span data-ttu-id="7a801-459">AppVM01에서 사용자 이름과 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="7a801-460">(허용) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="7a801-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7a801-461">웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="7a801-462">hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="7a801-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="7a801-463">Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽</span><span class="sxs-lookup"><span data-stu-id="7a801-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="7a801-464">아웃 바운드 NSG 규칙이 바인딩된 toohello 프런트 엔드 서브넷은, 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="7a801-465">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7a801-466">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-467">Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7a801-468">FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7a801-469">Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7a801-470">FW 규칙 9 (DNS)은 적용, 트래픽을 허용, 방화벽 전달 트래픽 too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="7a801-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="7a801-471">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7a801-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7a801-472">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-473">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="7a801-474">DNS 서버 hello 요청 수신</span><span class="sxs-lookup"><span data-stu-id="7a801-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="7a801-475">DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷</span><span class="sxs-lookup"><span data-stu-id="7a801-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="7a801-476">Hello 다음 홉으로 UDR 경로 아웃 바운드 트래픽 toohello 방화벽</span><span class="sxs-lookup"><span data-stu-id="7a801-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="7a801-477">백 엔드 서브넷에 아웃바운드 NSG 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="7a801-478">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="7a801-479">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-480">Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="7a801-481">FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="7a801-482">FW 규칙 8 (tooInternet)은 적용, 트래픽을 허용, 세션 hello 인터넷의 DNS 서버 tooroot 아웃 SNAT은</span><span class="sxs-lookup"><span data-stu-id="7a801-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="7a801-483">인터넷 DNS 서버 응답 hello 방화벽에서이 세션이 시작 된, 때문 hello 응답 수락한 경우 hello 방화벽</span><span class="sxs-lookup"><span data-stu-id="7a801-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="7a801-484">Hello 방화벽 전달 hello 응답 toohello DNS01 서버를 시작 합니다. 지금은 연결된 된 세션 이기</span><span class="sxs-lookup"><span data-stu-id="7a801-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="7a801-485">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7a801-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7a801-486">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-487">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="7a801-488">hello DNS 서버 hello 응답을 캐시 받아서 toohello 초기 요청 백 tooIIS01 응답</span><span class="sxs-lookup"><span data-stu-id="7a801-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="7a801-489">hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉</span><span class="sxs-lookup"><span data-stu-id="7a801-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="7a801-490">아웃 바운드 NSG 규칙이 hello 백 엔드 서브넷에 있는 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="7a801-491">이 hello 방화벽에서 연결된 된 세션, hello 응답 hello 방화벽 백 toohello IIS 서버에 의해 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="7a801-492">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7a801-493">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="7a801-494">hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용</span><span class="sxs-lookup"><span data-stu-id="7a801-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="7a801-495">IIS01은 DNS01에서 hello 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="7a801-496">(사용 가능) 백 엔드 서버 tooFrontend 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="7a801-497">로그온 한 tooAppVM02 RDP 통해 관리자는 파일 서버에서 직접 요청 hello IIS01 windows 파일 탐색기를 통해</span><span class="sxs-lookup"><span data-stu-id="7a801-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="7a801-498">hello UDR 백 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉</span><span class="sxs-lookup"><span data-stu-id="7a801-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="7a801-499">이어서 hello 백 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù</span><span class="sxs-lookup"><span data-stu-id="7a801-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="7a801-500">방화벽에서 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="7a801-501">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-502">Toonext 규칙 이동 FW 규칙 2-5 (RDP 규칙)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7a801-503">FW 규칙 6 및 7 (앱 규칙) 적용 안 함, toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7a801-504">Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7a801-505">Toonext 규칙 이동 FW 규칙 9 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="7a801-506">FW 규칙 10 (내 서브넷)은 적용, 트래픽을 허용, 방화벽 전달 트래픽 too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="7a801-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="7a801-507">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="7a801-508">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-509">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="7a801-510">적절 한 인증 및 권한 부여 라고 가정할 경우 IIS01 hello 요청을 수락 및 응답</span><span class="sxs-lookup"><span data-stu-id="7a801-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="7a801-511">hello UDR 프런트 엔드 서브넷에 경로로 hello 방화벽 hello 다음 홉</span><span class="sxs-lookup"><span data-stu-id="7a801-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="7a801-512">이어서 hello 프런트 엔드 서브넷 hello 응답에 대 한 아웃 바운드 NSG 규칙 없는 ï ´ ù</span><span class="sxs-lookup"><span data-stu-id="7a801-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="7a801-513">Hello 방화벽에서 기존 세션의 경우 이것이이 응답이 허용 하 고 hello 방화벽 hello 응답 tooAppVM02를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="7a801-514">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="7a801-515">Toonext 규칙 이동 NSG 규칙 1 (블록 인터넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="7a801-516">서브넷 toosubnet 트래픽을 허용 하는 기본 NSG 규칙, 트래픽이 허용 됩니다, 그리고 NSG 규칙 처리를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="7a801-517">AppVM02는 hello 응답 수신</span><span class="sxs-lookup"><span data-stu-id="7a801-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="7a801-518">(거부 됨) 인터넷 직접 tooWeb 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="7a801-519">인터넷 사용자가 tooaccess hello 웹 IIS01를 통해 서버 hello FrontEnd001.CloudApp.Net 서비스</span><span class="sxs-lookup"><span data-stu-id="7a801-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7a801-520">HTTP 트래픽에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스를 통과 하지는 및 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7a801-521">어떤 이유로 hello 끝점 열려 있던 경우 hello 프런트 엔드 서브넷에 NSG (블록 인터넷) hello를이 트래픽 차단</span><span class="sxs-lookup"><span data-stu-id="7a801-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="7a801-522">마지막으로, hello 프런트 엔드 서브넷 UDR 경로 hello 다음 홉으로 IIS01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답의 3 개 이상 독립적인 층 따라서 방어 hello 간의 인터넷 및 IIS01 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="7a801-523">(거부 됨) 인터넷 tooBackend 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="7a801-524">인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="7a801-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="7a801-525">파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지</span><span class="sxs-lookup"><span data-stu-id="7a801-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7a801-526">어떤 이유로 hello 끝점 열려 있던 경우 hello NSG (블록 인터넷)를이 트래픽 차단</span><span class="sxs-lookup"><span data-stu-id="7a801-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="7a801-527">마지막으로, hello UDR 경로 hello 다음 홉으로 AppVM01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답 따라서 방어 사이의 세 개 이상의 독립 층 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 인터넷 및 AppVM01 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="7a801-528">(거부 됨) 프런트 엔드 서버 tooBackend 서버</span><span class="sxs-lookup"><span data-stu-id="7a801-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="7a801-529">IIS01 보안이 손상 되 고 서버가 tooscan hello 백 엔드 서브넷을 시도 하는 악성 코드를 실행 중인 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="7a801-530">hello 프런트 엔드 서브넷 UDR 경로 hello 다음 홉으로 IIS01 toohello 방화벽에서 아웃 바운드 트래픽을 보낼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="7a801-531">이것이 하 여 변경할 수 있는 hello VM을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="7a801-532">hello 방화벽 hello 요청이 tooAppVM01, 또는 트래픽 수 tooFW 규칙 7-9) (인해 hello 방화벽에 의해 잠재적으로 허용 되는 DNS 조회에 대 한 DNS 서버 toohello 경우 hello 트래픽을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="7a801-533">기타 트래픽은 FW 규칙 11(모두 거부)에서 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="7a801-534">Hello 방화벽에서 이동 하는 위협 검색을 사용할 수 (이 문서에서는 다루지 않습니다, 고급 위협 기능이 특정 네트워크 장치에 대 한 hello 공급 업체 설명서를 참조)를 포함 하 여 전달 규칙 기본 hello에서 허용 되는 트래픽 이 항목에 설명 된 hello 트래픽 알려진된 서명이 나 고급 위협 규칙 플래그를 지정 하는 패턴을 포함 하는 경우 문서 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="7a801-535">(거부) DNS 서버에서 인터넷 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="7a801-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="7a801-536">인터넷 사용자가 toolookup BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드</span><span class="sxs-lookup"><span data-stu-id="7a801-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="7a801-537">DNS 트래픽에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스를 통과 하지는 및 hello 서버에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="7a801-538">Hello hello 프런트 엔드 서브넷에 NSG 규칙 (블록 인터넷)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우</span><span class="sxs-lookup"><span data-stu-id="7a801-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="7a801-539">마지막으로, hello 백 엔드 서브넷 UDR 경로 hello 다음 홉으로 DNS01 toohello 방화벽에서 모든 아웃 바운드 트래픽을 보내는 것과 및 hello 방화벽은 비대칭 트래픽으로 표시 되는이 놓습니다 hello 아웃 바운드 응답의 3 개 이상 독립적인 층 따라서 방어 hello 간의 인터넷 및 DNS01 권한이 없음/부적절 한 액세스를 방지 하는 클라우드 서비스를 통해 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="7a801-540">(거부 됨) 방화벽을 통해 인터넷 tooSQL 액세스</span><span class="sxs-lookup"><span data-stu-id="7a801-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="7a801-541">인터넷 사용자가 SecSvc001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="7a801-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="7a801-542">SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 고 hello 방화벽에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="7a801-543">어떤 이유로 SQL 끝점 열려 있던 hello 방화벽 규칙을 처리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="7a801-544">Toonext 규칙 이동 FW 규칙 1 (FW Mgmt) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="7a801-545">FW 규칙 2-5 (RDP 규칙), 적용 하지 않는 toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="7a801-546">FW 규칙 6 및 7 (응용 프로그램 규칙) 적용 안 함, toonext 규칙 이동</span><span class="sxs-lookup"><span data-stu-id="7a801-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="7a801-547">Toonext 규칙 이동 FW 규칙 8 (tooInternet) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="7a801-548">Toonext 규칙 이동 FW 규칙 9 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="7a801-549">Toonext 규칙 이동 FW 규칙 10 (내 서브넷) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="7a801-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="7a801-550">FW 규칙 11(모두 거부)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="7a801-551">참조</span><span class="sxs-lookup"><span data-stu-id="7a801-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="7a801-552">기본 스크립트 및 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="7a801-552">Main Script and Network Config</span></span>
<span data-ttu-id="7a801-553">PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="7a801-554">Hello 네트워크 구성 "NetworkConf2.xml" 라는 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="7a801-555">필요에 따라 hello 사용자 정의 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="7a801-556">Hello 스크립트를 실행 한 다음 위의 hello 방화벽 규칙 설정 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="7a801-557">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="7a801-557">Full Script</span></span>
<span data-ttu-id="7a801-558">이 스크립트는 hello 사용자 정의 변수를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="7a801-559">Tooan Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="7a801-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="7a801-560">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="7a801-560">Create a new storage account</span></span>
3. <span data-ttu-id="7a801-561">VNet을 새로 만들고 hello 네트워크 구성 파일에 정의 된 대로 세 개의 서브넷</span><span class="sxs-lookup"><span data-stu-id="7a801-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="7a801-562">5개의 가상 머신(1개 방화벽, 4개 Windows Server VM)을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="7a801-563">다음을 포함하여 UDR을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="7a801-564">2개의 새 경로 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="7a801-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="7a801-565">경로 toohello 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="7a801-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="7a801-566">바인딩할 테이블 tooappropriate 서브넷</span><span class="sxs-lookup"><span data-stu-id="7a801-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="7a801-567">IP 전달은 hello NVA에서 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7a801-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="7a801-568">다음을 포함하여 NSG를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="7a801-569">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="7a801-569">Creating a NSG</span></span>
   2. <span data-ttu-id="7a801-570">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="7a801-570">Adding a rule</span></span>
   3. <span data-ttu-id="7a801-571">바인딩 hello NSG toohello 적절 한 서브넷</span><span class="sxs-lookup"><span data-stu-id="7a801-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="7a801-572">이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a801-573">이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="7a801-574">빨간색 오류 메시지만 심각한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
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

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="7a801-575">네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="7a801-575">Network Config File</span></span>
<span data-ttu-id="7a801-576">업데이트 된 위치와이 xml 파일을 저장 하 고 hello 링크 toothis toohello $NetworkConfigFile 변수 위의 hello 스크립트에서 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a801-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="7a801-577">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="7a801-577">Sample Application Scripts</span></span>
<span data-ttu-id="7a801-578">Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="7a801-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "NVA, NSG, UDR을 사용하는 양방향 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Hello 방화벽 규칙의 논리적 보기"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "프런트 엔드 네트워크 개체 만들기"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "DNS 서버 개체 만들기"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "기본 RDP 규칙의 복사본"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 규칙"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "응용 프로그램 리디렉션 아이콘"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "대상 NAT 아이콘"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "전달 아이콘"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "방화벽 관리 규칙"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "방화벽 RDP 규칙"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "방화벽 웹 규칙"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "방화벽 AppVM01 규칙"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "방화벽 아웃바운드 규칙"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "방화벽 DNS 규칙"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "VNet 내 방화벽 규칙"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "방화벽 거부 규칙"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "방화벽 규칙 활성화"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
