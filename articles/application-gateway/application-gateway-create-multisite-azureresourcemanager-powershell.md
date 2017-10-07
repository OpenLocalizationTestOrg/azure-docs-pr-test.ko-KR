---
title: "여러 사이트를 호스팅하는 응용 프로그램 게이트웨이 aaaCreate | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate hello에서 여러 웹 응용 프로그램에 대 한 Azure 응용 프로그램 게이트웨이 구성, 동일한 게이트웨이에 합니다."
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
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="8022f-103">여러 웹 응용 프로그램을 호스트하는 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8022f-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="8022f-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="8022f-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8022f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="8022f-106">여러 사이트 호스팅 사용 하면 하나의 웹 응용 프로그램 둘 이상의 toodeploy hello에 동일한 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="8022f-107">Hello 들어오는 HTTP 요청에는 수신기가 트래픽을 받게 toodetermine 호스트 헤더의 존재 여부에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="8022f-108">hello 수신기는 다음 트래픽 tooappropriate 백 엔드 풀의 hello 게이트웨이 hello 규칙 정의에 구성 된 대로 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="8022f-109">SSL 사용한 웹 응용 프로그램에서 응용 프로그램 게이트웨이 hello SNI 서버 이름 표시 () 확장 toochoose hello 올바른 수신기 hello 웹 트래픽에 대 한 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="8022f-110">여러 사이트 호스팅에 대 한 일반적인 용도는 다른 웹 도메인 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="8022f-111">마찬가지로 여러 하위 도메인의 hello에 동일한 루트 도메인을 호스팅할 수 또한 동일한 응용 프로그램 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="8022f-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="8022f-112">Scenario</span></span>

<span data-ttu-id="8022f-113">다음 예제는 hello에서 응용 프로그램 게이트웨이으로 두 개의 백 엔드 서버 풀 contoso.com과 fabrikam.com을에 대 한 트래픽을 제공: contoso 서버 풀 및 fabrikam 서버 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="8022f-114">유사한 설정을 app.contoso.com 및 blog.contoso.com와 같은 하위 도메인을 사용 하는 toohost 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="8022f-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8022f-116">Before you begin</span></span>

1. <span data-ttu-id="8022f-117">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="8022f-118">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8022f-119">hello 서버 toohello 백 엔드 풀 toouse hello 응용 프로그램 게이트웨이 있어야 하거나 끝점 만든 hello 할당 된 공용 IP/VIP를 사용 하거나 별도 서브넷에서 가상 네트워크에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="8022f-120">요구 사항</span><span class="sxs-lookup"><span data-stu-id="8022f-120">Requirements</span></span>

* <span data-ttu-id="8022f-121">**백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="8022f-122">나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="8022f-123">FQDN을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-123">FQDN can also be used.</span></span>
* <span data-ttu-id="8022f-124">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8022f-125">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="8022f-126">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="8022f-127">트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="8022f-128">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8022f-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="8022f-129">다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="8022f-130">**규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="8022f-131">트래픽 구체적인 정도 관계 없이 일치 하는 hello 첫 번째 규칙을 통해 이동 됩니다 및 규칙 나열 된 hello 순서로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="8022f-132">예를 들어 기본 수신기를 사용 하 여 규칙과 동일한 포트를 사용 하는 hello 규칙 hello에서 모두 다중 사이트 수신기를 사용 하 여 규칙을 설정한 경우 hello 다중 사이트 수신기 해야 보다 먼저 나열 되어야 hello 규칙으로 다중 사이트 규칙 toofunction hello에 대 한 순서 대로 기본 수신기 hello와 가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="8022f-133">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-133">Create an application gateway</span></span>

<span data-ttu-id="8022f-134">hello 다음은 위해 필요한 응용 프로그램 게이트웨이 toocreate hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="8022f-135">리소스 관리자에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="8022f-136">가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="8022f-137">응용 프로그램 게이트웨이 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="8022f-138">응용 프로그램 게이트웨이 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="8022f-139">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="8022f-140">Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="8022f-141">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8022f-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="8022f-142">1단계</span><span class="sxs-lookup"><span data-stu-id="8022f-142">Step 1</span></span>

<span data-ttu-id="8022f-143">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="8022f-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="8022f-144">사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="8022f-145">2단계</span><span class="sxs-lookup"><span data-stu-id="8022f-145">Step 2</span></span>

<span data-ttu-id="8022f-146">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="8022f-147">3단계</span><span class="sxs-lookup"><span data-stu-id="8022f-147">Step 3</span></span>

