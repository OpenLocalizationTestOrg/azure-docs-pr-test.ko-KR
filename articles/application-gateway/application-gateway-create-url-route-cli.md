---
title: "aaaCreate URL 라우팅을 사용 하 여 응용 프로그램 게이트웨이 규칙-Azure CLI 2.0 | Microsoft Docs"
description: "이 페이지에서는 지침 toocreate, URL 라우팅 규칙을 사용 하 여 Azure 응용 프로그램 게이트웨이 구성 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="07375-103">Azure CLI 2.0과 함께 경로 기반 라우팅을 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07375-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="07375-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="07375-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="07375-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="07375-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="07375-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="07375-107">URL 라우팅 경로 기반 있습니다 tooassociate 경로 Http 요청의 hello URL 경로에 따라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07375-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="07375-108">응용 프로그램 게이트웨이 hello에 제공 된 hello URL에 대해 구성 하는 경로 tooa 백 엔드 풀에 없는 경우를 확인 하 고 hello 네트워크 트래픽 toohello 백 엔드 풀 정의 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="07375-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="07375-109">URL 기반 라우팅에 대 한 일반적인 용도는 서로 다른 내용 유형 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="07375-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="07375-110">URL 기반 라우팅 새 규칙 유형 tooapplication 게이트웨이 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="07375-111">응용 프로그램 게이트웨이에는 두 가지 규칙 형식(기본 및 PathBasedRouting)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07375-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="07375-112">기본 규칙 종류는 hello 백 엔드에 대 한 라운드 로빈 서비스 PathBasedRouting 하면서 또한 tooround 로빈 배포 풀, 고려 hello 요청 URL의 경로 패턴 hello 백 엔드 풀을 선택 하는 동안를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="07375-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="07375-113">Scenario</span></span>

<span data-ttu-id="07375-114">다음 예제는 hello에서 응용 프로그램 게이트웨이 백 엔드 서버 풀 두으로 contoso.com에 대 한 트래픽을 제공: 기본 서버 풀 및 이미지 서버 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="07375-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="07375-115">요청에 대 한 http://contoso.com/image *은 tooimage 서버 풀 (imagesBackendPool)를 라우팅할 경로 패턴이 일치 하지 않는 경우 hello, 기본 서버 풀 (appGatewayBackendPool)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![url 경로](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="07375-117">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="07375-117">Log in tooAzure</span></span>

<span data-ttu-id="07375-118">열기 hello **Microsoft Azure 명령 프롬프트**, 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="07375-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="07375-119">사용할 수도 있습니다 `az login` aka.ms/devicelogin에서 코드를 입력 해야 하는 장치 로그인에 대 한 hello 스위치 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="07375-120">앞 예제는 hello를 입력 한 후에 코드가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07375-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="07375-121">Toohttps://aka.ms/devicelogin 브라우저 toocontinue hello 로그인 프로세스에서를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![장치 로그인을 보여 주는 cmd][1]

<span data-ttu-id="07375-123">Hello 브라우저에서 hello 받은 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="07375-124">로그인 페이지로 리디렉션된 tooa 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07375-124">You are redirected tooa sign-in page.</span></span>

![브라우저 tooenter 코드][2]

<span data-ttu-id="07375-126">Hello 코드 입력 되 면 로그인, 닫기 hello 브라우저 toocontinue hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="07375-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![성공적으로 로그인][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="07375-128">경로 기반 규칙 tooan 기존 응용 프로그램 게이트웨이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="07375-129">정의된 경로 규칙을 사용하여 응용 프로그램 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="07375-130">새 백 엔드 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-130">Create a new back-end pool</span></span>

