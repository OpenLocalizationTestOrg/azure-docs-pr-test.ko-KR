---
title: "aaaOverview와 비교에는 azure 미디어 인코더 요청 | Microsoft Docs"
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="c0760-103">Azure 주문형 미디어 인코더 개요 및 비교</span><span class="sxs-lookup"><span data-stu-id="c0760-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="c0760-104">인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="c0760-104">Encoding overview</span></span>
<span data-ttu-id="c0760-105">Azure 미디어 서비스는 hello hello 클라우드에 있는 미디어의 인코딩에 대 한 여러 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="c0760-106">미디어 서비스 시작, 경우에 중요 한 toounderstand hello 차이 코덱 및 파일 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="c0760-107">코덱은 파일 형식은 압축 hello 비디오를 보관 하는 컨테이너는 hello 압축/압축 풀기 알고리즘을 구현 하는 hello 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="c0760-108">미디어 서비스는로 toore 패키지 필요 없이 적응 비트 전송률 MP4 또는 부드러운 스트리밍으로 인코딩 (MPEG DASH, HLS, 부드러운 스트리밍) 미디어 서비스에서 지 원하는 형식 스트리밍을의 콘텐츠 toodeliver 수 있는 동적 패키징을 제공 합니다. 형식 스트리밍을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="c0760-109">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="c0760-110">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="c0760-111">tootake 활용 [동적 패키징](media-services-dynamic-packaging-overview.md), toodo hello 다음 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="c0760-112">또한, 일련의 적응 비트 전송률 MP4 파일 또는 적응 비트 전송률 부드러운 스트리밍 파일 (hello 인코딩 단계는이 자습서의 뒷부분에서 설명)로 소스 파일을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="c0760-113">미디어 서비스는이 문서에서 설명 하는 요청 시 인코더에 hello 다음을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="c0760-114">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="c0760-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="c0760-115">Media Encoder Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="c0760-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="c0760-116">이 문서에 간략하게 설명 필요에 따라 미디어 인코더를 제공 하 고 보다 자세한 정보를 제공 하는 링크 tooarticles를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="c0760-117">또한 hello 항목 hello 인코더의 비교를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="c0760-118">기본적으로 각 미디어 서비스 계정은 한번에 하나의 인코딩 작업을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="c0760-119">구입한 각 인코딩 예약된 단위에 대 한 동시에 실행할 여러 인코딩 작업 toohave를 허용 하는 인코딩 단위를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="c0760-120">자세한 내용은 [인코딩 단위 크기 조정](media-services-scale-media-processing-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0760-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="c0760-121">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="c0760-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="c0760-122">어떻게 toouse</span><span class="sxs-lookup"><span data-stu-id="c0760-122">How toouse</span></span>
[<span data-ttu-id="c0760-123">방식으로 미디어 인코더 표준 tooencode</span><span class="sxs-lookup"><span data-stu-id="c0760-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="c0760-124">형식</span><span class="sxs-lookup"><span data-stu-id="c0760-124">Formats</span></span>
[<span data-ttu-id="c0760-125">형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="c0760-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="c0760-126">기본 설정</span><span class="sxs-lookup"><span data-stu-id="c0760-126">Presets</span></span>
<span data-ttu-id="c0760-127">미디어 인코더 표준 구성 된 설명 hello 인코더 사전 설정 중 하나를 사용 하 여 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="c0760-128">입력 및 출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="c0760-128">Input and output metadata</span></span>
<span data-ttu-id="c0760-129">hello 인코더 입력된 메타 데이터 설명 [여기](media-services-input-metadata-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="c0760-130">hello 인코더 출력 메타 데이터 설명 [여기](media-services-output-metadata-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="c0760-131">미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="c0760-131">Generate thumbnails</span></span>
<span data-ttu-id="c0760-132">정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 toogenerate 축소판 그림](media-services-advanced-encoding-with-mes.md#thumbnails)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="c0760-133">비디오 자르기(클리핑)</span><span class="sxs-lookup"><span data-stu-id="c0760-133">Trim videos (clipping)</span></span>
<span data-ttu-id="c0760-134">정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 tootrim 비디오](media-services-advanced-encoding-with-mes.md#trim_video)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="c0760-135">오버레이 만들기</span><span class="sxs-lookup"><span data-stu-id="c0760-135">Create overlays</span></span>
<span data-ttu-id="c0760-136">정보를 참조 하십시오. [방법을 사용 하 여 미디어 인코더 표준 toocreate 오버레이](media-services-advanced-encoding-with-mes.md#overlay)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="c0760-137">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c0760-137">See also</span></span>
[<span data-ttu-id="c0760-138">hello 미디어 서비스 블로그</span><span class="sxs-lookup"><span data-stu-id="c0760-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="c0760-139">미디어 인코더 Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="c0760-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="c0760-140">개요</span><span class="sxs-lookup"><span data-stu-id="c0760-140">Overview</span></span>
[<span data-ttu-id="c0760-141">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="c0760-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="c0760-142">어떻게 toouse</span><span class="sxs-lookup"><span data-stu-id="c0760-142">How toouse</span></span>
<span data-ttu-id="c0760-143">미디어 인코더 Premium 워크플로는 복잡한 워크플로를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="c0760-144">워크플로 파일을 만들 수 및 hello를 사용 하 여 업데이트할 [워크플로 디자이너](media-services-workflow-designer.md) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="c0760-145">어떻게 tooUse Azure 미디어 서비스에서 프리미엄 인코딩</span><span class="sxs-lookup"><span data-stu-id="c0760-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="c0760-146">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="c0760-146">Known issues</span></span>
<span data-ttu-id="c0760-147">입력된 비디오 닫힌 캡션를 포함 하지 않으면 hello 출력 자산 빈 TTML 파일에 계속 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c0760-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="c0760-148">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="c0760-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c0760-149">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c0760-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="c0760-150">관련 문서</span><span class="sxs-lookup"><span data-stu-id="c0760-150">Related articles</span></span>
* [<span data-ttu-id="c0760-151">미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행</span><span class="sxs-lookup"><span data-stu-id="c0760-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="c0760-152">할당량 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c0760-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
