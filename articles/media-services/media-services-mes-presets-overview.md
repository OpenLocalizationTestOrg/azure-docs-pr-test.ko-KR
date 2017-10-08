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
# <a name="task-presets-for-mes-media-encoder-standard"></a>MES(Media Encoder Standard)에 대한 작업 미리 설정

**Media Encoder Standard**는 인코딩 작업을 만들 때 사용할 수 있는 인코딩 미리 설정을 정의합니다. Toouse hello "적응 스트리밍" tooencode 비디오 미디어 서비스 스트리밍 하려는 경우를 미리 설정 된 것이 좋습니다. 사전 설정을 지정할 경우 Media Encoder Standard는 [비트 전송률 단계를 자동으로 생성](media-services-autogen-bitrate-ladder-with-mes.md)합니다. 

그러나 toocustomize는 인코딩 사전 설정을 해야 할 경우 수행 해야 인코딩 사전 설정을 사용자 지정 구성에 대 한 템플릿으로이 섹션에 정의 된 hello 중 하나입니다. 이러한 사전 설정 방법 및 hello 유효한 값에 있는 각 요소의의 각 요소에 대 한 설명을 참조 hello [미디어 인코더 표준 스키마](media-services-mes-schema.md) 항목입니다.  
  
> [!NOTE]
>  4k 인코딩합니다에 대 한 사전 설정을 사용 하 여, hello 얻어야 `S3` 예약 단위 형식입니다. 자세한 내용은 참조 [어떻게 tooScale 인코딩](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units)합니다.  
  
Media Encoder Standard로 작업할 때 기본적으로 회전이 사용됩니다. 이러한 사전 설정, 기본적으로 돌려 tooLandscape 모드 이전 tooencoding (달리, 여기서 비디오 회전은 수동 작업, Azure 미디어 인코더를 사용할 때 다음 비디오는 스마트폰 또는 세로 모드의 기타 모바일 장치에 기록 된 경우 에 설명 된 대로 [이](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) 블로그의 "비디오 회전"에서).  
  
사용 가능한 사전 설정:  
  
 [H264 다중 비트 전송률 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) 6000 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) 6000 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 16x9 iOS 용](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) 8500 kbps too200 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 16x9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) 1900 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) 1900 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 4k Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) 20000 kbps too1000 kbps 및 AAC 5.1 오디오에서 사이의 12 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 4k](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) 20000 kbps too1000 kbps 및 AAC 오디오 스테레오에서 사이의 12 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 4x3 iOS 용](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) 8500 kbps too200 kbps 및 AAC 오디오 스테레오에서 까지의 8 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 4x3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) 1600 kbps too400 kbps 및 AAC 5.1 오디오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) 1600 kbps too400 kbps 및 AAC 오디오 스테레오에서 까지의 5 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) 3400 kbps too400 kbps 및 AAC 5.1 오디오에서 사이의 6 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 3400 kbps too400 kbps 및 AAC 오디오 스테레오에서 사이의 6 GOP 정렬 MP4 파일 집합을 생성 합니다.  
  
 [H264 단일 비트 전송 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md)는 스테레오 AAC 오디오 및 비트 전송률이 6750kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md)는 스테레오 AAC 오디오 및 비트 전송률이 18000kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 1800kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md)는 스테레오 AAC 오디오 및 비트 전송률이 2200kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md)은 AAC 5.1 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.  
  
 [Android용 H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md)은 스테레오 AAC 및 비트 전송률이 2000kbps인 단일 MP4 파일을 생성합니다.  
  
 [H264 단일 비트 전송 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md)는 스테레오 AAC 오디오 및 비트 전송률이 4500kbps인 단일 MP4 파일을 생성합니다.  
  
 [Android용 H264 단일 비트 전송 고품질 SD](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 500kbps인 단일 MP4 파일을 생성합니다.  
  
 [Android용 H264 단일 비트 전송 저품질 SD](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md)는 스테레오 AAC 오디오 및 비트 전송률이 56kbps인 단일 MP4 파일을 생성합니다.  
  
 자세한 내용은 관련된 tooMedia 서비스 인코더 참조 [인코딩 주문형 Azure 미디어 서비스로](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/)합니다.
