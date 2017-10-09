---
title: "Mobile Engagement REST Api와 aaaAuthenticate"
description: "설명 방법을 tooauthenticate Azure Mobile Engagement REST Api와"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="09588-103">Mobile Engagement REST API를 사용한 인증</span><span class="sxs-lookup"><span data-stu-id="09588-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="09588-104">개요</span><span class="sxs-lookup"><span data-stu-id="09588-104">Overview</span></span>
<span data-ttu-id="09588-105">이 문서에서는 tooget 유효한 AAD Oauth hello Mobile Engagement REST Api로 tooauthenticate 토큰 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="09588-106">여러분이 유효한 Azure 구독을 보유하고 있고 [개발자 자습서](mobile-engagement-windows-store-dotnet-get-started.md)중 하나를 사용하여 Mobile Engagement 앱을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="09588-107">인증</span><span class="sxs-lookup"><span data-stu-id="09588-107">Authentication</span></span>
<span data-ttu-id="09588-108">Microsoft Azure Active Directory 기반 OAuth 토큰을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="09588-109">주문 tooauthentication API 요청에 권한 부여 헤더 hello 다음 폼의 tooevery 요청을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="09588-110">Azure Active Directory 토큰은 1시간 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="09588-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="09588-111">토큰은 몇 가지 방법으로 tooget 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-111">There are several ways tooget a token.</span></span> <span data-ttu-id="09588-112">Api는 일반적으로 클라우드 서비스에서 호출 하는 hello, 이후 toouse API 키 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="09588-113">Azure 용어에서는 API 키를 서비스 주체 암호라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="09588-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="09588-114">hello 다음 절차에서는 한 가지 방법은 toosetting 것 수동으로 위로 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="09588-115">일 회 설정(스크립트 사용)</span><span class="sxs-lookup"><span data-stu-id="09588-115">One-time setup (using script)</span></span>
<span data-ttu-id="09588-116">Hello 일련의 설치에 대 한 최소 시간 hello 걸리지만 hello 가장 허용 가능한 기본값을 사용 하는 PowerShell 스크립트를 사용 하 여 tooperform hello 설정 아래 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="09588-117">필요에 따라 있습니다 수 또한 hello 지침에에서 따라 hello [수동 설치](mobile-engagement-api-authentication-manual.md) hello Azure 포털에 직접 및 do 더욱 세밀 하 게 구성에서 이러한 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="09588-118">PowerShell에서 Azure의 hello 최신 버전 가져오기 [여기](http://aka.ms/webpi-azps)합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="09588-119">Hello 다운로드 명령에 대 한 자세한 내용은 볼 수 있습니다 [링크](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="09588-120">사용 하 여 hello 다음 hello 있다고 tooensure 명령을 Azure PowerShell 설치 되 면 **Azure 모듈** 설치:</span><span class="sxs-lookup"><span data-stu-id="09588-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="09588-121">a.</span><span class="sxs-lookup"><span data-stu-id="09588-121">a.</span></span> <span data-ttu-id="09588-122">Hello Azure PowerShell 모듈을 사용할 수 있는 모듈의 hello 목록에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![사용 가능한 Azure 모듈][1]
   
    <span data-ttu-id="09588-124">b.</span><span class="sxs-lookup"><span data-stu-id="09588-124">b.</span></span> <span data-ttu-id="09588-125">목록 위의 hello에 hello Azure PowerShell 모듈을 찾지 못한 경우 toorun hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="09588-126">로그인 toohello PowerShell에서 Azure 리소스 관리자를 실행 하 여 Azure 계정에 대 한 사용자 이름 및 암호를 제공 하 고 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="09588-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="09588-127">여러 구독이 있는 경우 hello 다음을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="09588-128">a.</span><span class="sxs-lookup"><span data-stu-id="09588-128">a.</span></span> <span data-ttu-id="09588-129">모든 구독 및 복사 hello 원하는 hello 구독의 구독 Id의 목록을 toouse를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="09588-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="09588-130">이 구독에는 Mobile Engagement 앱 hello 갖는 동일 hello 인지 확인 사용 하 여 toointeract hello Api입니다.</span><span class="sxs-lookup"><span data-stu-id="09588-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="09588-131">b.</span><span class="sxs-lookup"><span data-stu-id="09588-131">b.</span></span> <span data-ttu-id="09588-132">실행된 hello 다음 명령은 사용 제공 hello SubscriptionId tooconfigure hello 구독 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="09588-133">Hello에 대 한 hello 텍스트 복사 [새로 AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour 로컬 컴퓨터를 스크립트 및 PowerShell cmdlet으로 저장 (예: `APIAuth.ps1`) 하 고 실행 `.\APIAuth.ps1`합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="09588-134">hello 스크립트 묻는 메시지가 나타납니다에 대 한 입력은 tooprovide **principalName**합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="09588-135">되도록 toouse toocreate Active Directory 응용 프로그램 (예: APIAuth) 적절 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="09588-136">Hello 다음 해야 하는 4 개의 값이 표시 됩니다 hello 스크립트를 완료 한 후 tooauthenticate AD 사용한 프로그래밍 방식으로 만들어지므로 toocopy 있는지를 확인 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="09588-137">**TenantId**, **SubscriptionId**, **ApplicationId** 및 **Secret**입니다.</span><span class="sxs-lookup"><span data-stu-id="09588-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="09588-138">TenantId를 `{TENANT_ID}`로, ApplicationId `{CLIENT_ID}`로, Secret을 `{CLIENT_SECRET}`으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09588-139">PowerShell 스크립트를 실행할 수 없도록 기본 보안 정책이 설정되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="09588-140">따라서 일시적으로 구성한 경우 다음 명령을 hello를 사용 하 여 실행 정책 tooallow 스크립트 실행:</span><span class="sxs-lookup"><span data-stu-id="09588-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="09588-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="09588-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="09588-142">같은 PS cmdlet 집합이 hello 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="09588-143">새 AD 응용 프로그램 만들어졌는지 hello 이름의 있습니다 toohello 스크립트 호출 제공 hello Azure 관리 포털에서 확인 **principalName** 아래 **회사가 보유 한 응용 프로그램 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="09588-144">단계 tooget 유효한 토큰</span><span class="sxs-lookup"><span data-stu-id="09588-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="09588-145">매개 변수 뒤 hello로 hello API를 호출 하 고 있는지 tooreplace hello 테 넌 트\_ID, 클라이언트\_ID와 클라이언트\_암호:</span><span class="sxs-lookup"><span data-stu-id="09588-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="09588-146">**요청 URL** *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="09588-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="09588-147">**application/x-www-form-urlencoded** 인 *HTTP 콘텐츠 형식 헤더*</span><span class="sxs-lookup"><span data-stu-id="09588-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="09588-148">**HTTP 요청 본문** *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="09588-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="09588-149">hello 다음은 예제 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="09588-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="09588-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="09588-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="09588-151">다음은 응답 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="09588-151">Here is an example response:</span></span>
     
       <span data-ttu-id="09588-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="09588-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="09588-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="09588-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="09588-154">이 예제에서는 hello POST 매개 변수의 URL 인코딩을 포함 `resource` 값이 실제로 `https://management.core.windows.net/`합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="09588-155">Tooalso URL 인코딩할 조심 `{CLIENT_SECRET}` 으로 특수 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="09588-156">테스트를 위해 [Fiddler](http://www.telerik.com/fiddler) 또는 [Chrome Postman 확장](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)과 같은 HTTP 클라이언트 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="09588-157">이제 모든 API 호출에서 hello 권한 부여 요청 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="09588-158">반환 401 상태 코드 검사 hello 응답 본문을 발생 하는 경우 것 알려 hello 토큰이 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="09588-159">토큰이 만료된 경우 새 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="09588-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="09588-160">Hello Api를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="09588-160">Using hello APIs</span></span>
<span data-ttu-id="09588-161">유효한 토큰을가지고 준비 toomake hello API 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09588-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="09588-162">각 API 요청 toopass hello 이전 섹션에서 받은 되는 유효 하 고 만료 되지 않은 토큰을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="09588-163">일부 매개 변수에서 tooplug hello 요청 응용 프로그램을 식별 하는 URI에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="09588-164">hello 요청 URI hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="09588-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="09588-165">tooget hello 매개 변수를 응용 프로그램 이름을 클릭 하 고 대시보드를 클릭 하 고 모든 hello 다음 3 개의 매개 변수를 hello와 같은 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09588-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="09588-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="09588-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="09588-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="09588-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="09588-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="09588-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="09588-169">**4** your 리소스 그룹 이름은 toobe 되기 **MobileEngagement** 만들지 않은 경우 새 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI 매개 변수][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="09588-171">이 hello에 대 한 API 루트 주소 hello 무시 이전 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="09588-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="09588-172">Azure 클래식 포털을 사용 하 여 hello 응용 프로그램을 만든 경우 hello 응용 프로그램 이름 자체 보다 다른 toouse hello 응용 프로그램 리소스 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="09588-173">Hello 앱 hello Azure 포털에서에서 만든 경우 응용 프로그램 이름 (응용 프로그램 리소스 이름 및 hello 새로운 포털에서 만든 앱에 대 한 응용 프로그램 이름 구분 되지 않습니다는) 자체 hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09588-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



