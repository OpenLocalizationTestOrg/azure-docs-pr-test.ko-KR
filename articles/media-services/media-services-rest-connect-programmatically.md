---
title: "REST API를 사용 하 여 서비스 계정을 aaaConnecting tooMedia | Microsoft Docs"
description: "이 항목에서 설명 하는 방법을 tooconnect tooMedia 서비스 데 REST API입니다."
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
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="7ceac-103">미디어 서비스 REST API를 사용 하 여 서비스 계정을 tooMedia 연결</span><span class="sxs-lookup"><span data-stu-id="7ceac-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ceac-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7ceac-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="7ceac-105">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="7ceac-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="7ceac-106">이 항목에서는 프로그래밍 방식으로 연결 tooMicrosoft Azure 미디어 서비스를 사용 하 여 프로그래밍할 때 tooobtain 미디어 서비스 REST API를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="7ceac-107">Microsoft Azure 미디어 서비스에 액세스할 때 다음 두 가지 사항은: 자체 Azure 액세스 제어 서비스 (ACS), 및 hello 미디어 서비스의 URI에서 제공 하는 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="7ceac-108">Hello 올바른 헤더 값을 지정 하 고 전달 hello 액세스 토큰에 올바르게 호출 하는 경우 미디어 서비스에 이러한 요청을 만들 때 원하는 모든 수단을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="7ceac-109">미디어 서비스 REST API tooconnect tooMedia hello를 사용 하 여 서비스 때 hello 가장 일반적인 워크플로 설명 하는 단계를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="7ceac-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="7ceac-110">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="7ceac-110">Getting an access token</span></span> 
2. <span data-ttu-id="7ceac-111">미디어 서비스 URI toohello 연결</span><span class="sxs-lookup"><span data-stu-id="7ceac-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7ceac-112">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="7ceac-113">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="7ceac-114">Hello ODATA API 메타 데이터 설명을 포함 하는 HTTP/1.1 200 응답을 나타날 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="7ceac-115">후속 API 호출 toohello 새 URL을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="7ceac-116">예를 들어 tooconnect을 시도한 후 hello 다음을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="7ceac-117">후속 API 호출 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ 프로그램을 게시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7ceac-118">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="7ceac-119">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="7ceac-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="7ceac-120">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ceac-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="7ceac-121">액세스 제어 주소</span><span class="sxs-lookup"><span data-stu-id="7ceac-121">Access control address</span></span>
<span data-ttu-id="7ceac-122">Media Services 액세스 제어 주소는 중국 북부 지역을 제외하고 https://wamsprodglobal001acs.accesscontrol.windows.net입니다. 중국 북부 지역은 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="7ceac-123">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="7ceac-123">Getting an access token</span></span>
<span data-ttu-id="7ceac-124">tooaccess 미디어 서비스 직접 hello REST API를 통해 ACS에서 액세스 토큰을 검색 하 고 hello 서비스에 모든 HTTP 요청 중에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="7ceac-125">이 토큰은 HTTP 요청 및 hello OAuth v2 프로토콜을 사용 하 여 hello 헤더에 제공 된 액세스 클레임을 기반으로 하는 ACS에서 제공 하는 비슷한 tooother 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="7ceac-126">TooMedia 서비스에 직접 연결 하기 전에 다른 필수 구성 요소가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="7ceac-127">hello 다음 예제에서는 hello HTTP 요청 헤더와 본문 사용 tooretrieve 토큰</span><span class="sxs-lookup"><span data-stu-id="7ceac-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="7ceac-128">**헤더**:</span><span class="sxs-lookup"><span data-stu-id="7ceac-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="7ceac-129">**본문**:</span><span class="sxs-lookup"><span data-stu-id="7ceac-129">**Body**:</span></span>

<span data-ttu-id="7ceac-130">이 요청의; hello 본문에 tooprove hello client_id 및 client_secret 값이 필요 하면 client_id 및 client_secret toohello AccountName 및 AccountKey 값을 각각 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="7ceac-131">이러한 값 계정을 설정 하는 경우 tooyou 미디어 서비스에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="7ceac-132">URL로 인코딩된 미디어 서비스 계정 이어야 합니다는 hello AccountKey 참고 (참조 [퍼센트 인코딩이](http://tools.ietf.org/html/rfc3986#section-2.1) 액세스 토큰 요청에 hello client_secret 값으로 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7ceac-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="7ceac-133">예:</span><span class="sxs-lookup"><span data-stu-id="7ceac-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="7ceac-134">hello 다음 예제에서는 hello 액세스를 포함 하는 hello HTTP 응답 토큰 hello 응답 본문에는</span><span class="sxs-lookup"><span data-stu-id="7ceac-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="7ceac-135">Toocache hello "access_token" 및 "expires_in" 값 tooan 외부 저장소 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="7ceac-136">hello 토큰 데이터를 hello 저장소에서 검색 하 고 미디어 서비스 REST API 호출에서 다시 사용할 수 나중 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="7ceac-137">이 hello 토큰 공유할 수 있는 안전 하 게 여러 프로세스 또는 컴퓨터 간에 시나리오에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="7ceac-138">토큰의 hello access 있는지 toomonitor hello "expires_in" 값을 확인 하 고 필요에 따라 새 토큰으로 REST API 호출을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="7ceac-139">미디어 서비스 URI toohello 연결</span><span class="sxs-lookup"><span data-stu-id="7ceac-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="7ceac-140">hello 루트 미디어 서비스에 대 한 URI에는 https://media.windows.net/입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="7ceac-141">Toothis URI를 처음 연결 해야 하며 후속 호출은 toohello를 구성 해야는 301 리디렉션을에 응답을 발생 하면 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="7ceac-142">또한 요청에서 자동 리디렉션/팔로우 논리를 사용하지 마세요</span><span class="sxs-lookup"><span data-stu-id="7ceac-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="7ceac-143">HTTP 동사 및 요청 본문이 전달 되지 것입니다 toohello 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="7ceac-144">업로드 하기 위한 해당 hello 루트 URI를 기록한 https://yourstorageaccount.blob.core.windows.net/입니다. 여기서 hello 저장소 계정 이름은 미디어 서비스 계정 설정 중에 사용한 동일한 하나 hello 자산 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="7ceac-145">다음 예제는 hello HTTP 요청 toohello 미디어 서비스 루트 URI (https://media.windows.net/)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="7ceac-146">hello 요청에 응답은 301 리디렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="7ceac-147">hello 후속 요청은 사용 하 여 새 URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="7ceac-148">**HTTP 요청**:</span><span class="sxs-lookup"><span data-stu-id="7ceac-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="7ceac-149">**HTTP 응답**:</span><span class="sxs-lookup"><span data-stu-id="7ceac-149">**HTTP Response**:</span></span>

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
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="7ceac-150">**HTTP 요청** (새 URI를 hello를 사용 하 여):</span><span class="sxs-lookup"><span data-stu-id="7ceac-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="7ceac-151">**HTTP 응답**:</span><span class="sxs-lookup"><span data-stu-id="7ceac-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="7ceac-152">구입한 후 hello 새 URI는 hello 미디어 서비스를 사용 하는 toocommunicate 되어야 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ceac-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="7ceac-153">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="7ceac-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7ceac-154">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="7ceac-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

