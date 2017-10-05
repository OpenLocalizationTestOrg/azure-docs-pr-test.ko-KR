---
title: "URL 기반 콘텐츠 라우팅 개요 | Microsoft Docs"
description: "이 페이지에서는 Application Gateway URL 기반 콘텐츠 라우팅, UrlPathMap 구성 및 PathBasedRouting 규칙에 대한 개요를 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="ea57d-103">URL 경로 기반 라우팅 개요</span><span class="sxs-lookup"><span data-stu-id="ea57d-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="ea57d-104">URL 경로 기반 라우팅을 사용하여 요청의 URL 경로에 따라 트래픽을 백 엔드 서버 풀로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="ea57d-105">시나리오 중 하나는 여러 콘텐츠 형식에 대한 요청을 서로 다른 백 엔드 서버 풀로 라우팅하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="ea57d-106">다음 예제에서는 Application Gateway가 세 개의 백 엔드 서버 풀(예: VideoServerPool, ImageServerPool 및 DefaultServerPool)에서 contoso.com에 대한 트래픽을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="ea57d-108">http://contoso.com/video*에 대한 요청은 VideoServerPool로 라우팅되고 http://contoso.com/images*에 대한 요청은 ImageServerPool로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="ea57d-109">경로 패턴과 일치하는 항목이 없는 경우 DefaultServerPool이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea57d-110">규칙은 포털에 나열된 순서대로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="ea57d-111">기본 수신기를 구성하기 전에 먼저 다중 사이트 수신기를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="ea57d-112">그러면 트래픽이 올바른 백 엔드로 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="ea57d-113">기본 수신기가 먼저 나열되고 들어오는 요청과 일치하면 해당 수신기에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="ea57d-114">UrlPathMap 구성 요소</span><span class="sxs-lookup"><span data-stu-id="ea57d-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="ea57d-115">urlPathMap 요소는 백 엔드 서버 풀 매핑에 대한 경로 패턴을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="ea57d-116">다음 코드 예제는 템플릿 파일의 urlPathMap 요소 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> <span data-ttu-id="ea57d-117">PathPattern: 이 설정은 일치하는 경로 패턴의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="ea57d-118">각각은 /로 시작해야 하고 "*"는 "/" 다음의 끝에 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="ea57d-119">경로 검사기에 제공하는 문자열은 ? 또는 #으로 시작하는 텍스트는 포함하지 않습니다. 이러한 문자는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="ea57d-120">자세한 내용은 [URL 기반 라우팅을 사용하는 Resource Manager 템플릿](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea57d-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="ea57d-121">PathBasedRouting 규칙</span><span class="sxs-lookup"><span data-stu-id="ea57d-121">PathBasedRouting rule</span></span>

<span data-ttu-id="ea57d-122">PathBasedRouting 형식의 RequestRoutingRule은 수신기를 urlPathMap에 바인딩하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="ea57d-123">이 수신기에 대해 수신되는 모든 요청은 urlPathMap에 지정된 정책에 따라 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="ea57d-124">PathBasedRouting 규칙 조각:</span><span class="sxs-lookup"><span data-stu-id="ea57d-124">Snippet of PathBasedRouting rule:</span></span>

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="ea57d-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea57d-125">Next steps</span></span>

<span data-ttu-id="ea57d-126">URL 기반 콘텐츠 라우팅을 알아본 후에는 [URL 기반 라우팅을 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-create-url-route-portal.md) 로 이동하여 URL 라우팅 규칙을 사용하여 응용 프로그램 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ea57d-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
