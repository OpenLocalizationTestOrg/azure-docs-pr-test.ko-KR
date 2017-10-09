---
title: "Azure 사용 하 여 aaaProtect 개인 데이터를 네트워크 보안 기능 | Microsoft Docs"
description: "Azure 네트워크 보안 기능을 사용하여 개인 데이터를 보호합니다."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="e074f-103">네트워크 보안 기능을 사용하여 개인 데이터 보호: Azure Application Gateway 및 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="e074f-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="e074f-104">이 문서 정보 및 Azure 응용 프로그램 게이트웨이 및 네트워크 보안 그룹 tooprotect 개인 데이터를 사용 하는 데 도움이 되는 절차를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups tooprotect personal data.</span></span>

<span data-ttu-id="e074f-105">다중 계층된 보안 전략 tooprotect hello 개인정보 취급 방침의 개인 데이터에 중요 한 요소는 SQL 삽입 또는 사이트 간 스크립팅 같은 일반적인 취약점 악용 으로부터 방어입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-105">An important element in a multi-layered security strategy tooprotect hello privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="e074f-106">Azure 가상 네트워크가 나가는 유지 원치 않는 네트워크 트래픽 중요 한 데이터 및 도구 toohelp 공격자 로부터 데이터를 보호 하는 Microsoft Azure에서는 잠재적인 손상 으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools toohelp protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="e074f-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="e074f-107">Scenario</span></span>

<span data-ttu-id="e074f-108">Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="e074f-109">이러한 노력의 furtherance에서 획득 여러 개의 더 작은 순항 이탈리아, 독일, 덴마크 및 hello 영국에 기반 하는 줄</span><span class="sxs-lookup"><span data-stu-id="e074f-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="e074f-110">hello 회사에서 Microsoft Azure의 hello toostore 회사 데이터 클라우드 및 처리 하 고이 데이터에 액세스 하는 가상 컴퓨터에서 응용 프로그램을 실행을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-110">hello company uses Microsoft Azure toostore corporate data in hello cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="e074f-111">이 데이터에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="e074f-112">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="e074f-113">hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="e074f-114">회사 직원 hello 회사의 원격 사무실 및 hello world 주변에 있는 여행사에서 hello 네트워크 액세스 toosome 회사 리소스에 액세스가 있고 함께 toointeract Azure Vm에서에서 호스팅되는 웹 기반 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-114">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources and use web-based applications hosted in Azure VMs toointeract with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="e074f-115">문제 설명</span><span class="sxs-lookup"><span data-stu-id="e074f-115">Problem statement</span></span>

<span data-ttu-id="e074f-116">hello 회사에서 고객의의 hello 개인 정보를 보호 해야 하 고 공격자가 개인 데이터에 노출 시킬 수 소프트웨어 취약점 toorun 악성 코드가 악용할에서 직원의 개인 데이터 저장 하거나 hello 회사의 클라우드 기반 응용 프로그램에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-116">hello company must protect hello privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities toorun malicious code that could expose personal data stored or used by hello company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="e074f-117">회사 목표</span><span class="sxs-lookup"><span data-stu-id="e074f-117">Company goal</span></span>

<span data-ttu-id="e074f-118">hello 사용자 권한이 없는 회사의 목표 tooensure에 액세스할 수 없습니다 회사 Azure 가상 네트워크 및 hello 응용 프로그램과 일반적인 취약점을 악용 하 여 상주 하는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-118">hello company’s goal tooensure that unauthorized persons cannot access corporate Azure Virtual Networks and hello applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="e074f-119">솔루션</span><span class="sxs-lookup"><span data-stu-id="e074f-119">Solutions</span></span>

