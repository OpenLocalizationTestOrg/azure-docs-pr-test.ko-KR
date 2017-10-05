---
title: "H264 다중 비트 전송률 1080p Media Encoder Standard 사전 설정-Azure | Microsoft Docs"
description: "이 항목은 **H264 다중 비트 전송률 1080p** 태스크 미리 설정에 대한 개요를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 7096d8e9-2953-48b3-9d1c-8f7ff6a38e91
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: a1aa9c097ae3eba6c14476d58b432d8d8cc126c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="h264-multiple-bitrate-1080p"></a><span data-ttu-id="c5726-103">H264 다중 비트 전송률 1080p</span><span class="sxs-lookup"><span data-stu-id="c5726-103">H264 Multiple Bitrate 1080p</span></span>
<span data-ttu-id="c5726-104">`Media Encoder Standard`는 인코딩 작업을 만들 때 사용할 수 있는 인코딩 미리 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="c5726-105">`preset name`을 사용하여 미디어 파일을 인코딩할 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="c5726-106">또는 자신만의 JSON 또는 XML 기반 미리 설정(UTF-8 또는 UTF-16 인코딩을 사용하여)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="c5726-107">그런 다음 사용자 지정 미리 설정을 인코더에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="c5726-108">`Media Encoder Standard` 인코더에서 지원되는 모든 미리 설정 이름의 목록을 보려면 [Media Encoder Standard에 대한 작업 미리 설정](media-services-mes-presets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5726-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="c5726-109">이 항목은 XML 및 JSON 형식의 `H264 Multiple Bitrate 1080p` 미리 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-109">This topic shows the `H264 Multiple Bitrate 1080p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="c5726-110">미리 설정은 스테레오 AAC 오디오 및 6000kbps에서 400kbps에 이르는 8 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-110">This preset produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps to 400 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="c5726-111">미리 설정의 프로필, 비트 전송률, 샘플링 주기 등에 대한 자세한 내용을 보려면 아래 정의된 XML 또는 JSON을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="c5726-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="c5726-112">미리 설정에 포함된 각 요소의 의미 및 유효한 값에 대한 설명은 [Media Encoder Standard 스키마](media-services-mes-schema.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5726-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c5726-113">계층에서 `Width` 및 `Height` 값을 수정하는 경우 가로 세로 비율을 일관적으로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5726-113">When modifying the `Width` and `Height` values across layers, make sure that the aspect ratio remains consistent.</span></span> <span data-ttu-id="c5726-114">예: 1920x1080, 1280x720, 1080x576, 640x360.</span><span class="sxs-lookup"><span data-stu-id="c5726-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="c5726-115">가로 세로 비율을 혼합하여 사용하지 말아야 합니다. 예: 1280x720, 720x480, 640x360.</span><span class="sxs-lookup"><span data-stu-id="c5726-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="c5726-116">XML</span><span class="sxs-lookup"><span data-stu-id="c5726-116">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>6000</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>6000</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>4700</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>4700</MaxBitrate>  
        </H264Layer>  
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
      <Chapters />  
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
```  
  
 <span data-ttu-id="c5726-117">JSON</span><span class="sxs-lookup"><span data-stu-id="c5726-117">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 6000,  
          "MaxBitrate": 6000,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
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
          "Bitrate": 4700,  
          "MaxBitrate": 4700,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
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
```
