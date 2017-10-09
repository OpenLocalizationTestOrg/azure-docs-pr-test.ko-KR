---
title: "aaaConfigure 웹 응용 프로그램 방화벽 Azure 응용 프로그램 게이트웨이 | Microsoft Docs"
description: "이 문서는 어떻게 toostart 웹를 사용 하는 기존 또는 새 응용 프로그램 게이트웨이에 응용 프로그램 방화벽에 지침을 제공 합니다."
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
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="1813f-103">Azure CLI를 사용하여 새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="1813f-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1813f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1813f-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="1813f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1813f-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="1813f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1813f-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="1813f-107">웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 하거나 웹 응용 프로그램 방화벽 toocreate 응용 프로그램 게이트웨이 사용 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="1813f-108">hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="1813f-109">Azure Application Gateway는 계층 7 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="1813f-110">장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="1813f-111">Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="1813f-112">지원 되는 기능의 전체 목록은 toofind 방문: [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="1813f-113">hello 다음 문서에서는 어떻게 너무[추가 웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들](#create-an-application-gateway-with-web-application-firewall)합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![시나리오 이미지][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="1813f-115">필수 구성 요소: hello Azure CLI 2.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="1813f-116">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="1813f-117">WAF 구성 차이</span><span class="sxs-lookup"><span data-stu-id="1813f-117">WAF configuration differences</span></span>

<span data-ttu-id="1813f-118">읽기 있으면 [Azure CLI 응용 프로그램 게이트웨이 만들기](application-gateway-create-gateway-cli.md), 응용 프로그램 게이트웨이 만들 때 hello SKU 설정 tooconfigure 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="1813f-119">WAF는 hello SKU 응용 프로그램 게이트웨이를 구성 하는 경우 추가 설정을 toodefine를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="1813f-120">추가 변경 된 사항이 없습니다 hello 응용 프로그램 게이트웨이 자체에서 설정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="1813f-121">**설정**</span><span class="sxs-lookup"><span data-stu-id="1813f-121">**Setting**</span></span> | <span data-ttu-id="1813f-122">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="1813f-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="1813f-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="1813f-123">**SKU**</span></span> |<span data-ttu-id="1813f-124">WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="1813f-125">WAF의 hello 도입으로 두 개의 추가 Sku는 **WAF\_보통** 및 **WAF\_Large**합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="1813f-126">소형 Application Gateway에는 WAF가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="1813f-127">**모드**</span><span class="sxs-lookup"><span data-stu-id="1813f-127">**Mode**</span></span> | <span data-ttu-id="1813f-128">이 설정은 WAF의 hello 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="1813f-129">허용되는 값은 **검색** 및 **방지**입니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="1813f-130">WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="1813f-131">방지 모드에서 이벤트는 여전히 로깅되지만 hello 공격자가 hello 응용 프로그램 게이트웨이에서 403 권한 없는 응답을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="1813f-132">웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="1813f-133">hello 명령 변경 내용은 기존 표준 응용 프로그램 게이트웨이 tooa WAF 사용된 응용 프로그램 게이트웨이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="1813f-134">이 명령은 웹 응용 프로그램 방화벽으로 hello 응용 프로그램 게이트웨이 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="1813f-135">방문 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md) toounderstand tooview 응용 프로그램 게이트웨이 기록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="1813f-136">WAF에서는 toohello 보안 이기 때문 로그 필요 toobe toounderstand 웹 응용 프로그램의 보안 상태를 hello 정기적으로 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="1813f-137">웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="1813f-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="1813f-138">다음 명령을 hello 웹 응용 프로그램 방화벽이 설치 된 응용 프로그램 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-138">hello following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="1813f-139">Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="1813f-140">응용 프로그램 게이트웨이 DNS 이름 가져오기</span><span class="sxs-lookup"><span data-stu-id="1813f-140">Get application gateway DNS name</span></span>

<span data-ttu-id="1813f-141">Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="1813f-142">공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="1813f-143">tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="1813f-144">[Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1813f-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="1813f-145">CNAME 레코드 tooconfigure hello 응용 프로그램 게이트웨이 및 연결 된 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여 해당 IP/DNS 이름 세부 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="1813f-146">hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="1813f-147">A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1813f-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1813f-148">Next steps</span></span>

<span data-ttu-id="1813f-149">Toocustomize WAF 방문 하 여 규칙의 방식에 대해 알아봅니다: [hello Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정](application-gateway-customize-waf-rules-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1813f-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
