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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>미디어 서비스 REST API를 사용 하 여 서비스 계정을 tooMedia 연결
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST (영문)](media-services-rest-connect-programmatically.md)
> 
> 

이 항목에서는 프로그래밍 방식으로 연결 tooMicrosoft Azure 미디어 서비스를 사용 하 여 프로그래밍할 때 tooobtain 미디어 서비스 REST API를 hello 하는 방법을 설명 합니다.

Microsoft Azure 미디어 서비스에 액세스할 때 다음 두 가지 사항은: 자체 Azure 액세스 제어 서비스 (ACS), 및 hello 미디어 서비스의 URI에서 제공 하는 액세스 토큰입니다. Hello 올바른 헤더 값을 지정 하 고 전달 hello 액세스 토큰에 올바르게 호출 하는 경우 미디어 서비스에 이러한 요청을 만들 때 원하는 모든 수단을 사용할 수 있습니다.

미디어 서비스 REST API tooconnect tooMedia hello를 사용 하 여 서비스 때 hello 가장 일반적인 워크플로 설명 하는 단계를 수행 하는 hello:

1. 액세스 토큰 가져오기 
2. 미디어 서비스 URI toohello 연결 
   
   > [!NOTE]
   > Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.
   > Hello ODATA API 메타 데이터 설명을 포함 하는 HTTP/1.1 200 응답을 나타날 수도 있습니다.
   > 
   > 
3. 후속 API 호출 toohello 새 URL을 게시 합니다. 
   
    예를 들어 tooconnect을 시도한 후 hello 다음을 가져왔습니다.
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    후속 API 호출 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ 프로그램을 게시 해야 합니다.

    >[!NOTE]
    >다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

## <a name="access-control-address"></a>액세스 제어 주소
Media Services 액세스 제어 주소는 중국 북부 지역을 제외하고 https://wamsprodglobal001acs.accesscontrol.windows.net입니다. 중국 북부 지역은 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn입니다.

## <a name="getting-an-access-token"></a>액세스 토큰 가져오기
tooaccess 미디어 서비스 직접 hello REST API를 통해 ACS에서 액세스 토큰을 검색 하 고 hello 서비스에 모든 HTTP 요청 중에 사용 합니다. 이 토큰은 HTTP 요청 및 hello OAuth v2 프로토콜을 사용 하 여 hello 헤더에 제공 된 액세스 클레임을 기반으로 하는 ACS에서 제공 하는 비슷한 tooother 토큰입니다. TooMedia 서비스에 직접 연결 하기 전에 다른 필수 구성 요소가 필요가 없습니다.

hello 다음 예제에서는 hello HTTP 요청 헤더와 본문 사용 tooretrieve 토큰

**헤더**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**본문**:

이 요청의; hello 본문에 tooprove hello client_id 및 client_secret 값이 필요 하면 client_id 및 client_secret toohello AccountName 및 AccountKey 값을 각각 해당 합니다. 이러한 값 계정을 설정 하는 경우 tooyou 미디어 서비스에 의해 제공 됩니다. 

URL로 인코딩된 미디어 서비스 계정 이어야 합니다는 hello AccountKey 참고 (참조 [퍼센트 인코딩이](http://tools.ietf.org/html/rfc3986#section-2.1) 액세스 토큰 요청에 hello client_secret 값으로 사용 하는 경우.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


예: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


hello 다음 예제에서는 hello 액세스를 포함 하는 hello HTTP 응답 토큰 hello 응답 본문에는

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
> Toocache hello "access_token" 및 "expires_in" 값 tooan 외부 저장소 것이 좋습니다. hello 토큰 데이터를 hello 저장소에서 검색 하 고 미디어 서비스 REST API 호출에서 다시 사용할 수 나중 합니다. 이 hello 토큰 공유할 수 있는 안전 하 게 여러 프로세스 또는 컴퓨터 간에 시나리오에 특히 유용 합니다.
> 
> 

토큰의 hello access 있는지 toomonitor hello "expires_in" 값을 확인 하 고 필요에 따라 새 토큰으로 REST API 호출을 업데이트 합니다.

### <a name="connecting-toohello-media-services-uri"></a>미디어 서비스 URI toohello 연결
hello 루트 미디어 서비스에 대 한 URI에는 https://media.windows.net/입니다. Toothis URI를 처음 연결 해야 하며 후속 호출은 toohello를 구성 해야는 301 리디렉션을에 응답을 발생 하면 새 URI입니다. 또한 요청에서 자동 리디렉션/팔로우 논리를 사용하지 마세요 HTTP 동사 및 요청 본문이 전달 되지 것입니다 toohello 새 URI입니다.

업로드 하기 위한 해당 hello 루트 URI를 기록한 https://yourstorageaccount.blob.core.windows.net/입니다. 여기서 hello 저장소 계정 이름은 미디어 서비스 계정 설정 중에 사용한 동일한 하나 hello 자산 파일을 다운로드 합니다.

다음 예제는 hello HTTP 요청 toohello 미디어 서비스 루트 URI (https://media.windows.net/)를 보여 줍니다. hello 요청에 응답은 301 리디렉션을 가져옵니다. hello 후속 요청은 사용 하 여 새 URI (https://wamsbayclus001rest-hs.cloudapp.net/api/) hello 합니다.     

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
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP 요청** (새 URI를 hello를 사용 하 여):

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
> 구입한 후 hello 새 URI는 hello 미디어 서비스를 사용 하는 toocommunicate 되어야 하는 URI입니다. 
> 
> 

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

