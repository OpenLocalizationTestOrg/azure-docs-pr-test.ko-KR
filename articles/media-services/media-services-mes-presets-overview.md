---
title: "MES(Media Encoder Standard)에 대한 작업 미리 설정 | Microsoft Docs"
description: "이 항목에서는 MES(Media Encoder Standard)에 대한 작업 미리 설정에 대해 간단히 설명합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 6fcdd361b7725b1a5136828cede24cdaac5dacc1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a><span data-ttu-id="54913-103">MES(Media Encoder Standard)에 대한 작업 미리 설정</span><span class="sxs-lookup"><span data-stu-id="54913-103">Task Presets for MES (Media Encoder Standard)</span></span>

<span data-ttu-id="54913-104">**Media Encoder Standard**는 인코딩 작업을 만들 때 사용할 수 있는 인코딩 미리 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-104">**Media Encoder Standard** defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="54913-105">Media Services로 스트리밍을 위해 비디오를 인코딩하려면 "적응 스트리밍" 사전 설정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="54913-105">It is recommended to use the "Adaptive Streaming" preset if you want to encode a video for streaming with Media Services.</span></span> <span data-ttu-id="54913-106">사전 설정을 지정할 경우 Media Encoder Standard는 [비트 전송률 단계를 자동으로 생성](media-services-autogen-bitrate-ladder-with-mes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-106">When you specify this preset, Media Encoder Standard will [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md).</span></span> 

<span data-ttu-id="54913-107">그러나 인코딩 사전 설정을 사용자 지정해야 하는 경우 이 섹션에 정의된 인코딩 사전 설정 중 하나를 사용자 지정 구성에 대한 템플릿으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-107">However, if you need to customize an encoding preset, you should take one of the encoding presets defined in this section as a template for your custom configuration.</span></span> <span data-ttu-id="54913-108">미리 설정에 포함된 각 요소의 의미 및 유효한 값에 대한 설명은 [Media Encoder Standard 스키마](media-services-mes-schema.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54913-108">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="54913-109">4k 인코드에 대한 미리 설정을 사용하는 경우 `S3` 예약 단위 형식을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-109">When using a preset for 4k encodes, you should get the `S3` reserved unit type.</span></span> <span data-ttu-id="54913-110">자세한 내용은 [인코딩 크기를 조정하는 방법](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54913-110">For more information, see [How to Scale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
<span data-ttu-id="54913-111">Media Encoder Standard로 작업할 때 기본적으로 회전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="54913-111">When working with Media Encoder Standard, rotation is enabled by default.</span></span> <span data-ttu-id="54913-112">비디오를 스마트폰 또는 기타 모바일 장치에 세로 모드로 녹화한 경우 기본적으로 이러한 미리 설정에 따라 인코딩 전에 가로 모드로 회전됩니다([이](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) 블로그의 "비디오 회전"에 설명된 것처럼 비디오 회전이 수동 작업인 Azure Media Encoder로 작업하는 경우와 다름).</span><span class="sxs-lookup"><span data-stu-id="54913-112">If your video has been recorded on a smartphone or other mobile device in Portrait mode, then these presets will, by default, rotate them to Landscape mode prior to encoding (unlike, when you work with Azure Media Encoder, where video rotation is a manual operation, as documented in [this](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, under “Video Rotation”).</span></span>  
  
<span data-ttu-id="54913-113">사용 가능한 사전 설정:</span><span class="sxs-lookup"><span data-stu-id="54913-113">Available presets:</span></span>  
  
 <span data-ttu-id="54913-114">[H264 다중 비트 전송 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md)은 AAC 5.1 오디오 및 6000kbps에서 400kbps에 이르는 8 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-114">[H264 Multiple Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-115">[H264 다중 비트 전송 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md)은 스테레오 AAC 오디오 및 6000kbps에서 400kbps에 이르는 8 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-115">[H264 Multiple Bitrate 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-116">[iOS용 H264 다중 비트 전송 16x9](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md)는 스테레오 AAC 오디오 및 8500kbps에서 200kbps에 이르는 8 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-116">[H264 Multiple Bitrate 16x9 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps to 200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-117">[H264 다중 비트 전송 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 1900kbps에서 400kbps에 이르는 5 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-117">[H264 Multiple Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-118">[H264 다중 비트 전송 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md)은 스테레오 AAC 오디오 및 1900kbps에서 400kbps에 이르는 5 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-118">[H264 Multiple Bitrate 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-119">[H264 다중 비트 전송 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md)은 AAC 5.1 오디오 및 20000kbps에서 1000kbps에 이르는 12 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-119">[H264 Multiple Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps to 1000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-120">[H264 다중 비트 전송 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md)은 스테레오 AAC 오디오 및 20000kbps에서 1000kbps에 이르는 12 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-120">[H264 Multiple Bitrate 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps to 1000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-121">[iOS용 H264 다중 비트 전송 4x3](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md)는 스테레오 AAC 오디오 및 8500kbps에서 200kbps에 이르는 8 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-121">[H264 Multiple Bitrate 4x3 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps to 200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-122">[H264 다중 비트 전송 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 1600kbps에서 400kbps에 이르는 5 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-122">[H264 Multiple Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-123">[H264 다중 비트 전송 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md)는 스테레오 AAC 오디오 및 1600kbps에서 400kbps에 이르는 5 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-123">[H264 Multiple Bitrate 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-124">[H264 다중 비트 전송 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md)은 AAC 5.1 오디오 및 3400kbps에서 400kbps에 이르는 6 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-124">[H264 Multiple Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps to 400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-125">[H264 다중 비트 전송 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md)는 스테레오 AAC 오디오 및 3400kbps에서 400kbps에 이르는 6 GOP 정렬 MP4 파일 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-125">[H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps to 400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-126">[H264 단일 비트 전송 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-126">[H264 Single Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produces a single MP4 file with a bitrate of 6750 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-127">[H264 단일 비트 전송 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md)는 스테레오 AAC 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-127">[H264 Single Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produces a single MP4 file with a bitrate of 6750 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-128">[H264 단일 비트 전송 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-128">[H264 Single Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-129">[H264 단일 비트 전송 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md)는 스테레오 AAC 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-129">[H264 Single Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-130">[H264 단일 비트 전송 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-130">[H264 Single Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 1800 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-131">[H264 단일 비트 전송 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-131">[H264 Single Bitrate 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produces a single MP4 file with a bitrate of 1800 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-132">[H264 단일 비트 전송 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-132">[H264 Single Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 2200 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-133">[H264 단일 비트 전송 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-133">[H264 Single Bitrate 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-134">[H264 단일 비트 전송 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-134">[H264 Single Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="54913-135">[Android용 H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md)은 스테레오 AAC 및 비트 전송률이 2000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-135">[H264 Single Bitrate 720p for Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) preset produces a single MP4 file with a bitrate of 2000 kbps, and stereo AAC.</span></span>  
  
 <span data-ttu-id="54913-136">[H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md)는 스테레오 AAC 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-136">[H264 Single Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-137">[Android용 H264 단일 비트 전송 고품질 SD](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-137">[H264 Single Bitrate High Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio..</span></span>  
  
 <span data-ttu-id="54913-138">[Android용 H264 단일 비트 전송 저품질 SD](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 56kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="54913-138">[H264 Single Bitrate Low Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 56 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="54913-139">Media Services 인코더와 관련된 자세한 내용은 [Azure Media Services를 사용하여 주문형 인코딩](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="54913-139">For more information related to Media Services encoders, see [Encoding On-Demand with Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).</span></span>
