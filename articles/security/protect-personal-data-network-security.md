---
title: "Azure 네트워크 보안 기능을 사용하여 개인 데이터 보호 | Microsoft Docs"
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
ms.openlocfilehash: b7a6343f37f890b65d9536eac34e1069d24ad97e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="4caa8-103">네트워크 보안 기능을 사용하여 개인 데이터 보호: Azure Application Gateway 및 네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4caa8-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="4caa8-104">이 문서는 Azure Application Gateway와 네트워크 보안 그룹을 사용하여 개인 데이터를 보호하는 데 도움이 되는 정보와 절차를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups to protect personal data.</span></span>

<span data-ttu-id="4caa8-105">개인 데이터의 개인 정보를 보호하기 위한 다계층 보안 전략의 중요한 요소는 SQL 삽입 또는 교차 사이트 스크립팅과 같은 일반적인 취약성 악용에 대한 방어입니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-105">An important element in a multi-layered security strategy to protect the privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="4caa8-106">Azure 가상 네트워크에서 원하지 않는 네트워크 트래픽을 차단하면 중요한 데이터가 손상되지 않도록 보호할 수 있으며, Microsoft Azure는 공격자로부터 데이터를 보호할 수 있는 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools to help protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="4caa8-107">시나리오</span><span class="sxs-lookup"><span data-stu-id="4caa8-107">Scenario</span></span>

<span data-ttu-id="4caa8-108">미국에 본사를 둔 대형 크루즈 회사는 영국 제도뿐만 아니라 지중해, 아드리아해 및 발트해의 여정을 제공하기 위해 운영을 확대하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="4caa8-109">이러한 노력을 촉진하기 위해 이탈리아, 독일, 덴마크 및 영국에 기반을 둔 몇 개의 소형 크루즈 라인을 인수했습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="4caa8-110">회사에서 Microsoft Azure를 사용하여 클라우드에 회사 데이터를 저장하고 이 데이터를 처리하고 액세스하는 가상 컴퓨터에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-110">The company uses Microsoft Azure to store corporate data in the cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="4caa8-111">이 데이터에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="4caa8-112">또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="4caa8-113">또한 크루즈 라인에서 현재 및 과거 고객과의 관계를 추적하기 위해 개인 정보가 포함된 보상 및 충성도 프로그램 구성원에 대한 대규모 데이터베이스를 유지하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-113">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="4caa8-114">회사 직원은 회사의 원격 사무실에서 네트워크에 액세스하고, 전 세계에 위치한 여행사는 일부 회사 리소스에 액세스하고 Azure VM에서 호스팅되는 웹 기반 응용 프로그램을 사용하여 상호 작용합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-114">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources and use web-based applications hosted in Azure VMs to interact with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="4caa8-115">문제 설명</span><span class="sxs-lookup"><span data-stu-id="4caa8-115">Problem statement</span></span>

<span data-ttu-id="4caa8-116">회사의 클라우드 기반 응용 프로그램에서 저장하거나 사용하는 개인 데이터를 노출시킬 수 있는 악의적인 코드를 실행하기 위해 소프트웨어 취약성을 악용하는 공격자로부터 고객 및 직원의 개인 데이터를 회사에서 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-116">The company must protect the privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities to run malicious code that could expose personal data stored or used by the company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="4caa8-117">회사 목표</span><span class="sxs-lookup"><span data-stu-id="4caa8-117">Company goal</span></span>

<span data-ttu-id="4caa8-118">권한 없는 사람이 Azure Virtual Network 및 일반적인 취약성을 악용하여 Azure Virtual Network에 있는 응용 프로그램과 데이터에 액세스할 수 없도록 하는 것이 회사의 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-118">The company’s goal to ensure that unauthorized persons cannot access corporate Azure Virtual Networks and the applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="4caa8-119">솔루션</span><span class="sxs-lookup"><span data-stu-id="4caa8-119">Solutions</span></span>