<span data-ttu-id="e074f-120">Microsoft Azure에서는 보안 메커니즘 toohelp를 Azure 가상 네트워크를 입력할 원치 않는 트래픽에 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-120">Microsoft Azure provides security mechanisms toohelp prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="e074f-121">인바운드 및 아웃바운드 트래픽 제어는 일반적으로 방화벽에 의해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="e074f-122">Azure에서 간단한 분산된 방화벽으로 역할을 하는 웹 응용 프로그램 방화벽 hello로 응용 프로그램 게이트웨이 hello 및 보안 그룹 NSG (네트워크)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-122">In Azure, you can use hello Application Gateway with hello Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="e074f-123">이러한 도구는 toodetect를 사용 하 고 불필요 한 네트워크 트래픽을 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-123">These tools enable you toodetect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="e074f-124">Application Gateway/웹 응용 프로그램 방화벽</span><span class="sxs-lookup"><span data-stu-id="e074f-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="e074f-125">hello [웹 응용 프로그램 방화벽](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) hello의 구성 요소 (WAF) [Azure 응용 프로그램 게이트웨이](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) 이용 하는 일반적인 알려진 악의적인 공격의 대상이 되 고 있는 웹 응용 프로그램 보호 취약점입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-125">hello [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of hello [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="e074f-126">중앙 집중식 WAF는 웹 공격으로부터 보호하고, 응용 프로그램을 변경하지 않고도 보안 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="e074f-127">Azure WAF는 SQL 삽입, 교차 사이트 스크립팅, HTTP 프로토콜 위반 및 변칙, 봇, 크롤러, 스캐너, 일반적인 응용 프로그램 구성 오류, HTTP 서비스 거부 및 기타 일반적 공격(예: 명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할 및 원격 파일 포함 공격)을 포함하여 다양한 공격 범주를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="e074f-128">WAF와 응용 프로그램 게이트웨이 만들거나 WAF tooan 기존 응용 프로그램 게이트웨이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-128">You can create an application gateway with WAF, or add WAF tooan existing application gateway.</span></span> <span data-ttu-id="e074f-129">두 경우 모두 Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="e074f-130">WAF를 사용하여 응용 프로그램 게이트웨이를 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e074f-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="e074f-131">toocreate WAF 사용 하도록 설정 된 새 응용 프로그램 게이트웨이 뒤 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-131">toocreate a new application gateway with WAF enabled, do hello following:</span></span>

1. <span data-ttu-id="e074f-132">Hello 및 toohello Azure 포털에서에서 로그 **즐겨찾기** hello 포털의 창 클릭 **새로 만들기**</span><span class="sxs-lookup"><span data-stu-id="e074f-132">Log in toohello Azure portal and in hello **Favorites** pane of hello portal, click **New**</span></span>

