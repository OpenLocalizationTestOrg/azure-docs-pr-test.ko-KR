---
title: "여러 사이트를 호스트하는 Application Gateway 만들기 | Microsoft Docs"
description: "이 페이지에서는 동일한 게이트웨이에서 여러 웹 응용 프로그램을 호스트하는 Azure 응용 프로그램 게이트웨이를 만들고 구성하는 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="69d23-103">여러 웹 응용 프로그램을 호스트하는 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69d23-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="69d23-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="69d23-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="69d23-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="69d23-106">다중 사이트 호스팅을 통해 둘 이상의 웹 응용 프로그램을 동일한 응용 프로그램 게이트웨이에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="69d23-107">들어오는 HTTP 요청의 호스트 헤더 존재 여부에 따라 트래픽을 수신할 수신기가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="69d23-108">그런 다음 수신기는 게이트웨이 규칙 정의에 구성된 대로 적절한 백 엔드 풀로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="69d23-109">SSL 사용 웹 응용 프로그램에서 응용 프로그램 게이트웨이는 SNI(서버 이름 표시) 확장에 의존하여 웹 트래픽에 대한 올바른 수신기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="69d23-110">다중 사이트 호스팅의 일반적인 용도는 여러 웹 도메인에 대한 요청의 부하를 여러 백 엔드 서버 풀에 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="69d23-111">마찬가지로 같은 루트 도메인의 여러 하위 도메인을 동일한 응용 프로그램 게이트웨이에서 호스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="69d23-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="69d23-112">Scenario</span></span>

<span data-ttu-id="69d23-113">다음 예제에서 응용 프로그램 게이트웨이는 두 개의 백 엔드 서버 풀(contoso 서버 풀 및 fabrikam 서버 풀)을 통해 contoso.com 및 fabrikam.com에 대한 트래픽을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="69d23-114">유사한 설정을 사용하여 app.contoso.com 및 blog.contoso.com과 같은 하위 도메인을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="69d23-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="69d23-116">Before you begin</span></span>

1. <span data-ttu-id="69d23-117">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="69d23-118">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="69d23-119">응용 프로그램 게이트웨이를 사용하도록 백 엔드 풀에 추가된 서버가 존재하거나 별도의 서브넷에서 가상 네트워크에 또는 할당된 공용 IP/VIP와 함께 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="69d23-120">요구 사항</span><span class="sxs-lookup"><span data-stu-id="69d23-120">Requirements</span></span>

* <span data-ttu-id="69d23-121">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="69d23-122">나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="69d23-123">FQDN을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-123">FQDN can also be used.</span></span>
* <span data-ttu-id="69d23-124">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="69d23-125">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="69d23-126">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="69d23-127">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="69d23-128">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="69d23-129">다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="69d23-130">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 전달되어야 하는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="69d23-131">규칙은 나열된 순서대로 처리되고 트래픽은 특이성에 관계없이 일치하는 첫 번째 규칙을 통해 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="69d23-132">예를 들어 기본 수신기를 사용하는 규칙과 다중 사이트 수신기를 사용하는 규칙이 둘 다 같은 포트에 있는 경우 다중 사이트 규칙이 예상대로 작동하려면 다중 사이트 수신기를 사용하는 규칙은 기본 수신기를 사용하는 규칙 앞에 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="69d23-133">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-133">Create an application gateway</span></span>

<span data-ttu-id="69d23-134">다음은 Application Gateway를 만드는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="69d23-135">리소스 관리자에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="69d23-136">응용 프로그램 게이트웨이에 대한 가상 네트워크, 서브넷 및 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="69d23-137">응용 프로그램 게이트웨이 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="69d23-138">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="69d23-139">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="69d23-140">Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="69d23-141">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69d23-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="69d23-142">1단계</span><span class="sxs-lookup"><span data-stu-id="69d23-142">Step 1</span></span>

<span data-ttu-id="69d23-143">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="69d23-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="69d23-144">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="69d23-145">2단계:</span><span class="sxs-lookup"><span data-stu-id="69d23-145">Step 2</span></span>

<span data-ttu-id="69d23-146">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="69d23-147">3단계:</span><span class="sxs-lookup"><span data-stu-id="69d23-147">Step 3</span></span>

