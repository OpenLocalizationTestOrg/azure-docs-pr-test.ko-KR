---
title: "REST를 사용 하 여 필요에 따라 콘텐츠를 배달 aaaGet 시작 | Microsoft Docs"
description: "이 자습서는 Azure 미디어 서비스 REST API를 사용 하 여 온 요청 콘텐츠 배달 응용 프로그램을 구현할의 hello 단계를 안내 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>REST를 사용한 주문형 콘텐츠 제공 시작
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

이 퀵 스타트의 hello Azure 미디어 서비스 (AMS) REST Api를 사용 하 여 주문형 비디오 (VoD) 콘텐츠 배달 응용 프로그램 구현 단계를 안내 합니다.

hello 자습서에서는 기본 미디어 서비스 워크플로 hello hello 가장 일반적인 프로그래밍 개체 및 미디어 서비스 개발에 필요한 작업을 소개 합니다. Hello 자습서를 완료 한 hello 시점에서 있습니다 수 toostream 되거나 될 점진적으로 업로드, 인코딩, 다운로드 한 샘플 미디어 파일을 다운로드 합니다.

hello 다음 이미지에서는 가장 일반적으로 사용 하는 hello 개체 중 일부를 hello 미디어 서비스 OData 모델에 대 한 VoD 응용 프로그램을 개발 하는 경우

전체 크기로 hello 이미지 tooview를 클릭 합니다.  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>필수 조건
hello 다음과 같은 조건이 필요한 toostart 미디어 서비스 REST Api를 사용 하 여 개발 합니다.

