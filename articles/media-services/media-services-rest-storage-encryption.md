---
title: "aaaEncrypting AMS REST API를 사용 하 여 저장소 암호화를 사용 하 여 콘텐츠"
description: "자세한 내용은 방법 tooencrypt AMS REST Api를 사용 하 여 저장소 암호화를 사용 하 여 콘텐츠입니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a>저장소 암호화로 콘텐츠 암호화

Tooencrypt 권장 AES 256을 사용 하 여 로컬로 콘텐츠 비트 암호화 한 다음 암호화 된 상태로 저장 될 저장소 tooAzure 업로드 합니다.

이 문서 AMS 저장소 암호화에 대 한 개요를 제공 하 고 tooupload hello 저장소에서 콘텐츠를 암호화 하는 방법을 보여 줍니다.

* 콘텐츠 키를 만듭니다.
* 자산을 만듭니다. Hello AssetCreationOption tooStorageEncryption hello 자산을 만들 때 설정 합니다.
  
     암호화 된 자산 toobe 콘텐츠 키와 연결 된 경우
* Hello 콘텐츠 키 toohello 자산을 링크 합니다.  
* 설정 hello 암호화 관련 hello AssetFile 엔터티에서 매개 변수입니다.

## <a name="considerations"></a>고려 사항 

Toodeliver 저장소 암호화 된 자산을 원한다 면 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 hello 서버 제거 hello 저장소 암호화 및 스트림 hello를 사용 하 여 콘텐츠 스트리밍 배달 정책을 지정 합니다. 자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.

미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다. 자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요. 

## <a name="connect-toomedia-services"></a>TooMedia 서비스 연결

AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다. 

>[!NOTE]
>Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다. 후속 호출 toohello 해야 새 URI입니다.

## <a name="storage-encryption-overview"></a>저장소 암호화 개요
hello AMS 저장소 암호화 적용 **AES CTR** 모드 암호화 toohello 전체 파일입니다.  AES CTR 모드는 임의 길이 데이터를 여백 없이 암호화할 수 있는 블록 암호화입니다. Hello AES 알고리즘 및 데이터 tooencrypt hello 사용 하 여 AES의 XOR ing hello 출력 카운터 블록을 암호화 하 여 작동 또는 암호를 해독 합니다.  사용 되는 hello 카운터 블록 hello hello initializationvector입니다 toobytes 0 too7 hello 카운터 값의 값을 복사 하 여 만들어지고 hello 카운터 값의 8 바이트 too15 toozero 설정 됩니다. 8 바이트 too15 hello 16 바이트 카운터 블록의 네트워크 바이트 순서에 보관 되는 처리 된 데이터의 각 후속 블록에 대 한 1 씩 증가 하는 간단한 64 비트 부호 없는 정수 (예: hello 최하위 바이트) 사용 됩니다. 이 정수 증가 하기 최대 hello 값 (0xFFFFFFFFFFFFFFFF)에 도달 하는 경우 다른 hello hello 카운터 (예: 0 바이트 too7)의 64 비트 영향을 주지 않고 hello 블록 카운터 toozero (8 바이트 too15)을 다시 설정 하는 참고 합니다.   순서 toomaintain hello hello AES CTR 모드 암호화의 보안에서 각 콘텐츠 키 각 파일에 대해 고유 해야 합니다.에 대 한 지정된 된 키 식별자에 대 한 initializationvector입니다 값 hello 및 파일 2 보다 작은 여야 ^64 블록의 길이입니다.  이 카운터 값은 tooensure는 지정된 된 키와 다시 사용 합니다. Hello CTR 모드에 대 한 자세한 내용은 참조 [이 wiki 페이지](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello 단어 "임시"의 "initializationvector 입니다" 대신 사용 하 여 hello wiki 문서).

사용 하 여 **저장소 암호화** tooencrypt AES 256을 사용 하 여 로컬로 되어 있지 않은 콘텐츠 비트 암호화 한 다음 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다. 자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다. 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.

순서 toodeliver 저장소 암호화 된 자산을 원하는 toodeliver 콘텐츠 미디어 서비스에서 알 수 있도록 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 스트리밍 서버 제거 hello 저장소 암호화 및 스트림을 hello를 사용 하 여 콘텐츠 hello 배달 정책 (예: AES, 일반 암호화 또는 암호화 안 함)를 지정 합니다.

## <a name="create-contentkeys-used-for-encryption"></a>암호화에 사용되는 ContentKey 만들기
암호화 된 자산 toobe 저장소 암호화 키와 연결 된 경우 Hello 콘텐츠 키 toobe hello 자산 파일을 만들기 전에 암호화에 사용 되는 만들어야 합니다. 이 섹션에서는 설명 방법을 toocreate 콘텐츠 키입니다.

hello 다음은 연결할 자산 암호화 toobe 원하는 콘텐츠 키를 생성 하기 위한 일반적인 단계입니다. 

1. 저장소 암호화를 위해 32바이트 AES 키를 임의로 생성합니다. 
   
    즉, 연결 된 모든 파일이 자산에 대 한 콘텐츠 키 hello 됩니다 해당 자산에는 필요한 toouse hello 동일한 콘텐츠 키에 암호 해독 과정입니다. 
