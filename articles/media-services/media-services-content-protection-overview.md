---
title: "aaaProtect Azure 미디어 서비스를 사용 하 여 콘텐츠 | Microsoft Docs"
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
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a><span data-ttu-id="ee30a-103">콘텐츠 보호 개요</span><span class="sxs-lookup"><span data-stu-id="ee30a-103">Protecting content overview</span></span>
<span data-ttu-id="ee30a-104">Microsoft Azure 미디어 서비스 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-104">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="ee30a-105">미디어 서비스에서는 라이브 및 주문형 콘텐츠에 사용 하 여 동적으로 암호화 toodeliver 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 또는 hello 주요 DRMs: Microsoft PlayReady, Google Widevine 및 Apple FairPlay 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-105">Media Services allows you toodeliver your live and on-demand content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys) or any of hello major DRMs: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span> <span data-ttu-id="ee30a-106">또한 미디어 서비스 AES 키 배달용 서비스를 제공 하 고 DRM (PlayReady, Widevine, 및 FairPlay) tooauthorized 클라이언트 라이선스 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-106">Media Services also provides a service for delivering AES keys and DRM (PlayReady, Widevine, and FairPlay) licenses tooauthorized clients.</span></span> 

<span data-ttu-id="ee30a-107">다음 이미지는 hello AMS 지원 hello 콘텐츠 보호 워크플로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-107">hello following image demonstrates hello content protection workflows that AMS supports.</span></span> 

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
><span data-ttu-id="ee30a-109">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ee30a-110">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="ee30a-111">이 항목에서는 설명 [개념 및 용어](media-services-content-protection-overview.md) 관련 toounderstanding AMS로 내용을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-111">This topic explains [concepts and terminology](media-services-content-protection-overview.md) relevant toounderstanding content protection with AMS.</span></span> <span data-ttu-id="ee30a-112">hello 항목에 포함 되어 [링크](media-services-content-protection-overview.md#common-scenarios) 방법을 tooachieve 콘텐츠 보호 작업을 보여 주는 tootopics 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-112">hello topic also contains [links](media-services-content-protection-overview.md#common-scenarios) tootopics that show how tooachieve content protection tasks.</span></span> 

## <a name="dynamic-encryption"></a><span data-ttu-id="ee30a-113">동적 암호화</span><span class="sxs-lookup"><span data-stu-id="ee30a-113">Dynamic encryption</span></span>
<span data-ttu-id="ee30a-114">Microsoft Azure 미디어 서비스 사용 하면 콘텐츠 지우기 키 AES 또는 DRM 암호화를 사용 하 여 동적으로 암호화 toodeliver: Microsoft PlayReady, Google Widevine 및 Apple FairPlay 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-114">Microsoft Azure Media Services enables you toodeliver your content encrypted  dynamically with AES clear key or DRM encryption: Microsoft PlayReady, Google Widevine, and Apple FairPlay.</span></span>

<span data-ttu-id="ee30a-115">현재 다음 스트리밍 형식 hello를 암호화할 수 있습니다: HLS, MPEG DASH, 부드러운 스트리밍 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-115">Currently, you can encrypt hello following streaming formats: HLS, MPEG DASH, and Smooth Streaming.</span></span> <span data-ttu-id="ee30a-116">점진적 다운로드를 암호화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-116">You cannot encrypt progressive downloads.</span></span>

<span data-ttu-id="ee30a-117">에 대해 원하는 tooencrypt 미디어 서비스 자산, 자산을 사용 하 여 암호화 키 (CommonEncryption 또는 EnvelopeEncryption) tooassociate 필요한 고 hello 키에 대 한 권한 부여 정책을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-117">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (CommonEncryption or EnvelopeEncryption) with your asset and also configure authorization policies for hello key.</span></span>

<span data-ttu-id="ee30a-118">Tooconfigure hello 자산의 배달 정책을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-118">You also need tooconfigure hello asset's delivery policy.</span></span> <span data-ttu-id="ee30a-119">Toostream 저장소 암호화 된 자산을 확인 방법을 있는지 toospecify toodeliver 자산 배달 정책을 구성 하 여 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-119">If you want toostream a storage encrypted asset, make sure toospecify how you want toodeliver it by configuring asset delivery policy.</span></span>

<span data-ttu-id="ee30a-120">미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically 지우기 키 AES를 사용 하 여 콘텐츠 또는 DRM 암호화를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-120">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES clear key or DRM encryption.</span></span> <span data-ttu-id="ee30a-121">toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-121">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="ee30a-122">hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-122">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>


## <a name="storage-encryption"></a><span data-ttu-id="ee30a-123">저장소 암호화</span><span class="sxs-lookup"><span data-stu-id="ee30a-123">Storage encryption</span></span>
<span data-ttu-id="ee30a-124">저장소 암호화 tooencrypt AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 사용 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-124">Use storage encryption tooencrypt your clear content locally using AES 256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="ee30a-125">자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-125">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="ee30a-126">강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-126">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="ee30a-127">순서 toodeliver 저장소 암호화 된 자산을 원하는 toodeliver 콘텐츠 미디어 서비스에서 알 수 있도록 hello 자산의 배달 정책을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-127">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="ee30a-128">자산을 스트리밍하기 전에 스트리밍 서버 제거 hello 저장소 암호화 및 스트림을 hello를 사용 하 여 콘텐츠 hello 배달 정책 (예: AES, 일반 암호화 또는 암호화 안 함)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-128">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="common-encryption-cenc"></a><span data-ttu-id="ee30a-129">CENC(일반 암호화)</span><span class="sxs-lookup"><span data-stu-id="ee30a-129">Common encryption (CENC)</span></span>
<span data-ttu-id="ee30a-130">일반 암호화는 PlayReady 또는/및 Widewine으로 콘텐츠를 암호화하는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-130">Common encryption is used when encrypting your content with PlayReady or/and Widewine.</span></span>

## <a name="using-cbcs-aapl-encryption"></a><span data-ttu-id="ee30a-131">cbcs-aapl 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="ee30a-131">Using cbcs-aapl encryption</span></span>
<span data-ttu-id="ee30a-132">cbcs-aapl은 FairPlay로 콘텐츠를 암호화하는 경우 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-132">Cbcs-aapl is used when encrypting your content with FairPlay.</span></span>

## <a name="envelope-encryption"></a><span data-ttu-id="ee30a-133">봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="ee30a-133">Envelope encryption</span></span>
<span data-ttu-id="ee30a-134">원하는 tooprotect 콘텐츠 aes-128 암호화 되지 않은 키와이 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-134">Use this option if you want tooprotect your content with AES-128 clear key.</span></span> <span data-ttu-id="ee30a-135">보다 안전한 옵션을 사용 하도록 하려는 경우이 항목에 나열 된 hello DRMs 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-135">If you want a more secure option, choose one of hello DRMs listed in this topic.</span></span> 

## <a name="licenses-and-keys-delivery-service"></a><span data-ttu-id="ee30a-136">라이선스 및 키 배달 서비스</span><span class="sxs-lookup"><span data-stu-id="ee30a-136">Licenses and keys delivery service</span></span>
<span data-ttu-id="ee30a-137">미디어 서비스는 DRM (PlayReady, Widevine, FairPlay) 라이선스 배달용 서비스를 제공 하 고 AES 키 tooauthorized 클라이언트를 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-137">Media Services provides a service for delivering DRM (PlayReady, Widevine, FairPlay) licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="ee30a-138">사용할 수 있습니다 [Azure 포털 hello](media-services-portal-protect-content.md), REST API 또는 Media Services SDK for.NET 라이선스 및 키에 대 한 권한 부여 및 인증 정책 tooconfigure 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-138">You can use [hello Azure portal](media-services-portal-protect-content.md), REST API, or Media Services SDK for .NET tooconfigure authorization and authentication policies for your licenses and keys.</span></span>

## <a name="token-restriction"></a><span data-ttu-id="ee30a-139">토큰 제한</span><span class="sxs-lookup"><span data-stu-id="ee30a-139">Token restriction</span></span>
<span data-ttu-id="ee30a-140">hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열거나 토큰 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-140">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="ee30a-141">보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-141">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="ee30a-142">미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-142">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="ee30a-143">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-143">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="ee30a-144">사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-144">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="ee30a-145">hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-145">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="ee30a-146">hello 미디어 서비스 키 배달 서비스는 hello 요청한 키 (또는 라이선스) toohello 클라이언트 hello 토큰이 유효한 경우 및 hello 반환 hello 토큰 일치 항목에 구성 된 hello 키 (또는 라이선스)에 대 한 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-146">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="ee30a-147">토큰 제한 정책 hello를 구성할 때 hello 기본 확인 키, 발급자 및 대상 매개 변수를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-147">When configuring hello token restricted policy, you must specify hello primary verification key, issuer and audience parameters.</span></span> <span data-ttu-id="ee30a-148">hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-148">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="ee30a-149">hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-149">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="ee30a-150">hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-150">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

## <a name="streaming-urls"></a><span data-ttu-id="ee30a-151">스트리밍 URL</span><span class="sxs-lookup"><span data-stu-id="ee30a-151">Streaming URLs</span></span>
<span data-ttu-id="ee30a-152">Hello 스트리밍 URL에에서는 암호화 태그를 사용 해야 둘 이상의 DRM으로 자산 암호화 된 경우: (형식 ='m3u8-aapl' 암호화 'xxx' =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-152">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="ee30a-153">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-153">hello following considerations apply:</span></span>

* <span data-ttu-id="ee30a-154">1개 이하의 암호화 형식만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-154">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="ee30a-155">암호화 유형 toobe 한 암호화가 적용 된 toohello 자산만 hello url에 지정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-155">Encryption type doesn't have toobe specified in hello url if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="ee30a-156">암호화 형식은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-156">Encryption type is case insensitive.</span></span>
* <span data-ttu-id="ee30a-157">hello 다음 암호화 종류를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-157">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="ee30a-158">**cenc**: 일반 암호화(Playready 또는 Widevine)</span><span class="sxs-lookup"><span data-stu-id="ee30a-158">**cenc**:  Common encryption (Playready or Widevine)</span></span>
  * <span data-ttu-id="ee30a-159">**cbcs-aapl**: Fairplay</span><span class="sxs-lookup"><span data-stu-id="ee30a-159">**cbcs-aapl**: Fairplay</span></span>
  * <span data-ttu-id="ee30a-160">**cbc**: AES 봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="ee30a-160">**cbc**: AES envelope encryption.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="ee30a-161">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="ee30a-161">Common scenarios</span></span>
<span data-ttu-id="ee30a-162">hello 다음 항목에서는 설명 AMS 키/라이선스 배달 서비스를 사용 하 여 저장소의 tooprotect 콘텐츠 스트리밍 미디어를 동적으로 암호화를 제공 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ee30a-162">hello following topics demonstrate how tooprotect content in storage, deliver dynamically encrypted streaming media, use AMS key/license delivery service</span></span>

* [<span data-ttu-id="ee30a-163">AES로 보호</span><span class="sxs-lookup"><span data-stu-id="ee30a-163">Protect with AES</span></span>](media-services-protect-with-aes128.md) 
* [<span data-ttu-id="ee30a-164">PlayReady 및/또는 Widevine으로 보호 </span><span class="sxs-lookup"><span data-stu-id="ee30a-164">Protect with PlayReady and/or Widevine </span></span>](media-services-protect-with-drm.md)
* [<span data-ttu-id="ee30a-165">Apple FairPlay 및/또는 PlayReady로 보호되는 HLS 콘텐츠 스트림</span><span class="sxs-lookup"><span data-stu-id="ee30a-165">Stream your HLS content Protected with Apple FairPlay and/or PlayReady</span></span>](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a><span data-ttu-id="ee30a-166">추가 시나리오</span><span class="sxs-lookup"><span data-stu-id="ee30a-166">Additional scenarios</span></span>
* <span data-ttu-id="ee30a-167">[암호기/스트리밍 서버와 함께 toointegrate Azure PlayReady 라이선스 서비스 어떻게](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-167">[How toointegrate Azure PlayReady License service with your own encryptor/streaming server](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).</span></span>
* [<span data-ttu-id="ee30a-168">CastLabs toodeliver DRM 라이선스 tooAzure 미디어 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ee30a-168">Using castLabs toodeliver DRM licenses tooAzure Media Services</span></span>](media-services-castlabs-integration.md)

>[!NOTE]
><span data-ttu-id="ee30a-169">외부 DRM 서버(기술)를 사용하고 AMS에서 스트리밍하는 시나리오는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-169">A scenario in which you use an external DRM server(technology) and stream from AMS is currently not supported.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ee30a-170">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ee30a-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ee30a-171">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ee30a-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ee30a-172">관련 링크</span><span class="sxs-lookup"><span data-stu-id="ee30a-172">Related Links</span></span>
[<span data-ttu-id="ee30a-173">Azure 미디어 서비스를 사용하여 AES 동적 암호화로 PlayReady 발표</span><span class="sxs-lookup"><span data-stu-id="ee30a-173">Announcing PlayReady as a service and AES dynamic encryption with Azure Media Services</span></span>](http://mingfeiy.com/playready)

[<span data-ttu-id="ee30a-174">Azure 미디어 서비스 PlayReady 라이선스 배달 가격 설명</span><span class="sxs-lookup"><span data-stu-id="ee30a-174">Azure Media Services PlayReady license delivery pricing explained</span></span>](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[<span data-ttu-id="ee30a-175">Aes toodebug Azure 미디어 서비스에서 스트림으로 암호화 하는 방법</span><span class="sxs-lookup"><span data-stu-id="ee30a-175">How toodebug for AES encrypted stream in Azure Media Services</span></span>](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[<span data-ttu-id="ee30a-176">JWT 토큰 인증을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ee30a-176">JWT token authenitcation</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="ee30a-177">[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="ee30a-177">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="ee30a-178">[Azure ACS tooissue 토큰을 사용 하 여](http://mingfeiy.com/acs-with-key-services)합니다.</span><span class="sxs-lookup"><span data-stu-id="ee30a-178">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
