---
title: "URL 라우팅 규칙을 사용하여 Application Gateway 만들기 | Microsoft Docs"
description: "이 페이지에서는 URL 라우팅 규칙을 사용하여 Azure 응용 프로그램 게이트웨이를 만들고, 구성하기 위한 지침을 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: ba756d3262b9780c5701e69faad860ba32bba08b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="d33a3-103">경로 기반 라우팅을 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d33a3-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d33a3-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="d33a3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="d33a3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="d33a3-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d33a3-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="d33a3-107">URL 경로 기반 라우팅을 사용하여 Http 요청의 URL 경로에 따라 경로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="d33a3-108">Application Gateway에 제공된 URL에 대해 구성된 백 엔드 풀에 대한 경로가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway.</span></span> <span data-ttu-id="d33a3-109">그런 다음 정의된 백 엔드 풀로 네트워크 트래픽을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-109">It then sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="d33a3-110">URL 기반 라우팅의 일반적인 용도는 여러 콘텐츠 형식에 대한 요청의 부하를 여러 백 엔드 서버 풀에 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-110">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="d33a3-111">URL 기반 라우팅에서는 응용 프로그램 게이트웨이에 새로운 규칙 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-111">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="d33a3-112">응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 PathBasedRouting)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="d33a3-113">기본 규칙 형식은 라운드 로빈 배포 외에도 PathBasedRouting 동안 백 엔드 풀에 대한 라운드 로빈 서비스를 제공하며 백 엔드 풀을 선택한 상태에서는 요청 URL의 경로 패턴도 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-113">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="d33a3-114">시나리오</span><span class="sxs-lookup"><span data-stu-id="d33a3-114">Scenario</span></span>

<span data-ttu-id="d33a3-115">다음 예제에서 Application Gateway는 두 개의 백 엔드 서버 풀(video 서버 풀 및 image 서버 풀)과 함께 contoso.com에 대한 트래픽을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-115">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="d33a3-116">http://contoso.com/image*에 대한 요청은 image 서버 풀(pool1)로 라우팅되고 http://contoso.com/video*에 대한 요청은 video 서버 풀(pool2)로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-116">Requests for http://contoso.com/image* are routed to image server pool (pool1), and http://contoso.com/video* are routed to video server pool (pool2).</span></span> <span data-ttu-id="d33a3-117">경로 패턴과 일치하는 항목이 없는 경우 기본 서버 풀(pool1)이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-117">if none of the path patterns match, a default server pool (pool1) is selected.</span></span>

