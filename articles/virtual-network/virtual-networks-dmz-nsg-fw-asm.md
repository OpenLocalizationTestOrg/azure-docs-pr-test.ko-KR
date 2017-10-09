---
title: "예 – aaaDMZ DMZ tooprotect 방화벽과 Nsg로 응용 프로그램을 작성 | Microsoft Docs"
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
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="0b7cd-103">예제 2 – DMZ tooprotect 방화벽과 Nsg로 응용 프로그램을 작성</span><span class="sxs-lookup"><span data-stu-id="0b7cd-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="0b7cd-104">[Toohello 보안 모범 사례 페이지 경계를 반환 합니다.][HOME]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="0b7cd-105">이 예에서는 방화벽, 4개의 Windows Server 및 네트워크 보안 그룹이 포함된 DMZ를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="0b7cd-106">그는 또한 안내 각각 hello 관련 명령 tooprovide의 각 단계에 대 한 깊은 이해가.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="0b7cd-107">이기도 한 트래픽 시나리오 섹션 tooprovide 심층 분석 하는 단계별 트래픽 hello 계층의 철저 한 방어 기능을 통해 진행 방법 hello DMZ 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="0b7cd-108">마지막으로 hello references 섹션에는 전체 코드 hello 및 명령 toobuild이 환경 tootest 및 다양 한 시나리오와 실험입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="0b7cd-109">![NVA NSG와 인바운드 DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="0b7cd-110">환경 설명</span><span class="sxs-lookup"><span data-stu-id="0b7cd-110">Environment Description</span></span>
<span data-ttu-id="0b7cd-111">이 예제는 hello 다음을 포함 하는 구독:</span><span class="sxs-lookup"><span data-stu-id="0b7cd-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="0b7cd-112">두 클라우드 서비스: "FrontEnd001" 및 "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="0b7cd-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="0b7cd-113">"FrontEnd" 및 "BackEnd"의 두 서브넷을 포함하는 가상 네트워크 "CorpNetwork"</span><span class="sxs-lookup"><span data-stu-id="0b7cd-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="0b7cd-114">적용 된 tooboth 서브넷은 단일 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="0b7cd-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="0b7cd-115">이 예제에서는 Barracuda NextGen 방화벽에서 네트워크 가상 어플라이언스 toohello 프런트 엔드 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="0b7cd-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="0b7cd-116">응용 프로그램 웹 서버("IIS01")를 나타내는 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="0b7cd-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="0b7cd-117">응용 프로그램 백 엔드 서버("AppVM01", "AppVM02")를 나타내는 두 Windows 서버</span><span class="sxs-lookup"><span data-stu-id="0b7cd-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="0b7cd-118">DNS 서버("DNS01")를 나타내는 Windows Server</span><span class="sxs-lookup"><span data-stu-id="0b7cd-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="0b7cd-119">이 예제에서는 다양 한 다른 네트워크 가상 어플라이언스를이 예제에 사용 될 수는 hello Barracuda NextGen 방화벽을 사용 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="0b7cd-120">아래 hello references 섹션에는 PowerShell 스크립트를 위에서 설명한 hello 환경의 대부분 빌드됩니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="0b7cd-121">건물 hello Vm 및 가상 네트워크를 hello 예제 스크립트에 의해 수행 하지만이 문서에 자세히 설명에서 하지 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="0b7cd-122">toobuild hello 환경:</span><span class="sxs-lookup"><span data-stu-id="0b7cd-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="0b7cd-123">Hello 네트워크 구성 xml 파일 (이름, 위치 및 IP 주소 toomatch hello 주어진 시나리오에 업데이트) hello references 섹션에 포함 된 저장</span><span class="sxs-lookup"><span data-stu-id="0b7cd-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="0b7cd-124">Hello 스크립트 toomatch hello 환경 hello 스크립트의 update hello 사용자 변수는 toobe (구독, 서비스 이름 등)에 대해 실행</span><span class="sxs-lookup"><span data-stu-id="0b7cd-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="0b7cd-125">PowerShell에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="0b7cd-126">**참고**: hello PowerShell 스크립트에서에서 표시 하는 hello 지역 hello 네트워크 구성 xml 파일에서 표시 하는 hello 지역 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="0b7cd-127">Hello 스크립트가 성공적으로 실행 되 면 이후 스크립트 단계를 수행 하는 hello는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="0b7cd-128">이 이라는 hello 섹션에서 설명 되 hello 방화벽 규칙을 설정,: 방화벽 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="0b7cd-129">필요에 따라 hello references 섹션에는 두 개의 스크립트 tooset hello 웹 서버와이 DMZ 구성을 테스트 하는 간단한 웹 응용 프로그램 tooallow와 응용 프로그램 서버.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="0b7cd-130">hello 다음 섹션에서는 대부분의 hello 스크립트 문 상대 tooNetwork 보안 그룹을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="0b7cd-131">네트워크 보안 그룹(NSG)</span><span class="sxs-lookup"><span data-stu-id="0b7cd-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="0b7cd-132">이 예에서는 NSG 그룹을 빌드한 후 6개의 규칙과 함께 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="0b7cd-133">일반적으로 특정 "Allow" 규칙을 먼저 만든 하 고 보다 일반적인 "거부" 규칙을 마지막 hello 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="0b7cd-134">우선 순위가 할당 된 hello는 규칙이 먼저 평가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="0b7cd-135">트래픽 tooapply tooa 특정 규칙 발견 되 면 더 이상 규칙이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="0b7cd-136">NSG 규칙의 hello에 적용할 수 측면에서 볼 hello hello 서브넷의 인바운드 또는 아웃 바운드 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="0b7cd-137">선언적 규칙에 따라 hello 인바운드 트래픽에 대 한 빌드 중인:</span><span class="sxs-lookup"><span data-stu-id="0b7cd-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="0b7cd-138">내부 DNS 트래픽(포트 53) 허용됨</span><span class="sxs-lookup"><span data-stu-id="0b7cd-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="0b7cd-139">RDP 트래픽 (포트 3389 hello 인터넷 tooany VM에서 에서) 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="0b7cd-140">Hello 인터넷 toohello NVA (방화벽)에서 HTTP 트래픽 (포트 80)가 허용</span><span class="sxs-lookup"><span data-stu-id="0b7cd-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="0b7cd-141">(모든 포트) IIS01 tooAppVM1에서 모든 트래픽을 허용합니다</span><span class="sxs-lookup"><span data-stu-id="0b7cd-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="0b7cd-142">전체 VNet (두 서브넷)에서 거부 된 hello 인터넷 toohello에서 모든 트래픽 (모든 포트)</span><span class="sxs-lookup"><span data-stu-id="0b7cd-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="0b7cd-143">Hello 프런트 엔드 서브넷 toohello 백 엔드 서브넷에서 모든 트래픽 (모든 포트) 거부 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="0b7cd-144">이러한 규칙 바인딩된 tooeach 서브넷이 있는 HTTP 요청을 한 hello 인터넷 toohello 웹 서버에서 바인딩된 경우 모두 규칙 3 (허용)이 고 5 (거부) 적용 하는 것을 히 규칙 3 보다 우선 순위가 규칙 5는 하지 고려해 야 하 고 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="0b7cd-145">따라서 toohello 방화벽 hello HTTP 요청 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="0b7cd-146">동일한 트래픽이 해당 tooreach hello DNS01 서버를 시도 하 고, 규칙 5 (거부) hello 첫 번째 tooapply 및 hello 트래픽 toopass toohello 서버 허용 되지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="0b7cd-147">(제외 규칙 1 및 4에서에서 허용 된 트래픽) toohello 백 엔드 서브넷 통하게에서 6 (거부) 블록 hello 프런트 엔드 서브넷 규칙, hello 백 엔드 네트워크 보호는 공격자가 손상 hello에서 웹 응용 프로그램 hello 프런트 엔드, hello 공격자가 있을 경우 제한 된 액세스 toohello 백 엔드 "보호" (만 hello AppVM01 서버에서 노출 tooresources) 네트워크.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="0b7cd-148">Toohello 아웃 트래픽을 허용 하는 기본 아웃 바운드 규칙이 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="0b7cd-149">이 예에서는 아웃바운드 트래픽을 허용하고 아웃바운드 규칙을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="0b7cd-150">양방향에서 트래픽 아래로 toolock, 사용자 정의 된 라우팅 필수가, hello에서 찾을 수 있는 다른 예에 대해서는이 [주요 보안 경계 문서][HOME]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="0b7cd-151">위의 설명 hello NSG 규칙에서 매우 유사한 toohello NSG 규칙은 [예제 1-Nsg 간단한 DMZ 빌드][Example1]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="0b7cd-152">자세히 살펴보려면 각 NSG 규칙 및 해당 특성에 대 한 해당 문서의 hello NSG 설명을 검토 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="0b7cd-153">방화벽 규칙</span><span class="sxs-lookup"><span data-stu-id="0b7cd-153">Firewall Rules</span></span>
<span data-ttu-id="0b7cd-154">관리 클라이언트에서는 toobe PC toomanage hello 방화벽에 설치 되어 있어야 하 고 필요한 hello 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="0b7cd-155">어떻게 toomanage hello 장치에 hello 설명서 방화벽 (또는 다른 NVA)에서 공급 업체를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="0b7cd-156">이 섹션의 나머지 부분은 hello hello 공급 업체 관리 클라이언트 (즉, 하지 hello Azure 포털 또는 PowerShell)를 통해 자체 hello 방화벽의 hello 구성에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="0b7cd-157">클라이언트 다운로드 및 연결 toohello Barracuda이 예에서 사용에 대 한 지침은 여기: [Barracuda NG 관리자](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="0b7cd-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="0b7cd-158">Hello 방화벽에서 전달 규칙 toobe 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="0b7cd-159">하나의 전달 NAT 규칙은이 예에서는 인터넷 트래픽 inbound toohello 방화벽 및 웹 서버 toohello 라우트, 하므로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="0b7cd-160">이 예제에서는 hello에 사용 된 Barracuda NextGen 방화벽 hello에 규칙 것 대상 NAT 규칙 ("Dst NAT") toopass이이 트래픽을입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="0b7cd-161">toocreate hello 다음 규칙 (또는 기존 기본 규칙 확인) hello Operational 구성 섹션에서 규칙 집합을 toohello 구성 탭 이동 hello Barracuda NG 관리 클라이언트 대시보드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="0b7cd-162">표 호출 하 여 "Main 규칙" hello 방화벽에 대 한 규칙 활성화 및 비활성화 된 기존 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="0b7cd-163">Hello 오른쪽 상단의이 눈금은 작은 녹색 "+" 단추를 클릭이 toocreate 새 규칙 (참고: 방화벽 "잠겨" 변경에 대 한 단추를 "잠글"으로 표시 하 고는 없습니다 toocreate 또는 규칙 편집을 클릭 표시 되 면이 단추 너무 "잠금 해제" hello, ruleset 편집).</span><span class="sxs-lookup"><span data-stu-id="0b7cd-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="0b7cd-164">기존 규칙 tooedit을 원한다 해당 규칙을 선택, 마우스 오른쪽 단추로 클릭 하 고 편집할 규칙을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="0b7cd-165">새 규칙을 만들고 "WebTraffic"과 같은 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="0b7cd-166">hello 대상 NAT 규칙 아이콘은 다음과 같습니다: ![대상 NAT 아이콘][2]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="0b7cd-167">자체 hello 규칙 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="0b7cd-168">![방화벽 규칙][3]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="0b7cd-169">여기 적중 hello 방화벽 tooreach HTTP (포트 80 또는 443을 HTTPS)을 시도 하는 모든 인바운드 주소 전송 방화벽의 "DHCP1 로컬 IP" 인터페이스 및 리디렉션된 toohello hello 10.0.1.5의 IP 주소와 웹 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="0b7cd-170">포트 80 및 포트 80에서 진행 중인 toohello 웹 서버에서 들어오는 hello 트래픽 이후 포트 변경 안 함이 필요 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="0b7cd-171">그러나 hello 대상 목록 했을 수 10.0.1.5:8080 포트 8080 따라서 변환에 웹 서버 수신 대기 하는 경우 인바운드 포트 80 hello 웹 서버에서 방화벽 tooinbound 포트 8080 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="0b7cd-172">연결 방법은 해야도 수 표시를 hello 인터넷에서에서 대상 규칙 hello에 대 한 "동적 SNAT"는 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="0b7cd-173">하나의 규칙만 만들어지지만 우선순위가 바르게 설정되는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="0b7cd-174">Hello 방화벽에 대 한 모든 규칙의 hello 그리드에서 ("hello"BLOCKALL"규칙) 아래 hello 아래쪽에 새이 규칙은에 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="0b7cd-175">웹 트래픽에 대 한 hello 새로 만든 규칙 hello BLOCKALL 규칙 보다 높은 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="0b7cd-176">해야 hello 규칙을 만든 후 toohello 방화벽 푸시되 며 다음 처리 되 고 활성화, 이렇게 하지 않으면 hello 규칙 변경 내용이 적용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="0b7cd-177">hello 푸시 및 활성화 프로세스는 hello 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="0b7cd-178">규칙 활성화</span><span class="sxs-lookup"><span data-stu-id="0b7cd-178">Rule Activation</span></span>
<span data-ttu-id="0b7cd-179">Hello로 ruleset tooadd이이 규칙을 수정 hello ruleset 해야 toohello 방화벽을 업로드 하 고 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="0b7cd-180">![방화벽 규칙 활성화][4]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="0b7cd-181">Hello 관리 클라이언트의 오른쪽 상단 모서리 hello 단추의 클러스터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="0b7cd-182">Hello "보낼 변경" 단추 toosend hello 수정 규칙 toohello 방화벽 클릭 hello "활성화" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="0b7cd-183">이 예에서는 환경 구축 hello 방화벽 규칙 집합의 정품 인증의 hello 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="0b7cd-184">필요에 따라 hello에 hello 후 빌드 스크립트 참조 섹션 수 실행 tooadd 아래의 트래픽 시나리오는 응용 프로그램 toothis 환경 tootest hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b7cd-185">것이 중요 한 toorealize는 직접 hello 웹 서버를 하지 적중지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="0b7cd-186">브라우저에서 FrontEnd001.CloudApp.Net HTTP 페이지를 요청 하면이 트래픽을 toohello 방화벽 하지 hello hello HTTP 끝점 (포트 80) 전달 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="0b7cd-187">다음 방화벽 hello toohello 웹 서버를 요청 하는 Nat 위에서 만든 toohello 규칙에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="0b7cd-188">트래픽 시나리오</span><span class="sxs-lookup"><span data-stu-id="0b7cd-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="0b7cd-189">(사용 가능) 웹 tooWeb 방화벽을 통해 서버</span><span class="sxs-lookup"><span data-stu-id="0b7cd-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="0b7cd-190">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 HTTP 페이지를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="0b7cd-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="0b7cd-191">포트 80 toofirewall 10.0.1.4:80에서 로컬 인터페이스에 대 한 열린 끝점을 통해 클라우드 서비스 전달 트래픽</span><span class="sxs-lookup"><span data-stu-id="0b7cd-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="0b7cd-192">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-193">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="0b7cd-194">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="0b7cd-195">NSG 규칙 3 (인터넷 tooFirewall)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="0b7cd-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="0b7cd-196">트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="0b7cd-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="0b7cd-197">이 포트 80 트래픽, toohello 웹 서버 IIS01 리디렉션합니다 방화벽 전달 규칙 참조</span><span class="sxs-lookup"><span data-stu-id="0b7cd-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="0b7cd-198">IIS01 웹 트래픽에 대 한 수신이 요청을 수신 하 고 hello 요청 처리를 시작합니다</span><span class="sxs-lookup"><span data-stu-id="0b7cd-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="0b7cd-199">IIS01 정보 AppVM01에 SQL Server hello를 요청</span><span class="sxs-lookup"><span data-stu-id="0b7cd-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="0b7cd-200">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="0b7cd-201">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="0b7cd-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-202">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="0b7cd-203">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="0b7cd-204">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="0b7cd-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="0b7cd-205">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="0b7cd-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="0b7cd-206">AppVM01 hello SQL 쿼리를 받아 응답</span><span class="sxs-lookup"><span data-stu-id="0b7cd-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="0b7cd-207">백 엔드 서브넷 hello 응답 hello에 대 한 없는 아웃 바운드 규칙은 사용할 수 있기 때문</span><span class="sxs-lookup"><span data-stu-id="0b7cd-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="0b7cd-208">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="0b7cd-209">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="0b7cd-210">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="0b7cd-211">hello IIS 서버 hello SQL 응답을 수신 하 고 hello HTTP 응답을 완료 및 toohello 요청자에 게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="0b7cd-212">Hello 방화벽에 대 한 hello 응답 대상 (처음)은 hello 방화벽에서 NAT 세션 이므로,</span><span class="sxs-lookup"><span data-stu-id="0b7cd-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="0b7cd-213">hello 방화벽 hello 응답 hello 웹 서버에서에서 주고 받는 백 toohello 인터넷 사용자</span><span class="sxs-lookup"><span data-stu-id="0b7cd-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="0b7cd-214">이어서 hello 프런트 엔드 서브넷 hello 응답에 아웃 바운드 규칙이 없습니다 허용 되 고 hello 인터넷 사용자 hello 웹 페이지 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="0b7cd-215">(사용 가능) RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="0b7cd-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="0b7cd-216">인터넷에서 서버 관리자 요청 BackEnd001.CloudApp.Net:xxxxx 여기서 xxxxx는 RDP tooAppVM01 hello 임의로 할당 된 포트 번호에서 RDP 세션 tooAppVM01 (hello 할당 된 포트를 찾을 수 hello Azure 포털에서 또는 PowerShell을 통해)</span><span class="sxs-lookup"><span data-stu-id="0b7cd-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="0b7cd-217">방화벽은 hello FrontEnd001.CloudApp.Net 주소 에서만 수신 대기 하는 hello, 이후이 트래픽 흐름에 포함 되지 않은</span><span class="sxs-lookup"><span data-stu-id="0b7cd-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="0b7cd-218">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-219">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="0b7cd-220">NSG 규칙 2(RDP)가 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="0b7cd-221">아웃바운드 규칙이 없는 경우 기본 규칙이 적용되고 반환 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="0b7cd-222">RDP 세션이 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-222">RDP session is enabled</span></span>
6. <span data-ttu-id="0b7cd-223">AppVM01에서 사용자 이름과 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="0b7cd-224">(허용) DNS 서버에서 웹 서버 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="0b7cd-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="0b7cd-225">웹 www.data.gov 하지만 요구 tooresolve hello 주소에서 데이터 피드 IIS01, 서버 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="0b7cd-226">hello 네트워크 구성을 DNS01 hello VNet 목록에 대 한 (hello 백 엔드 서브넷에 10.0.2.4) hello 주 DNS 서버로 IIS01 보냅니다 hello DNS 요청 tooDNS01</span><span class="sxs-lookup"><span data-stu-id="0b7cd-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="0b7cd-227">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="0b7cd-228">백 엔드 서브넷이 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-229">NSG 규칙 1(DNS)이 적용되고 트래픽이 허용되며 규칙 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="0b7cd-230">DNS 서버 hello 요청 수신</span><span class="sxs-lookup"><span data-stu-id="0b7cd-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="0b7cd-231">DNS 서버 캐시 hello 주소 없고 루트 DNS 서버 hello에 요청 인터넷</span><span class="sxs-lookup"><span data-stu-id="0b7cd-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="0b7cd-232">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="0b7cd-233">이 세션은 내부적으로 시작 된 이후 인터넷 DNS 서버 응답을 hello 응답이 허용</span><span class="sxs-lookup"><span data-stu-id="0b7cd-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="0b7cd-234">DNS 서버 hello 응답을 캐시 및 toohello 초기 요청 백 tooIIS01 이벤트에 응답</span><span class="sxs-lookup"><span data-stu-id="0b7cd-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="0b7cd-235">백 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="0b7cd-236">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="0b7cd-237">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="0b7cd-238">hello 트래픽이 허용 됩니다 서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽은 허용</span><span class="sxs-lookup"><span data-stu-id="0b7cd-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="0b7cd-239">IIS01은 DNS01에서 hello 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="0b7cd-240">(허용) AppVM01에서 웹 서버가 파일 액세스</span><span class="sxs-lookup"><span data-stu-id="0b7cd-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="0b7cd-241">IIS01은 AppVM01에서 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="0b7cd-242">프런트 엔드 서브넷에 아웃바운드 규칙이 없고 트래픽이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="0b7cd-243">인바운드 규칙 처리를 시작 하는 hello 백 엔드 서브넷:</span><span class="sxs-lookup"><span data-stu-id="0b7cd-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-244">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="0b7cd-245">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="0b7cd-246">Toonext 규칙 이동 NSG 규칙 3 (인터넷 tooFirewall) 적용 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="0b7cd-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="0b7cd-247">NSG 규칙 4 (IIS01 tooAppVM01)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="0b7cd-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="0b7cd-248">AppVM01은 hello 요청을 받아 파일 (액세스 권한이 부여 가정)를 사용 하 여 응답</span><span class="sxs-lookup"><span data-stu-id="0b7cd-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="0b7cd-249">백 엔드 서브넷 hello 응답 hello에 대 한 없는 아웃 바운드 규칙은 사용할 수 있기 때문</span><span class="sxs-lookup"><span data-stu-id="0b7cd-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="0b7cd-250">프런트 엔드 서브넷에서 인바운드 규칙 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-251">사용자에 게 적용 hello NSG 규칙 중 tooInbound 트래픽을 hello 백 엔드 서브넷 toohello 프런트 엔드 서브넷에서 적용 되는 NSG 규칙이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="0b7cd-252">서브넷 간의 트래픽을 허용 하는 hello 기본 시스템 규칙이이 트래픽을 하면 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="0b7cd-253">hello IIS 서버 hello 파일 수신</span><span class="sxs-lookup"><span data-stu-id="0b7cd-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="0b7cd-254">(거부 됨) 직접 tooWeb 웹 서버</span><span class="sxs-lookup"><span data-stu-id="0b7cd-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="0b7cd-255">웹 서버 hello, IIS01, 및 hello 방화벽 이후는 hello에 동일한 클라우드 서비스를 공유 hello 동일한 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="0b7cd-256">모든 HTTP 트래픽을 전송할 것 따라서 toohello 방화벽입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="0b7cd-257">Hello 요청이 성공적으로 제공 될 것 동안 이동할 수 없습니다 웹 서버 toohello 전달 것을 직접을 정상적으로 hello를 통해 방화벽 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="0b7cd-258">참조 hello hello 트래픽 흐름에 대 한이 섹션의 첫 번째 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="0b7cd-259">(거부 됨) 웹 tooBackend 서버</span><span class="sxs-lookup"><span data-stu-id="0b7cd-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="0b7cd-260">인터넷 사용자가 tooaccess hello BackEnd001.CloudApp.Net 서비스를 통해 AppVM01에 있는 파일</span><span class="sxs-lookup"><span data-stu-id="0b7cd-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="0b7cd-261">파일 공유에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지</span><span class="sxs-lookup"><span data-stu-id="0b7cd-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="0b7cd-262">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 인 경우</span><span class="sxs-lookup"><span data-stu-id="0b7cd-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="0b7cd-263">(거부) DNS 서버에서 웹 DNS 조회</span><span class="sxs-lookup"><span data-stu-id="0b7cd-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="0b7cd-264">인터넷 사용자가 toolookup hello BackEnd001.CloudApp.Net 서비스를 통해 DNS01에 내부 DNS 레코드</span><span class="sxs-lookup"><span data-stu-id="0b7cd-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="0b7cd-265">DNS에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 한 hello 서버에 도달 하지</span><span class="sxs-lookup"><span data-stu-id="0b7cd-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="0b7cd-266">NSG 규칙 5 (인터넷 tooVNet)이이 트래픽을 차단는 몇 가지 이유로 hello 끝점 열려 있던 경우 (참고: 규칙 1 (DNS) 같은 두 가지 이유로 적용 되지 않습니다, 첫 번째 hello 소스 주소는 인터넷을 hello,이 규칙은 toohello 적용 됩니다. 또한 지역 VNet으로 hello 원본 이 트래픽이 거부 하지 않습니다 것 이므로 허용 규칙)</span><span class="sxs-lookup"><span data-stu-id="0b7cd-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="0b7cd-267">(거부 됨) 방화벽을 통해 웹 tooSQL 액세스</span><span class="sxs-lookup"><span data-stu-id="0b7cd-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="0b7cd-268">인터넷 사용자가 FrontEnd001.CloudApp.Net에서 SQL 데이터를 요청합니다(인터넷 연결 클라우드 서비스).</span><span class="sxs-lookup"><span data-stu-id="0b7cd-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="0b7cd-269">SQL에 대 한 열린 끝점을 하나도 있을 경우이 hello 클라우드 서비스에 전달 하는 고 hello 방화벽에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="0b7cd-270">어떤 이유로 끝점 열려 있던 hello 프런트 엔드 서브넷 인바운드 규칙 처리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="0b7cd-271">Toonext 규칙 이동 NSG 규칙 1 (DNS)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="0b7cd-272">Toonext 규칙 이동 NSG 규칙 2 (RDP)를 적용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="0b7cd-273">NSG 규칙 2 (인터넷 tooFirewall)은 적용, 트래픽은 허용, 중지 규칙 처리</span><span class="sxs-lookup"><span data-stu-id="0b7cd-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="0b7cd-274">트래픽은 hello 방화벽 (10.0.1.4)의 내부 IP 주소에 도달</span><span class="sxs-lookup"><span data-stu-id="0b7cd-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="0b7cd-275">SQL에 대 한 전달 규칙에 방화벽 및 삭제 합니다. hello 트래픽</span><span class="sxs-lookup"><span data-stu-id="0b7cd-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="0b7cd-276">결론</span><span class="sxs-lookup"><span data-stu-id="0b7cd-276">Conclusion</span></span>
<span data-ttu-id="0b7cd-277">이 방법은 방화벽 응용 프로그램을 보호 하 고 hello 백 엔드 서브넷 인바운드 트래픽에서 격리의 비교적 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="0b7cd-278">네트워크 보안 경계에 대한 더 많은 예와 개요는 [여기][HOME]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="0b7cd-279">참조</span><span class="sxs-lookup"><span data-stu-id="0b7cd-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="0b7cd-280">기본 스크립트 및 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="0b7cd-280">Main Script and Network Config</span></span>
<span data-ttu-id="0b7cd-281">PowerShell 스크립트 파일에 hello 전체 스크립트를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="0b7cd-282">Hello 네트워크 구성 "NetworkConf2.xml" 라는 파일에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="0b7cd-283">필요에 따라 hello 사용자 정의 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="0b7cd-284">Hello 스크립트를 실행 한 다음 위의 hello 방화벽 규칙 설정 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="0b7cd-285">전체 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b7cd-285">Full Script</span></span>
<span data-ttu-id="0b7cd-286">이 스크립트는 hello 사용자 정의 변수를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="0b7cd-287">Tooan Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="0b7cd-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="0b7cd-288">새 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="0b7cd-288">Create a new storage account</span></span>
3. <span data-ttu-id="0b7cd-289">VNet을 새로 만들고 hello 네트워크 구성 파일에 정의 된 대로 두 서브넷</span><span class="sxs-lookup"><span data-stu-id="0b7cd-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="0b7cd-290">4개의 Windows Server VM 빌드</span><span class="sxs-lookup"><span data-stu-id="0b7cd-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="0b7cd-291">다음을 포함하여 NSG 구성</span><span class="sxs-lookup"><span data-stu-id="0b7cd-291">Configure NSG including:</span></span>
   * <span data-ttu-id="0b7cd-292">NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="0b7cd-292">Creating a NSG</span></span>
   * <span data-ttu-id="0b7cd-293">규칙으로 채우기</span><span class="sxs-lookup"><span data-stu-id="0b7cd-293">Populating it with rules</span></span>
   * <span data-ttu-id="0b7cd-294">바인딩 hello NSG toohello 적절 한 서브넷</span><span class="sxs-lookup"><span data-stu-id="0b7cd-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="0b7cd-295">이 PowerShell 스크립트를 인터넷 연결된 PC 또는 서버에서 로컬로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b7cd-296">이 스크립트를 실행하는 경우 PowerShell에서 경고 또는 기타 정보 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="0b7cd-297">빨간색 오류 메시지만 심각한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-297">Only error messages in red are cause for concern.</span></span>
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
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
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
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="0b7cd-298">네트워크 구성 파일</span><span class="sxs-lookup"><span data-stu-id="0b7cd-298">Network Config File</span></span>
<span data-ttu-id="0b7cd-299">업데이트 된 위치와이 xml 파일을 저장 하 고 hello 링크 toothis toohello $NetworkConfigFile 변수 위의 hello 스크립트에서 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b7cd-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="0b7cd-300">샘플 응용 프로그램 스크립트</span><span class="sxs-lookup"><span data-stu-id="0b7cd-300">Sample Application Scripts</span></span>
<span data-ttu-id="0b7cd-301">Hello 링크에 제공 된다는이 및 다른 DMZ 예제는 예제 응용 프로그램 tooinstall 원하면: [샘플 응용 프로그램 스크립트][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="0b7cd-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "NSG와 인바운드 DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "대상 NAT 아이콘"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "방화벽 규칙"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "방화벽 규칙 활성화"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
