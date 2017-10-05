---
title: "웹 응용 프로그램 방화벽 구성 - Azure Application Gateway | Microsoft Docs"
description: "이 문서에서는 기존 또는 새 Application Gateway에 웹 응용 프로그램 방화벽을 사용하는 방법을 안내합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="25ce9-103">Azure CLI를 사용하여 새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="25ce9-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25ce9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="25ce9-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="25ce9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25ce9-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="25ce9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="25ce9-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="25ce9-107">웹 응용 프로그램 방화벽을 사용하도록 설정된 응용 프로그램 게이트웨이를 만들거나 기존 응용 프로그램 게이트웨이에 웹 응용 프로그램 방화벽을 추가하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="25ce9-108">Azure Application Gateway의 웹 응용 프로그램 방화벽(WAF)은 SQL 삽입 공격, 사이트 간 스크립팅 공격, 세션 하이재킹 등의 일반적인 웹 기반 공격으로부터 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="25ce9-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="25ce9-110">클라우드 또는 온-프레미스이든 상관없이 서로 다른 서버 간에 장애 조치(Failover), 성능 라우팅 HTTP 요청을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="25ce9-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="25ce9-112">지원되는 기능의 전체 목록을 찾으려면 [Application Gateway에 대한 개요](application-gateway-introduction.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="25ce9-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="25ce9-113">다음 문서에서는 [기존 Application Gateway에 웹 응용 프로그램 방화벽 추가](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용하는 Application Gateway 만들기](#create-an-application-gateway-with-web-application-firewall)에 대해 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![시나리오 이미지][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="25ce9-115">필수 조건: Azure CLI 2.0 설치</span><span class="sxs-lookup"><span data-stu-id="25ce9-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="25ce9-116">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="25ce9-117">WAF 구성 차이</span><span class="sxs-lookup"><span data-stu-id="25ce9-117">WAF configuration differences</span></span>

<span data-ttu-id="25ce9-118">[Azure CLI를 사용하여 Application Gateway 만들기](application-gateway-create-gateway-cli.md)를 읽어 보셨다면 Application Gateway를 만들 때 구성하는 SKU 설정에 대해 알고 계실 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="25ce9-119">WAF는 Application Gateway에 SKU를 구성할 때 정의하는 추가 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="25ce9-120">Application Gateway 자체에서 추가로 변경해야 하는 사항은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="25ce9-121">**설정**</span><span class="sxs-lookup"><span data-stu-id="25ce9-121">**Setting**</span></span> | <span data-ttu-id="25ce9-122">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="25ce9-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="25ce9-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="25ce9-123">**SKU**</span></span> |<span data-ttu-id="25ce9-124">WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="25ce9-125">WAF의 도입으로 두 개의 SKU, 즉 **WAF\_Medium** 및 **WAF\_Large** SKU가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="25ce9-126">소형 Application Gateway에는 WAF가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="25ce9-127">**모드**</span><span class="sxs-lookup"><span data-stu-id="25ce9-127">**Mode**</span></span> | <span data-ttu-id="25ce9-128">이 설정은 WAF 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="25ce9-129">허용되는 값은 **검색** 및 **방지**입니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="25ce9-130">WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="25ce9-131">방지 모드에서는 이벤트를 여전히 기록하지만 공격자가 Application Gateway로부터 403 권한 없음 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="25ce9-132">기존 Application Gateway에 웹 응용 프로그램 방화벽 추가</span><span class="sxs-lookup"><span data-stu-id="25ce9-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="25ce9-133">다음 명령은 기존 표준 응용 프로그램 게이트웨이를 WAF가 활성화된 응용 프로그램 게이트웨이로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="25ce9-134">이 명령은 웹 응용 프로그램 방화벽이 있는 Application Gateway를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="25ce9-135">[Application Gateway 진단](application-gateway-diagnostics.md)을 방문하여 응용 프로그램 게이트웨이에 대한 로그를 보는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="25ce9-136">WAF의 보안 특성상, 주기적으로 로그를 검토하여 웹 응용 프로그램의 보안 상태를 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="25ce9-137">웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="25ce9-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="25ce9-138">다음 명령은 웹 응용 프로그램 방화벽을 사용하여 Application Gateway를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-138">The following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="25ce9-139">기본 웹 응용 프로그램 방화벽 구성을 사용하여 만든 응용 프로그램 게이트웨이는 보호를 위해 CRS 3.0으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="25ce9-140">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="25ce9-140">Get application gateway DNS name</span></span>

<span data-ttu-id="25ce9-141">게이트웨이가 생성되면 다음 단계는 통신에 대한 프런트 엔드를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="25ce9-142">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="25ce9-143">최종 사용자가 Application Gateway를 누를 수 있도록 하려면 CNAME 레코드를 사용하여 Application Gateway의 공용 끝점을 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="25ce9-144">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25ce9-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="25ce9-145">CNAME 기록을 구성하려면 응용 프로그램 게이트웨이에 연결된 PublicIPAddress 요소를 사용하여 응용 프로그램 게이트웨이 및 관련 IP/DNS 이름에 대한 세부 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="25ce9-146">응용 프로그램 게이트웨이의 DNS 이름은 두 개의 웹 응용 프로그램을 이 DNS 이름으로 가리키는 CNAME 레코드를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="25ce9-147">A 레코드를 사용할 경우 응용 프로그램 게이트웨이 다시 시작 시 VIP가 변경될 수 있으므로 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a><span data-ttu-id="25ce9-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25ce9-148">Next steps</span></span>

<span data-ttu-id="25ce9-149">[Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙 사용자 지정](application-gateway-customize-waf-rules-cli.md)을 방문하여 WAF 규칙을 사용자 지정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="25ce9-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
