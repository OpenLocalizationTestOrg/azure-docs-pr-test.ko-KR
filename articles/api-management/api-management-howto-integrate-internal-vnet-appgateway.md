---
title: "aaaHow toouse 응용 프로그램 게이트웨이 사용 하 여 가상 네트워크에서 Azure API 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toosetup 및 내부 가상 네트워크와 응용 프로그램 게이트웨이 (WAF) 프런트 엔드로의 Azure API 관리 구성"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="3211d-103">내부 VNET에서 Application Gateway와 API Management 통합</span><span class="sxs-lookup"><span data-stu-id="3211d-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="3211d-104"><a name="overview"> </a> 개요</span><span class="sxs-lookup"><span data-stu-id="3211d-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="3211d-105">hello 가상 네트워크 내 에서만 액세스할 수 있도록 내부 모드에서 가상 네트워크의 hello API 관리 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="3211d-106">Azure Application Gateway는 계층 7 부하 분산 장치를 제공하는 PAAS 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="3211d-107">역방향 프록시 서비스 역할을 하고 제품에 WAF(웹 응용 프로그램 방화벽)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="3211d-108">Hello 다음 시나리오를 활성화 hello 응용 프로그램 게이트웨이 프런트엔드와 내부는 VNET에 사용자를 프로 비전 하는 API 관리를 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="3211d-109">사용 하 여 hello 동일한 API 관리 리소스 소비자가 내부 및 외부 소비자가 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="3211d-110">단일 API Management 리소스를 사용하며 외부 소비자가 사용할 수 있는 API Management에서 정의된 API의 하위 집합을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="3211d-111">Hello에서 턴키 방식으로 tooswitch 액세스 tooAPI 관리 제공 공용 인터넷 켜고 끕니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="3211d-112"><a name="scenario"> </a> 시나리오</span><span class="sxs-lookup"><span data-stu-id="3211d-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="3211d-113">이 문서는 내부 및 외부 소비자에 대 한 toouse 단일 API 관리 서비스 하는 방법을 설명 하 고 두 온-프레미스에 대 한 단일 프런트엔드로 역할 및 Api 클라우드를 쉽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="3211d-114">살펴보면 어떻게 tooexpose hello 예에서는 녹색으로 강조 표시 된 Api의 하위 집합만을 통해 외부 응용 프로그램 게이트웨이에서 사용할 수 있는 hello PathBasedRouting 기능을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="3211d-115">첫 번째 설치 예제 hello에에서 모든 Api 가상 네트워크 내 에서만 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="3211d-116">내부 소비자(주황색으로 강조 표시됨)는 모든 내부 및 외부 API에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="3211d-117">트래픽은은 Express 경로 회로 통해 전달 되는 고성능 tooInternet 아웃 되지 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![url 경로](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="3211d-119"><a name="before-you-begin"> </a> 시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3211d-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="3211d-120">Hello 웹 플랫폼 설치 관리자를 사용 하 여 hello 최신 버전의 hello Azure PowerShell cmdlet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="3211d-121">다운로드 하 고 hello에서 hello 최신 버전을 설치할 수 **Windows PowerShell** hello 섹션 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="3211d-122">Virtual Network를 만들고 API Management 및 Application Gateway에 대한 별도 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="3211d-123">Toocreate hello 가상 네트워크에 대 한 사용자 지정 DNS 서버를 가져오려는 경우 그렇게 hello 배포를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="3211d-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="3211d-124">Hello 가상 네트워크에서에서 새 서브넷에서 만든 가상 컴퓨터에서 작동 하는 이중 확인 해결 하 고 모든 Azure 서비스 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="3211d-125">필요한 toocreate API 관리와 응용 프로그램 게이트웨이 간의 통합 이란?</span><span class="sxs-lookup"><span data-stu-id="3211d-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="3211d-126">**백 엔드 서버 풀:** hello 내부 가상 IP 주소를 hello API 관리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="3211d-127">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="3211d-128">이러한 설정은 hello 풀 내에서 적용 된 tooall 서버에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="3211d-129">**프런트 엔드 포트:** hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="3211d-130">것에 도달 하는 트래픽이 리디렉션된 tooone hello의 백 엔드 서버를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="3211d-131">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3211d-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="3211d-132">**규칙:** hello 규칙 수신기 tooa 백 엔드 서버 풀에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="3211d-133">**사용자 정의 상태 검사:** 응용 프로그램 게이트웨이 기본적으로 사용 하 여 IP 주소 기반 프로브 toofigure BackendAddressPool 어떤 서버 hello에 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="3211d-134">hello API 관리 서비스에만 toorequests hello 올바른 호스트 헤더를 포함 하는 응답, 따라서 hello 기본 프로브 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="3211d-135">사용자 지정 상태 프로브 필요한 toobe 정의 toohelp 응용 프로그램 게이트웨이 지 여부를 확인할 hello 서비스는 활성 상태 요청을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="3211d-136">**사용자 지정 도메인 인증서:** hello에서 API 관리 tooaccess 인터넷 toocreate 해당 이름의 호스트 이름 toohello 응용 프로그램 게이트웨이 프런트 엔드 DNS의 CNAME 매핑이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="3211d-137">이렇게 하면 hello hostname 헤더 및 보낸 인증서 tooApplication tooAPI 전달 되는 게이트웨이 관리 하나 임을 APIM 유효한 것으로 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="3211d-138"><a name="overview-steps"> </a> API Management 및 Application Gateway 통합에 필요한 단계</span><span class="sxs-lookup"><span data-stu-id="3211d-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="3211d-139">리소스 관리자에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="3211d-140">가상 네트워크, 서브넷 및 응용 프로그램 게이트웨이 hello에 대 한 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="3211d-141">API Management에 대한 다른 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="3211d-142">위에서 만든 hello VNET 서브넷 내에 API 관리 서비스를 만들고 hello 내부 모드를 사용 하 여 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="3211d-143">API 관리 서비스 hello에 hello 사용자 지정 도메인 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="3211d-144">Application Gateway 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="3211d-145">Application Gateway 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="3211d-146">API 관리 프록시 호스트 이름 hello 응용 프로그램 게이트웨이 toohello의 hello 공용 DNS 이름에서 CNAME을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="3211d-147">리소스 관리자에 대한 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="3211d-148">Hello 최신 버전의 Azure PowerShell을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="3211d-149">자세한 내용은 [Resource Manager에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3211d-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="3211d-150">1단계</span><span class="sxs-lookup"><span data-stu-id="3211d-150">Step 1</span></span>

<span data-ttu-id="3211d-151">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="3211d-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3211d-152">자격 증명을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="3211d-153">2단계</span><span class="sxs-lookup"><span data-stu-id="3211d-153">Step 2</span></span>

<span data-ttu-id="3211d-154">Hello 계정에 대 한 hello 구독을 확인 하 고 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="3211d-155">3단계</span><span class="sxs-lookup"><span data-stu-id="3211d-155">Step 3</span></span>

<span data-ttu-id="3211d-156">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="3211d-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="3211d-157">Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="3211d-158">이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="3211d-159">모든 명령을 toocreate 응용 프로그램 게이트웨이 사용 하 여 hello 확인 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="3211d-160">가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="3211d-161">다음 예제는 hello toocreate 사용 하 여 가상 네트워크에서 리소스 관리자를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="3211d-162">1단계</span><span class="sxs-lookup"><span data-stu-id="3211d-162">Step 1</span></span>

<span data-ttu-id="3211d-163">Hello 주소 범위 10.0.0.0/24 toohello 서브넷 변수 toobe 가상 네트워크를 만드는 동안 응용 프로그램 게이트웨이에 대 한 사용을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="3211d-164">2단계</span><span class="sxs-lookup"><span data-stu-id="3211d-164">Step 2</span></span>

<span data-ttu-id="3211d-165">Hello 주소 범위 10.0.1.0/24 toohello 서브넷 변수 toobe API 관리에 대 한 가상 네트워크를 만드는 동안 사용 되는 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="3211d-166">3단계</span><span class="sxs-lookup"><span data-stu-id="3211d-166">Step 3</span></span>

<span data-ttu-id="3211d-167">명명 된 가상 네트워크 만들기 **appgwvnet** 리소스 그룹에 **apim-appGw-RG** 접두사 10.0.0.0/16 hello를 사용 하 여 hello 미국 서 부 지역에 대 한 서브넷 10.0.0.0/24 및 10.0.1.0/24 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="3211d-168">4단계</span><span class="sxs-lookup"><span data-stu-id="3211d-168">Step 4</span></span>

<span data-ttu-id="3211d-169">Hello 다음 단계에 대 한 서브넷 변수 할당</span><span class="sxs-lookup"><span data-stu-id="3211d-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="3211d-170">내부 모드로 구성된 VNET 내에서 API Management 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="3211d-171">hello 다음 예제에서는 어떻게 toocreate VNET에 있는 API 관리 서비스에 액세스 하도록 구성 내부만</span><span class="sxs-lookup"><span data-stu-id="3211d-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="3211d-172">1단계</span><span class="sxs-lookup"><span data-stu-id="3211d-172">Step 1</span></span>
<span data-ttu-id="3211d-173">위에서 만든 $apimsubnetdata hello 서브넷을 사용 하 여 API 관리 가상 네트워크 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="3211d-174">2단계</span><span class="sxs-lookup"><span data-stu-id="3211d-174">Step 2</span></span>
<span data-ttu-id="3211d-175">Hello 가상 네트워크 내에 API 관리 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="3211d-176">성공 하면 명령 위에 hello 너무 참조[DNS 구성이 필요 tooaccess 내부 VNET API 관리 서비스](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="3211d-177">API Management에서 사용자 지정 도메인 이름 설정</span><span class="sxs-lookup"><span data-stu-id="3211d-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="3211d-178">1단계</span><span class="sxs-lookup"><span data-stu-id="3211d-178">Step 1</span></span>
<span data-ttu-id="3211d-179">Hello 도메인에 대 한 개인 키가 있는 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="3211d-180">이 예에서는 `*.contoso.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="3211d-181">2단계</span><span class="sxs-lookup"><span data-stu-id="3211d-181">Step 2</span></span>
<span data-ttu-id="3211d-182">Hello 인증서를 업로드 한 후 hello 프록시에 대 한 호스트 이름 구성 개체의 호스트 이름을 만들 `api.contoso.net`hello 예제 인증서 hello에 대 한 권한을 제공 하는 대로 `*.contoso.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="3211d-183">Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="3211d-184">공용 IP 리소스 만들기 **publicIP01** 리소스 그룹에 **apim-appGw-RG** hello 미국 서 부 지역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="3211d-185">IP 주소는 hello 서비스가 시작 될 때 toohello 응용 프로그램 게이트웨이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="3211d-186">응용 프로그램 게이트웨이 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-186">Create application gateway configuration</span></span>

<span data-ttu-id="3211d-187">Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="3211d-188">hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="3211d-189">1단계</span><span class="sxs-lookup"><span data-stu-id="3211d-189">Step 1</span></span>

<span data-ttu-id="3211d-190">**gatewayIP01**이라는 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="3211d-191">응용 프로그램 게이트웨이 시작할 때 구성 hello 서브넷에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="3211d-192">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="3211d-193">2단계</span><span class="sxs-lookup"><span data-stu-id="3211d-193">Step 2</span></span>

<span data-ttu-id="3211d-194">Hello hello 공용 IP 끝점에 대 한 프런트 엔드 IP 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="3211d-195">이 포트는 최종 사용자에 연결 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="3211d-196">3단계</span><span class="sxs-lookup"><span data-stu-id="3211d-196">Step 3</span></span>

<span data-ttu-id="3211d-197">공용 IP 끝점으로 hello 프런트 엔드 IP를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="3211d-198">4단계</span><span class="sxs-lookup"><span data-stu-id="3211d-198">Step 4</span></span>

<span data-ttu-id="3211d-199">Hello 응용 프로그램 게이트웨이 사용 되는 toodecrypt hello 인증서를 구성 하 고 통과 hello 트래픽을 다시 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="3211d-200">5단계</span><span class="sxs-lookup"><span data-stu-id="3211d-200">Step 5</span></span>

<span data-ttu-id="3211d-201">응용 프로그램 게이트웨이 hello에 대 한 hello HTTP 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="3211d-202">Hello 프런트 엔드 IP 구성, 포트 및 ssl 인증서 tooit 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="3211d-203">6단계</span><span class="sxs-lookup"><span data-stu-id="3211d-203">Step 6</span></span>

<span data-ttu-id="3211d-204">사용자 지정 프로브 toohello API 관리 서비스 만들기 `ContosoApi` 프록시 도메인 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="3211d-205">hello 경로 `/status-0123456789abcdef` 모든 hello API 관리 서비스에서 호스팅되는 기본 상태 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="3211d-206">설정 `api.contoso.net` 사용자 지정 프로브 hostname toosecure로 사용 하 여 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="3211d-207">호스트 이름 hello `contosoapi.azure-api.net` 서비스 라는 hello 기본 프록시 호스트 이름이 구성 되어 `contosoapi` 공용 Azure에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="3211d-208">7단계</span><span class="sxs-lookup"><span data-stu-id="3211d-208">Step 7</span></span>

<span data-ttu-id="3211d-209">Toobe hello SSL 사용 가능 백 엔드 풀 리소스에 사용 하는 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="3211d-210">이 hello 위의 4 단계에서에서 제공 하는 동일한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="3211d-211">8단계</span><span class="sxs-lookup"><span data-stu-id="3211d-211">Step 8</span></span>

<span data-ttu-id="3211d-212">응용 프로그램 게이트웨이 hello에 대 한 HTTP 백 엔드 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="3211d-213">해당 설정이 취소된 후에 백 엔드 요청에 대한 제한 시간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="3211d-214">이 값은 hello 프로브 시간 초과와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="3211d-215">9단계</span><span class="sxs-lookup"><span data-stu-id="3211d-215">Step 9</span></span>

<span data-ttu-id="3211d-216">명명 된 백 엔드 IP 주소 풀을 구성 **apimbackend** hello 내부 가상 ip 주소 hello API 관리 서비스의 위에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="3211d-217">10단계</span><span class="sxs-lookup"><span data-stu-id="3211d-217">Step 10</span></span>

<span data-ttu-id="3211d-218">더미(존재하지 않는) 백 엔드에 대한 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="3211d-219">요청 tooAPI 경로 tooexpose 응용 프로그램 게이트웨이 통해 API 관리에서 원하지 않는 것이 백 엔드를 404 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="3211d-220">Hello 더미 백 엔드에 대 한 HTTP 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="3211d-221">더미 백 엔드 구성 **dummyBackendPool**, tooa FQDN 주소가 가리키는 **dummybackend.com**합니다. 이 FQDN 주소가 hello 가상 네트워크에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="3211d-222">응용 프로그램 게이트웨이 toohello 존재 하지 않는 백 엔드를 가리키는 기본적으로 사용 하는 해당 hello를 설정 하는 규칙을 만들 **dummybackend.com** hello 가상 네트워크에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="3211d-223">11단계</span><span class="sxs-lookup"><span data-stu-id="3211d-223">Step 11</span></span>

<span data-ttu-id="3211d-224">Hello 백 엔드 풀에 대 한 규칙 경로 URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="3211d-225">이 통해 toohello 공개 노출 되기 위한 hello API 관리에서 Api의 일부에 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="3211d-226">예를 들어 `Echo API` (/echo/), `Calculator API` (/calc/) 등이 있으면 인터넷에서 `Echo API`에만 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="3211d-227">hello 다음 예제에서는 hello "/ 에코 /" 경로 라우팅 트래픽 toohello 백 엔드 "apimProxyBackendPool"에 대 한 간단한 규칙</span><span class="sxs-lookup"><span data-stu-id="3211d-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="3211d-228">Hello 경로 tooenable 경로 맵 구성에는 또한 라는 기본 백 엔드 주소 풀을 구성 하는 hello 규칙, API 관리에서 원하는 규칙 hello 경로 일치 하지 않으면 **dummyBackendPool**합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="3211d-229">예를 들어 http://api.contoso.net/calc/ * 라인 너무**dummyBackendPool** 일치 하지 않는 트래픽에 대 한 hello 기본 풀으로 정의 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="3211d-230">단계 위에 hello만 hello 경로 대 한 요청을 사용 하면 "/ echo" hello 응용 프로그램 게이트웨이 통해 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="3211d-231">API 관리에서 구성 된 Api 요청 tooother hello 인터넷에서에서 액세스할 때 응용 프로그램 게이트웨이에서 404 오류를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="3211d-232">12단계</span><span class="sxs-lookup"><span data-stu-id="3211d-232">Step 12</span></span>

<span data-ttu-id="3211d-233">Hello 응용 프로그램 게이트웨이 toouse URL 경로 기반 라우팅에 대 한 규칙 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="3211d-234">13단계</span><span class="sxs-lookup"><span data-stu-id="3211d-234">Step 13</span></span>

<span data-ttu-id="3211d-235">Hello 인스턴스 수 및 크기 hello 응용 프로그램 게이트웨이를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="3211d-236">여기서 사용 하 여 hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) hello API 관리 리소스의 보안을 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="3211d-237">14단계</span><span class="sxs-lookup"><span data-stu-id="3211d-237">Step 14</span></span>

<span data-ttu-id="3211d-238">WAF toobe "방지" 모드에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="3211d-239">Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-239">Create Application Gateway</span></span>

<span data-ttu-id="3211d-240">Hello 이전 단계에서에서 hello 구성 개체를 모두 포함 된 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3211d-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="3211d-241">CNAME hello API 관리 프록시 호스트 이름 toohello의 공용 DNS 이름 hello 응용 프로그램 게이트웨이 리소스</span><span class="sxs-lookup"><span data-stu-id="3211d-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="3211d-242">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="3211d-243">공용 IP를 사용할 때 응용 프로그램 게이트웨이 하지 않을 수 있는 쉬운 toouse 동적으로 할당 된 DNS 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="3211d-244">hello 응용 프로그램 게이트웨이 DNS 이름 이어야 합니다 hello APIM 프록시 호스트 이름을 가리키는 CNAME 레코드를 사용 하는 toocreate (예: `api.contoso.net` 위의 hello 예에) toothis DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="3211d-245">tooconfigure hello 프런트 엔드 IP CNAME 레코드의 응용 프로그램 게이트웨이 hello hello 세부 정보 및 hello PublicIPAddress 요소를 사용 하 여 연결 된 IP/DNS 이름을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="3211d-246">hello VIP 수 변하기 때문에 게이트웨이 다시 시작 hello를 사용 하 여 A 레코드의 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="3211d-247"><a name="summary"> </a> 요약</span><span class="sxs-lookup"><span data-stu-id="3211d-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="3211d-248">VNET에 구성 된 azure API 관리 호스트 된 온-프레미스가 든 상관 없이 또는 hello 클라우드의 모든 구성 된 Api에 대 한 단일 게이트웨이 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="3211d-249">API 관리 응용 프로그램 게이트웨이 통합 프런트 엔드 tooyour API 관리 인스턴스로 웹 응용 프로그램 방화벽 제공 수 있을 뿐만 아니라 특정 Api toobe hello 인터넷에서 액세스할 수 있는지를 선택적으로 사용의 hello 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3211d-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="3211d-250"><a name="next-steps"> </a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="3211d-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="3211d-251">Azure Application Gateway에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="3211d-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="3211d-252">응용 프로그램 게이트웨이 개요</span><span class="sxs-lookup"><span data-stu-id="3211d-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="3211d-253">Application Gateway 웹 응용 프로그램 방화벽</span><span class="sxs-lookup"><span data-stu-id="3211d-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="3211d-254">경로 기반 라우팅을 사용하는 Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3211d-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="3211d-255">API Management 및 VNET에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="3211d-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="3211d-256">Hello VNET 내 에서만 사용할 수 있는 API 관리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3211d-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="3211d-257">VNET에서 API Management 사용</span><span class="sxs-lookup"><span data-stu-id="3211d-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
