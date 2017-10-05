---
title: "Mobile Engagement REST API를 사용한 인증"
description: "Azure Mobile Engagement REST API를 사용한 인증 방법 설명"
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
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="fd5d5-103">Mobile Engagement REST API를 사용한 인증</span><span class="sxs-lookup"><span data-stu-id="fd5d5-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="fd5d5-104">개요</span><span class="sxs-lookup"><span data-stu-id="fd5d5-104">Overview</span></span>
<span data-ttu-id="fd5d5-105">이 문서에서는 REST API를 사용하여 Mobile Engagement를 인증하도록 유효한 AAD Oauth 토큰을 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="fd5d5-106">여러분이 유효한 Azure 구독을 보유하고 있고 [개발자 자습서](mobile-engagement-windows-store-dotnet-get-started.md)중 하나를 사용하여 Mobile Engagement 앱을 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="fd5d5-107">인증</span><span class="sxs-lookup"><span data-stu-id="fd5d5-107">Authentication</span></span>
<span data-ttu-id="fd5d5-108">Microsoft Azure Active Directory 기반 OAuth 토큰을 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="fd5d5-109">API 요청을 인증하려면 다음 형식인 모든 요청에 인증 헤더를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="fd5d5-110">Azure Active Directory 토큰은 1시간 후에 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="fd5d5-111">토큰을 얻는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-111">There are several ways to get a token.</span></span> <span data-ttu-id="fd5d5-112">API가 일반적으로 클라우드 서비스에서 호출되므로 API 키를 사용하려 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="fd5d5-113">Azure 용어에서는 API 키를 서비스 주체 암호라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="fd5d5-114">다음은 키를 수동으로 설정하는 방법을 설명하는 절차입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="fd5d5-115">일 회 설정(스크립트 사용)</span><span class="sxs-lookup"><span data-stu-id="fd5d5-115">One-time setup (using script)</span></span>
<span data-ttu-id="fd5d5-116">설치에 대한 최소 시간이 걸리지만 허용될 수 있는 기본값을 사용하는 PowerShell 스크립트를 사용하여 설치를 수행하려면 아래 일련의 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="fd5d5-117">필요에 따라  Azure 포털에서 이를 직접 수행하기 위해 [수동 설치](mobile-engagement-api-authentication-manual.md) 의 지침에 따르고 세밀하게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="fd5d5-118">[여기](http://aka.ms/webpi-azps)에서 Azure PowerShell 최신 버전을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="fd5d5-119">다운로드 지침에 대한 자세한 내용은 [링크](/powershell/azure/overview)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="fd5d5-120">Azure PowerShell을 설치하면 다음 명령을 사용하여 **Azure 모듈** 을 설치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="fd5d5-121">a.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-121">a.</span></span> <span data-ttu-id="fd5d5-122">사용할 수 있는 모듈 목록에서 Azure PowerShell 모듈을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![사용 가능한 Azure 모듈][1]
   
    <span data-ttu-id="fd5d5-124">b.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-124">b.</span></span> <span data-ttu-id="fd5d5-125">위 목록에서 Azure PowerShell 모듈을 찾지 못한 경우 다음을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="fd5d5-126">다음 명령을 실행하고 Azure 계정에 사용자 이름 및 암호를 제공하여 PowerShell에서 Azure Resource Manager에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="fd5d5-127">여러 구독이 있다면 다음을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="fd5d5-128">a.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-128">a.</span></span> <span data-ttu-id="fd5d5-129">모든 구독 목록을 가져오고 사용하려는 구독의 SubscriptionId를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="fd5d5-130">API를 사용하여 상호 작용할 Mobile Engagement 앱을 갖는 동일한 구독인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="fd5d5-131">b.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-131">b.</span></span> <span data-ttu-id="fd5d5-132">SubscriptionId를 제공하는 다음 명령을 실행하여 사용할 구독을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="fd5d5-133">[New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) 스크립트의 텍스트를 로컬 컴퓨터에 복사하여 PowerShell cmdlet(예: `APIAuth.ps1`)으로 저장하고 실행합니다. `.\APIAuth.ps1`</span><span class="sxs-lookup"><span data-stu-id="fd5d5-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="fd5d5-134">스크립트는 **principalName**에 대한 입력을 제공하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="fd5d5-135">Active Directory 응용 프로그램(예: APIAuth)을 만드는 데 사용할 적절한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="fd5d5-136">스크립트가 완료되면 AD를 사용하여 프로그래밍 방식으로 인증해야 하는 다음 네 개의 값을 표시하고 복사하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="fd5d5-137">**TenantId**, **SubscriptionId**, **ApplicationId** 및 **Secret**입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="fd5d5-138">TenantId를 `{TENANT_ID}`로, ApplicationId `{CLIENT_ID}`로, Secret을 `{CLIENT_SECRET}`으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fd5d5-139">PowerShell 스크립트를 실행할 수 없도록 기본 보안 정책이 설정되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="fd5d5-140">이 경우 다음 명령을 사용하여 스크립트 실행을 허용하도록 실행 정책을 일시적으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="fd5d5-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="fd5d5-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="fd5d5-142">PS cmdlet의 집합의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="fd5d5-143">**회사가 보유한 응용 프로그램 표시**에서 **principalName**라는 스크립트에 제공한 이름으로 새 AD 응용 프로그램을 만든 Azure 관리 포털에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="fd5d5-144">유효한 토큰을 얻는 단계</span><span class="sxs-lookup"><span data-stu-id="fd5d5-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="fd5d5-145">다음 매개 변수를 사용하여 API를 호출하고 TENANT\_ID, CLIENT\_ID 및 CLIENT\_SECRET을 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="fd5d5-146">**요청 URL** *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="fd5d5-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="fd5d5-147">**application/x-www-form-urlencoded** 인 *HTTP 콘텐츠 형식 헤더*</span><span class="sxs-lookup"><span data-stu-id="fd5d5-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="fd5d5-148">**HTTP 요청 본문** *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="fd5d5-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="fd5d5-149">다음은 요청 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-149">The following is an example request:</span></span>
     
       <span data-ttu-id="fd5d5-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="fd5d5-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="fd5d5-151">다음은 응답 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-151">Here is an example response:</span></span>
     
       <span data-ttu-id="fd5d5-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="fd5d5-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="fd5d5-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="fd5d5-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="fd5d5-154">이 예제에서는 POST 매개 변수의 URL 인코딩을 포함했으며, `resource` 값은 실제로 `https://management.core.windows.net/`입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="fd5d5-155">또한 URL에 특수 문자가 포함될 수 있으므로 URL 인코드 `{CLIENT_SECRET}` 에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="fd5d5-156">테스트를 위해 [Fiddler](http://www.telerik.com/fiddler) 또는 [Chrome Postman 확장](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)과 같은 HTTP 클라이언트 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="fd5d5-157">이제 모든 API 호출에 권한 부여 요청 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="fd5d5-158">401 상태 코드가 반환되면 응답 본문을 검사합니다. 토큰이 만료되었을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="fd5d5-159">토큰이 만료된 경우 새 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="fd5d5-160">API 사용</span><span class="sxs-lookup"><span data-stu-id="fd5d5-160">Using the APIs</span></span>
<span data-ttu-id="fd5d5-161">이제 유효한 토큰이 있으니 API 호출을 만들 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="fd5d5-162">각 API 요청에서, 이전 섹션에서 얻은 만료되지 않은 유효한 토큰을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="fd5d5-163">응용 프로그램을 식별하는 일부 매개 변수를 요청 URI에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="fd5d5-164">요청 URI의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="fd5d5-165">매개 변수를 가져오려면 응용 프로그램 이름을 클릭하고 대시보드를 클릭합니다. 그러면 다음과 같은 페이지에 매개 변수 3개가 모두 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="fd5d5-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="fd5d5-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="fd5d5-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="fd5d5-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="fd5d5-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="fd5d5-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="fd5d5-169">**4** 리소스 그룹 이름은 새로 만들지 않은 한 **MobileEngagement**입니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI 매개 변수][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="fd5d5-171">이 API 루트 주소는 이전 API의 것이므로 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="fd5d5-172">Azure 클래식 포털을 사용하여 앱을 만든 경우 응용 프로그램 이름과 다른 응용 프로그램 리소스 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd5d5-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="fd5d5-173">Azure 포털에서 앱을 만든 경우 앱 이름을 사용해야 합니다(새 포털에서 만든 앱의 앱 이름과 응용 프로그램 리소스 이름은 차이가 없음).</span><span class="sxs-lookup"><span data-stu-id="fd5d5-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