2. <span data-ttu-id="e074f-133">Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-133">In hello **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="e074f-134">**Application Gateway**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="e074f-135">Azure 포털 toohello 이동 **새로 만들기 클릭 \> 네트워킹 \> 응용 프로그램 게이트웨이 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e074f-135">Navigate toohello Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![응용 프로그램 게이트웨이 만들기](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="e074f-137">Hello에 **기본 사항** 나타나는 블레이드 hello 필드 뒤에 대 한 hello 값을 입력: 이름, 계층 (Standard 또는 WAF) SKU 크기 (소형, 중형 또는 대형) 인스턴스 수 (2) 고가용성에 대 한 구독을 리소스 그룹 및 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-137">In hello **Basics** blade that appears, enter hello values for hello following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="e074f-138">Hello에 **설정** 아래에 나타나는 블레이드 **가상 네트워크**, 클릭 **가상 네트워크를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-138">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="e074f-139">열립니다 입력이 단계는 선택 가상 네트워크 블레이드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-139">This step opens enter hello Choose virtual network blade.</span></span>

7. <span data-ttu-id="e074f-140">클릭 **새로 만들기** tooopen hello **가상 네트워크 만들기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-140">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

8. <span data-ttu-id="e074f-141">다음 값에는 hello 입력: 이름, 주소 공간, 서브넷 이름입니다. 서브넷 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-141">Enter hello following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="e074f-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-142">Click **OK**.</span></span>

9. <span data-ttu-id="e074f-143">Hello에 **설정** 아래 블레이드 **프런트 엔드 IP 구성**, hello IP 주소 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-143">On hello **Settings** blade under **Frontend IP configuration**, choose hello IP address type.</span></span>

10. <span data-ttu-id="e074f-144">**공용 IP 주소 선택**, **새로 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="e074f-145">Hello 기본값을 허용 하 고 클릭 **확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e074f-145">Accept hello default value, and click **OK.**</span></span>

12. <span data-ttu-id="e074f-146">Hello에 **설정** 아래 블레이드 **수신기 구성**, HTTP 또는 HTTPS에서 toouse 선택 **프로토콜**합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-146">On hello **Settings** blade under **Listener configuration**, select toouse HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="e074f-147">HTTPS toouse는 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-147">toouse HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="e074f-148">Hello WAF 특정 설정을 구성: **상태 방화벽** (**Enabled**) 및 **방화벽 모드** (**방지**).</span><span class="sxs-lookup"><span data-stu-id="e074f-148">Configure hello WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="e074f-149">선택 하면 **검색** 트래픽 hello 모드로 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-149">If you choose **Detection** as hello mode, traffic is only logged.</span></span>

14. <span data-ttu-id="e074f-150">검토 hello **요약** 페이지 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-150">Review hello **Summary** page and click **OK**.</span></span> <span data-ttu-id="e074f-151">이제 hello 응용 프로그램 게이트웨이 대기 되 고 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-151">Now hello application gateway is queued up and created.</span></span>

<span data-ttu-id="e074f-152">Hello 응용 프로그램 게이트웨이 만든 후 tooit hello 포털에서 탐색할 수 있으며 hello 응용 프로그램 게이트웨이의 구성을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-152">After hello application gateway has been created, you can navigate tooit in hello portal and continue configuration of hello application gateway.</span></span>

![만든 응용 프로그램 게이트웨이](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a><span data-ttu-id="e074f-154">WAF tooan 기존 응용 프로그램을 추가 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="e074f-154">How do I add WAF tooan existing application?</span></span>

<span data-ttu-id="e074f-155">방지 모드에는 기존 응용 프로그램 게이트웨이 toosupport WAF tooupdate 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-155">tooupdate an existing application gateway toosupport WAF in prevention mode, do hello following:</span></span>

1. <span data-ttu-id="e074f-156">Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-156">In hello Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="e074f-157">클릭 하 여 hello hello에서 기존 응용 프로그램 게이트웨이 **모든 리소스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-157">Click hello existing Application Gateway in hello **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="e074f-158">참고: 이미 선택한 hello 구독에 여러 자원이 인 경우 이름을 입력할 수 있습니다 hello hello 필터의에서 이름으로...</span><span class="sxs-lookup"><span data-stu-id="e074f-158">Note: If hello subscription you selected already has several resources in it, you can enter hello name in hello Filter by name…</span></span> <span data-ttu-id="e074f-159">상자 tooeasily 액세스 hello DNS 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-159">box tooeasily access hello DNS zone.</span></span>
3. <span data-ttu-id="e074f-160">클릭 **웹 응용 프로그램 방화벽** hello 응용 프로그램 게이트웨이 설정 업데이트: **tooWAF 계층 업그레이드** (선택), **상태 방화벽** (사용)  **방화벽 모드** (차단).</span><span class="sxs-lookup"><span data-stu-id="e074f-160">Click **Web application firewall** and update hello application gateway settings: **Upgrade tooWAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="e074f-161">또한 tooconfigure 해야 규칙 집합 hello 고 비활성화 된 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-161">You also need tooconfigure hello rule set, and configure disabled rules.</span></span>

<span data-ttu-id="e074f-162">자세한 방법은 toocreate WAF 인 새 응용 프로그램 게이트웨이 방법을 tooadd WAF tooan 기존 응용 프로그램 게이트웨이 참조 [hello 포털을 사용 하 여 웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 작성 합니다.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span><span class="sxs-lookup"><span data-stu-id="e074f-162">For more detailed information on how toocreate a new application gateway with WAF and how tooadd WAF tooan existing application gateway, see [Create an application gateway with web application firewall by using hello portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="e074f-163">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="e074f-163">Network Security Groups</span></span>

<span data-ttu-id="e074f-164">A [네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) NSG ()를 허용 하거나 거부할 네트워크 트래픽 tooresources 너무 연결 하는 보안 규칙의 목록이 들어[Azure 가상 네트워크](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span><span class="sxs-lookup"><span data-stu-id="e074f-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic tooresources connected too[Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="e074f-165">Nsg 연결된 toosubnets 또는 개별 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-165">NSGs can be associated toosubnets or individual VMs.</span></span> <span data-ttu-id="e074f-166">NSG 연결된 tooa 서브넷 이면 tooall 리소스 연결 된 toohello 서브넷 hello 규칙에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-166">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> <span data-ttu-id="e074f-167">또한 VM 또는 NIC.는 NSG tooa를 연결 하 여 트래픽을 추가로 제한할 수</span><span class="sxs-lookup"><span data-stu-id="e074f-167">Traffic can further be restricted by also associating an NSG tooa VM or NIC.</span></span>

<span data-ttu-id="e074f-168">NSG에는 네 가지 속성, 즉 이름, 지역, 리소스 그룹 및 규칙이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="e074f-169">NSG에는 리소스 그룹에 없는 수 있습니다 모든 리소스 그룹에 연결 된 tooresources hello 리소스 hello의 일부인으로 NSG hello와 같은 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-169">Although an NSG exists in a resource group, it can be associated tooresources in any resource group, as long as hello resource is part of hello same Azure region as hello NSG.</span></span>

<span data-ttu-id="e074f-170">NSG 규칙에는 9가지 속성, 즉 이름, 프로토콜(TCP, UDP 또는 \*(UDP 및 TCP 외에도 ICMP 포함)), 원본 포트 범위, 대상 포트 범위, 원본 주소 접두사, 대상 주소 접두사, 방향(인바운드 또는 아웃바운드), 우선 순위(100-4096) 및 액세스 형식(허용 또는 거부)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="e074f-171">모든 Nsg 삭제 또는 작성 한 hello 규칙에 의해 재정의 될 수 있는 기본 규칙 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-171">All NSGs contain a set of default rules that can be deleted, or overridden by hello rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="e074f-172">NSG를 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e074f-172">How do I implement NSGs?</span></span>

<span data-ttu-id="e074f-173">계획, Nsg를 구현 하려면과 tootake 계정에 필요한 몇 가지 디자인 고려 사항.</span><span class="sxs-lookup"><span data-stu-id="e074f-173">Implementing NSGs requires planning, and there are several design considerations you need tootake into account.</span></span> <span data-ttu-id="e074f-174">여기에 NSG; 당 규칙 및 구독 당 Nsg의 hello 수에 대 한 제한 VNet과 서브넷 디자인, 특별 한 규칙, ICMP 트래픽을, 서브넷, 부하 분산 장치 및 계층의 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-174">These include limits on hello number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="e074f-175">NSG 계획 및 구현에 대한 자세한 지침과 샘플 배포 시나리오는 [네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e074f-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="e074f-176">NSG에서 규칙을 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="e074f-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="e074f-177">toocreate 인바운드 기존 NSG에서 규칙을 따르는 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-177">toocreate inbound rules in an existing NSG, do hello following:</span></span>

1. <span data-ttu-id="e074f-178">**찾아보기**를 클릭한 다음 **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="e074f-179">Nsg의 hello 목록에서 클릭 **NSG 프런트 엔드**, 차례로 **인바운드 보안 규칙입니다.**</span><span class="sxs-lookup"><span data-stu-id="e074f-179">In hello list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="e074f-180">인바운드 보안 규칙의 hello 목록에서 클릭 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e074f-180">In hello list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="e074f-181">Hello 필드 뒤에 hello 값을 입력: 이름, 우선 순위, 소스, 프로토콜, 원본 범위, 대상, 대상 포트 범위 및 작업.</span><span class="sxs-lookup"><span data-stu-id="e074f-181">Enter hello values in hello following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="e074f-182">새 규칙 hello 몇 초 후 hello NSG에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e074f-182">hello new rule will appear in hello NSG after a few seconds.</span></span>

![네트워크 보안 규칙](media/protect-netsec/inbound-security.png)

<span data-ttu-id="e074f-184">에 대 한 자세한 toocreate Nsg 서브넷에 있는 규칙을 만들어 하 고 프런트 엔드 및 백 엔드 서브넷과 NSG를 연결 하는 방법에 참조 [hello Azure 포털을 사용 하 여 네트워크 보안 그룹을 만듭니다.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span><span class="sxs-lookup"><span data-stu-id="e074f-184">For more instructions on how toocreate NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using hello Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e074f-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e074f-185">Next steps</span></span>

[<span data-ttu-id="e074f-186">Azure 네트워크 보안(영문)</span><span class="sxs-lookup"><span data-stu-id="e074f-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="e074f-187">Azure 네트워크 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="e074f-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="e074f-188">네트워크 보안 그룹에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e074f-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="e074f-189">WAF(웹 응용 프로그램 방화벽)</span><span class="sxs-lookup"><span data-stu-id="e074f-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
