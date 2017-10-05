---
title: "Azure Media Services를 사용한 콘텐츠 보호 | Microsoft Docs"
description: "이 기사는 미디어 서비스 콘텐츠 보호에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 64be4ea104bd11b8e191e2c8d4170a2de88acb47
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protecting-content-overview"></a><span data-ttu-id="ce5d2-103">콘텐츠 보호 개요</span><span class="sxs-lookup"><span data-stu-id="ce5d2-103">Protecting content overview</span></span>
<span data-ttu-id="ce5d2-104">Microsoft Azure 미디어 서비스를 사용하면 컴퓨터를 떠날 때부터 저장, 처리 및 배달에 이르는 과정 내내 미디어를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-104">Microsoft Azure Media Services enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="ce5d2-105">Media Services를 사용하면 128비트 암호화 키를 사용하는 AES(Advanced Encryption Standard) 또는 Microsoft PlayReady, Google Widevine 및 Apple FairPlay 등 주요 DRM 중 하나로 동적 암호화된 라이브 및 주문형 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-105">Media Services allows you to deliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or any of the major DRMs: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span> <span data-ttu-id="ce5d2-106">또한 Media Services는 인증된 클라이언트에게 AES 키 및DRM(PlayReady, Widevine 및 FairPlay) 라이선스를 배달하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-106">Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses to authorized clients.</span></span> 

<span data-ttu-id="ce5d2-107">다음 이미지는 AMS가 지원하는 콘텐츠 보호 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-107">The following image demonstrates the content protection workflows that AMS supports.</span></span> 

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
><span data-ttu-id="ce5d2-109">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="ce5d2-110">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

