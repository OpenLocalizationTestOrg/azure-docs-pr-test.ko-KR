---
title: ".NET SDK를 사용하여 자산 배달 정책 구성 | Microsoft 문서"
description: "이 항목에서는 Azure Media Services.NET SDK를 사용하여 여러 자산 배달 정책을 구성하는 방법을 설명합니다."
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
ms.openlocfilehash: 282fd9e24dc147e31613469926128894d48366f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="b5a08-103">.NET SDK를 사용하여 자산 배포 정책 구성</span><span class="sxs-lookup"><span data-stu-id="b5a08-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="b5a08-104">개요</span><span class="sxs-lookup"><span data-stu-id="b5a08-104">Overview</span></span>
<span data-ttu-id="b5a08-105">암호화된 자산을 배달하려는 경우 미디어 서비스 콘텐츠 배달 워크플로의 단계 중 하나는 자산에 대한 배달 정책을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-105">If you plan to delivery encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="b5a08-106">자산 배달 정책은 어떤 스트리밍 프로토콜(예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두)로 사용자의 자산을 동적으로 패키지할 지와 같은 사용자가 원하는 자산 배달 방법과 사용자의 자산을 동적으로 암호화할 지 여부 및 방법(봉투 또는 일반 암호화)를 미디어 서비스에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-106">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="b5a08-107">이 항목에서는 자산 배달 정책을 만들고 구성하는 이유와 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-107">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="b5a08-108">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-108">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="b5a08-109">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-109">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="b5a08-110">또한 동적 패키징 및 동적 암호화를 사용하려면 자산이 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-110">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="b5a08-111">동일한 자산에 다른 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-111">You could apply different policies to the same asset.</span></span> <span data-ttu-id="b5a08-112">예를 들어, 부드러운 스트리밍에 PlayReady 암호화, MPEG DASH 및 HLS에 AES 봉투(envelope) 암호화를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-112">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="b5a08-113">배달 정책에 정의되지 않은 모든 프로토콜(예: HLS만 프로토콜로 지정하는 단일 정책)은 스트리밍에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="b5a08-114">정의한 자산 배달 정책이 없는 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-114">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="b5a08-115">이렇게 하면 모든 프로토콜이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-115">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="b5a08-116">저장소에서 암호화된 자산을 배달하려는 경우 자산의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-116">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="b5a08-117">자산을 스트리밍하기 전에 스트리밍 서버가 저장소 암호화를 제거하고 지정된 배달 정책을 사용하여 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-117">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="b5a08-118">예를 들어 표준 AES 봉투 암호화 키로 암호화된 자산을 배달하려면 정책 유형을 **DynamicEnvelopeEncryption**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-118">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="b5a08-119">저장소 암호화를 제거하고 암호화되지 않은 자산을 스트리밍하려면 정책 유형을 **NoDynamicEncryption**으로 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="b5a08-119">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="b5a08-120">이러한 정책 유형을 구성 하는 방법을 보여주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-120">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="b5a08-121">사용자가 자산 배달 정책을 구성하는 방법에 따라 다음 스트리밍 프로토콜을 동적으로 패키지하고, 동적으로 암호화하고 스트림할 수 있습니다(부드러운 스트리밍, HLS 및 MPEG DASH 스트림).</span><span class="sxs-lookup"><span data-stu-id="b5a08-121">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="b5a08-122">다음 목록에서는 부드러운 스트리밍, HLS 및 DASH 등의 프로토콜을 스트리밍할 때 사용하는 형식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-122">The following list shows the formats that you use to stream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="b5a08-123">부드러운 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="b5a08-123">Smooth Streaming:</span></span>

<span data-ttu-id="b5a08-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="b5a08-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="b5a08-125">HLS:</span><span class="sxs-lookup"><span data-stu-id="b5a08-125">HLS:</span></span>

<span data-ttu-id="b5a08-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="b5a08-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="b5a08-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="b5a08-127">MPEG DASH</span></span>

