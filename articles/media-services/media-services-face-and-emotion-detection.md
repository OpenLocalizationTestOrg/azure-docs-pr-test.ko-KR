---
title: "aaaDetect 얼굴 및 Azure 미디어 분석을 Emotion | Microsoft Docs"
description: "이 항목에서는 toodetect 직면 하는 방법 및 감정을 Azure 미디어 분석을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="57180-103">Azure 미디어 분석으로 얼굴 및 감정 검색</span><span class="sxs-lookup"><span data-stu-id="57180-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="57180-104">개요</span><span class="sxs-lookup"><span data-stu-id="57180-104">Overview</span></span>
<span data-ttu-id="57180-105">hello **Azure 미디어 얼굴 탐지기** 미디어 프로세서 MP ()를 사용 하면 toocount, 트랙 이동을 계기 청중 참여도 있고 얼굴 식을 통해 반응 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="57180-106">이 서비스는 두 가지 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-106">This service contains two features:</span></span> 

* <span data-ttu-id="57180-107">**얼굴 검색**</span><span class="sxs-lookup"><span data-stu-id="57180-107">**Face detection**</span></span>
  
    <span data-ttu-id="57180-108">얼굴 검색은 동영상 내의 얼굴을 찾아 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="57180-109">여러 글꼴로 검색 하 hello 시간 및 위치 메타 데이터와 JSON 파일에서 반환 된, 이동 하는 동안 이후에 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="57180-110">추적 하는 동안 toogive hello 사용자가 이동 화면의 hello 프레임을 간단 하 게 유지 되거나 방해 하는 경우에 하는 동안에 맞서게 동일한 일관 된 ID toohello 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="57180-111">이 서비스는 안면 인식을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="57180-112">Hello 프레임을 벗어나거나에 대 한 방해 되는 사람이 너무 오래 하 게 할 새 ID를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="57180-113">**감정 검색**</span><span class="sxs-lookup"><span data-stu-id="57180-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="57180-114">Emotion 검색은 hello hello 얼굴 감지 만족도, 슬픔, 걱정, 분노를 등의 여러 있지만 특성을 분석을 반환 하는 얼굴 감지 미디어 프로세서의 선택적 구성 요소는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="57180-115">hello **Azure 미디어 얼굴 탐지기** MP는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="57180-116">이 항목에 대 한 세부 정보를 제공 **Azure 미디어 얼굴 탐지기** 표시 방법을 toouse Media Services SDK for.NET으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="57180-117">얼굴 탐지기 입력 파일</span><span class="sxs-lookup"><span data-stu-id="57180-117">Face Detector input files</span></span>
