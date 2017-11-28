---
title: "REST로 내용 키 aaaCreate | Microsoft Docs"
description: "보안을 제공 하는 콘텐츠 키를 toocreate tooAssets를 액세스 하는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95e9322b-168e-4a9d-8d5d-d7c946103745
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: cb3b74bdb72c43ab5b375c0376b6704f4a93bb8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="a7f52-103">REST를 사용하여 콘텐츠 키 만들기</span><span class="sxs-lookup"><span data-stu-id="a7f52-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7f52-104">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="a7f52-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="a7f52-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a7f52-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="a7f52-106">미디어 서비스 toocreate 새 있으며 암호화 된 자산을 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-106">Media Services enables you toocreate new and deliver encrypted assets.</span></span> <span data-ttu-id="a7f52-107">A **ContentKey** 보안 액세스 tooyour 제공 **자산**s입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-107">A **ContentKey** provides secure access tooyour **Asset**s.</span></span> 

<span data-ttu-id="a7f52-108">새 자산을 만드는 경우 (예를 들어 하기 전에 [파일 업로드](media-services-rest-upload-files.md)), hello 다음 암호화 옵션을 지정할 수 있습니다: **StorageEncrypted**, **CommonEncryptionProtected**, 또는 **EnvelopeEncryptionProtected**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify hello following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="a7f52-109">Tooyour 클라이언트를 자산을 배달 하는 경우 다음을 할 수 있습니다 [자산 toobe 동적으로 암호화에 대 한 구성](media-services-rest-configure-asset-delivery-policy.md) hello 다음 두 가지 암호화 중 하 나와: **DynamicEnvelopeEncryption** 또는  **DynamicCommonEncryption**합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-109">When you deliver assets tooyour clients, you can [configure for assets toobe dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of hello following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="a7f52-110">암호화 된 자산에 연결 된 toobe가 **ContentKey**s입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-110">Encrypted assets have toobe associated with **ContentKey**s.</span></span> <span data-ttu-id="a7f52-111">이 문서에서는 설명 방법을 toocreate 콘텐츠 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-111">This article describes how toocreate a content key.</span></span>

