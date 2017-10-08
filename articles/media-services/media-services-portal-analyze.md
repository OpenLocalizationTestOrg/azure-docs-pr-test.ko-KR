---
title: "aaaAnalyze Azure 포털 hello 사용 하 여 미디어 | Microsoft Docs"
description: "이 항목에서는 방법을 tooprocess 미디어 분석 미디어 프로세서 (Mp)를 사용 하 여 미디어 hello Azure 포털입니다."
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
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="5c4e8-103">Hello Azure 포털을 사용 하 여 미디어를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="5c4e8-104">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5c4e8-105">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="5c4e8-106">개요</span><span class="sxs-lookup"><span data-stu-id="5c4e8-106">Overview</span></span>
<span data-ttu-id="5c4e8-107">Azure 미디어 서비스 분석은 음성 및 비전에서 구성 요소 (엔터프라이즈 규모, 규정 준수, 보안 및 글로벌 서비스)을 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="5c4e8-108">Azure Media Services Analytics에 대한 자세한 개요는 [이](media-services-analytics-overview.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="5c4e8-109">이 항목에서는 방법을 tooprocess 미디어 분석 미디어 프로세서 (Mp)를 사용 하 여 미디어 hello Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="5c4e8-110">미디어 분석 MP는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="5c4e8-111">미디어 프로세서 MP4 파일을 생성 하는 경우에 hello 파일을 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="5c4e8-112">미디어 프로세서는 JSON 파일을 생성 하는 경우에 hello Azure blob 저장소에서에서 hello 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="5c4e8-113">자산 선택 tooanalyze 원하는</span><span class="sxs-lookup"><span data-stu-id="5c4e8-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="5c4e8-114">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5c4e8-115">Hello에 **설정** 창에서 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="5c4e8-116">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-116">.</span></span>
    <span data-ttu-id="5c4e8-117">![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="5c4e8-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="5c4e8-118">원하는 선택 hello 자산 tooanalyze 및 키를 눌러 hello **분석** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="5c4e8-120">Hello에 **미디어 분석 인 미디어 자산 프로세스** 창, 선택 hello 프로세서.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="5c4e8-121">hello 문서의 hello 나머지 부분에서는 근거, 방법에 대해 설명 toouse 각 프로세서.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="5c4e8-122">키를 눌러 **만들기** toohello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="5c4e8-123">Azure 미디어 인덱서</span><span class="sxs-lookup"><span data-stu-id="5c4e8-123">Azure Media Indexer</span></span>
<span data-ttu-id="5c4e8-124">hello **Azure Media Indexer** 미디어 프로세서를 사용 하면 toomake 미디어 파일 및 콘텐츠를 검색할 수, 닫힌된 캡션 트랙을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="5c4e8-125">이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-125">This sections gives some details about options that you can specify for this MP.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="5c4e8-127">언어</span><span class="sxs-lookup"><span data-stu-id="5c4e8-127">Language</span></span>
<span data-ttu-id="5c4e8-128">hello 자연어 toobe hello 멀티미디어 파일에서 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="5c4e8-129">예를 들어 영어 또는 스페인어입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="5c4e8-130">자막</span><span class="sxs-lookup"><span data-stu-id="5c4e8-130">Captions</span></span>
<span data-ttu-id="5c4e8-131">콘텐츠에서 생성할 자막 형식을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="5c4e8-132">한 인덱싱 작업 hello 형식 뒤에 닫힌된 캡션 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="5c4e8-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="5c4e8-133">**SAMI**</span></span>
* <span data-ttu-id="5c4e8-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="5c4e8-134">**TTML**</span></span>
* <span data-ttu-id="5c4e8-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="5c4e8-135">**WebVTT**</span></span>

<span data-ttu-id="5c4e8-136">비디오 파일 청각 장애가 있는 toopeople를 액세스할 수 있으며 이러한 형식의 닫힌된 캡션 (CC) 파일 사용된 toomake 오디오를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="5c4e8-137">AIB 파일</span><span class="sxs-lookup"><span data-stu-id="5c4e8-137">AIB file</span></span>
<span data-ttu-id="5c4e8-138">사용자는 사용 하기 위해 toogenerate hello 오디오 인덱스 Blob 파일 같은 hello 사용자 지정 SQL Server IFilter이이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="5c4e8-139">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="5c4e8-140">키워드</span><span class="sxs-lookup"><span data-stu-id="5c4e8-140">Keywords</span></span>
<span data-ttu-id="5c4e8-141">Toogenerate 키워드 XML 파일을 원하는 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="5c4e8-142">이 파일에는 빈도 및 오프셋된 정보와 함께 hello 음성 콘텐츠에서 추출 된 키워드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="5c4e8-143">작업 이름</span><span class="sxs-lookup"><span data-stu-id="5c4e8-143">Job name</span></span>
<span data-ttu-id="5c4e8-144">Hello 작업을 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="5c4e8-145">[이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5c4e8-146">출력 파일</span><span class="sxs-lookup"><span data-stu-id="5c4e8-146">Output file</span></span>
<span data-ttu-id="5c4e8-147">Hello 출력 콘텐츠를 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="5c4e8-148">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="5c4e8-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="5c4e8-149">Azure Media Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만드는 MP입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="5c4e8-150">자세한 내용은 [이 항목](media-services-hyperlapse-content.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="5c4e8-151">이 섹션에서는 이 MP에 대해 지정할 수 있는 옵션에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-151">This sections gives some details about options that you can specify for this MP.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="5c4e8-153">속도</span><span class="sxs-lookup"><span data-stu-id="5c4e8-153">Speed</span></span>
<span data-ttu-id="5c4e8-154">Hello 입력된 비디오를 어떤 toospeed와 hello 속도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="5c4e8-155">hello 출력은 hello 입력된 비디오의 안정화 및 된 경과 된 시간 변환을입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="5c4e8-156">작업 이름</span><span class="sxs-lookup"><span data-stu-id="5c4e8-156">Job name</span></span>
<span data-ttu-id="5c4e8-157">Hello 작업을 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="5c4e8-158">[이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5c4e8-159">출력 파일</span><span class="sxs-lookup"><span data-stu-id="5c4e8-159">Output file</span></span>
<span data-ttu-id="5c4e8-160">Hello 출력 콘텐츠를 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="5c4e8-161">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="5c4e8-161">Azure Media Face Detector</span></span>
<span data-ttu-id="5c4e8-162">hello **Azure 미디어 얼굴 탐지기** 미디어 프로세서 MP ()를 사용 하면 toocount, 트랙 이동을 계기 청중 참여도 있고 얼굴 식을 통해 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="5c4e8-163">이 서비스는 두 가지 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-163">This service contains two features:</span></span> 

* <span data-ttu-id="5c4e8-164">**얼굴 검색**</span><span class="sxs-lookup"><span data-stu-id="5c4e8-164">**Face detection**</span></span>
  
    <span data-ttu-id="5c4e8-165">얼굴 검색은 동영상 내의 얼굴을 찾아 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="5c4e8-166">여러 글꼴로 검색 하 hello 시간 및 위치 메타 데이터와 JSON 파일에서 반환 된, 이동 하는 동안 이후에 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="5c4e8-167">추적 하는 동안 toogive hello 사용자가 이동 화면의 hello 프레임을 간단 하 게 유지 되거나 방해 하는 경우에 하는 동안에 맞서게 동일한 일관 된 ID toohello 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5c4e8-168">이 서비스는 안면 인식을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="5c4e8-169">Hello 프레임을 벗어나거나에 대 한 방해 되는 사람이 너무 오래 하 게 할 새 ID를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="5c4e8-170">**감정 검색**</span><span class="sxs-lookup"><span data-stu-id="5c4e8-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="5c4e8-171">Emotion 검색은 hello hello 얼굴 감지 만족도, 슬픔, 걱정, 분노를 등의 여러 있지만 특성을 분석을 반환 하는 얼굴 감지 미디어 프로세서의 선택적 구성 요소는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="5c4e8-173">감지 모드</span><span class="sxs-lookup"><span data-stu-id="5c4e8-173">Detection mode</span></span>
<span data-ttu-id="5c4e8-174">Hello 프로세서에 의해 hello 다음 모드 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="5c4e8-175">얼굴 감지</span><span class="sxs-lookup"><span data-stu-id="5c4e8-175">face detection</span></span>
* <span data-ttu-id="5c4e8-176">얼굴별 감정 감지</span><span class="sxs-lookup"><span data-stu-id="5c4e8-176">per face emotion detection</span></span>
* <span data-ttu-id="5c4e8-177">감정 집계 감지</span><span class="sxs-lookup"><span data-stu-id="5c4e8-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="5c4e8-178">작업 이름</span><span class="sxs-lookup"><span data-stu-id="5c4e8-178">Job name</span></span>
<span data-ttu-id="5c4e8-179">Hello 작업을 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="5c4e8-180">[이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5c4e8-181">출력 파일</span><span class="sxs-lookup"><span data-stu-id="5c4e8-181">Output file</span></span>
<span data-ttu-id="5c4e8-182">Hello 출력 콘텐츠를 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="5c4e8-183">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="5c4e8-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="5c4e8-184">hello **Azure 미디어 동작 탐지기** 미디어 프로세서 (MP) 사용 하도록 설정 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="5c4e8-185">동작 감지 동작 발생 hello 비디오의 정적 카메라 장면 tooidentify 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="5c4e8-186">타임 스탬프 및 hello hello 이벤트가 발생 하는 영역 경계와 메타 데이터를 포함 하는 JSON 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="5c4e8-187">이 기술은 보안 비디오 피드를 겨냥 수 toocategorize 동작 관련 이벤트 및 거짓 긍정 그림자 조명 변경 등으로입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="5c4e8-188">이렇게 하면 있습니다 카메라 피드에서 toogenerate 보안 경고 수 tooextract 시간이 매우 긴 거리 내 감시 비디오에서 관심 있는 하면서 무한 관련이 없는 이벤트로 스팸 메일 되지 않고.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="5c4e8-190">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="5c4e8-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="5c4e8-191">이 프로세서를 사용 하면 hello 원본 비디오에서 흥미로운 조각을 자동으로 선택 하 여 긴 비디오의 요약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="5c4e8-192">Tooprovide 비디오에서 어떤 tooexpect의 간략 한 개요를 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="5c4e8-193">자세한 내용 및 예제에 대 한 참조 [Azure 미디어 비디오 축소판 그림 사용 tooCreate 비디오 요약](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="5c4e8-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![비디오 분석](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="5c4e8-195">작업 이름</span><span class="sxs-lookup"><span data-stu-id="5c4e8-195">Job name</span></span>
<span data-ttu-id="5c4e8-196">Hello 작업을 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="5c4e8-197">[이](media-services-portal-check-job-progress.md) 작업의 hello 진행률을 모니터링 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="5c4e8-198">출력 파일</span><span class="sxs-lookup"><span data-stu-id="5c4e8-198">Output file</span></span>
<span data-ttu-id="5c4e8-199">Hello 출력 콘텐츠를 식별할 수 있는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c4e8-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c4e8-200">Next steps</span></span>
<span data-ttu-id="5c4e8-201">Media Services 학습 경로 보기.</span><span class="sxs-lookup"><span data-stu-id="5c4e8-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c4e8-202">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5c4e8-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

