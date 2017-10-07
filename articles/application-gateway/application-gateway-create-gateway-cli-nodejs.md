---
title: "Azure 응용 프로그램 게이트웨이-aaaCreate Azure CLI 1.0 | Microsoft Docs"
description: "Toocreate 응용 프로그램 게이트웨이 사용 하 여 리소스 관리자의 Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="4917b-103">Hello Azure CLI를 사용 하 여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="4917b-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4917b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4917b-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="4917b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="4917b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="4917b-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="4917b-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="4917b-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="4917b-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="4917b-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4917b-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="4917b-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4917b-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="4917b-110">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="4917b-111">장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="4917b-112">응용 프로그램 게이트웨이 같은 응용 프로그램 배달 기능 hello: HTTP 균형 조정, 쿠키 기반 세션 선호도 및 오프 로드 (SECURE Sockets Layer), 사용자 지정 상태 프로브를 로드 및 여러 사이트에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="4917b-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="4917b-113">필수 구성 요소: hello Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="4917b-114">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](../xplat-cli-install.md) 너무 필요[tooAzure 로그온](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="4917b-115">Azure 계정이 없는 경우 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="4917b-116">[여기서 무료 평가판](../active-directory/sign-up-organization.md)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="4917b-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="4917b-117">Scenario</span></span>

<span data-ttu-id="4917b-118">이 시나리오에서는 사용 하 여 응용 프로그램 게이트웨이 toocreate Azure 포털을 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="4917b-119">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-119">This scenario will:</span></span>

* <span data-ttu-id="4917b-120">두 인스턴스를 사용하여 중간 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="4917b-121">예약된 CIDR 블록으로 10.0.0.0/16을 사용하여 이름이 ContosoVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="4917b-122">CIDR 블록으로 10.0.0.0/28을 사용하는 subnet01이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="4917b-123">사용자 지정 상태를 포함 하 여 hello 응용 프로그램 게이트웨이 추가 구성 프로브를 통해 백 엔드 풀 주소 및 추가 규칙 hello 응용 프로그램 게이트웨이 구성한 후와 초기 배포 중이 아니라 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4917b-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4917b-124">Before you begin</span></span>

<span data-ttu-id="4917b-125">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="4917b-126">가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="4917b-127">추가 응용 프로그램 게이트웨이 수 toobe 추가 응용 프로그램 게이트웨이 tooa 서브넷을 배포한 후 toohello 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="4917b-128">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="4917b-128">Log in tooAzure</span></span>

<span data-ttu-id="4917b-129">열기 hello **Microsoft Azure 명령 프롬프트**, 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4917b-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="4917b-130">앞 예제는 hello를 입력 한 후에 코드가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="4917b-131">Toohttps://aka.ms/devicelogin 브라우저 toocontinue hello 로그인 프로세스에서를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![장치 로그인을 보여 주는 cmd][1]

<span data-ttu-id="4917b-133">Hello 브라우저에서 hello 받은 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="4917b-134">로그인 페이지로 리디렉션된 tooa 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-134">You are redirected tooa sign-in page.</span></span>

![브라우저 tooenter 코드][2]

<span data-ttu-id="4917b-136">Hello 코드 입력 되 면 로그인, 닫기 hello 브라우저 toocontinue hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![성공적으로 로그인][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="4917b-138">TooResource 관리자 모드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="4917b-139">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="4917b-139">Create hello resource group</span></span>

<span data-ttu-id="4917b-140">Hello 응용 프로그램 게이트웨이 만들기 전에 리소스 그룹 toocontain hello 응용 프로그램 게이트웨이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="4917b-141">hello 다음 hello 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="4917b-142">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="4917b-142">Create a virtual network</span></span>

<span data-ttu-id="4917b-143">Hello 리소스 그룹을 만든 후 hello 응용 프로그램 게이트웨이 가상 네트워크가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="4917b-144">다음 예제는 hello, hello 주소 공간으로 hello 시나리오 노트 앞에 정의 된 대로 10.0.0.0/16 였습니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="4917b-145">서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="4917b-145">Create a subnet</span></span>

<span data-ttu-id="4917b-146">Hello 가상 네트워크를 만든 후 hello 응용 프로그램 게이트웨이 서브넷 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="4917b-147">포함 된 경우 하려는 웹 앱과 toouse 응용 프로그램 게이트웨이 호스트 hello에 동일한 가상 네트워크에 hello 응용 프로그램 게이트웨이, 다른 서브넷에 대 한 충분 한 공간이 있는지 tooleave 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="4917b-148">Hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="4917b-148">Create hello application gateway</span></span>

<span data-ttu-id="4917b-149">Hello 가상 네트워크 및 서브넷을 만든 후 hello hello 응용 프로그램 게이트웨이에 대 한 필수 조건을 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="4917b-150">또한 이전에 내보낸된.pfx 인증서와 hello 인증서의 암호를 hello는 hello 단계 다음에 필요한: hello 백 엔드에 사용 되는 hello IP 주소는 백 엔드 서버에 대 한 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="4917b-151">이러한 값 hello 가상 네트워크, 공용 ip 또는 백 엔드 서버에 대 한 정규화 된 도메인 이름을 개인 Ip 중 하나가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="4917b-152">Hello 다음 명령을 실행 하는 생성 중에 제공 될 수 있는 매개 변수 목록은: **azure 네트워크 응용 프로그램 게이트웨이 만들기-도움말**합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="4917b-153">이 예제는 hello 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대 한 기본 설정으로 기본 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="4917b-154">Hello를 프로 비전 하는 것은 성공 후 배포 설정을 toosuit 이러한을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="4917b-155">이전 단계를 만든 후 hello hello 백 엔드 풀과 정의 된 웹 응용 프로그램에 이미 있는 경우 부하 분산 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4917b-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4917b-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4917b-156">Next steps</span></span>

<span data-ttu-id="4917b-157">사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4917b-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="4917b-158">어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4917b-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
