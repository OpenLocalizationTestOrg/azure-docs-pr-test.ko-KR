---
title: .net Contentkey aaaCreate
description: "보안을 제공 하는 콘텐츠 키를 toocreate tooAssets를 액세스 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a>.NET을 사용하여 Contentkey 만들기
> [!div class="op_single_selector"]
> * [REST (영문)](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

미디어 서비스 toocreate 있으며 암호화 된 자산을 배달 합니다. A **ContentKey** 보안 액세스 tooyour 제공 **자산**s입니다. 

새 자산을 만드는 경우 (예를 들어 하기 전에 [파일 업로드](media-services-dotnet-upload-files.md)), hello 다음 암호화 옵션을 지정할 수 있습니다: **StorageEncrypted**, **CommonEncryptionProtected**, 또는 **EnvelopeEncryptionProtected**합니다. 

Tooyour 클라이언트를 자산을 배달 하는 경우 다음을 할 수 있습니다 [자산 toobe 동적으로 암호화에 대 한 구성](media-services-dotnet-configure-asset-delivery-policy.md) hello 다음 두 가지 암호화 중 하 나와: **DynamicEnvelopeEncryption** 또는  **DynamicCommonEncryption**합니다.

암호화 된 자산에 연결 된 toobe가 **ContentKey**s입니다. 이 문서에서는 설명 방법을 toocreate 콘텐츠 키입니다.

> [!NOTE]
> 새로 만들 때 **StorageEncrypted** 사용 하 여 자산 hello 미디어 서비스.NET SDK hello **ContentKey** 가 자동으로 만들어지고 hello 자산에 연결 됩니다.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
콘텐츠를 만들 때 설정 해야 하는 hello 값 중 하나 키는 hello 콘텐츠 키 형식입니다. Hello 다음 값 중 하나를 선택 합니다. 

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

## <a id="envelope_contentkey"></a>봉투 유형의 ContentKey 만들기
hello 다음 코드 조각에서는 hello 봉투 암호화 형식의 콘텐츠 키입니다. 그런 다음 hello 키 hello 지정 된 자산에 연결합니다.

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

다음을 호출합니다.

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>일반 유형의 ContentKey 만들기
hello 다음 코드 조각에서는 hello 일반 암호화 종류의 콘텐츠 키입니다. 그런 다음 hello 키 hello 지정 된 자산에 연결합니다.

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

        // Associate hello key with hello asset.
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
다음을 호출합니다.

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

