---
title: ".NET을 사용하여 Contentkey 만들기"
description: "자산에 대한 보안 액세스를 제공하는 콘텐츠 키를 만드는 방법에 대해 알아봅니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="b44f2-103">.NET을 사용하여 Contentkey 만들기</span><span class="sxs-lookup"><span data-stu-id="b44f2-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b44f2-104">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b44f2-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="b44f2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b44f2-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="b44f2-106">미디어 서비스를 사용하면 암호화된 자산을 만들어서 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="b44f2-107">**ContentKey**는 **자산**에 대한 보안 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="b44f2-108">새 자산을 만들 때(예: [파일 업로드](media-services-dotnet-upload-files.md) 전) **StorageEncrypted**, **CommonEncryptionProtected** 또는 **EnvelopeEncryptionProtected** 암호화 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="b44f2-109">클라이언트에 자산을 제공할 때 **DynamicEnvelopeEncryption** 또는 **DynamicCommonEncryption** 암호화 중 하나를 사용하여 [자산이 동적으로 암호화되도록 구성](media-services-dotnet-configure-asset-delivery-policy.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="b44f2-110">암호화된 자산은 **ContentKey**와 연관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="b44f2-111">이 문서에서는 콘텐츠 키를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="b44f2-112">Media Services .NET SDK를 사용하여 새 **StorageEncrypted** 자산을 만들 때, **ContentKey**가 자동으로 생성되며 해당 자산과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="b44f2-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="b44f2-113">ContentKeyType</span></span>
<span data-ttu-id="b44f2-114">콘텐츠 키를 만들 때 설정해야 하는 값 중 하나가 콘텐츠 키 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="b44f2-115">다음 값 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-115">Choose from one of the following values.</span></span> 

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

## <span data-ttu-id="b44f2-116"><a id="envelope_contentkey"></a>봉투 유형의 ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="b44f2-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="b44f2-117">다음 코드 조각은 봉투 암호화 유형의 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="b44f2-118">그런 다음 키를 지정된 자산과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-118">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="b44f2-119">다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="b44f2-120"><a id="common_contentkey"></a>일반 유형의 ContentKey 만들기</span><span class="sxs-lookup"><span data-stu-id="b44f2-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="b44f2-121">다음 코드 조각은 일반 암호화 유형의 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="b44f2-122">그런 다음 키를 지정된 자산과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-122">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate the key with the asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="b44f2-123">다음을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b44f2-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="b44f2-124">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b44f2-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b44f2-125">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b44f2-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