* Azure 계정. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* Media Services 계정. 미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.
* 방법 이해 toodevelop 미디어 서비스 REST api입니다. 자세한 내용은 [Media Services REST API 개요](media-services-rest-how-to-use.md)를 참조하세요
* HTTP 요청 및 응답을 보낼 수 있도록 선택한 응용 프로그램입니다. 이 자습서에서는 [Fiddler](http://www.telerik.com/download/fiddler)를 사용합니다.

작업을 수행 하는 hello이 퀵이 스타트의에 표시 됩니다.

1. 스트리밍 끝점 (hello Azure 포털을 사용 하 여)을 시작 합니다.
2. REST API와 toohello 미디어 서비스 계정을 연결 하세요.
3. REST API를 통해 새 자산을 만들고 비디오를 업로드합니다.
4. Hello 소스 파일을 적응 비트 전송률 MP4 파일 REST api 집합을 인코딩하십시오.
5. Hello 자산 및 스트리밍 get 및 REST API와 점진적 다운로드 Url을 게시 합니다.
6. 콘텐츠를 재생합니다.

>[!NOTE]
>다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다. Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한. 자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.

이 항목에 사용된 AMS REST 엔터티에 대한 자세한 내용은 [Azure Media Services REST API 참조](/rest/api/media/services/azure-media-services-rest-api-reference)를 참조하세요. 참고 항목: [Azure Media Services 개념](media-services-concepts.md)

>[!NOTE]
>미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다. 자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 끝점을 스트리밍 시작

Azure 미디어 서비스를 통해 적응 비트 전송률 스트리밍 비디오를 제공 하는 hello 가장 일반적인 시나리오 중 하나 작업할 때는입니다. 미디어 서비스는 적응 비트 전송률 사전 패키지 toostore 필요 없이 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 적시에서 지 원하는 형식 스트리밍을에 인코딩된 MP4 콘텐츠 toodeliver 수 있는 동적 패키징 제공 각각의 형식 스트리밍을 버전입니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.

toostart hello 스트리밍 끝점을 다음 hello 수행 합니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 설정 창에서 스트리밍 끝점을 클릭 합니다.
3. Hello 기본 스트리밍 끝점을 클릭 합니다.

    hello 스트리밍 끝점 세부 정보 기본 창이 나타납니다.

4. Hello 시작 아이콘을 클릭 합니다.
5. 변경 내용을 저장 단추 toosave hello를 클릭 합니다.

## <a id="connect"></a>REST API를 사용 하 여 toohello 미디어 서비스 계정 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

>[!NOTE]
>Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

예를 들어 tooconnect을 시도한 후 hello 다음을 가져왔습니다.

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

후속 API 호출 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ 프로그램을 게시 해야 합니다.

## <a id="upload"></a>REST API를 통해 새 자산을 만들고 비디오를 업로드합니다.

미디어 서비스에서 자산에 디지털 파일을 업로드합니다. hello **자산** 엔터티 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 닫힌된 캡션 파일 (및 이러한 파일에 대 한 hello 메타 데이터)를 포함할 수 있습니다  Hello 파일 hello 자산으로 업로드 되 면 콘텐츠 추가 처리 및 스트리밍에 대 한 hello 클라우드에 안전 하 게 저장 됩니다.

자산을 만들 때 있는지 tooprovide hello 값 중 하나에 자산 만들기 옵션입니다. hello **옵션** 속성은 자산을 만들 수 있는 hello 암호화 옵션에 설명 하는 열거형 값입니다. 유효한 값이이 목록에서 값의 조합이 아니라 아래 hello 목록의 hello 값 중 하나입니다.

* **없음** = **0** - 암호화가 사용되지 않습니다. 이 옵션을 사용하면 콘텐츠가 전송 중인 상태이거나 저장소에 저장된 상태일 때 보호되지 않습니다.
    Toodeliver MP4 점진적 다운로드를 사용 하 여 하려는 경우이 옵션을 사용 합니다.
* **StorageEncrypted** = **1** -AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 암호화 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다. 자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다. toosecure 디스크에 저장 된 상태의 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일을 사용할 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.
* **CommonEncryptionProtected** = **2** - 이미 암호화되어 일반적인 암호화 또는 PlayReady DRM(예: PlayReady DRM으로 보호되는 부드러운 스트리밍)으로 보호된 콘텐츠를 업로드하는 경우 이 옵션을 사용합니다.
* **EnvelopeEncryptionProtected** = **4** - AES로 암호화된 HLS를 업로드하는 경우 이 옵션을 사용합니다. hello 파일 인코딩 및 Transform Manager를 통해 암호화 해야 합니다.

### <a name="create-an-asset"></a>자산 만들기
자산은 여러 유형이나 비디오, 오디오, 이미지, 미리 보기 컬렉션, 텍스트 트랙 및 선택된 캡션 파일을 포함한 미디어 서비스의 개체 집합에 대한 컨테이너입니다. REST API를 자산 만들기 POST를 전송 해야 하는 hello에서 tooMedia 서비스를 요청 하 고 hello 요청 본문에 자산에 대 한 속성 정보를 배치 합니다.

hello 방법을 예제와 다음 toocreate 자산입니다.

**HTTP 요청**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 201 Created
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
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>AssetFile 만들기
hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장 하는 비디오 또는 오디오 파일을 나타냅니다. 자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 AssetFile이 포함될 수 있습니다. hello 미디어 서비스 인코더 작업에는 자산 파일 개체가 blob 컨테이너의 디지털 파일과 연관 되지 않은 경우 실패 합니다.

Hello를 사용 하는 blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **병합** HTTP 요청 tooupdate hello AssetFile (같이 hello 항목의 뒷부분에 나오는) 하 여 미디어 파일에 대 한 정보입니다.

**HTTP 요청**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
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
Blob 저장소에 파일을 업로드 하기 전에 hello 액세스 tooan asset을 작성 하기 위한 정책 권한을 설정 합니다. HTTP 요청 toohello AccessPolicies 엔터티를 게시 하는 toodo 설정 합니다. 작성 시 DurationInMinutes 값을 정의하지 않으면 응답에서 500 내부 서버 오류 메시지가 다시 나타납니다. AccessPolicies에 대한 자세한 내용은 [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy)를 참조하세요.

hello 방법을 예제와 다음 toocreate AccessPolicy:

**HTTP 요청**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

**HTTP 응답**

성공 하면 다음 응답 hello 반환 됩니다.

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
    X-Powered-By: ASP.NET
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

SAS 로케이터에 대한 자세한 내용은 [이 블로그](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)를 참조하세요.

다음 예제는 hello toocreate 정의한 대로 SAS URL Locator를 (SAS 로케이터에 대 한 "1") 및 "2"에 대 한 주문형 origin locator hello 요청 본문의 Type 속성 hello 하는 방법을 보여 줍니다. hello **경로** 반환 된 속성을 사용 해야 tooupload 파일 hello URL이 포함 됩니다.

**HTTP 요청**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

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
Hello AccessPolicy와 Locator 집합 있으면 hello 실제 파일이 hello Azure 저장소 REST Api를 사용 하 여 업로드 된 tooan Azure blob 저장소 컨테이너. 블록 blob으로 hello 파일을 업로드 해야 합니다. 페이지 blob은 Azure Media Services에서 지원되지 않습니다.  

> [!NOTE]
> Hello 파일 이름을 추가 해야 tooupload toohello 로케이터 hello 파일에 대 한 원하는 **경로** hello 이전 섹션에서 받은 값입니다. 예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? 을 참조하세요. . 을 참조하세요.
>
>

Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.

### <a name="update-hello-assetfile"></a>Hello AssetFile 업데이트
파일을 업로드 한 했으므로 hello FileAsset 크기 (및 다른) 정보를 업데이트 합니다. 예:

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>Hello Locator와 AccessPolicy 삭제
**HTTP 요청**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 204 No Content
    ...

**HTTP 요청**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**HTTP 응답**

성공 하면 hello 다음 반환 됩니다.

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Hello 소스 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩

미디어 서비스에서 미디어에 자산을 인코딩할 수를 수집, 워터 마크를 삽입할 transmuxed 및 등 후 전에 제공 된다는 tooclients 합니다. 이러한 활동은 예약 되 고 여러 백그라운드 역할 인스턴스 tooensure 고성능 및 가용성에 대해 실행 합니다. 이러한 활동에는 작업 이라고 하며 각 작업 hello 자산 파일에서 실제 작업 hello 수행 하는 원자성 작업으로 구성 됩니다 (자세한 내용은 참조 [작업](/rest/api/media/services/job), [작업](/rest/api/media/services/task) 설명).

위에 언급 한 때 작업 hello 가장 일반적인 시나리오의 Azure 미디어 서비스 하나에 제공 하는 적응 비트 전송률 스트리밍 tooyour 클라이언트입니다. 미디어 서비스 hello 다음 형식 중 하나로 적응 비트 전송률 MP4 파일 집합이 동적으로 패키징할 수: HLS HTTP 라이브 스트리밍 (), 부드러운 스트리밍, MPEG DASH 합니다.

다음 단원을 hello 인코딩을 포함 하는 작업 작업 하는 toocreate 방법을 보여 줍니다. hello 작업 지정 tootranscode hello 중 2 층 파일을 사용 하 여 적응 비트 전송률 mp4 집합으로 **미디어 인코더 표준**합니다. hello 섹션에는 toomonitor 작업 처리 진행률 hello 하는 방법을 보여 줍니다. Hello 작업이 완료 되 면 수 toocreate 로케이터는 필요한 tooget tooyour 자산에 액세스 하는 것입니다.

### <a name="get-a-media-processor"></a>미디어 프로세서 가져오기
미디어 서비스에서 미디어 프로세서는 인코딩, 형식 변환, 콘텐츠, 암호화 또는 암호 해독 미디어와 같은 특정 처리 작업을 처리 하는 구성 요소입니다. 이 자습서의 예제 작업 인코딩 hello에 대 한 미디어 인코더 표준 toouse hello를 하겠습니다.

다음 코드 요청 hello 인코더의 id 번호입니다.

**HTTP 요청**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 응답**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a>작업 만들기
각 작업 하나를 사용할 수 또는 더 많은 작업 하는 처리가 hello 유형에 따라 tooaccomplish. Hello REST API를 통해 만들면 작업 및 관련된 작업에서 두 가지 방법 중 하나: 작업 hello Job 엔터티 작업 탐색 속성 또는 OData 일괄 처리를 통해 인라인으로 정의 될 수 있습니다. 미디어 서비스 SDK hello 일괄 처리를 사용합니다. 그러나이 항목의 코드 예제 hello hello 가독성을 위해 작업은 인라인으로 정의 됩니다. 일괄 처리에 대한 정보는 [Open Data Protocol(OData) 일괄 처리](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)를 참조하세요.

다음 예제는 hello 있습니다 설정 방법을 보여 줍니다 toocreate 및 post 작업 인 작업 tooencode 비디오 특정 해상도 및 품질에 있습니다. hello 설명서 섹션 뒤의 모든 hello hello 목록을 포함 [작업 사전 설정](http://msdn.microsoft.com/library/mt269960) 미디어 인코더 표준 hello 프로세서에서 지원 합니다.  

**HTTP 요청**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

**HTTP 응답**

성공 하면 다음 응답 hello 반환 됩니다.

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


모든 작업 요청에 몇 가지 중요 한 사항이 toonote가 있습니다.

* TaskBody 속성, 입력 또는 출력 자산 hello 작업에서 사용 되는 리터럴 XML toodefine hello 번호를 사용 해야 합니다. hello 작업 항목 XML hello에 대 한 hello XML 스키마 정의 포함합니다.
* TaskBody 정의 hello에 대 한 각 내부 값 <inputAsset> 및 <outputAsset> JobInputAsset(value) 또는 JobOutputAsset(value)로 설정 되어야 합니다.
* 작업 출력 자산은 여러 개일 수 있습니다. 작업에서 하나의 JobOutputAsset(x)을 작업 출력으로 한 번만 사용할 수 있습니다.
* JobInputAsset 또는 JobOutputAsset을 작업의 입력 자산으로 지정할 수 있습니다.
* 작업은 주기를 형성해서는 안됩니다.
* hello value 매개 변수 tooJobInputAsset 또는 JobOutputAsset을 전달 하는 자산에 대 한 hello 인덱스 값을 나타냅니다. hello 실제 자산에에서 정의 된 hello Job 엔터티 정의에서 hello InputMediaAssets 및 OutputMediaAssets 탐색 속성입니다.

> [!NOTE]
> 미디어 서비스는 OData v 3에서 빌드되므로 hello 개별 자산은 InputMediaAssets 및 OutputMediaAssets 탐색 속성 컬렉션을 통해 참조 되는 "__metadata: uri" 이름-값 쌍입니다.
>
>

* InputMediaAssets는 tooone 또는 미디어 서비스에서 만든 자세한 자산에 매핑합니다. Outputmediaasset은 hello 시스템에 의해 생성 됩니다. 기존 자산을 참조하지 않습니다.
* Outputmediaasset은 hello assetName 특성을 사용 하 여 이름을 지정할 수 있습니다. 이 특성이 없으면 경우 OutputMediaAsset hello의 hello 이름을 hello의 hello 내부 텍스트 값은 <outputAsset> 요소는 hello 작업 이름 값 또는 hello 작업 Id 값 (hello 경우 hello 이름 속성이 정의 되지 않습니다)의 접미사를 사용 합니다. 예를 들어 assetName에 대 한 값을 설정 하는 경우 너무 "Sample" 다음 hello OutputMediaAsset 이름 속성은 설정 너무 "Sample"입니다. 그러나 assetName에 대 한 값을 설정 하지 않은 했지만 hello 작업 이름을 설정할가 너무 "NewJob" 다음 hello OutputMediaAsset 이름은 것 "JobOutputAsset (값) _NewJob"입니다.

    다음 예제는 hello tooset assetName 특성을 hello 하는 방법을 보여 줍니다.

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* tooenable 작업 체인:

  * 작업에 작업이 2개 이상 있어야 합니다.
  * 해당 입력이 출력 hello 작업에서 다른 작업의 작업을 하나 이상 있어야 합니다.

자세한 내용은 참조 하십시오 [hello 미디어 서비스 REST API를 사용 하 여 인코딩 작업 만들기](media-services-rest-encode-asset.md)합니다.

### <a name="monitor-processing-progress"></a>처리 진행 상태 모니터링
다음 예제는 hello와 같이 hello State 속성을 사용 하 여 hello 작업 상태를 검색할 수 있습니다.

**HTTP 요청**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**HTTP 응답**

성공 하면 다음 응답 hello 반환 됩니다.

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a>작업 취소
미디어 서비스 toocancel hello CancelJob 함수를 통해 실행 중인 작업을 허용 합니다. 이 호출은 toocancel 상태로 취소 될 때 작업, 취소, 오류를 시도 하는 경우 400 오류 코드를 반환 하거나 완료 합니다.

hello 방법을 예제와 다음 toocall CancelJob 합니다.

**HTTP 요청**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


성공하는 경우 메시지 본문 없이 204 응답 코드가 반환됩니다.

> [!NOTE]
> URL로 인코드할 hello 작업 id를 해야 합니다 (일반적으로 nb:jid:UUID: somevalue) 매개 변수 tooCancelJob로 전달할 때.
>
>

### <a name="get-hello-output-asset"></a>Hello 출력 자산을 가져옵니다.
hello 다음 코드를 보여 줍니다 방법을 toorequest hello 출력 자산 id입니다.

**HTTP 요청**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 응답**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <a id="publish_get_urls"></a>Hello 자산 및 스트리밍 get 및 REST API와 점진적 다운로드 Url을 게시

toostream 또는 다운로드 자산 먼저 필요한 너무 "" 하 여 게시 한 로케이터를 만들어 합니다. 로케이터는 hello 자산에 포함 된 액세스 toofiles를 제공 합니다. 미디어 서비스는 두 가지 로케이터 유형을 지원: OnDemandOrigin 로케이터를 사용 하는 toostream 미디어 (예를 들어, MPEG DASH, HLS 또는 부드러운 스트리밍) 및 SAS (액세스 서명) locator toodownload 미디어 파일을 사용 합니다. SAS 로케이터에 대한 자세한 내용은 [이 블로그](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/)를 참조하세요.

Hello 로케이터를 만든 후에 사용 되는 toostream 또는 파일을 다운로드 하는 hello Url을 작성할 수 있습니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.

부드러운 스트리밍에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH에 대 한 스트리밍 URL 형식에 따라 hello에 있습니다.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


사용 되는 SAS URL toodownload 파일 형식에 따라 hello에 있습니다.

    {blob container name}/{asset name}/{file name}/{SAS signature}

이 섹션에서는 어떻게 tooperform hello 다음 필요한 너무 "게시 작업" 자산 보여 줍니다.  

* 읽기 권한으로 hello AccessPolicy 만들기
* 콘텐츠를 다운로드할 SAS URL 만들기
* 콘텐츠 스트리밍을 위한 원본 URL 만들기

### <a name="creating-hello-accesspolicy-with-read-permission"></a>읽기 권한으로 hello AccessPolicy 만들기
읽기 권한이 있으면 AccessPolicy를 다운로드 하거나 미디어 콘텐츠 스트리밍 하기 전에 먼저 정의 하 고 hello 형식을 지정 하는 hello 적합 한 Locator 엔터티를 만들 제공 메커니즘의 원하는 tooenable 클라이언트에 대 한 합니다. 사용할 수 있는 hello 속성에 대 한 자세한 내용은 참조 하십시오. [AccessPolicy 엔터티 속성](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties)합니다.

다음 예제는 hello toospecify 한 지정된 된 자산에 대 한 읽기 권한의 AccessPolicy를 hello 하는 방법을 보여 줍니다.

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

성공 하면 만든 hello AccessPolicy 엔터티를 설명 하는 201 성공 코드가 반환 됩니다. 그런 다음 hello (예: 출력 자산) toodeliver toocreate hello Locator 엔터티를 원하는 hello 파일을 포함 하는 hello 자산의 자산 Id와 함께 AccessPolicy Id hello를 사용 합니다.

> [!NOTE]
> 이 기본 워크플로 (이 항목의 앞부분에서 설명한)으로 자산 수집 시 파일을 업로드 동일 hello 됩니다. 또한 파일 업로드와 마찬가지로, 사용자 (또는 클라이언트) 필요 tooaccess 파일 즉시, StartTime 값 toofive 분 hello 현재 시간 전에 설정 합니다. 이 동작은 클록 hello 클라이언트 및 미디어 서비스 간에 일정 있을 수 있기 때문에 필요 합니다. 날짜/시간 형식에 따라 hello hello StartTime 값 이어야 합니다: YYYY-m M-DDTHH:mm:ssZ (예를 들어 "2014-05-23T17:53:50Z").
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>콘텐츠를 다운로드할 SAS URL 만들기
코드 다음 hello tooget 사용된 toodownload 미디어 파일 일 수 있는 URL 생성 및 방법을 이전에 업로드를 보여 줍니다. AccessPolicy hello에 대 한 읽기 권한 집합 및 hello 로케이터 경로 tooa SAS 다운로드 URL을 참조 합니다.

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

성공 하면 다음 응답 hello 반환 됩니다.

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


반환 된 hello **경로** 속성 hello SAS URL을 포함 합니다.

> [!NOTE]
> 저장소 암호화 된 콘텐츠를 다운로드 하는 경우 수동으로 렌더링 하기 전에 암호를 해독 하거나 hello 저장소 암호 해독 미디어 프로세서에서 처리 작업 toooutput hello 지우기 tooan OutputAsset의에서 파일을 처리 하 고 해당 자산에서 다운로드 한 다음 사용 합니다. 처리에 대 한 자세한 내용은 hello 미디어 서비스 REST API를 사용 하 여 인코딩 작업 만들기를 참조 하세요. 또한 SAS URL 로케이터를 만들고 나면 업데이트할 수 없습니다. 예를 들어 재사용할 수 없습니다는 업데이트 된 StartTime 값과 동일한 로케이터 hello 합니다. SAS Url을 만든 hello 방식 때문입니다. 원할 경우 tooaccess 자산 다운로드에 대 한 로케이터는 만료 된 후 다음 만들어야 새 StartTime로 새 레코드.
>
>

### <a name="download-files"></a>파일 다운로드
Hello AccessPolicy와 Locator 집합 있으면 hello Azure 저장소 REST Api를 사용 하 여 파일을 다운로드할 수 있습니다.  

> [!NOTE]
> Hello 파일 이름을 추가 해야 toodownload toohello 로케이터 hello 파일에 대 한 원하는 **경로** hello 이전 섹션에서 받은 값입니다. 예: https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? 을 참조하세요. . 을 참조하세요.
>
>

Azure 저장소 Blob 작업에 대한 자세한 내용은 [Blob 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API)를 참조하세요.

Hello 작업 이전에 수행한 인코딩 (적응 MP4 세트로 인코딩), 결과로 점진적으로 다운로드할 수 있는 여러 MP4 파일로 해야 합니다. 예:    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>콘텐츠 스트리밍을 위한 스트리밍 URL 만들기
코드에서 보여 주는 방법을 다음 hello toocreate 스트리밍 URL Locator:

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

성공 하면 다음 응답 hello 반환 됩니다.

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

스트리밍 미디어 플레이어에서 부드러운 스트리밍 원본 URL toostream 부드러운 스트리밍 매니페스트 파일을 다음 "/manifest" hello의 hello 이름의 hello 경로 속성을 추가 해야 합니다.

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

HLS toostream 추가 (형식 = m3u8 aapl) hello 후 "/manifest"입니다.

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

MPEG DASH toostream 추가 (형식 = mpd-시간-csf) hello 후 "/manifest"입니다.

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>콘텐츠 재생
비디오, 있습니다 사용할 toostream [Azure 미디어 서비스 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.

tootest 점진적 다운로드 전용는 URL (예를 들어, IE, Chrome, Safari) 브라우저에 붙여 넣습니다.

## <a name="next-steps-media-services-learning-paths"></a>다음 단계: 미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
