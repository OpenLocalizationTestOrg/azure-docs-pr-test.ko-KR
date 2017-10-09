---
title: "aaaCreate 웹 응용 프로그램 방화벽으로 Azure 응용 프로그램 게이트웨이 업데이트 하거나 | Microsoft Docs"
description: "웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 toocreate 포털 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a><span data-ttu-id="ae9d0-103">Hello 포털을 사용 하 여 웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ae9d0-103">Create an application gateway with web application firewall by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae9d0-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ae9d0-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="ae9d0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae9d0-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="ae9d0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae9d0-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="ae9d0-107">웹 응용 프로그램 방화벽 toocreate 응용 프로그램 게이트웨이 사용 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-107">Learn how toocreate a web application firewall enabled application gateway.</span></span>

<span data-ttu-id="ae9d0-108">hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span> <span data-ttu-id="ae9d0-109">웹 응용 프로그램 다양 한 hello OWASP 상위 10 개의 일반적인 웹 취약점 으로부터 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-109">Web application protects against many of hello OWASP top 10 common web vulnerabilities.</span></span>

## <a name="scenarios"></a><span data-ttu-id="ae9d0-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="ae9d0-110">Scenarios</span></span>

<span data-ttu-id="ae9d0-111">이 문서에는 두 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-111">In this article there are two scenarios:</span></span>

