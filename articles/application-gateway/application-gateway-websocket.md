---
title: "Azure 응용 프로그램 게이트웨이에서 aaaWebSocket 지원 | Microsoft Docs"
description: "이 페이지는 응용 프로그램 게이트웨이 WebSocket 지원 hello에 대 한 개요를 제공합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Application Gateway의 WebSocket 지원 개요

Application Gateway는 모든 게이트웨이 크기에 WebSocket에 대한 네이티브 지원을 제공합니다. 사용자 구성 가능 설정 tooselectively 사용 또는 사용 안 함 WebSocket 지원 없을 합니다. 

[RFC6455](https://tools.ietf.org/html/rfc6455)에서 표준화된 WebSocket 프로토콜을 사용하면 장기 실행 TCP 연결을 통해 서버와 클라이언트 간의 전이중 통신을 수행할 수 있습니다. 이 기능을 좀 더 대화형 hello 웹 서버와 양방향에 필요한 HTTP 기반 구현으로 폴링에 대 한 hello 필요 없이 될 수 있는 hello 클라이언트 간의 통신을 위해 사용 합니다. WebSocket에 HTTP와 달리 오버 헤드가 낮은 및 수 재사용 hello 동일한 리소스의 보다 효율적인 사용으로 인해 발생 하는 여러 요청/응답에 대 한 TCP 연결 합니다. WebSocket 프로토콜 기존의 HTTP 포트 80 및 443의 디자인 된 toowork은입니다.

포트 80 또는 443 tooreceive WebSocket 트래픽에서 표준 HTTP 수신기를 사용 하 여 계속할 수 있습니다. WebSocket 트래픽이 방향이 지정 된 toohello WebSocket 백 엔드 서버 hello 적절 한 백 엔드 풀을 사용 하 여 응용 프로그램 게이트웨이 규칙에 지정 된 대로 사용 됩니다. hello 백 엔드 서버 hello에 설명 되어 있는 toohello 응용 프로그램 게이트웨이 프로브 응답 해야 [상태 프로브 개요](application-gateway-probe-overview.md) 섹션. 응용 프로그램 게이트웨이 상태 프로브는 HTTP/HTTPS 전용입니다. 각 백 엔드 서버 응용 프로그램 게이트웨이 tooroute WebSocket 트래픽 toohello 서버에 대 한 tooHTTP 프로브 응답 해야 합니다.

## <a name="listener-configuration-element"></a>수신기 구성 요소

기존 HTTP 수신기 사용된 toosupport WebSocket 트래픽 될 수 있습니다. hello 다음은 예제 서식 파일에서 httpListeners 요소 조각입니다. HTTP 및 HTTPS 수신기 toosupport WebSocket 해야 하는 WebSocket 트래픽의 보안을 유지 합니다. 마찬가지로 hello를 사용할 수 있습니다 [포털](application-gateway-create-gateway-portal.md) 또는 [PowerShell](application-gateway-create-gateway-arm.md) toocreate 포트 80/443 toosupport WebSocket 트래픽을 수신기와 함께 응용 프로그램 게이트웨이 합니다.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>BackendAddressPool, BackendHttpSetting 및 라우팅 규칙 구성

BackendAddressPool 사용 되는 toodefine 활성화 WebSocket 서버와 백 엔드 풀입니다. hello backendHttpSetting 백 엔드 포트 80 및 443으로 정의 됩니다. 선호도 쿠키 기반 및 requestTimeouts hello 속성 관련 tooWebSocket 트래픽을 않습니다. Hello 라우팅 규칙에 필요한 변경 내용이 없는지, 'Basic'은 사용 되는 tootie hello 적절 한 수신기 toohello 백 엔드 주소 풀에 해당 합니다. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>WebSocket 활성화 백 엔드

백 엔드 hello 구성에서 실행 되는 HTTP/HTTPS 웹 서버가 있어야 합니다. WebSocket toowork에 대 한 포트 (일반적으로: 80/443). 이 요구 사항은 WebSocket 프로토콜 hello 초기 핸드셰이크 toobe HTTP 헤더 필드와 업그레이드 tooWebSocket 프로토콜에 필요 하기 때문에입니다. hello 다음은 헤더의 예입니다.

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

또 다른 이유는 응용 프로그램 게이트웨이 백 엔드 상태 프로브에서 HTTP/HTTPS 프로토콜만 지원하기 때문입니다. 백 엔드 서버 hello tooHTTP 또는 HTTPS 프로브 응답 하지 않으면 백 엔드 풀에서 수행 됩니다.

## <a name="next-steps"></a>다음 단계

WebSocket 지원에 대 한 학습 한 후 전환 너무[응용 프로그램 게이트웨이 만들](application-gateway-create-gateway.md) WebSocket 시작 tooget 웹 응용 프로그램을 사용 하도록 설정 합니다.

