---
title: "aaaHost Azure 응용 프로그램 게이트웨이 통해 여러 사이트 | Microsoft Docs"
description: "이 페이지에서는 지침 tooconfigure 기존 Azure 응용 프로그램 게이트웨이 hello에서 여러 웹 응용 프로그램에 대 한 Azure 포털 hello로 동일한 게이트웨이에 합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="54b66-103">여러 웹 응용 프로그램을 호스트하는 기존 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="54b66-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54b66-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="54b66-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="54b66-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="54b66-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="54b66-106">여러 사이트 호스팅 사용 하면 하나의 웹 응용 프로그램 둘 이상의 toodeploy hello에 동일한 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="54b66-107">Hello 들어오는 HTTP 요청에는 수신기가 트래픽을 받게 toodetermine 호스트 헤더의 존재 여부에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="54b66-108">hello 수신기는 다음 트래픽 tooappropriate 백 엔드 풀의 hello 게이트웨이 hello 규칙 정의에 구성 된 대로 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="54b66-109">SSL 사용한 웹 응용 프로그램에서 응용 프로그램 게이트웨이 hello SNI 서버 이름 표시 () 확장 toochoose hello 올바른 수신기 hello 웹 트래픽에 대 한 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="54b66-110">여러 사이트 호스팅에 대 한 일반적인 용도는 다른 웹 도메인 toodifferent 백 엔드 서버 풀에 대 한 tooload 잔액 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="54b66-111">마찬가지로 여러 하위 도메인의 hello에 동일한 루트 도메인을 호스팅할 수 또한 동일한 응용 프로그램 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="54b66-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="54b66-112">Scenario</span></span>

