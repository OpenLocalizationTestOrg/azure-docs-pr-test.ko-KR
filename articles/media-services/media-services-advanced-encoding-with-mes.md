---
title: "MES 사전 설정을 사용자 지정하여 고급 인코딩 수행 | Microsoft Docs"
description: "이 항목에서는 미디어 인코더 표준 태스크 사전 설정을 사용자 지정하여 고급 인코딩을 수행하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 8de3bdd45261c84a0e1bb90f1c58863ad740dd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="8cdc7-103">MES 사전 설정을 사용자 지정하여 고급 인코딩 수행</span><span class="sxs-lookup"><span data-stu-id="8cdc7-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="8cdc7-104">개요</span><span class="sxs-lookup"><span data-stu-id="8cdc7-104">Overview</span></span>

<span data-ttu-id="8cdc7-105">이 항목에서는 MES(Media Encoder Standard) 사전 설정을 사용자 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-105">This topic shows how to customize Media Encoder Standard presets.</span></span> <span data-ttu-id="8cdc7-106">[사전 설정을 사용자 지정하는 MES를 사용한 인코딩](media-services-custom-mes-presets-with-dotnet.md) 항목에서는 .NET을 사용하여 인코딩 태스크와 이 태스크를 실행하는 작업을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span></span> <span data-ttu-id="8cdc7-107">사전 설정을 사용자 지정한 후에는 이 사용자 지정 사전 설정을 인코딩 작업에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-107">Once you customize a preset, supply the custom presets to the encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="8cdc7-108">XML 사전 설정을 사용하는 경우 아래 XML 예제에 표시된 것처럼 요소 순서를 유지해야 합니다(예를 들어, KeyFrameInterval은 SceneChangeDetection 앞에 와야 함).</span><span class="sxs-lookup"><span data-stu-id="8cdc7-108">If using an XML preset, make sure to preserve the order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="8cdc7-109">이 항목에서는 다음 인코딩 태스크를 수행하는 사용자 지정 사전 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-109">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="8cdc7-110">상대적 크기에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="8cdc7-110">Support for relative sizes</span></span>

<span data-ttu-id="8cdc7-111">미리 보기를 생성하는 경우 출력 너비와 높이를 픽셀 단위로 반드시 지정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-111">When generating thumbnails, you do not need to always specify output width and height in pixels.</span></span> <span data-ttu-id="8cdc7-112">[1%, …, 100%] 범위에서 백분율로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-112">You can specify them in percentages, in the range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="8cdc7-113">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="8cdc7-114">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="8cdc7-115"><a id="thumbnails"></a>미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="8cdc7-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="8cdc7-116">이 섹션에서는 미리 보기를 생성하는 기본 설정을 사용자 지정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-116">This section shows how to customize a preset that generates thumbnails.</span></span> <span data-ttu-id="8cdc7-117">아래에 정의된 사전 설정은 미리 보기를 생성하는 데 필요한 정보 뿐만 아니라 파일을 인코딩하는 방법에 대한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-117">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="8cdc7-118">[이 섹션](media-services-mes-presets-overview.md)에 문서화된 MES 사전 설정 중 하나를 가져와서 미리 보기를 생성하는 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-118">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="8cdc7-119">다음 기본 설정에서 **SceneChangeDetection** 설정은 단일 비트 전송률 비디오로 Encoding하는 경우에만 true로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-119">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span></span> <span data-ttu-id="8cdc7-120">다중 비트 전송률 비디오로 인코딩하고 **SceneChangeDetection** 을 true로 설정하면 인코더에서 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-120">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span></span>  
>
>