<span data-ttu-id="4caa8-120">Microsoft Azure는 원하지 않는 트래픽이 Azure Virtual Network에 입력되지 않도록 방지하는 보안 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-120">Microsoft Azure provides security mechanisms to help prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="4caa8-121">인바운드 및 아웃바운드 트래픽 제어는 일반적으로 방화벽에 의해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="4caa8-122">Azure에서는 간단한 분산 방화벽 역할을 하는 웹 응용 프로그램 방화벽 및 NSG(네트워크 보안 그룹)과 함께 Application Gateway를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-122">In Azure, you can use the Application Gateway with the Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="4caa8-123">이러한 도구를 사용하면 원하지 않는 네트워크 트래픽을 검색하고 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-123">These tools enable you to detect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="4caa8-124">Application Gateway/웹 응용 프로그램 방화벽</span><span class="sxs-lookup"><span data-stu-id="4caa8-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="4caa8-125">[Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)의 [WAF(웹 응용 프로그램 방화벽)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) 구성 요소는 알려진 일반 취약성을 악용하는 악의적 공격의 대상이 되고 있는 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-125">The [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of the [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="4caa8-126">중앙 집중식 WAF는 웹 공격으로부터 보호하고, 응용 프로그램을 변경하지 않고도 보안 관리를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="4caa8-127">Azure WAF는 SQL 삽입, 교차 사이트 스크립팅, HTTP 프로토콜 위반 및 변칙, 봇, 크롤러, 스캐너, 일반적인 응용 프로그램 구성 오류, HTTP 서비스 거부 및 기타 일반적 공격(예: 명령 삽입, HTTP 요청 밀반입, HTTP 응답 분할 및 원격 파일 포함 공격)을 포함하여 다양한 공격 범주를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="4caa8-128">WAF를 사용하여 응용 프로그램 게이트웨이를 만들거나 기존 응용 프로그램 게이트웨이에 WAF를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-128">You can create an application gateway with WAF, or add WAF to an existing application gateway.</span></span> <span data-ttu-id="4caa8-129">두 경우 모두 Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="4caa8-130">WAF를 사용하여 응용 프로그램 게이트웨이를 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="4caa8-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="4caa8-131">WAF를 사용하도록 설정된 새 응용 프로그램 게이트웨이를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-131">To create a new application gateway with WAF enabled, do the following:</span></span>

1. <span data-ttu-id="4caa8-132">Azure Portal에 로그인하고 포털의 **즐겨찾기** 창에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-132">Log in to the Azure portal and in the **Favorites** pane of the portal, click **New**</span></span>

