---
title: "aaaH264 단일 비트 전송률 720p Audio 5.1 | Microsoft Docs"
description: "hello에 대 한 개요를 제공 하는 hello 항목 * * H264 단일 비트 전송률 720p Audio 5.1* * 작업 기본 설정 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ba2bfa57-3c87-4b1b-b91b-58f9108f4e85
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 32b8b104dd288954310e044c05c3bc67f8b8d27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-720p-audio-51"></a><span data-ttu-id="87104-103">H264 단일 비트 전송률 720p Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="87104-103">H264 Single Bitrate 720p Audio 5.1</span></span>
<span data-ttu-id="87104-104">`Media Encoder Standard`는 인코딩 작업을 만들 때 사용할 수 있는 인코딩 미리 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="87104-105">사용할 수 있습니다는 `preset name` 어떤 형식으로 원하는 tooencode toospecify 미디어 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="87104-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="87104-106">또는 자신만의 JSON 또는 XML 기반 미리 설정(UTF-8 또는 UTF-16 인코딩을 사용하여)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87104-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="87104-107">그런 다음 hello 미리 설정 된 toohello 사용자 지정 인코더를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="87104-108">사전 설정 이름을이에서 지 원하는 모든 hello 목록이 hello에 대 한 `Media Encoder Standard` 인코더 참조 [미디어 인코더 표준의 태스크 사전 설정](media-services-mes-presets-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="87104-109">이 항목에서는 hello `H264 Single Bitrate 720p Audio 5.1` XML 및 JSON 형식으로 미리 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-109">This topic shows hello `H264 Single Bitrate 720p Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="87104-110">이 미리 설정은 AAC 5.1 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="87104-111">프로필에 대 한 자세한 정보에 대 한 비트 전송률, 샘플링 속도 등에이 사전 설정, XML 또는 JSON 아래에 정의 된 hello를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="87104-112">각 요소의 의미 및 hello 유효한 값의 각 요소에 대 한 설명을 참조 hello [미디어 인코더 표준 스키마](media-services-mes-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87104-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
 <span data-ttu-id="87104-113">XML</span><span class="sxs-lookup"><span data-stu-id="87104-113">XML</span></span>  
  
```  
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
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="87104-114">JSON</span><span class="sxs-lookup"><span data-stu-id="87104-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 4500,  
          "MaxBitrate": 4500,  
          "BufferWindow": "00:00:05",  
          "Width": 1280,  
          "Height": 720,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