<span data-ttu-id="07375-131">응용 프로그램 게이트웨이 설정 구성 **imagesBackendPool** hello 백 엔드 풀의 hello 부하 분산 된 네트워크 트래픽에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="07375-132">이 예제에서는 새 백 엔드 풀 hello에 대 한 다른 백 엔드 풀 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="07375-133">각 백 엔드 풀에는 고유한 백 엔드 풀 설정이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07375-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="07375-134">백 엔드 HTTP 설정 규칙 tooroute 트래픽 toohello 올바른 백 엔드 풀 멤버에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="07375-135">Hello 프로토콜 및 백 엔드 풀 멤버가 toohello 트래픽을 보낼 때 사용 되는 포트를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="07375-136">쿠키 기반 세션 hello 백 엔드 HTTP 설정에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07375-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="07375-137">쿠키 기반 세션 선호도 트래픽 toohello 보냅니다 설정 된 경우 각 패킷에 대 한 이전 요청으로 동일한 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="07375-138">새 프런트 엔드 포트 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-138">Create a new front-end port</span></span>

<span data-ttu-id="07375-139">Hello 프런트 엔드 포트에 대 한 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="07375-140">hello 프런트 엔드 포트 구성 개체는 hello 수신기에서 트래픽을 hello 응용 프로그램 게이트웨이 수신 포트 기능 수신기 toodefine에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07375-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="07375-141">새 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-141">Create a new listener</span></span>

<span data-ttu-id="07375-142">Hello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-142">Configure hello listener.</span></span> <span data-ttu-id="07375-143">이 단계 hello 공용 IP 주소에 대 한 hello 수신기를 구성 하 고 포트 tooreceive 들어오는 네트워크 트래픽을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07375-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="07375-144">다음 예제는 hello hello 이전에 구성 된 프런트 엔드 IP 구성, 프런트 엔드 포트 구성 및 프로토콜 (http 또는 https)을 사용 하 고 hello 수신기를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="07375-145">이 예제에서는 hello 수신기 tooHTTP 트래픽을 82 hello 공용 IP 주소에서 이전에 생성 된 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="07375-146">Hello Url 경로 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="07375-146">Create hello Url path map</span></span>

<span data-ttu-id="07375-147">Hello 백 엔드 풀에 대 한 규칙 경로 URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="07375-148">이 단계에서 URL 경로 백 엔드 풀을 할당 toohandle hello 들어오는 트래픽을 사이의 응용 프로그램 게이트웨이 toodefine hello 매핑을 사용 하는 hello 상대 경로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07375-149">각 경로로 시작 해야 / hello만 장소는 "\*" hello 끝에를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="07375-150">사용 가능한 예는 /xyz, /xyz* 또는 /xyz/*입니다.</span><span class="sxs-lookup"><span data-stu-id="07375-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="07375-151">hello toohello 경로 검색 도구를 공급 하는 문자열을 다루지 않습니다 텍스트 hello 후 처음 "?" 또는 "#", 및 이러한 문자는 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07375-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="07375-152">hello 다음 예제에서는 하나의 규칙에 대 한 "/ 이미지 / *" 경로 간 tooback "imagesBackendPool" 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="07375-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="07375-153">이 규칙의 url 각 집합에 대 한 트래픽이 라우팅된 toohello 백 엔드 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="07375-154">예를 들어 http://adatum.com/images/figure1.jpg 라인 너무 "imagesBackendPool."</span><span class="sxs-lookup"><span data-stu-id="07375-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="07375-155">Hello 경로 hello 미리 정의 된 경로 규칙이 일치 하지 않으면, hello 규칙 경로 맵 구성도 기본 백 엔드 주소 풀을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="07375-156">예를 들어 http://adatum.com/shoppingcart/test.html가 일치 하지 않는 트래픽에 대 한 hello 기본 풀으로 정의 된 대로 toopool1를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="07375-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07375-157">Next steps</span></span>

<span data-ttu-id="07375-158">Toolearn Secure Sockets Layer (SSL) 오프 로드 하는 방법에 대 한 참조 [SSL 오프 로드에 대 한 응용 프로그램 게이트웨이 구성](application-gateway-ssl-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07375-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
