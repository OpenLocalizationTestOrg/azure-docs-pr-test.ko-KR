---
title: "Azure 응용 프로그램 게이트웨이 Azure CLI 2.0 aaaCustomize 웹 응용 프로그램 방화벽 규칙 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 2.0 hello로 응용 프로그램 게이트웨이에서 규칙 toocustomize 웹 응용 프로그램 방화벽 방식 설명 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Hello Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정

> [!div class="op_single_selector"]
> * [Azure 포털](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

hello Azure 응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF) 웹 응용 프로그램에 대 한 보호를 제공합니다. 이러한 보호는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) 핵심 규칙 집합 (CR)에서 제공 됩니다. 일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다. 이러한 이유로 응용 프로그램 게이트웨이 hello 기능 toocustomize 규칙 그룹 및 규칙을 제공합니다. Hello 특정 규칙 그룹 및 규칙에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙의 목록](application-gateway-crs-rulegroups-rules.md)합니다.

## <a name="view-rule-groups-and-rules"></a>규칙 그룹 및 규칙 보기

다음 코드 예제는 hello tooview의 규칙 및 규칙 그룹에 구성할 수 있는 방법을 보여 줍니다.

### <a name="view-rule-groups"></a>규칙 그룹 보기

다음 예제는 hello tooview 규칙 그룹을 hello 하는 방법을 보여 줍니다.

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

hello 다음 출력은 hello 예에서는 앞에서 잘린된 응답:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a>규칙 그룹에서 규칙 보기

다음 예제는 hello tooview 지정 된 규칙 그룹에 규칙 하는 방법을 보여 줍니다.

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

hello 다음 출력은 hello 예에서는 앞에서 잘린된 응답:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a>규칙 사용 안 함

hello 다음 예제에서는 비활성화 규칙 `910018` 및 `910017` 응용 프로그램 게이트웨이에:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>다음 단계

비활성화 된 규칙을 구성한 후 학습할 수 있는 방법을 tooview WAF 로그 합니다. 자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
