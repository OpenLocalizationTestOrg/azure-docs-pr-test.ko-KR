---
title: "Azure 응용 프로그램 게이트웨이 PowerShell aaaCustomize 웹 응용 프로그램 방화벽 규칙 | Microsoft Docs"
description: "이 문서에서 PowerShell과 함께 응용 프로그램 게이트웨이 toocustomize 웹 응용 프로그램 방화벽 규칙의 방식에 정보를 제공 합니다."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="8ea97-103">PowerShell을 통해 웹 응용 프로그램 방화벽 규칙 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8ea97-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ea97-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8ea97-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="8ea97-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ea97-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="8ea97-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ea97-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="8ea97-107">hello Azure 응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF) 웹 응용 프로그램에 대 한 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="8ea97-108">이러한 보호는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) 핵심 규칙 집합 (CR)에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="8ea97-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="8ea97-110">이러한 이유로 응용 프로그램 게이트웨이 hello 기능 toocustomize 규칙 그룹 및 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="8ea97-111">Hello 특정 규칙 그룹 및 규칙에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙의 목록](application-gateway-crs-rulegroups-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="8ea97-112">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="8ea97-112">View rule groups and rules</span></span>

<span data-ttu-id="8ea97-113">다음 코드 예제는 hello tooview의 규칙 및 규칙 그룹 WAF 사용 응용 프로그램 게이트웨이를 구성할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="8ea97-114">규칙 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="8ea97-114">View rule groups</span></span>

<span data-ttu-id="8ea97-115">hello 방법을 예제와 다음 tooview 규칙 그룹:</span><span class="sxs-lookup"><span data-stu-id="8ea97-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="8ea97-116">hello 다음 출력은 hello 예에서는 앞에서 잘린된 응답:</span><span class="sxs-lookup"><span data-stu-id="8ea97-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="8ea97-117">규칙 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8ea97-117">Disable rules</span></span>

<span data-ttu-id="8ea97-118">hello 다음 예제에서는 비활성화 규칙 `910018` 및 `910017` 응용 프로그램 게이트웨이에:</span><span class="sxs-lookup"><span data-stu-id="8ea97-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="8ea97-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ea97-119">Next steps</span></span>

<span data-ttu-id="8ea97-120">비활성화 된 규칙을 구성한 후 학습할 수 있는 방법을 tooview WAF 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ea97-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="8ea97-121">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ea97-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