<span data-ttu-id="a7f52-112">hello 다음은 연결할 자산 암호화 toobe 원하는 콘텐츠 키를 생성 하기 위한 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-112">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="a7f52-113">16바이트 AES 키(일반 및 봉투 암호화의 경우) 또는 32 바이트 AES 키(저장소 암호화의 경우)를 임의로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="a7f52-114">즉, 연결 된 모든 파일이 자산에 대 한 콘텐츠 키 hello 됩니다 해당 자산에는 필요한 toouse hello 동일한 콘텐츠 키에 암호 해독 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-114">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="a7f52-115">Hello 호출 [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 및 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 메서드 tooget hello tooencrypt 사용된 해야 하는 올바른 X.509 인증서 콘텐츠 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-115">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="a7f52-116">Hello hello X.509 인증서의 공개 키로 콘텐츠 키를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-116">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="a7f52-117">미디어 서비스.NET SDK hello 암호화를 수행할 때 OAEP와 RSA를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-117">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="a7f52-118">Hello에 예제를 볼 수 [EncryptSymmetricKeyData 함수](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-118">You can see an example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="a7f52-119">체크섬 값 (PlayReady AES 키 체크섬 알고리즘 hello에 기반) hello 키 식별자 및 콘텐츠 키를 사용 하 여 계산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-119">Create a checksum value (based on hello PlayReady AES key checksum algorithm) calculated using hello key identifier and content key.</span></span> <span data-ttu-id="a7f52-120">자세한 내용은 참조 hello hello PlayReady 헤더 개체에 대 한 문서의 "PlayReady AES 키 체크섬 알고리즘" 섹션에 있는 [여기](http://www.microsoft.com/playready/documents/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-120">For more information, see hello “PlayReady AES Key Checksum Algorithm” section of hello PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="a7f52-121">hello 다음은 hello 키 식별자의 GUID 부분 hello를 사용 하 여 hello 체크섬을 계산 하는.NET 예제 및 hello 콘텐츠 키의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-121">hello following is a .NET example that calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

         public static string CalculateChecksum(byte[] contentKey, Guid keyId)
         {

            byte[] array = null;
            using (AesCryptoServiceProvider aesCryptoServiceProvider = new AesCryptoServiceProvider())
            {
                aesCryptoServiceProvider.Mode = CipherMode.ECB;
                aesCryptoServiceProvider.Key = contentKey;
                aesCryptoServiceProvider.Padding = PaddingMode.None;
                ICryptoTransform cryptoTransform = aesCryptoServiceProvider.CreateEncryptor();
                array = new byte[16];
                cryptoTransform.TransformBlock(keyId.ToByteArray(), 0, 16, array, 0);
            }
            byte[] array2 = new byte[8];
            Array.Copy(array, array2, 8);
            return Convert.ToBase64String(array2);
         }
5. <span data-ttu-id="a7f52-122">Hello로 hello 콘텐츠 키를 만들 **EncryptedContentKey** (toobase64 인코딩된 문자열로 변환) **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, 및 **체크섬** 이전 단계에서 받은 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-122">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="a7f52-123">연결 hello **ContentKey** 엔터티와 사용자 **자산** hello $links 작업을 통해 엔터티.</span><span class="sxs-lookup"><span data-stu-id="a7f52-123">Associate hello **ContentKey** entity with your **Asset** entity through hello $links operation.</span></span>

<span data-ttu-id="a7f52-124">Note이 항목 toogenerate는 AES 키 hello 키를 암호화 하 고 hello 체크섬을 계산 하는 방법을 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-124">Note that this topic does not show how toogenerate an AES key, encrypt hello key, and calculate hello checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="a7f52-125">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a7f52-126">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7f52-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="a7f52-127">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="a7f52-127">Connect tooMedia Services</span></span>

<span data-ttu-id="a7f52-128">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-128">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a7f52-129">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-129">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a7f52-130">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-130">You must make subsequent calls toohello new URI.</span></span>

## <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="a7f52-131">Hello ProtectionKeyId를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-131">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="a7f52-132">다음 예제는 hello tooretrieve ProtectionKeyId를 콘텐츠 키를 암호화할 때 사용 해야 하는 hello 인증서에 대 한 인증서 지문을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-132">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="a7f52-133">이 단계 toomake hello 적절 한 인증서는 컴퓨터에가 이미 선택 되어 있는지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-133">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="a7f52-134">요청:</span><span class="sxs-lookup"><span data-stu-id="a7f52-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="a7f52-135">응답:</span><span class="sxs-lookup"><span data-stu-id="a7f52-135">Response:</span></span>

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

## <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="a7f52-136">ProtectionKeyId hello에 대 한 hello ProtectionKey 검색</span><span class="sxs-lookup"><span data-stu-id="a7f52-136">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="a7f52-137">hello 다음 예제에서는 hello ProtectionKeyId를 사용 하 여 tooretrieve hello X.509 인증서의 수령 방법 hello 이전 단계에서</span><span class="sxs-lookup"><span data-stu-id="a7f52-137">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="a7f52-138">요청:</span><span class="sxs-lookup"><span data-stu-id="a7f52-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="a7f52-139">응답:</span><span class="sxs-lookup"><span data-stu-id="a7f52-139">Response:</span></span>

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

## <a name="create-hello-contentkey"></a><span data-ttu-id="a7f52-140">Hello ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="a7f52-140">Create hello ContentKey</span></span>
<span data-ttu-id="a7f52-141">Hello X.509 인증서를 검색 하 여 콘텐츠 키의 공개 키 tooencrypt 사용 후 만들는 **ContentKey** 엔터티 및 해당 속성 값에 적절 하 게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-141">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="a7f52-142">콘텐츠 키가 hello 형식이 hello 만들 때 설정 해야 하는 hello 값 중 하나.</span><span class="sxs-lookup"><span data-stu-id="a7f52-142">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="a7f52-143">Hello 다음 값 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-143">Choose from one of hello following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }


<span data-ttu-id="a7f52-144">hello 방법을 예제와 다음 toocreate는 **ContentKey** 와 **ContentKeyType** 저장소 암호화 ("1") 및 hello에 대 한 설정 **ProtectionKeyType** 설정 "0" 너무 보호 키 Id hello tooindicate hello X.509 인증서 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="a7f52-144">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="a7f52-145">요청</span><span class="sxs-lookup"><span data-stu-id="a7f52-145">Request</span></span>

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


<span data-ttu-id="a7f52-146">응답:</span><span class="sxs-lookup"><span data-stu-id="a7f52-146">Response:</span></span>

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

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="a7f52-147">자산에 ContentKey hello 연관</span><span class="sxs-lookup"><span data-stu-id="a7f52-147">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="a7f52-148">Hello ContentKey를 만든 후에 연결할 hello $links 연산을 사용 하 여 자산 hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="a7f52-148">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="a7f52-149">요청:</span><span class="sxs-lookup"><span data-stu-id="a7f52-149">Request:</span></span>

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

<span data-ttu-id="a7f52-150">응답:</span><span class="sxs-lookup"><span data-stu-id="a7f52-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="a7f52-151">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a7f52-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7f52-152">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a7f52-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