![url 경로](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="d33a3-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d33a3-119">Before you begin</span></span>

1. <span data-ttu-id="d33a3-120">웹 플랫폼 설치 관리자를 사용하는 Azure PowerShell cmdlet의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="d33a3-121">**다운로드 페이지** 의 [Windows PowerShell](https://azure.microsoft.com/downloads/)섹션에서 최신 버전을 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d33a3-122">Application Gateway에 대한 가상 네트워크 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="d33a3-123">서브넷을 사용 중인 가상 컴퓨터 또는 클라우드 배포가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-123">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="d33a3-124">응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-124">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d33a3-125">응용 프로그램 게이트웨이를 사용하도록 백 엔드 풀에 추가된 서버가 존재하거나 가상 네트워크 또는 공용 IP/VIP가 할당된 해당 끝점이 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-125">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="d33a3-126">응용 프로그램 게이트웨이를 만드는 데 필요한 것은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d33a3-126">What is required to create an application gateway?</span></span>

* <span data-ttu-id="d33a3-127">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="d33a3-128">나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d33a3-129">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d33a3-130">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="d33a3-131">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="d33a3-132">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="d33a3-133">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d33a3-134">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 전달되어야 하는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-134">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="d33a3-135">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-135">Create an application gateway</span></span>

<span data-ttu-id="d33a3-136">Azure Classic 및 Azure Resource Manager 간의 차이점은 응용 프로그램 게이트웨이를 만드는 순서와 구성할 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-136">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="d33a3-137">Resource Manager를 사용하면 응용 프로그램 게이트웨이를 만드는 모든 항목이 개별적으로 구성된 후 응용 프로그램 게이트웨이 리소스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-137">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="d33a3-138">다음은 응용 프로그램 게이트웨이를 만드는 데 필요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-138">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="d33a3-139">리소스 관리자에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="d33a3-140">응용 프로그램 게이트웨이에 대한 가상 네트워크, 서브넷 및 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-140">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="d33a3-141">응용 프로그램 게이트웨이 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="d33a3-142">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d33a3-143">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d33a3-144">Azure PowerShell의 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-144">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="d33a3-145">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d33a3-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d33a3-146">1단계:</span><span class="sxs-lookup"><span data-stu-id="d33a3-146">Step 1</span></span>

<span data-ttu-id="d33a3-147">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="d33a3-147">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d33a3-148">자격 증명을 사용하여 인증하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-148">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="d33a3-149">2단계:</span><span class="sxs-lookup"><span data-stu-id="d33a3-149">Step 2</span></span>

<span data-ttu-id="d33a3-150">계정에 대한 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-150">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="d33a3-151">3단계:</span><span class="sxs-lookup"><span data-stu-id="d33a3-151">Step 3</span></span>

<span data-ttu-id="d33a3-152">사용할 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-152">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="d33a3-153">4단계:</span><span class="sxs-lookup"><span data-stu-id="d33a3-153">Step 4</span></span>

<span data-ttu-id="d33a3-154">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="d33a3-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="d33a3-155">또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="d33a3-156">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d33a3-157">이 리소스 그룹은 해당 리소스 그룹에서 리소스의 기본 위치로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-157">This resource group is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="d33a3-158">응용 프로그램 게이트웨이를 만들기 위한 모든 명령이 동일한 리소스 그룹을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-158">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="d33a3-159">위 예제에서는 "appgw-RG"라는 리소스 그룹과 "West US"라는 위치를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-159">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="d33a3-160">응용 프로그램 게이트웨이에 사용자 지정 프로브를 구성해야 하는 경우 [PowerShell을 사용하여 사용자 지정 프로브로 응용 프로그램 게이트웨이 만들기](application-gateway-create-probe-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d33a3-160">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="d33a3-161">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="d33a3-162">응용 프로그램 게이트웨이에 대한 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-162">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="d33a3-163">다음 예제에서는 리소스 관리자를 사용하여 가상 네트워크를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-163">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="d33a3-164">이 예제에서는 Application Gateway에 대한 VNET을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-164">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="d33a3-165">Application Gateway에는 자체의 서브넷이 필요하며, 이러한 이유로 Application Gateway에 대해 만들어진 서브넷은 VNET 주소 공간보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-165">Application Gateway requires its own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="d33a3-166">동일한 VNET에서 구성할 웹 서버를 포함하지만 이에 제한되지 않는 다른 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-166">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="d33a3-167">1단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-167">Step 1</span></span>

<span data-ttu-id="d33a3-168">주소 범위 10.0.0.0/24를 가상 네트워크를 만드는 데 사용할 서브넷 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="d33a3-169">다음 예제에서 사용되는 Application Gateway에 대한 서브넷 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-169">This creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="d33a3-170">2단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-170">Step 2</span></span>

<span data-ttu-id="d33a3-171">접두사 10.0.0.0/16과 서브넷 10.0.0.0/24를 사용하여 미국 서부 지역에 리소스 그룹 **appgw-rg**에서 **appgwvnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="d33a3-172">배치할 Application Gateway에 대한 단일 서브넷을 사용하여 VNET 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-172">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="d33a3-173">3단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-173">Step 3</span></span>

<span data-ttu-id="d33a3-174">다음 단계의 서브넷 변수를 할당합니다. 이 변수는 이후 단계에서 `New-AzureRMApplicationGateway` cmdlet에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-174">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="d33a3-175">프런트 엔드 구성에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-175">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="d33a3-176">미국 서부 지역에 리소스 그룹 **appgw-rg**에서 공용 IP 리소스 **publicIP01**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="d33a3-177">Application Gateway는 공용 IP 주소, 내부 IP 주소 또는 둘 다를 사용하여 부하 분산 요청을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-177">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="d33a3-178">이 예제에서는 공용 IP 주소만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-178">This example only uses a public IP address.</span></span> <span data-ttu-id="d33a3-179">다음 예제에는 공용 IP 주소를 만들도록 구성된 DNS 이름이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-179">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="d33a3-180">Application Gateway는 공용 IP 주소에서 사용자 지정 DNS 이름을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="d33a3-181">공용 끝점에 사용자 지정 이름이 필요한 경우 공용 IP 주소에 대해 자동으로 생성된 DNS 이름을 가리키도록 CNAME 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-181">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="d33a3-182">서비스를 시작할 때 응용 프로그램 게이트웨이에 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-182">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="d33a3-183">응용 프로그램 게이트웨이 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-183">Create application gateway configuration</span></span>

<span data-ttu-id="d33a3-184">응용 프로그램 게이트웨이를 만들기 전에 모든 구성 항목을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-184">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="d33a3-185">다음 단계 응용 프로그램 게이트웨이 리소스에 필요한 구성 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="d33a3-186">1단계:</span><span class="sxs-lookup"><span data-stu-id="d33a3-186">Step 1</span></span>

<span data-ttu-id="d33a3-187">**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="d33a3-188">Application Gateway는 시작되면 구성된 서브넷에서 IP 주소를 선택하고 백 엔드 IP 풀의 IP 주소로 네트워크 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-188">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="d33a3-189">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="d33a3-190">2단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-190">Step 2</span></span>

<span data-ttu-id="d33a3-191">**pool1** 및 **pool2**에 대해 IP 주소가 **pool01** 및 **pool2**인 백 엔드 IP 주소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-191">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="d33a3-192">이러한 IP 주소는 응용 프로그램 게이트웨이에서 보호될 웹 응용 프로그램을 호스팅하는 리소스의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-192">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="d33a3-193">이러한 백 엔드 풀 멤버는 모두 기본 프로브인지 아니면 사용자 지정 프로브인지에 관계 없이 프로브를 통해 유효성이 정상 상태인 것으로 검사되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-193">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="d33a3-194">그런 다음 요청이 응용 프로그램 게이트웨이로 들어오면 트래픽이 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-194">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="d33a3-195">백 엔드 풀은 응용 프로그램 게이트웨이 내에서 여러 규칙을 통해 사용될 수 있습니다. 즉, 하나의 백 엔드 풀이 동일한 호스트에 있는 여러 웹 응용 프로그램에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-195">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="d33a3-196">이 예제에서는 URL 경로를 기반으로 네트워크 트래픽을 라우트하는 두 개의 백 엔드 풀이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-196">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="d33a3-197">하나의 풀은 URL 경로 "/video"에서 트래픽을 수신하고 또 다른 풀은 경로 "/image"에서 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="d33a3-198">사용자 고유의 응용 프로그램 IP 주소 끝점을 추가하려면 이전 IP 주소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-198">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="d33a3-199">3단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-199">Step 3</span></span>

<span data-ttu-id="d33a3-200">백 엔드 풀에서 부하가 분산된 네트워크 트래픽에 대해 Application Gateway 설정 **poolsetting01** 및 **poolsetting02**를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="d33a3-201">이 예제에서는 백 엔드 풀에 대한 다른 백 엔드 풀 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-201">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="d33a3-202">각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="d33a3-203">백 엔드 HTTP 설정은 올바른 백 엔드 풀 멤버에게 트래픽을 라우팅하는 규칙에서 사용되며,</span><span class="sxs-lookup"><span data-stu-id="d33a3-203">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="d33a3-204">백 엔드 풀 멤버에 트래픽을 보낼 때 사용되는 프로토콜과 포트를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-204">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="d33a3-205">쿠키 기반 세션도 백 엔드 HTTP 설정에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-205">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="d33a3-206">이 설정이 활성화되면 쿠키 기반 세션 선호도는 각 패킷에 대한 이전 요청과 동일한 백 엔드로 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-206">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="d33a3-207">4단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-207">Step 4</span></span>

<span data-ttu-id="d33a3-208">공용 IP 끝점으로 프런트 엔드 IP를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-208">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="d33a3-209">프런트 엔드 IP 구성 개체는 외부 연결 IP 주소와 수신기의 관계를 설정하기 위해 수신기에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-209">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="d33a3-210">5단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-210">Step 5</span></span>

<span data-ttu-id="d33a3-211">응용 프로그램 게이트웨이에 대한 프런트 엔드 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-211">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="d33a3-212">프런트 엔드 포트 구성 개체는 Application Gateway에서 수신기의 트래픽을 수신 대기하는 포트를 정의하기 위해 수신기에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-212">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="d33a3-213">6단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-213">Step 6</span></span>

<span data-ttu-id="d33a3-214">수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-214">Configure the listener.</span></span> <span data-ttu-id="d33a3-215">이 단계에서는 들어오는 네트워크 트래픽을 수신하는 데 사용되는 공용 IP 주소 및 포트에 대한 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-215">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="d33a3-216">다음 예제에서는 이전에 구성한 프런트 엔드 IP 구성, 프런트 엔드 포트 구성 및 프로토콜(http 또는 https)을 사용하여 수신기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-216">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="d33a3-217">이 예제에서 수신기는 이전에 만든 공용 IP 주소의 80 포트에서 HTTP 트래픽을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-217">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="d33a3-218">7단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-218">Step 7</span></span>

<span data-ttu-id="d33a3-219">백 엔드 풀에 대한 URL 규칙 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-219">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="d33a3-220">이 단계에서는 응용 프로그램 게이트웨이에서 사용되는 상대 경로를 구성하고 URL 경로와 들어오는 트래픽을 처리하는 데 할당되는 백 엔드 풀 간의 매핑을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-220">This step configures the relative path used by application gateway and defines the mapping between the URL path and the back-end pool that is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d33a3-221">각 경로는 /로 시작해야 하고 "\*"는 끝에만 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-221">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="d33a3-222">사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="d33a3-223">경로 검사기에 제공하는 문자열은 "?" 또는 "#"으로 시작하는 텍스트는 포함하지 않습니다. 이러한 문자는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-223">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="d33a3-224">다음의 예제에서는 두 개의 규칙을 만듭니다. 백 엔드 "pool1"로 트래픽을 라우트하는 "/image/" 경로에 대한 규칙과 백 엔드 "pool2"로 트래픽을 라우트하는 "/video/" 경로에 대한 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-224">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2."</span></span> <span data-ttu-id="d33a3-225">이러한 규칙은 각 url 집합에 대한 트래픽이 백 엔드에 라우팅되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-225">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="d33a3-226">예를 들어 http://contoso.com/image/figure1.jpg는 pool1로 이동하고 http://contoso.com/video/example.mp4는 pool2로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-226">For example, http://contoso.com/image/figure1.jpg goes to pool1 and http://contoso.com/video/example.mp4 goes to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="d33a3-227">또한 경로가 미리 정의된 경로 규칙과 일치하지 않으면 규칙 경로 맵 구성은 기본 백 엔드 주소 풀을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-227">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="d33a3-228">예를 들어 http://contoso.com/shoppingcart/test.html은 일치하지 않는 트래픽에 대한 기본 풀로 정의된 대로 pool1로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-228">For example, http://contoso.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="d33a3-229">8단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-229">Step 8</span></span>

<span data-ttu-id="d33a3-230">규칙 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-230">Create a rule setting.</span></span> <span data-ttu-id="d33a3-231">이 단계에서는 URL 경로 기반 라우팅을 사용하도록 응용 프로그램 게이트웨이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-231">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="d33a3-232">이전 단계에서 정의된 `$urlPathMap` 변수는 이제 경로 기반 규칙을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-232">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="d33a3-233">이 단계에서 규칙을 수신기 및 앞에서 만든 url 경로 매핑에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-233">In this step, we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="d33a3-234">9단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-234">Step 9</span></span>

<span data-ttu-id="d33a3-235">응용 프로그램 게이트웨이에 대한 크기 및 인스턴스 수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-235">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="d33a3-236">Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="d33a3-236">Create Application Gateway</span></span>

<span data-ttu-id="d33a3-237">이전 단계의 모든 구성 개체로 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-237">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d33a3-238">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="d33a3-238">Get application gateway DNS name</span></span>

<span data-ttu-id="d33a3-239">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-239">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="d33a3-240">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d33a3-241">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-241">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="d33a3-242">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d33a3-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d33a3-243">프런트 엔드 IP CNAME 기록을 구성하려면 Application Gateway에 연결된 PublicIPAddress 요소를 사용하여 Application Gateway 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-243">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="d33a3-244">응용 프로그램 게이트웨이의 DNS 이름은 CNAME 레코드를 만드는 데 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-244">The application gateway's DNS name should be used to create a CNAME record.</span></span> <span data-ttu-id="d33a3-245">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d33a3-245">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d33a3-246">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d33a3-246">Next steps</span></span>

<span data-ttu-id="d33a3-247">SSL(Secure Sockets Layer) 오프로드를 알아보려는 경우 [SSL 오프로드에 대해 응용 프로그램 게이트웨이 구성](application-gateway-ssl-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d33a3-247">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