<span data-ttu-id="54b66-113">다음 예제는 hello에서 응용 프로그램 게이트웨이으로 두 개의 백 엔드 서버 풀 contoso.com과 fabrikam.com을에 대 한 트래픽을 제공: contoso 서버 풀 및 fabrikam 서버 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="54b66-114">유사한 설정을 app.contoso.com 및 blog.contoso.com와 같은 하위 도메인을 사용 하는 toohost 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![다중 사이트 시나리오][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="54b66-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="54b66-116">Before you begin</span></span>

<span data-ttu-id="54b66-117">이 시나리오는 멀티 사이트 지원 tooan 기존 응용 프로그램 게이트웨이 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-117">This scenario adds multi-site support tooan existing application gateway.</span></span> <span data-ttu-id="54b66-118">toocomplete이이 시나리오에서는 기존 응용 프로그램 게이트웨이 toobe 사용 가능한 tooconfigure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-118">toocomplete this scenario, an existing application gateway needs toobe available tooconfigure.</span></span> <span data-ttu-id="54b66-119">방문 [hello 포털을 사용 하 여 응용 프로그램 게이트웨이 만들](application-gateway-create-gateway-portal.md) toolearn 어떻게 toocreate hello 포털에서 기본 응용 프로그램 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-119">Visit [Create an application gateway by using hello portal](application-gateway-create-gateway-portal.md) toolearn how toocreate a basic application gateway in hello portal.</span></span>

<span data-ttu-id="54b66-120">hello 다음은 tooupdate hello 응용 프로그램 게이트웨이 위해 필요한 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-120">hello following are hello steps needed tooupdate hello application gateway:</span></span>

1. <span data-ttu-id="54b66-121">각 사이트에 대 한 백 엔드 풀 toouse를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-121">Create back-end pools toouse for each site.</span></span>
2. <span data-ttu-id="54b66-122">각 사이트 Application Gateway에서 지원할 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="54b66-123">Hello 적절 한 백 엔드 사용 규칙 toomap 각 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-123">Create rules toomap each listener with hello appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="54b66-124">요구 사항</span><span class="sxs-lookup"><span data-stu-id="54b66-124">Requirements</span></span>

* <span data-ttu-id="54b66-125">**백 엔드 서버 풀:** hello hello 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-125">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="54b66-126">나열 된 hello IP 주소 하거나 toohello 가상 네트워크 서브넷에 속해야 하거나 공용 IP/VIP가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-126">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="54b66-127">FQDN을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-127">FQDN can also be used.</span></span>
* <span data-ttu-id="54b66-128">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="54b66-129">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="54b66-130">**프런트 엔드 포트:** 이 포트는 hello 응용 프로그램 게이트웨이에 열려 있는 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-130">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="54b66-131">트래픽이이 포트에 도달 하 고 가져옵니다 hello 백 엔드 서버의 tooone 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-131">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="54b66-132">**수신기:** hello 수신기에는 프런트 엔드 포트 프로토콜 (Http 또는 Https의 경우, 이러한 값은 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="54b66-132">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="54b66-133">다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="54b66-134">**규칙:** hello 규칙 hello 수신기를 hello 백 엔드 서버 풀에 바인딩하고 정의 백 엔드 서버 풀 hello 트래픽을 특정 수신기 페이로드만 directed toowhen 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-134">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="54b66-135">트래픽 구체적인 정도 관계 없이 일치 하는 hello 첫 번째 규칙을 통해 이동 됩니다 및 규칙 나열 된 hello 순서로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-135">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="54b66-136">예를 들어 기본 수신기를 사용 하 여 규칙과 동일한 포트를 사용 하는 hello 규칙 hello에서 모두 다중 사이트 수신기를 사용 하 여 규칙을 설정한 경우 hello 다중 사이트 수신기 해야 보다 먼저 나열 되어야 hello 규칙으로 다중 사이트 규칙 toofunction hello에 대 한 순서 대로 기본 수신기 hello와 가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span> 
* <span data-ttu-id="54b66-137">**인증서:** 각 수신기에는 고유한 인증서가 필요하며, 이 예에서는 다중 사이트의 수신기가 2개 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="54b66-138">두 개의.pfx 인증서와 해당에 대 한 hello 암호 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-138">Two .pfx certificates and hello passwords for them need toobe created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="54b66-139">각 사이트에 사용할 백 엔드 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="54b66-139">Create back-end pools for each site</span></span>

<span data-ttu-id="54b66-140">Application Gateway에서 지원할 각 사이트에는 백 엔드 풀이 필요합니다. 이 예에서는 2개 백 엔드 풀, 즉 하나는 contoso11.com, 다른 하나는 fabrikam11.com의 백 엔드 풀이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="54b66-141">1단계</span><span class="sxs-lookup"><span data-stu-id="54b66-141">Step 1</span></span>

<span data-ttu-id="54b66-142">Azure 포털 (https://portal.azure.com) hello에 tooan 기존 응용 프로그램 게이트웨이 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-142">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="54b66-143">**백엔드 풀**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-143">Select **Backend pools** and click **Add**</span></span>

![백 엔드 풀 추가][7]

### <a name="step-2"></a><span data-ttu-id="54b66-145">2단계</span><span class="sxs-lookup"><span data-stu-id="54b66-145">Step 2</span></span>

<span data-ttu-id="54b66-146">Hello 백 엔드 풀에 대 한 hello 정보를 입력 **pool1**hello 백 엔드 서버에 대 한 hello ip 주소 또는 Fqdn을 추가 하 고 클릭, **확인**</span><span class="sxs-lookup"><span data-stu-id="54b66-146">Fill in hello information for hello back-end pool **pool1**, adding hello ip addresses or FQDNs for hello back-end servers and click **OK**</span></span>

![pool1 백엔드 풀 설정][8]

### <a name="step-3"></a><span data-ttu-id="54b66-148">3단계</span><span class="sxs-lookup"><span data-stu-id="54b66-148">Step 3</span></span>

<span data-ttu-id="54b66-149">Hello 백 엔드 풀 블레이드에서 클릭 **추가** tooadd 프로그램 추가 백 엔드 풀 **pool2**hello 백 엔드 서버에 대 한 hello ip 주소 또는 FQDN을 추가 하 고 클릭, **확인**</span><span class="sxs-lookup"><span data-stu-id="54b66-149">On hello backend-pools blade click **Add** tooadd an additional back-end pool **pool2**, adding hello ip addresses or FQDNS for hello back-end servers and click **OK**</span></span>

![pool2 백엔드 풀 설정][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="54b66-151">각 백 엔드 풀의 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="54b66-151">Create listeners for each back-end</span></span>

<span data-ttu-id="54b66-152">응용 프로그램 게이트웨이 HTTP 1.1 사용 한 웹 사이트에 둘 이상의 호스트 헤더 toohost hello 동일한 공용 IP 주소 및 포트.</span><span class="sxs-lookup"><span data-stu-id="54b66-152">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="54b66-153">hello 기본 수신기 hello 포털에서 만들어진이 속성이 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-153">hello basic listener created in hello portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="54b66-154">1단계</span><span class="sxs-lookup"><span data-stu-id="54b66-154">Step 1</span></span>

<span data-ttu-id="54b66-155">클릭 **수신기** 기존 응용 프로그램 게이트웨이 hello 되 고 클릭 **다중 사이트** tooadd hello에 대 한 첫 번째 수신기입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-155">Click **Listeners** on hello existing application gateway and click **Multi-site** tooadd hello first listener.</span></span>

![수신기 개요 블레이드][1]

### <a name="step-2"></a><span data-ttu-id="54b66-157">2단계</span><span class="sxs-lookup"><span data-stu-id="54b66-157">Step 2</span></span>

<span data-ttu-id="54b66-158">Hello 수신기에 대 한 hello 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-158">Fill out hello information for hello listener.</span></span> <span data-ttu-id="54b66-159">이 예에서는 SSL 종료를 구성하고 새 프런트 엔드 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="54b66-160">SSL 종료에 사용 되는 hello.pfx 인증서 toobe를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-160">Upload hello .pfx certificate toobe used for SSL termination.</span></span> <span data-ttu-id="54b66-161">이 블레이드 비교 toohello 표준 기본 수신기 블레이드에서 hello 유일한 차이는 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-161">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span>

![수신기 속성 블레이드][2]

### <a name="step-3"></a><span data-ttu-id="54b66-163">3단계</span><span class="sxs-lookup"><span data-stu-id="54b66-163">Step 3</span></span>

<span data-ttu-id="54b66-164">클릭 **다중 사이트** hello 두 번째 사이트에 대 한 hello 이전 단계에 설명 된 대로 다른 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-164">Click **Multi-site** and create another listener as described in hello previous step for hello second site.</span></span> <span data-ttu-id="54b66-165">있는지 toouse hello 두 번째 수신기에 대 한 다른 인증서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-165">Make sure toouse a different certificate for hello second listener.</span></span> <span data-ttu-id="54b66-166">이 블레이드 비교 toohello 표준 기본 수신기 블레이드에서 hello 유일한 차이는 hello 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-166">hello only difference on this blade compared toohello standard basic listener blade is hello hostname.</span></span> <span data-ttu-id="54b66-167">Hello 수신기에 대 한 hello 정보를 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-167">Fill out hello information for hello listener and click **OK**.</span></span>

![수신기 속성 블레이드][3]

> [!NOTE]
> <span data-ttu-id="54b66-169">Hello 응용 프로그램 게이트웨이 용 Azure 포털의에서 수신기 생성은 장기 실행 작업, 소요 시간 toocreate hello 일부 두 수신기가이 시나리오에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-169">Creation of listeners in hello Azure portal for application gateway is a long running task, it may take some time toocreate hello two listeners in this scenario.</span></span> <span data-ttu-id="54b66-170">경우 전체 hello 수신기 hello 다음 이미지와 같이 hello 포털에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-170">When complete hello listeners show in hello portal as seen in hello following image:</span></span>

![수신기 개요][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a><span data-ttu-id="54b66-172">규칙 toomap 수신기 toobackend 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="54b66-172">Create rules toomap listeners toobackend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="54b66-173">1단계</span><span class="sxs-lookup"><span data-stu-id="54b66-173">Step 1</span></span>

<span data-ttu-id="54b66-174">Azure 포털 (https://portal.azure.com) hello에 tooan 기존 응용 프로그램 게이트웨이 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-174">Navigate tooan existing application gateway in hello Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="54b66-175">선택 **규칙** hello 기존 기본 규칙을 선택 하 고 **rule1** 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-175">Select **Rules** and choose hello existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="54b66-176">2단계</span><span class="sxs-lookup"><span data-stu-id="54b66-176">Step 2</span></span>

<span data-ttu-id="54b66-177">다음 이미지는 hello와 같이 hello 규칙 블레이드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-177">Fill out hello rules blade as seen in hello following image.</span></span> <span data-ttu-id="54b66-178">첫 번째 수신기 hello 및 첫 번째 풀을 선택 하 고 클릭 하면 **저장** 완료 된 경우.</span><span class="sxs-lookup"><span data-stu-id="54b66-178">Choosing hello first listener and first pool and clicking **Save** when complete.</span></span>

![기존 규칙 편집][6]

### <a name="step-3"></a><span data-ttu-id="54b66-180">3단계</span><span class="sxs-lookup"><span data-stu-id="54b66-180">Step 3</span></span>

<span data-ttu-id="54b66-181">클릭 **기본 규칙** toocreate hello에 대 한 두 번째 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-181">Click **Basic rule** toocreate hello second rule.</span></span> <span data-ttu-id="54b66-182">Hello 두 번째 수신기 및 두 번째 백 엔드 풀과 hello 양식을 작성 하 고 클릭 **확인** toosave 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-182">Fill out hello form with hello second listener and second backend pool and click **OK** toosave.</span></span>

![기본 규칙 추가 블레이드][10]

<span data-ttu-id="54b66-184">이 시나리오를 완료 hello Azure 포털을 통한 멀티 사이트 지원을 사용 하 여 기존 응용 프로그램 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="54b66-184">This scenario completes configuring an existing application gateway with multi-site support through hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54b66-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="54b66-185">Next steps</span></span>

<span data-ttu-id="54b66-186">자세한 내용은 방법 tooprotect와 웹 사이트 [응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="54b66-186">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
