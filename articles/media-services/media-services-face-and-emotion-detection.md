---
title: "Azure 미디어 분석으로 얼굴 및 감정 탐지 | Microsoft 문서"
description: "이 토픽에는 Azure Media Analytics로 얼굴 및 감정을 감지하는 방법을 보여 줍니다."
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="f49a3-103">Azure 미디어 분석으로 얼굴 및 감정 검색</span><span class="sxs-lookup"><span data-stu-id="f49a3-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="f49a3-104">개요</span><span class="sxs-lookup"><span data-stu-id="f49a3-104">Overview</span></span>
<span data-ttu-id="f49a3-105">**Azure 미디어 얼굴 탐지기** MP(미디어 프로세서)를 사용하여 이동 추적, 계산이 가능해지며 표정을 통해 대상 그룹 참여 및 반응 판단도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="f49a3-106">이 서비스는 두 가지 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-106">This service contains two features:</span></span> 

* <span data-ttu-id="f49a3-107">**얼굴 검색**</span><span class="sxs-lookup"><span data-stu-id="f49a3-107">**Face detection**</span></span>
  
    <span data-ttu-id="f49a3-108">얼굴 검색은 동영상 내의 얼굴을 찾아 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="f49a3-109">여러 얼굴이 검색될 수 있으며 이후 JSON 파일로 반환되는 시간 및 위치 메타데이터를 사용하여 얼굴이 움직일 때마다 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="f49a3-110">추적하는 동안 화면에서 사용자가 움직일 때, 가려지거나 프레임에서 잠시 벗어나는 경우에도 동일한 얼굴에 일관된 ID를 지정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="f49a3-111">이 서비스는 안면 인식을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="f49a3-112">너무 오래 프레임에서 벗어나있거나 가려지는 경우에는 다시 돌아왔을 때 새 ID가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="f49a3-113">**감정 검색**</span><span class="sxs-lookup"><span data-stu-id="f49a3-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="f49a3-114">감정 검색은 검색된 얼굴로부터 행복, 슬픔, 두려움, 분노 등의 여러 감정적 특성에 대한 분석을 반환하는 얼굴 탐지 미디어 프로세서의 선택적 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="f49a3-115">**Azure 미디어 얼굴 탐지기** MP는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="f49a3-116">이 토픽은 **Azure Media Face Detector** 에 대한 세부 정보 및 .NET용 Media Services SDK와 함께 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="f49a3-117">얼굴 탐지기 입력 파일</span><span class="sxs-lookup"><span data-stu-id="f49a3-117">Face Detector input files</span></span>
