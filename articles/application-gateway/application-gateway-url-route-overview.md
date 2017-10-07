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
# <a name="url-path-based-routing-overview"></a>URL 경로 기반 라우팅 개요

URL 경로 기반 라우팅 있습니다 tooroute 트래픽 tooback 엔드 서버 풀을 hello 요청의 URL 경로에 따라 수 있습니다. 

Hello 시나리오 중 하나는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooroute 요청 합니다.

다음 예제는 hello에서 응용 프로그램 게이트웨이 처리 세 백 엔드 서버 풀에서 contoso.com에 대 한 트래픽을 예: VideoServerPool, ImageServerPool, 및 DefaultServerPool 합니다.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

요청에 대 한 http://contoso.com/video * 라우트된 tooVideoServerPool 되며 http://contoso.com/images * 라우트된 tooImageServerPool 됩니다. DefaultServerPool은 hello 경로 패턴의 조건과 일치 하는 경우에 선택 되어 있습니다.

> [!IMPORTANT]
> 규칙은 hello 포털에 나열 된 hello 순서로 처리 됩니다. 것이 권장된 사항임 tooconfigure 다중 사이트 수신기 첫 번째 이전 tooconfiguring 기본 수신기 합니다.  이렇게 하면 해당 트래픽을 가져옵니다 라우트된 toohello 다시 종료 합니다. 기본 수신기가 먼저 나열되고 들어오는 요청과 일치하면 해당 수신기에서 처리합니다.

## <a name="urlpathmap-configuration-element"></a>UrlPathMap 구성 요소

hello urlPathMap 요소는 사용 되는 경로 패턴 tooback 엔드 toospecify 서버 풀 매핑입니다. hello 다음 코드 예제는 서식 파일에서 urlPathMap 요소의 hello 조각입니다.

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
> PathPattern:이 설정은 경로 패턴 toomatch의 목록입니다. 각로 시작 해야 합니다 / hello만 장소는 "*" hello에 끝 팔 로우 허용 되는 "/." toohello 경로 검색 도구를 공급 하는 hello 문자열 hello 후 텍스트를 먼저 포함 되지 됩니까? 또는 해당 문자 및 #, 여기 허용 되지 않습니다.

자세한 내용은 [URL 기반 라우팅을 사용하는 Resource Manager 템플릿](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing)을 참조하세요.

## <a name="pathbasedrouting-rule"></a>PathBasedRouting 규칙

PathBasedRouting 형식의 RequestRoutingRule 사용 되는 toobind 수신기 tooa urlPathMap입니다. 이 수신기에 대해 수신되는 모든 요청은 urlPathMap에 지정된 정책에 따라 라우팅됩니다.
PathBasedRouting 규칙 조각:

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

## <a name="next-steps"></a>다음 단계

콘텐츠 라우팅 URL 기반에 대 한 학습 한 후 전환 너무[URL 기반 라우팅을 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-url-route-portal.md) toocreate URL 라우팅 규칙으로 응용 프로그램 게이트웨이 합니다.
