---
title: "Media Encoder Standard로 비디오를 자르는 방법 - Azure | Microsoft Docs"
description: "이 문서에서는 미디어 인코더 표준으로 비디오를 자르는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="c2693-103">미디어 인코더 표준으로 비디오 자르기</span><span class="sxs-lookup"><span data-stu-id="c2693-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="c2693-104">미디어 인코더 표준(MES)을 사용하여 입력 비디오를 자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="c2693-105">자르기는 비디오 프레임 내에서 사각형 창을 선택하는 과정이며 해당 창 내의 픽셀을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="c2693-106">다음 다이어그램은 프로세스를 설명하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-106">The following diagram helps illustrate the process.</span></span>

![비디오 자르기](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="c2693-108">해상도가 1920x1080픽셀(16:9 가로 세로 비율)인 비디오를 입력으로 포함하고 왼쪽 및 오른쪽에 검은색 막대가 있다고 가정하면 4:3 창 또는 1440x1080픽셀만 실제 비디오를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="c2693-109">MES를 사용하여 검은색 막대를 자르거나 편집하고 1440x1080 영역을 인코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="c2693-110">MES에서 자르기는 전처리 단계이므로 인코딩 사전 설정의 자르기 매개 변수를 원래 입력 비디오에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="c2693-111">Encoding은 후속 단계이며 너비/높이 설정은 원본 비디오가 아닌 *전처리된* 비디오에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="c2693-112">사전 설정을 지정할 경우 다음을 수행해야 합니다. (a) 원본 입력 비디오를 기반으로 자르기 매개 변수를 선택하고 (b) 자른 비디오를 기반으로 인코딩 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="c2693-113">인코딩 설정이 자른 비디오와 일치하지 않는 경우 예상한 대로 출력되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="c2693-114">[다음](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) 토픽은 MES로 인코딩 작업을 만드는 방법과 인코딩 작업에 대한 사용자 지정 사전 설정을 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="c2693-115">사용자 지정 사전 설정 만들기</span><span class="sxs-lookup"><span data-stu-id="c2693-115">Creating a custom preset</span></span>
<span data-ttu-id="c2693-116">다이어그램에 표시된 예:</span><span class="sxs-lookup"><span data-stu-id="c2693-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="c2693-117">원본 입력은 1920x1080입니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="c2693-118">입력 프레임의 가운데에 있는 1440x1080의 출력으로 잘라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="c2693-119">즉, X 오프셋은 (1920 – 1440)/2 = 240이고 Y 오프셋은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="c2693-120">자르기 사각형의 너비 및 높이는 각각 1440 및 1080입니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="c2693-121">인코딩 단계에서 해상도가 각각 1440x1080, 960x720 및 480x360인 세 계층을 생성할지를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="c2693-122">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="c2693-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


## <a name="restrictions-on-cropping"></a><span data-ttu-id="c2693-123">자르기에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c2693-123">Restrictions on cropping</span></span>
<span data-ttu-id="c2693-124">자르기 기능은 수동입니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="c2693-125">관심 있는 프레임을 선택할 수 있는 적당한 편집 도구로 입력 비디오를 로드하고 커서 위치를 지정하여 자르기 사각형의 오프셋을 결정한 후 특정 비디오 등에 맞게 조정된 인코딩 사전 설정을 결정해야 합니다. 이 기능은 입력 비디오에서 자동 검색 및 검은색 레터박스/필러박스 테두리의 제거와 같은 기능을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="c2693-126">자르기 기능에는 다음과 같은 제약 조건이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="c2693-127">이러한 제약 조건이 충족되지 않으면 인코딩 작업이 실패하거나 예기치 않은 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="c2693-128">자르기 사각형의 좌표 및 크기가 입력 비디오 내에 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="c2693-129">위에서 설명했듯이 인코딩 설정의 너비 및 높이는 자른 비디오와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="c2693-130">자르기는 가로 모드에서 캡처된 비디오에 적용됩니다(즉, 세로로 또는 인물 모드로 스마트폰을 잡고 기록한 비디오에는 적용되지 않음).</span><span class="sxs-lookup"><span data-stu-id="c2693-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="c2693-131">정사각형 픽셀로 캡처된 프로그레시브 비디오에서 가장 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c2693-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="c2693-132">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c2693-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="c2693-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2693-133">Next step</span></span>
<span data-ttu-id="c2693-134">AMS에서 제공하는 훌륭한 기능에 대해 자세히 알아보려면 Azure 미디어 서비스 학습 경로를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c2693-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