<span data-ttu-id="8cdc7-121">스키마에 대한 자세한 내용은 [이 항목](media-services-mes-schema.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="8cdc7-122">[고려 사항](#considerations) 섹션을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-122">Make sure to review the [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="8cdc7-123"><a id="json"></a>JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="8cdc7-124"><a id="xml"></a>XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="8cdc7-125">고려 사항</span><span class="sxs-lookup"><span data-stu-id="8cdc7-125">Considerations</span></span>

<span data-ttu-id="8cdc7-126">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-126">The following considerations apply:</span></span>

* <span data-ttu-id="8cdc7-127">시작/단계/범위에 대한 명시적 타임스탬프 사용 시 입력 소스의 길이가 1분 이상이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-127">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="8cdc7-128">Jpg/Png/BmpImage 요소에는 Start, Step 및 Range 문자열 특성이 있으며, 이러한 특성은 다음과 같이 해석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="8cdc7-129">음수가 아닌 정수인 경우 프레임 번호(예: "Start": "120")</span><span class="sxs-lookup"><span data-stu-id="8cdc7-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="8cdc7-130">% 접미사로 표시된 경우 소스 기간 기준(예: "Start": "15%")</span><span class="sxs-lookup"><span data-stu-id="8cdc7-130">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="8cdc7-131">HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="8cdc7-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="8cdc7-132">형식으로 표현되는 경우 타임스탬프(예: "Start" : "00:01:00")</span><span class="sxs-lookup"><span data-stu-id="8cdc7-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="8cdc7-133">표기법을 원하는 대로 혼용하거나 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="8cdc7-134">또한 Start는 콘텐츠의 첫 번째 "흥미로운" 프레임의 결정을 시도하는 특수 Macro:{Best}를 지원합니다. 참고: (Step 및 Range는 Start를 {Best}로 설정하면 무시됨)</span><span class="sxs-lookup"><span data-stu-id="8cdc7-134">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="8cdc7-135">기본값: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="8cdc7-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="8cdc7-136">각 이미지 형식에 대해 출력 형식을 명시적으로 제공해야 합니다. Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-136">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="8cdc7-137">출력 형식이 있는 경우 MES는 JpgVideo를 JpgFormat에 일치시키는 식으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-137">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="8cdc7-138">OutputFormat은 새 이미지 코덱 특유의 Macro: {Index}를 도입하며, 이는 이미지 출력 형식에 대해 존재해야(한 번만) 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="8cdc7-139"><a id="trim_video"></a>비디오 자르기(클리핑)</span><span class="sxs-lookup"><span data-stu-id="8cdc7-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="8cdc7-140">이 섹션에서는 입력이 소위 중 2층 파일이나 주문형 파일인 경우 입력 비디오를 클립하거나 자르는 인코더 사전 설정을 수정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-140">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="8cdc7-141">인코더는 라이브 스트림에서 캡처되거나 보관된 자산을 클립하거나 자르는 데 사용할 수도 있습니다. 이에 대한 세부 정보는 [이 블로그](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-141">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="8cdc7-142">비디오를 자르려면 [이 섹션](media-services-mes-presets-overview.md)에 문서화된 MES 사전 설정 중 하나를 수행하고 **Sources** 요소를 아래와 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-142">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span></span> <span data-ttu-id="8cdc7-143">StartTime 값이 입력 비디오의 절대 타임스탬프와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-143">The value of StartTime needs to match the absolute timestamps of the input video.</span></span> <span data-ttu-id="8cdc7-144">예를 들어 입력 비디오의 첫 번째 프레임에 12:00:10.000 타임스탬프가 있으면 StartTime은 12:00:10.000 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-144">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="8cdc7-145">아래 예에서는 입력 비디오의 시작 타임스탬프가 0인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-145">In the example below, we assume that the input video has a starting timestamp of zero.</span></span> <span data-ttu-id="8cdc7-146">**Sources** 는 사전 설정의 맨 앞에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-146">**Sources** should be placed at the beginning of the preset.</span></span>

### <span data-ttu-id="8cdc7-147"><a id="json"></a>JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
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
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a><span data-ttu-id="8cdc7-148">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-148">XML preset</span></span>
<span data-ttu-id="8cdc7-149">비디오를 자르려면 [여기](media-services-mes-presets-overview.md) 에서 문서화된 MES 사전 설정 중 하나를 수행하고 **원본** 요소를 아래와 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-149">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="8cdc7-150"><a id="overlay"></a>오버레이 만들기</span><span class="sxs-lookup"><span data-stu-id="8cdc7-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="8cdc7-151">미디어 인코더 표준을 사용하면 이미지를 기존 비디오에 오버레이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-151">The Media Encoder Standard allows you to overlay an image onto an existing video.</span></span> <span data-ttu-id="8cdc7-152">현재 png, jpg, gif 및 bmp 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-152">Currently, the following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="8cdc7-153">아래에 정의된 사전 설정은 비디오 오버레이의 기본적인 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-153">The preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="8cdc7-154">또한 사전 설정 파일을 정의하는 것 외에도 미디어 서비스를 통해 오버레이 이미지에 해당하는 자산의 파일 및 이미지를 오버레이하려는 원본 비디오에 해당하는 파일을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-154">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span></span> <span data-ttu-id="8cdc7-155">비디오 파일은 **기본** 파일이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-155">The video file has to be the **primary** file.</span></span>

<span data-ttu-id="8cdc7-156">.NET을 사용하는 경우 [이 항목](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet)에 정의된 .NET 예제에 다음 두 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-156">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="8cdc7-157">**UploadMediaFilesFromFolder** 함수는 폴더에서 파일(예: BigBuckBunny.mp4 및 Image001.png)을 업로드하고 mp4 파일을 자산의 기본 파일로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-157">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span></span> <span data-ttu-id="8cdc7-158">**EncodeWithOverlay** 함수는 전달된 사용자 지정 사전 설정 파일(예: 다음에 나오는 사전 설정)을 사용하여 인코딩 태스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-158">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // The following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input assets to be encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset to contain the results of the job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="8cdc7-159">현재 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="8cdc7-159">Current limitations:</span></span>
>
> <span data-ttu-id="8cdc7-160">오버레이 불투명도 설정이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-160">The overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="8cdc7-161">원본 비디오 파일과 오버레이 이미지 파일은 같은 자산에 있어야 하며 이 자산에서 비디오 파일을 기본 파일로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-161">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="8cdc7-162">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
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
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="8cdc7-163">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="8cdc7-164"><a id="silent_audio"></a>입력에 오디오가 없을 때 조용한 오디오 트랙 삽입</span><span class="sxs-lookup"><span data-stu-id="8cdc7-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="8cdc7-165">기본적으로 비디오만 포함하며 오디오는 없는 입력을 인코더로 보내면 출력 자산에는 비디오 데이터만 들어 있는 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-165">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span></span> <span data-ttu-id="8cdc7-166">일부 플레이어는 해당 출력 스트림을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-166">Some players may not be able to handle such output streams.</span></span> <span data-ttu-id="8cdc7-167">이 시나리오에서는 이 설정을 사용하여 출력에 조용한 오디오 트랙을 추가하는 인코더를 강제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-167">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span></span>

<span data-ttu-id="8cdc7-168">입력에 오디오가 없을 때 조용한 오디오 트랙을 포함하는 자산을 생성하도록 인코더를 적용하려면 "InsertSilenceIfNoAudio" 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-168">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="8cdc7-169">[이 섹션](media-services-mes-presets-overview.md)에 문서화된 MES 사전 설정 중 하나를 가져온 후에 다음과 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-169">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="8cdc7-170">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="8cdc7-171">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="8cdc7-172"><a id="deinterlacing"></a>자동 디인터레이스 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="8cdc7-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="8cdc7-173">인터레이스 콘텐츠가 자동으로 디인터레이스되도록 원하는 고객은 아무 작업도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-173">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span></span> <span data-ttu-id="8cdc7-174">자동 디인터레이스가 설정(기본값)된 경우 MES에서는 인터레이스 프레임 및 인터레이스로 표시된 디인터레이스 프레임만 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-174">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="8cdc7-175">자동 디인터레이스를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-175">You can turn the auto de-interlacing off.</span></span> <span data-ttu-id="8cdc7-176">이 옵션은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="8cdc7-177">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="8cdc7-178">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="8cdc7-179"><a id="audio_only"></a>오디오 전용 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="8cdc7-180">이 섹션에서는 AAC 오디오 및 AAC 고급 품질 오디오라는 두 개의 오디오 전용 MES 사전 설정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="8cdc7-181">AAC 오디오</span><span class="sxs-lookup"><span data-stu-id="8cdc7-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="8cdc7-182">AAC 고급 음질 오디오</span><span class="sxs-lookup"><span data-stu-id="8cdc7-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="8cdc7-183"><a id="concatenate"></a>둘 이상의 비디오 파일 연결</span><span class="sxs-lookup"><span data-stu-id="8cdc7-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="8cdc7-184">다음 예제에서는 사전 설정을 생성하여 둘 이상의 비디오 파일을 연결하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-184">The following example illustrates how you can generate a preset to concatenate two or more video files.</span></span> <span data-ttu-id="8cdc7-185">가장 일반적인 시나리오는 기본 비디오에 헤더나 트레일러를 추가하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-185">The most common scenario is when you want to add a header or a trailer to the main video.</span></span> <span data-ttu-id="8cdc7-186">편집 중인 비디오 파일이 속성(비디오 해상도, 프레임 속도, 오디오 트랙 수 등)을 공유하는 경우에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-186">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="8cdc7-187">프레임 속도나 오디오 트랙 수가 서로 다른 비디오를 섞지 않게 주의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-187">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="8cdc7-188">연결 기능의 현재 설계에서는 입력된 비디오 클립이 해상도, 프레임 속도 측면에서 일관적이라고 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-188">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="8cdc7-189">요구 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="8cdc7-189">Requirements and considerations</span></span>

* <span data-ttu-id="8cdc7-190">입력 비디오에는 오디오 트랙이 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="8cdc7-191">입력 비디오는 모두 프레임 속도가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-191">Input videos should all have the same frame rate.</span></span>
* <span data-ttu-id="8cdc7-192">비디오는 별도의 자산에 업로드하고 비디오를 각 자산의 기본 파일로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-192">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span></span>
* <span data-ttu-id="8cdc7-193">비디오의 기간을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-193">You need to know the duration of your videos.</span></span>
* <span data-ttu-id="8cdc7-194">아래의 사전 설정 예제에서는 모든 입력 비디오가 타임스탬프 0에서 시작한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-194">The preset examples below assumes that all the input videos start with a timestamp of zero.</span></span> <span data-ttu-id="8cdc7-195">시작 타임스탬프가 다르면 StartTime 값을 수정해야 합니다. 라이브 보관에서는 이런 경우가 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-195">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span></span>
* <span data-ttu-id="8cdc7-196">JSON 사전 설정은 입력 자산의 AssetID 값에 대한 명시적 참조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-196">The JSON preset makes explicit references to the AssetID values of the input assets.</span></span>
* <span data-ttu-id="8cdc7-197">샘플 코드에서는 JSON 사전 설정이 로컬 파일(예: "C:\supportFiles\preset.json")에 저장되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-197">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="8cdc7-198">또한 두 비디오 파일을 업로드하여 두 자산을 만들었으며 사용자가 그에 따른 AssetID 값을 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-198">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span></span>
* <span data-ttu-id="8cdc7-199">코드 조각 및 JSON 사전 설정은 두 비디오 파일을 연결하는 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-199">The code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="8cdc7-200">이 예를 다음을 통해 3개 이상의 비디오로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-200">You can extend it to more than two videos by:</span></span>

  1. <span data-ttu-id="8cdc7-201">task.InputAssets.Add()를 반복 호출하여 순서대로 더 많은 비디오 추가</span><span class="sxs-lookup"><span data-stu-id="8cdc7-201">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span></span>
  2. <span data-ttu-id="8cdc7-202">같은 순서로 다른 항목을 추가하여 JSON에서 "Sources" 요소를 그에 맞게 편집</span><span class="sxs-lookup"><span data-stu-id="8cdc7-202">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="8cdc7-203">.NET 코드</span><span class="sxs-lookup"><span data-stu-id="8cdc7-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass to it the name of the
    // processor to use for the specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load the XML (or JSON) from the local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify the input videos to be concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset to contain the results of the job.
    // This output is specified as AssetCreationOptions.None, which
    // means the output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="8cdc7-204">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-204">JSON preset</span></span>

<span data-ttu-id="8cdc7-205">연결하려는 자산의 ID와 각 비디오에 적합한 시간 세그먼트로 사용자 지정 사전 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-205">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <span data-ttu-id="8cdc7-206"><a id="crop"></a>미디어 인코더 표준으로 비디오 자르기</span><span class="sxs-lookup"><span data-stu-id="8cdc7-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="8cdc7-207">[미디어 인코더 표준으로 비디오 자르기](media-services-crop-video.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-207">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="8cdc7-208"><a id="no_video"></a>입력에 비디오가 없을 때 비디오 트랙 삽입</span><span class="sxs-lookup"><span data-stu-id="8cdc7-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="8cdc7-209">기본적으로 오디오만 포함하며 비디오는 없는 입력을 인코더로 보내면 출력 자산에는 오디오 데이터만 들어 있는 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-209">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span></span> <span data-ttu-id="8cdc7-210">Azure Media Player( [이 항목](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)참조)를 비롯한 일부 플레이어는 이러한 스트림을 처리하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span></span> <span data-ttu-id="8cdc7-211">해당 시나리오에서는 이 설정을 사용하여 인코더가 출력에 단색 비디오 트랙을 추가하도록 강제 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-211">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="8cdc7-212">인코더가 출력 비디오 트랙을 삽입하도록 강제 지정하면 출력 자산의 크기가 증가하므로 인코딩 태스크에 대한 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-212">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span></span> <span data-ttu-id="8cdc7-213">따라서 테스트를 실행하여 이러한 크기 증가가 월 요금에 주는 영향이 적절한 수준인지를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-213">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-the-lowest-bitrate"></a><span data-ttu-id="8cdc7-214">최저 비트 전송률에서만 비디오 삽입</span><span class="sxs-lookup"><span data-stu-id="8cdc7-214">Inserting video at only the lowest bitrate</span></span>

<span data-ttu-id="8cdc7-215">["H264 다중 비트 전송률 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) 와 같은 다중 비트 전송률 인코딩 사전 설정을 사용하여 비디오 파일과 오디오 전용 파일이 혼합되어 있는 입력 카탈로그 전체를 스트리밍용으로 인코딩한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="8cdc7-216">이 시나리오에서는 입력에 비디오가 없으면 모든 출력 비트 속도에서 비디오를 삽입하는 대신 인코더가 최저 비트 속도에서만 단색 비디오 트랙을 삽입하도록 강제 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-216">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span></span> <span data-ttu-id="8cdc7-217">이렇게 하려면 **InsertBlackIfNoVideoBottomLayerOnly** 플래그를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-217">To achieve this, you need to use the **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="8cdc7-218">[이 섹션](media-services-mes-presets-overview.md)에 문서화된 MES 사전 설정 중 하나를 가져온 후에 다음과 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-218">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="8cdc7-219">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="8cdc7-220">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-220">XML preset</span></span>

<span data-ttu-id="8cdc7-221">XML을 사용하는 경우 **H264Video** 요소에 대한 특성으로 Condition="InsertBlackIfNoVideoBottomLayerOnly"를 사용하고 **AACAudio**에 대한 특성으로 Condition="InsertSilenceIfNoAudio"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="8cdc7-222">모든 출력 비트 전송률에서 비디오 삽입</span><span class="sxs-lookup"><span data-stu-id="8cdc7-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="8cdc7-223">["H264 다중 비트 전송률 720p"](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 와 같은 다중 비트 전송률 인코딩 사전 설정을 사용하여 비디오 파일과 오디오 전용 파일이 혼합되어 있는 입력 카탈로그 전체를 스트리밍용으로 인코딩한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="8cdc7-224">이 시나리오에서는 입력에 비디오가 없으면 인코더가 모든 출력 비트 속도에서 단색 비디오 트랙을 삽입하도록 강제 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-224">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span></span> <span data-ttu-id="8cdc7-225">이렇게 하면 출력 자산의 비디오 트래픽 및 오디오 트랙 수가 모두 같아집니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-225">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span></span> <span data-ttu-id="8cdc7-226">이렇게 하려면 "InsertBlackIfNoVideo" 플래그를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-226">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="8cdc7-227">[이 섹션](media-services-mes-presets-overview.md)에 문서화된 MES 사전 설정 중 하나를 가져온 후에 다음과 같이 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-227">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="8cdc7-228">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="8cdc7-229">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-229">XML preset</span></span>

<span data-ttu-id="8cdc7-230">XML을 사용하는 경우 **H264Video** 요소에 대한 특성으로 Condition="InsertBlackIfNoVideo"를 사용하고 **AACAudio**에 대한 특성으로 Condition="InsertSilenceIfNoAudio"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="8cdc7-231"><a id="rotate_video"></a>비디오 회전</span><span class="sxs-lookup"><span data-stu-id="8cdc7-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="8cdc7-232">[Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)는 0/90/180/270도 회전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-232">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="8cdc7-233">기본 동작은 들어오는 비디오 파일에서 회전 메타데이터를 검색하여 그에 맞게 보정하는 "Auto"입니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-233">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span></span> <span data-ttu-id="8cdc7-234">다음 **Sources** 요소를 [이 섹션](media-services-mes-presets-overview.md)에 정의된 사전 설정 중 하나에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-234">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="8cdc7-235">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="8cdc7-236">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="8cdc7-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="8cdc7-237">또한 회전 보정이 트리거된 경우 인코더가 사전 설정에서 너비 및 높이를 해석하는 방법에 대한 자세한 내용은 [이](media-services-mes-schema.md#PreserveResolutionAfterRotation) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cdc7-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="8cdc7-238">"0" 값을 사용하여 인코더가 입력 비디오에서 회전 메타데이터를 무시한다는 것을 나타낼 수 있습니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="8cdc7-238">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8cdc7-239">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="8cdc7-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8cdc7-240">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="8cdc7-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8cdc7-241">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8cdc7-241">See Also</span></span>
[<span data-ttu-id="8cdc7-242">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="8cdc7-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
