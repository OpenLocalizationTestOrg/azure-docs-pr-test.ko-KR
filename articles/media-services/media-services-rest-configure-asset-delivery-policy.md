---
title: "미디어 서비스 REST API를 사용 하 여 aaaConfiguring 자산 배달 정책을 | Microsoft Docs"
description: "이 항목에서는 방법을 미디어 서비스 REST API를 사용 하 여 tooconfigure 다른 자산 배달 정책을 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a>자산 배달 정책 구성
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

Toodeliver 동적으로 암호화 된 자산을 하려는 경우 단계 중 하나 hello hello 미디어 서비스 콘텐츠 배달 워크플로 자산에 대 한 배달 정책을 구성 합니다. hello 자산 배달 정책 미디어 서비스 프로그램 자산 toobe 배달에 대해 원하는 방법을 알려 줍니다: 스트리밍 프로토콜에 자산 패키지 되어야 하며 동적으로 (예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), 용 toodynamically 원하는 여부 자산 암호화 및 방법 (봉투 (envelope) 또는 일반 암호화) 합니다.

이 항목에서는 근거, 방법 설명 toocreate 고 자산 배달 정책을 구성 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 
>
>또한 toobe 수 toouse 동적 패키징 및 동적 암호화 자산인 있어야 적응 비트 전송률 mp4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합입니다.

Toohello 각기 다른 정책을 적용할 수 동일한 자산입니다. 예를 들어 PlayReady 암호화 tooSmooth 스트리밍 및 AES 봉투 (envelope) 암호화 tooMPEG를 적용할 수 있습니다 DASH 및 HLS입니다. 배달 정책에 정의 되어 있지 않은 모든 프로토콜 (예를 들어 추가한만 hello 프로토콜로 HLS를 지정 하는 단일 정책을) 스트리밍에서 차단 됩니다. hello 예외 toothis는 없는 자산 배달 정책을 정의 해야 합니다. 그런 다음 모든 프로토콜이 일반 hello에 허용 됩니다.

Toodeliver 저장소 암호화 된 자산을 원한다 면 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 hello 서버 제거 hello 저장소 암호화 및 스트림 hello를 사용 하 여 콘텐츠 스트리밍 배달 정책을 지정 합니다. 예를 들어 toodeliver 자산 암호화 표준 AES (고급) 봉투 (envelope) 암호화 키로 암호화, 너무 hello 정책 형식을 설정**DynamicEnvelopeEncryption**합니다. tooremove 저장소 암호화 및 명확 hello에 스트림 hello 자산 hello 정책 형식을 설정 너무**NoDynamicEncryption**합니다. 이러한 정책 형식과 수행 하는 tooconfigure 방법을 보여 주는 예제입니다.

Hello 자산 배달 정책을 구성 하는 방법에 따라 것 수 toodynamically 패키지 수, 동적으로 암호화 하 고 스트림 스트리밍 프로토콜을 따르는 hello: 부드러운 스트리밍, HLS, MPEG DASH 스트림을 합니다.

다음 목록에서는 hello hello toostream 부드러운 스트리밍, HLS, 대시를 사용 하는 형식을 지정 합니다.

부드러운 스트리밍:

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS:

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Toopublish 자산 및 빌드 스트리밍 URL 참조 하는 방법에 대 한 지침은 [스트리밍 URL을 작성할](media-services-deliver-streaming-content.md)합니다.

## <a name="considerations"></a>고려 사항
* 자산에 대한 주문형(스트리밍) 로케이터가 있는 동안 해당 자산과 연결된 AssetDeliveryPolicy를 삭제할 수 없습니다. hello 권장은 hello 정책 삭제 하기 전에 hello 자산에서 tooremove hello 정책입니다.
* 자산 배달 정책이 설정되지 않은 경우 암호화된 저장소 자산에 스트리밍 로케이터를 만들 수 없습니다.  Hello 자산 없는 경우 저장소 암호화,이 hello 시스템은 자산 배달 정책 없이 지우기 hello에 로케이터 및 스트림 hello 자산을 만들 수 있습니다.
* 단일 자산과 연결 된 여러 자산 배달 정책을 있는데는 한 가지 방법은 toohandle 주어진된 AssetDeliveryProtocol만 지정할 수 있습니다.  모르기 때문에 hello 시스템 어떤 것에서 오류가 발생 하는 hello AssetDeliveryProtocol.SmoothStreaming 프로토콜을 지정 하는 toolink 두 배달 정책을 시도 하는 경우 의미 원하는 tooapply 때 클라이언트에서 부드러운 스트리밍 요청 합니다.
* 기존 스트리밍 로케이터는 자산 있는 경우 새 정책 toohello 자산을 연결할 수 없습니다, 그리고 기존 정책을 hello 자산에서의 연결을 해제 또는 hello 자산과 연결 된 배달 정책을 업데이트 합니다.  먼저 tooremove hello 스트리밍 로케이터, hello 정책을 조정 있고 hello 스트리밍 로케이터를 다시 만들어야 합니다.  Hello 원본이 나 다운스트림 CDN에서 콘텐츠를 캐시할 수 있으므로 클라이언트에 대 한 문제를 발생 하지 않습니다 스트리밍 로케이터 있지만 hello를 다시 만들 때 동일한 locatorId 확인 해야 하는 hello를 사용할 수 있습니다.

>[!NOTE]

>미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다. 자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.

## <a name="connect-toomedia-services"></a>TooMedia 서비스 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

>[!NOTE]
>Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