2. <span data-ttu-id="4caa8-133">**새로 만들기** 블레이드에서 **네트워킹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-133">In the **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="4caa8-134">**Application Gateway**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="4caa8-135">Azure Portal로 이동하여 **새로 만들기 \> 네트워킹\> Application Gateway**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-135">Navigate to the Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![응용 프로그램 게이트웨이 만들기](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="4caa8-137">표시되는 **기본 사항** 블레이드에서 이름, 계층(표준 또는 WAF), SKU 크기(소형, 중형 또는 대형), 인스턴스 수(고가용성의 경우 2), 구독, 리소스 그룹 및 위치 필드에 대한 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-137">In the **Basics** blade that appears, enter the values for the following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="4caa8-138">**가상 네트워크** 아래에 표시되는 **설정** 블레이드에서 **가상 네트워크 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-138">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="4caa8-139">이 단계에서는 [가상 네트워크 선택] 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-139">This step opens enter the Choose virtual network blade.</span></span>

7. <span data-ttu-id="4caa8-140">**새로 만들기**를 클릭하여 **가상 네트워크 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-140">Click **Create new** to open the **Create virtual network** blade.</span></span>

8. <span data-ttu-id="4caa8-141">이름, 주소 공간, 서브넷 이름, 서브넷 주소 범위 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-141">Enter the following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="4caa8-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-142">Click **OK**.</span></span>

9. <span data-ttu-id="4caa8-143">**설정** 블레이드의 **프런트 엔드 IP 구성** 아래에서 IP 주소 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-143">On the **Settings** blade under **Frontend IP configuration**, choose the IP address type.</span></span>

10. <span data-ttu-id="4caa8-144">**공용 IP 주소 선택**, **새로 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="4caa8-145">기본값을 그대로 적용하고 **확인**을 클릭합니다</span><span class="sxs-lookup"><span data-stu-id="4caa8-145">Accept the default value, and click **OK.**</span></span>

12. <span data-ttu-id="4caa8-146">**설정** 블레이드의 **수신기 구성** 아래에 있는 **프로토콜**에서 HTTP 또는 HTTPS를 사용하도록 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-146">On the **Settings** blade under **Listener configuration**, select to use HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="4caa8-147">HTTPS를 사용하려면 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-147">To use HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="4caa8-148">WAF 특정 설정, 즉 **방화벽 상태**(**사용**) 및 **방화벽 모드**(**방지**)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-148">Configure the WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="4caa8-149">모드로 **검색**을 선택하면 트래픽만 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-149">If you choose **Detection** as the mode, traffic is only logged.</span></span>

14. <span data-ttu-id="4caa8-150">**요약** 페이지를 검토하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-150">Review the **Summary** page and click **OK**.</span></span> <span data-ttu-id="4caa8-151">이제 응용 프로그램 게이트웨이가 만들어지고 대기 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-151">Now the application gateway is queued up and created.</span></span>

<span data-ttu-id="4caa8-152">응용 프로그램 게이트웨이를 만들었으면 포털에서 해당 응용 프로그램 게이트웨이로 이동하여 해당 구성을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-152">After the application gateway has been created, you can navigate to it in the portal and continue configuration of the application gateway.</span></span>

![만든 응용 프로그램 게이트웨이](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-to-an-existing-application"></a><span data-ttu-id="4caa8-154">기존 응용 프로그램에 WAF를 추가하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="4caa8-154">How do I add WAF to an existing application?</span></span>

<span data-ttu-id="4caa8-155">방지 모드에서 WAF를 지원하도록 기존 응용 프로그램 게이트웨이를 업데이트하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-155">To update an existing application gateway to support WAF in prevention mode, do the following:</span></span>

1. <span data-ttu-id="4caa8-156">Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-156">In the Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="4caa8-157">**모든 리소스** 블레이드에서 기존 Application Gateway를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-157">Click the existing Application Gateway in the **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="4caa8-158">참고: 선택한 구독에 이미 여러 리소스가 있는 경우 [이름으로 필터링...]에서 이름 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-158">Note: If the subscription you selected already has several resources in it, you can enter the name in the Filter by name…</span></span> <span data-ttu-id="4caa8-159">DNS 영역에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-159">box to easily access the DNS zone.</span></span>
3. <span data-ttu-id="4caa8-160">**웹 응용 프로그램 방화벽**을 클릭하고, 응용 프로그램 게이트웨이 설정, 즉 **WAF 계층으로 업그레이드**(선택), **방화벽 상태**(사용), **방화벽 모드**(방지)를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-160">Click **Web application firewall** and update the application gateway settings: **Upgrade to WAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="4caa8-161">또한 규칙 집합을 구성하고 사용하지 않는 규칙을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-161">You also need to configure the rule set, and configure disabled rules.</span></span>

<span data-ttu-id="4caa8-162">WAF를 사용하여 새 응용 프로그램 게이트웨이를 만드는 방법과 기존 응용 프로그램 게이트웨이에 WAF를 추가하는 방법에 대한 자세한 내용은 [포털을 사용하여 웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4caa8-162">For more detailed information on how to create a new application gateway with WAF and how to add WAF to an existing application gateway, see [Create an application gateway with web application firewall by using the portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="4caa8-163">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="4caa8-163">Network Security Groups</span></span>

<span data-ttu-id="4caa8-164">[NSG(네트워크 보안 그룹)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)에는 [Azure VNet(Virtual Network)](https://docs.microsoft.com/azure/virtual-network/)에 연결된 리소스에 대한 네트워크 트래픽을 허용하거나 거부하는 보안 규칙 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic to resources connected to [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="4caa8-165">NSG는 서브넷 또는 개별 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-165">NSGs can be associated to subnets or individual VMs.</span></span> <span data-ttu-id="4caa8-166">NSG를 서브넷에 연결하면 규칙이 서브넷에 연결된 모든 리소스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-166">When an NSG is associated to a subnet, the rules apply to all resources connected to the subnet.</span></span> <span data-ttu-id="4caa8-167">또한 NSG를 VM 또는 NIC에 연결하여 트래픽을 더욱 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-167">Traffic can further be restricted by also associating an NSG to a VM or NIC.</span></span>

<span data-ttu-id="4caa8-168">NSG에는 네 가지 속성, 즉 이름, 지역, 리소스 그룹 및 규칙이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="4caa8-169">NSG는 하나의 리소스 그룹에 속하지만, NSG와 동일한 Azure 지역의 일부인 리소스는 모든 리소스 그룹의 리소스에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-169">Although an NSG exists in a resource group, it can be associated to resources in any resource group, as long as the resource is part of the same Azure region as the NSG.</span></span>

<span data-ttu-id="4caa8-170">NSG 규칙에는 9가지 속성, 즉 이름, 프로토콜(TCP, UDP 또는 \*(UDP 및 TCP 외에도 ICMP 포함)), 원본 포트 범위, 대상 포트 범위, 원본 주소 접두사, 대상 주소 접두사, 방향(인바운드 또는 아웃바운드), 우선 순위(100-4096) 및 액세스 형식(허용 또는 거부)이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="4caa8-171">모든 NSG에는 만든 규칙으로 삭제되거나 재정의될 수 있는 기본 규칙 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-171">All NSGs contain a set of default rules that can be deleted, or overridden by the rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="4caa8-172">NSG를 구현하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="4caa8-172">How do I implement NSGs?</span></span>

<span data-ttu-id="4caa8-173">NSG를 구현하려면 계획이 필요하며 고려해야 할 몇 가지 설계 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-173">Implementing NSGs requires planning, and there are several design considerations you need to take into account.</span></span> <span data-ttu-id="4caa8-174">여기에는 구독당 NSG 수 및 NSG당 규칙 수에 대한 제한, VNet 및 서브넷 디자인, 특별 규칙, ICMP 트래픽, 서브넷을 통한 계층 격리, 부하 분산 장치 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-174">These include limits on the number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="4caa8-175">NSG 계획 및 구현에 대한 자세한 지침과 샘플 배포 시나리오는 [네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4caa8-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="4caa8-176">NSG에서 규칙을 만들려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="4caa8-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="4caa8-177">기존 NSG에서 인바운드 규칙을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-177">To create inbound rules in an existing NSG, do the following:</span></span>

1. <span data-ttu-id="4caa8-178">**찾아보기**를 클릭한 다음 **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="4caa8-179">NSG 목록에서 **NSG-FrontEnd**, **인바운드 보안 규칙**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-179">In the list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="4caa8-180">인바운드 보안 규칙 목록에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-180">In the list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="4caa8-181">이름, 우선 순위, 원본, 프로토콜, 원본 범위, 대상, 대상 포트 범위 및 작업 필드에 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-181">Enter the values in the following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="4caa8-182">몇 초 후에 새 규칙이 NSG에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4caa8-182">The new rule will appear in the NSG after a few seconds.</span></span>

![네트워크 보안 규칙](media/protect-netsec/inbound-security.png)

<span data-ttu-id="4caa8-184">서브넷에 NSG를 만들고, 규칙을 만들고, NSG를 프런트 엔드/백 엔드 서브넷과 연결하는 방법에 대한 자세한 지침은 [Azure Portal을 사용하여 네트워크 보안 그룹 만들기](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4caa8-184">For more instructions on how to create NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using the Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4caa8-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4caa8-185">Next steps</span></span>

[<span data-ttu-id="4caa8-186">Azure 네트워크 보안(영문)</span><span class="sxs-lookup"><span data-stu-id="4caa8-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="4caa8-187">Azure 네트워크 보안 모범 사례</span><span class="sxs-lookup"><span data-stu-id="4caa8-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="4caa8-188">네트워크 보안 그룹에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="4caa8-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="4caa8-189">WAF(웹 응용 프로그램 방화벽)</span><span class="sxs-lookup"><span data-stu-id="4caa8-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
