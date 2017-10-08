---
title: "미디어 인코더 표준-Azure와 aaaHow toocrop 비디오 | Microsoft Docs"
description: "이 문서에서는 어떻게 toocrop 비디오를 미디어 인코더 표준입니다."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a>미디어 인코더 표준으로 비디오 자르기
입력의 비디오 toocrop 미디어 인코더 표준 MES ()를 사용할 수 있습니다. 자르기 직사각형 창은 hello 비디오 프레임 내에서 선택 하 고 해당 창 내의 hello 픽셀 방금 인코딩 hello 과정은 합니다. 다음 다이어그램 hello hello 과정을 보여 줍니다 수 있습니다.

![비디오 자르기](./media/media-services-crop-video/media-services-crop-video01.png)

비디오 1920 x 1080 픽셀이 고 (16:9 가로 세로 비율) 해상도 되었지만 검정 막대 (pillar 상자) hello에 왼쪽 및 오른쪽으로, 4:3 창이 나 1440 x 1080 픽셀이 고 활성 비디오 포함 되도록 하는 입력으로 있다고 가정 합니다. MES toocrop를 사용 하 여 또는 편집 hello 검은 막대 아웃 하 고 hello 1440 x 1080 지역 인코딩합니다.

MES에 자르기 되므로 전 전처리 단계 hello 인코딩 사전 설정 hello 자르기 매개 변수 toohello 원래 입력된 비디오를 적용 합니다. 후속 단계 인코딩이 및 hello 너비/높이 설정은 적용 toohello *미리 처리* 비디오 및 toohello 원본 비디오 하지 않습니다. Toodo hello 다음 필요한 사전 설정 디자인할 때: (a) hello 원본 입력된 비디오를 기반으로 hello 자르기 매개 변수를 선택 하 고 (b) 선택 하면 인코딩 설정을 비디오 자를 hello에 따라 합니다. 일치 하지 않으면 사용자 설정 toohello 자를 비디오를 인코딩할 예상 대로 hello 출력 되지 것입니다.

hello [다음](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) 항목 toocreate MES 사용 하는 인코딩 작업 및 방법 toospecify 사용자 지정 사전 설정을 hello 인코딩 작업 방법을 보여 줍니다. 

## <a name="creating-a-custom-preset"></a>사용자 지정 사전 설정 만들기
Hello 다이어그램에 표시 된 hello 예제:

1. 원본 입력은 1920x1080입니다.
2. 가운데 hello 입력된 프레임에 표시 되는 1440 x 1080 tooan 출력 자를 toobe 필요한
3. 즉, X 오프셋은 (1920 – 1440)/2 = 240이고 Y 오프셋은 0입니다.
4. hello 너비 및 hello 자르기 사각형의 높이 1440 1080, 각각 및
5. Hello에 인코드 단계, hello는 tooproduce 3 계층, 해상도, 1440 x 1080 960 x 720 및 480 x 360은 각각

### <a name="json-preset"></a>JSON 사전 설정
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


## <a name="restrictions-on-cropping"></a>자르기에 대한 제한 사항
기능 자르기 hello toobe 수동을 것입니다. 해야 tooload 입력 비디오에 관심 있는 프레임을 선택, 자르기 직사각형 hello에 대 한 hello 커서 toodetermine 오프셋 위치 수 있는 적합 한 편집 도구, toodetermine hello는 해당 특정 비디오 등에 대 한 조정 하는 인코딩 사전 설정입니다. 이 기능은 tooenable 등을 고려 하지 않은: 자동 검색 및 비디오 입력에서 검은색 letterbox/pillarbox 테두리를 제거 합니다.

다음과 같은 제약 조건을 기능 자르기 toohello를 적용 됩니다. Hello 인코딩 작업이 충족 되지 않는 경우 실패 하거나 예기치 않은 출력 생성할 수 있습니다.

1. hello 좌표 및 hello 자르기 사각형의 크기는 hello 입력된 비디오 내 toofit
2. 위에서 설명 했 듯이 hello 너비 및 높이 hello에 인코딩 설정을 비디오 자를 toocorrespond toohello 했습니다
3. 자르기 가로 모드 (즉, 해당 없음 toovideos 기록 세로로 보유 스마트폰 또는 세로 모드)에서 캡처된 toovideos 적용 됩니다.
4. 정사각형 픽셀로 캡처된 프로그레시브 비디오에서 가장 잘 작동합니다.

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>다음 단계
Azure 미디어 서비스 학습 경로 toohelp AMS에서 제공 하는 뛰어난 기능에 대 한 자세한 내용은 참조 하십시오.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
