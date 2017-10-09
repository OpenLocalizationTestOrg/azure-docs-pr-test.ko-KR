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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Azure CLI를 사용하여 새 또는 기존 Application Gateway에 웹 응용 프로그램 방화벽 구성

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 하거나 웹 응용 프로그램 방화벽 toocreate 응용 프로그램 게이트웨이 사용 하는 방법을 알아봅니다.

hello 웹 응용 프로그램 방화벽 (WAF)에서 Azure 응용 프로그램 게이트웨이 SQL 삽입 같은 일반적인 웹 기반 공격, 사이트 간 스크립팅 공격이 및 도용 하는 세션에서 웹 응용 프로그램을 보호합니다.

Azure Application Gateway는 계층 7 부하 분산 장치입니다. 장애 조치의 경우 서로 다른 서버 간에 HTTP 요청 성능 라우팅 hello 클라우드 또는 온-프레미스에 있는지 여부를 제공 합니다. Application Gateway는 HTTP 부하 분산, 쿠키 기반 세션 선호도, SSL(Secure Sockets Layer) 오프로드, 사용자 지정 상태 프로브, 다중 사이트 지원 및 기타 여러 기능을 포함하여 다양한 ADC(Application Delivery Controller)를 제공합니다. 지원 되는 기능의 전체 목록은 toofind 방문: [응용 프로그램 게이트웨이 개요](application-gateway-introduction.md)합니다.

hello 다음 문서에서는 어떻게 너무[추가 웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이](#add-web-application-firewall-to-an-existing-application-gateway) 및 [웹 응용 프로그램 방화벽을 사용 하 여 응용 프로그램 게이트웨이 만들](#create-an-application-gateway-with-web-application-firewall)합니다.

![시나리오 이미지][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>필수 구성 요소: hello Azure CLI 2.0를 설치 합니다.

이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.

## <a name="waf-configuration-differences"></a>WAF 구성 차이

읽기 있으면 [Azure CLI 응용 프로그램 게이트웨이 만들기](application-gateway-create-gateway-cli.md), 응용 프로그램 게이트웨이 만들 때 hello SKU 설정 tooconfigure 이해 합니다. WAF는 hello SKU 응용 프로그램 게이트웨이를 구성 하는 경우 추가 설정을 toodefine를 제공 합니다. 추가 변경 된 사항이 없습니다 hello 응용 프로그램 게이트웨이 자체에서 설정한 합니다.

| **설정** | **세부 정보**
|---|---|
|**SKU** |WAF가 없는 일반 Application Gateway는 **Standard\_Small**, **Standard\_Medium** 및 **Standard\_Large** 크기를 지원합니다. WAF의 hello 도입으로 두 개의 추가 Sku는 **WAF\_보통** 및 **WAF\_Large**합니다. 소형 Application Gateway에는 WAF가 지원되지 않습니다.|
|**모드** | 이 설정은 WAF의 hello 모드입니다. 허용되는 값은 **검색** 및 **방지**입니다. WAF를 검색 모드로 설정하면 모든 위협이 로그 파일에 저장됩니다. 방지 모드에서 이벤트는 여전히 로깅되지만 hello 공격자가 hello 응용 프로그램 게이트웨이에서 403 권한 없는 응답을 받습니다.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>웹 응용 프로그램 방화벽 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.

hello 명령 변경 내용은 기존 표준 응용 프로그램 게이트웨이 tooa WAF 사용된 응용 프로그램 게이트웨이 수행 합니다.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

이 명령은 웹 응용 프로그램 방화벽으로 hello 응용 프로그램 게이트웨이 업데이트합니다. 방문 [응용 프로그램 게이트웨이 진단](application-gateway-diagnostics.md) toounderstand tooview 응용 프로그램 게이트웨이 기록 하는 방법입니다. WAF에서는 toohello 보안 이기 때문 로그 필요 toobe toounderstand 웹 응용 프로그램의 보안 상태를 hello 정기적으로 검토 합니다.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>웹 응용 프로그램 방화벽이 있는 Application Gateway 만들기

다음 명령을 hello 웹 응용 프로그램 방화벽이 설치 된 응용 프로그램 게이트웨이 만듭니다.

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
> Hello 기본 웹 응용 프로그램 방화벽 구성을 사용 하 여 만든 응용 프로그램 게이트웨이 보호 기능에 대 한 CRS 3.0으로 구성 됩니다.

## <a name="get-application-gateway-dns-name"></a>응용 프로그램 게이트웨이 DNS 이름 가져오기

Hello 게이트웨이가 생성 된 hello 다음 단계는 통신을 위해 tooconfigure hello 프런트 엔드입니다. 공용 IP를 사용할 때 Application Gateway는 식별 이름이 아닌 동적으로 할당된 DNS 이름이 필요합니다. tooensure 최종 사용자가 hello 응용 프로그램 게이트웨이 적중할 수, CNAME 레코드를 사용 하는 toopoint toohello hello 응용 프로그램 게이트웨이의 공용 끝점 수 있습니다. [Azure에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md). CNAME 레코드 tooconfigure hello 응용 프로그램 게이트웨이 및 연결 된 hello PublicIPAddress 요소 toohello 연결 된 응용 프로그램 게이트웨이 사용 하 여 해당 IP/DNS 이름 세부 정보를 검색 합니다. hello 응용 프로그램 게이트웨이 DNS 이름이 사용 되는 toocreate CNAME 레코드는 포인트 hello 두 웹 응용 프로그램 toothis DNS 이름 이어야 합니다. A 레코드의 hello 사용 hello VIP는 응용 프로그램 게이트웨이 다시 시작으로 변동 될 수 있으므로 권장 되지 않습니다.

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

## <a name="next-steps"></a>다음 단계

Toocustomize WAF 방문 하 여 규칙의 방식에 대해 알아봅니다: [hello Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정](application-gateway-customize-waf-rules-cli.md)합니다.

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