<span data-ttu-id="8022f-148">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="8022f-149">4단계</span><span class="sxs-lookup"><span data-stu-id="8022f-149">Step 4</span></span>

<span data-ttu-id="8022f-150">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="8022f-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="8022f-151">또는 응용 프로그램 게이트웨이의 리소스 그룹에 대한 태그를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="8022f-152">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="8022f-153">이 위치는 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="8022f-154">모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="8022f-155">리소스 그룹이 위의 hello 예제에서 만든 **appgw RG** 의 위치와 **West US**합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="8022f-156">응용 프로그램 게이트웨이에 대 한 사용자 지정 프로브 tooconfigure 해야 할 경우 참조 [PowerShell을 사용 하 여 사용자 지정 프로브 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-probe-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="8022f-157">자세한 내용은 [사용자 지정 프로브 및 상태 모니터링](application-gateway-probe-overview.md)으로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="8022f-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="8022f-158">가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="8022f-159">hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="8022f-160">이 단계에서는 두 개의 서브넷이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-160">Two subnets are created in this step.</span></span> <span data-ttu-id="8022f-161">첫 번째 서브넷 hello hello 응용 프로그램 게이트웨이 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="8022f-162">응용 프로그램 게이트웨이 해당 인스턴스는 자체 서브넷 toohold를 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="8022f-163">다른 응용 프로그램 게이트웨이의 해당 서브넷에만 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="8022f-164">hello 두 번째 서브넷이 사용 되는 toohold hello 응용 프로그램 백 엔드 서버.</span><span class="sxs-lookup"><span data-stu-id="8022f-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="8022f-165">1단계</span><span class="sxs-lookup"><span data-stu-id="8022f-165">Step 1</span></span>

<span data-ttu-id="8022f-166">Hello 주소 범위 10.0.0.0/24 toohello 서브넷 변수 toobe 사용 되는 toohold hello 응용 프로그램 게이트웨이 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="8022f-167">2단계</span><span class="sxs-lookup"><span data-stu-id="8022f-167">Step 2</span></span>

<span data-ttu-id="8022f-168">Hello 주소 범위 10.0.1.0/24 toohello e t 2 변수 toobe hello 백 엔드 풀에 사용 되는 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="8022f-169">3단계</span><span class="sxs-lookup"><span data-stu-id="8022f-169">Step 3</span></span>

<span data-ttu-id="8022f-170">명명 된 가상 네트워크 만들기 **appgwvnet** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 및 10.0.1.0/24 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="8022f-171">4단계</span><span class="sxs-lookup"><span data-stu-id="8022f-171">Step 4</span></span>

<span data-ttu-id="8022f-172">응용 프로그램 게이트웨이 만드는 hello 다음 단계에 대 한 서브넷 변수를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="8022f-173">Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="8022f-174">공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="8022f-175">IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="8022f-176">응용 프로그램 게이트웨이 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-176">Create application gateway configuration</span></span>

<span data-ttu-id="8022f-177">Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목을 tooset을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="8022f-178">hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="8022f-179">1단계</span><span class="sxs-lookup"><span data-stu-id="8022f-179">Step 1</span></span>

<span data-ttu-id="8022f-180">**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="8022f-181">응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="8022f-182">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="8022f-183">2단계</span><span class="sxs-lookup"><span data-stu-id="8022f-183">Step 2</span></span>

<span data-ttu-id="8022f-184">명명 된 hello 백 엔드 IP 주소 풀을 구성 **pool01** 및 **pool2** IP 주소와 **134.170.185.46**, **134.170.188.221**, **134.170.185.50** 에 대 한 **pool1** 및 **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  에 대 한 **pool2**합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="8022f-185">이 예제는 hello 요청 된 사이트에 따라 두 개의 백 엔드 풀 tooroute 네트워크 트래픽의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="8022f-186">하나의 풀은 사이트 "contoso.com"에서 트래픽을 수신하고 또 다른 풀은 사이트 "fabrikam.com"에서 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="8022f-187">사용자 고유의 응용 프로그램의 IP 주소 끝점 IP 주소 tooadd 앞 tooreplace hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="8022f-188">내부 IP 주소 대신 공용 IP 주소, FQDN 또는 VM의 NIC를 백 엔드 인스턴스에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="8022f-189">PowerShell 사용에 대신 Ip Fqdn toospecify "-BackendFQDNs" 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="8022f-190">3단계</span><span class="sxs-lookup"><span data-stu-id="8022f-190">Step 3</span></span>