<span data-ttu-id="69d23-148">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="69d23-149">4단계:</span><span class="sxs-lookup"><span data-stu-id="69d23-149">Step 4</span></span>

<span data-ttu-id="69d23-150">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="69d23-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="69d23-151">또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="69d23-152">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="69d23-153">이 위치는 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="69d23-154">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="69d23-155">위 예제에서는 **appgw-RG**라는 리소스 그룹과 **West US**라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="69d23-156">응용 프로그램 게이트웨이에 사용자 지정 프로브를 구성해야 하는 경우 [PowerShell을 사용하여 사용자 지정 프로브로 응용 프로그램 게이트웨이 만들기](application-gateway-create-probe-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69d23-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="69d23-157">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="69d23-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="69d23-158">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="69d23-159">다음 예제에서는 리소스 관리자를 사용하여 가상 네트워크를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="69d23-160">이 단계에서는 두 개의 서브넷이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-160">Two subnets are created in this step.</span></span> <span data-ttu-id="69d23-161">응용 프로그램 게이트웨이 자체에 대 한 첫 번째 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="69d23-162">응용 프로그램 게이트웨이에서 자체 인스턴스를 보유하려면 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="69d23-163">다른 응용 프로그램 게이트웨이의 해당 서브넷에만 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="69d23-164">두 번째 서브넷은 응용 프로그램 백 엔드 서버를 보유하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="69d23-165">1단계</span><span class="sxs-lookup"><span data-stu-id="69d23-165">Step 1</span></span>

<span data-ttu-id="69d23-166">주소 범위 10.0.0.0/24를 응용 프로그램 게이트웨이를 보유하는 데 사용할 서브넷 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="69d23-167">2단계</span><span class="sxs-lookup"><span data-stu-id="69d23-167">Step 2</span></span>

<span data-ttu-id="69d23-168">주소 범위 10.0.1.0/24를 백엔드 풀에 사용할 서브넷2 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="69d23-169">3단계</span><span class="sxs-lookup"><span data-stu-id="69d23-169">Step 3</span></span>

<span data-ttu-id="69d23-170">접두사 10.0.0.0/16과 서브넷 10.0.0.0/24및 10.0.1.0/24를 사용하여 미국 서부 지역에 리소스 그룹 **appgw-rg**에서 **appgwvnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="69d23-171">4단계</span><span class="sxs-lookup"><span data-stu-id="69d23-171">Step 4</span></span>

<span data-ttu-id="69d23-172">응용 프로그램 게이트웨이를 만드는 다음 단계에 서브넷 변수를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="69d23-173">프런트 엔드 구성에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="69d23-174">미국 서부 지역에 리소스 그룹 **appgw-rg**에서 공용 IP 리소스 **publicIP01**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="69d23-175">서비스를 시작할 때 응용 프로그램 게이트웨이에 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="69d23-176">응용 프로그램 게이트웨이 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-176">Create application gateway configuration</span></span>

<span data-ttu-id="69d23-177">응용 프로그램 게이트웨이를 만들기 전에 모든 구성 항목을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="69d23-178">다음 단계 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="69d23-179">1단계:</span><span class="sxs-lookup"><span data-stu-id="69d23-179">Step 1</span></span>

<span data-ttu-id="69d23-180">**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="69d23-181">응용 프로그램 게이트웨이는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="69d23-182">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="69d23-183">2단계</span><span class="sxs-lookup"><span data-stu-id="69d23-183">Step 2</span></span>

<span data-ttu-id="69d23-184">IP 주소가 **134.170.185.46**, **134.170.188.221**, **134.170.185.50**인 **pool1**과 IP 주소가 **134.170.186.46**, **134.170.189.221**, **134.170.186.50**인 **pool2**로 백 엔드 IP 주소 풀, **pool01**과 **pool2**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="69d23-185">이 예제에서는 요청된 사이트를 기반으로 네트워크 트래픽을 라우팅하는 두 개의 백 엔드 풀이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="69d23-186">하나의 풀은 사이트 "contoso.com"에서 트래픽을 수신하고 또 다른 풀은 사이트 "fabrikam.com"에서 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="69d23-187">사용자 고유의 응용 프로그램 IP 주소 끝점을 추가하려면 이전 IP 주소를 교체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="69d23-188">내부 IP 주소 대신 공용 IP 주소, FQDN 또는 VM의 NIC를 백 엔드 인스턴스에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="69d23-189">PowerShell에서 IP 대신 FQDN을 지정하려면 "-BackendFQDNs" 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="69d23-190">3단계:</span><span class="sxs-lookup"><span data-stu-id="69d23-190">Step 3</span></span>

