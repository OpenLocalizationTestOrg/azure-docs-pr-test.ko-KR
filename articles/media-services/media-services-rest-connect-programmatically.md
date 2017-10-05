---
title: "REST API를 사용하여 Media Services 계정에 연결 | Microsoft 문서"
description: "이 토픽에서는 REST API를 사용하여 Media Services에 연결하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="e6427-103">미디어 서비스 REST API를 사용하여 미디어 서비스 계정에 연결</span><span class="sxs-lookup"><span data-stu-id="e6427-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6427-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e6427-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="e6427-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="e6427-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="e6427-106">이 토픽에서는 Media Services REST API로 프로그래밍할 때 Microsoft Azure Media Services에 대한 프로그래밍 방식의 연결을 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="e6427-107">Microsoft Azure 미디어 서비스에 액세스할 때는 Azure 액세스 제어 서비스(ACS)와 미디어 서비스 자체의 URI 등, 두 가지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="e6427-108">미디어 서비스를 호출할 때 올바른 헤더 값을 지정하고 액세스 토큰을 올바르게 통과하면 이 요청을 할 때 사용자가 원하는 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="e6427-109">다음 단계는 미디어 서비스 REST API를 사용하여 미디어 서비스에 연결할 때 가장 일반적인 워크플로를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="e6427-110">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6427-110">Getting an access token</span></span> 
2. <span data-ttu-id="e6427-111">미디어 서비스 URI에 연결</span><span class="sxs-lookup"><span data-stu-id="e6427-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e6427-112">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="e6427-113">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="e6427-114">ODATA API 메타데이터 설명을 포함하는 HTTP/1.1 200 응답을 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="e6427-115">새 URL에 대 한 후속 API 호출을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="e6427-116">예를 들어 연결을 시도한 후 다음 항목을 받은 경우.</span><span class="sxs-lookup"><span data-stu-id="e6427-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="e6427-117">https://wamsbayclus001rest-hs.cloudapp.net/api/에 후속 API 호출을 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e6427-118">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e6427-119">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e6427-120">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6427-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="e6427-121">액세스 제어 주소</span><span class="sxs-lookup"><span data-stu-id="e6427-121">Access control address</span></span>
<span data-ttu-id="e6427-122">Media Services 액세스 제어 주소는 중국 북부 지역을 제외하고 https://wamsprodglobal001acs.accesscontrol.windows.net입니다. 중국 북부 지역은 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn입니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="e6427-123">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6427-123">Getting an access token</span></span>
<span data-ttu-id="e6427-124">REST API를 통해 바로 미디어 서비스에 액세스하려면 ACS에서 액세스 토큰을 검색하여 서비스에 HTTP 요청을 할 때마다 이를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="e6427-125">이 토큰은 HTTP 요청 헤더에서 제공하는 액세스 클레임을 기반으로 하고 OAuth v2 프로토콜을 사용하는 ACS에서 제공하는 다른 토큰과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="e6427-126">미디어 서비스에 직접 연결하기 전에는 다른 필수 조건은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="e6427-127">다음 예제에서는 HTTP 요청 헤더와 토큰을 검색하는 데 사용되는 본문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="e6427-128">**헤더**:</span><span class="sxs-lookup"><span data-stu-id="e6427-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="e6427-129">**본문**:</span><span class="sxs-lookup"><span data-stu-id="e6427-129">**Body**:</span></span>

<span data-ttu-id="e6427-130">이 요청의 본문에 있는 client_id와 client_secret 값을 입증해야 합니다. client_id와 client_secret은 각각 AccountName과 AccountKey 값에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="e6427-131">이러한 값은 계정을 설정할 때 미디어 서비스에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="e6427-132">Media Services 계정에 대한 AccountKey는 URL Encoding이어야 합니다(이 항목을 액세스 토큰 요청에서 client_secret 값으로 사용할 경우 [퍼센트 Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) 참조).</span><span class="sxs-lookup"><span data-stu-id="e6427-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="e6427-133">예:</span><span class="sxs-lookup"><span data-stu-id="e6427-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="e6427-134">다음 예제에서는 응답 본문에 액세스 토큰을 포함하는 HTTP 응답을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="e6427-135">외부 저장소에 "access_token" 및 "expires_in" 값을 캐시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="e6427-136">나중에 저장소에서 토큰 데이터를 검색하여 미디어 서비스 REST API 호출에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="e6427-137">여러 프로세스 또는 컴퓨터 사이에서 토큰을 안전하게 공유할 수 있는 시나리오에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="e6427-138">액세스 토큰의 "expires_in" 값을 모니터링하고 필요에 따라 REST API 호출을 새 토큰으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="e6427-139">미디어 서비스 URI에 연결</span><span class="sxs-lookup"><span data-stu-id="e6427-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="e6427-140">미디어 서비스의 루트 URI는 https://media.windows.net/입니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="e6427-141">이 URI에 처음으로 연결해야 하며 응답으로 301 리디렉션을 받은 경우 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="e6427-142">또한 요청에서 자동 리디렉션/팔로우 논리를 사용하지 마세요</span><span class="sxs-lookup"><span data-stu-id="e6427-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="e6427-143">HTTP 동사와 요청 본문은 새 URI로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="e6427-144">Note 루트 자산 파일 업로드 및 다운로드에 대 한 URI 인지 https://yourstorageaccount.blob.core.windows.net/ 미디어 서비스 계정 설정을 하는 동안 사용 되는 동일한 저장소 계정 이름 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="e6427-145">다음 예제에서는 Media Services 루트 URI(https://media.windows.net/)에 대한 HTTP 요청을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="e6427-146">요청은 응답에서 301 리디렉션을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="e6427-147">후속 요청은 새 URI(https://wamsbayclus001rest-hs.cloudapp.net/api/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="e6427-148">**HTTP 요청**:</span><span class="sxs-lookup"><span data-stu-id="e6427-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="e6427-149">**HTTP 응답**:</span><span class="sxs-lookup"><span data-stu-id="e6427-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="e6427-150">**HTTP 요청** (새 URI 사용):</span><span class="sxs-lookup"><span data-stu-id="e6427-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="e6427-151">**HTTP 응답**:</span><span class="sxs-lookup"><span data-stu-id="e6427-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="e6427-152">새 URI를 받은 후 미디어 서비스와 통신 하는데 사용 해야 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="e6427-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="e6427-153">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="e6427-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e6427-154">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="e6427-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

