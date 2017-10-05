---
title: "Azure Application Gateway의 WebSocket 지원 | Microsoft Docs"
description: "이 페이지에서는 Application Gateway WebSocket 지원에 대한 개요를 제공합니다."
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
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="7feec-103">Application Gateway의 WebSocket 지원 개요</span><span class="sxs-lookup"><span data-stu-id="7feec-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="7feec-104">Application Gateway는 모든 게이트웨이 크기에 WebSocket에 대한 네이티브 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="7feec-105">WebSocket 지원을 선택적으로 사용하거나 사용하지 않도록 설정하는 사용자 구성 가능 설정은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="7feec-106">[RFC6455](https://tools.ietf.org/html/rfc6455)에서 표준화된 WebSocket 프로토콜을 사용하면 장기 실행 TCP 연결을 통해 서버와 클라이언트 간의 전이중 통신을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="7feec-107">이 기능을 사용하면 웹 서버와 클라이언트 간의 대화형 통신이 가능하며, HTTP 기반 구현에서 필요에 따라 폴링하지 않고도 양방향 통신을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="7feec-108">WebSocket은 HTTP와 달리 오버헤드가 낮고 여러 요청/응답에 동일한 TCP 연결을 다시 사용하므로 리소스를 더 효율적으로 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="7feec-109">WebSocket 프로토콜은 기존의 HTTP 포트 80 및 443을 통해 작동하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="7feec-110">80 또는 443 포트에서 표준 HTTP 수신기를 계속 사용하여 WebSocket 트래픽을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="7feec-111">WebSocket 트래픽은 Application Gateway 규칙에 지정된 대로 적절한 백 엔드 풀을 사용하여 WebSocket 활성화된 백 엔드 서버로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="7feec-112">백 엔드 서버는 [상태 프로브 개요](application-gateway-probe-overview.md) 섹션에서 설명한 대로 응용 프로그램 게이트웨이 프로브에 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="7feec-113">응용 프로그램 게이트웨이 상태 프로브는 HTTP/HTTPS 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="7feec-114">각 백 엔드 서버는 WebSocket 트래픽을 서버로 라우팅하기 위해 응용 프로그램 게이트웨이에 대한 HTTP 프로브에 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="7feec-115">수신기 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7feec-115">Listener configuration element</span></span>

<span data-ttu-id="7feec-116">기존 HTTP 수신기를 사용하여 WebSocket을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="7feec-117">다음은 샘플 템플릿 파일에 있는 httpListeners 요소의 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="7feec-118">WebSocket을 지원하고 WebSocket 트래픽을 보호하기 위해 HTTP 및 HTTPS 수신기가 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="7feec-119">마찬가지로 [포털](application-gateway-create-gateway-portal.md) 또는 [PowerShell](application-gateway-create-gateway-arm.md)을 사용하여 WebSocket 트래픽을 지원하기 위해 포트 80/443에 대한 수신기를 포함한 Application Gateway를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="7feec-120">BackendAddressPool, BackendHttpSetting 및 라우팅 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="7feec-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="7feec-121">BackendAddressPool은 WebSocket 지원 서버가 포함된 백 엔드 풀을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="7feec-122">backendHttpSetting은 80 및 443 백 엔드 포트로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="7feec-123">쿠키 기반 선호도 및 requestTimeouts의 속성은 WebSocket 트래픽과 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="7feec-124">라우팅 규칙은 변경할 필요가 없으며, 'Basic'(기본)은 적절한 수신기를 해당 백 엔드 주소 풀에 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="7feec-125">WebSocket 활성화 백 엔드</span><span class="sxs-lookup"><span data-stu-id="7feec-125">WebSocket enabled backend</span></span>

<span data-ttu-id="7feec-126">WebSocket이 작동되려면 사용자의 백 엔드가 구성된 포트(대개 80/443)에서 HTTP/HTTPS 웹 서버를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="7feec-127">이 요구 사항은 WebSocket 프로토콜을 헤더 필드로 업그레이드하여 초기 핸드 셰이크가 HTTP가 되도록 WebSocket 프로토콜에서 요구하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="7feec-128">다음은 헤더의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-128">The following is an example of a header:</span></span>

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

<span data-ttu-id="7feec-129">또 다른 이유는 응용 프로그램 게이트웨이 백 엔드 상태 프로브에서 HTTP/HTTPS 프로토콜만 지원하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="7feec-130">백 엔드 서버에서 HTTP 또는 HTTPS 프로브에 응답하지 않으면 해당 백 엔드 서버가 백 엔드 풀에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7feec-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7feec-131">Next steps</span></span>

<span data-ttu-id="7feec-132">WebSocket 지원에 대해 알아본 후에 [Application Gateway 만들기](application-gateway-create-gateway.md)로 이동하여 WebSocket 활성화 웹 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7feec-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