<span data-ttu-id="b5a08-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="b5a08-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="b5a08-129">고려 사항</span><span class="sxs-lookup"><span data-stu-id="b5a08-129">Considerations</span></span>
* <span data-ttu-id="b5a08-130">자산에 대한 주문형(스트리밍) 로케이터가 있는 동안 해당 자산과 연결된 AssetDeliveryPolicy를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="b5a08-131">정책을 삭제하기 전에 자산에서 정책을 제거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="b5a08-132">자산 배달 정책이 설정되지 않은 경우 암호화된 저장소 자산에 스트리밍 로케이터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="b5a08-133">자산이 암호화된 저장소가 아닌 경우 시스템에서 로케이터를 만들고 자산 배달 정책 없이 일반 텍스트인 자산을 스트리밍할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="b5a08-134">단일 자산과 여러 자산 배달 정책을 연결하여 사용할 수 있지만 지정된 AssetDeliveryProtocol을 처리하는 방법은 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="b5a08-135">즉, AssetDeliveryProtocol.SmoothStreaming 프로토콜을 지정하는 두 가지 배달 정책을 연결하려는 경우 클라이언트가 부드러운 스트리밍을 요청할 때 시스템이 어떤 정책을 적용할지 모르기 때문에 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="b5a08-136">기존 스트리밍 로케이터를 사용하는 자산이 있는 경우 해당 자산에 새 정책을 연결할 수 없습니다. 자산에서 기존 정책의 연결을 해제하거나 자산과 연결된 배달 정책을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset (you can either unlink an existing policy from the asset, or update a delivery policy associated with the asset).</span></span>  <span data-ttu-id="b5a08-137">먼저 스트리밍 로케이터를 제거하고, 정책을 조정한 다음, 스트리밍 로케이터를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="b5a08-138">스트리밍 로케이터를 다시 만들 때 동일한 locatorId를 사용할 수 있지만 원본 또는 다운스트림 CDN이 콘텐츠를 캐시할 수 있으므로 클라이언트에 문제가 발생하지 않는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="b5a08-139">자산 배달 정책 지우기</span><span class="sxs-lookup"><span data-stu-id="b5a08-139">Clear asset delivery policy</span></span>

<span data-ttu-id="b5a08-140">다음 **ConfigureClearAssetDeliveryPolicy** 메서드는 동적 암호화를 적용하지 않고 MPEG DASH, HLS 및 부드러운 스트리밍 프로토콜 중 하나에서 스트림을 배달하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-140">The following **ConfigureClearAssetDeliveryPolicy** method specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="b5a08-141">이 정책을 저장소에서 암호화된 자산에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-141">You might want to apply this policy to your storage encrypted assets.</span></span>

