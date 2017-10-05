---
title: "Azure Application Gateway에서 여러 사이트 호스트 | Microsoft Docs"
description: "이 문서에서는 Azure 포털을 통해 동일한 게이트웨이에서 여러 웹 응용 프로그램을 호스트하는 기존 Azure 응용 프로그램 게이트웨이를 구성하는 지침을 제공합니다."
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
ms.openlocfilehash: 84bd62ae17b7f7ba4cd815ef1f9880679607ebce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="a81bb-103">여러 웹 응용 프로그램을 호스트하는 기존 응용 프로그램 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="a81bb-103">Configure an existing application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a81bb-104">쉬운 테이블</span><span class="sxs-lookup"><span data-stu-id="a81bb-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="a81bb-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a81bb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

<span data-ttu-id="a81bb-106">다중 사이트 호스팅을 통해 둘 이상의 웹 응용 프로그램을 동일한 응용 프로그램 게이트웨이에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="a81bb-107">들어오는 HTTP 요청의 호스트 헤더 존재 여부에 따라 트래픽을 수신할 수신기가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="a81bb-108">그런 다음 수신기는 게이트웨이 규칙 정의에 구성된 대로 적절한 백 엔드 풀로 트래픽을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="a81bb-109">SSL 사용 웹 응용 프로그램에서 응용 프로그램 게이트웨이는 SNI(서버 이름 표시) 확장에 의존하여 웹 트래픽에 대한 올바른 수신기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="a81bb-110">다중 사이트 호스팅의 일반적인 용도는 여러 웹 도메인에 대한 요청의 부하를 여러 백 엔드 서버 풀에 분산하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="a81bb-111">마찬가지로 같은 루트 도메인의 여러 하위 도메인을 동일한 응용 프로그램 게이트웨이에서 호스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="a81bb-112">시나리오</span><span class="sxs-lookup"><span data-stu-id="a81bb-112">Scenario</span></span>

<span data-ttu-id="a81bb-113">다음 예제에서 응용 프로그램 게이트웨이는 두 개의 백 엔드 서버 풀(contoso 서버 풀 및 fabrikam 서버 풀)을 통해 contoso.com 및 fabrikam.com에 대한 트래픽을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="a81bb-114">유사한 설정을 사용하여 app.contoso.com 및 blog.contoso.com과 같은 하위 도메인을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![다중 사이트 시나리오][multisite]

## <a name="before-you-begin"></a><span data-ttu-id="a81bb-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="a81bb-116">Before you begin</span></span>

<span data-ttu-id="a81bb-117">이 시나리오에서는 기존 응용 프로그램 게이트웨이에 다중 사이트 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-117">This scenario adds multi-site support to an existing application gateway.</span></span> <span data-ttu-id="a81bb-118">이 시나리오를 완료하려면 기존 Application Gateway를 구성할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-118">To complete this scenario, an existing application gateway needs to be available to configure.</span></span> <span data-ttu-id="a81bb-119">[포털을 사용하여 응용 프로그램 게이트웨이 만들기](application-gateway-create-gateway-portal.md)를 참조하여 포털에서 기본 응용 프로그램 게이트웨이를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-119">Visit [Create an application gateway by using the portal](application-gateway-create-gateway-portal.md) to learn how to create a basic application gateway in the portal.</span></span>

<span data-ttu-id="a81bb-120">응용 프로그램 게이트웨이를 만드는 데 필요한 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-120">The following are the steps needed to update the application gateway:</span></span>

1. <span data-ttu-id="a81bb-121">각 사이트에 사용할 백 엔드 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-121">Create back-end pools to use for each site.</span></span>
2. <span data-ttu-id="a81bb-122">각 사이트 Application Gateway에서 지원할 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-122">Create a listener for each site application gateway supports.</span></span>
3. <span data-ttu-id="a81bb-123">각 수신기를 적절한 백 엔드에 매핑하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-123">Create rules to map each listener with the appropriate back-end.</span></span>

## <a name="requirements"></a><span data-ttu-id="a81bb-124">요구 사항</span><span class="sxs-lookup"><span data-stu-id="a81bb-124">Requirements</span></span>