2. Hello 호출 [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 및 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 메서드 tooget hello tooencrypt 사용된 해야 하는 올바른 X.509 인증서 콘텐츠 키입니다.
3. Hello hello X.509 인증서의 공개 키로 콘텐츠 키를 암호화 합니다. 
   
   미디어 서비스.NET SDK hello 암호화를 수행할 때 OAEP와 RSA를 사용 합니다.  Hello에.NET 예제를 볼 수 있습니다 [EncryptSymmetricKeyData 함수](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)합니다.
4. Hello 키 식별자 및 콘텐츠 키를 사용 하 여 계산 된 체크섬 값을 만듭니다. 다음.NET 예제는 hello hello 키 식별자의 GUID 부분 hello를 사용 하 여 hello 체크섬을 계산 하 고 hello 콘텐츠 키를 취소 합니다.

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. Hello로 hello 콘텐츠 키를 만들 **EncryptedContentKey** (toobase64 인코딩된 문자열로 변환) **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, 및 **체크섬** 이전 단계에서 받은 값입니다.

    저장소 암호화에 대 한 hello 다음과 같은 속성이 포함 되어야 합니다 hello 요청 본문에.

    요청 본문 속성    | 설명
    ---|---
    Id | hello 생성 하는 ContentKey Id를 수행 하는 hello를 사용 하 여 직접 형식으로 "nb:kid:UUID:<NEW GUID>"입니다.
    ContentKeyType | 이 콘텐츠 키에 대 한 정수 hello 콘텐츠 키 형식입니다. 저장소 암호화에 대 한 hello 값 1을 전달합니다.
    EncryptedContentKey | 256비트(32바이트) 값인 새 콘텐츠 키 값을 만듭니다. hello 키는 hello 저장소 암호화 X.509 인증서를 hello GetProtectionKeyId 및 GetProtectionKey 메서드에 대 한 HTTP GET 요청을 실행 하 여 Microsoft Azure 미디어 서비스에서 검색을 사용 하 여 암호화 됩니다. 예를 들어.NET 코드 다음 hello 참조: hello **EncryptSymmetricKeyData** 정의 된 메서드 [여기](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)합니다.
    ProtectionKeyId | 콘텐츠 키를 사용 하는 tooencrypt hello 저장소 암호화 X.509 인증서에 대 한 보호 키 id hello는이 합니다.
    ProtectionKeyType | Hello 보호 키를 사용 하는 tooencrypt hello 콘텐츠 키에 대 한 hello 암호화 형식입니다. 이 값은 예제에서 StorageEncryption(1)입니다.
    Checksum |hello MD5 hello 콘텐츠 키에 대 한 계산 된 체크섬입니다. Hello 콘텐츠 키를 가진 hello 콘텐츠 Id를 암호화 하 여 계산 됩니다. 예제 코드에서는 hello toocalculate 체크섬 hello 하는 방법을 보여 줍니다.


### <a name="retrieve-hello-protectionkeyid"></a>Hello ProtectionKeyId를 검색 합니다.
다음 예제는 hello tooretrieve ProtectionKeyId를 콘텐츠 키를 암호화할 때 사용 해야 하는 hello 인증서에 대 한 인증서 지문을 hello 하는 방법을 보여 줍니다. 이 단계 toomake hello 적절 한 인증서는 컴퓨터에가 이미 선택 되어 있는지를 수행 합니다.

요청:

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

응답:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>ProtectionKeyId hello에 대 한 hello ProtectionKey 검색
hello 다음 예제에서는 hello ProtectionKeyId를 사용 하 여 tooretrieve hello X.509 인증서의 수령 방법 hello 이전 단계에서

요청:

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

응답:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a>Hello 콘텐츠 키 만들기
Hello X.509 인증서를 검색 하 여 콘텐츠 키의 공개 키 tooencrypt 사용 후 만들는 **ContentKey** 엔터티 및 해당 속성 값에 적절 하 게 설정 합니다.

콘텐츠 키가 hello 형식이 hello 만들 때 설정 해야 하는 hello 값 중 하나. Hello 저장소 암호화의 경우 hello 값은 '1'. 

hello 방법을 예제와 다음 toocreate는 **ContentKey** 와 **ContentKeyType** 저장소 암호화 ("1") 및 hello에 대 한 설정 **ProtectionKeyType** 설정 "0" 너무 보호 키 Id hello tooindicate hello X.509 인증서 지문입니다.  

요청

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

응답:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a>자산 만들기
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

    {"Name":"BigBuckBunny" "Options":1}

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
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a>자산에 ContentKey hello 연관
Hello ContentKey를 만든 후에 연결할 hello $links 연산을 사용 하 여 자산 hello 다음 예제와 같이:

요청:

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

응답:

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>AssetFile 만들기
hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장 하는 비디오 또는 오디오 파일을 나타냅니다. 자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 자산 파일이 포함될 수 있습니다. hello 미디어 서비스 인코더 작업에는 자산 파일 개체가 blob 컨테이너의 디지털 파일과 연관 되지 않은 경우 실패 합니다.

해당 hello 참고 **AssetFile** 인스턴스와 hello 실제 미디어 파일에는 별개의 두 개체 인스턴스가 있습니다. hello AssetFile 인스턴스 hello 미디어 파일 hello 실제 미디어 콘텐츠가 포함 되어 있지만 hello 미디어 파일에 대 한 메타 데이터를 포함 합니다.

Hello를 사용 하는 blob 컨테이너에 디지털 미디어 파일을 업로드 한 후 **병합** HTTP 요청 tooupdate hello AssetFile (이 항목에 표시 되지 않음) 하 여 미디어 파일에 대 한 정보입니다. 

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
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
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
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
