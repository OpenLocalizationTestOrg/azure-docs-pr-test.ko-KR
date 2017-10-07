---
title: "REST를 사용 하 여 미디어 서비스 계정으로 aaaUpload 파일 | Microsoft Docs"
description: "만들고 자산을 업로드 하 여 tooget 미디어를 미디어 서비스 콘텐츠 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a>REST를 사용하여 Media Services 계정에 파일 업로드
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST (영문)](media-services-rest-upload-files.md)
> * [포털](media-services-portal-upload-files.md)
> 
> 

미디어 서비스에서 자산에 디지털 파일을 업로드합니다. hello [자산](https://docs.microsoft.com/rest/api/media/operations/asset) 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 hello 자산으로 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다. 

> [!NOTE]
> hello 고려 사항에 따라 적용 됩니다.
> 
> * 미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다. 값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다. 또한 하나만 있을 수 있습니다 하나 '.' hello 파일 이름 확장명에 대 한 합니다.
> * hello hello 이름 길이 260 자 보다 클 수 없습니다.
> * 미디어 서비스에서 처리에 지원 되는 제한 toohello 최대 파일 크기 있습니다. 참조 하십시오 [이](media-services-quotas-and-limitations.md) hello 파일 크기 제한에 대 한 세부 정보에 대 한 항목입니다.
> 

자산을 업로드 하기 위한 기본 워크플로 hello hello 다음 섹션으로 구분 됩니다.

* 자산 만들기
* 자산 암호화(선택 사항)
* 업로드 파일 tooblob 저장소

AMS는 tooupload 자산을을 대량 있습니다. 자세한 내용은 [이](media-services-rest-upload-files.md#upload_in_bulk) 섹션을 참조하세요.

> [!NOTE]
> 미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다. 자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.
> 

## <a name="connect-toomedia-services"></a>TooMedia 서비스 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

>[!NOTE]
>Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

## <a name="upload-assets"></a>자산 업로드

### <a name="create-an-asset"></a>자산 만들기

자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다. REST API를 자산 만들기 POST를 전송 해야 하는 hello에서 tooMedia 서비스를 요청 하 고 hello 요청 본문에 자산에 대 한 속성 정보를 배치 합니다.

자산을 만드는 경우를 지정할 수 있는 hello 속성 중 하나 **옵션**합니다. **옵션** 자산을 만들 수 있는 hello 암호화 옵션을 설명 하는 열거 값입니다. 유효한 값은 hello 아래 목록 값의 조합이 아니라 hello 값 중 하나입니다. 

* **None** = **0**: 암호화가 사용되지 않습니다. Hello 기본값입니다. 이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.
    Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다. 
* **StorageEncrypted** = **1**: 업로드 및 저장에 대 한 AES 256 비트 암호화로 암호화 된 파일 toobe 프로그램에 대 한 여부를 지정 합니다.
  
    자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다. 자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.
* **CommonEncryptionProtected** = **2**: 일반적인 암호화 방식(예: PlayReady)으로 보호된 파일을 업로드하는 경우 지정합니다. 
* **EnvelopeEncryptionProtected** = **4**: AES로 암호화된 HLS 파일을 업로드하는 경우 지정합니다. 참고 hello 파일을 인코딩된 있는지 및 Transform Manager를 통해 암호화 해야 합니다.

> [!NOTE]
> 자산 암호화를 사용 하는 경우 만들어야 합니다는 **ContentKey** hello 항목에 설명 된 대로 tooyour 자산에 연결:[어떻게 toocreate ContentKey](media-services-rest-create-contentkey.md)합니다. Hello 자산으로 hello 파일을 업로드 한 후 해야 hello에 tooupdate hello 암호화 속성 참고 **AssetFile** hello 하는 동안 가져온 hello 값이 있는 엔터티 **자산** 암호화 합니다. Hello를 사용 하 여 작업을 수행할 **병합** HTTP 요청입니다. 
> 
> 

hello 방법을 예제와 다음 toocreate 자산입니다.

**HTTP 요청**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>AssetFile 만들기
hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장 하는 비디오 또는 오디오 파일을 나타냅니다. 자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 자산 파일이 포함될 수 있습니다. hello 미디어 서비스 인코더 작업에는 자산 파일 개체가 blob 컨테이너의 디지털 파일과 연관 되지 않은 경우 실패 합니다.

해당 hello 참고 **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다. hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.

Hello를 사용 하는 blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **병합** HTTP 요청 tooupdate hello AssetFile (같이 hello 항목의 뒷부분에 나오는) 하 여 미디어 파일에 대 한 정보입니다. 

**HTTP 요청**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

**HTTP 응답**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }

### <a name="creating-hello-accesspolicy-with-write-permission"></a>쓰기 권한으로 hello AccessPolicy 만들기

>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

Blob 저장소에 파일을 업로드 하기 전에 hello 액세스 tooan asset을 작성 하기 위한 정책 권한을 설정 합니다. HTTP 요청 toohello AccessPolicies 엔터티를 게시 하는 toodo 설정 합니다. 작성 시 DurationInMinutes 값을 정의하지 않으면 응답에서 500 내부 서버 오류 메시지가 다시 나타납니다. AccessPolicies에 대한 자세한 내용은 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)를 참조하세요.

