---
title: "Azure Application Gateway에서 웹 응용 프로그램 방화벽 규칙 사용자 지정 - Azure CLI 2.0 | Microsoft Docs"
description: "이 문서에서는 Azure CLI 2.0을 통해 Application Gateway에서 웹 응용 프로그램 방화벽 규칙을 사용자 지정하는 방법을 설명합니다."
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="dff6d-103">Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="dff6d-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dff6d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dff6d-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="dff6d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dff6d-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="dff6d-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dff6d-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="dff6d-107">Azure Application Gateway WAF(웹 응용 프로그램 방화벽)는 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="dff6d-108">이러한 보호 기능은 OWASP(Open Web Application Security Project) CRS(코어 규칙 집합)을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="dff6d-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="dff6d-110">이러한 이유로 Application Gateway는 규칙 그룹 및 규칙을 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="dff6d-111">특정 규칙 그룹 및 규칙에 대한 자세한 내용은 [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙 목록](application-gateway-crs-rulegroups-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dff6d-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="dff6d-112">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="dff6d-112">View rule groups and rules</span></span>

<span data-ttu-id="dff6d-113">다음 코드 예제에서는 구성 가능한 규칙 및 규칙 그룹을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="dff6d-114">규칙 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="dff6d-114">View rule groups</span></span>

<span data-ttu-id="dff6d-115">다음 예제에서는 규칙 그룹을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="dff6d-116">다음 출력은 이전 예제에서 잘린 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="dff6d-117">규칙 그룹에서 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="dff6d-117">View rules in a rule group</span></span>

<span data-ttu-id="dff6d-118">다음 예제에서는 지정된 규칙 그룹에서 규칙을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="dff6d-119">다음 출력은 이전 예제에서 잘린 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="dff6d-120">규칙 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="dff6d-120">Disable rules</span></span>

<span data-ttu-id="dff6d-121">다음 예제는 응용 프로그램 게이트웨이에서 규칙 `910018` 및 `910017`을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="dff6d-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dff6d-122">Next steps</span></span>

<span data-ttu-id="dff6d-123">비활성화된 규칙을 구성한 후 WAF 로그를 보는 방법에 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dff6d-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="dff6d-124">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dff6d-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
