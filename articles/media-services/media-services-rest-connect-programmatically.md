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
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a>미디어 서비스 REST API를 사용하여 미디어 서비스 계정에 연결
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST (영문)](media-services-rest-connect-programmatically.md)
> 
> 

이 토픽에서는 Media Services REST API로 프로그래밍할 때 Microsoft Azure Media Services에 대한 프로그래밍 방식의 연결을 가져오는 방법을 설명합니다.

Microsoft Azure 미디어 서비스에 액세스할 때는 Azure 액세스 제어 서비스(ACS)와 미디어 서비스 자체의 URI 등, 두 가지가 필요합니다. 미디어 서비스를 호출할 때 올바른 헤더 값을 지정하고 액세스 토큰을 올바르게 통과하면 이 요청을 할 때 사용자가 원하는 방법을 사용할 수 있습니다.

다음 단계는 미디어 서비스 REST API를 사용하여 미디어 서비스에 연결할 때 가장 일반적인 워크플로를 설명합니다.

1. 액세스 토큰 가져오기 
2. 미디어 서비스 URI에 연결 
   
   > [!NOTE]
   > https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다. 사용자는 새 URI에 대한 후속 호출을 해야 합니다.
   > ODATA API 메타데이터 설명을 포함하는 HTTP/1.1 200 응답을 받을 수도 있습니다.
   > 
   > 
3. 새 URL에 대 한 후속 API 호출을 게시합니다. 
   
    예를 들어 연결을 시도한 후 다음 항목을 받은 경우.
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    https://wamsbayclus001rest-hs.cloudapp.net/api/에 후속 API 호출을 게시해야 합니다.

    >[!NOTE]
    >다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. 항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

## <a name="access-control-address"></a>액세스 제어 주소
Media Services 액세스 제어 주소는 중국 북부 지역을 제외하고 https://wamsprodglobal001acs.accesscontrol.windows.net입니다. 중국 북부 지역은 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn입니다.

## <a name="getting-an-access-token"></a>액세스 토큰 가져오기
REST API를 통해 바로 미디어 서비스에 액세스하려면 ACS에서 액세스 토큰을 검색하여 서비스에 HTTP 요청을 할 때마다 이를 사용합니다. 이 토큰은 HTTP 요청 헤더에서 제공하는 액세스 클레임을 기반으로 하고 OAuth v2 프로토콜을 사용하는 ACS에서 제공하는 다른 토큰과 비슷합니다. 미디어 서비스에 직접 연결하기 전에는 다른 필수 조건은 필요하지 않습니다.

다음 예제에서는 HTTP 요청 헤더와 토큰을 검색하는 데 사용되는 본문을 보여 줍니다.

**헤더**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**본문**:

이 요청의 본문에 있는 client_id와 client_secret 값을 입증해야 합니다. client_id와 client_secret은 각각 AccountName과 AccountKey 값에 해당합니다. 이러한 값은 계정을 설정할 때 미디어 서비스에서 제공합니다. 

Media Services 계정에 대한 AccountKey는 URL Encoding이어야 합니다(이 항목을 액세스 토큰 요청에서 client_secret 값으로 사용할 경우 [퍼센트 Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) 참조).

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


예: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


다음 예제에서는 응답 본문에 액세스 토큰을 포함하는 HTTP 응답을 보여 줍니다.

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
> 외부 저장소에 "access_token" 및 "expires_in" 값을 캐시하는 것이 좋습니다. 나중에 저장소에서 토큰 데이터를 검색하여 미디어 서비스 REST API 호출에서 다시 사용할 수 있습니다. 여러 프로세스 또는 컴퓨터 사이에서 토큰을 안전하게 공유할 수 있는 시나리오에 특히 유용합니다.
> 
> 

액세스 토큰의 "expires_in" 값을 모니터링하고 필요에 따라 REST API 호출을 새 토큰으로 업데이트해야 합니다.

### <a name="connecting-to-the-media-services-uri"></a>미디어 서비스 URI에 연결
미디어 서비스의 루트 URI는 https://media.windows.net/입니다. 이 URI에 처음으로 연결해야 하며 응답으로 301 리디렉션을 받은 경우 새 URI에 대한 후속 호출을 해야 합니다. 또한 요청에서 자동 리디렉션/팔로우 논리를 사용하지 마세요 HTTP 동사와 요청 본문은 새 URI로 전달되지 않습니다.

Note 루트 자산 파일 업로드 및 다운로드에 대 한 URI 인지 https://yourstorageaccount.blob.core.windows.net/ 미디어 서비스 계정 설정을 하는 동안 사용 되는 동일한 저장소 계정 이름 됩니다.

다음 예제에서는 Media Services 루트 URI(https://media.windows.net/)에 대한 HTTP 요청을 설명합니다. 요청은 응답에서 301 리디렉션을 받습니다. 후속 요청은 새 URI(https://wamsbayclus001rest-hs.cloudapp.net/api/)를 사용합니다.     

**HTTP 요청**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**HTTP 응답**:

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


**HTTP 요청** (새 URI 사용):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 응답**:

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
> 새 URI를 받은 후 미디어 서비스와 통신 하는데 사용 해야 하는 URI입니다. 
> 
> 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