## <a name="clear-asset-delivery-policy"></a>자산 배달 정책 지우기
### <a id="create_asset_delivery_policy"></a>자산 배달 정책 만들기
hello 다음 HTTP 요청을 만듭니다 toonot 동적 암호화를 적용 하 고 프로토콜을 통해 toodeliver hello 스트림 hello 다음 중 하나를 지정 하는 자산 배달 정책: MPEG DASH, HLS 및 부드러운 스트리밍 프로토콜입니다. 

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.   

요청:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

응답:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <a id="link_asset_with_asset_delivery_policy"></a>자산을 자산 배달 정책과 연결
다음 HTTP 요청 링크 hello hello 자산 toohello 자산 배달 정책에 지정 합니다.

요청:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

응답:

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption 자산 배달 정책
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a>Hello EnvelopeEncryption 형식의 콘텐츠 키를 만들고 toohello 자산에 연결
DynamicEnvelopeEncryption 배달 정책을 지정할 때는 toomake 있는지 toolink 자산 tooa 콘텐츠 키의 hello envelopeencryption의 형식이 필요 합니다. 자세한 내용은 [콘텐츠 키 만들기](media-services-rest-create-contentkey.md)를 참조하세요.

### <a id="get_delivery_url"></a>배달 URL 가져오기
Hello에 대 한 get hello 배달 URL hello 이전 단계에서 만든 hello 콘텐츠 키의 배달 방법을 지정 합니다. 클라이언트가 반환 URL toorequest hello를 사용 하는 AES 키 또는 PlayReady 라이선스 순서 tooplayback hello에 콘텐츠를 보호 합니다.

Hello hello HTTP 요청 본문에 hello URL tooget hello 유형을 지정 합니다. 미디어 서비스 PlayReady 라이선스 취득 URL을 요청 PlayReady 사용 하 여 콘텐츠를 보호할 경우 1을 사용 하 여 hello keyDeliveryType에 대 한: {"keyDeliveryType": 1을 (를). Hello 봉투 (envelope) 암호화를 사용 하 여 콘텐츠를 보호 하는 경우 2 keyDeliveryType 지정 하 여 키 획득 URL 요청: {"keyDeliveryType": 2}.

요청:

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

응답:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a>자산 배달 정책 만들기
hello 다음 HTTP 요청을 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 봉투 암호화 (**DynamicEnvelopeEncryption**) toohello **HLS**프로토콜 (이 예제에서는 다른 프로토콜은 스트리밍에서 차단). 

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.   

요청:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


응답:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a>자산을 자산 배달 정책과 연결
[자산을 자산 배달 정책과 연결](#link_asset_with_asset_delivery_policy)

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption 자산 배달 정책
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a>Hello CommonEncryption 형식의 콘텐츠 키를 만들고 toohello 자산에 연결
DynamicCommonEncryption 배달 정책을 지정할 때는 toomake 있는지 toolink 자산 tooa 콘텐츠 키의 hello CommonEncryption 형식이 필요 합니다. 자세한 내용은 [콘텐츠 키 만들기](media-services-rest-create-contentkey.md)를 참조하세요.

### <a name="get-delivery-url"></a>배달 URL 가져오기
Hello 이전 단계에서 만든 hello 콘텐츠 키의 hello PlayReady 배달 방법에 대 한 hello 배달 URL을 가져옵니다. 클라이언트 hello URL toorequest 순서 tooplayback hello에 PlayReady 라이선스 보호 된 콘텐츠 반환을 사용 합니다. 자세한 내용은 [배달 URL 가져오기](#get_delivery_url)를 참조하세요.

### <a name="create-asset-delivery-policy"></a>자산 배달 정책 만들기
hello 다음 HTTP 요청을 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 일반 암호화 (**DynamicCommonEncryption**) toohello **부드러운 스트리밍**  프로토콜 (이 예제에서는 다른 프로토콜은 스트리밍에서 차단). 

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.   

요청:

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


Widevine DRM을 사용 하 여 콘텐츠 tooprotect 원하는 hello AssetDeliveryConfiguration 값 toouse WidevineLicenseAcquisitionUrl (들어 있는 hello 값 7)을 업데이트 하 고 라이선스 배달 서비스의 hello URL을 지정 합니다. Widevine 라이선스를 배달 AMS 파트너 toohelp 다음 hello를 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다.

예: 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> Widevine를 암호화 하는 경우 대시를 사용 하 여 수 toodeliver만 있을 수 있습니다. 있는지 toospecify 대시 (2)에 hello 자산 배달 프로토콜을 확인 합니다.
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a>자산을 자산 배달 정책과 연결
[자산을 자산 배달 정책과 연결](#link_asset_with_asset_delivery_policy)

## <a id="types"></a>AssetDeliveryPolicy를 정의할 때 사용되는 형식

### <a name="assetdeliveryprotocol"></a>AssetDeliveryProtocol

hello 다음 열거형 값에 설명 hello 자산 배달 프로토콜에 대해 설정할 수 있습니다.

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a>AssetDeliveryPolicyType

hello 다음 열거형 값에 설명 hello 자산 배달 정책 형식에 대해 설정할 수 있습니다.  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a>ContentKeyDeliveryType

hello 다음 열거형 값에 설명 hello 콘텐츠 키 toohello 클라이언트의 tooconfigure hello 배달 방법을 사용할 수 있습니다.
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a>AssetDeliveryPolicyConfigurationKey

다음 열거형 hello tooconfigure 사용 되는 키 tooget 자산 배달 정책에 대 한 특정 구성을 설정할 수 있는 값을 설명 합니다.

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

