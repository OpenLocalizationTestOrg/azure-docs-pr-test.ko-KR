---
title: "Azure 응용 프로그램 게이트웨이-aaaCreate Azure CLI 2.0 | Microsoft Docs"
description: "방법을 사용 하 여 응용 프로그램 게이트웨이 toocreate hello Azure CLI 2.0 리소스 관리자에 알아봅니다."
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
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="3a417-103">Hello Azure CLI 2.0을 사용 하 여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3a417-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a417-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3a417-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="3a417-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a417-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="3a417-106">Azure 클래식 PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a417-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="3a417-107">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3a417-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="3a417-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3a417-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="3a417-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3a417-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="3a417-110">Application Gateway는 ADC(응용 프로그램 배달 컨트롤러)를 서비스로 제공하여 다양한 7계층 부하 분산 기능을 제공하는 전용 가상 어플라이언스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3a417-111">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="3a417-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="3a417-112">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="3a417-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="3a417-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="3a417-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="3a417-115">필수 구성 요소: hello Azure CLI 2.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="3a417-116">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="3a417-117">Azure 계정이 없는 경우 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="3a417-118">[여기서 무료 평가판](../active-directory/sign-up-organization.md)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="3a417-119">시나리오</span><span class="sxs-lookup"><span data-stu-id="3a417-119">Scenario</span></span>

<span data-ttu-id="3a417-120">이 시나리오에서는 사용 하 여 응용 프로그램 게이트웨이 toocreate Azure 포털을 hello 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="3a417-121">이 시나리오에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-121">This scenario will:</span></span>

* <span data-ttu-id="3a417-122">두 인스턴스를 사용하여 중간 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="3a417-123">예약된 CIDR 블록이 10.0.0.0/16이고 이름이 AdatumAppGatewayVNET인 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="3a417-124">CIDR 블록으로 10.0.0.0/28을 사용하는 Appgatewaysubnet이라고 하는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="3a417-125">사용자 지정 상태를 포함 하 여 hello 응용 프로그램 게이트웨이 추가 구성 프로브를 통해 백 엔드 풀 주소 및 추가 규칙 hello 응용 프로그램 게이트웨이 구성한 후와 초기 배포 중이 아니라 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a417-126">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="3a417-126">Before you begin</span></span>

<span data-ttu-id="3a417-127">Azure Application Gateway에는 자체 서브넷이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="3a417-128">가상 네트워크를 만들 때 상태로 두고 충분 한 주소 공간 toohave 여러 서브넷을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="3a417-129">응용 프로그램 게이트웨이 tooa 서브넷을 배포한 후 추가로 응용 프로그램 게이트웨이 toohello 서브넷을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="3a417-130">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="3a417-130">Log in tooAzure</span></span>

<span data-ttu-id="3a417-131">열기 hello **Microsoft Azure 명령 프롬프트**, 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a417-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="3a417-132">사용할 수도 있습니다 `az login` aka.ms/devicelogin에서 코드를 입력 해야 하는 장치 로그인에 대 한 hello 스위치 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="3a417-133">앞 예제는 hello를 입력 한 후에 코드가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="3a417-134">Toohttps://aka.ms/devicelogin 브라우저 toocontinue hello 로그인 프로세스에서를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![장치 로그인을 보여 주는 cmd][1]

<span data-ttu-id="3a417-136">Hello 브라우저에서 hello 받은 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="3a417-137">로그인 페이지로 리디렉션된 tooa 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-137">You are redirected tooa sign-in page.</span></span>

![브라우저 tooenter 코드][2]

<span data-ttu-id="3a417-139">Hello 코드 입력 되 면 로그인, 닫기 hello 브라우저 toocontinue hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![성공적으로 로그인][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="3a417-141">Hello 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3a417-141">Create hello resource group</span></span>

<span data-ttu-id="3a417-142">Hello 응용 프로그램 게이트웨이 만들기 전에 리소스 그룹 toocontain hello 응용 프로그램 게이트웨이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="3a417-143">hello 다음 hello 명령을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="3a417-144">Hello 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="3a417-144">Create hello application gateway</span></span>

<span data-ttu-id="3a417-145">hello 백 엔드에 사용 되는 hello IP 주소는 백 엔드 서버에 대 한 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="3a417-146">이러한 값 hello 가상 네트워크, 공용 ip 또는 백 엔드 서버에 대 한 정규화 된 도메인 이름을 개인 Ip 중 하나가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="3a417-147">hello 다음 예제에서는 응용 프로그램 게이트웨이 http 설정, 포트 및 규칙에 대 한 추가 구성 설정을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3a417-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="3a417-148">hello 앞의 예제를 보여 줍니다 hello 응용 프로그램 게이트웨이 만드는 동안 필요 하지 않은 많은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="3a417-149">다음 코드 예제는 hello hello 필요한 정보와 함께 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-149">hello following code example creates an application gateway with hello required information.</span></span>

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
> <span data-ttu-id="3a417-150">다음 명령을 실행 하는 생성 hello 하는 동안 제공 될 수 있는 매개 변수 목록은: `az network application-gateway create --help`합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="3a417-151">이 예제는 hello 수신기, 백 엔드 풀, 백 엔드 http 설정 및 규칙에 대 한 기본 설정으로 기본 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="3a417-152">Hello를 프로 비전 하는 것은 성공 후 배포 설정을 toosuit 이러한을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="3a417-153">이전 단계를 만든 후 hello hello 백 엔드 풀과 정의 된 웹 응용 프로그램에 이미 있는 경우 부하 분산 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="3a417-154">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a417-154">Get application gateway DNS name</span></span>

<span data-ttu-id="3a417-155">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="3a417-156">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="3a417-157">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="3a417-158">[Azure에서 사용자 지정 도메인 이름 구성](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3a417-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="3a417-159">별칭을 tooconfigure hello 응용 프로그램 게이트웨이 및 연결 된 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여 해당 IP/DNS 이름 세부 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="3a417-160">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="3a417-161">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a417-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="3a417-162">모든 리소스 삭제</span><span class="sxs-lookup"><span data-stu-id="3a417-162">Delete all resources</span></span>

<span data-ttu-id="3a417-163">이 문서에서는 다음 단계 완료 hello에서에서 만든 모든 리소스를 toodelete:</span><span class="sxs-lookup"><span data-stu-id="3a417-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="3a417-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a417-164">Next steps</span></span>

<span data-ttu-id="3a417-165">사용자 지정 상태 toocreate 방문 하 여 조사 하는 방법에 대해 알아봅니다 [만들 사용자 지정 상태 프로브](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3a417-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="3a417-166">어떻게 tooconfigure SSL 오프 로딩 및 take hello 비용이 많이 드는 SSL 암호 해독 해제 하면 웹 서버 방문 하 여 자세한 [SSL 오프 로드 구성](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="3a417-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
