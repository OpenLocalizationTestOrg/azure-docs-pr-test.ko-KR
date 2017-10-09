---
title: "-Azure 응용 프로그램 게이트웨이-PowerShell aaaConfigure SSL 오프 로드를 | Microsoft Docs"
description: "이 페이지에서는 Azure 리소스 관리자를 사용 하 여 응용 프로그램 게이트웨이 ssl 오프 로드 하는 지침 toocreate 제공"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="6bb28-103">Azure Resource Manager를 사용하여 SSL 오프로드에 대한 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="6bb28-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bb28-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bb28-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="6bb28-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb28-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="6bb28-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bb28-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="6bb28-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6bb28-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="6bb28-108">Azure 응용 프로그램 게이트웨이 hello 게이트웨이 tooavoid 비용이 많이 드는 SSL 암호 해독 작업 toohappen hello 웹 팜에서에 구성 된 tooterminate hello (SECURE Sockets Layer) 세션 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="6bb28-109">SSL 오프 로드 hello 프런트 엔드 서버 설치 및 hello 웹 응용 프로그램 관리를 단순화합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6bb28-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6bb28-110">Before you begin</span></span>

1. <span data-ttu-id="6bb28-111">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="6bb28-112">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6bb28-113">가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="6bb28-114">가상 컴퓨터 또는 클라우드 배포 없습니다 hello 서브넷 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="6bb28-115">응용 프로그램 게이트웨이는 가상 네트워크 서브넷에서 단독이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="6bb28-116">toouse hello 응용 프로그램 게이트웨이 구성 하는 hello 서버 있어야 하거나 끝점 만든 hello 가상 네트워크 또는 할당 된 공용 IP/VIP와 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="6bb28-117">필요한 toocreate 응용 프로그램 게이트웨이 란?</span><span class="sxs-lookup"><span data-stu-id="6bb28-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="6bb28-118">**백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="6bb28-119">나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="6bb28-120">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="6bb28-121">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="6bb28-122">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="6bb28-123">트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="6bb28-124">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 설정은 대/소문자 구분) 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6bb28-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="6bb28-125">**규칙:** hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="6bb28-126">현재만 hello *기본* 규칙 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="6bb28-127">hello *기본* 규칙은 라운드 로빈 부하 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="6bb28-128">**추가 구성 정보**</span><span class="sxs-lookup"><span data-stu-id="6bb28-128">**Additional configuration notes**</span></span>

<span data-ttu-id="6bb28-129">SSL 인증서 구성에 대 한 프로토콜에서 hello **HttpListener** 도 변경 해야*Https* (대/소문자 구분).</span><span class="sxs-lookup"><span data-stu-id="6bb28-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="6bb28-130">hello **SslCertificate** 요소가 너무 추가**HttpListener** hello SSL 인증서에 대해 구성 하는 hello 변수 값으로.</span><span class="sxs-lookup"><span data-stu-id="6bb28-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="6bb28-131">hello 프런트 엔드 포트에는 업데이트 된 too443 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="6bb28-132">**tooenable 쿠키 기반 선호도**: 응용 프로그램 게이트웨이 클라이언트 세션에서 요청은 항상 방향이 지정 된 toohello 구성된 tooensure 수 hello 웹 팜의 동일한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="6bb28-133">이 시나리오는 hello 게이트웨이 toodirect 트래픽을 적절 하 게 허용 하는 세션 쿠키의 삽입으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="6bb28-134">tooenable 쿠키 기반 선호도 설정 **CookieBasedAffinity** 너무*Enabled* hello에 **BackendHttpSettings** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="6bb28-135">응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-135">Create an application gateway</span></span>

<span data-ttu-id="6bb28-136">hello hello Azure 클래식 배포 모델 및 Azure 리소스 관리자를 사용 하는 차이점은 toobe 구성 해야 하는 응용 프로그램 게이트웨이와 hello 항목이 만드는 hello 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="6bb28-137">리소스 관리자와 응용 프로그램 게이트웨이의 모든 구성 요소는 개별적으로 구성 하 고 다음 관리 함께 toocreate 응용 프로그램 게이트웨이 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="6bb28-138">응용 프로그램 게이트웨이 hello 필요한 단계 toocreate 키를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="6bb28-139">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="6bb28-140">가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="6bb28-141">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="6bb28-142">응용 프로그램 게이트웨이 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="6bb28-143">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="6bb28-144">PowerShell 모드 toouse hello Azure 리소스 관리자 cmdlet을 전환 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="6bb28-145">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bb28-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="6bb28-146">1단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="6bb28-147">2단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-147">Step 2</span></span>

<span data-ttu-id="6bb28-148">Hello 계정에 대 한 hello 구독을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6bb28-149">사용자가 입력 정보 요청된 tooauthenticate 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="6bb28-150">3단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-150">Step 3</span></span>

<span data-ttu-id="6bb28-151">Azure 구독 toouse 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="6bb28-152">4단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-152">Step 4</span></span>

