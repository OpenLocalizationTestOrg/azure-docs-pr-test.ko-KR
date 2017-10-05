---
title: "Azure Application Gateway에서 웹 응용 프로그램 방화벽 규칙 사용자 지정 - Azure Portal | Microsoft Docs"
description: "이 문서에서는 Azure Portal을 통해 Application Gateway에서 웹 응용 프로그램 방화벽 규칙을 사용자 지정하는 방법을 설명합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="14a0e-103">Azure Portal을 통해 웹 응용 프로그램 방화벽 규칙 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="14a0e-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="14a0e-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="14a0e-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="14a0e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14a0e-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="14a0e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="14a0e-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="14a0e-107">Azure Application Gateway WAF(웹 응용 프로그램 방화벽)는 웹 응용 프로그램을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="14a0e-108">이러한 보호 기능은 OWASP(Open Web Application Security Project) CRS(코어 규칙 집합)을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="14a0e-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="14a0e-110">이러한 이유로 Application Gateway는 규칙 그룹 및 규칙을 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="14a0e-111">특정 규칙 그룹 및 규칙에 대한 자세한 내용은 [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙 목록](application-gateway-crs-rulegroups-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a0e-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="14a0e-112">Application Gateway에서 WAF 계층을 사용하지 않는 경우 Application Gateway를 WAF 계층으로 업그레이드하는 옵션이 오른쪽 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![WAF 사용][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="14a0e-114">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="14a0e-114">View rule groups and rules</span></span>

<span data-ttu-id="14a0e-115">**규칙 그룹 및 규칙을 보려면**</span><span class="sxs-lookup"><span data-stu-id="14a0e-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="14a0e-116">Application Gateway로 이동하여 **웹 응용 프로그램 방화벽**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="14a0e-117">**고급 규칙 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="14a0e-118">이 보기는 선택된 규칙 집합과 함께 제공되는 모든 규칙 그룹의 페이지에 하나의 테이블을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="14a0e-119">모든 규칙의 확인란이 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-119">All of the rule's check boxes are selected.</span></span>

![사용하지 않도록 설정된 규칙 구성][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="14a0e-121">사용하지 않을 규칙 검색</span><span class="sxs-lookup"><span data-stu-id="14a0e-121">Search for rules to disable</span></span>

<span data-ttu-id="14a0e-122">**웹 응용 프로그램 방화벽 설정** 블레이드는 텍스트 검색으로 규칙을 필터링하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="14a0e-123">검색 텍스트가 포함된 규칙 그룹 및 규칙만 결과에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![규칙 검색][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="14a0e-125">규칙 그룹 및 규칙을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="14a0e-125">Disable rule groups and rules</span></span>

<span data-ttu-id="14a0e-126">규칙을 사용하지 않도록 설정할 때 규칙 그룹 전체를 사용하지 않도록 설정하거나 하나 이상의 규칙 그룹에서 특정 규칙만 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="14a0e-127">**규칙 그룹 또는 특정 규칙을 사용하지 않도록 설정하려면**</span><span class="sxs-lookup"><span data-stu-id="14a0e-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="14a0e-128">사용하지 않도록 설정할 규칙 또는 규칙 그룹을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="14a0e-129">사용하지 않도록 설정하려는 규칙에 대한 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="14a0e-130">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-130">Select **Save**.</span></span> 

![변경 내용 저장][3]

## <a name="next-steps"></a><span data-ttu-id="14a0e-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14a0e-132">Next steps</span></span>

<span data-ttu-id="14a0e-133">비활성화된 규칙을 구성한 후 WAF 로그를 보는 방법에 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a0e-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="14a0e-134">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a0e-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
