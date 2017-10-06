---
title: "미디어 서비스 REST API를 사용 하 여 aaaConfiguring 자산 배달 정책을 | Microsoft Docs"
description: "이 항목에서는 방법을 미디어 서비스 REST API를 사용 하 여 tooconfigure 다른 자산 배달 정책을 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="fa0d5-103">자산 배달 정책 구성</span><span class="sxs-lookup"><span data-stu-id="fa0d5-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="fa0d5-104">Toodeliver 동적으로 암호화 된 자산을 하려는 경우 단계 중 하나 hello hello 미디어 서비스 콘텐츠 배달 워크플로 자산에 대 한 배달 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="fa0d5-105">hello 자산 배달 정책 미디어 서비스 프로그램 자산 toobe 배달에 대해 원하는 방법을 알려 줍니다: 스트리밍 프로토콜에 자산 패키지 되어야 하며 동적으로 (예: MPEG DASH, HLS, 부드러운 스트리밍 또는 모두), 용 toodynamically 원하는 여부 자산 암호화 및 방법 (봉투 (envelope) 또는 일반 암호화) 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="fa0d5-106">이 항목에서는 근거, 방법 설명 toocreate 고 자산 배달 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="fa0d5-107">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="fa0d5-108">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="fa0d5-109">또한 toobe 수 toouse 동적 패키징 및 동적 암호화 자산인 있어야 적응 비트 전송률 mp4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="fa0d5-110">Toohello 각기 다른 정책을 적용할 수 동일한 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="fa0d5-111">예를 들어 PlayReady 암호화 tooSmooth 스트리밍 및 AES 봉투 (envelope) 암호화 tooMPEG를 적용할 수 있습니다 DASH 및 HLS입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="fa0d5-112">배달 정책에 정의 되어 있지 않은 모든 프로토콜 (예를 들어 추가한만 hello 프로토콜로 HLS를 지정 하는 단일 정책을) 스트리밍에서 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="fa0d5-113">hello 예외 toothis는 없는 자산 배달 정책을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="fa0d5-114">그런 다음 모든 프로토콜이 일반 hello에 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="fa0d5-115">Toodeliver 저장소 암호화 된 자산을 원한다 면 hello 자산의 배달 정책을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="fa0d5-116">자산을 스트리밍하기 전에 hello 서버 제거 hello 저장소 암호화 및 스트림 hello를 사용 하 여 콘텐츠 스트리밍 배달 정책을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="fa0d5-117">예를 들어 toodeliver 자산 암호화 표준 AES (고급) 봉투 (envelope) 암호화 키로 암호화, 너무 hello 정책 형식을 설정**DynamicEnvelopeEncryption**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="fa0d5-118">tooremove 저장소 암호화 및 명확 hello에 스트림 hello 자산 hello 정책 형식을 설정 너무**NoDynamicEncryption**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="fa0d5-119">이러한 정책 형식과 수행 하는 tooconfigure 방법을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="fa0d5-120">Hello 자산 배달 정책을 구성 하는 방법에 따라 것 수 toodynamically 패키지 수, 동적으로 암호화 하 고 스트림 스트리밍 프로토콜을 따르는 hello: 부드러운 스트리밍, HLS, MPEG DASH 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="fa0d5-121">다음 목록에서는 hello hello toostream 부드러운 스트리밍, HLS, 대시를 사용 하는 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="fa0d5-122">부드러운 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-122">Smooth Streaming:</span></span>

<span data-ttu-id="fa0d5-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="fa0d5-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="fa0d5-124">HLS:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-124">HLS:</span></span>

<span data-ttu-id="fa0d5-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="fa0d5-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="fa0d5-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="fa0d5-126">MPEG DASH</span></span>