<span data-ttu-id="69d23-191">백 엔드 풀에서 부하가 분산된 네트워크 트래픽에 대해 Application Gateway 설정 **poolsetting01** 및 **poolsetting02**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="69d23-192">이 예제에서는 백 엔드 풀에 대한 다른 백 엔드 풀 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="69d23-193">각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="69d23-194">4단계</span><span class="sxs-lookup"><span data-stu-id="69d23-194">Step 4</span></span>

<span data-ttu-id="69d23-195">공용 IP 끝점으로 프런트 엔드 IP를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="69d23-196">5단계</span><span class="sxs-lookup"><span data-stu-id="69d23-196">Step 5</span></span>

<span data-ttu-id="69d23-197">응용 프로그램 게이트웨이에 대한 프런트 엔드 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="69d23-198">6단계</span><span class="sxs-lookup"><span data-stu-id="69d23-198">Step 6</span></span>

<span data-ttu-id="69d23-199">이 예제에서 지원하려는 두 웹 사이트에 대해 두 개의 SSL 인증서를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="69d23-200">인증서 하나는 contoso.com 트래픽용이고, 나머지는 fabrikam.com 트래픽용입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="69d23-201">이러한 인증서는 사용자 웹 사이트용으로 인증 기관에서 발급한 인증서여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="69d23-202">자체 서명된 인증서는 지원되지만 프로덕션 트래픽에 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="69d23-203">7단계</span><span class="sxs-lookup"><span data-stu-id="69d23-203">Step 7</span></span>

<span data-ttu-id="69d23-204">이 예제의 두 웹 사이트에 대한 두 개의 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="69d23-205">이 단계에서는 들어오는 트래픽을 수신하는 데 사용되는 공용 IP 주소, 포트 및 호스트에 대한 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="69d23-206">HostName 매개 변수는 다중 사이트 지원에 필요하며 트래픽이 수신되는 적절한 웹 사이트로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="69d23-207">RequireServerNameIndication 매개 변수는 다중 호스트 시나리오에서 SSL 지원이 필요한 웹 사이트에 대해 true로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="69d23-208">SSL 지원이 필요한 경우 해당 웹 응용 프로그램에 대한 트래픽의 보안을 유지하는 데 사용되는 SSL 인증서도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="69d23-209">FrontendIPConfiguration, FrontendPort 및 HostName의 조합은 수신기에 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="69d23-210">각 수신기는 하나의 인증서를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="69d23-211">8단계</span><span class="sxs-lookup"><span data-stu-id="69d23-211">Step 8</span></span>

<span data-ttu-id="69d23-212">이 예제의 두 웹 응용 프로그램에 대한 두 개의 규칙 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="69d23-213">규칙은 수신기, 백 엔드 풀 및 http 설정을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="69d23-214">이 단계에서는 각 웹 사이트에 기본 라우팅 규칙을 사용하도록 응용 프로그램 게이트웨이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="69d23-215">각 웹 사이트의 트래픽은 구성된 해당 수신기에서 수신된 후 BackendHttpSettings에 지정된 속성을 사용하여 구성된 해당 백 엔드 풀로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="69d23-216">9단계</span><span class="sxs-lookup"><span data-stu-id="69d23-216">Step 9</span></span>

<span data-ttu-id="69d23-217">응용 프로그램 게이트웨이에 대한 크기 및 인스턴스 수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="69d23-218">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="69d23-218">Create application gateway</span></span>

<span data-ttu-id="69d23-219">이전 단계의 모든 구성 개체로 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="69d23-220">응용 프로그램 게이트웨이 프로비전은 장기 실행 작업이며 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="69d23-221">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="69d23-221">Get application gateway DNS name</span></span>

<span data-ttu-id="69d23-222">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="69d23-223">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="69d23-224">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="69d23-225">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69d23-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="69d23-226">이 작업을 수행하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="69d23-227">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="69d23-228">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="69d23-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69d23-229">Next steps</span></span>

<span data-ttu-id="69d23-230">[응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)을 사용하여 웹 사이트를 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="69d23-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