<span data-ttu-id="ce5d2-111">이 토픽에서는 AMS를 사용한 콘텐츠 보호를 이해하는 것과 관련된 [개념 및 용어](media-services-content-protection-overview.md) 를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-111">This topic explains [concepts and terminology](media-services-content-protection-overview.md) relevant to understanding content protection with AMS.</span></span> <span data-ttu-id="ce5d2-112">토픽에는 콘텐츠 보호 태스크의 수행 방법을 보여 주는 토픽에 대한 [링크](media-services-content-protection-overview.md#common-scenarios) 도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-112">The topic also contains [links](media-services-content-protection-overview.md#common-scenarios) to topics that show how to achieve content protection tasks.</span></span> 

## <a name="dynamic-encryption"></a><span data-ttu-id="ce5d2-113">동적 암호화</span><span class="sxs-lookup"><span data-stu-id="ce5d2-113">Dynamic encryption</span></span>
<span data-ttu-id="ce5d2-114">Microsoft Azure Media Services를 사용하면 AES 암호화되지 않은 키 또는 Microsoft PlayReady, Google Widevine 및 Apple FairPlay 등과 같은 DRM 암호화로 동적 암호화된 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-114">Microsoft Azure Media Services enables you to deliver your content encrypted  dynamically with AES clear key or DRM encryption: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span>

<span data-ttu-id="ce5d2-115">현재 암호화할 수 있는 스트리밍 형식은 HLS, MPEG DASH 및 부드러운 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-115">Currently, you can encrypt the following streaming formats: HLS, MPEG DASH, and Smooth Streaming.</span></span> <span data-ttu-id="ce5d2-116">점진적 다운로드를 암호화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-116">You cannot encrypt progressive downloads.</span></span>

<span data-ttu-id="ce5d2-117">미디어 서비스에서 자산을 암호화하려는 경우 암호화 키(CommonEncryption 또는 EnvelopeEncryption)를 자산에 연결하고 해당 키에 대해 권한 부여 정책도 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-117">If you want for Media Services to encrypt an asset, you need to associate an encryption key (CommonEncryption or EnvelopeEncryption) with your asset and also configure authorization policies for the key.</span></span>

<span data-ttu-id="ce5d2-118">또한 자산의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-118">You also need to configure the asset's delivery policy.</span></span> <span data-ttu-id="ce5d2-119">저장소에서 암호화된 자산을 스트리밍하려면 자산 배달 정책을 구성하여 배달 방법을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-119">If you want to stream a storage encrypted asset, make sure to specify how you want to deliver it by configuring asset delivery policy.</span></span>

<span data-ttu-id="ce5d2-120">플레이어가 스트림을 요청하면 Media Services는 지정된 키를 사용하고 AES 암호화되지 않은 키 또는 DRM 암호화를 사용하여 동적으로 사용자의 콘텐츠를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-120">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES clear key or DRM encryption.</span></span> <span data-ttu-id="ce5d2-121">스트림을 해독하기 위해 플레이어는 키 배달 서비스에서 키를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-121">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="ce5d2-122">사용자에게 키를 얻을 수 있는 권한이 있는지 여부를 결정하기 위해 서비스는 키에 지정된 권한 부여 정책을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-122">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>


## <a name="storage-encryption"></a><span data-ttu-id="ce5d2-123">저장소 암호화</span><span class="sxs-lookup"><span data-stu-id="ce5d2-123">Storage encryption</span></span>
<span data-ttu-id="ce5d2-124">AES 256비트 암호화를 사용하여 암호화되지 않은 콘텐츠를 로컬에서 암호화한 다음에 암호화되어 저장된 Azure Storage에 업로드하려면 저장소 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-124">Use storage encryption to encrypt your clear content locally using AES 256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ce5d2-125">저장소 암호화로 보호된 자산은 자동으로 암호 해제되어 인코딩되기 전에 암호화된 파일 시스템에 배치됩니다. 그리고 필요에 따라 새 출력 자산으로 다시 업로드되기 전에 다시 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-125">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="ce5d2-126">저장소 암호화를 사용하는 기본적인 사례는 디스크에 저장된 상태일 때 강력한 암호화로 고품질의 입력 미디어 파일을 보호하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-126">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="ce5d2-127">저장소에서 암호화된 자산을 배달하려면 미디어 서비스에서 콘텐츠 배달 방법을 알 수 있도록 자산의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-127">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="ce5d2-128">자산을 스트리밍하기 전에 스트리밍 서버에서 저장소 암호화를 제거하고 지정된 배달 정책(예: AES, 일반 암호화 또는 암호화 없음)을 사용하여 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-128">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="common-encryption-cenc"></a><span data-ttu-id="ce5d2-129">CENC(일반 암호화)</span><span class="sxs-lookup"><span data-stu-id="ce5d2-129">Common encryption (CENC)</span></span>
<span data-ttu-id="ce5d2-130">일반 암호화는 PlayReady 또는/및 Widewine으로 콘텐츠를 암호화하는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-130">Common encryption is used when encrypting your content with PlayReady or/and Widewine.</span></span>

## <a name="using-cbcs-aapl-encryption"></a><span data-ttu-id="ce5d2-131">cbcs-aapl 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ce5d2-131">Using cbcs-aapl encryption</span></span>
<span data-ttu-id="ce5d2-132">cbcs-aapl은 FairPlay로 콘텐츠를 암호화하는 경우 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-132">Cbcs-aapl is used when encrypting your content with FairPlay.</span></span>

## <a name="envelope-encryption"></a><span data-ttu-id="ce5d2-133">봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="ce5d2-133">Envelope encryption</span></span>
<span data-ttu-id="ce5d2-134">AES-128 암호화되지 않은 키로 콘텐츠를 보호하려는 경우 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-134">Use this option if you want to protect your content with AES-128 clear key.</span></span> <span data-ttu-id="ce5d2-135">이보다 안전한 옵션을 원하는 경우 이 토픽에 나열된 DRM 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-135">If you want a more secure option, choose one of the DRMs listed in this topic.</span></span> 

## <a name="licenses-and-keys-delivery-service"></a><span data-ttu-id="ce5d2-136">라이선스 및 키 배달 서비스</span><span class="sxs-lookup"><span data-stu-id="ce5d2-136">Licenses and keys delivery service</span></span>
<span data-ttu-id="ce5d2-137">Media Services는 DRM(PlayReady, Widevine, FairPlay) 라이선스 및 AES 암호화되지 않은 키를 인증된 클라이언트에 배달하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-137">Media Services provides a service for delivering DRM (PlayReady, Widevine, FairPlay) licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="ce5d2-138">[Azure Portal](media-services-portal-protect-content.md), REST API 또는 .NET용 Media Services SDK를 사용하여 라이선스 및 키에 대한 권한 부여 및 인증 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-138">You can use [the Azure portal](media-services-portal-protect-content.md), REST API, or Media Services SDK for .NET to configure authorization and authentication policies for your licenses and keys.</span></span>

## <a name="token-restriction"></a><span data-ttu-id="ce5d2-139">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="ce5d2-139">Token restriction</span></span>
<span data-ttu-id="ce5d2-140">콘텐츠 키 권한 부여 정책에는 열기 또는 토큰 제한과 같은 하나 이상의 권한 부여 제한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-140">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="ce5d2-141">토큰 제한 정책은 보안 토큰 서비스(STS)에 의해 발급된 토큰이 수반되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-141">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="ce5d2-142">미디어 서비스 지원 토큰에는 간단한 웹 토큰(SWT) 형식 및 JSON 웹 토큰(JWT) 형식의 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-142">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="ce5d2-143">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-143">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="ce5d2-144">사용자 지정 STS를 만들거나 Microsoft Azure ACS를 활용하여 토큰을 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-144">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="ce5d2-145">지정된 키로 서명된 토큰을 만들고 토큰 제한 구성에서 지정한 클레임을 발급하려면 반드시 STS를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-145">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="ce5d2-146">토큰이 유효하고 해당 토큰의 클레임이 키(또는 라이선스)에 대해 구성된 클레임과 일치하는 경우 미디어 서비스 키 배달 서비스는 요청된 키(또는 라이선스)를 클라이언트에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-146">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="ce5d2-147">토큰 제한 정책을 구성하는 경우 기본 확인 키, 발급자 및 대상 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-147">When configuring the token restricted policy, you must specify the primary verification key, issuer and audience parameters.</span></span> <span data-ttu-id="ce5d2-148">기본 확인 키는 토큰이 서명된 키를 포함하며 발급자는 토큰을 발행하는 보안 토큰 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-148">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="ce5d2-149">청중(범위) 라고도 함)은 토큰의 의도 또는 토큰이 접근을 인증하는 대상 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-149">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="ce5d2-150">미디어 서비스 키 배달 서비스는 이러한 토큰의 값이 템플릿 파일에 있는 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-150">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

## <a name="streaming-urls"></a><span data-ttu-id="ce5d2-151">스트리밍 URL</span><span class="sxs-lookup"><span data-stu-id="ce5d2-151">Streaming URLs</span></span>
<span data-ttu-id="ce5d2-152">자산이 하나 이상의 DRM으로 암호화되어 있는 경우 스트리밍 URL에서 암호화 태그를 사용해야 합니다(형식='m3u8-aapl', 암호화='xxx').</span><span class="sxs-lookup"><span data-stu-id="ce5d2-152">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="ce5d2-153">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-153">The following considerations apply:</span></span>

* <span data-ttu-id="ce5d2-154">1개 이하의 암호화 형식만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-154">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="ce5d2-155">하나의 암호화가 자산에 적용되었다면 암호화 형식을 URL에 지정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-155">Encryption type doesn't have to be specified in the url if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="ce5d2-156">암호화 형식은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-156">Encryption type is case insensitive.</span></span>
* <span data-ttu-id="ce5d2-157">다음과 같은 암호화 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-157">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="ce5d2-158">**cenc**: 일반 암호화(Playready 또는 Widevine)</span><span class="sxs-lookup"><span data-stu-id="ce5d2-158">**cenc**:  Common encryption (Playready or Widevine)</span></span>
  * <span data-ttu-id="ce5d2-159">**cbcs-aapl**: Fairplay</span><span class="sxs-lookup"><span data-stu-id="ce5d2-159">**cbcs-aapl**: Fairplay</span></span>
  * <span data-ttu-id="ce5d2-160">**cbc**: AES 봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="ce5d2-160">**cbc**: AES envelope encryption.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="ce5d2-161">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="ce5d2-161">Common scenarios</span></span>
<span data-ttu-id="ce5d2-162">다음 토픽에서는 저장소의 콘텐츠를 보호하고, 암호화된 스트리밍 미디어를 동적으로 배달하며, AMS 키/라이선스 배달 서비스를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-162">The following topics demonstrate how to protect content in storage, deliver dynamically encrypted streaming media, use AMS key/license delivery service</span></span>

* [<span data-ttu-id="ce5d2-163">AES로 보호</span><span class="sxs-lookup"><span data-stu-id="ce5d2-163">Protect with AES</span></span>](media-services-protect-with-aes128.md) 
* [<span data-ttu-id="ce5d2-164">PlayReady 및/또는 Widevine으로 보호 </span><span class="sxs-lookup"><span data-stu-id="ce5d2-164">Protect with PlayReady and/or Widevine </span></span>](media-services-protect-with-drm.md)
* [<span data-ttu-id="ce5d2-165">Apple FairPlay 및/또는 PlayReady로 보호되는 HLS 콘텐츠 스트림</span><span class="sxs-lookup"><span data-stu-id="ce5d2-165">Stream your HLS content Protected with Apple FairPlay and/or PlayReady</span></span>](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a><span data-ttu-id="ce5d2-166">추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="ce5d2-166">Additional scenarios</span></span>
* <span data-ttu-id="ce5d2-167">[암호기/스트리밍 서버와 함께 Azure PlayReady License 서비스를 통합하는 방법](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)</span><span class="sxs-lookup"><span data-stu-id="ce5d2-167">[How to integrate Azure PlayReady License service with your own encryptor/streaming server](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).</span></span>
* [<span data-ttu-id="ce5d2-168">castLabs를 사용하여 Azure 미디어 서비스에 DRM 라이선스 제공</span><span class="sxs-lookup"><span data-stu-id="ce5d2-168">Using castLabs to deliver DRM licenses to Azure Media Services</span></span>](media-services-castlabs-integration.md)

>[!NOTE]
><span data-ttu-id="ce5d2-169">외부 DRM 서버(기술)를 사용하고 AMS에서 스트리밍하는 시나리오는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-169">A scenario in which you use an external DRM server(technology) and stream from AMS is currently not supported.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ce5d2-170">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ce5d2-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ce5d2-171">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ce5d2-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ce5d2-172">관련 링크</span><span class="sxs-lookup"><span data-stu-id="ce5d2-172">Related Links</span></span>
[<span data-ttu-id="ce5d2-173">Azure 미디어 서비스를 사용하여 AES 동적 암호화로 PlayReady 발표</span><span class="sxs-lookup"><span data-stu-id="ce5d2-173">Announcing PlayReady as a service and AES dynamic encryption with Azure Media Services</span></span>](http://mingfeiy.com/playready)

[<span data-ttu-id="ce5d2-174">Azure 미디어 서비스 PlayReady 라이선스 배달 가격 설명</span><span class="sxs-lookup"><span data-stu-id="ce5d2-174">Azure Media Services PlayReady license delivery pricing explained</span></span>](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[<span data-ttu-id="ce5d2-175">Azure 미디어 서비스에서 AES 암호화된 스트림에 대한 디버깅 방법</span><span class="sxs-lookup"><span data-stu-id="ce5d2-175">How to debug for AES encrypted stream in Azure Media Services</span></span>](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[<span data-ttu-id="ce5d2-176">JWT 토큰 인증을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce5d2-176">JWT token authenitcation</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="ce5d2-177">[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="ce5d2-177">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="ce5d2-178">[Azure ACS를 사용하여 토큰을 발급합니다](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="ce5d2-178">[Use Azure ACS to issue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