<span data-ttu-id="57180-118">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="57180-118">Video files.</span></span> <span data-ttu-id="57180-119">현재 형식에 따라 hello 지원 됩니다: MP4, MOV, 및 WMV입니다.</span><span class="sxs-lookup"><span data-stu-id="57180-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="57180-120">얼굴 탐지기 출력 파일</span><span class="sxs-lookup"><span data-stu-id="57180-120">Face Detector output files</span></span>
<span data-ttu-id="57180-121">hello 얼굴 감지 및 추적 API 고정밀 얼굴 위치 검색 및 비디오에 too64 휴먼 면을 검색할 수 있는 추적을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="57180-122">전면 제공 하는 동안 측면 및 작은 면 hello 최상의 결과 (미만 too24x24 픽셀 같은) 정확한 것으로 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="57180-123">hello 검색 되 고 추적 되 면 반환 되 면 hello 이미지 픽셀에서의 hello 위치를 나타내는 수 있을 뿐만 아니라 글꼴 ID 번호 표시 하는 hello 해당 개인의 추적 된 좌표 (왼쪽, 위쪽, 너비 및 높이).</span><span class="sxs-lookup"><span data-stu-id="57180-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="57180-124">글꼴 ID 번호는 상황에서 발생 하기 쉬운 tooreset hello 전면 손실 되거나 hello 프레임에서 겹쳐진의 결과로 나타나는 일부 사용자를 가져오는 여러 Id를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="57180-125"><a id="output_elements"></a>Hello 출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="57180-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="57180-126">Face 탐지기 (여기서 hello 이벤트 분리 됩니다 너무 커질 경우) 분할 하 고 조각화 (여기서 hello 메타 데이터는 시간 기반 청크로 나눌 수 있습니다 및 필요한 기능만 다운로드할 수 있습니다) 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="57180-127">몇 가지 간단한 계산 hello 데이터를 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="57180-128">예를 들어 이벤트가 6300(틱)에서 시작하고 날짜 표시줄이 2997(틱/초), 프레임 속도가 29.97(프레임/초)인 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="57180-129">시작/날짜 표시줄 = 2.1초</span><span class="sxs-lookup"><span data-stu-id="57180-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="57180-130">초 x 프레임 속도 = 63개 프레임</span><span class="sxs-lookup"><span data-stu-id="57180-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="57180-131">얼굴 검색 입력 및 출력 예제</span><span class="sxs-lookup"><span data-stu-id="57180-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="57180-132">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="57180-132">Input video</span></span>
[<span data-ttu-id="57180-133">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="57180-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="57180-134">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="57180-134">Task configuration (preset)</span></span>
<span data-ttu-id="57180-135">**Azure 미디어 얼굴 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="57180-136">hello 구성 사전 설정에 따라 얼굴 감지 하는 데는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="57180-137">특성 설명</span><span class="sxs-lookup"><span data-stu-id="57180-137">Attribute descriptions</span></span>
| <span data-ttu-id="57180-138">특성 이름</span><span class="sxs-lookup"><span data-stu-id="57180-138">Attribute name</span></span> | <span data-ttu-id="57180-139">설명</span><span class="sxs-lookup"><span data-stu-id="57180-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57180-140">Mode</span><span class="sxs-lookup"><span data-stu-id="57180-140">Mode</span></span> |<span data-ttu-id="57180-141">빠르게: 처리 속도는 빠르지만 정확도가 떨어집니다(기본값).</span><span class="sxs-lookup"><span data-stu-id="57180-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="57180-142">JSON 출력</span><span class="sxs-lookup"><span data-stu-id="57180-142">JSON output</span></span>
<span data-ttu-id="57180-143">다음 예에서는 JSON 출력의 hello가 잘렸습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="57180-144">감정 검색 입력 및 출력 예제</span><span class="sxs-lookup"><span data-stu-id="57180-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="57180-145">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="57180-145">Input video</span></span>
[<span data-ttu-id="57180-146">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="57180-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="57180-147">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="57180-147">Task configuration (preset)</span></span>
<span data-ttu-id="57180-148">**Azure 미디어 얼굴 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="57180-149">다음 구성 사전 설정 hello toocreate hello emotion 검색에 따라 JSON을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="57180-150">특성 설명</span><span class="sxs-lookup"><span data-stu-id="57180-150">Attribute descriptions</span></span>
| <span data-ttu-id="57180-151">특성 이름</span><span class="sxs-lookup"><span data-stu-id="57180-151">Attribute name</span></span> | <span data-ttu-id="57180-152">설명</span><span class="sxs-lookup"><span data-stu-id="57180-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57180-153">Mode</span><span class="sxs-lookup"><span data-stu-id="57180-153">Mode</span></span> |<span data-ttu-id="57180-154">얼굴: 얼굴만 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="57180-155">PerFaceEmotion: 각 얼굴 감지에 대해 독립적으로 감정을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="57180-156">AggregateEmotion: 프레임의 모든 얼굴에 대한 평균 감정 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="57180-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="57180-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="57180-158">AggregateEmotion 모드가 선택된 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="57180-159">밀리초 단위로 사용 되는 비디오 tooproduce의 hello 길이 각 집계 결과 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="57180-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="57180-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="57180-161">AggregateEmotion 모드가 선택된 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="57180-162">어떤 주파수 tooproduce 집계 결과를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="57180-163">집계 기본값</span><span class="sxs-lookup"><span data-stu-id="57180-163">Aggregate defaults</span></span>
<span data-ttu-id="57180-164">아래 hello 집계 창 및 간격 설정에 대 한 값을 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57180-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="57180-165">AggregateEmotionWindowMs는 AggregateEmotionIntervalMs보다 길어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="57180-166">기본값</span><span class="sxs-lookup"><span data-stu-id="57180-166">Defaults(s)</span></span> | <span data-ttu-id="57180-167">최소값</span><span class="sxs-lookup"><span data-stu-id="57180-167">Min(s)</span></span> | <span data-ttu-id="57180-168">최대값</span><span class="sxs-lookup"><span data-stu-id="57180-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="57180-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="57180-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="57180-170">0.5</span><span class="sxs-lookup"><span data-stu-id="57180-170">0.5</span></span> |<span data-ttu-id="57180-171">2</span><span class="sxs-lookup"><span data-stu-id="57180-171">2</span></span> |<span data-ttu-id="57180-172">0.25</span><span class="sxs-lookup"><span data-stu-id="57180-172">0.25</span></span>|
| <span data-ttu-id="57180-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="57180-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="57180-174">0.5</span><span class="sxs-lookup"><span data-stu-id="57180-174">0.5</span></span> |<span data-ttu-id="57180-175">1</span><span class="sxs-lookup"><span data-stu-id="57180-175">1</span></span> |<span data-ttu-id="57180-176">0.25</span><span class="sxs-lookup"><span data-stu-id="57180-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="57180-177">JSON 출력</span><span class="sxs-lookup"><span data-stu-id="57180-177">JSON output</span></span>
<span data-ttu-id="57180-178">감정 집계에 대한 JSON 출력(잘림)입니다.</span><span class="sxs-lookup"><span data-stu-id="57180-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="57180-179">제한 사항</span><span class="sxs-lookup"><span data-stu-id="57180-179">Limitations</span></span>
* <span data-ttu-id="57180-180">입력된 비디오 형식을 지원 hello MP4, MOV, 및 WMV 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57180-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="57180-181">hello를 감지할 수 글꼴 크기 범위는 24 x 24 too2048x2048 픽셀입니다.</span><span class="sxs-lookup"><span data-stu-id="57180-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="57180-182">이 범위를 벗어난 hello 면 문제가 발견 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57180-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="57180-183">각 비디오에 대 한 반환 되 면 hello 최대 개수는 64입니다.</span><span class="sxs-lookup"><span data-stu-id="57180-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="57180-184">일부 면 tootechnical 과제; 인해 검색 되지 않습니다. 예를 들어 매우 큰 글꼴 각도 (h e a d-포즈)와 큰 폐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="57180-185">전면 및 근처 정면 얼굴 hello 최상의 결과 얻으려면 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="57180-186">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="57180-186">.NET sample code</span></span>

<span data-ttu-id="57180-187">hello 다음 프로그램 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="57180-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="57180-188">자산 만들기 hello 자산 미디어 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="57180-189">다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 얼굴 감지 작업과 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57180-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="57180-190">Hello 출력 JSON 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="57180-191">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="57180-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="57180-192">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57180-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="57180-193">예제</span><span class="sxs-lookup"><span data-stu-id="57180-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
            private static readonly string _AADTenantDomain =
                      ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                      ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

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

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="57180-194">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="57180-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="57180-195">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="57180-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="57180-196">관련 링크</span><span class="sxs-lookup"><span data-stu-id="57180-196">Related links</span></span>
[<span data-ttu-id="57180-197">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="57180-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="57180-198">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="57180-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

