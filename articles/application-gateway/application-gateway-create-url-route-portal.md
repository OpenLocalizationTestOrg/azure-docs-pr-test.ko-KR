---
title: "경로 기반 규칙 만들기 - Azure Application Gateway - Azure Portal | Microsoft Docs"
description: "포털을 사용하여 응용 프로그램 게이트웨이에 대한 경로 기반 규칙을 만드는 방법을 알아봅니다."
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="ed350-103">포털을 사용하여 응용 프로그램 게이트웨이에 대한 경로 기반 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="ed350-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed350-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ed350-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="ed350-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed350-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="ed350-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ed350-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="ed350-107">URL 경로 기반 라우팅을 사용하여 Http 요청의 URL 경로에 따라 경로를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="ed350-108">Application Gateway에 나열된 URL에 대해 구성된 백 엔드 풀에 대한 경로가 있는지 확인하고 정의된 백 엔드 풀로 네트워크 트래픽을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="ed350-109">URL 기반 라우팅의 일반적인 용도는 여러 콘텐츠 형식에 대한 요청의 부하를 여러 백 엔드 서버 풀에 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="ed350-110">URL 기반 라우팅에서는 응용 프로그램 게이트웨이에 새로운 규칙 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="ed350-111">응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 경로 기반 규칙)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="ed350-112">기본 규칙 형식은 백 엔드 풀에 대한 라운드 로빈 서비스를 제공하는 반면 경로 기반 규칙은 해당 백 엔드 풀을 선택하는 동안 라운드 로빈 배포 외에도 계정에 요청 URL의 경로 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="ed350-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="ed350-113">Scenario</span></span>

<span data-ttu-id="ed350-114">다음 시나리오에서는 기존 응용 프로그램 게이트웨이에서 경로 기반 규칙을 만드는 과정을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="ed350-115">이 시나리오에서는 [Application Gateway 만들기](application-gateway-create-gateway-portal.md)단계를 이미 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![url 경로][scenario]

## <span data-ttu-id="ed350-117"><a name="createrule"></a>경로 기반 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="ed350-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="ed350-118">경로 기반 규칙에는 고유한 수신기가 필요합니다. 규칙을 만들기 전에 사용할 수 있는 수신기가 있는지 반드시 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="ed350-119">1단계:</span><span class="sxs-lookup"><span data-stu-id="ed350-119">Step 1</span></span>

<span data-ttu-id="ed350-120">[Azure Portal](http://portal.azure.com)로 이동하여 기존 Application Gateway를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="ed350-121">**규칙**</span><span class="sxs-lookup"><span data-stu-id="ed350-121">Click **Rules**</span></span>

![Application Gateway 개요][1]

### <a name="step-2"></a><span data-ttu-id="ed350-123">2단계</span><span class="sxs-lookup"><span data-stu-id="ed350-123">Step 2</span></span>

<span data-ttu-id="ed350-124">**경로 기반** 단추를 클릭하여 새 경로 기반 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="ed350-125">3단계</span><span class="sxs-lookup"><span data-stu-id="ed350-125">Step 3</span></span>

<span data-ttu-id="ed350-126">**경로 기반 규칙 추가** 블레이드에는 다음 두 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="ed350-127">두 번째 섹션에서는 수신기, 규칙의 이름 및 기본 경로 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="ed350-128">기본 경로 설정은 사용자 지정 경로 기반 경로에 속하지 않는 경로에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="ed350-129">**경로 기반 규칙 추가** 블레이드의 두 번째 섹션에서는 경로 기반 규칙을 직접 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="ed350-130">**기본 설정**</span><span class="sxs-lookup"><span data-stu-id="ed350-130">**Basic Settings**</span></span>

* <span data-ttu-id="ed350-131">**이름** - 이 값은 포털에서 액세스할 수 있는 규칙에 대한 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="ed350-132">**수신기** - 이 값은 규칙에 사용되는 수신기입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="ed350-133">**기본 백 엔드 풀** - 기본 규칙에 사용할 백 엔드를 정의하는 설정입니다</span><span class="sxs-lookup"><span data-stu-id="ed350-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="ed350-134">**기본 HTTP 설정** - 기본 규칙에 사용할 HTTP 설정을 정의하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="ed350-135">**경로 기반 규칙**</span><span class="sxs-lookup"><span data-stu-id="ed350-135">**Path-based rules**</span></span>

* <span data-ttu-id="ed350-136">**이름** - 이 값은 경로 기반 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="ed350-137">**경로** - 이 설정은 트래픽을 전달할 때 규칙이 찾는 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="ed350-138">**백 엔드 풀** - 규칙에 사용할 백 엔드를 정의하는 설정입니다</span><span class="sxs-lookup"><span data-stu-id="ed350-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="ed350-139">**HTTP 설정** - 규칙에 사용할 HTTP 설정을 정의하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed350-140">경로: 일치하는 경로 패턴의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="ed350-141">각각은 /로 시작해야 하고 "\*"는 끝에만 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="ed350-142">사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![정보가 입력된 경로 기반 규칙 추가 블레이드][2]

<span data-ttu-id="ed350-144">기존 응용 프로그램 게이트웨이에 경로 기반 규칙을 추가하는 작업은 포털을 통해 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="ed350-145">경로 기반 규칙을 만든 후 추가 규칙을 추가하도록 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![추가 경로 기반 규칙 추가][3]

<span data-ttu-id="ed350-147">이 단계는 경로 기반 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-147">This step configures a path-based route.</span></span> <span data-ttu-id="ed350-148">응용 프로그램에 요청이 들어 올 때 요청은 다시 작성되지 않고, 게이트웨이가 요청 및 URL 패턴에 대한 기본 사항을 검사한 후 해당 백 엔드로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed350-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed350-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed350-149">Next steps</span></span>

<span data-ttu-id="ed350-150">Azure Application Gateway를 사용하여 SSL 오프로드를 구성하는 방법은 [SSL 오프로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ed350-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
