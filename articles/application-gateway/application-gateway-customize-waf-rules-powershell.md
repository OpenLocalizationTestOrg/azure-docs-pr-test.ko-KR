---
title: "Azure Application Gateway에서 웹 응용 프로그램 방화벽 규칙 사용자 지정 - PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 통해 Application Gateway에서 웹 응용 프로그램 방화벽 규칙을 사용자 지정하는 방법을 설명합니다."
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
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="3bab5-103">PowerShell을 통해 웹 응용 프로그램 방화벽 규칙 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3bab5-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bab5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3bab5-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="3bab5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bab5-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="3bab5-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3bab5-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="3bab5-107">Azure Application Gateway WAF(웹 응용 프로그램 방화벽)는 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="3bab5-108">이러한 보호 기능은 OWASP(Open Web Application Security Project) CRS(코어 규칙 집합)을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="3bab5-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="3bab5-110">이러한 이유로 Application Gateway는 규칙 그룹 및 규칙을 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="3bab5-111">특정 규칙 그룹 및 규칙에 대한 자세한 내용은 [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙 목록](application-gateway-crs-rulegroups-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bab5-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="3bab5-112">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="3bab5-112">View rule groups and rules</span></span>

<span data-ttu-id="3bab5-113">다음은 WAF가 활성화된 응용 프로그램 게이트웨이에서 구성 가능한 규칙 및 규칙 그룹을 보는 방법을 보여 주는 코드 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="3bab5-114">규칙 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="3bab5-114">View rule groups</span></span>

<span data-ttu-id="3bab5-115">다음 예제에서는 규칙 그룹을 보는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="3bab5-116">다음 출력은 이전 예제에서 잘린 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="3bab5-117">규칙 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="3bab5-117">Disable rules</span></span>

<span data-ttu-id="3bab5-118">다음 예제는 응용 프로그램 게이트웨이에서 규칙 `910018` 및 `910017`을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="3bab5-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3bab5-119">Next steps</span></span>

<span data-ttu-id="3bab5-120">비활성화된 규칙을 구성한 후 WAF 로그를 보는 방법에 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bab5-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="3bab5-121">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3bab5-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
