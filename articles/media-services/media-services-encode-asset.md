---
title: "Azure 주문형 미디어 인코더 개요 및 비교 | Microsoft 문서"
description: "이 항목에서는 Azure 주문형 미디어 인코더를 대략적으로 설명하고 비교한 데이터를 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="14a15-103">Azure 주문형 미디어 인코더 개요 및 비교</span><span class="sxs-lookup"><span data-stu-id="14a15-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="14a15-104">인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="14a15-104">Encoding overview</span></span>
<span data-ttu-id="14a15-105">Azure 미디어 서비스는 클라우드에서 미디어의 인코딩에 대한 여러 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="14a15-106">미디어 서비스로 시작하는 경우 코덱과 파일 형식 간의 차이점을 이해하는 것은 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="14a15-107">코덱은 압축/압축 해제 알고리즘을 구현하는 소프트웨어이고 파일 형식은 압축된 비디오를 보관하는 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="14a15-108">미디어 서비스는 적응 비트 전송률 MP4 또는 부드러운 스트리밍 인코딩 콘텐츠를 미디어 서비스에서 지원되는 스트리밍 형식(MPEG DASH, HLS, 부드러운 스트리밍)으로 다시 패키지하지 않고도 이런 스트리밍 형식으로 배달할 수 있게 하는 동적 패키징을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="14a15-109">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="14a15-110">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 콘텐츠를 스트리밍하려는 스트리밍 끝점은 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="14a15-111">[동적 패키징](media-services-dynamic-packaging-overview.md)을 이용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="14a15-112">또한 원본 파일을 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합으로 인코딩합니다(인코딩 단계는 이 자습서의 뒷부분에서 설명).</span><span class="sxs-lookup"><span data-stu-id="14a15-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="14a15-113">미디어 서비스는 이 문서에서 설명하는 다음 주문형 인코더를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="14a15-114">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="14a15-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="14a15-115">미디어 인코더 Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="14a15-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="14a15-116">이 문서에서는 주문형 미디어 인코더에 대한 간략한 개요와 보다 자세한 정보를 제공하는 문서에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="14a15-117">또한 항목에서는 인코더에 대한 비교를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="14a15-118">기본적으로 각 미디어 서비스 계정은 한번에 하나의 인코딩 작업을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="14a15-119">구입한 각 인코딩 예약 단위에 대해 하나씩, 여러 인코딩 작업을 동시에 실행할 수 있는 인코딩 단위를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="14a15-120">자세한 내용은 [인코딩 단위 크기 조정](media-services-scale-media-processing-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a15-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="14a15-121">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="14a15-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="14a15-122">사용 방법</span><span class="sxs-lookup"><span data-stu-id="14a15-122">How to use</span></span>
[<span data-ttu-id="14a15-123">미디어 인코더 표준으로 인코딩하는 방법</span><span class="sxs-lookup"><span data-stu-id="14a15-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="14a15-124">형식</span><span class="sxs-lookup"><span data-stu-id="14a15-124">Formats</span></span>
[<span data-ttu-id="14a15-125">형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="14a15-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="14a15-126">기본 설정</span><span class="sxs-lookup"><span data-stu-id="14a15-126">Presets</span></span>
<span data-ttu-id="14a15-127">미디어 인코더 표준은 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)에서 설명한 인코더 기본 설정 중 하나를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="14a15-128">입력 및 출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="14a15-128">Input and output metadata</span></span>
<span data-ttu-id="14a15-129">인코더 입력 메타데이터는 [여기](media-services-input-metadata-schema.md)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="14a15-130">인코더 출력 메타데이터는 [여기](media-services-output-metadata-schema.md)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="14a15-131">미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="14a15-131">Generate thumbnails</span></span>
<span data-ttu-id="14a15-132">자세한 내용은 [미디어 인코더 표준을 사용하여 미리 보기를 생성하는 방법](media-services-advanced-encoding-with-mes.md#thumbnails)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a15-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="14a15-133">비디오 자르기(클리핑)</span><span class="sxs-lookup"><span data-stu-id="14a15-133">Trim videos (clipping)</span></span>
<span data-ttu-id="14a15-134">자세한 내용은 [미디어 인코더 표준을 사용하여 비디오를 자르는 방법](media-services-advanced-encoding-with-mes.md#trim_video)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a15-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="14a15-135">오버레이 만들기</span><span class="sxs-lookup"><span data-stu-id="14a15-135">Create overlays</span></span>
<span data-ttu-id="14a15-136">자세한 내용은 [미디어 인코더 표준을 사용하여 오버레이를 만드는 방법](media-services-advanced-encoding-with-mes.md#overlay)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14a15-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="14a15-137">참고 항목</span><span class="sxs-lookup"><span data-stu-id="14a15-137">See also</span></span>
[<span data-ttu-id="14a15-138">미디어 서비스 블로그</span><span class="sxs-lookup"><span data-stu-id="14a15-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="14a15-139">미디어 인코더 Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="14a15-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="14a15-140">개요</span><span class="sxs-lookup"><span data-stu-id="14a15-140">Overview</span></span>
[<span data-ttu-id="14a15-141">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="14a15-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="14a15-142">사용 방법</span><span class="sxs-lookup"><span data-stu-id="14a15-142">How to use</span></span>
<span data-ttu-id="14a15-143">미디어 인코더 Premium 워크플로는 복잡한 워크플로를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="14a15-144">워크플로 파일은 [Workflow Designer](media-services-workflow-designer.md) 도구를 사용하여 만들고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="14a15-145">Azure 미디어 서비스의 프리미엄 인코딩 사용 방법</span><span class="sxs-lookup"><span data-stu-id="14a15-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="14a15-146">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="14a15-146">Known issues</span></span>
<span data-ttu-id="14a15-147">입력된 비디오에 자막이 없는 경우, 출력 자산은 빈 TTML 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="14a15-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="14a15-148">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="14a15-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="14a15-149">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="14a15-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="14a15-150">관련 문서</span><span class="sxs-lookup"><span data-stu-id="14a15-150">Related articles</span></span>
* [<span data-ttu-id="14a15-151">미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행</span><span class="sxs-lookup"><span data-stu-id="14a15-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="14a15-152">할당량 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="14a15-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
