---
title: "aaaConfigure 끝 tooend Azure 응용 프로그램 게이트웨이 통해 SSL | Microsoft Docs"
description: "이 문서에서는 tooconfigure tooend Azure 리소스 관리자 PowerShell을 사용 하 여 응용 프로그램 게이트웨이 함께 SSL 종료 하는 방법을 설명 합니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="99db3-103">PowerShell을 사용 하 여 응용 프로그램 게이트웨이 사용 하 여 최종 tooend SSL 구성</span><span class="sxs-lookup"><span data-stu-id="99db3-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="99db3-104">개요</span><span class="sxs-lookup"><span data-stu-id="99db3-104">Overview</span></span>

<span data-ttu-id="99db3-105">응용 프로그램 게이트웨이 지원 트래픽의 tooend 암호화를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="99db3-106">응용 프로그램 게이트웨이 hello 응용 프로그램 게이트웨이에서 hello SSL 연결을 종료 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="99db3-107">hello 게이트웨이 toohello 트래픽을 다시 hello 패킷 암호화 및 hello 패킷 toohello 적절 한 백 엔드 hello 라우팅 규칙 정의에 따라 전달 hello 라우팅 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="99db3-108">Hello 웹 서버에서 받은 모든 응답 hello를 통해 이동 백 toohello 최종 사용자를 처리 하는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="99db3-109">Application Gateway가 사용자 지정 SSL 옵션을 정의하도록 지원하는 다른 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="99db3-110">응용 프로그램 게이트웨이 다음 프로토콜 버전; 해제 hello를 지원 합니다. **TLSv1.0**, **TLSv1.1**, 및 **TLSv1.2** 도 암호화 된 기본 설정의 도구 모음 toouse 및 hello 순서는 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="99db3-111">구성 가능한 SSL 옵션에 대해 자세히 toolearn 방문 [SSL 정책 개요](application-gateway-SSL-policy-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="99db3-112">SSL 2.0 및 SSL 3.0은 기본적으로 사용할 수 없도록 설정되며 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="99db3-113">보안 되지 않은 것으로 간주 되며 응용 프로그램 게이트웨이 함께 사용할 수 toobe 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![시나리오 이미지][scenario]

## <a name="scenario"></a><span data-ttu-id="99db3-115">시나리오</span><span class="sxs-lookup"><span data-stu-id="99db3-115">Scenario</span></span>

<span data-ttu-id="99db3-116">사용 하 여 응용 프로그램 게이트웨이 toocreate tooend SSL 종료 하는 방법을 배웁니다이 시나리오에서는 PowerShell을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="99db3-117">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-117">This scenario will:</span></span>

* <span data-ttu-id="99db3-118">**appgw-rg**라는 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="99db3-119">주소 공간이 10.0.0.0/16인 **appgwvnet**이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="99db3-120">**appgwsubnet** 및 **appsubnet**라는 두 개의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="99db3-121">암호 그룹 및 SSL 프로토콜 버전 제한 하는 작은 응용 프로그램 게이트웨이 지원 끝 tooend SSL 암호화를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="99db3-122">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="99db3-122">Before you begin</span></span>

<span data-ttu-id="99db3-123">응용 프로그램 게이트웨이와 tooconfigure 끝 tooend SSL는 인증서가 필요 hello 게이트웨이에 대 한 고 hello 백 엔드 서버에 대 한 인증서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="99db3-124">hello 게이트웨이 인증서가 사용 되는 tooencrypt 및 암호 해독 hello 보낸 트래픽은 tooit SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="99db3-125">hello 게이트웨이 인증서 toobe 개인 정보 교환 (pfx) 형태로 표시 되어야합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="99db3-126">이 파일 형식을 사용 하면 hello에 대 한 개인 키 toobe 내보낸 hello 응용 프로그램 게이트웨이 tooperform hello 암호화 및 암호 해독 트래픽의 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="99db3-127">끝에 대 한 tooend SSL 암호화 hello 백 엔드 응용 프로그램 게이트웨이와 허용 목록 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="99db3-128">이 hello hello 백 엔드 toohello 응용 프로그램 게이트웨이의 공용 인증서를 업로드 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="99db3-129">이렇게 하면 해당 hello 응용 프로그램 게이트웨이 백 엔드 알려진된 인스턴스와만 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="99db3-130">이 추가 hello 끝 tooend 통신을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="99db3-131">이 프로세스는 hello 다음 단계에에서 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="99db3-132">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-132">Create hello Resource Group</span></span>

<span data-ttu-id="99db3-133">이 섹션에서는 hello 응용 프로그램 게이트웨이 포함 하는 리소스 그룹을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="99db3-134">1단계</span><span class="sxs-lookup"><span data-stu-id="99db3-134">Step 1</span></span>

<span data-ttu-id="99db3-135">Tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="99db3-136">2단계</span><span class="sxs-lookup"><span data-stu-id="99db3-136">Step 2</span></span>

<span data-ttu-id="99db3-137">이 시나리오에 대 한 구독 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="99db3-138">3단계</span><span class="sxs-lookup"><span data-stu-id="99db3-138">Step 3</span></span>

<span data-ttu-id="99db3-139">리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.</span><span class="sxs-lookup"><span data-stu-id="99db3-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="99db3-140">가상 네트워크 및 서브넷을 hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="99db3-141">hello 다음 예제에서는 가상 네트워크 및 서브넷 2 개</span><span class="sxs-lookup"><span data-stu-id="99db3-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="99db3-142">한 서브넷은 사용 되는 toohold hello 응용 프로그램 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="99db3-143">hello 다른 서브넷 hello 백 엔드 호스팅 hello 웹 응용 프로그램 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="99db3-144">1단계</span><span class="sxs-lookup"><span data-stu-id="99db3-144">Step 1</span></span>

<span data-ttu-id="99db3-145">응용 프로그램 게이트웨이 자체 hello에 대 한 hello 서브넷을 사용할 수는 주소 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="99db3-146">Application Gateway를 구성하는 서브넷은 크기가 적절해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="99db3-147">응용 프로그램 게이트웨이 too10 인스턴스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="99db3-148">각 인스턴스는 hello 서브넷에서 IP 주소를 하나 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="99db3-149">서브넷이 너무 적으면 Application Gateway의 크기에 불리한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="99db3-150">2단계</span><span class="sxs-lookup"><span data-stu-id="99db3-150">Step 2</span></span>

<span data-ttu-id="99db3-151">Hello 백 엔드 주소 풀에 사용 되는 주소 범위 toobe를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="99db3-152">3단계</span><span class="sxs-lookup"><span data-stu-id="99db3-152">Step 3</span></span>

<span data-ttu-id="99db3-153">Hello 이전 단계에에서 정의 된 hello 서브넷과 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="99db3-154">4단계</span><span class="sxs-lookup"><span data-stu-id="99db3-154">Step 4</span></span>

<span data-ttu-id="99db3-155">Hello 가상 네트워크 리소스와 서브넷 리소스 toobe hello 다음 단계에에서 사용 되는 검색:</span><span class="sxs-lookup"><span data-stu-id="99db3-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="99db3-156">Hello 프런트 엔드 구성에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="99db3-157">Hello 응용 프로그램 게이트웨이 공용 IP 리소스 toobe를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="99db3-158">이 공용 IP 주소는 다음 단계에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="99db3-159">응용 프로그램 게이트웨이 공용 IP 주소는 도메인 레이블이 정의 사용 하 여 만든 hello 사용을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="99db3-160">도메인 레이블이 동적으로 생성된 공용 IP 주소만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="99db3-161">응용 프로그램 게이트웨이 hello에 대 한 친숙 한 dns 이름, 필요한 경우 좋습니다 toouse CNAME 별칭으로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="99db3-162">응용 프로그램 게이트웨이 구성 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="99db3-163">Hello 응용 프로그램 게이트웨이 만들기 전에 모든 구성 항목 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="99db3-164">hello 다음 단계 hello 구성 항목을 만드는 응용 프로그램 게이트웨이 리소스에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="99db3-165">1단계</span><span class="sxs-lookup"><span data-stu-id="99db3-165">Step 1</span></span>

<span data-ttu-id="99db3-166">이 설정은 구성 서브넷 hello 응용 프로그램 게이트웨이 사용, 응용 프로그램 게이트웨이 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="99db3-167">응용 프로그램 게이트웨이 시작할 때 hello 서브넷 구성에서 IP 주소를 선택 하 고 hello 백 엔드 IP 풀의 네트워크 트래픽을 toohello IP 주소를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="99db3-168">인스턴스마다 하나의 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="99db3-169">2단계</span><span class="sxs-lookup"><span data-stu-id="99db3-169">Step 2</span></span>

<span data-ttu-id="99db3-170">이 설정은 매핑하는 사설 또는 공용 ip 주소 toohello의 프런트 엔드 응용 프로그램 게이트웨이 hello, 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="99db3-171">단계 다음에 나오는 hello hello hello hello 프런트 엔드 IP 구성 사용 하 여 단계를 앞에 공용 IP 주소에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="99db3-172">3단계</span><span class="sxs-lookup"><span data-stu-id="99db3-172">Step 3</span></span>

<span data-ttu-id="99db3-173">Hello 백 엔드 웹 서버의 hello IP 주소와 hello 백 엔드 IP 주소 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="99db3-174">이러한 IP 주소는 hello 프런트 엔드 IP 끝점에서 제공 되는 hello 네트워크 트래픽을 수신 하는 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="99db3-175">사용자 고유의 응용 프로그램의 IP 주소 끝점 IP 주소 tooadd 다음 hello를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="99db3-176">Hello-BackendFqdns 스위치를 사용 하 여 정규화 된 도메인 이름 (FQDN)은 hello 백 엔드 서버에 대 한 ip 주소 대신 유효한 값 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="99db3-177">4단계</span><span class="sxs-lookup"><span data-stu-id="99db3-177">Step 4</span></span>

<span data-ttu-id="99db3-178">Hello hello 공용 IP 끝점에 대 한 프런트 엔드 IP 포트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="99db3-179">이 포트는 최종 사용자에 연결 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="99db3-180">5단계</span><span class="sxs-lookup"><span data-stu-id="99db3-180">Step 5</span></span>

<span data-ttu-id="99db3-181">응용 프로그램 게이트웨이 hello에 대 한 hello 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="99db3-182">이 인증서 사용된 toodecrypt 이며 hello 응용 프로그램 게이트웨이에 hello 트래픽을 다시 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="99db3-183">이 샘플에서는 SSL 연결에 사용 되는 hello 인증서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="99db3-184">hello 인증서.pfx 형식에서 toobe 하며 hello 암호 4 too12 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="99db3-185">6단계</span><span class="sxs-lookup"><span data-stu-id="99db3-185">Step 6</span></span>

<span data-ttu-id="99db3-186">응용 프로그램 게이트웨이 hello에 대 한 hello HTTP 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="99db3-187">Hello 프런트 엔드 ip 구성, 포트 및 SSL 인증서 toouse 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="99db3-188">7단계</span><span class="sxs-lookup"><span data-stu-id="99db3-188">Step 7</span></span>

<span data-ttu-id="99db3-189">Toobe hello SSL에 사용 되는 백 엔드 풀 리소스를 사용 하는 hello 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="99db3-190">hello 기본 프로브 hello에서 hello 공개 키를 가져옵니다 **기본** hello 백 엔드의 IP 주소와 비교 하 여 hello 공개 키 값 toohello 공개 키 값 여기에서 제공 받은에서 SSL 바인딩을 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="99db3-191">hello 검색 된 공개 키는 반드시 hello 의도 한 사이트 toowhich 트래픽 흐름 **경우** hello 백 엔드에서 SNI 및 호스트 헤더를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="99db3-192">의문이 있는 경우 https://127.0.0.1/ hello 백 엔드가 tooconfirm hello에 대 한 사용 되는 인증서에 방문 **기본** SSL 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="99db3-193">이 섹션의 해당 요청에서 사용 하 여 hello의 공개 키입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="99db3-194">HTTPS 바인딩을에서 SNI 및 호스트 헤더를 사용 하는 경우 hello 백 엔드에서 수동 브라우저 요청 toohttps://127.0.0.1/에서 응답 및 인증서를 수신 하지 않습니다 hello 백 엔드에서 기본 SSL 바인딩을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="99db3-195">이렇게 하지 않으면 프로브 실패 하 고 hello 백 엔드 허용 목록 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="99db3-196">이 단계에 제공 된 hello 인증서 hello hello 백 엔드에 hello pfx 인증서의 공개 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="99db3-197">Hello 인증서 (hello 루트 인증서가 아닌) hello 백 엔드 서버에 설치 되어 내보냅니다. CER 서식을 지정 하 고이 단계에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="99db3-198">이 단계 허용 목록을 hello hello 응용 프로그램 게이트웨이 백 엔드가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="99db3-199">8단계</span><span class="sxs-lookup"><span data-stu-id="99db3-199">Step 8</span></span>

<span data-ttu-id="99db3-200">Hello 응용 프로그램 게이트웨이 백 엔드 http 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="99db3-201">Hello toohello http 설정 단계 이전에 업로드 한 hello 인증서를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="99db3-202">9단계</span><span class="sxs-lookup"><span data-stu-id="99db3-202">Step 9</span></span>

<span data-ttu-id="99db3-203">Hello 부하 분산 장치 동작을 구성 하는 부하 분산 장치 라우팅 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="99db3-204">이 예제에서는 기본 라운드 로빈 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="99db3-205">10단계</span><span class="sxs-lookup"><span data-stu-id="99db3-205">Step 10</span></span>

<span data-ttu-id="99db3-206">Hello 인스턴스 크기의 hello 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="99db3-207">hello 사용 가능한 크기는 **표준\_작은**, **표준\_보통**, 및 **표준\_Large**합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="99db3-208">용량을 hello 사용 가능한 값은 1부터 10입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="99db3-209">테스트 목적으로 인스턴스 수 1을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="99db3-210">고 것이 중요에 모든 인스턴스 수의 두 인스턴스가 tooknow hello SLA에서 다루지 않는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="99db3-211">작은 게이트웨이 toobe 개발 테스트에 대 한 프로덕션 환경에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="99db3-212">11단계</span><span class="sxs-lookup"><span data-stu-id="99db3-212">Step 11</span></span>

<span data-ttu-id="99db3-213">응용 프로그램 게이트웨이 hello에 사용 되는 hello SSL 정책 toobe를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="99db3-214">응용 프로그램 게이트웨이 SSL 프로토콜 버전에 대 한 hello 기능 tooset 최소 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="99db3-215">hello 다음 값은 정의할 수 있는 프로토콜 버전의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="99db3-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="99db3-216">**TLSv1_0**</span></span>
* <span data-ttu-id="99db3-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="99db3-217">**TLSv1_1**</span></span>
* <span data-ttu-id="99db3-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="99db3-218">**TLSv1_2**</span></span>

<span data-ttu-id="99db3-219">집합 최소 프로토콜 버전을 너무 hello**TLSv1_2** 수 있도록 **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ S h a 256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, 및 **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** 만 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="99db3-220">Hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="99db3-220">Create hello Application Gateway</span></span>

<span data-ttu-id="99db3-221">이전 단계는 모든 hello를 hello 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="99db3-222">hello 게이트웨이의 hello 만들기는 장기 실행 프로세스.</span><span class="sxs-lookup"><span data-stu-id="99db3-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="99db3-223">기존 Application Gateway의 SSL 프로토콜 버전 제한</span><span class="sxs-lookup"><span data-stu-id="99db3-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="99db3-224">hello 앞의 단계 수행 끝 tooend SSL 사용 하 여 응용 프로그램 만들기 및 특정 SSL 프로토콜 버전을 사용 하지 않도록 설정 하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="99db3-225">hello 다음 예제에서는 비활성화 기존 응용 프로그램 게이트웨이에 특정 SSL 정책을 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="99db3-226">1단계</span><span class="sxs-lookup"><span data-stu-id="99db3-226">Step 1</span></span>

<span data-ttu-id="99db3-227">응용 프로그램 게이트웨이 tooupdate hello를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="99db3-228">2단계</span><span class="sxs-lookup"><span data-stu-id="99db3-228">Step 2</span></span>

<span data-ttu-id="99db3-229">SSL 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-229">Define an SSL policy.</span></span> <span data-ttu-id="99db3-230">다음 예제는 hello에서 TLSv1.0 및 TLSv1.1 해제 되 고 암호 그룹 hello **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, 및  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** hello 뿐 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="99db3-231">3단계</span><span class="sxs-lookup"><span data-stu-id="99db3-231">Step 3</span></span>

<span data-ttu-id="99db3-232">Hello 게이트웨이 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-232">Finally, update hello gateway.</span></span> <span data-ttu-id="99db3-233">것이 중요 한 toonote이 마지막 단계는 장기 실행 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="99db3-234">완료 되 면 최종 tooend SSL hello 응용 프로그램 게이트웨이 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="99db3-235">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="99db3-235">Get application gateway DNS name</span></span>

<span data-ttu-id="99db3-236">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="99db3-237">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="99db3-238">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="99db3-239">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99db3-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="99db3-240">toodo hello 응용 프로그램 게이트웨이 및 연결 된 해당 IP/DNS 이름 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여이 검색 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="99db3-241">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="99db3-242">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99db3-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="99db3-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99db3-243">Next steps</span></span>

<span data-ttu-id="99db3-244">방문 하 여 웹 응용 프로그램을 응용 프로그램 게이트웨이 통해 웹 응용 프로그램 방화벽의 hello 보안을 강화 하는 방법에 대 한 자세한 내용은 [웹 응용 프로그램 방화벽 개요](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="99db3-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
