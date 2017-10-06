---
title: ".NET SDK를 사용 하 여 aaaConfigure 자산 배달 정책을 | Microsoft Docs"
description: "이 항목에서는 방법을 Azure 미디어 서비스.NET SDK를 사용 하 여 tooconfigure 다른 자산 배달 정책을 합니다."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a>.NET SDK를 사용하여 자산 배포 정책 구성
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a>개요
자산 암호화 toodelivery 하려는 경우 단계 중 하나 hello hello 미디어 서비스 콘텐츠 배달 워크플로 자산에 대 한 배달 정책을 구성 합니다. hello 자산 배달 정책 미디어 서비스 프로그램 자산 toobe 배달에 대해 원하는 방법을 알려 줍니다: 스트리밍 프로토콜에 자산 패키지 되어야 하며 동적으로 (예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), 용 toodynamically 원하는 여부 자산 암호화 및 방법 (봉투 (envelope) 또는 일반 암호화) 합니다.

이 항목에서는 근거, 방법 설명 toocreate 고 자산 배달 정책을 구성 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 
>
>또한 toobe 수 toouse 동적 패키징 및 동적 암호화 자산인 있어야 적응 비트 전송률 mp4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합입니다.


Toohello 각기 다른 정책을 적용할 수 동일한 자산입니다. 예를 들어 PlayReady 암호화 tooSmooth 스트리밍 및 AES 봉투 (envelope) 암호화 tooMPEG를 적용할 수 있습니다 DASH 및 HLS입니다. 배달 정책에 정의 되어 있지 않은 모든 프로토콜 (예를 들어 추가한만 hello 프로토콜로 HLS를 지정 하는 단일 정책을) 스트리밍에서 차단 됩니다. hello 예외 toothis는 없는 자산 배달 정책을 정의 해야 합니다. 그런 다음 모든 프로토콜이 일반 hello에 허용 됩니다.

Toodeliver 저장소 암호화 된 자산을 원한다 면 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 hello 서버 제거 hello 저장소 암호화 및 스트림 hello를 사용 하 여 콘텐츠 스트리밍 배달 정책을 지정 합니다. 예를 들어 toodeliver 자산 암호화 표준 AES (고급) 봉투 (envelope) 암호화 키로 암호화, 너무 hello 정책 형식을 설정**DynamicEnvelopeEncryption**합니다. tooremove 저장소 암호화 및 명확 hello에 스트림 hello 자산 hello 정책 형식을 설정 너무**NoDynamicEncryption**합니다. 이러한 정책 형식과 수행 하는 tooconfigure 방법을 보여 주는 예제입니다.

Hello 자산 배달 정책을 구성 하는 방법에 따라 것 수 toodynamically 패키지 수, 동적으로 암호화 하 고 스트림 스트리밍 프로토콜을 따르는 hello: 부드러운 스트리밍, HLS 및 MPEG DASH 스트림을 합니다.

hello 다음 목록은 hello 형식 toostream 부드러운 스트리밍, HLS 및 대시를 사용 하는입니다.

부드러운 스트리밍:

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS:

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

MPEG DASH

{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


## <a name="considerations"></a>고려 사항
* 자산에 대한 주문형(스트리밍) 로케이터가 있는 동안 해당 자산과 연결된 AssetDeliveryPolicy를 삭제할 수 없습니다. hello 권장은 hello 정책 삭제 하기 전에 hello 자산에서 tooremove hello 정책입니다.
* 자산 배달 정책이 설정되지 않은 경우 암호화된 저장소 자산에 스트리밍 로케이터를 만들 수 없습니다.  Hello 자산 없는 경우 저장소 암호화,이 hello 시스템은 자산 배달 정책 없이 지우기 hello에 로케이터 및 스트림 hello 자산을 만들 수 있습니다.
* 단일 자산과 연결 된 여러 자산 배달 정책을 있는데는 한 가지 방법은 toohandle 주어진된 AssetDeliveryProtocol만 지정할 수 있습니다.  모르기 때문에 hello 시스템 어떤 것에서 오류가 발생 하는 hello AssetDeliveryProtocol.SmoothStreaming 프로토콜을 지정 하는 toolink 두 배달 정책을 시도 하는 경우 의미 원하는 tooapply 때 클라이언트에서 부드러운 스트리밍 요청 합니다.
* 기존 스트리밍 로케이터는 자산 있는 경우 새 정책 toohello 자산 (기존 정책을 hello 자산에서의 연결을 해제 하거나 hello 자산과 연결 된 배달 정책을 업데이트)를 연결할 수 없습니다.  먼저 tooremove hello 스트리밍 로케이터, hello 정책을 조정 있고 hello 스트리밍 로케이터를 다시 만들어야 합니다.  Hello 원본이 나 다운스트림 CDN에서 콘텐츠를 캐시할 수 있으므로 클라이언트에 대 한 문제를 발생 하지 않습니다 스트리밍 로케이터 있지만 hello를 다시 만들 때 동일한 locatorId 확인 해야 하는 hello를 사용할 수 있습니다.

## <a name="clear-asset-delivery-policy"></a>자산 배달 정책 지우기

hello 다음 **ConfigureClearAssetDeliveryPolicy** 메서드 지정 toonot 동적 암호화를 적용 하 고 프로토콜을 통해 hello 다음 중 하나에서 toodeliver hello 스트림을: MPEG DASH, HLS 및 부드러운 스트리밍 프로토콜입니다. 이 정책 tooyour 저장소 암호화 된 자산 tooapply를 할 수 있습니다.

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a>DynamicCommonEncryption 자산 배달 정책

hello 다음 **CreateAssetDeliveryPolicy** 메서드 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 일반 암호화 (**DynamicCommonEncryption**) tooa 부드러운 스트리밍 프로토콜 (다른 프로토콜 스트리밍에서 차단 됩니다). 두 개의 매개 변수를 사용 하는 hello 메서드: **자산** (tooapply hello 배달 정책을 자산 toowhich hello) 및 **IContentKey** (hello 콘텐츠 키의 hello **CommonEncryption**자세한 내용은 형식/참조: [콘텐츠 키를 만드는](media-services-dotnet-create-contentkey.md#common_contentkey)).

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

Azure 미디어 서비스 tooadd Widevine 암호화를 사용 합니다. hello 다음 예제에서는 PlayReady와 Widevine toohello 자산 배달 정책을 추가

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> Widevine를 암호화 하는 경우 대시를 사용 하 여 수 toodeliver만 있을 수 있습니다. Hello 자산 배달 프로토콜에서 있는지 toospecify 대시를 확인 합니다.
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a>DynamicEnvelopeEncryption 자산 배달 정책
hello 다음 **CreateAssetDeliveryPolicy** 메서드 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 봉투 암호화 (**DynamicEnvelopeEncryption** ) tooSmooth 스트리밍, HLS 및 DASH 프로토콜 (경우 결정 toonot 지정 일부 프로토콜, 스트리밍에서 차단 됩니다). 두 개의 매개 변수를 사용 하는 hello 메서드: **자산** (tooapply hello 배달 정책을 자산 toowhich hello) 및 **IContentKey** (hello 콘텐츠 키의 hello **EnvelopeEncryption**자세한 내용은 형식/참조: [콘텐츠 키를 만드는](media-services-dotnet-create-contentkey.md#envelope_contentkey)).

Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <a id="types"></a>AssetDeliveryPolicy를 정의할 때 사용되는 형식

### <a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol

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

### <a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType

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

### <a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType

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

### <a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey

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

