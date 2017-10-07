---
title: "aaaHosting 여러 개의 사이트에서 Azure 응용 프로그램 게이트웨이 | Microsoft Docs"
description: "이 페이지는 hello 응용 프로그램 게이트웨이 멀티 사이트 지원의 개요를 제공합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>응용 프로그램 게이트웨이 다중 사이트 호스팅

Tooconfigure 두 개 이상의 hello에 하나의 웹 응용 프로그램을 통해 여러 사이트 호스팅 응용 프로그램 게이트웨이 동일 합니다. 이 기능 too20 웹 사이트 tooone 응용 프로그램 게이트웨이를 추가 하 여 배포에 대 한 보다 효율적인 토폴로지 tooconfigure가 있습니다. 각 웹 사이트를 전송할 수 tooits 백 엔드 풀을 소유 합니다. 다음 예제는 hello, 응용 프로그램 게이트웨이 contoso.com 및 fabrikam.com ContosoServerPool 및 FabrikamServerPool 라는 두 개의 백 엔드 서버 풀에서에 대 한 트래픽을 처리 합니다.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> 규칙은 hello 포털에 나열 된 hello 순서로 처리 됩니다. 것이 권장된 사항임 tooconfigure 다중 사이트 수신기 첫 번째 이전 tooconfiguring 기본 수신기 합니다.  이렇게 하면 해당 트래픽을 가져옵니다 라우트된 toohello 다시 종료 합니다. 기본 수신기가 먼저 나열되고 들어오는 요청과 일치하면 해당 수신기에서 처리합니다.

Http://contoso.com에 대 한 요청 라우트된 tooContosoServerPool 않으며 http://fabrikam.com 라우트된 tooFabrikamServerPool 합니다.

마찬가지로 두 하위 도메인의 동일한 부모 도메인에서 호스팅할 수 hello hello 동일한 응용 프로그램 게이트웨이 배포 합니다. 하위 도메인을 사용하는 예제에는 단일 Application Gateway 배포에 호스팅되는 http://blog.contoso.com 및 http://app.contoso.com이 포함됩니다.

## <a name="host-headers-and-server-name-indication-sni"></a>호스트 헤더 및 SNI(서버 이름 표시)

동일한 hello에 호스트 하는 여러 사이트를 사용 하기 위한 세 가지 일반적인 메커니즘은 인프라입니다.

1. 여러 웹 응용 프로그램 각각을 고유한 IP 주소에서 호스트합니다.
2. 사용 하 여 호스트 이름을 toohost hello에 여러 웹 응용 프로그램 같은 IP 주소입니다.
3. 사용 하 여 서로 다른 포트 toohost hello에 여러 웹 응용 프로그램 같은 IP 주소입니다.

현재 응용 프로그램 게이트웨이는 단일 공용 IP 주소를 사용하여 트래픽을 수신합니다. 따라서 고유한 IP 주소로 여러 응용 프로그램을 지원하는 기능은 현재 지원되지 않습니다. 응용 프로그램 게이트웨이 여러 응용 프로그램을 호스팅할 각 서로 다른 포트에서 수신 하지만이 시나리오 hello 응용 프로그램 tooaccept 트래픽에 비표준 포트에서 필요 하 고 하지 적절된 한 구성 인 경우가 많습니다. 응용 프로그램 게이트웨이 HTTP 1.1 사용 한 웹 사이트에 둘 이상의 호스트 헤더 toohost hello 동일한 공용 IP 주소 및 포트. 응용 프로그램 게이트웨이에서 호스팅되는 hello 사이트 지원 SSL 오프 로드를 서버 이름 표시 (SNI) TLS 확장명이 수도 있습니다. 이 시나리오는 HTTP/1.1 및 TLS 확장 6066 RFC에에서 정의 된 대로 해당 hello 클라이언트 브라우저 및 백 엔드 웹 팜에 지원 해야 의미 합니다.

## <a name="listener-configuration-element"></a>수신기 구성 요소

구성 요소는 기존 HTTPListener 응용 프로그램 게이트웨이 tooroute 트래픽 tooappropriate 백 엔드 풀에서 사용 되는 toosupport 호스트 이름 및 서버 이름 표시 요소를 강화 합니다. hello 다음 코드 예제는 서식 파일에서 HttpListeners 요소의 hello 조각입니다.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

방문할 수 있는 [여러 사이트 호스팅 사용 하 여 리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) 최종 tooend 템플릿 기반 배포에 대 한 합니다.

## <a name="routing-rule"></a>라우팅 규칙

Hello 라우팅 규칙에 필요한 변경 되지 않았습니다. 라우팅 규칙 선택 toobe tootie hello 적절 한 사이트 수신기 toohello 해당 백 엔드 주소 풀을 계속 해야 '기본' hello 합니다.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>다음 단계

여러 사이트 호스팅에 대 한 학습 한 후 전환 너무[여러 사이트 호스팅 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate 하나의 웹 응용 프로그램 보다 더 많은 기능 toosupport 응용 프로그램 게이트웨이 합니다.

