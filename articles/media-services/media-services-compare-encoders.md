---
title: "요청 시 미디어 인코더에서 Azure의 aaaComparison | Microsoft Docs"
description: "이 항목에서는의 hello 인코딩 기능 비교 * * 미디어 인코더 표준 * * 및 * * 미디어 인코더 프리미엄 워크플로 * *입니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: ee04ad10d8e7c5f4f3c6e91e9b7679c2aba82c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Azure 주문형 미디어 인코더 비교

이 항목에서는의 hello 인코딩 기능 비교 **미디어 인코더 표준** 및 **미디어 인코더 프리미엄 워크플로**합니다.

## <a name="video-and-audio-processing-capabilities"></a>비디오 및 오디오 처리 기능

다음 표에서 hello 미디어 인코더 표준 MES () 및 미디어 인코더 프리미엄 워크플로 (MEPW) 사이의 hello 기능을 비교 합니다. 

|기능|미디어 인코더 표준|미디어 인코더 Premium 워크플로|
|---|---|---|
|인코딩 중에 조건부 논리 적용<br/>(예를 들어 hello 입력 HD 이면 다음 5.1 오디오 인코딩)|아니요|예|
|선택 자막|아니요|[예](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Dolby® Professional Loudness Correction](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> Dialogue Intelligence™ 사용|아니요|예|
|디-인터레이스, 역텔레시네|Basic|브로드캐스트 품질|
|검은색 테두리 감지 및 제거 <br/>(필러박스, 레터박스)|아니요|예|
|썸네일 생성|[예](media-services-dotnet-generate-thumbnail-with-mes.md)|[예](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|비디오 클리핑/잘라내기 및 붙이기|[예](media-services-advanced-encoding-with-mes.md#trim_video)|예|
|오디오 또는 비디오 오버레이|[예](media-services-advanced-encoding-with-mes.md#overlay)|[예](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|그래픽 오버레이|이미지 원본에서|이미지 및 텍스트 원본에서|
|다중 오디오 언어 트랙|제한적|[예](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>각 인코더에서 사용되는 요금 청구 기준
| 미디어 프로세서 이름 | 적용 가능한 가격 | 참고 사항 |
| --- | --- | --- |
| **미디어 인코더 표준** |인코더 |인코딩 작업 비용이 청구 됩니다 (분) 지정 하는 hello 속도로 출력으로 생성 된 모든 hello 미디어 파일의 hello 총 기간에 따라 [여기][1], hello 인코더 열 아래에서 합니다. |
| **Media Encoder Premium 워크플로** |프리미엄 인코더 |인코딩 작업 비용이 청구 됩니다 (분) 지정 하는 hello 속도로 출력으로 생성 된 모든 hello 미디어 파일의 hello 총 기간에 따라 [여기][1], hello 프리미엄 인코더 열 아래에서 합니다. |

## <a name="input-containerfile-formats"></a>입력 컨테이너/파일 형식
| 입력 컨테이너/파일 형식 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| Adobe® Flash® F4V |예 |예 |
| MXF/SMPTE 377M |예 |예 |
| GXF |예 |예 |
| MPEG-2 전송 스트림 |예 |예 |
| MPEG-2 프로그램 스트림 |예 |예 |
| MPEG-4/MP4 |예 |예 |
| Windows Media/ASF |예 |예 |
| AVI(압축되지 않은 8비트/10비트) |예 |예 |
| 3GPP/3GPP2 |예 |아니요 |
| 부드러운 스트리밍 파일 형식(PIFF 1.3) |예 |아니요 |
| [DVR-MS(Microsoft Digital Video Recording)](https://msdn.microsoft.com/library/windows/desktop/dd692984) |예 |아니요 |
| Matroska/WebM |예 |아니요 |
| QuickTime(.mov) |예 |아니요 |

## <a name="input-video-codecs"></a>입력 비디오 코덱
| 입력 비디오 코덱 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| AVC 8 비트/10-비트, AVCIntra를 포함 하 여 too4:2:2 |8비트 4:2:0 및 4:2:2 |예 |
| Avid DNxHD(MXF) |예 |예 |
| DVCPro/DVCProHD(MXF) |예 |예 |
| JPEG2000 |예 |예 |
| Mpeg-2 (too422 프로필 및 상위 수준을 비롯 하 여, 변형 XDCAM, XDCAM HD, XDCAM IMX, CableLabs® d 10 등) |Too422 프로필 |예 |
| MPEG-1 |예 |예 |
| Windows Media 비디오/VC-1 |예 |예 |
| Canopus HQ/HQX |아니요 |아니요 |
| Mpeg-4 2부 |예 |아니요 |
| [Theora](https://en.wikipedia.org/wiki/Theora) |예 |아니요 |
| Apple ProRes 422 |예 |아니요 |
| Apple ProRes 422 LT |예 |아니요 |
| Apple ProRes 422 HQ |예 |아니요 |
| Apple ProRes Proxy |예 |아니요 |
| Apple ProRes 4444 |예 |아니요 |
| Apple ProRes 4444 XQ |예 |아니요 |

## <a name="input-audio-codecs"></a>입력 오디오 코덱
| 입력 오디오 코덱 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| AES(SMPTE 331M 및 302M, AES3-2003) |아니요 |예 |
| Dolby® E |아니요 |예 |
| Dolby® Digital(AC3) |아니요 |예 |
| Dolby® Digital Plus(E-AC3) |아니요 |예 |
| AAC (AAC-LC, AAC 그 및 AAC HEv2; too5.1 구성) |예 |예 |
| MPEG Layer 2 |예 |예 |
| MP3(MPEG-1 Audio Layer 3) |예 |예 |
| Windows Media 오디오 |예 |예 |
| WAV/PCM |예 |예 |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |예 |아니요 |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |예 |아니요 |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |예 |아니요 |

## <a name="output-containerfile-formats"></a>출력 컨테이너/파일 형식
| 출력 컨테이너/파일 형식 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| Adobe® Flash® F4V |아니요 |예 |
| MXF(OP1a, XDCAM 및 AS02) |아니요 |예 |
| DPP(AS11 포함) |아니요 |예 |
| GXF |아니요 |예 |
| MPEG-4/MP4 |예 |예 |
| MPEG-TS |예 |예 |
| Windows Media/ASF |아니요 |예 |
| AVI(압축되지 않은 8비트/10비트) |아니요 |예 |
| 부드러운 스트리밍 파일 형식(PIFF 1.3) |아니요 |예 |

## <a name="output-video-codecs"></a>출력 비디오 코덱
| 출력 비디오 코덱 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| AVC (h. 264; 8 비트; tooHigh 프로필 수준 5.2; 4k 울트라 HD; 위로 AVC 내) |8비트 4:2:0만 |예 |
| Avid DNxHD(MXF) |아니요 |예 |
| Mpeg-2 (too422 프로필 및 상위 수준을 비롯 하 여, 변형 XDCAM, XDCAM HD, XDCAM IMX, CableLabs® d 10 등) |아니요 |예 |
| MPEG-1 |아니요 |예 |
| Windows Media 비디오/VC-1 |아니요 |예 |
| JPEG 축소판 그림 만들기 |예 |예 |
| PNG 썸네일 만들기 |예 |예 |
| BMP 썸네일 만들기 |예 |아니요 |

## <a name="output-audio-codecs"></a>출력 오디오 코덱
| 출력 오디오 코덱 | 미디어 인코더 표준 | 미디어 인코더 Premium 워크플로 |
| --- | --- | --- |
| AES(SMPTE 331M 및 302M, AES3-2003) |아니요 |예 |
| Dolby® Digital(AC3) |아니요 |예 |
| Dolby® Digital Plus (AC3 E) 위쪽 too7.1 |아니요 |예 |
| AAC (AAC-LC, AAC 그 및 AAC HEv2; too5.1 구성) |예 |예 |
| MPEG Layer 2 |아니요 |예 |
| MP3(MPEG-1 Audio Layer 3) |아니요 |예 |
| Windows Media 오디오 |아니요 |예 |

>[!NOTE]
>TooDolby를 인코딩할 경우® Digital (AC3) hello 출력 ISO MP4 파일에만 기록할 수 있습니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>관련 문서
* [미디어 인코더 표준 사전 설정을 사용자 지정하여 고급 인코딩 작업 수행](media-services-custom-mes-presets-with-dotnet.md)
* [할당량 및 제한 사항](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
