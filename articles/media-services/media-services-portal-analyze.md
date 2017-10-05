---
title: "Azure Portal을 사용하여 미디어 분석 | Microsoft 문서"
description: "이 항목에서는 Azure Portal을 사용하여 미디어 분석 미디어 프로세서(MP)로 미디어를 처리하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="654b1-103">Azure Portal을 사용하여 미디어 분석</span><span class="sxs-lookup"><span data-stu-id="654b1-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="654b1-104">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="654b1-105">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b1-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="654b1-106">개요</span><span class="sxs-lookup"><span data-stu-id="654b1-106">Overview</span></span>
<span data-ttu-id="654b1-107">Azure Media Services Analytics는 조직과 기업이 비디오 파일에서 실질적인 통찰력을 끌어내기 쉽도록 만드는 언어 및 시각 구성 요소 모음으로, 미디어 분석을 엔터프라이즈 규모, 규정 준수, 보안 및 전 세계 범위로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="654b1-108">Azure Media Services Analytics에 대한 자세한 개요는 [이](media-services-analytics-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b1-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="654b1-109">이 항목에서는 Azure Portal을 사용하여 미디어 분석 미디어 프로세서(MP)로 미디어를 처리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="654b1-110">미디어 분석 MP는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="654b1-111">미디어 프로세서가 MP4 파일을 생한 경우 파일을 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="654b1-112">미디어 프로세서가 JSON 파일을 생성한 경우 Azure Blob 저장소에서 해당 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="654b1-113">분석하려는 자산을 선택</span><span class="sxs-lookup"><span data-stu-id="654b1-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="654b1-114">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="654b1-115">**설정** 창에서 **자산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="654b1-116">을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b1-116">.</span></span>
    <span data-ttu-id="654b1-117">![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="654b1-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="654b1-118">분석할 자산을 선택하고 **분석** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="654b1-120">**미디어 분석기를 사용하여 미디어 자산 처리** 창에서 프로세서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="654b1-121">문서의 나머지 부분에서는 각 프로세서를 사용하는 이유와 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="654b1-122">**만들기**를 눌러 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="654b1-123">Azure 미디어 인덱서</span><span class="sxs-lookup"><span data-stu-id="654b1-123">Azure Media Indexer</span></span>
<span data-ttu-id="654b1-124">**Azure Media Indexer** 미디어 프로세서를 사용하여 미디어 파일과 콘텐츠를 검색 가능하도록 설정할 수 있으며 선택 캡션 트랙을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="654b1-125">이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-125">This sections gives some details about options that you can specify for this MP.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="654b1-127">언어</span><span class="sxs-lookup"><span data-stu-id="654b1-127">Language</span></span>
<span data-ttu-id="654b1-128">멀티미디어 파일에서 인식되는 자연 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="654b1-129">예를 들어 영어 또는 스페인어입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="654b1-130">자막</span><span class="sxs-lookup"><span data-stu-id="654b1-130">Captions</span></span>
<span data-ttu-id="654b1-131">콘텐츠에서 생성할 자막 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="654b1-132">인덱싱 작업은 다음 형식의 선택 캡션 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="654b1-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="654b1-133">**SAMI**</span></span>
* <span data-ttu-id="654b1-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="654b1-134">**TTML**</span></span>
* <span data-ttu-id="654b1-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="654b1-135">**WebVTT**</span></span>

<span data-ttu-id="654b1-136">이러한 형식의 CC(선택 캡션)는 청각 장애가 있는 사용자가 액세스할 수 있는 오디오 및 비디오 파일을 만드는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="654b1-137">AIB 파일</span><span class="sxs-lookup"><span data-stu-id="654b1-137">AIB file</span></span>
<span data-ttu-id="654b1-138">사용자 지정 SQL Server IFilter에 사용하기 위해 Audio Index Blob 파일을 생성하려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="654b1-139">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b1-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="654b1-140">키워드</span><span class="sxs-lookup"><span data-stu-id="654b1-140">Keywords</span></span>
<span data-ttu-id="654b1-141">키워드 XML 파일을 생성하려는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="654b1-142">이 파일은 빈도 및 오프셋 정보를 포함하며 음성 콘텐츠에서 추출된 키워드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="654b1-143">작업 이름</span><span class="sxs-lookup"><span data-stu-id="654b1-143">Job name</span></span>
<span data-ttu-id="654b1-144">작업을 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="654b1-145">[이](media-services-portal-check-job-progress.md) 문서에서는 작업 진행률을 모니터링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="654b1-146">출력 파일</span><span class="sxs-lookup"><span data-stu-id="654b1-146">Output file</span></span>
<span data-ttu-id="654b1-147">출력 콘텐츠를 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="654b1-148">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="654b1-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="654b1-149">Azure Media Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만드는 MP입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="654b1-150">자세한 내용은 [이 항목](media-services-hyperlapse-content.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654b1-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="654b1-151">이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-151">This sections gives some details about options that you can specify for this MP.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="654b1-153">속도</span><span class="sxs-lookup"><span data-stu-id="654b1-153">Speed</span></span>
<span data-ttu-id="654b1-154">입력 비디오를 가속화할 속도를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="654b1-155">출력은 입력 비디오의 안정화되고 시간 경과된 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="654b1-156">작업 이름</span><span class="sxs-lookup"><span data-stu-id="654b1-156">Job name</span></span>
<span data-ttu-id="654b1-157">작업을 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="654b1-158">[이](media-services-portal-check-job-progress.md) 문서에서는 작업 진행률을 모니터링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="654b1-159">출력 파일</span><span class="sxs-lookup"><span data-stu-id="654b1-159">Output file</span></span>
<span data-ttu-id="654b1-160">출력 콘텐츠를 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="654b1-161">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="654b1-161">Azure Media Face Detector</span></span>
<span data-ttu-id="654b1-162">**Azure 미디어 얼굴 탐지기** MP(미디어 프로세서)를 사용하여 이동 추적, 계산이 가능해지며 표정을 통해 대상 그룹 참여 및 반응 판단도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="654b1-163">이 서비스는 두 가지 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-163">This service contains two features:</span></span> 

* <span data-ttu-id="654b1-164">**얼굴 검색**</span><span class="sxs-lookup"><span data-stu-id="654b1-164">**Face detection**</span></span>
  
    <span data-ttu-id="654b1-165">얼굴 검색은 동영상 내의 얼굴을 찾아 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="654b1-166">여러 얼굴이 검색될 수 있으며 이후 JSON 파일로 반환되는 시간 및 위치 메타데이터를 사용하여 얼굴이 움직일 때마다 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="654b1-167">추적하는 동안 화면에서 사용자가 움직일 때, 가려지거나 프레임에서 잠시 벗어나는 경우에도 동일한 얼굴에 일관된 ID를 지정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="654b1-168">이 서비스는 안면 인식을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="654b1-169">너무 오래 프레임에서 벗어나있거나 가려지는 경우에는 다시 돌아왔을 때 새 ID가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="654b1-170">**감정 검색**</span><span class="sxs-lookup"><span data-stu-id="654b1-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="654b1-171">감정 검색은 검색된 얼굴로부터 행복, 슬픔, 두려움, 분노 등의 여러 감정적 특성에 대한 분석을 반환하는 얼굴 탐지 미디어 프로세서의 선택적 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="654b1-173">감지 모드</span><span class="sxs-lookup"><span data-stu-id="654b1-173">Detection mode</span></span>
<span data-ttu-id="654b1-174">프로세서에 다음 모드 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="654b1-175">얼굴 감지</span><span class="sxs-lookup"><span data-stu-id="654b1-175">face detection</span></span>
* <span data-ttu-id="654b1-176">얼굴별 감정 감지</span><span class="sxs-lookup"><span data-stu-id="654b1-176">per face emotion detection</span></span>
* <span data-ttu-id="654b1-177">감정 집계 감지</span><span class="sxs-lookup"><span data-stu-id="654b1-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="654b1-178">작업 이름</span><span class="sxs-lookup"><span data-stu-id="654b1-178">Job name</span></span>
<span data-ttu-id="654b1-179">작업을 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="654b1-180">[이](media-services-portal-check-job-progress.md) 문서에서는 작업 진행률을 모니터링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="654b1-181">출력 파일</span><span class="sxs-lookup"><span data-stu-id="654b1-181">Output file</span></span>
<span data-ttu-id="654b1-182">출력 콘텐츠를 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="654b1-183">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="654b1-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="654b1-184">**Azure 미디어 동작 탐지기** 의 MP(미디어 프로세서)를 사용하여 길고 특별하지 않은 동영상 중에서 원하는 섹션을 효율적으로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="654b1-185">동작 검색은 고정된 카메라 장면에서 동작이 발생한 동영상 섹션을 식별하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="654b1-186">이벤트가 발생한 경계 영역 및 타임스탬프가 있는 메타데이터를 포함하는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="654b1-187">보안 동영상 피드를 대상으로 하는 이 기술은 동작을 관련 이벤트와 그림자 및 조명 변화와 같은 가양성으로 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="654b1-188">이를 통해 수많은 관련 없는 이벤트로 인해 스팸 처리되지 않고 카메라 피드로부터 보안 경고를 생성할 수 있으며, 아주 긴 감시 동영상으로부터 필요한 순간을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="654b1-190">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="654b1-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="654b1-191">이 프로세서를 사용하면 원본 비디오에서 흥미로운 조각을 자동으로 선택하여 긴 비디오의 요약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="654b1-192">이는 긴 비디오에서 예상되는 사항에 대한 빠른 개요를 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="654b1-193">자세한 내용 및 예제는 [Azure 미디어 비디오 미리 보기를 사용하여 비디오 요약 만들기](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="654b1-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="654b1-195">작업 이름</span><span class="sxs-lookup"><span data-stu-id="654b1-195">Job name</span></span>
<span data-ttu-id="654b1-196">작업을 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="654b1-197">[이](media-services-portal-check-job-progress.md) 문서에서는 작업 진행률을 모니터링하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="654b1-198">출력 파일</span><span class="sxs-lookup"><span data-stu-id="654b1-198">Output file</span></span>
<span data-ttu-id="654b1-199">출력 콘텐츠를 식별할 수 있는 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="654b1-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="654b1-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="654b1-200">Next steps</span></span>
<span data-ttu-id="654b1-201">Media Services 학습 경로 보기.</span><span class="sxs-lookup"><span data-stu-id="654b1-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="654b1-202">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="654b1-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

