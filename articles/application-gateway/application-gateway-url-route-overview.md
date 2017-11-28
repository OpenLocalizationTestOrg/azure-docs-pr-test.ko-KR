---
title: "aaaURL 기반 콘텐츠 라우팅 개요 | Microsoft Docs"
description: "이 페이지는 hello 응용 프로그램 게이트웨이 URL 기반 콘텐츠 라우팅, UrlPathMap 구성 및 PathBasedRouting 규칙에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="bc8ee-103">URL 경로 기반 라우팅 개요</span><span class="sxs-lookup"><span data-stu-id="bc8ee-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="bc8ee-104">URL 경로 기반 라우팅 있습니다 tooroute 트래픽 tooback 엔드 서버 풀을 hello 요청의 URL 경로에 따라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="bc8ee-105">Hello 시나리오 중 하나는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooroute 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="bc8ee-106">다음 예제는 hello에서 응용 프로그램 게이트웨이 처리 세 백 엔드 서버 풀에서 contoso.com에 대 한 트래픽을 예: VideoServerPool, ImageServerPool, 및 DefaultServerPool 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="bc8ee-108">요청에 대 한 http://contoso.com/video * 라우트된 tooVideoServerPool 되며 http://contoso.com/images * 라우트된 tooImageServerPool 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="bc8ee-109">DefaultServerPool은 hello 경로 패턴의 조건과 일치 하는 경우에 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc8ee-110">규칙은 hello 포털에 나열 된 hello 순서로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="bc8ee-111">것이 권장된 사항임 tooconfigure 다중 사이트 수신기 첫 번째 이전 tooconfiguring 기본 수신기 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="bc8ee-112">이렇게 하면 해당 트래픽을 가져옵니다 라우트된 toohello 다시 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="bc8ee-113">기본 수신기가 먼저 나열되고 들어오는 요청과 일치하면 해당 수신기에서 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="bc8ee-114">UrlPathMap 구성 요소</span><span class="sxs-lookup"><span data-stu-id="bc8ee-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="bc8ee-115">hello urlPathMap 요소는 사용 되는 경로 패턴 tooback 엔드 toospecify 서버 풀 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="bc8ee-116">hello 다음 코드 예제는 서식 파일에서 urlPathMap 요소의 hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="bc8ee-117">PathPattern:이 설정은 경로 패턴 toomatch의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="bc8ee-118">각로 시작 해야 합니다 / hello만 장소는 "*" hello에 끝 팔 로우 허용 되는 "/."</span><span class="sxs-lookup"><span data-stu-id="bc8ee-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="bc8ee-119">toohello 경로 검색 도구를 공급 하는 hello 문자열 hello 후 텍스트를 먼저 포함 되지 됩니까? 또는 해당 문자 및 #, 여기 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="bc8ee-120">자세한 내용은 [URL 기반 라우팅을 사용하는 Resource Manager 템플릿](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="bc8ee-121">PathBasedRouting 규칙</span><span class="sxs-lookup"><span data-stu-id="bc8ee-121">PathBasedRouting rule</span></span>

<span data-ttu-id="bc8ee-122">PathBasedRouting 형식의 RequestRoutingRule 사용 되는 toobind 수신기 tooa urlPathMap입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="bc8ee-123">이 수신기에 대해 수신되는 모든 요청은 urlPathMap에 지정된 정책에 따라 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="bc8ee-124">PathBasedRouting 규칙 조각:</span><span class="sxs-lookup"><span data-stu-id="bc8ee-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bc8ee-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc8ee-125">Next steps</span></span>

<span data-ttu-id="bc8ee-126">콘텐츠 라우팅 URL 기반에 대 한 학습 한 후 전환 너무[URL 기반 라우팅을 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-url-route-portal.md) toocreate URL 라우팅 규칙으로 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8ee-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