* <span data-ttu-id="a81bb-125">**백 엔드 서버 풀:** 백 엔드 서버의 IP 주소 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="a81bb-126">나열된 IP 주소는 가상 네트워크 서브넷에 속하거나 공용 IP/VIP이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="a81bb-127">FQDN을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-127">FQDN can also be used.</span></span>
* <span data-ttu-id="a81bb-128">**백 엔드 서버 풀 설정:** 모든 풀에는 포트, 프로토콜 및 쿠키 기반의 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a81bb-129">이러한 설정은 풀에 연결 및 풀 내의 모든 서버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="a81bb-130">**프런트 엔드 포트:** 이 포트는 응용 프로그램 게이트웨이에 열려 있는 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="a81bb-131">트래픽이 이 포트에 도달하면, 백 엔드 서버 중의 하나로 리디렉트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="a81bb-132">**수신기:** 수신기에는 프런트 엔드 포트, 프로토콜(Http 또는 Https, 이 값은 대/소문자 구분) 및 SSL 인증서 이름(SSL 오프로드를 구성하는 경우)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="a81bb-133">다중 사이트 지원 응용 프로그램 게이트웨이의 경우 호스트 이름 및 SNI 표시도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-133">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="a81bb-134">**규칙:** 규칙은 수신기와 백 엔드 서버 풀을 바인딩하고 특정 수신기에 도달했을 때 트래픽이 전달되어야 하는 백 엔드 서버 풀을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-134">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="a81bb-135">규칙은 나열된 순서대로 처리되고 트래픽은 특이성에 관계없이 일치하는 첫 번째 규칙을 통해 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-135">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="a81bb-136">예를 들어 기본 수신기를 사용하는 규칙과 다중 사이트 수신기를 사용하는 규칙이 둘 다 같은 포트에 있는 경우 다중 사이트 규칙이 예상대로 작동하려면 다중 사이트 수신기를 사용하는 규칙은 기본 수신기를 사용하는 규칙 앞에 나열되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-136">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span> 
* <span data-ttu-id="a81bb-137">**인증서:** 각 수신기에는 고유한 인증서가 필요하며, 이 예에서는 다중 사이트의 수신기가 2개 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-137">**Certificates:** Each listener requires a unique certificate, in this example 2 listeners are created for multi-site.</span></span> <span data-ttu-id="a81bb-138">이 수신기에 대해 2개의 .pfx 인증서와 해당 암호를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-138">Two .pfx certificates and the passwords for them need to be created.</span></span>

## <a name="create-back-end-pools-for-each-site"></a><span data-ttu-id="a81bb-139">각 사이트에 사용할 백 엔드 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="a81bb-139">Create back-end pools for each site</span></span>

<span data-ttu-id="a81bb-140">Application Gateway에서 지원할 각 사이트에는 백 엔드 풀이 필요합니다. 이 예에서는 2개 백 엔드 풀, 즉 하나는 contoso11.com, 다른 하나는 fabrikam11.com의 백 엔드 풀이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-140">A back-end pool for each site that application gateway supports is needed, in this case 2 are be created, one for contoso11.com and one for fabrikam11.com.</span></span>

### <a name="step-1"></a><span data-ttu-id="a81bb-141">1단계:</span><span class="sxs-lookup"><span data-stu-id="a81bb-141">Step 1</span></span>

