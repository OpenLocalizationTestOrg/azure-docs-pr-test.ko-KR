---
title: "MES (미디어 인코더 표준)에 대 한 사전 설정 aaaTask | Microsoft Docs"
description: "MES (미디어 인코더 표준)의 태스크 사전 설정의 개요 및 hello 항목 제공 합니다."
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
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a><span data-ttu-id="f16e2-103">MES(Media Encoder Standard)에 대한 작업 미리 설정</span><span class="sxs-lookup"><span data-stu-id="f16e2-103">Task Presets for MES (Media Encoder Standard)</span></span>

<span data-ttu-id="f16e2-104">**Media Encoder Standard**는 인코딩 작업을 만들 때 사용할 수 있는 인코딩 미리 설정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-104">**Media Encoder Standard** defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="f16e2-105">Toouse hello "적응 스트리밍" tooencode 비디오 미디어 서비스 스트리밍 하려는 경우를 미리 설정 된 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-105">It is recommended toouse hello "Adaptive Streaming" preset if you want tooencode a video for streaming with Media Services.</span></span> <span data-ttu-id="f16e2-106">사전 설정을 지정할 경우 Media Encoder Standard는 [비트 전송률 단계를 자동으로 생성](media-services-autogen-bitrate-ladder-with-mes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-106">When you specify this preset, Media Encoder Standard will [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md).</span></span> 

<span data-ttu-id="f16e2-107">그러나 toocustomize는 인코딩 사전 설정을 해야 할 경우 수행 해야 인코딩 사전 설정을 사용자 지정 구성에 대 한 템플릿으로이 섹션에 정의 된 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-107">However, if you need toocustomize an encoding preset, you should take one of hello encoding presets defined in this section as a template for your custom configuration.</span></span> <span data-ttu-id="f16e2-108">이러한 사전 설정 방법 및 hello 유효한 값에 있는 각 요소의의 각 요소에 대 한 설명을 참조 hello [미디어 인코더 표준 스키마](media-services-mes-schema.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-108">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f16e2-109">4k 인코딩합니다에 대 한 사전 설정을 사용 하 여, hello 얻어야 `S3` 예약 단위 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-109">When using a preset for 4k encodes, you should get hello `S3` reserved unit type.</span></span> <span data-ttu-id="f16e2-110">자세한 내용은 참조 [어떻게 tooScale 인코딩](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-110">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
<span data-ttu-id="f16e2-111">Media Encoder Standard로 작업할 때 기본적으로 회전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-111">When working with Media Encoder Standard, rotation is enabled by default.</span></span> <span data-ttu-id="f16e2-112">이러한 사전 설정, 기본적으로 돌려 tooLandscape 모드 이전 tooencoding (달리, 여기서 비디오 회전은 수동 작업, Azure 미디어 인코더를 사용할 때 다음 비디오는 스마트폰 또는 세로 모드의 기타 모바일 장치에 기록 된 경우 에 설명 된 대로 [이](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) 블로그의 "비디오 회전"에서).</span><span class="sxs-lookup"><span data-stu-id="f16e2-112">If your video has been recorded on a smartphone or other mobile device in Portrait mode, then these presets will, by default, rotate them tooLandscape mode prior tooencoding (unlike, when you work with Azure Media Encoder, where video rotation is a manual operation, as documented in [this](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, under “Video Rotation”).</span></span>  
  
<span data-ttu-id="f16e2-113">사용 가능한 사전 설정:</span><span class="sxs-lookup"><span data-stu-id="f16e2-113">Available presets:</span></span>  
  
 <span data-ttu-id="f16e2-114">[H264 다중 비트 전송률 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) 6000 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-114">[H264 Multiple Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps too400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-115">[H264 다중 비트 전송률 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) 6000 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-115">[H264 Multiple Bitrate 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produces a set of 8 GOP-aligned MP4 files, ranging from 6000 kbps too400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-116">[H264 다중 비트 전송률 16x9 iOS 용](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) 8500 kbps too200 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-116">[H264 Multiple Bitrate 16x9 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps too200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-117">[H264 다중 비트 전송률 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) 1900 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-117">[H264 Multiple Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps too400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-118">[H264 다중 비트 전송률 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) 1900 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-118">[H264 Multiple Bitrate 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps too400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-119">[H264 다중 비트 전송률 4k Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) 20000 kbps too1000 kbps 및 AAC 5.1 오디오에서 사이의 12 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-119">[H264 Multiple Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps too1000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-120">[H264 다중 비트 전송률 4k](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) 20000 kbps too1000 kbps 및 AAC 오디오 스테레오에서 사이의 12 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-120">[H264 Multiple Bitrate 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produces a set of 12 GOP-aligned MP4 files, ranging from 20000 kbps too1000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-121">[H264 다중 비트 전송률 4x3 iOS 용](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) 8500 kbps too200 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-121">[H264 Multiple Bitrate 4x3 for iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produces a set of 8 GOP-aligned MP4 files, ranging from 8500 kbps too200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-122">[H264 다중 비트 전송률 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) 1600 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-122">[H264 Multiple Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps too400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-123">[H264 다중 비트 전송률 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) 1600 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-123">[H264 Multiple Bitrate 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produces a set of 5 GOP-aligned MP4 files, ranging from 1600 kbps too400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-124">[H264 다중 비트 전송률 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) 3400 kbps too400 kbps 및 AAC 5.1 오디오에서 사이의 6 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-124">[H264 Multiple Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps too400 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-125">[H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 3400 kbps too400 kbps 및 AAC 오디오 스테레오에서 사이의 6 GOP 정렬 MP4 파일 집합을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-125">[H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produces a set of 6 GOP-aligned MP4 files, ranging from 3400 kbps too400 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-126">[H264 단일 비트 전송 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-126">[H264 Single Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) produces a single MP4 file with a bitrate of 6750 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-127">[H264 단일 비트 전송 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md)는 스테레오 AAC 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-127">[H264 Single Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) produces a single MP4 file with a bitrate of 6750 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-128">[H264 단일 비트 전송 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-128">[H264 Single Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-129">[H264 단일 비트 전송 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md)는 스테레오 AAC 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-129">[H264 Single Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-130">[H264 단일 비트 전송 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-130">[H264 Single Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 1800 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-131">[H264 단일 비트 전송 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-131">[H264 Single Bitrate 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) produces a single MP4 file with a bitrate of 1800 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-132">[H264 단일 비트 전송 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-132">[H264 Single Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) produces a single MP4 file with a bitrate of 2200 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-133">[H264 단일 비트 전송 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-133">[H264 Single Bitrate 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-134">[H264 단일 비트 전송 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-134">[H264 Single Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) produces a single MP4 file with a bitrate of 4500 kbps, and AAC 5.1 audio.</span></span>  
  
 <span data-ttu-id="f16e2-135">[Android용 H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md)은 스테레오 AAC 및 비트 전송률이 2000kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-135">[H264 Single Bitrate 720p for Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) preset produces a single MP4 file with a bitrate of 2000 kbps, and stereo AAC.</span></span>  
  
 <span data-ttu-id="f16e2-136">[H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md)는 스테레오 AAC 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-136">[H264 Single Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-137">[Android용 H264 단일 비트 전송 고품질 SD](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 500kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-137">[H264 Single Bitrate High Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio..</span></span>  
  
 <span data-ttu-id="f16e2-138">[Android용 H264 단일 비트 전송 저품질 SD](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 56kbps인 단일 MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-138">[H264 Single Bitrate Low Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) produces a single MP4 file with a bitrate of 56 kbps, and stereo AAC audio.</span></span>  
  
 <span data-ttu-id="f16e2-139">자세한 내용은 관련된 tooMedia 서비스 인코더 참조 [인코딩 주문형 Azure 미디어 서비스로](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f16e2-139">For more information related tooMedia Services encoders, see [Encoding On-Demand with Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).</span></span>