<span data-ttu-id="ae9d0-112">Hello 첫 번째 시나리오에 알아봅니다 너무[웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이 만들기](#create-an-application-gateway-with-web-application-firewall)</span><span class="sxs-lookup"><span data-stu-id="ae9d0-112">In hello first scenario, you learn too[create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span></span>

<span data-ttu-id="ae9d0-113">Hello 두 번째 시나리오에 알아봅니다 너무[추가 웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이](#add-web-application-firewall-to-an-existing-application-gateway)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-113">In hello second scenario, you learn too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span></span>

![예제 시나리오][scenario]

> [!NOTE]
> <span data-ttu-id="ae9d0-115">사용자 지정 상태를 포함 하 여 hello 응용 프로그램 게이트웨이 추가 구성 프로브를 통해 백 엔드 풀 주소 및 추가 규칙 hello 응용 프로그램 게이트웨이 구성한 후와 초기 배포 중이 아니라 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-115">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae9d0-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ae9d0-116">Before you begin</span></span>

<span data-ttu-id="ae9d0-117">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-117">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="ae9d0-118">가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-118">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="ae9d0-119">추가 응용 프로그램 게이트웨이 수 toobe 추가 응용 프로그램 게이트웨이 tooa 서브넷을 배포한 후 toohello 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-119">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

##<span data-ttu-id="ae9d0-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a>웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="ae9d0-121">이 예에서는 기존 응용 프로그램 게이트웨이 toosupport 웹 응용 프로그램 방화벽 방지 모드에서를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-121">This example updates an existing application gateway toosupport web application firewall in prevention mode.</span></span>

1. <span data-ttu-id="ae9d0-122">Hello Azure 포털에서에서 **즐겨찾기** 창에서 클릭 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-122">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="ae9d0-123">클릭 하 여 hello hello에서 기존 응용 프로그램 게이트웨이 **모든 리소스** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-123">Click hello existing Application Gateway in hello **All resources** blade.</span></span> <span data-ttu-id="ae9d0-124">이미 선택한 hello 구독에 여러 자원이 인 경우 hello에 hello 이름을 입력할 수 있습니다 **이름별으로 필터링...**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-124">If hello subscription you selected already has several resources in it, you can enter hello name in hello **Filter by name…**</span></span> <span data-ttu-id="ae9d0-125">상자 tooeasily 액세스 hello DNS 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-125">box tooeasily access hello DNS zone.</span></span>

   ![Application Gateway 만들기][1]

1. <span data-ttu-id="ae9d0-127">클릭 **웹 응용 프로그램 방화벽** hello 응용 프로그램 게이트웨이 설정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-127">Click **Web application firewall** and update hello application gateway settings.</span></span> <span data-ttu-id="ae9d0-128">완료되면 **저장**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-128">When complete click **Save**</span></span>

    <span data-ttu-id="ae9d0-129">hello 설정을 tooupdate 기존 응용 프로그램 게이트웨이 toosupport 웹 응용 프로그램 방화벽은:</span><span class="sxs-lookup"><span data-stu-id="ae9d0-129">hello settings tooupdate an existing application gateway toosupport web application firewall are:</span></span>

   | <span data-ttu-id="ae9d0-130">**설정**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-130">**Setting**</span></span> | <span data-ttu-id="ae9d0-131">**값**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-131">**Value**</span></span> | <span data-ttu-id="ae9d0-132">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-132">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="ae9d0-133">**TooWAF 계층 업그레이드**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-133">**Upgrade tooWAF Tier**</span></span>| <span data-ttu-id="ae9d0-134">선택</span><span class="sxs-lookup"><span data-stu-id="ae9d0-134">Checked</span></span> | <span data-ttu-id="ae9d0-135">Hello 응용 프로그램 게이트웨이 toohello WAF 계층의 hello 계층을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-135">This sets hello tier of hello application gateway toohello WAF tier.</span></span>|
   |<span data-ttu-id="ae9d0-136">**방화벽 상태**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-136">**Firewall status**</span></span>| <span data-ttu-id="ae9d0-137">사용</span><span class="sxs-lookup"><span data-stu-id="ae9d0-137">Enabled</span></span> | <span data-ttu-id="ae9d0-138">이 설정은 WAF hello에서 hello 방화벽을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-138">This setting enables hello firewall on hello WAF.</span></span>|
   |<span data-ttu-id="ae9d0-139">**방화벽 모드**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-139">**Firewall mode**</span></span> | <span data-ttu-id="ae9d0-140">방지</span><span class="sxs-lookup"><span data-stu-id="ae9d0-140">Prevention</span></span> | <span data-ttu-id="ae9d0-141">웹 응용 프로그램 방화벽이 악의적인 트래픽을 처리하는 방식에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-141">This setting is how web application firewall deals with malicious traffic.</span></span> <span data-ttu-id="ae9d0-142">**검색** 모드 hello 이벤트 기록 여기서 **방지** 모드 hello 이벤트를 기록 하 고 중지 hello 악의적인 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-142">**Detection** mode only logs hello events, where **Prevention** mode logs hello events and stops hello malicious traffic.</span></span>|
   |<span data-ttu-id="ae9d0-143">**규칙 집합**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-143">**Rule set**</span></span>|<span data-ttu-id="ae9d0-144">3.0</span><span class="sxs-lookup"><span data-stu-id="ae9d0-144">3.0</span></span>|<span data-ttu-id="ae9d0-145">이 설정은 결정 hello [규칙 집합 핵심](application-gateway-web-application-firewall-overview.md#core-rule-sets) 즉 사용 되는 tooprotect hello 백 엔드 풀 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-145">This setting determines hello [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used tooprotect hello backend pool members.</span></span>|
   |<span data-ttu-id="ae9d0-146">**사용하지 않는 규칙 구성**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-146">**Configure disabled rules**</span></span>|<span data-ttu-id="ae9d0-147">다름</span><span class="sxs-lookup"><span data-stu-id="ae9d0-147">varies</span></span>|<span data-ttu-id="ae9d0-148">tooprevent 가능한 가양성이이 설정을 통해 toodisable 특정 [규칙 및 규칙 그룹](application-gateway-crs-rulegroups-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-148">tooprevent possible false positives, this setting allows you toodisable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span></span>|

    >[!NOTE]
    > <span data-ttu-id="ae9d0-149">기존 응용 프로그램 게이트웨이 toohello WAF SKU로 업그레이드할 때 hello SKU 크기를 변경 너무**보통**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-149">When upgrading an existing application gateway toohello WAF SKU, hello SKU size changes too**medium**.</span></span> <span data-ttu-id="ae9d0-150">구성이 완료된 후 이 크기를 다시 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-150">This can be reconfigured after configuration is complete.</span></span>

    ![기본 설정이 표시된 블레이드][2-1]

    > [!NOTE]
    > <span data-ttu-id="ae9d0-152">tooview 웹 응용 프로그램 방화벽 로그, 진단 설정 해야 하 고 ApplicationGatewayFirewallLog 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-152">tooview web application firewall logs, diagnostics must be enabled and ApplicationGatewayFirewallLog selected.</span></span> <span data-ttu-id="ae9d0-153">테스트 목적으로 인스턴스 수 1을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-153">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="ae9d0-154">고 것이 중요에 모든 인스턴스 수의 두 인스턴스가 tooknow hello SLA에서 다루지 않는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-154">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="ae9d0-155">웹 응용 프로그램 방화벽을 사용하는 경우 소형 게이트웨이를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-155">Small gateways are not available when using web application firewall.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="ae9d0-156">웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ae9d0-156">Create an application gateway with web application firewall</span></span>

<span data-ttu-id="ae9d0-157">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-157">This scenario will:</span></span>

* <span data-ttu-id="ae9d0-158">두 인스턴스를 사용하여 중형 웹 응용 프로그램 방화벽 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-158">Create a medium web application firewall application gateway with two instances.</span></span>
* <span data-ttu-id="ae9d0-159">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 AdatumAppGatewayVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-159">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ae9d0-160">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-160">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="ae9d0-161">SSL 오프로드용 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-161">Configure a certificate for SSL offload.</span></span>

1. <span data-ttu-id="ae9d0-162">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-162">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ae9d0-163">아직 계정이 없는 경우 [1개월 평가판](https://azure.microsoft.com/free)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-163">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>
1. <span data-ttu-id="ae9d0-164">Hello 포털의 hello 즐겨찾기 창에서 클릭 **새로 만들기**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-164">In hello Favorites pane of hello portal, click **New**</span></span>
1. <span data-ttu-id="ae9d0-165">Hello에 **새로** 블레이드에서 클릭 **네트워킹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-165">In hello **New** blade, click **Networking**.</span></span> <span data-ttu-id="ae9d0-166">Hello에 **네트워킹** 블레이드에서 클릭 **응용 프로그램 게이트웨이**hello 다음 이미지에에서 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="ae9d0-166">In hello **Networking** blade, click **Application Gateway**, as shown in hello following image:</span></span>
1. <span data-ttu-id="ae9d0-167">Azure 포털 toohello 탐색, 클릭 **새로** > **네트워킹** > **응용 프로그램 게이트웨이**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-167">Navigate toohello Azure portal, click **New** > **Networking** > **Application Gateway**</span></span>

    ![Application Gateway 만들기][1]

1. <span data-ttu-id="ae9d0-169">Hello에 **기본 사항** 나타나는 블레이드 hello 다음 값을 입력 한 다음 클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="ae9d0-169">In hello **Basics** blade that appears, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="ae9d0-170">**설정**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-170">**Setting**</span></span> | <span data-ttu-id="ae9d0-171">**값**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-171">**Value**</span></span> | <span data-ttu-id="ae9d0-172">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-172">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="ae9d0-173">**Name**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-173">**Name**</span></span>|<span data-ttu-id="ae9d0-174">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="ae9d0-174">AdatumAppGateway</span></span>|<span data-ttu-id="ae9d0-175">hello 응용 프로그램 게이트웨이의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="ae9d0-175">hello name of hello application gateway</span></span>|
   |<span data-ttu-id="ae9d0-176">**계층**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-176">**Tier**</span></span>|<span data-ttu-id="ae9d0-177">WAF</span><span class="sxs-lookup"><span data-stu-id="ae9d0-177">WAF</span></span>|<span data-ttu-id="ae9d0-178">사용 가능한 값은 표준 또는 WAF입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-178">Available values are Standard and WAF.</span></span> <span data-ttu-id="ae9d0-179">방문 [웹 응용 프로그램 방화벽](application-gateway-web-application-firewall-overview.md) toolearn WAF에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-179">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn more about WAF.</span></span>|
   |<span data-ttu-id="ae9d0-180">**SKU 크기**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-180">**SKU Size**</span></span>|<span data-ttu-id="ae9d0-181">중간</span><span class="sxs-lookup"><span data-stu-id="ae9d0-181">Medium</span></span>|<span data-ttu-id="ae9d0-182">표준 계층을 선택할 때 제공되는 옵션으로 소형, 중형 및 대형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-182">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="ae9d0-183">WAF 계층을 선택할 때 옵션은 중간 및 대형 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-183">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="ae9d0-184">**인스턴스 수**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-184">**Instance count**</span></span>|<span data-ttu-id="ae9d0-185">2</span><span class="sxs-lookup"><span data-stu-id="ae9d0-185">2</span></span>|<span data-ttu-id="ae9d0-186">고가용성에 대 한 응용 프로그램 게이트웨이 hello의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-186">Number of instances of hello application gateway for high availability.</span></span> <span data-ttu-id="ae9d0-187">인스턴스 수 1은 테스트 목적으로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-187">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="ae9d0-188">**구독**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-188">**Subscription**</span></span>|<span data-ttu-id="ae9d0-189">[구독 이름]</span><span class="sxs-lookup"><span data-stu-id="ae9d0-189">[Your subscription]</span></span>|<span data-ttu-id="ae9d0-190">구독 toocreate hello 응용 프로그램 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-190">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="ae9d0-191">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-191">**Resource group**</span></span>|<span data-ttu-id="ae9d0-192">**새로 만들기:** AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="ae9d0-192">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="ae9d0-193">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-193">Create a resource group.</span></span> <span data-ttu-id="ae9d0-194">hello 리소스 그룹 이름은 선택한 hello 구독 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-194">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="ae9d0-195">리소스 그룹을 읽기 hello에 대 한 자세한 toolearn [리소스 관리자](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 개요 문서.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-195">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="ae9d0-196">**위치**:</span><span class="sxs-lookup"><span data-stu-id="ae9d0-196">**Location**</span></span>|<span data-ttu-id="ae9d0-197">미국 서부</span><span class="sxs-lookup"><span data-stu-id="ae9d0-197">West US</span></span>||

   ![기본 설정이 표시된 블레이드][2-2]

1. <span data-ttu-id="ae9d0-199">Hello에 **설정** 아래에 나타나는 블레이드 **가상 네트워크**, 클릭 **가상 네트워크를 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-199">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="ae9d0-200">이 단계 열립니다 입력 hello **가상 네트워크 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-200">This step opens enter hello **Choose virtual network** blade.</span></span>  <span data-ttu-id="ae9d0-201">클릭 **새로 만들기** tooopen hello **가상 네트워크 만들기** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-201">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

   ![가상 네트워크 선택][2]

1. <span data-ttu-id="ae9d0-203">Hello에 **만들기 가상 네트워크 블레이드** hello 다음 값을 입력 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-203">On hello **Create virtual network blade** enter hello following values, then click **OK**.</span></span> <span data-ttu-id="ae9d0-204">이 단계는 hello 닫습니다 **가상 네트워크 만들기** 및 **가상 네트워크 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-204">This step closes hello **Create virtual network** and **Choose virtual network** blades.</span></span> <span data-ttu-id="ae9d0-205">이렇게 hello 채워집니다 **서브넷** 필드 hello에 **설정** 블레이드 hello 서브넷을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-205">This populates hello **Subnet** field on hello **Settings** blade with hello subnet chosen.</span></span>

   |<span data-ttu-id="ae9d0-206">**설정**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-206">**Setting**</span></span> | <span data-ttu-id="ae9d0-207">**값**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-207">**Value**</span></span> | <span data-ttu-id="ae9d0-208">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-208">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="ae9d0-209">**Name**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-209">**Name**</span></span>|<span data-ttu-id="ae9d0-210">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="ae9d0-210">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="ae9d0-211">Hello 응용 프로그램 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="ae9d0-211">Name of hello application gateway</span></span>|
   |<span data-ttu-id="ae9d0-212">**주소 공간**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-212">**Address Space**</span></span>|<span data-ttu-id="ae9d0-213">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ae9d0-213">10.0.0.0/16</span></span>| <span data-ttu-id="ae9d0-214">이 값은 hello hello 가상 네트워크 주소 공간</span><span class="sxs-lookup"><span data-stu-id="ae9d0-214">This value is hello address space for hello virtual network</span></span>|
   |<span data-ttu-id="ae9d0-215">**서브넷 이름**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-215">**Subnet name**</span></span>|<span data-ttu-id="ae9d0-216">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="ae9d0-216">AppGatewaySubnet</span></span>|<span data-ttu-id="ae9d0-217">응용 프로그램 게이트웨이 hello에 대 한 hello 서브넷의 이름</span><span class="sxs-lookup"><span data-stu-id="ae9d0-217">Name of hello subnet for hello application gateway</span></span>|
   |<span data-ttu-id="ae9d0-218">**서브넷 주소 범위**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-218">**Subnet address range**</span></span>|<span data-ttu-id="ae9d0-219">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="ae9d0-219">10.0.0.0/28</span></span> | <span data-ttu-id="ae9d0-220">이 서브넷이 백 엔드 풀 멤버에 대 한 hello 가상 네트워크의 서브넷을 더 추가 허용</span><span class="sxs-lookup"><span data-stu-id="ae9d0-220">This subnet allows more additional subnets in hello virtual network for backend pool members</span></span>|

1. <span data-ttu-id="ae9d0-221">Hello에 **설정** 아래 블레이드 **프런트 엔드 IP 구성**, 선택 **공용** hello로 **IP 주소 유형**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-221">On hello **Settings** blade under **Frontend IP configuration**, choose **Public** as hello **IP address type**</span></span>

1. <span data-ttu-id="ae9d0-222">Hello에 **설정** 아래 블레이드 **공용 IP 주소**, 클릭 **공용 IP 주소를 선택**,이 단계는 hello 엽니다 **공용IP주소선택**블레이드에서 클릭 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-222">On hello **Settings** blade under **Public IP address**, click **Choose a public IP address**, this step opens hello **Choose public IP address** blade, click **Create new**.</span></span>

   ![공용 IP 선택][3]

1. <span data-ttu-id="ae9d0-224">Hello에 **공용 IP 주소 만들기** 블레이드에서 hello 기본값을 허용 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-224">On hello **Create public IP address** blade, accept hello default value, and click **OK**.</span></span> <span data-ttu-id="ae9d0-225">이 단계는 hello 닫습니다 **공용 IP 주소 선택** 블레이드, hello **공용 IP 주소 만들기** 블레이드에서 채웁니다 **공용 IP 주소** 선택 hello 공용 IP 주소와 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-225">This step closes hello **Choose public IP address** blade, hello **Create public IP address** blade, and populate **Public IP address** with hello public IP address chosen.</span></span>

1. <span data-ttu-id="ae9d0-226">Hello에 **설정** 아래 블레이드 **수신기 구성**, 클릭 **HTTP** 아래 **프로토콜**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-226">On hello **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="ae9d0-227">toouse **https**는 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-227">toouse **https**, a certificate is required.</span></span> <span data-ttu-id="ae9d0-228">hello 인증서의 개인 키 hello hello 인증서의.pfx 내보내기 toobe 제공 하며 hello 파일에 대 한 암호를 hello 하므로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-228">hello private key of hello certificate is needed so a .pfx export of hello certificate needs toobe provided and hello password for hello file.</span></span>

1. <span data-ttu-id="ae9d0-229">Hello 구성 **WAF** 특정 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-229">Configure hello **WAF** specific settings.</span></span>

   |<span data-ttu-id="ae9d0-230">**설정**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-230">**Setting**</span></span> | <span data-ttu-id="ae9d0-231">**값**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-231">**Value**</span></span> | <span data-ttu-id="ae9d0-232">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-232">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="ae9d0-233">**방화벽 상태**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-233">**Firewall status**</span></span>| <span data-ttu-id="ae9d0-234">사용</span><span class="sxs-lookup"><span data-stu-id="ae9d0-234">Enabled</span></span>| <span data-ttu-id="ae9d0-235">이 설정은 WAF를 켜고 끕니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-235">This setting turns WAF on or off.</span></span>|
   |<span data-ttu-id="ae9d0-236">**방화벽 모드**</span><span class="sxs-lookup"><span data-stu-id="ae9d0-236">**Firewall mode**</span></span> | <span data-ttu-id="ae9d0-237">방지</span><span class="sxs-lookup"><span data-stu-id="ae9d0-237">Prevention</span></span>| <span data-ttu-id="ae9d0-238">이 설정은 WAF 악의적인 트래픽을 수행 하는 hello 작업을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-238">This setting determines hello actions WAF takes on malicious traffic.</span></span> <span data-ttu-id="ae9d0-239">**검색** 을 선택하면 트래픽이 기록되기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-239">If **Detection** is chosen, traffic is only logged.</span></span>  <span data-ttu-id="ae9d0-240">**방지**를 선택하면 트래픽이 기록되고 403 권한 없음 응답에 따라 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-240">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span></span>|


1. <span data-ttu-id="ae9d0-241">Hello 요약 페이지를 검토 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-241">Review hello Summary page and click **OK**.</span></span>  <span data-ttu-id="ae9d0-242">이제 hello 응용 프로그램 게이트웨이 대기 되 고 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-242">Now hello application gateway is queued up and created.</span></span>

1. <span data-ttu-id="ae9d0-243">Hello 응용 프로그램 게이트웨이 만든 후 tooit hello 응용 프로그램 게이트웨이의 hello 포털 toocontinue 구성에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-243">Once hello application gateway has been created, navigate tooit in hello portal toocontinue configuration of hello application gateway.</span></span>

    ![Application Gateway 리소스 보기][10]

<span data-ttu-id="ae9d0-245">다음이 단계는 hello 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대 한 기본 설정으로 기본 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-245">These steps create a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="ae9d0-246">수정할 수 있습니다 이러한 설정을 toosuit 배포 hello를 프로 비전 하는 것은 성공 후</span><span class="sxs-lookup"><span data-stu-id="ae9d0-246">You can modify these settings toosuit your deployment once hello provisioning is successful</span></span>

> [!NOTE]
> <span data-ttu-id="ae9d0-247">Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-247">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae9d0-248">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae9d0-248">Next steps</span></span>

<span data-ttu-id="ae9d0-249">다음에 대해 알아볼 수 있습니다 어떻게 tooconfigure hello에 대 한 사용자 지정 도메인 별칭 [공용 IP 주소](../dns/dns-custom-domain.md#public-ip-address) Azure DNS 또는 다른 DNS 공급자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae9d0-249">Next, you can learn how tooconfigure a custom domain alias for hello [public IP address](../dns/dns-custom-domain.md#public-ip-address) using Azure DNS or another DNS provider.</span></span>

<span data-ttu-id="ae9d0-250">자세한 내용은 방법 tooconfigure 진단 로깅 toolog hello 되거나 되는 이벤트 검색 방문 하 여 웹 응용 프로그램 방화벽을 모두 방지할 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="ae9d0-250">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="ae9d0-251">사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ae9d0-251">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="ae9d0-252">어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ae9d0-252">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
