---
title: "Azure Application Gateway 만들기 - Azure CLI 1.0 | Microsoft Docs"
description: "Resource Manager에서 Azure CLI 1.0을 사용하여 Application Gateway를 만드는 방법 알아보기"
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
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="73891-103">Azure CLI를 사용하여 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="73891-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="73891-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="73891-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="73891-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="73891-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="73891-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="73891-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="73891-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="73891-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="73891-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="73891-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="73891-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="73891-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="73891-110">Azure 응용 프로그램 게이트웨이는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="73891-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="73891-111">클라우드 또는 온-프레미스이든 상관없이 서로 다른 서버 간에 장애 조치(Failover), 성능 라우팅 HTTP 요청을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="73891-112">응용 프로그램 게이트웨이의 응용 프로그램 전달 기능에는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73891-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="73891-113">필수 조건: Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="73891-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="73891-114">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](../xplat-cli-install.md)하고 [Azure에 로그온](../xplat-cli-connect.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="73891-115">Azure 계정이 없는 경우 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="73891-116">[여기서 무료 평가판](../active-directory/sign-up-organization.md)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="73891-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="73891-117">Scenario</span></span>

<span data-ttu-id="73891-118">이 시나리오에서는 Azure Portal을 사용하여 응용 프로그램 게이트웨이를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="73891-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="73891-119">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-119">This scenario will:</span></span>

* <span data-ttu-id="73891-120">두 인스턴스를 사용하여 중간 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73891-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="73891-121">예약된 CIDR 블록으로 10.0.0.0/16을 사용하여 이름이 ContosoVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73891-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="73891-122">CIDR 블록으로 10.0.0.0/28을 사용하는 subnet01이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73891-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="73891-123">초기 배포 중이 아닌 경우 응용 프로그램 게이트웨이를 구성하면 사용자 지정 상태 프로브, 백 엔드 풀 주소, 추가 규칙 등 응용 프로그램 게이트웨이에 대한 추가 구성이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="73891-124">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="73891-124">Before you begin</span></span>

<span data-ttu-id="73891-125">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="73891-126">가상 네트워크를 만들 때 여러 서브넷을 둘 수 있는 충분한 주소 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="73891-127">Application Gateway를 서브넷에 배포한 경우 추가 Application Gateway를 서브넷에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73891-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="73891-128">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="73891-128">Log in to Azure</span></span>

<span data-ttu-id="73891-129">**Microsoft Azure 명령 프롬프트**를 열고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="73891-130">앞의 예제를 입력하면 코드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="73891-131">브라우저에서 https://aka.ms/devicelogin으로 이동하여 로그인 프로세스를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![장치 로그인을 보여 주는 cmd][1]

<span data-ttu-id="73891-133">브라우저에서 받은 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="73891-134">로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-134">You are redirected to a sign-in page.</span></span>

![코드를 입력하는 브라우저][2]

<span data-ttu-id="73891-136">로그인한 코드가 입력된 후 브라우저를 닫아 시나리오를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![성공적으로 로그인][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="73891-138">Resource Manager 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="73891-139">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="73891-139">Create the resource group</span></span>

<span data-ttu-id="73891-140">Application Gateway를 만들기 전에 리소스 그룹이 Application Gateway를 포함하도록 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73891-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="73891-141">다음은 명령을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="73891-142">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="73891-142">Create a virtual network</span></span>

<span data-ttu-id="73891-143">리소스 그룹을 만든 후에 Application Gateway에 가상 네트워크가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="73891-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="73891-144">다음 예제에서 주소 공간은 이전 시나리오 노트에 정의된 대로 10.0.0.0/16이었습니다.</span><span class="sxs-lookup"><span data-stu-id="73891-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="73891-145">서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="73891-145">Create a subnet</span></span>

<span data-ttu-id="73891-146">가상 네트워크를 만든 후에 Application Gateway에 서브넷이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="73891-147">Application Gateway와 동일한 가상 네트워크에서 호스팅된 웹앱을 포함한 Application Gateway를 사용하려는 경우 다른 서브넷을 위해 충분한 공간을 남겨야 합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="73891-148">Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="73891-148">Create the application gateway</span></span>

<span data-ttu-id="73891-149">가상 네트워크와 서브넷을 만들면 Application Gateway에 대한 필수 구성 요소가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="73891-150">또한 이전에 내보낸 .pfx 인증서 및 인증서의 암호는 다음 단계에 필요합니다. 백 엔드에 사용되는 IP 주소는 백 엔드 서버에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="73891-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="73891-151">이 값은 가상 네트워크의 개인 IP, 공용 IP 또는 백 엔드 서버의 정규화된 도메인 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73891-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="73891-152">만드는 동안 제공할 수 있는 매개 변수 목록의 경우 **azure network application-gateway create --help** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73891-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="73891-153">이 예제에서는 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대한 기본 설정으로 기본 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="73891-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="73891-154">프로비전에 성공하면 배포에 맞게 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73891-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="73891-155">이전 단계에서 백 엔드 풀로 정의된 웹 응용 프로그램이 이미 있는 경우 만들어지면 부하 분산이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="73891-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73891-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="73891-156">Next steps</span></span>

<span data-ttu-id="73891-157">[사용자 지정 상태 프로브 만들기](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="73891-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="73891-158">[SSL 오프로드 구성](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="73891-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
