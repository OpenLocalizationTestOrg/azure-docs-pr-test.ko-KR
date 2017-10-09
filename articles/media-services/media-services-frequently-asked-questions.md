---
title: "aaaAzure 미디어 서비스 질문과 대답 | Microsoft Docs"
description: "FAQ(질문과 대답)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="5a199-103">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="5a199-103">Frequently asked questions</span></span>

<span data-ttu-id="5a199-104">이 문서에서는 질문과 대답 hello Azure 미디어 서비스 (AMS) 사용자 커뮤니티에 의해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="5a199-105">일반 AMS FAQ</span><span class="sxs-lookup"><span data-stu-id="5a199-105">General AMS FAQs</span></span>
<span data-ttu-id="5a199-106">Q: 인덱싱을 확장하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="5a199-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="5a199-107">A: hello 예약 단위는 인코딩 및 인덱싱 작업에 대 한 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="5a199-108">지침에 따라 [어떻게 tooScale 인코딩 예약 단위](media-services-scale-media-processing-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="5a199-109">**참고** : 인덱서 성능은 예약 단위 유형의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="5a199-110">Q: 업로드, 인코딩 및 동영상을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="5a199-111">Hello 이유 hello 비디오 것은 toostream 때 재생 되지 않으면 해당?</span><span class="sxs-lookup"><span data-stu-id="5a199-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="5a199-112">A: hello 가장 일반적으로이 스트리밍 끝점에서 hello tooplayback 하려는 hello 없는 이유 중 하나 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="5a199-113">Q: 라이브 스트림에서 합치기를 수행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="5a199-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="5a199-114">A: 합성 라이브 스트림에는 현재 제공 되지 않습니다 Azure 미디어 서비스에서 toopre 해야 하므로-컴퓨터에 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="5a199-115">Q: 라이브 스트리밍으로 Azure CDN을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="5a199-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="5a199-116">A: 미디어 서비스와 Azure CDN 통합을 지원 (자세한 내용은 참조 [방법을 미디어 서비스 계정에서 tooManage 스트리밍 끝점](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="5a199-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="5a199-117">CDN을 사용하여 라이브 스트리밍을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="5a199-118">Azure 미디어 서비스는 부드러운 스트리밍, HLS 및 MPEG-DASH 출력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="5a199-119">이러한 형식에서는 HTTP를 데이터 전송에 사용하여 HTTP 캐싱의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="5a199-120">라이브 스트리밍 비디오/오디오의 실제 데이터 분할된 toofragments 되며이 개별 조각을 CDN에 캐시 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="5a199-121">새로 고친된 데이터 요구 toobe만는 hello 매니페스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="5a199-122">CDN은 매니페스트 데이터를 주기적으로 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="5a199-123">Q: Azure 미디어 서비스는 저장된 이미지를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="5a199-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="5a199-124">A: toostore JPEG 또는 PNG 이미지 방금 찾으려는 경우 Azure Blob 저장소에 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="5a199-125">비디오 또는 오디오 자산와 연결 된 해당 tookeep 사용 하려는 경우가 아니면 미디어 서비스에서 계정 없는 혜택 tooputting이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="5a199-126">또는 경우 hello 비디오 인코더에 오버레이 필요 toouse hello 이미지를 할 수 있습니다. 미디어 인코더 표준 비디오, 위에 이미지 오버레이 지원 하며 JPEG 및 PNG 지원 나열 작업 하는 형식을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="5a199-127">자세한 내용은 [오버레이 만들기](media-services-advanced-encoding-with-mes.md#overlay)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a199-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="5a199-128">Q: 자산 하나 미디어 서비스 계정 tooanother에서 어떻게 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="5a199-129">A: toocopy 자산.NET을 사용 하 여 한 미디어 서비스 계정 tooanother에서 사용 하 여 [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) hello에서 사용할 수 있는 확장 메서드 [Azure 미디어 서비스.NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="5a199-130">자세한 내용은 [이](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 포럼 스레드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a199-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="5a199-131">Q: hello 지원 되는 문자 AMS 작업할 때 파일 이름 지정</span><span class="sxs-lookup"><span data-stu-id="5a199-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="5a199-132">A: 미디어 서비스 스트리밍 콘텐츠 (예를 들어 http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) hello에 대 한 Url 작성 시 hello IAssetFile.Name 속성의 hello 값을 사용 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="5a199-133">값의 hello hello **이름** 속성 hello 다음 중 하나를 사용할 수 없습니다 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # "입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="5a199-134">또한 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="5a199-135">hello 파일 이름 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-135">for hello file name extension.</span></span>

<span data-ttu-id="5a199-136">Q: 어떻게를 놓으면 tooconnect를 사용 하 여?</span><span class="sxs-lookup"><span data-stu-id="5a199-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="5a199-137">A:에 대 한 내용은 tooconnect toohello AMS API를 확인 하려면 어떻게 해야 [Azure AD 인증 액세스 hello Azure 미디어 서비스 API](media-services-use-aad-auth-to-access-ams-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="5a199-138">Toohttps://media.windows.net을 성공적으로 연결한 후 다른 Media Services URI를 지정 하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5a199-139">후속 호출 toohello 해야 새 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="5a199-140">Q: hello 인코딩 프로세스 동안 비디오를 어떻게 회전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="5a199-141">A: hello [미디어 인코더 표준](media-services-dotnet-encode-with-media-encoder-standard.md) 90/180/270의 회전 각도으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="5a199-142">hello 기본 동작은 "자동", hello 들어오는 MP4/MOV 파일에 toodetect hello 회전 메타 데이터를 시도 하 고 그에 대 한 보정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a199-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="5a199-143">Hello 다음이 포함 **소스** hello json 정의 사전 설정의 요소 tooone [여기](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="5a199-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="5a199-144">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5a199-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5a199-145">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5a199-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
