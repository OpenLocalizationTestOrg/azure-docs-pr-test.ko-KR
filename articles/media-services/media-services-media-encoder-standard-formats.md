---
title: "aaaMedia 인코더 표준 형식 및 코덱을"
description: "이 항목에서는 미디어 인코더 표준 형식 및 코덱에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>미디어 인코더 표준 형식 및 코덱
이 문서에는 hello 가장 일반적인 가져오기 및 미디어 인코더 표준 함께 사용할 수 있는 내보내기 파일 형식 목록이 포함 되어 있습니다.

## <a name="input-containerfile-formats"></a>입력 컨테이너/파일 형식
| 파일 형식(파일 확장명) | 지원됨 |
| --- | --- | --- | --- |
| FLV(H.264 및 AAC 코덱 포함)(.flv) |예 |
| MXF(.mxf) |예 |
| GXF(.gxf) |예 |
| MPEG2-PS, MPEG2-TS, 3GP(.ts, .ps, .3gp, .3gpp, .mpg) |예 |
| WMV(Windows Media Video)/ASF(.wmv, .asf) |예 |
| AVI(압축되지 않은 8비트/10비트)(.avi) |예 |
| MP4(.mp4, .m4a, .m4v)/ISMV(.isma, .ismv) |예 |
| [DVR-MS(Microsoft Digital Video Recording)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |예 |
| Matroska/WebM(.mkv) |예 |
| WAVE/WAV(.wav) |예 |
| QuickTime(.mov) |예 |

> [!NOTE]
> 위에 더 일반적으로 발생 하는 hello 파일 확장명의 목록이입니다. 미디어 인코더 표준은 여러 다른 확장명도 지원합니다(예: .m2ts, .mpeg2video, .qt). Tooencode 파일을 시도 하는 경우 지원 되지 않는 hello 형식에 대 한 오류 메시지가 피드백을 제공 해 [여기](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/)합니다.
> 
> 

### <a name="audio-formats-in-input-containers"></a>입력 컨테이너의 오디오 형식
미디어 인코더 표준 노트북 hello 오디오 형식이 입력된 컨테이너에서 다음을 지원 합니다.

* 인터리브 스테레오 오디오 또는 5.1 샘플을 포함하는 오디오 트랙이 있는 MXF, GXF 및 QuickTime 파일

또는

* 별도 PCM 트랙 같지만 hello 채널 매핑 hello 오디오 운반 MXF, GXF QuickTime 파일 (toostereo 또는 5.1) hello 파일 메타 데이터에서 추론할 수

명시적/사용자가 제공한 채널 매핑의 가까운 미래 hello에 제공 됩니다에 대 한 지 원하는 note 합니다.

## <a name="input-video-codecs"></a>입력 비디오 코덱
| 입력 비디오 코덱 | 지원됨 |
| --- | --- | --- | --- |
| AVC 8 비트/10-비트, AVCIntra를 포함 하 여 too4:2:2 |8비트 4:2:0 및 4:2:2 |
| Avid DNxHD(MXF) |예 |
| DVCPro/DVCProHD(MXF) |예 |
| DV(디지털 비디오)(AVI 파일) |예 |
| JPEG 2000 |예 |
| Mpeg-2 (too422 프로필 및 상위 수준을 비롯 하 여, 변형 XDCAM, XDCAM HD, XDCAM IMX, CableLabs® d 10 등) |Too422 프로필 |
| MPEG-1 |예 |
| VC-1/WMV9 |예 |
| Canopus HQ/HQX |아니요 |
| Mpeg-4 2부 |예 |
| [Theora](https://en.wikipedia.org/wiki/Theora) |예 |
| 압축되지 않은 YUV420 또는 mezzanine |예 |
| Apple ProRes 422 |예 |
| Apple ProRes 422 LT |예 |
| Apple ProRes 422 HQ |예 |
| Apple ProRes Proxy |예 |
| Apple ProRes 4444 |예 |
| Apple ProRes 4444 XQ |예 |

## <a name="input-audio-codecs"></a>입력 오디오 코덱
| 입력 오디오 코덱 | 지원됨 |
| --- | --- | --- | --- |
| AAC (AAC-LC, AAC 그 및 AAC HEv2; too5.1 구성) |예 |
| MPEG Layer 2 |예 |
| MP3(MPEG-1 Audio Layer 3) |예 |
| Windows Media 오디오 |예 |
| WAV/PCM |예 |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |예 |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |예 |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |예 |
| AMR(Adaptive Multi-Rate) |예 |
| AES(SMPTE 331M 및 302M, AES3-2003) |아니요 |
| Dolby® E |아니요 |
| Dolby® Digital(AC3) |아니요 |
| Dolby® Digital Plus(E-AC3) |아니요 |

## <a name="output-formats-and-codecs"></a>출력 형식 및 코덱
다음 표에서 hello 내보내기에 지원 되는 hello 코덱 및 파일 형식을 보여 줍니다.

| 파일 형식 | 비디오 코덱 | 오디오 코덱 |
| --- | --- | --- |
| MP4 <br/><br/>(다중 비트 전송률 MP4 컨테이너 포함) |H.264(High, Main 및 Baseline Profiles) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264(High, Main 및 Baseline Profiles) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[Azure 미디어 서비스로 주문형 콘텐츠 인코딩](media-services-encode-asset.md)

[방식으로 미디어 인코더 표준 tooencode](media-services-dotnet-encode-with-media-encoder-standard.md)

