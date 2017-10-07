---
title: "경로 기반 aaaCreate 규칙-Azure 응용 프로그램 게이트웨이-Azure 포털 | Microsoft Docs"
description: "자세한 내용은 응용 프로그램 게이트웨이 사용 하 여에 대 한 경로 기반 규칙 toocreate 포털 hello 하는 방법"
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="064dd-103">Hello 포털을 사용 하 여 응용 프로그램 게이트웨이 대 한 기준으로 경로 규칙을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="064dd-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="064dd-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="064dd-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="064dd-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="064dd-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="064dd-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="064dd-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="064dd-107">URL 라우팅 경로 기반 있습니다 tooassociate 경로 Http 요청의 hello URL 경로에 따라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="064dd-108">경로 tooa 백 엔드 풀 응용 프로그램 게이트웨이 hello에 나열 된 hello URL에 대해 구성 된 경우를 확인 하 고 hello 네트워크 트래픽 toohello 백 엔드 풀 정의 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="064dd-109">URL 기반 라우팅에 대 한 일반적인 용도는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="064dd-110">URL 기반 라우팅 새 규칙 유형 tooapplication 게이트웨이 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="064dd-111">응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 경로 기반 규칙)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="064dd-112">기본 규칙 종류 hello hello 백 엔드에 대 한 라운드 로빈 서비스 경로 기반 규칙 하면서 또한 tooround 로빈 배포 풀, 고려 hello 요청 URL의 경로 패턴 hello 적절 한 백 엔드 풀을 선택 하는 동안를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="064dd-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="064dd-113">Scenario</span></span>

<span data-ttu-id="064dd-114">hello 다음과 같은 시나리오를 진행 기존 응용 프로그램 게이트웨이에서 경로 기반 규칙 만들기.</span><span class="sxs-lookup"><span data-stu-id="064dd-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="064dd-115">hello 시나리오에서는 가정 이미 수행 hello 단계 너무[응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![url 경로][scenario]

## <span data-ttu-id="064dd-117"><a name="createrule"></a>Hello 경로 기반 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="064dd-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="064dd-118">경로 기반 규칙 수 있는 사용 가능한 수신기 toouse 있는지 tooverify hello 규칙을 만들기 전에 해당 수신기가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="064dd-119">1단계</span><span class="sxs-lookup"><span data-stu-id="064dd-119">Step 1</span></span>

<span data-ttu-id="064dd-120">Toohello 이동 [Azure 포털](http://portal.azure.com) 하 고 기존 응용 프로그램 게이트웨이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="064dd-121">**규칙**</span><span class="sxs-lookup"><span data-stu-id="064dd-121">Click **Rules**</span></span>

![Application Gateway 개요][1]

### <a name="step-2"></a><span data-ttu-id="064dd-123">2단계</span><span class="sxs-lookup"><span data-stu-id="064dd-123">Step 2</span></span>

<span data-ttu-id="064dd-124">클릭 **경로 기반** 단추 tooadd 새 경로 기반 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="064dd-125">3단계</span><span class="sxs-lookup"><span data-stu-id="064dd-125">Step 3</span></span>

<span data-ttu-id="064dd-126">hello **경로 기반 규칙 추가** 블레이드는 다음 두 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="064dd-127">hello 첫 번째 섹션은 hello 수신기, hello 이름 hello 규칙 및 hello 기본 경로 설정을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="064dd-128">사용자 지정 경로 기반 경로 hello에서 포함 되지 않는 경로 대 한 hello 기본 경로 설정이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="064dd-129">hello의 두 번째 섹션 hello **경로 기반 규칙 추가** 블레이드 스스로 hello 경로 기반 규칙을 정의한는 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="064dd-130">**기본 설정**</span><span class="sxs-lookup"><span data-stu-id="064dd-130">**Basic Settings**</span></span>

* <span data-ttu-id="064dd-131">**이름** -이 값은 hello 포털에 액세스할 수 있는 친숙 한 이름 toohello 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="064dd-132">**수신기** -이 값은 hello 규칙에 사용 되는 hello 수신기입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="064dd-133">**백 엔드 풀 기본** -이 설정은 hello 백 엔드 toobe hello 기본 규칙에 사용 되는 정의 하는 hello 설정</span><span class="sxs-lookup"><span data-stu-id="064dd-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="064dd-134">**기본 HTTP 설정** -이 설정은이 hello HTTP 설정 toobe hello 기본 규칙에 사용 되는 정의 하는 hello 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="064dd-135">**경로 기반 규칙**</span><span class="sxs-lookup"><span data-stu-id="064dd-135">**Path-based rules**</span></span>

* <span data-ttu-id="064dd-136">**이름** -이 값은 친숙 한 이름 toopath 기반 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="064dd-137">**경로** -트래픽을 전달 하는 경우이 설정은 정의 hello에 대 한 경로 hello 규칙 검색</span><span class="sxs-lookup"><span data-stu-id="064dd-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="064dd-138">**백 엔드 풀** -이 설정은 hello 백 엔드 toobe hello 규칙에 사용 되는 정의 하는 hello 설정</span><span class="sxs-lookup"><span data-stu-id="064dd-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="064dd-139">**HTTP 설정** -이 설정은이 hello HTTP 설정 toobe hello 규칙에 사용 되는 정의 하는 hello 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="064dd-140">경로 패턴 toomatch의 경로: hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="064dd-141">로 시작 해야 각 / hello만 장소는 "\*" ï ´ ù hello 끝에 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="064dd-142">사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![정보가 입력된 경로 기반 규칙 추가 블레이드][2]

<span data-ttu-id="064dd-144">기존 응용 프로그램 게이트웨이 hello 포털을 통해 쉽게 프로세스 경로 기반 규칙 tooan를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="064dd-145">경로 기반 규칙을 만든 후 편집된 tooadd 추가 규칙 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![추가 경로 기반 규칙 추가][3]

<span data-ttu-id="064dd-147">이 단계는 경로 기반 경로를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-147">This step configures a path-based route.</span></span> <span data-ttu-id="064dd-148">중요 한 toounderstand 요청은 다시 작성 하지 이면 hello 요청 및 basic hello url 패턴 보냅니다 hello 요청 toohello 적절 한 백 엔드에 요청 제공 응용 프로그램 게이트웨이으로 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="064dd-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="064dd-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="064dd-149">Next steps</span></span>

<span data-ttu-id="064dd-150">Azure 응용 프로그램 게이트웨이 통해 SSL 오프 로딩 tooconfigure 참조 toolearn [SSL 오프 로드 구성](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="064dd-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
