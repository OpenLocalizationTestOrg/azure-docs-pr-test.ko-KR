---
title: "표준 인코더 스키마 aaaMedia | Microsoft Docs"
description: "hello 항목 hello 미디어 인코더 표준 스키마의 개요를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Media Encoder Standard 스키마
이 항목에서는에 hello 요소와 hello XML 스키마의 유형 중 일부를 설명 [미디어 인코더 표준 사전 설정](media-services-mes-presets-overview.md) 기반 합니다. hello 항목 설명은 요소와 유효한 값을 제공합니다. hello 전체 스키마를 나중에 게시 됩니다.  

## <a name="Preset"></a> 기본 설정(루트 요소)
인코딩 기본 설정을 정의합니다.  

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Encoding** |[Encoding](media-services-mes-schema.md#Encoding) |루트 요소 hello 입력된 소스 인코딩된 toobe 있음을 나타냅니다. |
| **Outputs** |[Outputs](media-services-mes-schema.md#Output) |원하는 출력 파일의 컬렉션입니다. |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **버전**<br/><br/> 필수 |**xs: decimal** |hello 미리 설정 된 버전입니다. hello 다음과 같은 제한 사항이: xs:fractionDigits 값 = "1"에서 xs:minInclusive value = "1" 예를 들어 **버전 = "1.0"**합니다. |

## <a name="Encoding"></a> Encoding
Hello 요소 다음의 시퀀스를 포함 합니다.  

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |H.264 비디오 인코딩 설정입니다. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |AAC 오디오 인코딩 설정입니다. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Bmp 이미지 설정입니다. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Png 이미지 설정입니다. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Jpg 이미지 설정입니다. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs: boolean** |현재는 1 패스 인코딩만 지원됩니다. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs: time** |Hello 고정 시간 (초) 단위로 IDR 프레임 사이의 간격을 결정 합니다. Tooas hello GOP 기간이 라고도합니다. 참조 **SceneChangeDetection** (아래 참조) 여부를 제어 hello에 대 한 인코더 벗어날 수에서이 값입니다. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default=”false” |**xs: boolean** |경우 집합 tootrue, 인코더 시도 toodetect 장면 hello 비디오에서 변경 하 고 IDR 프레임을 삽입 합니다. |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |컨트롤 사이의 절충 값 hello 속도 비디오 품질을 인코딩합니다. Hello 다음 값 중 하나일 수 있습니다: **속도**, **균형**, 또는 **품질**<br/><br/> 기본값: **Balanced** |
| **SyncMode**<br/><br/> minOccurs="0" | |향후 릴리스에서 공개될 기능입니다. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |출력 비디오 레이어의 컬렉션입니다. |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Condition** |**xs:string** | Hello 입력에 화면이 표시 되지 않음, tooforce hello 인코더 tooinsert 단색 비디오 트랙 할 수 있습니다. toodo 조건을 사용 하는 조건 또는 "InsertBlackIfNoVideoBottomLayerOnly" (tooinsert만 hello 가장 낮은 비트 전송률 비디오) = = "InsertBlackIfNoVideo" (tooinsert 모든 출력 비트 전송률로 비디오). 자세한 내용은 [이 항목](media-services-advanced-encoding-with-mes.md#no_video) 을 참조하세요.|

## <a name="H264Layers"></a> H264Layers

기본적으로 오디오와 비디오가 없는 포함 하는 입력된 toohello 인코더를 보낼 경우 hello 출력 자산 파일이 들어갑니다 오디오 데이터로. 일부 플레이어 못할 toohandle 이러한 출력 스트림 합니다. Hello H264Video를 사용할 수 있습니다 **InsertBlackIfNoVideo** 특성이 시나리오에서 tooforce hello 인코더 tooadd 비디오 트랙 toohello 출력을 설정 합니다. 자세한 내용은 [이 항목](media-services-advanced-encoding-with-mes.md#no_video) 을 참조하세요.
              
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |H264 레이어의 컬렉션입니다. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> 비디오 제한 hello에 설명 된 hello 값에 따라 [H264 수준](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) 테이블입니다.  
> 
> 

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **프로필**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** |Hello 다음 중 하나가 될 수 **xs: string** 값: **자동**, **초기**, **Main**, **높은**합니다. |
| **Level**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |이 비디오 레이어를 kbps로 지정에 사용 되는 hello 비트입니다. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |hello 최대 비트 전송률 비디오이 계층에서 kbps로 지정에 사용 합니다. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs: time** |Hello 비디오 버퍼의 길이입니다. |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Hello 출력 비디오 프레임의 픽셀에서 너비입니다.<br/><br/> 현재는 너비와 높이를 모두 지정해야 합니다. hello 너비와 높이 toobe 짝수 숫자가 필요 합니다. |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Hello 출력 비디오 프레임의 픽셀 단위에서 높이입니다.<br/><br/> 현재는 너비와 높이를 모두 지정해야 합니다. hello 너비와 높이 toobe 짝수 숫자가 필요 합니다.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |참조 프레임 사이의 B 프레임 수입니다. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |GOP의 참조 프레임 수입니다. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default=”Cabac” |**xs:string** |Hello 다음 값 중 하나일 수 있습니다: **Cabac** 및 **Cavlc**합니다. |
| **FrameRate**<br/><br/> minOccurs="0" |유리수입니다. |비디오 hello 출력의 hello 프레임 속도 결정합니다. 기본값은 "0/1" toolet hello 인코더 사용 하 여 hello 같은 프레임 속도 입력 hello로 비디오를 사용 합니다. 허용 되는 값은 예상된 toobe 일반적인 비디오 프레임 속도, 다음과 같습니다. 유효한 유리수는 모두 허용됩니다. 예를 들어 1/1은 1fps이고 사용할 수 있습니다.<br/><br/> - 12/1(12fps)<br/><br/> - 15/1(15fps)<br/><br/> - 24/1(24fps)<br/><br/> - 24000/1001(23.976fps)<br/><br/> - 25/1(25fps)<br/><br/>  - 30/1(30fps)<br/><br/> - 30000/1001(29.97fps) <br/> <br/>**참고** 다중 비트 전송률 인코딩 사전 설정을 사용자 지정을 만드는 경우 다음 모든 계층의 hello 사전 설정 **해야** 사용 하 여 hello 동일한 프레임 속도의 값입니다.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs: boolean** |Azure Media Encoder에서 복사합니다. |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |프레임이 분할되는 조각 수를 결정합니다. 기본값을 사용하는 것이 좋습니다. |

## <a name="AACAudio"></a> AACAudio
 Hello 요소 다음의 시퀀스를 포함 하 고 그룹화 합니다.  

 AAC에 대한 자세한 내용은 [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding)를 참조하세요.  

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **프로필**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Hello 다음 값 중 하나일 수 있습니다: **AACLC**, **HEAACV1**, 또는 **HEAACV2**합니다. |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce hello 인코더 tooproduce 입력에 오디오 없음 될 때 자동 오디오 트랙을 포함 하는 자산 hello "InsertSilenceIfNoAudio" 값을 지정 합니다.<br/><br/> 기본적으로 비디오 및 오디오 없음만 포함 하는 입력된 toohello 인코더를 전송 하면 hello 출력 자산 포함 됩니다만 비디오 데이터를 포함 하는 파일입니다. 일부 플레이어 못할 toohandle 이러한 출력 스트림 합니다. 이 시나리오에서이 설정을 tooforce hello 인코더 tooadd 자동 오디오 트랙 toohello 출력을 사용할 수 있습니다. |

### <a name="groups"></a>그룹
| 참조 | 설명 |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |설명을 참조 [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello 채널, 샘플링 속도 및 각 프로필에 대해 설정할 수 있는 비트 전송률의 적절 한 수입니다. |

## <a name="AudioGroup"></a> AudioGroup
각 프로필에 대 한 유효한 값에 대 한 세부 정보를 뒤에 오는 hello "오디오 코덱 details" 표를 참조 합니다.  

### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |hello 인코딩된 오디오 채널 수입니다. hello 다음은 사용할 수 있는 옵션: 1, 2, 5, 6, 8입니다.<br/><br/> 기본값: 2 |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |Hz에 지정 된 hello 오디오 샘플링 속도입니다. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |hello 비트 전송률 인코딩 hello 오디오, kbps로 지정 하는 경우 사용 합니다. |

### <a name="audio-codec-details"></a>오디오 코덱 세부 정보
오디오 코덱|세부 정보  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025 : 8 &lt;= 비트 전송률 &lt; 16<br/><br/> - 12000 : 8 &lt;= 비트 전송률 &lt; 16<br/><br/> - 16000 : 8 &lt;= 비트 전송률 &lt;32<br/><br/>- 22050 : 24 &lt;= 비트 전송률 &lt; 32<br/><br/> - 24000 : 24 &lt;= 비트 전송률 &lt; 32<br/><br/> - 32000 : 32 &lt;= 비트 전송률 &lt;= 192<br/><br/> - 44100 : 56 &lt;= 비트 전송률 &lt;= 288<br/><br/> - 48000 : 56 &lt;= 비트 전송률 &lt;= 288<br/><br/> - 88200 : 128 &lt;= 비트 전송률 &lt;= 288<br/><br/> - 96000 : 128 &lt;= 비트 전송률 &lt;= 288<br/><br/> 2:<br/><br/> - 11025 : 16 &lt;= 비트 전송률 &lt; 24<br/><br/> - 12000 : 16 &lt;= 비트 전송률 &lt; 24<br/><br/> - 16000 : 16 &lt;= 비트 전송률 &lt; 40<br/><br/> - 22050 : 32 &lt;= 비트 전송률 &lt; 40<br/><br/> - 24000 : 32 &lt;= 비트 전송률 &lt; 40<br/><br/> - 32000 :  40 &lt;= 비트 전송률 &lt;= 384<br/><br/> - 44100 : 96 &lt;= 비트 전송률 &lt;= 576<br/><br/> - 48000 : 96 &lt;= 비트 전송률 &lt;= 576<br/><br/> - 88200 : 256 &lt;= 비트 전송률 &lt;= 576<br/><br/> - 96000 : 256 &lt;= 비트 전송률 &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000 : 160 &lt;= 비트 전송률 &lt;= 896<br/><br/> - 44100 : 240 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 48000 : 240 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 88200 : 640 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 96000 : 640 &lt;= 비트 전송률 &lt;= 1024<br/><br/> 8:<br/><br/> - 32000 : 224 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 44100 : 384 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 48000 : 384 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 88200 : 896 &lt;= 비트 전송률 &lt;= 1024<br/><br/> - 96000 : 896 &lt;= 비트 전송률 &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050 : 비트 전송률 = 8<br/><br/> - 24000 : 8 &lt;= 비트 전송률 &lt;= 10<br/><br/> - 32000 : 12 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 44100 : 20 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 48000 : 20 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 88200 : 비트 전송률 = 64<br/><br/> 2:<br/><br/> - 32000 : 16 &lt;= 비트 전송률 &lt;= 128<br/><br/> - 44100 : 16 &lt;= 비트 전송률 &lt;= 128<br/><br/> - 48000 : 16 &lt;= 비트 전송률 &lt;= 128<br/><br/> - 88200 : 96 &lt;= 비트 전송률 &lt;= 128<br/><br/> - 96000 : 96 &lt;= 비트 전송률 &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000 : 64 &lt;= 비트 전송률 &lt;= 320<br/><br/> - 44100 : 64 &lt;= 비트 전송률 &lt;= 320<br/><br/> - 48000 : 64 &lt;= 비트 전송률 &lt;= 320<br/><br/> - 88200 : 256 &lt;= 비트 전송률 &lt;= 320<br/><br/> - 96000 : 256 &lt;= 비트 전송률 &lt;= 320<br/><br/> 8:<br/><br/> - 32000 : 96 &lt;= 비트 전송률 &lt;= 448<br/><br/> - 44100 : 96 &lt;= 비트 전송률 &lt;= 448<br/><br/> - 48000 : 96 &lt;= 비트 전송률 &lt;= 448<br/><br/> - 88200 : 384 &lt;= 비트 전송률 &lt;= 448<br/><br/> - 96000 : 384 &lt;= 비트 전송률 &lt;= 448  
**HEAACV2**|2:<br/><br/> - 22050 : 8 &lt;= 비트 전송률 &lt;= 10<br/><br/> - 24000 : 8 &lt;= 비트 전송률 &lt;= 10<br/><br/> - 32000 : 12 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 44100 : 20 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 48000 : 20 &lt;= 비트 전송률 &lt;= 64<br/><br/> - 88200 : 64 &lt;= 비트 전송률 &lt;= 64  
  

## <a name="Clip"></a> Clip
### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **StartTime** |**xs:duration** |프레젠테이션의 hello 시작 시간을 지정합니다. StartTime 값 hello toomatch hello 절대의 타임 스탬프 hello 입력된 비디오가 필요합니다. 예를 들어 hello hello 입력된 비디오의 첫 번째 프레임에 12:00:10.000의 타임 스탬프 경우 StartTime 보다 길거나 같아야 12:00:10.000 큽니다. |
| **Duration** |**xs:duration** |프레젠테이션의 (예를 들어 hello 비디오에서 오버레이가의 모양) hello 기간을 지정 합니다. |

## <a name="Output"></a> Output
### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **FileName** |**xs:string** |hello hello 출력 파일 이름입니다.<br/><br/> Hello 테이블 toobuild hello 출력 파일 이름 다음에 설명 된 매크로 사용할 수 있습니다. 예:<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Macros
| 매크로 | 설명 |
| --- | --- |
| **{Basename}** |VoD 인코딩을 수행 하는 경우 hello {Basename} hello hello 입력된 자산에 주 파일의 hello AssetFile.Name 속성의 처음 32 자 hello 됩니다.<br/><br/> 라이브 보관 hello 입력된 자산을 사용 하는 경우 다음 hello {Basename}에서 파생 됩니다 hello 서버 매니페스트에 hello trackName 특성. 와 같이 TopBitrate, hello를 사용 하는 하위 클립 작업을 제출 하는 경우: "< VideoStream\>TopBitrate < / VideoStream\>", hello 출력 파일에는 비디오를 포함 하 고 다음 hello {Basename}의 hello hello trackName의 처음 32 자 hello은 hello 가장 높은 비트 전송률 비디오 계층입니다.<br/><br/> 대신 사용 하 여 모든 비트 전송률 입력된 hello와 같은 하위 클립 작업을 제출 하는 경우 "< VideoStream\>* < / VideoStream\>", hello 출력 파일에는 비디오를 포함 하 고 다음 {Basename}는 hello 먼저의 hello trackName의 32 자 hello 해당 비디오 계층입니다. |
| **{Codec}** |너무 매핑합니다 "H264" 비디오 및 오디오에 대 한 "AAC"입니다. |
| **{Bitrate}** |hello 대상 비디오 비트 전송률 비디오 및 오디오, hello 출력 파일에 포함 되어 있거나 대상 오디오 비트 전송률 hello 파일을 출력 하는 경우 포함 되어 오디오에만 있으면 됩니다. 사용 되는 hello 값에는 kbps에서 hello 비트 전송률입니다. |
| **{Channel}** |Hello 파일 오디오 있으면 오디오 채널 수입니다. |
| **{Width}** |Hello 비디오, hello 출력 파일에 픽셀 단위에서 hello 파일 비디오를 포함 하는 경우의 너비입니다. |
| **{Height}** |Hello 비디오, hello 출력 파일에 픽셀 단위에서 hello 파일 비디오를 포함 하는 경우의 높이입니다. |
| **{Extension}** |Hello hello 출력 파일에 대 한 "Type" 속성에서에서 상속합니다. hello 출력 파일 이름에는 하나는 확장명은의: "mp4", "ts", "jpg", "png" 또는 "bmp"입니다. |
| **{Index}** |미리 보기의 경우 필수 항목입니다. 한 번만 존재해야 합니다. |

## <a name="Video"></a> Video(Codec에서 상속되는 복합 형식)
### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **시작** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs: boolean** |에 대 한 자세한 내용은 다음 단원을 hello 참조: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
해상도 값 백분율 측면에서 표현으로 조합 하 여 toouse hello PreserveResolutionAfterRotation 플래그 것이 좋습니다 (너비 = "100%", 높이 = "100%").  

기본적으로 hello hello 사전 설정 미디어 인코더 표준 MES ()을 대상으로 0도 회전 된 비디오 해상도 설정 (너비, 높이) 인코드 합니다. 예를 들어 입력된 비디오 0도 회전 된 1280 x 720이 다음 hello 기본 사전 설정에 있는지 확인 hello 출력 hello 해상도 동일 합니다. 아래 그림을 참조하세요.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

그러나이 의미 하는 hello 입력된 비디오를 0이 아닌 순환으로 캡처 되었습니다 (예:. 스마트폰 또는 태블릿 보유 세로로), 적용 된 후 기본적으로는 MES hello 적용 됩니다 해상도 설정 (너비, 높이) toohello 비디오에서는 입력 하 고 다음 hello 회전에 대 한 보정을 인코딩합니다. 예를 들어 아래 hello 그림을 참조 하십시오. hello 사전 설정을 사용 하 여 너비 = "100%", 높이 = hello 출력 toobe 1280 픽셀 너비 및 높이가 720 픽셀 필요한 것으로 해석 하는 MES "100%"입니다. Hello 비디오를 회전 후 다음 축소 hello 그림 toofit 해당 창으로 toopillar 입력란 영역 hello에 앞에 왼쪽 및 오른쪽입니다.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

위의 hello 하지 hello 필요한 동작 경우 너무 "true"로 설정 하 고 hello PreserveResolutionAfterRotation 플래그의 사용 하 여 만들 수 있습니다 (기본값은 "false"). 따라서 경우에 미리 설정 된 너비는 "100%", 높이 = = "100%" 및 PreserveResolutionAfterRotation 설정 너무 "true", 1280 픽셀 너비 및 높이 (90도 회전) 720 픽셀은 입력된 비디오가 0도 회전 하지만 720 픽셀 너비와 1280 인 출력을 생성 합니다 높이가 픽셀입니다. 아래 hello 그림을 참조 하십시오.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup(그룹)
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |유효한 값: 1(최저)-100(최고) |

### <a name="attributes"></a>특성
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage(Video에서 상속되는 복합 형식)
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="JpgImage"></a> JpgImage(Video에서 상속되는 복합 형식)
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="PngImage"></a> PngImage(Video에서 상속되는 복합 형식)
### <a name="elements"></a>요소
| 이름 | 형식 | 설명 |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="examples"></a>예
이 스키마에 기반하여 작성된 XML 기본 설정 예제를 보려면 [MES(Media Encoder Standard)의 작업 기본 설정](media-services-mes-presets-overview.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

