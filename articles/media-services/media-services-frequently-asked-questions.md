---
title: "Azure Media Services 질문과 대답 | Microsoft Docs"
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
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="b40ea-103">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="b40ea-103">Frequently asked questions</span></span>

<span data-ttu-id="b40ea-104">이 문서에서는 AMS(Azure Media Services) 사용자 커뮤니티에 자주 올라오는 질문과 대답을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="b40ea-105">일반 AMS FAQ</span><span class="sxs-lookup"><span data-stu-id="b40ea-105">General AMS FAQs</span></span>
<span data-ttu-id="b40ea-106">Q: 인덱싱을 확장하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="b40ea-107">A: 예약 단위는 인코딩 및 인덱싱 작업에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="b40ea-108">[인코딩 예약 단위 크기를 조정하는 방법](media-services-scale-media-processing-overview.md)의 지침에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="b40ea-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="b40ea-109">**참고** : 인덱서 성능은 예약 단위 유형의 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="b40ea-110">Q: 업로드, 인코딩 및 동영상을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="b40ea-111">스트리밍하려고 할 때 어떤 이유로 비디오가 재생되지 않는 걸까요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="b40ea-112">A: 가장 일반적인 이유 중 하나는 재생하려고 하는 스트리밍 끝점이 **실행 중** 상태가 아니기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="b40ea-113">Q: 라이브 스트림에서 합치기를 수행할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="b40ea-114">A: 라이브 스트림 합치기는 현재 Azure 미디어 서비스에서 제공되지 않으므로, 컴퓨터에 미리 합치기를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="b40ea-115">Q: 라이브 스트리밍으로 Azure CDN을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="b40ea-116">A: Media Services는 Azure CDN와의 통합을 지원합니다. 자세한 내용은 [Media Services 계정에서 스트리밍 끝점을 관리하는 방법](media-services-portal-manage-streaming-endpoints.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b40ea-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="b40ea-117">CDN을 사용하여 라이브 스트리밍을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="b40ea-118">Azure 미디어 서비스는 부드러운 스트리밍, HLS 및 MPEG-DASH 출력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="b40ea-119">이러한 형식에서는 HTTP를 데이터 전송에 사용하여 HTTP 캐싱의 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="b40ea-120">라이브 스트리밍에서 실제 비디오/오디오 데이터가 조각으로 분할되고 이 개별 조각은 CDN에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="b40ea-121">새로 고쳐야 하는 데이터 요구는 매니페스트 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="b40ea-122">CDN은 매니페스트 데이터를 주기적으로 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="b40ea-123">Q: Azure 미디어 서비스는 저장된 이미지를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="b40ea-124">A: JPEG 또는 PNG 이미지를 저장하기 위해 찾으려는 경우 Azure Blob 저장소에 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="b40ea-125">비디오 또는 오디오 자산와 연결된 상태를 유지하려는 경우가 아니면 미디어 서비스 계정에 넣어도 이점은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="b40ea-126">또는 비디오 인코더에서 오버레이로 이미지를 사용해야 하는 경우입니다. 미디어 인코더 표준은 비디오 위에 이미지 겹치기를 지원하며 지원되는 입력 형식으로 JPEG 및 PNG를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="b40ea-127">자세한 내용은 [오버레이 만들기](media-services-advanced-encoding-with-mes.md#overlay)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b40ea-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="b40ea-128">Q: 미디어 서비스 계정 간에 자산을 복사하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="b40ea-129">A: .NET을 사용하여 Media Services 계정 간에 자산을 복사하려면 [Azure Media Services .NET SDK 확장](https://github.com/Azure/azure-sdk-for-media-services-extensions/) 리포지토리에서 제공하는 [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) 확장 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="b40ea-130">자세한 내용은 [이](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) 포럼 스레드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b40ea-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="b40ea-131">Q: AMS에서 작업할 때 파일 이름 지정에 지원되는 문자는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="b40ea-132">A: Media Services에서는 스트리밍 콘텐츠의 URL을 작성할 때 IAssetFile.Name 속성 값을 사용합니다(예: http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters). 이러한 이유로 퍼센트 인코딩은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="b40ea-133">**Name** 속성 값에는 !*'();:@&=+$,/?%#[]"와 같은 [퍼센트 인코딩 예약 문자](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters)를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="b40ea-134">또한 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="b40ea-135">또한 파일 이름 확장명에는 ‘.’ 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-135">for the file name extension.</span></span>

<span data-ttu-id="b40ea-136">Q: REST를 사용하여 연결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="b40ea-137">A: AMS API에 연결하는 방법에 대한 자세한 내용은 [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b40ea-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="b40ea-138">https://media.windows.net에 연결하면 다른 미디어 서비스 URI를 지정하는 301 리디렉션을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b40ea-139">사용자는 새 URI에 대한 후속 호출을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="b40ea-140">Q: 인코딩 프로세스 중에 비디오를 회전하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b40ea-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="b40ea-141">A: [미디어 인코더 표준](media-services-dotnet-encode-with-media-encoder-standard.md) 은 90/180/270도 회전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="b40ea-142">기본 동작은 들어오는 MP4/MOV 파일에서 회전 메타데이터를 검색하여 그에 맞게 보정하는 "Auto"입니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="b40ea-143">다음 **소스** 요소를 [여기](media-services-mes-presets-overview.md)에 정의된 json 사전 설정 중 하나에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b40ea-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="b40ea-144">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b40ea-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b40ea-145">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b40ea-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
