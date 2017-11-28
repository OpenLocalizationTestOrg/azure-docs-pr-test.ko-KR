---
title: "웹 응용 프로그램 방화벽이 있는 Azure Application Gateway 만들기 또는 업데이트 | Microsoft Docs"
description: "포털을 사용하여 웹 응용 프로그램 방화벽이 있는 Application Gateway를 만드는 방법에 대해 알아보기"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 650f26d19615d27a94f3947aad7b7904b6c1fabc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a><span data-ttu-id="7cada-103">포털을 사용하여 웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="7cada-103">Create an application gateway with web application firewall by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7cada-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7cada-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="7cada-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cada-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="7cada-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7cada-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="7cada-107">웹 응용 프로그램 방화벽을 사용하도록 설정된 응용 프로그램 게이트웨이를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-107">Learn how to create a web application firewall enabled application gateway.</span></span>

<span data-ttu-id="7cada-108">Azure Application Gateway의 웹 응용 프로그램 방화벽(WAF)은 SQL 삽입 공격, 사이트 간 스크립팅 공격, 세션 하이재킹 등의 일반적인 웹 기반 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span> <span data-ttu-id="7cada-109">웹 응용 프로그램은 다양한 OWASP 상위 10 일반적인 웹 취약점으로부터 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-109">Web application protects against many of the OWASP top 10 common web vulnerabilities.</span></span>

## <a name="scenarios"></a><span data-ttu-id="7cada-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="7cada-110">Scenarios</span></span>

<span data-ttu-id="7cada-111">이 문서에는 두 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-111">In this article there are two scenarios:</span></span>