<span data-ttu-id="8022f-191">응용 프로그램 게이트웨이 설정 구성 **poolsetting01** 및 **poolsetting02** hello 백 엔드 풀의 hello 부하 분산 된 네트워크 트래픽에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="8022f-192">이 예제에서는 hello 백 엔드 풀에 대 한 다른 백 엔드 풀 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="8022f-193">각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="8022f-194">4단계</span><span class="sxs-lookup"><span data-stu-id="8022f-194">Step 4</span></span>

<span data-ttu-id="8022f-195">공용 IP 끝점으로 hello 프런트 엔드 IP를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="8022f-196">5단계</span><span class="sxs-lookup"><span data-stu-id="8022f-196">Step 5</span></span>

<span data-ttu-id="8022f-197">Hello 프런트 엔드 포트에 대 한 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="8022f-198">6단계</span><span class="sxs-lookup"><span data-stu-id="8022f-198">Step 6</span></span>

<span data-ttu-id="8022f-199">SSL 인증서를 두 개의 구성 hello 두 웹 사이트에 대 한이 예에서 toosupport는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="8022f-200">인증서가 두 개는 contoso.com 트래픽 이며 다른 hello fabrikam.com 트래픽에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="8022f-201">이러한 인증서는 사용자 웹 사이트용으로 인증 기관에서 발급한 인증서여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="8022f-202">자체 서명된 인증서는 지원되지만 프로덕션 트래픽에 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="8022f-203">7단계</span><span class="sxs-lookup"><span data-stu-id="8022f-203">Step 7</span></span>

<span data-ttu-id="8022f-204">이 예에서 hello 두 개의 웹 사이트에 대 한 두 가지 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="8022f-205">이 단계에서는 사용 되는 tooreceive 들어오는 트래픽의 공용 IP 주소, 포트 및 호스트 hello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="8022f-206">HostName 매개 변수는 여러 사이트 지원에 대 한 필요 하며 집합 toohello 적절 한 웹 사이트는 hello에 대 한 트래픽을 수신 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="8022f-207">Requireservernameindication이 매개 변수는 여러 호스트 시나리오에서 SSL에 대 한 지원이 필요로 하는 웹 사이트에 대 한 tootrue를 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="8022f-208">SSL 지원이 필요한 경우 또한 해야 toospecify hello SSL 인증서 사용 되는 toosecure 트래픽이 해당 웹 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="8022f-209">FrontendIPConfiguration, FrontendPort, 및 호스트 이름 조합을 hello 고유 tooa 수신기 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="8022f-210">각 수신기는 하나의 인증서를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="8022f-211">8단계</span><span class="sxs-lookup"><span data-stu-id="8022f-211">Step 8</span></span>

<span data-ttu-id="8022f-212">이 예제에서 두 개의 웹 응용 프로그램을 hello에 대 한 설정 하는 두 개의 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="8022f-213">규칙은 수신기, 백 엔드 풀 및 http 설정을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="8022f-214">이 단계에서는 hello 응용 프로그램 게이트웨이 toouse 기본 라우팅 규칙을 각 웹 사이트에 대 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="8022f-215">트래픽 tooeach 웹 사이트는 해당 구성 된 수신기에서 수신 및 tooits 구성 BackendHttpSettings hello에 지정 된 hello 속성을 사용 하 여 백 엔드 풀을 향합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="8022f-216">9단계</span><span class="sxs-lookup"><span data-stu-id="8022f-216">Step 9</span></span>

<span data-ttu-id="8022f-217">Hello 인스턴스 수 및 크기 hello 응용 프로그램 게이트웨이를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="8022f-218">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="8022f-218">Create application gateway</span></span>

<span data-ttu-id="8022f-219">Hello 이전 단계에서에서 모든 구성 개체를 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="8022f-220">응용 프로그램 게이트웨이 프로 비전 장기 실행 작업으로 일부 시간 toocomplete 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8022f-221">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="8022f-221">Get application gateway DNS name</span></span>

<span data-ttu-id="8022f-222">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="8022f-223">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8022f-224">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="8022f-225">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8022f-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8022f-226">toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="8022f-227">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="8022f-228">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8022f-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8022f-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8022f-229">Next steps</span></span>

<span data-ttu-id="8022f-230">자세한 내용은 방법 tooprotect와 웹 사이트 [응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8022f-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

