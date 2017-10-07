---
title: "aaaAzure 미디어 서비스 동적 패키징 개요 | Microsoft Docs"
description: "동적 패키징 개요 및 hello 항목 제공 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="215ea-103">동적 패키징</span><span class="sxs-lookup"><span data-stu-id="215ea-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="215ea-104">개요</span><span class="sxs-lookup"><span data-stu-id="215ea-104">Overview</span></span>
<span data-ttu-id="215ea-105">Microsoft Azure 미디어 서비스에 사용 되는 toodeliver 수 많은 미디어 소스 파일 형식, 미디어 스트리밍 형식 및 콘텐츠 보호 형식 tooa 다양 한 클라이언트 기술 (예를 들어 iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="215ea-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="215ea-106">이러한 클라이언트는 여러 가지 프로토콜을 이해합니다. 예를 들어 iOS에는 HLS(HTTP 라이브 스트리밍) V4 형식이 필요하고 Silverlight와 Xbox에는 부드러운 스트리밍이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="215ea-107">적응 비트 전송률 (다중 비트 전송률) 집합이 있으면 MP4 (ISO 기본 미디어 14496-12) 파일 또는 MPEG DASH, HLS 또는 부드러운 스트리밍을 이해 하는 tooserve tooclients 원하는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 사용 해야 미디어의 서비스 동적 패키징입니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="215ea-108">하기만 하면 동적 패키징하 toocreate 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합이 포함 된 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="215ea-109">그런 다음 hello hello 매니페스트에 지정 된 형식에 따라 또는 요청 조각, 주문형 스트리밍 서버 hello 스트림이 선택한 hello 프로토콜에 수신 하는 방법을 사용 하면 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="215ea-110">결과적으로, toostore 하기만 하면 및 단일 저장소 형식 및 미디어 서비스 서비스의 hello 파일에 대 한 급여 빌드하고 클라이언트에서에서 요청에 따라 hello 적절 한 응답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="215ea-111">hello 다음 다이어그램에서는 기존의 인코딩 hello 및 정적 패키징 워크플로</span><span class="sxs-lookup"><span data-stu-id="215ea-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![정적 인코딩](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="215ea-113">hello 다음 다이어그램에서는 hello 동적 패키징 워크플로</span><span class="sxs-lookup"><span data-stu-id="215ea-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![동적 인코딩](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="215ea-115">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="215ea-115">Common scenario</span></span>
1. <span data-ttu-id="215ea-116">입력 파일(mezzanine 파일이라고 함)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="215ea-117">예를 들어 H.264, MP4 또는 WMV (지원 되는 형식의 hello 목록에 대 한 참조 [hello 미디어 인코더 표준에서 형식 지원](media-services-media-encoder-standard-formats.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="215ea-118">사용자 중 2 층 파일 tooH.264 MP4 적응 비트 전송률 집합을으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="215ea-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="215ea-119">Hello 적응 비트 전송률 MP4 세트 hello 주문형 로케이터를 만들어 포함 된 hello 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="215ea-120">스트리밍 Url tooaccess hello 빌드하고 콘텐츠를 스트리밍해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="215ea-121">동적 스트리밍을 위한 자산 준비</span><span class="sxs-lookup"><span data-stu-id="215ea-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="215ea-122">tooprepare 자산의 동적 스트리밍 있습니다에 대 한 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="215ea-123">[마스터 파일을 업로드합니다](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="215ea-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="215ea-124">[Hello 미디어 인코더 표준 인코더 tooproduce H.264 MP4 적응 비트 전송률 세트를 사용 하 여](media-services-dotnet-encode-with-media-encoder-standard.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="215ea-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="215ea-125">[콘텐츠를 스트림합니다](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="215ea-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="215ea-126"><a id="unsupported_formats"></a>동적 패키징에서 지원하지 않는 형식</span><span class="sxs-lookup"><span data-stu-id="215ea-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="215ea-127">hello 다음 원본 파일 형식은 지원 되지 않습니다 동적 패키징에서.</span><span class="sxs-lookup"><span data-stu-id="215ea-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="215ea-128">Dolby Digital mp4 파일</span><span class="sxs-lookup"><span data-stu-id="215ea-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="215ea-129">Dolby Digital 부드러운 파일</span><span class="sxs-lookup"><span data-stu-id="215ea-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="215ea-130">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="215ea-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="215ea-131">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="215ea-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