<span data-ttu-id="b5a08-142">AssetDeliveryPolicy을 만들 때 사용자가 지정하는 값에 대한 자세한 정보는 [AssetDeliveryPolicy를 정의할 때 사용되는 형식](#types) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5a08-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="b5a08-143">DynamicCommonEncryption 자산 배달 정책</span><span class="sxs-lookup"><span data-stu-id="b5a08-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="b5a08-144">다음 **CreateAssetDeliveryPolicy** 메서드는 부드러운 스트리밍 프로토콜에 동적 일반 암호화(**DynamicCommonEncryption**)를 적용하도록 구성된 **AssetDeliveryPolicy**를 만듭니다(스트리밍에서 다른 프로토콜은 차단됨).</span><span class="sxs-lookup"><span data-stu-id="b5a08-144">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to a smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="b5a08-145">이 메서드는 두 매개 변수, 즉 **Asset**(배달 정책을 적용하려는 자산) 및 **IContentKey**(**CommonEncryption** 유형의 콘텐츠 키, 자세한 내용은 [콘텐츠 키 만들기](media-services-dotnet-create-contentkey.md#common_contentkey) 참조)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-145">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="b5a08-146">AssetDeliveryPolicy을 만들 때 사용자가 지정하는 값에 대한 자세한 정보는 [AssetDeliveryPolicy를 정의할 때 사용되는 형식](#types) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5a08-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

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
    
            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="b5a08-147">Azure 미디어 서비스를 사용하면 Widevine 암호화를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-147">Azure Media Services also enables you to add Widevine encryption.</span></span> <span data-ttu-id="b5a08-148">다음 예제에서는 PlayReady 및 Widevine이 자산 배달 정책에 추가되는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-148">The following example demonstrates both PlayReady and Widevine being added to the asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get the PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // to append /? KID =< keyId > to the end of the url when creating the manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

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


        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="b5a08-149">Widevine을 사용하여 암호화하는 경우 DASH를 통해서만 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-149">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="b5a08-150">자산 배달 프로토콜에서 DASH를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-150">Make sure to specify DASH in the asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="b5a08-151">DynamicEnvelopeEncryption 자산 배달 정책</span><span class="sxs-lookup"><span data-stu-id="b5a08-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="b5a08-152">다음 **CreateAssetDeliveryPolicy** 메서드는 부드러운 스트리밍, HLS 및 DASH 프로토콜에 동적 봉투 암호화(**DynamicEnvelopeEncryption**)를 적용하도록 구성된 **AssetDeliveryPolicy**를 만듭니다(일부 프로토콜은 지정되지 않으면 스트리밍에서 차단됨).</span><span class="sxs-lookup"><span data-stu-id="b5a08-152">The following **CreateAssetDeliveryPolicy** method creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to Smooth Streaming, HLS, and DASH protocols (if you decide to not specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="b5a08-153">이 메서드는 두 매개 변수, 즉 **Asset**(배달 정책을 적용하려는 자산) 및 **IContentKey**(**EnvelopeEncryption** 유형의 콘텐츠 키, 자세한 내용은 [콘텐츠 키 만들기](media-services-dotnet-create-contentkey.md#envelope_contentkey) 참조)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-153">The method takes two parameters : **Asset** (the asset to which you want to apply the delivery policy) and **IContentKey** (the content key of the **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="b5a08-154">AssetDeliveryPolicy을 만들 때 사용자가 지정하는 값에 대한 자세한 정보는 [AssetDeliveryPolicy를 정의할 때 사용되는 형식](#types) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5a08-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get the Key Delivery Base Url by removing the Query parameter.  The Dynamic Encryption service will
        //  automatically add the correct key identifier to the url when it generates the Envelope encrypted content
        //  manifest.  Omitting the IV will also cause the Dynamice Encryption service to generate a deterministic
        //  IV for the content automatically.  By using the EnvelopeBaseKeyAcquisitionUrl and omitting the IV, this
        //  allows the AssetDelivery policy to be reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // The following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended to the envelope and
        //   the Initialization Vector (IV) to use for the envelope encryption.
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

        // Add AssetDelivery Policy to the asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="b5a08-155"><a id="types"></a>AssetDeliveryPolicy를 정의할 때 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="b5a08-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="b5a08-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="b5a08-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="b5a08-157">다음 열거형은 자산 배달 프로토콜에 대해 설정할 수 있는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-157">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <span data-ttu-id="b5a08-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="b5a08-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="b5a08-159">다음 열거형은 자산 배달 정책 유형에 대해 설정할 수 있는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-159">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <span data-ttu-id="b5a08-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="b5a08-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="b5a08-161">다음 열거형은 클라이언트로의 콘텐츠 키 배달 방법을 구성하는 데 사용할 수 있는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-161">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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

### <span data-ttu-id="b5a08-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="b5a08-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="b5a08-163">다음 열거형은 자산 배달 정책에 대한 특정 구성을 가져오는 데 사용되는 키를 구성하기 위해 설정할 수 있는 값을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5a08-163">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="b5a08-164">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b5a08-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b5a08-165">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b5a08-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

