---
title: "AMS REST API를 사용하여 저장소 암호화로 콘텐츠 암호화"
description: "AMS REST API를 사용하여 저장소 암호화로 콘텐츠를 암호화하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="07e90-103">저장소 암호화로 콘텐츠 암호화</span><span class="sxs-lookup"><span data-stu-id="07e90-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="07e90-104">AES-256비트 암호화를 사용하여 암호화되지 않은 콘텐츠를 로컬에서 암호화한 다음 암호화된 상태로 저장할 Azure 저장소에 이를 업로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="07e90-105">이 문서에서는 AMS 저장소 암호화에 대한 개요를 제공하며, 저장소 암호화된 콘텐츠를 업로드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="07e90-106">콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-106">Create a content key.</span></span>
* <span data-ttu-id="07e90-107">자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-107">Create an Asset.</span></span> <span data-ttu-id="07e90-108">자산을 만들 때 AssetCreationOption을 StorageEncryption으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="07e90-109">암호화된 자산을 콘텐츠 키와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="07e90-110">콘텐츠 키를 자산에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="07e90-111">AssetFile 엔터티에서 암호화 관련 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="07e90-112">고려 사항</span><span class="sxs-lookup"><span data-stu-id="07e90-112">Considerations</span></span> 

<span data-ttu-id="07e90-113">저장소에서 암호화된 자산을 배달하려는 경우 자산의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="07e90-114">자산을 스트리밍하기 전에 스트리밍 서버가 저장소 암호화를 제거하고 지정된 배달 정책을 사용하여 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="07e90-115">자세한 내용은 [자산 배달 정책 구성](media-services-rest-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e90-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="07e90-116">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="07e90-117">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e90-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="07e90-118">미디어 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="07e90-118">Connect to Media Services</span></span>

<span data-ttu-id="07e90-119">AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e90-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="07e90-120">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="07e90-121">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="07e90-122">저장소 암호화 개요</span><span class="sxs-lookup"><span data-stu-id="07e90-122">Storage encryption overview</span></span>
<span data-ttu-id="07e90-123">AMS 저장소 암호화는 **AES-CTR** 모드 암호화를 전체 파일에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="07e90-124">AES CTR 모드는 임의 길이 데이터를 여백 없이 암호화할 수 있는 블록 암호화입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="07e90-125">AES 알고리즘으로 카운터 블록을 암호화한 다음 암호화 또는 해독할 데이터에 대해 AES의 출력을 XOR 연산하는 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="07e90-126">사용되는 카운터 블록은 카운터 값의 0~7바이트에 InitializationVector 값을 복사하여 구조화되며 카운터 값의 8~15바이트는 0으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="07e90-127">16바이트 카운터 블록에서 8~15바이트(즉 최하위 바이트)는 부호 없는 64비트 단순 정수로 사용되며, 처리되는 후속 데이터 블록마다 1씩 증가하고 네트워크 바이트 순으로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="07e90-128">이 정수가 최대값(0xFFFFFFFFFFFFFFFF)에 도달했을 때 이 값이 증가하면 카운터의 다른 64비트(즉 0~7바이트)에 미치는 영향 없이 블록 카운트가 0(8~15바이트)으로 재설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="07e90-129">AES-CTR 모드 암호화의 보안 유지를 위해 각 콘텐츠 키의 지정된 키 식별자에 대한 InitializationVector 값은 파일마다 고유해야 하며 파일 길이는 2^64블록 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="07e90-130">이것은 카운터 값이 특정 키에서 재사용되지 않게 하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="07e90-131">CTR 모드에 대한 자세한 내용은 [이 wiki 페이지](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) 를 참조하세요(wiki 문서에서는 "InitializationVector" 대신 "Nonce"라는 용어를 사용함).</span><span class="sxs-lookup"><span data-stu-id="07e90-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="07e90-132">AES 256비트 암호화를 사용하여 암호화되지 않은 콘텐츠를 로컬에서 암호화한 다음에 암호화되어 저장된 Azure Storage에 업로드하려면 **저장소 암호화**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="07e90-133">저장소 암호화로 보호된 자산은 자동으로 암호 해제되어 인코딩되기 전에 암호화된 파일 시스템에 배치됩니다. 그리고 필요에 따라 새 출력 자산으로 다시 업로드되기 전에 다시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="07e90-134">저장소 암호화를 사용하는 기본적인 사례는 디스크에 저장된 상태일 때 강력한 암호화로 고품질의 입력 미디어 파일을 보호하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="07e90-135">저장소에서 암호화된 자산을 배달하려면 미디어 서비스에서 콘텐츠 배달 방법을 알 수 있도록 자산의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="07e90-136">자산을 스트리밍하기 전에 스트리밍 서버에서 저장소 암호화를 제거하고 지정된 배달 정책(예: AES, 일반 암호화 또는 암호화 없음)을 사용하여 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="07e90-137">암호화에 사용되는 ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="07e90-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="07e90-138">암호화된 자산을 저장소 암호화 키에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="07e90-139">자산 파일을 만들기 전에 암호화에 사용할 콘텐츠 키를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="07e90-140">이 섹션에서는 콘텐츠 키를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="07e90-141">다음은 암호화하려는 자산과 연결할 콘텐츠 키를 생성하기 위한 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="07e90-142">저장소 암호화를 위해 32바이트 AES 키를 임의로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="07e90-143">이는 자산에 대한 콘텐츠 키로 암호화하는 동안 해당 자산과 연결된 모든 파일이 동일한 콘텐츠 키를 사용해야 한다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="07e90-144">[GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 및 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 메서드를 호출하여 콘텐츠 키를 암호화하는 데 사용해야 하는 올바른 X.509 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="07e90-145">X.509 인증서의 공개 키로 콘텐츠 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="07e90-146">Media Services.NET SDK는 암호화 시 OAEP가 포함된 RSA를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="07e90-147">[EncryptSymmetricKeyData 함수](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)에서 .NET 예제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="07e90-148">키 식별자 및 콘텐츠 키를 사용하여 계산된 체크섬 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="07e90-149">다음.NET 예제에서는 키 식별자와 암호화되지 않은 콘텐츠 키의 GUID 부분을 사용하여 체크섬을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
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

1. <span data-ttu-id="07e90-150">이전 단계에서 받은**EncryptedContentKey**(base64 인코딩된 문자열로 변환), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType** 및 **Checksum** 값을 사용하여 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="07e90-151">저장소 암호화를 위해 다음 속성을 요청 본문에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="07e90-152">요청 본문 속성</span><span class="sxs-lookup"><span data-stu-id="07e90-152">Request body property</span></span>    | <span data-ttu-id="07e90-153">설명</span><span class="sxs-lookup"><span data-stu-id="07e90-153">Description</span></span>
    ---|---
    <span data-ttu-id="07e90-154">Id</span><span class="sxs-lookup"><span data-stu-id="07e90-154">Id</span></span> | <span data-ttu-id="07e90-155">“nb:kid:UUID:<NEW GUID>” 형식을 사용하여 직접 생성하는 ContentKey Id입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="07e90-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="07e90-156">ContentKeyType</span></span> | <span data-ttu-id="07e90-157">이 콘텐츠 키에 대한 정수인 콘텐츠 키 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="07e90-158">저장소 암호화에 1값을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="07e90-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="07e90-159">EncryptedContentKey</span></span> | <span data-ttu-id="07e90-160">256비트(32바이트) 값인 새 콘텐츠 키 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="07e90-161">GetProtectionKeyId 및 GetProtectionKey 메서드에 대한 HTTP GET 요청을 실행하여 Microsoft Azure 미디어 서비스에서 검색하는 저장소 암호화 X.509 인증서를 사용하여 키를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="07e90-162">.NET 코드에 대한 예제로, **여기** 에 정의된 [EncryptSymmetricKeyData](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)메서드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07e90-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="07e90-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="07e90-163">ProtectionKeyId</span></span> | <span data-ttu-id="07e90-164">콘텐츠 키를 암호화하는 데 사용한 저장소 암호화 X.509 인증서에 대한 보호 키 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="07e90-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="07e90-165">ProtectionKeyType</span></span> | <span data-ttu-id="07e90-166">콘텐츠 키를 암호화하는 데 사용한 보호 키에 대한 암호화 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="07e90-167">이 값은 예제에서 StorageEncryption(1)입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="07e90-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="07e90-168">Checksum</span></span> |<span data-ttu-id="07e90-169">콘텐츠 키에 대한 MD5 계산 된 체크섬입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="07e90-170">콘텐츠 키로 콘텐츠 ID를 암호화하여 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="07e90-171">예제 코드는 체크섬을 계산하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="07e90-172">ProtectionKeyId 검색</span><span class="sxs-lookup"><span data-stu-id="07e90-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="07e90-173">다음 예제에서는 콘텐츠 키를 암호화할 때 사용해야 하는 인증서의 ProtectionKeyId(인증서 지문)를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="07e90-174">컴퓨터에 적절한 인증서가 이미 있는지 확인하려면 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="07e90-175">요청:</span><span class="sxs-lookup"><span data-stu-id="07e90-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="07e90-176">응답:</span><span class="sxs-lookup"><span data-stu-id="07e90-176">Response:</span></span>

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

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="07e90-177">ProtectionKeyId에 대한 Protectionkey 검색</span><span class="sxs-lookup"><span data-stu-id="07e90-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="07e90-178">다음 예제에서는 이전 단계에서 받은 ProtectionKeyId를 사용하여 X.509 인증서를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="07e90-179">요청:</span><span class="sxs-lookup"><span data-stu-id="07e90-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="07e90-180">응답:</span><span class="sxs-lookup"><span data-stu-id="07e90-180">Response:</span></span>

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

### <a name="create-the-content-key"></a><span data-ttu-id="07e90-181">콘텐츠 키 만들기</span><span class="sxs-lookup"><span data-stu-id="07e90-181">Create the content key</span></span>
<span data-ttu-id="07e90-182">X.509 인증서를 검색한 다음 이 인증서의 공개 키를 사용하여 콘텐츠 키를 암호화한 후 **ContentKey** 엔터티를 만들고 해당 속성 값을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="07e90-183">콘텐츠 키를 만들 때 설정해야 하는 값 중 하나가 이 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="07e90-184">저장소 암호화의 경우 값은 '1'입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="07e90-185">다음 예제에서는 저장소 암호화("1")에 대해 설정된 **ContentKeyType**과 "0"으로 설정된 **ProtectionKeyType**으로 **ContentKey**를 만들어서 보호 키 Id가 X.509 인증서 지문임을 나타내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="07e90-186">요청</span><span class="sxs-lookup"><span data-stu-id="07e90-186">Request</span></span>

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

<span data-ttu-id="07e90-187">응답:</span><span class="sxs-lookup"><span data-stu-id="07e90-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="07e90-188">자산 만들기</span><span class="sxs-lookup"><span data-stu-id="07e90-188">Create an asset</span></span>
<span data-ttu-id="07e90-189">다음 예제에서는 자산을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="07e90-190">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="07e90-190">**HTTP Request**</span></span>

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

<span data-ttu-id="07e90-191">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="07e90-191">**HTTP Response**</span></span>

<span data-ttu-id="07e90-192">성공하면 다음이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-192">If successful, the following is returned:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="07e90-193">자산으로 ContentKey 연결</span><span class="sxs-lookup"><span data-stu-id="07e90-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="07e90-194">ContentKey를 만든 후 다음 예제와 같이 $links 작업을 사용하여 이를 자산에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="07e90-195">요청:</span><span class="sxs-lookup"><span data-stu-id="07e90-195">Request:</span></span>

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

<span data-ttu-id="07e90-196">응답:</span><span class="sxs-lookup"><span data-stu-id="07e90-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="07e90-197">AssetFile 만들기</span><span class="sxs-lookup"><span data-stu-id="07e90-197">Create an AssetFile</span></span>
<span data-ttu-id="07e90-198">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 엔터티는 blob 컨테이너에 저장된 비디오 또는 오디오 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="07e90-199">자산 파일은 항상 자산에 연결되며 자산에는 하나 이상의 자산 파일이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="07e90-200">자산 파일 개체가 blob 컨테이너의 디지털 파일과 연결되지 않은 경우 미디어 서비스 인코더 작업을 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="07e90-201">**AssetFile** 인스턴스와 실제 미디어 파일은 뚜렷이 다른 두 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="07e90-202">AssetFile 인스턴스는 미디어 파일에 대한 메타데이터를 포함하는 반면 미디어 파일은 실제 미디어 콘텐츠를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="07e90-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="07e90-203">Blob 컨테이너에 디지털 미디어 파일을 업로드하면 **MERGE** HTTP 요청을 사용하여 미디어 파일에 대한 정보로 AssetFile을 업데이트하게 됩니다(이 토픽에 나와 있지 않음).</span><span class="sxs-lookup"><span data-stu-id="07e90-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="07e90-204">**HTTP 요청**</span><span class="sxs-lookup"><span data-stu-id="07e90-204">**HTTP Request**</span></span>

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

<span data-ttu-id="07e90-205">**HTTP 응답**</span><span class="sxs-lookup"><span data-stu-id="07e90-205">**HTTP Response**</span></span>

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
