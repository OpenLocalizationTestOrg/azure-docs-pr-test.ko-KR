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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="245ff-103">Hello Azure CLI 2.0을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="245ff-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="245ff-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="245ff-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="245ff-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="245ff-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="245ff-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="245ff-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="245ff-107">hello Azure 응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF) 웹 응용 프로그램에 대 한 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="245ff-108">이러한 보호는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) 핵심 규칙 집합 (CR)에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="245ff-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="245ff-110">이러한 이유로 응용 프로그램 게이트웨이 hello 기능 toocustomize 규칙 그룹 및 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="245ff-111">Hello 특정 규칙 그룹 및 규칙에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙의 목록](application-gateway-crs-rulegroups-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="245ff-112">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="245ff-112">View rule groups and rules</span></span>

<span data-ttu-id="245ff-113">다음 코드 예제는 hello tooview의 규칙 및 규칙 그룹에 구성할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="245ff-114">규칙 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="245ff-114">View rule groups</span></span>

<span data-ttu-id="245ff-115">다음 예제는 hello tooview 규칙 그룹을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="245ff-116">hello 다음 출력은 hello 예에서는 앞에서 잘린된 응답:</span><span class="sxs-lookup"><span data-stu-id="245ff-116">hello following output is a truncated response from hello preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="245ff-117">규칙 그룹에서 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="245ff-117">View rules in a rule group</span></span>

<span data-ttu-id="245ff-118">다음 예제는 hello tooview 지정 된 규칙 그룹에 규칙 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="245ff-119">hello 다음 출력은 hello 예에서는 앞에서 잘린된 응답:</span><span class="sxs-lookup"><span data-stu-id="245ff-119">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="245ff-120">규칙 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="245ff-120">Disable rules</span></span>

<span data-ttu-id="245ff-121">hello 다음 예제에서는 비활성화 규칙 `910018` 및 `910017` 응용 프로그램 게이트웨이에:</span><span class="sxs-lookup"><span data-stu-id="245ff-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="245ff-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="245ff-122">Next steps</span></span>

<span data-ttu-id="245ff-123">비활성화 된 규칙을 구성한 후 학습할 수 있는 방법을 tooview WAF 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="245ff-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="245ff-124">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="245ff-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
