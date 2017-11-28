---
title: "hello 미디어 서비스 플랫폼에서 분석 aaaMedia | Microsoft Docs"
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
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="ff359-103">미디어 분석 hello 미디어 서비스 플랫폼에서</span><span class="sxs-lookup"><span data-stu-id="ff359-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="ff359-104">개요</span><span class="sxs-lookup"><span data-stu-id="ff359-104">Overview</span></span>
<span data-ttu-id="ff359-105">많은 조직에서 사용 하는 비디오 선호 중간 tootrain hello 직원, 자신의 고객 및 비즈니스 기능 문서 의견을 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="ff359-106">클라우드 컴퓨팅 방식으로 toostore 제공 스트림, 및 이러한 큰 미디어 파일에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="ff359-107">하지만는 회사의 라이브러리의 비디오 콘텐츠까지 확장 되면서 hello 콘텐츠에서 통찰력을 추출 하는 효과적인 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="ff359-108">tooaddress이 증가 요구 Azure 미디어 서비스는 Azure 미디어 분석을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="ff359-109">미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 및 비전 구성 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="ff359-110">미디어 분석 hello 핵심 미디어 서비스 플랫폼 구성 요소를 사용 하 여 작성, 하루만에 대규모로 처리 하는 미디어를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="ff359-111">개발자는 미디어 분석을 통해 응용 프로그램에 고급 비디오 기능을 신속하게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="ff359-112">Hello 대형, 규정 준수, 보안, 대규모 조직에 필요한 글로벌 서비스와 엔터프라이즈 환경에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="ff359-113">hello 다음 보여 주는 다이어그램 미디어 분석 및 hello 미디어 서비스 플랫폼의 다른 주요 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![VoD 워크플로](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="ff359-115">미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="ff359-116">MP4 파일을 생성 하는 미디어 프로세서를 점진적으로 hello 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="ff359-117">JSON 파일을 생성 하는 미디어 프로세서 하는 경우에 Azure Blob 저장소에서 hello 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="ff359-118">미디어 분석 서비스</span><span class="sxs-lookup"><span data-stu-id="ff359-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="ff359-119">인덱서</span><span class="sxs-lookup"><span data-stu-id="ff359-119">Indexer</span></span>
<span data-ttu-id="ff359-120">Azure Media Indexer를 사용하면 콘텐츠를 검색할 수 있도록 설정하고 선택 캡션 트랙을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="ff359-121">비교 toohello 이전 버전에서는 Azure 미디어 인덱서 2 미리 보기에서 인덱싱 빠르고 보다 광범위 한 언어를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="ff359-122">지원되는 언어는 영어, 스페인어, 프랑스어, 독일어, 이탈리아어, 중국어, 포르투갈어, 아랍어 등입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="ff359-123">자세한 내용 및 예제는 [Azure Media Indexer 2를 사용하여 비디오 처리](media-services-process-content-with-indexer2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="ff359-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="ff359-124">Hyperlapse</span></span>
<span data-ttu-id="ff359-125">Microsoft Hyperlapse 안정화 비디오 및 long 형식의 콘텐츠에서 경과 기능 toocreate 신속 하 고 사용 될 수 있습니다 비디오에 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="ff359-126">경과 비디오를 만드는 것 외에도 Hyperlapse toocreate 안정적인 비디오 휴대 전화 및 캠코더를 통해 캡처된 떨림 비디오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="ff359-127">자세한 내용 및 예제는 [Hyperlapse 미디어 파일 및 Azure Media Hyperlapse](media-services-hyperlapse-content.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="ff359-128">동작 감지기</span><span class="sxs-lookup"><span data-stu-id="ff359-128">Motion Detector</span></span>
<span data-ttu-id="ff359-129">고정 배경이 있는 비디오 동작 탐지기 toodetect 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="ff359-130">따라서 거짓 긍정에 대 한 가능한 toocheck 동작 이벤트에서 감시 카메라 검색에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="ff359-131">자세한 내용 및 예제는 [Azure Media 분석에 대한 동작 감지](media-services-motion-detection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="ff359-132">얼굴 감지기</span><span class="sxs-lookup"><span data-stu-id="ff359-132">Face Detector</span></span>
<span data-ttu-id="ff359-133">얼굴 감지기를 사용하여 사람들의 얼굴과 행복, 슬픔, 놀라움 등의 감정을 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="ff359-134">여기에는 이벤트 참여자의 반응을 집계하고 분석하는 등 나중에 설명된 몇 가지 유용한 산업 응용 분야가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="ff359-135">자세한 내용 및 예제는 [Azure Media 분석에 대한 얼굴 및 감정 감지](media-services-face-and-emotion-detection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="ff359-136">비디오 요약</span><span class="sxs-lookup"><span data-stu-id="ff359-136">Video summarization</span></span>
<span data-ttu-id="ff359-137">비디오 요약을 사용 하면 hello 원본 비디오에서 흥미로운 조각을 자동으로 선택 하 여 긴 비디오의 요약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="ff359-138">이 기능은 tooprovide 비디오에서 어떤 tooexpect의 간략 한 개요를 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="ff359-139">자세한 내용 및 예제에 대 한 참조 [사용 하 여 Azure 미디어 비디오 축소판 toocreate 비디오 요약](media-services-video-summarization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="ff359-140">광학 문자 인식</span><span class="sxs-lookup"><span data-stu-id="ff359-140">Optical character recognition</span></span>
<span data-ttu-id="ff359-141">Azure Media OCR(광학 문자 인식)을 사용하여 비디오 파일의 텍스트 콘텐츠를 편집 및 검색 가능한 디지털 텍스트로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="ff359-142">그런 다음 미디어의 hello 비디오 신호에서 의미 있는 메타 데이터 추출 hello를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="ff359-143">확장 가능한 얼굴 편집</span><span class="sxs-lookup"><span data-stu-id="ff359-143">Scalable face redaction</span></span>
<span data-ttu-id="ff359-144">Azure 미디어 Redactor hello 클라우드에서 확장 가능한 글꼴 교정 제공 하는 미디어 분석 미디어 프로세서입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="ff359-145">Face 교정을 사용 하 여 선택한 개인의 비디오 tooblur 면 프로그램을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="ff359-146">뉴스 미디어 또는 공공 안전 관련 된 경우 toouse hello 얼굴 교정 서비스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="ff359-147">몇 분 정도 장면 여러 글꼴로 포함 하 고 표시 되려면 시간 tooredact 수동으로 마이그레이션하지만이 서비스와 얼굴 교정 몇 가지 간단한 단계만 거치면 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="ff359-148">자세한 내용은 참조 hello [Azure 미디어 분석을 면 교정](media-services-face-redaction.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="ff359-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="ff359-149">일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="ff359-149">Common scenarios</span></span>
<span data-ttu-id="ff359-150">미디어 분석은 조직 및 기업이 비디오에서 새로운 통찰력을 얻고 대용량의 비디오 콘텐츠를 효율적으로 관리하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="ff359-151">다음은 몇 가지 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-151">Here are several scenarios:</span></span>

* <span data-ttu-id="ff359-152">**콜 센터**</span><span class="sxs-lookup"><span data-stu-id="ff359-152">**Call centers**.</span></span> <span data-ttu-id="ff359-153">소셜 미디어, hello 도입 된 경우에 고객의 전화 교환 국 높은 비율의 고객 서비스 트랜잭션이 여전히 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="ff359-154">이 오디오 데이터 인코딩된 tooachieve 고객 만족도 분석 하는 많은 양의 될 수 있는 고객 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="ff359-155">미디어 인덱서를 사용하여 조직은 텍스트를 추출하고 검색 인덱스와 대시보드를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="ff359-156">그런 다음 일반적인 불만, 불만의 원인 및 기타 관련 데이터 인텔리전스를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="ff359-157">**사용자 생성 콘텐츠 조정**</span><span class="sxs-lookup"><span data-stu-id="ff359-157">**User-generated content moderation**.</span></span> <span data-ttu-id="ff359-158">뉴스 미디어 콘센트 toopolice 부서의 많은 조직은 비디오 및 이미지와 같은 미디어 사용자 생성을 허용 하는 공용 웹 포털 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="ff359-159">hello 볼륨이 콘텐츠 toounexpected 이벤트 인해 스파이크 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="ff359-160">이러한 시나리오에서는 것이 어려운 tooconduct 적합성에 대 한 콘텐츠 효과적인 수동 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="ff359-161">해당 되는 콘텐츠에 hello 콘텐츠 중재 서비스 toofocus 고객 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="ff359-162">**감시**</span><span class="sxs-lookup"><span data-stu-id="ff359-162">**Surveillance**.</span></span> <span data-ttu-id="ff359-163">Hello로 사용 하 여 IP 카메라의 증가 거리 내 감시 비디오의 증가 하 고 인벤토리를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="ff359-164">거리 내 감시 비디오를 수동으로 검토 하는 시간이 많이 사용 하 고 발생할 가능성이 toohuman 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="ff359-165">미디어 분석 동작 감지, 얼굴 감지, 검토, 관리 및 파생 항목을 쉽게 만들 Hyperlapse toomake hello 과정 등과 같은 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="ff359-166">미디어 분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="ff359-166">Media Analytics media processors</span></span>
<span data-ttu-id="ff359-167">이 섹션 목록 hello 미디어 분석 미디어 프로세서 및 표시 방법을 toouse.NET 또는 REST tooget 미디어 프로세서 (MP) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="ff359-168">MP 이름</span><span class="sxs-lookup"><span data-stu-id="ff359-168">MP names</span></span>
* <span data-ttu-id="ff359-169">Azure 미디어 인덱서 2 미리 보기</span><span class="sxs-lookup"><span data-stu-id="ff359-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="ff359-170">Azure 미디어 인덱서</span><span class="sxs-lookup"><span data-stu-id="ff359-170">Azure Media Indexer</span></span>
* <span data-ttu-id="ff359-171">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="ff359-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="ff359-172">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="ff359-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="ff359-173">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="ff359-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="ff359-174">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="ff359-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="ff359-175">Azure 미디어 OCR</span><span class="sxs-lookup"><span data-stu-id="ff359-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="ff359-176">.NET</span><span class="sxs-lookup"><span data-stu-id="ff359-176">.NET</span></span>
<span data-ttu-id="ff359-177">hello의 함수 하나 하나를 수행 하는 hello MP 이름을 지정 하 고 MP 개체를 반환을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="ff359-178">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="ff359-178">REST</span></span>
<span data-ttu-id="ff359-179">요청:</span><span class="sxs-lookup"><span data-stu-id="ff359-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="ff359-180">응답:</span><span class="sxs-lookup"><span data-stu-id="ff359-180">Response:</span></span>

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

## <a name="demos"></a><span data-ttu-id="ff359-181">데모</span><span class="sxs-lookup"><span data-stu-id="ff359-181">Demos</span></span>
<span data-ttu-id="ff359-182">[Azure Media 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff359-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff359-183">Next steps</span></span>
<span data-ttu-id="ff359-184">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="ff359-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ff359-185">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ff359-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="ff359-186">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="ff359-186">Related articles</span></span>
<span data-ttu-id="ff359-187">[Media Services 분석 알림](https://azure.microsoft.com/blog/introducing-azure-media-analytics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff359-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
