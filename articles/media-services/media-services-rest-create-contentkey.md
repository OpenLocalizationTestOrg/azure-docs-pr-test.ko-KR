---
title: "REST를 사용하여 콘텐츠 키 만들기 | Microsoft Docs"
description: "자산에 대한 보안 액세스를 제공하는 콘텐츠 키를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ece09277d26fafb7c0eebf62730031c4dc01bfe0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="ec2ce-103">REST를 사용하여 콘텐츠 키 만들기</span><span class="sxs-lookup"><span data-stu-id="ec2ce-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec2ce-104">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="ec2ce-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="ec2ce-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ec2ce-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="ec2ce-106">미디어 서비스를 사용하면 암호화된 자산을 새로 만들어서 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-106">Media Services enables you to create new and deliver encrypted assets.</span></span> <span data-ttu-id="ec2ce-107">**ContentKey**는 **자산**에 대한 보안 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="ec2ce-108">새 자산을 만들 때(예: [파일 업로드](media-services-rest-upload-files.md) 전) **StorageEncrypted**, **CommonEncryptionProtected** 또는 **EnvelopeEncryptionProtected** 암호화 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="ec2ce-109">클라이언트에 자산을 제공할 때 **DynamicEnvelopeEncryption** 또는 **DynamicCommonEncryption** 암호화 중 하나를 사용하여 [자산이 동적으로 암호화되도록 구성](media-services-rest-configure-asset-delivery-policy.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="ec2ce-110">암호화된 자산은 **ContentKey**와 연관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="ec2ce-111">이 문서에서는 콘텐츠 키를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-111">This article describes how to create a content key.</span></span>

<span data-ttu-id="ec2ce-112">다음은 암호화하려는 자산과 연결할 콘텐츠 키를 생성하기 위한 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-112">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="ec2ce-113">16바이트 AES 키(일반 및 봉투 암호화의 경우) 또는 32 바이트 AES 키(저장소 암호화의 경우)를 임의로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="ec2ce-114">이는 자산에 대한 콘텐츠 키로 암호화하는 동안 해당 자산과 연결된 모든 파일이 동일한 콘텐츠 키를 사용해야 한다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-114">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="ec2ce-115">[GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 및 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 메서드를 호출하여 콘텐츠 키를 암호화하는 데 사용해야 하는 올바른 X.509 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-115">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="ec2ce-116">X.509 인증서의 공개 키로 콘텐츠 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-116">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="ec2ce-117">Media Services.NET SDK는 암호화 시 OAEP가 포함된 RSA를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-117">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="ec2ce-118">[EncryptSymmetricKeyData 함수](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)에서 예를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-118">You can see an example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="ec2ce-119">키 식별자 및 콘텐츠 키를 사용하여 계산된 체크섬 값(PlayReady AES 키 체크섬 알고리즘에 기반)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-119">Create a checksum value (based on the PlayReady AES key checksum algorithm) calculated using the key identifier and content key.</span></span> <span data-ttu-id="ec2ce-120">자세한 내용은 [여기](http://www.microsoft.com/playready/documents/)에 있는 PlayReady 헤더 개체 문서의 "PlayReady AES 키 체크섬 알고리즘" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-120">For more information, see the “PlayReady AES Key Checksum Algorithm” section of the PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="ec2ce-121">다음은 키 식별자와 암호화되지 않은 콘텐츠 키의 GUID 부분을 사용하여 체크섬을 계산하는 .NET 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-121">The following is a .NET example that calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

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
5. <span data-ttu-id="ec2ce-122">이전 단계에서 받은**EncryptedContentKey**(base64 인코딩된 문자열로 변환), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** 및 **Checksum** 값을 사용하여 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-122">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="ec2ce-123">$links 작업을 통해 **ContentKey** 엔터티와 **Asset** 엔터티를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-123">Associate the **ContentKey** entity with your **Asset** entity through the $links operation.</span></span>

<span data-ttu-id="ec2ce-124">이 토픽은 AES 키 생성, 키 암호화 및 체크섬을 계산하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-124">Note that this topic does not show how to generate an AES key, encrypt the key, and calculate the checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="ec2ce-125">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ec2ce-126">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="ec2ce-127">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="ec2ce-127">Connect to Media Services</span></span>

<span data-ttu-id="ec2ce-128">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-128">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ec2ce-129">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-129">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ec2ce-130">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-130">You must make subsequent calls to the new URI.</span></span>

## <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="ec2ce-131">ProtectionKeyId 검색</span><span class="sxs-lookup"><span data-stu-id="ec2ce-131">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="ec2ce-132">다음 예제에서는 콘텐츠 키를 암호화할 때 사용해야 하는 인증서의 ProtectionKeyId(인증서 지문)를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-132">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="ec2ce-133">컴퓨터에 적절한 인증서가 이미 있는지 확인하려면 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-133">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="ec2ce-134">요청:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="ec2ce-135">응답:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-135">Response:</span></span>

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

## <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="ec2ce-136">ProtectionKeyId에 대한 Protectionkey 검색</span><span class="sxs-lookup"><span data-stu-id="ec2ce-136">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="ec2ce-137">다음 예제에서는 이전 단계에서 받은 ProtectionKeyId를 사용하여 X.509 인증서를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-137">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="ec2ce-138">요청:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="ec2ce-139">응답:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-139">Response:</span></span>

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

## <a name="create-the-contentkey"></a><span data-ttu-id="ec2ce-140">ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="ec2ce-140">Create the ContentKey</span></span>
<span data-ttu-id="ec2ce-141">X.509 인증서를 검색한 다음 이 인증서의 공개 키를 사용하여 콘텐츠 키를 암호화한 후 **ContentKey** 엔터티를 만들고 해당 속성 값을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-141">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="ec2ce-142">콘텐츠 키를 만들 때 설정해야 하는 값 중 하나가 이 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-142">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="ec2ce-143">다음 값 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-143">Choose from one of the following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
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


<span data-ttu-id="ec2ce-144">다음 예제에서는 저장소 암호화("1")에 대해 설정된 **ContentKeyType**과 "0"으로 설정된 **ProtectionKeyType**으로 **ContentKey**를 만들어서 보호 키 Id가 X.509 인증서 지문임을 나타내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-144">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="ec2ce-145">요청</span><span class="sxs-lookup"><span data-stu-id="ec2ce-145">Request</span></span>

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


<span data-ttu-id="ec2ce-146">응답:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-146">Response:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="ec2ce-147">자산으로 ContentKey 연결</span><span class="sxs-lookup"><span data-stu-id="ec2ce-147">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="ec2ce-148">ContentKey를 만든 후 다음 예제와 같이 $links 작업을 사용하여 이를 자산에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ec2ce-148">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="ec2ce-149">요청:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-149">Request:</span></span>

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

<span data-ttu-id="ec2ce-150">응답:</span><span class="sxs-lookup"><span data-stu-id="ec2ce-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="ec2ce-151">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ec2ce-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ec2ce-152">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ec2ce-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

