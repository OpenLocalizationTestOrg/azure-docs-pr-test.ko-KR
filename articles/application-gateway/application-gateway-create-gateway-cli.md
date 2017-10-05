---
title: "Azure Application Gateway 만들기 - Azure CLI 2.0 | Microsoft Docs"
description: "Resource Manager에서 Azure CLI 2.0을 사용하여 Application Gateway를 만드는 방법 알아보기"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="bd5f3-103">Azure CLI 2.0을 사용하여 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5f3-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd5f3-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd5f3-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="bd5f3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd5f3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="bd5f3-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd5f3-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="bd5f3-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="bd5f3-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="bd5f3-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bd5f3-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="bd5f3-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bd5f3-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="bd5f3-110">Application Gateway는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 7계층 부하 분산 기능을 제공하는 전용 가상 어플라이언스입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bd5f3-111">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="bd5f3-111">CLI versions to complete the task</span></span>

<span data-ttu-id="bd5f3-112">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="bd5f3-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="bd5f3-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="bd5f3-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="bd5f3-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="bd5f3-115">필수 조건: Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="bd5f3-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="bd5f3-116">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="bd5f3-117">Azure 계정이 없는 경우 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="bd5f3-118">[여기서 무료 평가판](../active-directory/sign-up-organization.md)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="bd5f3-119">시나리오</span><span class="sxs-lookup"><span data-stu-id="bd5f3-119">Scenario</span></span>

<span data-ttu-id="bd5f3-120">이 시나리오에서는 Azure Portal을 사용하여 응용 프로그램 게이트웨이를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="bd5f3-121">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-121">This scenario will:</span></span>

* <span data-ttu-id="bd5f3-122">두 인스턴스를 사용하여 중간 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="bd5f3-123">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 AdatumAppGatewayVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="bd5f3-124">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="bd5f3-125">초기 배포 중이 아닌 경우 응용 프로그램 게이트웨이를 구성하면 사용자 지정 상태 프로브, 백 엔드 풀 주소, 추가 규칙 등 응용 프로그램 게이트웨이에 대한 추가 구성이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bd5f3-126">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="bd5f3-126">Before you begin</span></span>

<span data-ttu-id="bd5f3-127">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="bd5f3-128">가상 네트워크를 만들 때 여러 서브넷을 둘 수 있는 충분한 주소 공간이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="bd5f3-129">Application Gateway를 서브넷에 배포한 경우 추가 Application Gateway를 서브넷에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="bd5f3-130">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="bd5f3-130">Log in to Azure</span></span>

<span data-ttu-id="bd5f3-131">**Microsoft Azure 명령 프롬프트**를 열고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="bd5f3-132">aka.ms/devicelogin에서 코드를 입력해야 하는 장치 로그인에 대한 스위치 없이 `az login`을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="bd5f3-133">앞의 예제를 입력하면 코드가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="bd5f3-134">브라우저에서 https://aka.ms/devicelogin으로 이동하여 로그인 프로세스를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![장치 로그인을 보여 주는 cmd][1]

<span data-ttu-id="bd5f3-136">브라우저에서 받은 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="bd5f3-137">로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-137">You are redirected to a sign-in page.</span></span>

![코드를 입력하는 브라우저][2]

<span data-ttu-id="bd5f3-139">로그인한 코드가 입력된 후 브라우저를 닫아 시나리오를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![성공적으로 로그인][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="bd5f3-141">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5f3-141">Create the resource group</span></span>

<span data-ttu-id="bd5f3-142">Application Gateway를 만들기 전에 리소스 그룹이 Application Gateway를 포함하도록 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="bd5f3-143">다음은 명령을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="bd5f3-144">Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="bd5f3-144">Create the application gateway</span></span>

<span data-ttu-id="bd5f3-145">백 엔드에 사용되는 IP 주소는 백 엔드 서버에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="bd5f3-146">이 값은 가상 네트워크의 개인 IP, 공용 IP 또는 백 엔드 서버의 정규화된 도메인 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="bd5f3-147">다음 예제에서는 http 설정, 포트 및 규칙에 대한 추가 구성 설정을 사용하여 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

<span data-ttu-id="bd5f3-148">앞의 예제에서는 응용 프로그램 게이트웨이를 만드는 동안 필요하지 않은 많은 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="bd5f3-149">다음 코드 예제는 필요한 정보를 사용하여 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-149">The following code example creates an application gateway with the required information.</span></span>

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> <span data-ttu-id="bd5f3-150">만드는 동안 제공할 수 있는 매개 변수 목록의 경우 `az network application-gateway create --help` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="bd5f3-151">이 예제에서는 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대한 기본 설정으로 기본 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="bd5f3-152">프로비전에 성공하면 배포에 맞게 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="bd5f3-153">이전 단계에서 백 엔드 풀로 정의된 웹 응용 프로그램이 이미 있는 경우 만들어지면 부하 분산이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="bd5f3-154">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="bd5f3-154">Get application gateway DNS name</span></span>

<span data-ttu-id="bd5f3-155">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="bd5f3-156">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="bd5f3-157">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="bd5f3-158">[Azure에서 사용자 지정 도메인 이름 구성](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="bd5f3-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="bd5f3-159">별칭을 구성하려면 응용 프로그램 게이트웨이에 연결된 PublicIPAddress 요소를 사용하여 응용 프로그램 게이트웨이 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="bd5f3-160">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="bd5f3-161">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a><span data-ttu-id="bd5f3-162">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="bd5f3-162">Delete all resources</span></span>

<span data-ttu-id="bd5f3-163">이 문서에서 만든 모든 리소스를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bd5f3-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="bd5f3-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bd5f3-164">Next steps</span></span>

<span data-ttu-id="bd5f3-165">[사용자 지정 상태 프로브 만들기](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="bd5f3-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="bd5f3-166">[SSL 오프로드 구성](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="bd5f3-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
