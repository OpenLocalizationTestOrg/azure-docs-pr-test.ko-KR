---
title: "Media Services 플랫폼에서 미디어 분석 | Microsoft 문서"
description: "엔터프라이즈 규모, 규정 준수, 보안 및 전 세계 범위의 음성 및 컴퓨터 비전 서비스 컬렉션인 미디어 분석의 공개 미리 보기"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: c0bbe6f80370515fa783b12757434897fe2221b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="12d77-103">Media Services 플랫폼에서 미디어 분석</span><span class="sxs-lookup"><span data-stu-id="12d77-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="12d77-104">개요</span><span class="sxs-lookup"><span data-stu-id="12d77-104">Overview</span></span>
<span data-ttu-id="12d77-105">직원을 교육하고, 고객을 참여시키고, 비즈니스 기능을 문서화하는 기본 미디어로 비디오를 사용하는 조직이 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="12d77-106">클라우드 컴퓨팅은 이러한 대용량 미디어 파일을 저장, 스트림, 액세스하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="12d77-107">하지만 비디오 콘텐츠의 회사 라이브러리가 늘어남에 따라 콘텐츠에서 통찰력을 추출하는 효과적인 방법이 동일하게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="12d77-108">이 증가하는 요구를 해결하기 위해 Azure Media Services는 Azure Media 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="12d77-109">미디어 분석은 조직과 기업이 비디오 파일에서 실질적인 통찰력을 끌어내기 쉽도록 만드는 언어 및 시각 구성 요소 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="12d77-110">핵심 Media Services 플랫폼 구성 요소를 사용하여 구축된 미디어 분석은 대규모 미디어를 하루에 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="12d77-111">개발자는 미디어 분석을 통해 응용 프로그램에 고급 비디오 기능을 신속하게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="12d77-112">대기업에 필요한 전체 규모, 규정 준수, 보안 및 전 세계 범위의 엔터프라이즈 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="12d77-113">다음 다이어그램에서는 미디어 분석 및 Media Services 플랫폼의 다른 주요 부분을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![VoD 워크플로](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="12d77-115">미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="12d77-116">미디어 프로세서가 MP4 파일을 생성한 경우 파일을 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="12d77-117">미디어 프로세서가 JSON 파일을 생성한 경우 Azure Blob Storage에서 해당 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="12d77-118">미디어 분석 서비스</span><span class="sxs-lookup"><span data-stu-id="12d77-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="12d77-119">인덱서</span><span class="sxs-lookup"><span data-stu-id="12d77-119">Indexer</span></span>
<span data-ttu-id="12d77-120">Azure Media Indexer를 사용하면 콘텐츠를 검색할 수 있도록 설정하고 선택 캡션 트랙을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="12d77-121">Azure Media Indexer 2 미리 보기에는 이전 버전에 비해 보다 빠른 인덱싱과 더 광범위한 언어 지원이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="12d77-122">지원되는 언어는 영어, 스페인어, 프랑스어, 독일어, 이탈리아어, 중국어, 포르투갈어, 아랍어 등입니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="12d77-123">자세한 내용 및 예제는 [Azure Media Indexer 2를 사용하여 비디오 처리](media-services-process-content-with-indexer2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="12d77-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="12d77-124">Hyperlapse</span></span>
<span data-ttu-id="12d77-125">Microsoft Hyperlapse는 긴 형식의 콘텐츠에서 빠르고 사용할 수 있는 비디오를 만들도록 비디오 안정화 및 시간 경과 기능을 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="12d77-126">시간 경과 비디오를 만드는 것 외에 Hyperlapse를 사용하여 휴대폰 및 캠코더를 통해 캡처한 흔들리는 비디오에서 안정적인 비디오를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="12d77-127">자세한 내용 및 예제는 [Hyperlapse 미디어 파일 및 Azure Media Hyperlapse](media-services-hyperlapse-content.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="12d77-128">동작 감지기</span><span class="sxs-lookup"><span data-stu-id="12d77-128">Motion Detector</span></span>
<span data-ttu-id="12d77-129">동작 감지기를 사용하여 편지지 배경의 비디오에서 동작을 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="12d77-130">그러면 감시 카메라에서 감지된 동작 이벤트에서의 거짓 긍정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="12d77-131">자세한 내용 및 예제는 [Azure Media 분석에 대한 동작 감지](media-services-motion-detection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="12d77-132">얼굴 감지기</span><span class="sxs-lookup"><span data-stu-id="12d77-132">Face Detector</span></span>
<span data-ttu-id="12d77-133">얼굴 감지기를 사용하여 사람들의 얼굴과 행복, 슬픔, 놀라움 등의 감정을 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="12d77-134">여기에는 이벤트 참여자의 반응을 집계하고 분석하는 등 나중에 설명된 몇 가지 유용한 산업 응용 분야가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="12d77-135">자세한 내용 및 예제는 [Azure Media 분석에 대한 얼굴 및 감정 감지](media-services-face-and-emotion-detection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="12d77-136">비디오 요약</span><span class="sxs-lookup"><span data-stu-id="12d77-136">Video summarization</span></span>
<span data-ttu-id="12d77-137">비디오 요약을 사용하면 원본 비디오에서 흥미로운 조각을 자동으로 선택하여 긴 비디오의 요약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="12d77-138">이 기능은 긴 비디오에서 예상되는 사항에 대한 빠른 개요를 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="12d77-139">자세한 내용 및 예제는 [Azure Media Video Thumbnails를 사용하여 비디오 요약 만들기](media-services-video-summarization.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="12d77-140">광학 문자 인식</span><span class="sxs-lookup"><span data-stu-id="12d77-140">Optical character recognition</span></span>
<span data-ttu-id="12d77-141">Azure Media OCR(광학 문자 인식)을 사용하여 비디오 파일의 텍스트 콘텐츠를 편집 및 검색 가능한 디지털 텍스트로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="12d77-142">그러면 미디어의 비디오 신호에서 의미 있는 메타데이터를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="12d77-143">확장 가능한 얼굴 편집</span><span class="sxs-lookup"><span data-stu-id="12d77-143">Scalable face redaction</span></span>
<span data-ttu-id="12d77-144">Azure Media Redactor는 클라우드에서 확장성 있는 얼굴 편집 기능을 제공하는 Media Analytics 미디어 프로세서입니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="12d77-145">얼굴 편집을 사용하면 선택한 개인의 얼굴을 흐리게 표시하기 위해 동영상을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="12d77-146">뉴스 미디어 또는 공공 안전과 관련된 경우 얼굴 편집 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="12d77-147">짧은 장면이라도 여러 명의 얼굴이 포함된 경우 수동으로 편집하려면 많은 시간이 걸릴 수 있지만 이 서비스를 사용하면 몇 번의 간단한 단계를 통해 얼굴을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="12d77-148">자세한 내용은 [Azure Media 분석으로 얼굴 편집](media-services-face-redaction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="12d77-149">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="12d77-149">Common scenarios</span></span>
<span data-ttu-id="12d77-150">미디어 분석은 조직 및 기업이 비디오에서 새로운 통찰력을 얻고 대용량의 비디오 콘텐츠를 효율적으로 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="12d77-151">다음은 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-151">Here are several scenarios:</span></span>

* <span data-ttu-id="12d77-152">**콜 센터**</span><span class="sxs-lookup"><span data-stu-id="12d77-152">**Call centers**.</span></span> <span data-ttu-id="12d77-153">소셜 미디어의 출현에도 고객 콜 센터는 여전히 고객 서비스 트랜잭션의 많은 부분을 용이하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-153">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="12d77-154">높은 고객 만족도 달성하기 위해 분석될 수 있는 많은 양의 고객 정보가 이 오디오 데이터에서 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-154">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="12d77-155">미디어 인덱서를 사용하여 조직은 텍스트를 추출하고 검색 인덱스와 대시보드를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="12d77-156">그런 다음 일반적인 불만, 불만의 원인 및 기타 관련 데이터 인텔리전스를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="12d77-157">**사용자 생성 콘텐츠 조정**</span><span class="sxs-lookup"><span data-stu-id="12d77-157">**User-generated content moderation**.</span></span> <span data-ttu-id="12d77-158">뉴스 미디어 방송국부터 경찰서까지 많은 조직에는 비디오 및 이미지와 같은 사용자 생성 미디어를 허용하는 공공 포털이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-158">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="12d77-159">예기치 않은 이벤트로 인해 콘텐츠 양이 급증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-159">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="12d77-160">이러한 시나리오에서는 콘텐츠의 적합성을 수동으로 효과적으로 검토하는 것이 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-160">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="12d77-161">고객은 콘텐츠 감수 서비스에 의존하여 적절한 콘텐츠에 중점을 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-161">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="12d77-162">**감시**</span><span class="sxs-lookup"><span data-stu-id="12d77-162">**Surveillance**.</span></span> <span data-ttu-id="12d77-163">IP 카메라 사용이 증가함에 따라 감시 비디오의 인벤토리도 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-163">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="12d77-164">감시 비디오를 수동으로 검토하는 것은 많은 시간이 소요되고 실수가 발생하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-164">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="12d77-165">미디어 분석에서는 파생물을 보다 쉽게 검토, 관리 및 생성할 수 있도록 동작 감지, 얼굴 감지 및 Hyperlapse와 같은 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="12d77-166">미디어 분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="12d77-166">Media Analytics media processors</span></span>
<span data-ttu-id="12d77-167">이 섹션에서는 미디어 분석 미디어 프로세서를 나열하고 .NET 또는 REST를 사용하여 미디어 프로세서(MP) 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-167">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="12d77-168">MP 이름</span><span class="sxs-lookup"><span data-stu-id="12d77-168">MP names</span></span>
* <span data-ttu-id="12d77-169">Azure 미디어 인덱서 2 미리 보기</span><span class="sxs-lookup"><span data-stu-id="12d77-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="12d77-170">Azure 미디어 인덱서</span><span class="sxs-lookup"><span data-stu-id="12d77-170">Azure Media Indexer</span></span>
* <span data-ttu-id="12d77-171">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="12d77-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="12d77-172">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="12d77-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="12d77-173">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="12d77-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="12d77-174">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="12d77-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="12d77-175">Azure 미디어 OCR</span><span class="sxs-lookup"><span data-stu-id="12d77-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="12d77-176">.NET</span><span class="sxs-lookup"><span data-stu-id="12d77-176">.NET</span></span>
<span data-ttu-id="12d77-177">다음 함수는 지정된 MP 이름 중 하나를 사용하고 MP 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-177">The following function takes one of the specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="12d77-178">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="12d77-178">REST</span></span>
<span data-ttu-id="12d77-179">요청:</span><span class="sxs-lookup"><span data-stu-id="12d77-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="12d77-180">응답:</span><span class="sxs-lookup"><span data-stu-id="12d77-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="12d77-181">데모</span><span class="sxs-lookup"><span data-stu-id="12d77-181">Demos</span></span>
<span data-ttu-id="12d77-182">[Azure Media 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12d77-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12d77-183">Next steps</span></span>
<span data-ttu-id="12d77-184">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="12d77-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="12d77-185">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="12d77-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="12d77-186">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="12d77-186">Related articles</span></span>
<span data-ttu-id="12d77-187">[Media Services 분석 알림](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12d77-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