<span data-ttu-id="6bb28-153">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="6bb28-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="6bb28-154">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6bb28-155">이 설정은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="6bb28-156">응용 프로그램 게이트웨이 사용 하 여 모든 명령을 toocreate hello 동일 하 고 있는지 확인 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="6bb28-157">리소스 그룹이 위의 hello 예제에서 만든 **appgw RG** 및 위치 **West US**합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="6bb28-158">가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="6bb28-159">hello 방법을 예제와 다음 toocreate 리소스 관리자를 사용 하 여 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="6bb28-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="6bb28-160">1단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="6bb28-161">이 샘플 hello 주소 범위 10.0.0.0/24 tooa 서브넷 사용 되는 변수 toobe toocreate 가상 네트워크를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="6bb28-162">2단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="6bb28-163">이 샘플 이라는 가상 네트워크를 만들어 **appgwvnet** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역 서브넷 10.0.0.0/24 hello 접두사 10.0.0.0/16 사용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="6bb28-164">3단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="6bb28-165">이 샘플에는 hello 서브넷 개체 toovariable $subnet hello 다음 단계에 대 한 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="6bb28-166">Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="6bb28-167">이 샘플에서는 공용 IP 리소스 **publicIP01** 리소스 그룹에 **appgw rg** hello 미국 서 부 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="6bb28-168">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="6bb28-169">1단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="6bb28-170">이 샘플은 **gatewayIP01**이라는 Application Gateway IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="6bb28-171">응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="6bb28-172">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="6bb28-173">2단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="6bb28-174">이 샘플에서는 이라는 hello 백 엔드 IP 주소 풀을 구성 **pool01** IP 주소와 **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="6bb28-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="6bb28-175">이러한 값은 hello 프런트 엔드 IP 끝점에서 제공 되는 hello 네트워크 트래픽을 수신 하는 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="6bb28-176">Hello hello IP 주소와 웹 응용 프로그램 끝점의 예를 앞에서 hello IP 주소를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="6bb28-177">3단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="6bb28-178">이 샘플에서는 응용 프로그램 게이트웨이 설정 구성 **poolsetting01** hello 백 엔드 풀에서 네트워크 트래픽을 tooload 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="6bb28-179">4단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="6bb28-180">이 샘플에서는 명명 된 hello 프런트 엔드 IP 포트 구성 **frontendport01** hello 공용 IP 끝점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="6bb28-181">5단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="6bb28-182">이 샘플에서는 SSL 연결에 사용 되는 hello 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="6bb28-183">hello 인증서.pfx 형식에서 toobe 하며 hello 암호 4 too12 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="6bb28-184">6단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="6bb28-185">이 샘플에서는 라는 hello 프런트 엔드 IP 구성을 만듭니다. **fipconfig01** associates hello hello 프런트 엔드 IP 구성 사용 하 여 공용 IP 주소 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="6bb28-186">7단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="6bb28-187">이 샘플에서는 수신기 이름을 hello 만듭니다 **listener01** 프런트 엔드 포트 toohello 프런트 엔드 IP 구성 및 인증서 associates hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="6bb28-188">8단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="6bb28-189">이 샘플에서는 hello 부하 분산 장치 라우팅 규칙 이라는 만듭니다 **rule01** hello 부하 분산 장치 동작을 구성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="6bb28-190">9단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="6bb28-191">이 샘플에서는 hello 인스턴스 크기의 hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="6bb28-192">기본값에 대 한 hello *InstanceCount* 최대 값이 10 인 2입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="6bb28-193">에 대 한 기본값을 hello *GatewaySize* 보통입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="6bb28-194">Standard_Small, Standard_Medium 및 Standard_Large 간에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="6bb28-195">10단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="6bb28-196">이 단계는 hello 응용 프로그램 게이트웨이에 hello SSL 정책 toouse를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="6bb28-197">방문 [SSL 구성 정책 버전 및 응용 프로그램 게이트웨이에 암호 그룹](application-gateway-configure-ssl-policy-powershell.md) toolearn 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="6bb28-198">New-AzureApplicationGateway를 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="6bb28-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="6bb28-199">이 샘플에서는 hello 이전 단계에서에서 모든 구성 항목을 포함 한 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="6bb28-200">Hello 예제에서는 응용 프로그램 게이트웨이 hello 라고 **appgwtest**합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="6bb28-201">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="6bb28-201">Get application gateway DNS name</span></span>

<span data-ttu-id="6bb28-202">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="6bb28-203">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="6bb28-204">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="6bb28-205">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6bb28-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="6bb28-206">toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="6bb28-207">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="6bb28-208">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="6bb28-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bb28-209">Next steps</span></span>

<span data-ttu-id="6bb28-210">내부 부하 분산 장치 ILB ()는 응용 프로그램 게이트웨이 toouse tooconfigure 참조 [내부 부하 분산 장치 (ILB) 응용 프로그램 게이트웨이 만들](application-gateway-ilb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bb28-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="6bb28-211">보다 자세한 내용을 원한다면 일반적 부하 분산 옵션을 참조:</span><span class="sxs-lookup"><span data-stu-id="6bb28-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="6bb28-212">Azure 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="6bb28-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="6bb28-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="6bb28-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