hello 방법을 예제와 다음 toocreate AccessPolicy:

**HTTP 요청**

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

**HTTP 요청**

    If successful, hello following response is returned:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a>Hello 업로드 URL 가져오기
tooreceive 실제 업로드 URL hello, SAS 로케이터를 만듭니다. 로케이터는 tooaccess는 자산의 파일에에서는 클라이언트에 대 한 hello 시작 시간과 연결 끝점 유형을 정의 합니다. 요청 및 요구 사항이 지정된 된 AccessPolicy-자산 쌍 toohandle 다른 클라이언트에 대 한 여러 개의 Locator 엔터티를 만들 수 있습니다. 이러한 각 로케이터 사용 하 여 hello StartTime 값과 DurationInMinutes 값 hello hello AccessPolicy toodetermine hello 기간 URL이 사용 될 수 있습니다. 자세한 내용은 [로케이터](https://docs.microsoft.com/rest/api/media/operations/locator)를 참조하세요.

SAS URL 형식에 따라 hello에 있습니다.

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

다음과 같은 몇 가지 고려 사항이 적용됩니다.

* 지정된 자산과 연관된 고유 로케이터는 한 번에 5개 이상 가질 수 없습니다. 자세한 내용은 로케이터를 참조하세요.
* 필요한 경우 tooupload 파일 즉시, StartTime 값 toofive 분 hello 현재 시간 전에 설정 해야 합니다. 클라이언트 컴퓨터와 미디어 서비스 사이에 시간차가 있을 수 있기 때문입니다. 또한 StartTime 값 날짜/시간 형식에 따라 hello에 이어야 합니다: YYYY-m M-DDTHH:mm:ssZ (예를 들어 "2014-05-23T17:53:50Z").    
* 30 ~ 40 초 있을 수 있습니다 지연 로케이터를 만들면 toowhen 사용 하기 위해 사용할 수 있습니다. 이 문제는 tooboth SAS URL 및 Origin Locator를 적용합니다.

다음 예제는 hello toocreate 정의한 대로 SAS URL Locator를 (SAS 로케이터에 대 한 "1") 및 "2"에 대 한 주문형 origin locator hello 요청 본문의 Type 속성 hello 하는 방법을 보여 줍니다. hello **경로** 반환 된 속성을 사용 해야 tooupload 파일 hello URL이 포함 됩니다.

**HTTP 요청**

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

**HTTP 응답**

성공 하면 다음 응답 hello 반환 됩니다.

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a>Blob 저장소 컨테이너에 파일 업로드
Hello AccessPolicy와 Locator 집합 있으면 hello 실제 파일이 hello Azure 저장소 REST Api를 사용 하 여 업로드 된 tooan Azure Blob 저장소 컨테이너. 블록 blob으로 hello 파일을 업로드 해야 합니다. 페이지 blob은 Azure Media Services에서 지원되지 않습니다.  

> [!NOTE]
> Hello 파일 이름을 추가 해야 tooupload toohello 로케이터 hello 파일에 대 한 원하는 **경로** hello 이전 섹션에서 받은 값입니다. 예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? 을 참조하세요. . 을 참조하세요. 
> 
> 

Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.

### <a name="update-hello-assetfile"></a>Hello AssetFile 업데이트
파일을 업로드 한 했으므로 hello FileAsset 크기 (및 다른) 정보를 업데이트 합니다. 예:

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**HTTP 응답**

성공 hello 다음이 반환 됩니다: HTTP/1.1 204 콘텐츠 없음

### <a name="delete-hello-locator-and-accesspolicy"></a>Hello Locator와 AccessPolicy 삭제
**HTTP 요청**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 204 No Content 
    ...

**HTTP 요청**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>대량으로 자산 업로드
### <a name="create-hello-ingestmanifest"></a>Hello IngestManifest 만들기
hello IngestManifest는 자산, 자산 파일 및 수 있는 통계 정보 집합에 대 한 컨테이너 toodetermine hello 진행률 hello 집합에 대 한 대량 수집을 사용 합니다.

**HTTP 요청**

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a>자산 만들기
Hello IngestManifestAsset을 만들기 전에 toocreate hello 자산 대량 수집을 사용 하 여 완료 해야 합니다. 자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다. Hello REST API, 자산 만들기 필요 Azure 미디어 서비스는 HTTP POST 요청 tooMicrosoft 보내고 hello 요청 본문에 자산에 대 한 속성 정보를 배치 합니다. 이 예제에서는 Asset hello hello 요청 본문에 포함 된 hello storageencrption (1) 옵션을 사용 하 여 생성 됩니다.

**HTTP 응답**

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a>Hello IngestManifestAssets 만들기
IngestManifestAssets은 대량 수집에 사용되는 IngestManifest 내에서 자산을 나타냅니다. 기본적으로 hello hello 자산 toohello 매니페스트를 연결 합니다. Azure 미디어 서비스 ingestmanifestfile은 연결 된 컬렉션 toohello IngestManifestAsset에 따라 hello 파일 업로드를 위해 내부적으로 감시 합니다. 이러한 파일 업로드 되 면 hello 자산이 완료 됩니다. HTTP POST 요청으로 새로운 IngestManifestAsset을 만들 수 있습니다. Hello 요청 본문에 hello IngestManifest Id 및 hello 자산 대량 수집을 위해 IngestManifestAsset이 함께 연결 해야 하는 hello Id를 포함 합니다.

**HTTP 응답**

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>각 자산에 대 한 hello Ingestmanifestfile 만들기
IngestManifestFile 자산에 대한 대량 수집의 일환으로 업로드될 실제 비디오 또는 오디오 blob 개체를 나타냅니다. 암호화 관련 hello 자산 암호화 옵션을 사용 하는 경우가 아니면 속성 필요 하지 않습니다. 이 섹션에 사용 하는 hello 예제 자산 이전에 만든 hello에 대 한 StorageEncryption을 사용 하는 IngestManifestFile 만들기를 보여 줍니다.

**HTTP 응답**

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a>Hello 파일 tooBlob 저장소에 업로드
Hello 자산 파일 toohello blob 저장소 컨테이너 hello hello IngestManifest의 BlobStorageUriForUpload 속성에서 제공 하는 Uri를 업로드할 수 있는 고속 클라이언트 응용 프로그램을 사용할 수 있습니다. 주목할 만한 고속 업로드 서비스 중 하나는 [Azure 응용 프로그램용 Aspera On Demand](http://go.microsoft.com/fwlink/?LinkId=272001)입니다.

### <a name="monitor-bulk-ingest-progress"></a>대량 수집 진행률 모니터
대량 hello IngestManifest의 hello 통계 속성을 폴링하여 IngestManifest에 대 한 작업을 수집 hello 진행률을 모니터링할 수 있습니다. 속성은 복합 형식인 [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics)입니다. 통계 속성 toopoll hello hello IngestManifest id입니다. 전달 HTTP GET 요청을 제출

## <a name="create-contentkeys-used-for-encryption"></a>암호화에 사용되는 ContentKey 만들기
자산 암호화를 사용 하는 경우 hello 자산 파일을 만들기 전에 암호화에 사용 되는 hello ContentKey toobe를 만들어야 합니다. 저장소 암호화에 대 한 hello 다음과 같은 속성이 포함 되어야 합니다 hello 요청 본문에.

| 요청 본문 속성 | 설명 |
| --- | --- |
| Id |hello 생성 하는 ContentKey Id를 수행 하는 hello를 사용 하 여 직접 형식으로 "nb:kid:UUID:<NEW GUID>"입니다. |
| ContentKeyType |이 콘텐츠 키에 대 한 정수 hello 콘텐츠 키 형식입니다. 저장소 암호화에 대 한 hello 값 1을 전달합니다. |
| EncryptedContentKey |256비트(32바이트) 값인 새 콘텐츠 키 값을 만듭니다. hello 키는 hello 저장소 암호화 X.509 인증서를 hello GetProtectionKeyId 및 GetProtectionKey 메서드에 대 한 HTTP GET 요청을 실행 하 여 Microsoft Azure 미디어 서비스에서 검색을 사용 하 여 암호화 됩니다. |
| ProtectionKeyId |콘텐츠 키를 사용 하는 tooencrypt hello 저장소 암호화 X.509 인증서에 대 한 보호 키 id hello는이 합니다. |
| ProtectionKeyType |Hello 보호 키를 사용 하는 tooencrypt hello 콘텐츠 키에 대 한 hello 암호화 형식입니다. 이 값은 예제에서 StorageEncryption(1)입니다. |
| Checksum |hello MD5 hello 콘텐츠 키에 대 한 계산 된 체크섬입니다. Hello 콘텐츠 키를 가진 hello 콘텐츠 Id를 암호화 하 여 계산 됩니다. 예제 코드에서는 hello toocalculate 체크섬 hello 하는 방법을 보여 줍니다. |

**HTTP 응답**

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a>링크 hello ContentKey toohello 자산
hello ContentKey는 HTTP POST 요청을 전송 하 여 관련된 tooone 또는 자세한 자산은 합니다. hello 다음 요청은 예제 toolink hello 예제 ContentKey toohello 예제 자산 id

**HTTP 응답**

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

**HTTP 응답**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>다음 단계

이제 업로드된 자산을 인코딩할 수 있습니다. 자세한 내용은 [자산 인코딩](media-services-portal-encode.md)을 참조하세요.

또한 Azure 함수 tootrigger hello 구성 컨테이너에 도착 하는 파일을 기반으로 하는 인코딩 작업을 사용할 수 있습니다. 자세한 내용은 [이 샘플](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )을 참조하세요.

## <a name="media-services-learning-paths"></a>Media Services 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