<span data-ttu-id="7cada-112">첫 번째 시나리오에서는 [웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법](#create-an-application-gateway-with-web-application-firewall)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-112">In the first scenario, you learn to [create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span></span>

<span data-ttu-id="7cada-113">두 번째 시나리오에서는 [기존 Application Gateway에 웹 응용 프로그램 방화벽을 추가하는 방법](#add-web-application-firewall-to-an-existing-application-gateway)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-113">In the second scenario, you learn to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span></span>

![예제 시나리오][scenario]

> [!NOTE]
> <span data-ttu-id="7cada-115">초기 배포 중이 아닌 경우 응용 프로그램 게이트웨이를 구성하면 사용자 지정 상태 프로브, 백 엔드 풀 주소, 추가 규칙 등 응용 프로그램 게이트웨이에 대한 추가 구성이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-115">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7cada-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7cada-116">Before you begin</span></span>

<span data-ttu-id="7cada-117">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-117">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="7cada-118">가상 네트워크를 만들 때 여러 서브넷을 둘 수 있는 충분한 주소 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-118">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="7cada-119">Application Gateway를 서브넷에 배포한 경우 추가 Application Gateway를 서브넷에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-119">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

##<span data-ttu-id="7cada-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> 기존 Application Gateway에 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="7cada-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="7cada-121">이 예제에서는 방지 모드에서 웹 응용 프로그램 방화벽을 지원하도록 기존 Application Gateway를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-121">This example updates an existing application gateway to support web application firewall in prevention mode.</span></span>

1. <span data-ttu-id="7cada-122">Azure Portal의 **즐겨찾기** 창에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-122">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7cada-123">**모든 리소스** 블레이드에서 기존 Application Gateway를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-123">Click the existing Application Gateway in the **All resources** blade.</span></span> <span data-ttu-id="7cada-124">선택한 구독에 이미 여러 개의 리소스가 있는 경우 **이름을 기준으로 필터링...**에 이름 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-124">If the subscription you selected already has several resources in it, you can enter the name in the **Filter by name…**</span></span> <span data-ttu-id="7cada-125">DNS 영역에 간편하게 액세스할 수 있는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-125">box to easily access the DNS zone.</span></span>

   ![Application Gateway 만들기][1]

1. <span data-ttu-id="7cada-127">**웹 응용 프로그램 방화벽**을 클릭하고 응용 프로그램 게이트웨이 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-127">Click **Web application firewall** and update the application gateway settings.</span></span> <span data-ttu-id="7cada-128">완료되면 **저장**</span><span class="sxs-lookup"><span data-stu-id="7cada-128">When complete click **Save**</span></span>

    <span data-ttu-id="7cada-129">웹 응용 프로그램 방화벽을 지원하도록 기존 Application Gateway를 업데이트하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-129">The settings to update an existing application gateway to support web application firewall are:</span></span>

   | <span data-ttu-id="7cada-130">**설정**</span><span class="sxs-lookup"><span data-stu-id="7cada-130">**Setting**</span></span> | <span data-ttu-id="7cada-131">**값**</span><span class="sxs-lookup"><span data-stu-id="7cada-131">**Value**</span></span> | <span data-ttu-id="7cada-132">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7cada-132">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="7cada-133">**WAF 계층으로 업그레이드**</span><span class="sxs-lookup"><span data-stu-id="7cada-133">**Upgrade to WAF Tier**</span></span>| <span data-ttu-id="7cada-134">선택</span><span class="sxs-lookup"><span data-stu-id="7cada-134">Checked</span></span> | <span data-ttu-id="7cada-135">Application Gateway의 계층을 WAF 계층으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-135">This sets the tier of the application gateway to the WAF tier.</span></span>|
   |<span data-ttu-id="7cada-136">**방화벽 상태**</span><span class="sxs-lookup"><span data-stu-id="7cada-136">**Firewall status**</span></span>| <span data-ttu-id="7cada-137">사용</span><span class="sxs-lookup"><span data-stu-id="7cada-137">Enabled</span></span> | <span data-ttu-id="7cada-138">이 설정은 WAF에서 방화벽을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-138">This setting enables the firewall on the WAF.</span></span>|
   |<span data-ttu-id="7cada-139">**방화벽 모드**</span><span class="sxs-lookup"><span data-stu-id="7cada-139">**Firewall mode**</span></span> | <span data-ttu-id="7cada-140">방지</span><span class="sxs-lookup"><span data-stu-id="7cada-140">Prevention</span></span> | <span data-ttu-id="7cada-141">웹 응용 프로그램 방화벽이 악의적인 트래픽을 처리하는 방식에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-141">This setting is how web application firewall deals with malicious traffic.</span></span> <span data-ttu-id="7cada-142">**검색** 모드는 이벤트를 기록하기만 하는 반면 **방지** 모드는 이벤트를 기록하고 악의적인 트래픽을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-142">**Detection** mode only logs the events, where **Prevention** mode logs the events and stops the malicious traffic.</span></span>|
   |<span data-ttu-id="7cada-143">**규칙 집합**</span><span class="sxs-lookup"><span data-stu-id="7cada-143">**Rule set**</span></span>|<span data-ttu-id="7cada-144">3.0</span><span class="sxs-lookup"><span data-stu-id="7cada-144">3.0</span></span>|<span data-ttu-id="7cada-145">이 설정은 백 엔드 풀 멤버를 보호하는 데 사용되는 [코어 규칙 집합](application-gateway-web-application-firewall-overview.md#core-rule-sets)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-145">This setting determines the [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used to protect the backend pool members.</span></span>|
   |<span data-ttu-id="7cada-146">**사용하지 않는 규칙 구성**</span><span class="sxs-lookup"><span data-stu-id="7cada-146">**Configure disabled rules**</span></span>|<span data-ttu-id="7cada-147">다름</span><span class="sxs-lookup"><span data-stu-id="7cada-147">varies</span></span>|<span data-ttu-id="7cada-148">가능한 가양성을 방지하기 위해 이 설정은 특정 [규칙 및 규칙 그룹](application-gateway-crs-rulegroups-rules.md)을 사용하지 않도록 설정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-148">To prevent possible false positives, this setting allows you to disable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span></span>|

    >[!NOTE]
    > <span data-ttu-id="7cada-149">기존 응용 프로그램 게이트웨이를 WAF SKU로 업그레이드할 때 SKU 크기는 **중형**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-149">When upgrading an existing application gateway to the WAF SKU, the SKU size changes to **medium**.</span></span> <span data-ttu-id="7cada-150">구성이 완료된 후 이 크기를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-150">This can be reconfigured after configuration is complete.</span></span>

    ![기본 설정이 표시된 블레이드][2-1]

    > [!NOTE]
    > <span data-ttu-id="7cada-152">웹 응용 프로그램 방화벽 로그를 보려면 진단을 활성화하고 ApplicationGatewayFirewallLog를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-152">To view web application firewall logs, diagnostics must be enabled and ApplicationGatewayFirewallLog selected.</span></span> <span data-ttu-id="7cada-153">테스트 목적으로 인스턴스 수 1을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-153">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="7cada-154">그러나 두 개 미만의 인스턴스 수는 SLA에서 다루지 않으므로 권장되지 않는다는 점을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-154">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="7cada-155">웹 응용 프로그램 방화벽을 사용하는 경우 소형 게이트웨이를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-155">Small gateways are not available when using web application firewall.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="7cada-156">웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7cada-156">Create an application gateway with web application firewall</span></span>

<span data-ttu-id="7cada-157">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-157">This scenario will:</span></span>

* <span data-ttu-id="7cada-158">두 인스턴스를 사용하여 중형 웹 응용 프로그램 방화벽 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-158">Create a medium web application firewall application gateway with two instances.</span></span>
* <span data-ttu-id="7cada-159">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 AdatumAppGatewayVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-159">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="7cada-160">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-160">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="7cada-161">SSL 오프로드용 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-161">Configure a certificate for SSL offload.</span></span>

1. <span data-ttu-id="7cada-162">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-162">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7cada-163">아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-163">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>
1. <span data-ttu-id="7cada-164">포털의 즐겨찾기 창에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-164">In the Favorites pane of the portal, click **New**</span></span>
1. <span data-ttu-id="7cada-165">**새로 만들기** 블레이드에서 **네트워킹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-165">In the **New** blade, click **Networking**.</span></span> <span data-ttu-id="7cada-166">다음 그림과 같이 **네트워킹** 블레이드에서 **Application Gateway**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-166">In the **Networking** blade, click **Application Gateway**, as shown in the following image:</span></span>
1. <span data-ttu-id="7cada-167">Azure Portal로 이동하여 **새로 만들기** > **네트워킹** > **Application Gateway**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-167">Navigate to the Azure portal, click **New** > **Networking** > **Application Gateway**</span></span>

    ![Application Gateway 만들기][1]

1. <span data-ttu-id="7cada-169">표시되는 **기본 사항** 블레이드에서 다음 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-169">In the **Basics** blade that appears, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="7cada-170">**설정**</span><span class="sxs-lookup"><span data-stu-id="7cada-170">**Setting**</span></span> | <span data-ttu-id="7cada-171">**값**</span><span class="sxs-lookup"><span data-stu-id="7cada-171">**Value**</span></span> | <span data-ttu-id="7cada-172">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7cada-172">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="7cada-173">**Name**</span><span class="sxs-lookup"><span data-stu-id="7cada-173">**Name**</span></span>|<span data-ttu-id="7cada-174">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="7cada-174">AdatumAppGateway</span></span>|<span data-ttu-id="7cada-175">Application Gateway의 이름</span><span class="sxs-lookup"><span data-stu-id="7cada-175">The name of the application gateway</span></span>|
   |<span data-ttu-id="7cada-176">**계층**</span><span class="sxs-lookup"><span data-stu-id="7cada-176">**Tier**</span></span>|<span data-ttu-id="7cada-177">WAF</span><span class="sxs-lookup"><span data-stu-id="7cada-177">WAF</span></span>|<span data-ttu-id="7cada-178">사용 가능한 값은 표준 또는 WAF입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-178">Available values are Standard and WAF.</span></span> <span data-ttu-id="7cada-179">[웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md)을 방문하여 WAF에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7cada-179">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) to learn more about WAF.</span></span>|
   |<span data-ttu-id="7cada-180">**SKU 크기**</span><span class="sxs-lookup"><span data-stu-id="7cada-180">**SKU Size**</span></span>|<span data-ttu-id="7cada-181">중간</span><span class="sxs-lookup"><span data-stu-id="7cada-181">Medium</span></span>|<span data-ttu-id="7cada-182">표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-182">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="7cada-183">WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-183">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="7cada-184">**인스턴스 수**</span><span class="sxs-lookup"><span data-stu-id="7cada-184">**Instance count**</span></span>|<span data-ttu-id="7cada-185">2</span><span class="sxs-lookup"><span data-stu-id="7cada-185">2</span></span>|<span data-ttu-id="7cada-186">고가용성을 위한 Application Gateway의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-186">Number of instances of the application gateway for high availability.</span></span> <span data-ttu-id="7cada-187">인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-187">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="7cada-188">**구독**</span><span class="sxs-lookup"><span data-stu-id="7cada-188">**Subscription**</span></span>|<span data-ttu-id="7cada-189">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="7cada-189">[Your subscription]</span></span>|<span data-ttu-id="7cada-190">응용 프로그램 게이트웨이를 만들 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-190">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="7cada-191">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="7cada-191">**Resource group**</span></span>|<span data-ttu-id="7cada-192">**새로 만들기:** AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="7cada-192">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="7cada-193">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-193">Create a resource group.</span></span> <span data-ttu-id="7cada-194">리소스 그룹 이름은 선택한 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-194">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="7cada-195">리소스 그룹에 대해 자세히 알아보려면 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7cada-195">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7cada-196">**위치**:</span><span class="sxs-lookup"><span data-stu-id="7cada-196">**Location**</span></span>|<span data-ttu-id="7cada-197">미국 서부</span><span class="sxs-lookup"><span data-stu-id="7cada-197">West US</span></span>||

   ![기본 설정이 표시된 블레이드][2-2]

1. <span data-ttu-id="7cada-199">**가상 네트워크** 아래에 표시되는 **설정** 블레이드에서 **가상 네트워크 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-199">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="7cada-200">이 단계는 **가상 네트워크 선택** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-200">This step opens enter the **Choose virtual network** blade.</span></span>  <span data-ttu-id="7cada-201">**새로 만들기**를 클릭하여 **가상 네트워크 만들기** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-201">Click **Create new** to open the **Create virtual network** blade.</span></span>

   ![가상 네트워크 선택][2]

1. <span data-ttu-id="7cada-203">**가상 네트워크 만들기** 블레이드에서 다음 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-203">On the **Create virtual network blade** enter the following values, then click **OK**.</span></span> <span data-ttu-id="7cada-204">이 단계는 **가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-204">This step closes the **Create virtual network** and **Choose virtual network** blades.</span></span> <span data-ttu-id="7cada-205">**설정** 블레이드의 **서브넷** 필드를 선택한 서브넷으로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-205">This populates the **Subnet** field on the **Settings** blade with the subnet chosen.</span></span>

   |<span data-ttu-id="7cada-206">**설정**</span><span class="sxs-lookup"><span data-stu-id="7cada-206">**Setting**</span></span> | <span data-ttu-id="7cada-207">**값**</span><span class="sxs-lookup"><span data-stu-id="7cada-207">**Value**</span></span> | <span data-ttu-id="7cada-208">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7cada-208">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7cada-209">**Name**</span><span class="sxs-lookup"><span data-stu-id="7cada-209">**Name**</span></span>|<span data-ttu-id="7cada-210">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="7cada-210">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="7cada-211">Application Gateway의 이름</span><span class="sxs-lookup"><span data-stu-id="7cada-211">Name of the application gateway</span></span>|
   |<span data-ttu-id="7cada-212">**주소 공간**</span><span class="sxs-lookup"><span data-stu-id="7cada-212">**Address Space**</span></span>|<span data-ttu-id="7cada-213">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7cada-213">10.0.0.0/16</span></span>| <span data-ttu-id="7cada-214">이 값은 가상 네트워크에 대한 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-214">This value is the address space for the virtual network</span></span>|
   |<span data-ttu-id="7cada-215">**서브넷 이름**</span><span class="sxs-lookup"><span data-stu-id="7cada-215">**Subnet name**</span></span>|<span data-ttu-id="7cada-216">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="7cada-216">AppGatewaySubnet</span></span>|<span data-ttu-id="7cada-217">Application Gateway의 서브넷 이름</span><span class="sxs-lookup"><span data-stu-id="7cada-217">Name of the subnet for the application gateway</span></span>|
   |<span data-ttu-id="7cada-218">**서브넷 주소 범위**</span><span class="sxs-lookup"><span data-stu-id="7cada-218">**Subnet address range**</span></span>|<span data-ttu-id="7cada-219">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="7cada-219">10.0.0.0/28</span></span> | <span data-ttu-id="7cada-220">이 서브넷을 사용하면 백 엔드 풀 멤버가 가상 네트워크에서 추가 서브넷을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-220">This subnet allows more additional subnets in the virtual network for backend pool members</span></span>|

1. <span data-ttu-id="7cada-221">**설정** 블레이드의 **프런트 엔드 IP 구성** 아래에서 **IP 주소 유형**으로 **공용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-221">On the **Settings** blade under **Frontend IP configuration**, choose **Public** as the **IP address type**</span></span>

1. <span data-ttu-id="7cada-222">**설정** 블레이드의 **공용 IP 주소**에서 **공용 IP 주소 선택**을 클릭합니다. 이 단계는 **공용 IP 주소 선택** 블레이드를 엽니다. 여기서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-222">On the **Settings** blade under **Public IP address**, click **Choose a public IP address**, this step opens the **Choose public IP address** blade, click **Create new**.</span></span>

   ![공용 IP 선택][3]

1. <span data-ttu-id="7cada-224">**공용 IP 주소 만들기** 블레이드에서 기본값을 그대로 적용하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-224">On the **Create public IP address** blade, accept the default value, and click **OK**.</span></span> <span data-ttu-id="7cada-225">이 단계는 **공용 IP 주소 선택** 블레이드, **공용 IP 주소 만들기** 블레이드를 닫고 **공용 IP 주소**를 선택한 공용 IP 주소로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-225">This step closes the **Choose public IP address** blade, the **Create public IP address** blade, and populate **Public IP address** with the public IP address chosen.</span></span>

1. <span data-ttu-id="7cada-226">**설정** 블레이드의 **수신기 구성** 아래에서 **프로토콜** 아래에 있는 **HTTP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-226">On the **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="7cada-227">**https**를 사용하려면 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-227">To use **https**, a certificate is required.</span></span> <span data-ttu-id="7cada-228">인증서의 개인 키가 필요하므로 인증서의 .pfx 내보내기 및 파일의 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-228">The private key of the certificate is needed so a .pfx export of the certificate needs to be provided and the password for the file.</span></span>

1. <span data-ttu-id="7cada-229">**WAF** 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-229">Configure the **WAF** specific settings.</span></span>

   |<span data-ttu-id="7cada-230">**설정**</span><span class="sxs-lookup"><span data-stu-id="7cada-230">**Setting**</span></span> | <span data-ttu-id="7cada-231">**값**</span><span class="sxs-lookup"><span data-stu-id="7cada-231">**Value**</span></span> | <span data-ttu-id="7cada-232">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7cada-232">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7cada-233">**방화벽 상태**</span><span class="sxs-lookup"><span data-stu-id="7cada-233">**Firewall status**</span></span>| <span data-ttu-id="7cada-234">사용</span><span class="sxs-lookup"><span data-stu-id="7cada-234">Enabled</span></span>| <span data-ttu-id="7cada-235">이 설정은 WAF를 켜고 끕니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-235">This setting turns WAF on or off.</span></span>|
   |<span data-ttu-id="7cada-236">**방화벽 모드**</span><span class="sxs-lookup"><span data-stu-id="7cada-236">**Firewall mode**</span></span> | <span data-ttu-id="7cada-237">방지</span><span class="sxs-lookup"><span data-stu-id="7cada-237">Prevention</span></span>| <span data-ttu-id="7cada-238">이 설정은 WAF가 악의적인 트래픽에 대해 수행하는 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-238">This setting determines the actions WAF takes on malicious traffic.</span></span> <span data-ttu-id="7cada-239">**검색** 을 선택하면 트래픽이 기록되기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-239">If **Detection** is chosen, traffic is only logged.</span></span>  <span data-ttu-id="7cada-240">**방지**를 선택하면 트래픽이 기록되고 403 권한 없음 응답에 따라 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-240">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span></span>|


1. <span data-ttu-id="7cada-241">요약 페이지를 검토하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-241">Review the Summary page and click **OK**.</span></span>  <span data-ttu-id="7cada-242">이제 응용 프로그램 게이트웨이가 만들어지고 대기 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-242">Now the application gateway is queued up and created.</span></span>

1. <span data-ttu-id="7cada-243">응용 프로그램 게이트웨이를 만든 후에는 포털에서 해당 응용 프로그램 게이트웨이로 이동하여 응용 프로그램 게이트웨이 구성을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-243">Once the application gateway has been created, navigate to it in the portal to continue configuration of the application gateway.</span></span>

    ![Application Gateway 리소스 보기][10]

<span data-ttu-id="7cada-245">이러한 단계에서는 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대한 기본 설정으로 기본 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-245">These steps create a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="7cada-246">프로비전에 성공하면 배포에 맞게 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-246">You can modify these settings to suit your deployment once the provisioning is successful</span></span>

> [!NOTE]
> <span data-ttu-id="7cada-247">기본 웹 응용 프로그램 방화벽 구성을 사용하여 만든 응용 프로그램 게이트웨이는 보호를 위해 CRS 3.0으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-247">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cada-248">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7cada-248">Next steps</span></span>

<span data-ttu-id="7cada-249">다음으로 Azure DNS 또는 다른 DNS 공급자를 사용하여 [공용 IP 주소](../dns/dns-custom-domain.md#public-ip-address)에 대한 사용자 지정 도메인 별칭을 구성하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7cada-249">Next, you can learn how to configure a custom domain alias for the [public IP address](../dns/dns-custom-domain.md#public-ip-address) using Azure DNS or another DNS provider.</span></span>

<span data-ttu-id="7cada-250">[Application Gateway 진단](application-gateway-diagnostics.md)을 방문하여 진단 로깅을 구성하는 방법 및 웹 응용 프로그램 방화벽을 통해 검색 또는 방지되는 이벤트를 기록하는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="7cada-250">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="7cada-251">[사용자 지정 상태 프로브 만들기](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7cada-251">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="7cada-252">[SSL 오프로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7cada-252">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
