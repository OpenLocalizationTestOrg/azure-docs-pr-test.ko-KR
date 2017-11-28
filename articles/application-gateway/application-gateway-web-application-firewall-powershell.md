---
title: "aaaConfigure 웹 응용 프로그램 방화벽 Azure 응용 프로그램 게이트웨이 | Microsoft Docs"
description: "이 문서는 어떻게 toostart 웹를 사용 하는 기존 또는 새 응용 프로그램 게이트웨이에 응용 프로그램 방화벽에 지침을 제공 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="ba42c-103">새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="ba42c-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba42c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ba42c-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="ba42c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba42c-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="ba42c-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ba42c-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="ba42c-107">웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 하거나 toocreate 웹 응용 프로그램 방화벽에서 응용 프로그램 게이트웨이 사용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="ba42c-108">hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="ba42c-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ba42c-110">장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="ba42c-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ba42c-112">지원 되는 기능의 전체 목록은 toofind 방문: [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="ba42c-113">hello 다음 문서에서는 어떻게 너무[응용 프로그램 게이트웨이 기존 웹 응용 프로그램 방화벽 tooan 추가](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들](#create-an-application-gateway-with-web-application-firewall)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![시나리오 이미지][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="ba42c-115">WAF 구성 차이</span><span class="sxs-lookup"><span data-stu-id="ba42c-115">WAF configuration differences</span></span>

<span data-ttu-id="ba42c-116">읽기 있으면 [PowerShell과 함께 응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-arm.md), 응용 프로그램 게이트웨이 만들 때 hello SKU 설정 tooconfigure 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="ba42c-117">WAF는 hello SKU 응용 프로그램 게이트웨이를 구성 하는 경우 추가 설정을 toodefine를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="ba42c-118">추가 변경 된 사항이 없습니다 hello 응용 프로그램 게이트웨이 자체에서 설정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="ba42c-119">**설정**</span><span class="sxs-lookup"><span data-stu-id="ba42c-119">**Setting**</span></span> | <span data-ttu-id="ba42c-120">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="ba42c-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="ba42c-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="ba42c-121">**SKU**</span></span> |<span data-ttu-id="ba42c-122">WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="ba42c-123">WAF의 hello 도입으로 두 개의 추가 Sku는 **WAF\_보통** 및 **WAF\_Large**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="ba42c-124">소형 Application Gateway에는 WAF가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="ba42c-125">**계층**</span><span class="sxs-lookup"><span data-stu-id="ba42c-125">**Tier**</span></span> | <span data-ttu-id="ba42c-126">hello 사용 가능한 값은 **표준** 또는 **WAF**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="ba42c-127">웹 응용 프로그램 방화벽을 사용하는 경우 **WAF**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="ba42c-128">**모드**</span><span class="sxs-lookup"><span data-stu-id="ba42c-128">**Mode**</span></span> | <span data-ttu-id="ba42c-129">이 설정은 WAF의 hello 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="ba42c-130">허용되는 값은 **검색** 및 **방지**입니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="ba42c-131">WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="ba42c-132">방지 모드에서 이벤트는 여전히 로깅되지만 hello 공격자가 응용 프로그램 게이트웨이 hello에서 403 권한 없는 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="ba42c-133">웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="ba42c-134">Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ba42c-135">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba42c-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="ba42c-136">Tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="ba42c-137">이 시나리오에 대 한 구독 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="ba42c-138">웹 응용 프로그램 방화벽에 추가 하는 hello 게이트웨이 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="ba42c-139">Hello 웹 응용 프로그램 방화벽 sku를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="ba42c-140">hello 사용 가능한 크기는 **WAF\_Large** 및 **WAF\_보통**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="ba42c-141">웹 응용 프로그램 방화벽 사용 되 면 hello 계층 야 **WAF**, hello sku를 설정할 때 hello 용량을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="ba42c-142">다음 예제는 hello에 정의 된 대로 WAF hello 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="ba42c-143">에 대 한 **FirewallMode**, hello 사용 가능한 값은 검색 및 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="ba42c-144">Hello 단계 이전에 정의 된 hello 설정을 사용 하 여 hello 응용 프로그램 게이트웨이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="ba42c-145">이 명령은 웹 응용 프로그램 방화벽으로 hello 응용 프로그램 게이트웨이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="ba42c-146">방문 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md) toounderstand tooview 응용 프로그램 게이트웨이 기록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="ba42c-147">WAF에서는 toohello 보안 이기 때문 로그 필요 toobe toounderstand 웹 응용 프로그램의 보안 상태를 hello 정기적으로 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="ba42c-148">웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="ba42c-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="ba42c-149">hello 다음 단계 이동에서 웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들기에 대 한 시작 tooend hello 전체 프로세스를 통해.</span><span class="sxs-lookup"><span data-stu-id="ba42c-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="ba42c-150">Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ba42c-151">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba42c-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="ba42c-152">TooAzure를 실행 하 여 로그인 `Login-AzureRmAccount`, 자격 증명으로 증명된 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="ba42c-153">실행 하 여 hello 계정에 대 한 hello 구독을 확인 합니다.`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="ba42c-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="ba42c-154">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="ba42c-155">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ba42c-155">Create a resource group</span></span>

<span data-ttu-id="ba42c-156">응용 프로그램 게이트웨이 hello에 대 한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="ba42c-157">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ba42c-158">이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ba42c-159">모든 명령을 사용 하 여 응용 프로그램 게이트웨이는 toocreate hello 동일한 리소스 그룹이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="ba42c-160">앞 예제는 hello, "appgw RG" 및 위치 "West US." 라는 리소스 그룹 생성</span><span class="sxs-lookup"><span data-stu-id="ba42c-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="ba42c-161">응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="ba42c-162">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="ba42c-163">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="ba42c-163">Configure virtual network</span></span>

<span data-ttu-id="ba42c-164">Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="ba42c-165">이 단계에서는 응용 프로그램 게이트웨이 hello 및 백 엔드 풀 멤버에 대 한 10.0.0.0/16 및 두 서브넷의 주소 공간을 사용 하 여 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="ba42c-166">공용 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="ba42c-166">Configure public IP address</span></span>

<span data-ttu-id="ba42c-167">주문 toohandle 외부 요청 응용 프로그램 게이트웨이 공용 IP 주소를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="ba42c-168">이 공용 IP 주소가 없어야는 `DomainNameLabel` hello 응용 프로그램 게이트웨이 사용한 toobe를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="ba42c-169">Hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="ba42c-170">Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ba42c-171">Application Gateway DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="ba42c-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="ba42c-172">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ba42c-173">공용 IP를 사용할 때 Application Gateway는 친근한 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ba42c-174">tooensure 최종 사용자가 응용 프로그램 게이트웨이 hello 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello 공용 끝점의 응용 프로그램 게이트웨이 hello 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="ba42c-175">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba42c-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="ba42c-176">별칭을 tooconfigure hello 응용 프로그램 게이트웨이 및 연결 된 hello PublicIPAddress 연결 요소 toohello 응용 프로그램 게이트웨이 사용 하 여 해당 IP/DNS 이름 세부 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="ba42c-177">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ba42c-178">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba42c-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="ba42c-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba42c-179">Next steps</span></span>

<span data-ttu-id="ba42c-180">자세한 내용은 방법 tooconfigure 진단 로깅 toolog hello 되거나 되는 이벤트 검색 방문 하 여 웹 응용 프로그램 방화벽을 모두 방지할 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="ba42c-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
