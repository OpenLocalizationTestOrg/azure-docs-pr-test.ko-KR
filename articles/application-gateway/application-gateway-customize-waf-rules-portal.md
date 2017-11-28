---
title: "Azure 응용 프로그램 게이트웨이-Azure 포털의 aaaCustomize 웹 응용 프로그램 방화벽 규칙 | Microsoft Docs"
description: "이 문서에서는 toocustomize 웹 응용 프로그램 방화벽 규칙의 방식에 응용 프로그램 게이트웨이에서 Azure 포털 hello로 정보를 제공 합니다."
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
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="8d70d-103">Hello Azure 포털을 통해 웹 응용 프로그램 방화벽 규칙을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8d70d-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d70d-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="8d70d-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="8d70d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d70d-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="8d70d-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8d70d-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="8d70d-107">hello Azure 응용 프로그램 게이트웨이 웹 응용 프로그램 방화벽 (WAF) 웹 응용 프로그램에 대 한 보호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="8d70d-108">이러한 보호는 hello Open 웹 응용 프로그램 보안 프로젝트 (OWASP) 핵심 규칙 집합 (CR)에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="8d70d-109">일부 규칙은 거짓 긍정의 원인이 되어 실제 트래픽을 차단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="8d70d-110">이러한 이유로 응용 프로그램 게이트웨이 hello 기능 toocustomize 규칙 그룹 및 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="8d70d-111">Hello 특정 규칙 그룹 및 규칙에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 방화벽 CRS 규칙 그룹 및 규칙의 목록](application-gateway-crs-rulegroups-rules.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="8d70d-112">응용 프로그램 게이트웨이 WAF 계층 hello를 사용 하지 않는 경우 hello 옵션 tooupgrade hello 응용 프로그램 게이트웨이 toohello WAF 계층 hello 오른쪽 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![WAF 사용][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="8d70d-114">규칙 그룹 및 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="8d70d-114">View rule groups and rules</span></span>

<span data-ttu-id="8d70d-115">**tooview 규칙 그룹 및 규칙**</span><span class="sxs-lookup"><span data-stu-id="8d70d-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="8d70d-116">Toohello 응용 프로그램 게이트웨이 이동한 다음 선택 **웹 응용 프로그램 방화벽**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="8d70d-117">**고급 규칙 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="8d70d-118">이 보기는 규칙 집합을 선택 하는 hello와 함께 제공 되는 모든 hello 규칙 그룹의 hello 페이지에는 표를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="8d70d-119">Hello 규칙의 확인란이 모두 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-119">All of hello rule's check boxes are selected.</span></span>

![사용하지 않도록 설정된 규칙 구성][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="8d70d-121">규칙 toodisable 검색</span><span class="sxs-lookup"><span data-stu-id="8d70d-121">Search for rules toodisable</span></span>

<span data-ttu-id="8d70d-122">hello **웹 응용 프로그램 방화벽 설정** 블레이드는 텍스트 검색을 통해 toofilter hello 규칙 hello 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="8d70d-123">hello 결과 hello 규칙 그룹 및 hello 검색 한 텍스트를 포함 하는 규칙을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![규칙 검색][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="8d70d-125">규칙 그룹 및 규칙을 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="8d70d-125">Disable rule groups and rules</span></span>

<span data-ttu-id="8d70d-126">규칙을 사용하지 않도록 설정할 때 규칙 그룹 전체를 사용하지 않도록 설정하거나 하나 이상의 규칙 그룹에서 특정 규칙만 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="8d70d-127">**toodisable 규칙 그룹 또는 특정 규칙**</span><span class="sxs-lookup"><span data-stu-id="8d70d-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="8d70d-128">Hello 규칙 또는 toodisable 규칙 그룹을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="8d70d-129">Hello toodisable 원하는 규칙에 대 한 hello 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="8d70d-130">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-130">Select **Save**.</span></span> 

![변경 내용 저장][3]

## <a name="next-steps"></a><span data-ttu-id="8d70d-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d70d-132">Next steps</span></span>

<span data-ttu-id="8d70d-133">비활성화 된 규칙을 구성한 후 학습할 수 있는 방법을 tooview WAF 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d70d-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="8d70d-134">자세한 내용은 [Application Gateway 진단](application-gateway-diagnostics.md#diagnostic-logging)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d70d-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