<span data-ttu-id="a81bb-142">Azure 포털 ( https://portal.azure.com ) 에서 기존 응용 프로그램 게이트웨이로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-142">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="a81bb-143">**백엔드 풀**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-143">Select **Backend pools** and click **Add**</span></span>

![백 엔드 풀 추가][7]

### <a name="step-2"></a><span data-ttu-id="a81bb-145">2단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-145">Step 2</span></span>

<span data-ttu-id="a81bb-146">**pool1** 백 엔드 풀에 대한 정보를 입력하고(백 엔드 서버의 경우 IP 주소 또는 FQDN을 추가함) **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-146">Fill in the information for the back-end pool **pool1**, adding the ip addresses or FQDNs for the back-end servers and click **OK**</span></span>

![pool1 백엔드 풀 설정][8]

### <a name="step-3"></a><span data-ttu-id="a81bb-148">3단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-148">Step 3</span></span>

<span data-ttu-id="a81bb-149">백 엔드 풀 블레이드에서 **추가**를 클릭하여 **pool2** 백 엔드 풀을 추가하고(백 엔드 서버의 경우 IP 주소 또는 FQDN을 추가함) **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-149">On the backend-pools blade click **Add** to add an additional back-end pool **pool2**, adding the ip addresses or FQDNS for the back-end servers and click **OK**</span></span>

![pool2 백엔드 풀 설정][9]

## <a name="create-listeners-for-each-back-end"></a><span data-ttu-id="a81bb-151">각 백 엔드 풀의 수신기 만들기</span><span class="sxs-lookup"><span data-stu-id="a81bb-151">Create listeners for each back-end</span></span>

<span data-ttu-id="a81bb-152">응용 프로그램 게이트웨이는 HTTP 1.1 호스트 헤더를 기반으로 동일한 공용 IP 주소 및 포트에서 둘 이상의 웹 사이트를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-152">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="a81bb-153">포털에서 만든 기본 수신기에는 이 속성이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-153">The basic listener created in the portal does not contain this property.</span></span>

### <a name="step-1"></a><span data-ttu-id="a81bb-154">1단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-154">Step 1</span></span>

<span data-ttu-id="a81bb-155">기존 응용 프로그램 게이트웨이에서 **수신기**를 클릭하고 **다중 사이트**를 클릭하여 첫 번째 수신기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-155">Click **Listeners** on the existing application gateway and click **Multi-site** to add the first listener.</span></span>

![수신기 개요 블레이드][1]

### <a name="step-2"></a><span data-ttu-id="a81bb-157">2단계:</span><span class="sxs-lookup"><span data-stu-id="a81bb-157">Step 2</span></span>

<span data-ttu-id="a81bb-158">수신기의 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-158">Fill out the information for the listener.</span></span> <span data-ttu-id="a81bb-159">이 예에서는 SSL 종료를 구성하고 새 프런트 엔드 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-159">In this example SSL termination is configured, create a new frontend port.</span></span> <span data-ttu-id="a81bb-160">SSL 종료에 사용할 .pfx 인증서를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-160">Upload the .pfx certificate to be used for SSL termination.</span></span> <span data-ttu-id="a81bb-161">이 블레이드와 표준 기본 수신기 블레이드 사이의 유일한 차이점은 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-161">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span>

![수신기 속성 블레이드][2]

### <a name="step-3"></a><span data-ttu-id="a81bb-163">3단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-163">Step 3</span></span>

<span data-ttu-id="a81bb-164">**다중 사이트**를 클릭하고 이전 단계에서 설명한 대로 두 번째 사이트의 다른 수신기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-164">Click **Multi-site** and create another listener as described in the previous step for the second site.</span></span> <span data-ttu-id="a81bb-165">두 번째 수신기에 대해 별도의 인증서를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-165">Make sure to use a different certificate for the second listener.</span></span> <span data-ttu-id="a81bb-166">이 블레이드와 표준 기본 수신기 블레이드 사이의 유일한 차이점은 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-166">The only difference on this blade compared to the standard basic listener blade is the hostname.</span></span> <span data-ttu-id="a81bb-167">수신기의 정보를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-167">Fill out the information for the listener and click **OK**.</span></span>

![수신기 속성 블레이드][3]

> [!NOTE]
> <span data-ttu-id="a81bb-169">Azure 포털에서 응용 프로그램 게이트웨이의 수신기를 만드는 것은 장기 실행 작업이므로 이 시나리오에서 두 수신기를 만드는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-169">Creation of listeners in the Azure portal for application gateway is a long running task, it may take some time to create the two listeners in this scenario.</span></span> <span data-ttu-id="a81bb-170">수신기가 완료되면 포털에서 다음 이미지와 같이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-170">When complete the listeners show in the portal as seen in the following image:</span></span>

![수신기 개요][4]

## <a name="create-rules-to-map-listeners-to-backend-pools"></a><span data-ttu-id="a81bb-172">백 엔드 풀에 수신기를 매핑하는 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="a81bb-172">Create rules to map listeners to backend pools</span></span>

### <a name="step-1"></a><span data-ttu-id="a81bb-173">1단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-173">Step 1</span></span>

<span data-ttu-id="a81bb-174">Azure 포털 ( https://portal.azure.com ) 에서 기존 응용 프로그램 게이트웨이로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-174">Navigate to an existing application gateway in the Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="a81bb-175">**규칙**을 선택하고 **rule1** 기존 기본 규칙을 선택한 다음 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-175">Select **Rules** and choose the existing default rule **rule1** and click **Edit**.</span></span>

### <a name="step-2"></a><span data-ttu-id="a81bb-176">2단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-176">Step 2</span></span>

<span data-ttu-id="a81bb-177">다음 그림과 같이 규칙 블레이드에서 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-177">Fill out the rules blade as seen in the following image.</span></span> <span data-ttu-id="a81bb-178">첫 번째 수신기와 첫 번째 풀을 선택하고, 완료하는 경우 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-178">Choosing the first listener and first pool and clicking **Save** when complete.</span></span>

![기존 규칙 편집][6]

### <a name="step-3"></a><span data-ttu-id="a81bb-180">3단계:</span><span class="sxs-lookup"><span data-stu-id="a81bb-180">Step 3</span></span>

<span data-ttu-id="a81bb-181">**기본 규칙**을 클릭하여 두 번째 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-181">Click **Basic rule** to create the second rule.</span></span> <span data-ttu-id="a81bb-182">두 번째 수신기와 두 번째 백 엔드 풀로 양식을 작성하고 **확인**을 클릭하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-182">Fill out the form with the second listener and second backend pool and click **OK** to save.</span></span>

![기본 규칙 추가 블레이드][10]

<span data-ttu-id="a81bb-184">이 시나리오는 Azure 포털을 통해 다중 사이트 지원을 사용하도록 기존 Application Gateway의 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-184">This scenario completes configuring an existing application gateway with multi-site support through the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a81bb-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a81bb-185">Next steps</span></span>

<span data-ttu-id="a81bb-186">[응용 프로그램 게이트웨이-웹 응용 프로그램 방화벽](application-gateway-webapplicationfirewall-overview.md)을 사용하여 웹 사이트를 보호하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a81bb-186">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

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