<span data-ttu-id="f49a3-118">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-118">Video files.</span></span> <span data-ttu-id="f49a3-119">현재 MP4, MOV 및 WMV 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="f49a3-120">얼굴 탐지기 출력 파일</span><span class="sxs-lookup"><span data-stu-id="f49a3-120">Face Detector output files</span></span>
<span data-ttu-id="f49a3-121">얼굴 검색 및 추적 API는 한 동영상 내에서 최대 64명의 얼굴을 검색할 수 있는 고정밀도 얼굴 위치 검색 및 추적을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="f49a3-122">정면이 최상의 결과를 제공하며 측면 또는 작은 얼굴(24x24 픽셀보다 작거나 같음)의 경우 비교적 정확도가 낮을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="f49a3-123">검색 및 추적된 얼굴은 개별적인 추적을 나타내는 얼굴 ID 번호뿐만 아니라 이미지 내에서 얼굴의 위치를 픽셀 단위로 나타내는 좌표(왼쪽, 위쪽, 너비 및 높이)와 함께 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="f49a3-124">얼굴 ID 번호는 프레임 안에 정면 얼굴이 없거나 겹쳐진 상황에서 재설정될 가능성이 크므로 결과적으로 일부 사용자에게 여러 ID가 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="f49a3-125"><a id="output_elements"></a>출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="f49a3-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="f49a3-126">얼굴 탐지기는 조각화 기술(메타데이터가 시간 기반 청크로 나뉠 수 있으며 필요한 것만 다운로드할 수 있음) 및 분할 기술(이벤트가 너무 커질 경우 분할)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="f49a3-127">몇 가지 간단한 계산으로 데이터를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="f49a3-128">예를 들어 이벤트가 6300(틱)에서 시작하고 날짜 표시줄이 2997(틱/초), 프레임 속도가 29.97(프레임/초)인 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="f49a3-129">시작/날짜 표시줄 = 2.1초</span><span class="sxs-lookup"><span data-stu-id="f49a3-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="f49a3-130">초 x 프레임 속도 = 63개 프레임</span><span class="sxs-lookup"><span data-stu-id="f49a3-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="f49a3-131">얼굴 검색 입력 및 출력 예제</span><span class="sxs-lookup"><span data-stu-id="f49a3-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="f49a3-132">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="f49a3-132">Input video</span></span>
[<span data-ttu-id="f49a3-133">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="f49a3-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="f49a3-134">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="f49a3-134">Task configuration (preset)</span></span>
<span data-ttu-id="f49a3-135">**Azure 미디어 얼굴 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="f49a3-136">다음은 얼굴 검색에 대한 구성 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="f49a3-137">특성 설명</span><span class="sxs-lookup"><span data-stu-id="f49a3-137">Attribute descriptions</span></span>
| <span data-ttu-id="f49a3-138">특성 이름</span><span class="sxs-lookup"><span data-stu-id="f49a3-138">Attribute name</span></span> | <span data-ttu-id="f49a3-139">설명</span><span class="sxs-lookup"><span data-stu-id="f49a3-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f49a3-140">Mode</span><span class="sxs-lookup"><span data-stu-id="f49a3-140">Mode</span></span> |<span data-ttu-id="f49a3-141">빠르게: 처리 속도는 빠르지만 정확도가 떨어집니다(기본값).</span><span class="sxs-lookup"><span data-stu-id="f49a3-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="f49a3-142">JSON 출력</span><span class="sxs-lookup"><span data-stu-id="f49a3-142">JSON output</span></span>
<span data-ttu-id="f49a3-143">다음 JSON 출력 예는 잘린 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="f49a3-144">감정 검색 입력 및 출력 예제</span><span class="sxs-lookup"><span data-stu-id="f49a3-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="f49a3-145">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="f49a3-145">Input video</span></span>
[<span data-ttu-id="f49a3-146">입력 동영상</span><span class="sxs-lookup"><span data-stu-id="f49a3-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="f49a3-147">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="f49a3-147">Task configuration (preset)</span></span>
<span data-ttu-id="f49a3-148">**Azure 미디어 얼굴 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="f49a3-149">다음 구성 기본 설정은 감정 검색을 기반으로 JSON을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="f49a3-150">특성 설명</span><span class="sxs-lookup"><span data-stu-id="f49a3-150">Attribute descriptions</span></span>
| <span data-ttu-id="f49a3-151">특성 이름</span><span class="sxs-lookup"><span data-stu-id="f49a3-151">Attribute name</span></span> | <span data-ttu-id="f49a3-152">설명</span><span class="sxs-lookup"><span data-stu-id="f49a3-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f49a3-153">Mode</span><span class="sxs-lookup"><span data-stu-id="f49a3-153">Mode</span></span> |<span data-ttu-id="f49a3-154">얼굴: 얼굴만 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="f49a3-155">PerFaceEmotion: 각 얼굴 감지에 대해 독립적으로 감정을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="f49a3-156">AggregateEmotion: 프레임의 모든 얼굴에 대한 평균 감정 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="f49a3-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="f49a3-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="f49a3-158">AggregateEmotion 모드가 선택된 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="f49a3-159">각 집계 결과를 생성하는 데 사용되는 동영상의 길이를 밀리초 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="f49a3-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="f49a3-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="f49a3-161">AggregateEmotion 모드가 선택된 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="f49a3-162">집계 결과 생성 빈도를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="f49a3-163">집계 기본값</span><span class="sxs-lookup"><span data-stu-id="f49a3-163">Aggregate defaults</span></span>
<span data-ttu-id="f49a3-164">집계 창 및 간격 설정에는 아래 값이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="f49a3-165">AggregateEmotionWindowMs는 AggregateEmotionIntervalMs보다 길어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="f49a3-166">기본값</span><span class="sxs-lookup"><span data-stu-id="f49a3-166">Defaults(s)</span></span> | <span data-ttu-id="f49a3-167">최소값</span><span class="sxs-lookup"><span data-stu-id="f49a3-167">Min(s)</span></span> | <span data-ttu-id="f49a3-168">최대값</span><span class="sxs-lookup"><span data-stu-id="f49a3-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="f49a3-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="f49a3-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="f49a3-170">0.5</span><span class="sxs-lookup"><span data-stu-id="f49a3-170">0.5</span></span> |<span data-ttu-id="f49a3-171">2</span><span class="sxs-lookup"><span data-stu-id="f49a3-171">2</span></span> |<span data-ttu-id="f49a3-172">0.25</span><span class="sxs-lookup"><span data-stu-id="f49a3-172">0.25</span></span>|
| <span data-ttu-id="f49a3-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="f49a3-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="f49a3-174">0.5</span><span class="sxs-lookup"><span data-stu-id="f49a3-174">0.5</span></span> |<span data-ttu-id="f49a3-175">1</span><span class="sxs-lookup"><span data-stu-id="f49a3-175">1</span></span> |<span data-ttu-id="f49a3-176">0.25</span><span class="sxs-lookup"><span data-stu-id="f49a3-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="f49a3-177">JSON 출력</span><span class="sxs-lookup"><span data-stu-id="f49a3-177">JSON output</span></span>
<span data-ttu-id="f49a3-178">감정 집계에 대한 JSON 출력(잘림)입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="f49a3-179">제한 사항</span><span class="sxs-lookup"><span data-stu-id="f49a3-179">Limitations</span></span>
* <span data-ttu-id="f49a3-180">지원되는 입력 동영상 형식에는 MP4, MOV 및 WMV가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="f49a3-181">검색 가능한 얼굴 크기 범위는 24x24 픽셀에서 2048x2048 픽셀입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="f49a3-182">이 범위를 벗어난 얼굴은 검색되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="f49a3-183">각 동영상에서 반환되는 최대 얼굴 수는 64입니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="f49a3-184">일부 얼굴은 기술적인 문제(예: 매우 큰 얼굴 각도(머리 포즈) 및 큰 폐색)로 인해 검색되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="f49a3-185">정면 및 정면에 가까운 얼굴이 최상의 결과를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="f49a3-186">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="f49a3-186">.NET sample code</span></span>

<span data-ttu-id="f49a3-187">다음 프로그램은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-187">The following program shows how to:</span></span>

1. <span data-ttu-id="f49a3-188">자산을 만들고 미디어 파일을 자산에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="f49a3-189">다음 json 기본 설정을 포함하는 구성 파일을 기반으로 얼굴 감지 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="f49a3-190">출력 JSON 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f49a3-191">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="f49a3-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="f49a3-192">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f49a3-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="f49a3-193">예제</span><span class="sxs-lookup"><span data-stu-id="f49a3-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="f49a3-194">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f49a3-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f49a3-195">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f49a3-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f49a3-196">관련 링크</span><span class="sxs-lookup"><span data-stu-id="f49a3-196">Related links</span></span>
[<span data-ttu-id="f49a3-197">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="f49a3-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f49a3-198">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="f49a3-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