<span data-ttu-id="fa0d5-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="fa0d5-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="fa0d5-128">Toopublish 자산 및 빌드 스트리밍 URL 참조 하는 방법에 대 한 지침은 [스트리밍 URL을 작성할](media-services-deliver-streaming-content.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="fa0d5-129">고려 사항</span><span class="sxs-lookup"><span data-stu-id="fa0d5-129">Considerations</span></span>
* <span data-ttu-id="fa0d5-130">자산에 대한 주문형(스트리밍) 로케이터가 있는 동안 해당 자산과 연결된 AssetDeliveryPolicy를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="fa0d5-131">hello 권장은 hello 정책 삭제 하기 전에 hello 자산에서 tooremove hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="fa0d5-132">자산 배달 정책이 설정되지 않은 경우 암호화된 저장소 자산에 스트리밍 로케이터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="fa0d5-133">Hello 자산 없는 경우 저장소 암호화,이 hello 시스템은 자산 배달 정책 없이 지우기 hello에 로케이터 및 스트림 hello 자산을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="fa0d5-134">단일 자산과 연결 된 여러 자산 배달 정책을 있는데는 한 가지 방법은 toohandle 주어진된 AssetDeliveryProtocol만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="fa0d5-135">모르기 때문에 hello 시스템 어떤 것에서 오류가 발생 하는 hello AssetDeliveryProtocol.SmoothStreaming 프로토콜을 지정 하는 toolink 두 배달 정책을 시도 하는 경우 의미 원하는 tooapply 때 클라이언트에서 부드러운 스트리밍 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="fa0d5-136">기존 스트리밍 로케이터는 자산 있는 경우 새 정책 toohello 자산을 연결할 수 없습니다, 그리고 기존 정책을 hello 자산에서의 연결을 해제 또는 hello 자산과 연결 된 배달 정책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="fa0d5-137">먼저 tooremove hello 스트리밍 로케이터, hello 정책을 조정 있고 hello 스트리밍 로케이터를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="fa0d5-138">Hello 원본이 나 다운스트림 CDN에서 콘텐츠를 캐시할 수 있으므로 클라이언트에 대 한 문제를 발생 하지 않습니다 스트리밍 로케이터 있지만 hello를 다시 만들 때 동일한 locatorId 확인 해야 하는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="fa0d5-139">미디어 서비스에서 엔터티에 액세스할 때는 HTTP 요청에서 구체적인 헤더 필드와 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="fa0d5-140">자세한 내용은 [미디어 서비스 REST API 개발 설정](media-services-rest-how-to-use.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="fa0d5-141">TooMedia 서비스 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-141">Connect tooMedia Services</span></span>

<span data-ttu-id="fa0d5-142">AMS API를 참조 하는 tooconnect toohello 방법에 대 한 내용은 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="fa0d5-143">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="fa0d5-144">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="fa0d5-145">자산 배달 정책 지우기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="fa0d5-146"><a id="create_asset_delivery_policy"></a>자산 배달 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="fa0d5-147">hello 다음 HTTP 요청을 만듭니다 toonot 동적 암호화를 적용 하 고 프로토콜을 통해 toodeliver hello 스트림 hello 다음 중 하나를 지정 하는 자산 배달 정책: MPEG DASH, HLS 및 부드러운 스트리밍 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="fa0d5-148">Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="fa0d5-149">요청:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="fa0d5-150">응답:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="fa0d5-151"><a id="link_asset_with_asset_delivery_policy"></a>자산을 자산 배달 정책과 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="fa0d5-152">다음 HTTP 요청 링크 hello hello 자산 toohello 자산 배달 정책에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="fa0d5-153">요청:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="fa0d5-154">응답:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="fa0d5-155">DynamicEnvelopeEncryption 자산 배달 정책</span><span class="sxs-lookup"><span data-stu-id="fa0d5-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="fa0d5-156">Hello EnvelopeEncryption 형식의 콘텐츠 키를 만들고 toohello 자산에 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="fa0d5-157">DynamicEnvelopeEncryption 배달 정책을 지정할 때는 toomake 있는지 toolink 자산 tooa 콘텐츠 키의 hello envelopeencryption의 형식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="fa0d5-158">자세한 내용은 [콘텐츠 키 만들기](media-services-rest-create-contentkey.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="fa0d5-159"><a id="get_delivery_url"></a>배달 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="fa0d5-160">Hello에 대 한 get hello 배달 URL hello 이전 단계에서 만든 hello 콘텐츠 키의 배달 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="fa0d5-161">클라이언트가 반환 URL toorequest hello를 사용 하는 AES 키 또는 PlayReady 라이선스 순서 tooplayback hello에 콘텐츠를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="fa0d5-162">Hello hello HTTP 요청 본문에 hello URL tooget hello 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="fa0d5-163">미디어 서비스 PlayReady 라이선스 취득 URL을 요청 PlayReady 사용 하 여 콘텐츠를 보호할 경우 1을 사용 하 여 hello keyDeliveryType에 대 한: {"keyDeliveryType": 1을 (를).</span><span class="sxs-lookup"><span data-stu-id="fa0d5-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="fa0d5-164">Hello 봉투 (envelope) 암호화를 사용 하 여 콘텐츠를 보호 하는 경우 2 keyDeliveryType 지정 하 여 키 획득 URL 요청: {"keyDeliveryType": 2}.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="fa0d5-165">요청:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="fa0d5-166">응답:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="fa0d5-167">자산 배달 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-167">Create asset delivery policy</span></span>
<span data-ttu-id="fa0d5-168">hello 다음 HTTP 요청을 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 봉투 암호화 (**DynamicEnvelopeEncryption**) toohello **HLS**프로토콜 (이 예제에서는 다른 프로토콜은 스트리밍에서 차단).</span><span class="sxs-lookup"><span data-stu-id="fa0d5-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="fa0d5-169">Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="fa0d5-170">요청:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="fa0d5-171">응답:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="fa0d5-172">자산을 자산 배달 정책과 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="fa0d5-173">[자산을 자산 배달 정책과 연결](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="fa0d5-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="fa0d5-174">DynamicCommonEncryption 자산 배달 정책</span><span class="sxs-lookup"><span data-stu-id="fa0d5-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="fa0d5-175">Hello CommonEncryption 형식의 콘텐츠 키를 만들고 toohello 자산에 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="fa0d5-176">DynamicCommonEncryption 배달 정책을 지정할 때는 toomake 있는지 toolink 자산 tooa 콘텐츠 키의 hello CommonEncryption 형식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="fa0d5-177">자세한 내용은 [콘텐츠 키 만들기](media-services-rest-create-contentkey.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="fa0d5-178">배달 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-178">Get Delivery URL</span></span>
<span data-ttu-id="fa0d5-179">Hello 이전 단계에서 만든 hello 콘텐츠 키의 hello PlayReady 배달 방법에 대 한 hello 배달 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="fa0d5-180">클라이언트 hello URL toorequest 순서 tooplayback hello에 PlayReady 라이선스 보호 된 콘텐츠 반환을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="fa0d5-181">자세한 내용은 [배달 URL 가져오기](#get_delivery_url)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="fa0d5-182">자산 배달 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="fa0d5-182">Create asset delivery policy</span></span>
<span data-ttu-id="fa0d5-183">hello 다음 HTTP 요청을 만듭니다 hello **AssetDeliveryPolicy** 즉 구성된 tooapply 동적 일반 암호화 (**DynamicCommonEncryption**) toohello **부드러운 스트리밍**  프로토콜 (이 예제에서는 다른 프로토콜은 스트리밍에서 차단).</span><span class="sxs-lookup"><span data-stu-id="fa0d5-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="fa0d5-184">Hello 참조 하면 값에 대 한 정보는 AssetDeliveryPolicy를 만들 때 지정할 수, [AssetDeliveryPolicy 정의할 때 사용 되는 형식](#types) 섹션.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="fa0d5-185">요청:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="fa0d5-186">Widevine DRM을 사용 하 여 콘텐츠 tooprotect 원하는 hello AssetDeliveryConfiguration 값 toouse WidevineLicenseAcquisitionUrl (들어 있는 hello 값 7)을 업데이트 하 고 라이선스 배달 서비스의 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="fa0d5-187">Widevine 라이선스를 배달 AMS 파트너 toohelp 다음 hello를 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="fa0d5-188">예:</span><span class="sxs-lookup"><span data-stu-id="fa0d5-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="fa0d5-189">Widevine를 암호화 하는 경우 대시를 사용 하 여 수 toodeliver만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="fa0d5-190">있는지 toospecify 대시 (2)에 hello 자산 배달 프로토콜을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="fa0d5-191">자산을 자산 배달 정책과 연결</span><span class="sxs-lookup"><span data-stu-id="fa0d5-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="fa0d5-192">[자산을 자산 배달 정책과 연결](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="fa0d5-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="fa0d5-193"><a id="types"></a>AssetDeliveryPolicy를 정의할 때 사용되는 형식</span><span class="sxs-lookup"><span data-stu-id="fa0d5-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="fa0d5-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="fa0d5-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="fa0d5-195">hello 다음 열거형 값에 설명 hello 자산 배달 프로토콜에 대해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="fa0d5-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="fa0d5-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="fa0d5-197">hello 다음 열거형 값에 설명 hello 자산 배달 정책 형식에 대해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="fa0d5-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="fa0d5-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="fa0d5-199">hello 다음 열거형 값에 설명 hello 콘텐츠 키 toohello 클라이언트의 tooconfigure hello 배달 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="fa0d5-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="fa0d5-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="fa0d5-201">다음 열거형 hello tooconfigure 사용 되는 키 tooget 자산 배달 정책에 대 한 특정 구성을 설정할 수 있는 값을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa0d5-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="fa0d5-202">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="fa0d5-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fa0d5-203">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="fa0d5-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

