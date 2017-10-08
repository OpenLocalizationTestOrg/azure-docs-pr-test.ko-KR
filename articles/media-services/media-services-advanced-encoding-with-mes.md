---
title: "MES 사전 설정 사용자 지정 하 여 인코딩 aaaPerform 고급 | Microsoft Docs"
description: "이 항목에서는 tooperform 고급 미디어 인코더 표준 태스크 사전 설정 사용자 지정 하 여 인코딩을 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>MES 사전 설정을 사용자 지정하여 고급 인코딩 수행 

## <a name="overview"></a>개요

이 항목에서는 미디어 인코더 표준 toocustomize 사전 설정 하는 방법을 보여 줍니다. hello [미디어 인코더 표준 사용자 지정 사전 설정을 사용 하 여 인코딩을](media-services-custom-mes-presets-with-dotnet.md) toouse.NET toocreate 인코딩 작업 하는 방법 및이 작업을 실행 하는 작업 항목을 보여 줍니다. 공급 hello 사용자 지정 사전 설정 toohello 인코딩 작업 사전 설정 사용자 지정 하면 됩니다. 

>[!NOTE]
>XML 사전 설정을 사용 하 여, 확인 되었는지 toopreserve hello 요소 순서를 아래 XML 예제에 나와 있는 것 처럼 (예를 들어 KeyFrameInterval 붙여야 SceneChangeDetection).
>

이 항목에서는 hello 다음 인코딩 작업을 수행 하는 hello 사용자 지정 사전 설정은 보여 줍니다.

## <a name="support-for-relative-sizes"></a>상대적 크기에 대한 지원

축소판 이미지를 생성 하는 경우 불필요 tooalways 출력 너비와 높이 픽셀 단위로 지정 합니다. Hello 범위 [1%, …, 100%]에서 백분율로 지정할 수 있습니다.

### <a name="json-preset"></a>JSON 사전 설정
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>XML 사전 설정
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>미리 보기 생성

이 섹션에서는 어떻게 toocustomize 미리 보기를 생성 하는 사전 설정입니다. hello 아래에 정의 된 사전 설정 정보가 포함 tooencode 하려는 방법에 파일 뿐만 아니라 필요한 정보를 toogenerate 미리 보기 됩니다. 문서화 된 hello MES 사전 설정에 사용할 수 있는 있습니다 [이](media-services-mes-presets-overview.md) 섹션을 미리 보기를 생성 하는 코드를 추가 합니다.  

> [!NOTE]
> hello **SceneChangeDetection** 설정을 hello 미리 설정 된 다음에 설정할 수 있습니다 tootrue tooa 단일 비트 전송률 비디오를 인코딩하는 경우. Tooa 다중 비트 전송률을 인코딩하는 경우 비디오 및 설정 **SceneChangeDetection** tootrue, hello 인코더에서 오류를 반환 합니다.  
>
>

스키마에 대한 자세한 내용은 [이 항목](media-services-mes-schema.md) 을 참조하세요.

있는지 tooreview hello 확인 [고려 사항](#considerations) 섹션.

### <a id="json"></a>JSON 사전 설정
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


### <a id="xml"></a>XML 사전 설정
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

### <a name="considerations"></a>고려 사항

hello 고려 사항에 따라 적용 됩니다.

* 시작/단계/범위에 대 한 명시적 타임 스탬프의 hello 사용 해당 hello 입력된 소스 1 분 이상 오래을 가정 합니다.
* Jpg/Png/BmpImage 요소에는 Start, Step 및 Range 문자열 특성이 있으며, 이러한 특성은 다음과 같이 해석될 수 있습니다.

  * 음수가 아닌 정수인 경우 프레임 번호(예: "Start": "120")
  * 상대 toosource 기간 % 접미사로으로 표시 되는 경우 예를 들어 "Start": "15%", 또는
  * HH:MM:SS... 형식으로 표현되는 경우 타임스탬프(예: "Start" : "00:01:00")

    표기법을 원하는 대로 혼용하거나 일치시킬 수 있습니다.

    시작 특수 매크로 지원 되는 또한: {최고}, toodetermine hello 첫 번째 "흥미로운" 프레임 참고 hello 콘텐츠의 시도: (단계 및 범위 시작 너무 설정 된 경우 무시 됩니다 {최상의})
  * 기본값: Start:{Best}
* 출력 형식 필요한 각 이미지 형식에 대해 명시적으로 제공 된 toobe: Jpg/Png/BmpFormat 합니다. 있는 경우 MES JpgVideo tooJpgFormat이 등과 일치 합니다. 새 이미지 코덱 특정 매크로 소개: {인덱스로} 요구 toobe 있는 (한 번만 한 번)에 있는 이미지 출력 형식의 합니다.

## <a id="trim_video"></a>비디오 자르기(클리핑)
Hello 인코더를 수정 하는 방법에 대 한이 섹션에서는 설명 tooclip 미리 설정 또는 trim hello 입력된 비디오 hello 입력은 소위 중 2 층 파일이 나 요청 시 파일입니다. 이 대 한 hello 세부 정보에서 사용할 수 있는 – hello 인코더도 사용 되는 tooclip 하거나 수 trim을 캡처하거나에서 라이브 스트림을 보관 하는 한 자산의 [이 블로그](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/)합니다.

tootrim 비디오를 있습니다 사용할 수 있는 문서화 hello MES 사전 설정 [이](media-services-mes-presets-overview.md) 섹션 및 hello 수정 **소스** 요소 중 (아래 참조). StartTime 값 hello toomatch hello 절대의 타임 스탬프 hello 입력된 비디오가 필요합니다. 예를 들어 hello hello 입력된 비디오의 첫 번째 프레임에 12:00:10.000의 타임 스탬프 경우 StartTime 보다 길거나 같아야 12:00:10.000 이상에 있습니다. Hello 아래의 예제에서는 hello 입력 비디오 0의 시작 타임 스탬프에 가정 합니다. **소스** hello 사전 설정의 hello 시작 부분에 배치 해야 합니다.

### <a id="json"></a>JSON 사전 설정
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

### <a name="xml-preset"></a>XML 사전 설정
tootrim 비디오를 있습니다 사용할 수 있는 문서화 hello MES 사전 설정 [여기](media-services-mes-presets-overview.md) hello 수정 **소스** 요소 중 (아래 참조).

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

## <a id="overlay"></a>오버레이 만들기

미디어 인코더 표준 hello toooverlay를 기존 비디오, 이미지 수 있습니다. 현재 형식에 따라 hello 지원 됩니다: png, jpg, gif, bmp 및 합니다. hello 아래에 정의 된 미리 설정 된 경우 비디오 오버레이가의 기본 예제에서는

또한 toodefining 사전 설정된 파일을 갖게 알고 toolet 미디어 서비스 hello 자산에는 파일은 hello 오버레이 이미지와 toooverlay hello 이미지에 원하는 hello 원본 비디오 파일이 됩니다. hello 비디오 파일에 toobe hello **기본** 파일입니다.

.NET을 사용 하는 경우 추가 toohello.NET 예제에 정의 된 두 개의 함수를 수행 하는 hello [이](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) 항목입니다. hello **UploadMediaFilesFromFolder** 함수 (예를 들어 BigBuckBunny.mp4 및 Image001.png) 폴더에서 파일을 업로드 하 고 집합 hello mp4 파일 toobe hello에에서 주 파일 hello 자산입니다. hello **EncodeWithOverlay** 함수 hello 사용자 지정 미리 설정 된 전달 된 파일을 tooit를 사용 하 여 (예를 들어 hello 미리 설정 된 해당 다음과) toocreate hello 인코딩 작업 합니다.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
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
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> 현재 제한 사항:
>
> hello 오버레이 불투명도 설정이 지원 되지 않습니다.
>
> 프로그램 소스 비디오 파일 및 hello 오버레이 이미지 파일 같은 자산의 hello 및 비디오 파일 요구 toobe 집합이이 자산에 hello 주 파일로 hello에 toobe 배포 해야 합니다.
>
>

### <a name="json-preset"></a>JSON 사전 설정
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


### <a name="xml-preset"></a>XML 사전 설정
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


## <a id="silent_audio"></a>입력에 오디오가 없을 때 조용한 오디오 트랙 삽입
기본적으로 비디오 및 오디오 없음만 포함 하는 입력된 toohello 인코더를 보낼 경우 hello 출력 자산이 포함만 비디오 데이터를 포함 하는 파일입니다. 일부 플레이어 못할 toohandle 이러한 출력 스트림 합니다. 이 시나리오에서이 설정을 tooforce hello 인코더 tooadd 자동 오디오 트랙 toohello 출력을 사용할 수 있습니다.

tooforce hello 인코더 tooproduce 입력에 오디오 없음 될 때 자동 오디오 트랙을 포함 하는 자산 hello "InsertSilenceIfNoAudio" 값을 지정 합니다.

Hello에 문서화 되어 MES 사전 설정을 사용할 수 있는 [이](media-services-mes-presets-overview.md) 섹션을 선택한 다음 수정 하는 hello 확인:

### <a name="json-preset"></a>JSON 사전 설정
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>XML 사전 설정
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>자동 디인터레이스 사용 안 함
고객 필요 하지 않습니다 toodo 아무 것도 자동으로 취소 인터레이스 콘텐츠 toobe 인터레이스 hello 같은 될 경우. MES hello지 않습니다 (기본값) hello hello 자동 디인터레이스 켜져 있을 때 자동으로 인터레이스된 프레임을 검색 하 고 인터레이스된로 표시 된 프레임을 해제 interlaces만 합니다.

해제 hello 자동 디인터레이스를 해제할 수 있습니다. 이 옵션은 권장되지 않습니다.

### <a name="json-preset"></a>JSON 사전 설정
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>XML 사전 설정
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>오디오 전용 사전 설정
이 섹션에서는 AAC 오디오 및 AAC 고급 품질 오디오라는 두 개의 오디오 전용 MES 사전 설정을 설명합니다.

### <a name="aac-audio"></a>AAC 오디오
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

### <a name="aac-good-quality-audio"></a>AAC 고급 음질 오디오
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

## <a id="concatenate"></a>둘 이상의 비디오 파일 연결

hello 다음 예제에서는 미리 설정 된 tooconcatenate 두를 생성 하는 방법 또는 더 많은 비디오 파일입니다. hello 가장 일반적인 시나리오는 헤더 나 트레일러 toohello 주 비디오 tooadd 하려는 경우입니다. hello는 hello 비디오 파일 함께 편집 중인 속성 (비디오 해상도, 프레임 속도, 오디오 트랙 수 등)을 공유 하는 경우 사용 하는 것입니다. Toomix 비디오 또는 오디오 트랙 수가 서로 다르므로 서로 다른 프레임 속도의 하지 주의 해야 합니다.

>[!NOTE]
>hello hello 연결 기능의 현재 설계에서는 해당 hello 입력 비디오 클립 해상도, 측면에서 일관성이 프레임 속도 등입니다. 

### <a name="requirements-and-considerations"></a>요구 사항 및 고려 사항

* 입력 비디오에는 오디오 트랙이 하나만 있어야 합니다.
* 입력 비디오 hello 해야 동일한 프레임 속도입니다.
* 비디오를 별도 자산에 업로드 하 고 각 자산에 hello 주 파일로 hello 비디오를 설정 해야 합니다.
* 비디오의 tooknow hello 기간이 필요합니다.
* hello 아래 미리 설정 된 예제 가정 0의 타임 스탬프를 갖는 모든 hello 입력된 비디오를 시작 합니다. 값이 필요 하면 toomodify hello StartTime hello 비디오 시작 타임 스탬프 있으면 경우 일반적으로 hello와 마찬가지로 라이브 보관 합니다.
* hello JSON 사전 설정을 사용 하면 명시적 참조 hello 입력 자산의 AssetID 값 toohello 있습니다.
* hello 샘플 코드는 JSON 사전 설정 하는 hello tooa 로컬 파일 "C:\supportFiles\preset.json"와 같은 저장 된 가정 합니다. 또한 파악 하는 hello 결과 AssetID 값 및 두 개의 비디오 파일을 업로드 하 여 두 개의 자산을 만들었다고 가정 합니다.
* 코드 조각 및 JSON hello 미리 설정 된 두 개의 비디오 파일을 연결 하는 모양의 예제가 나와 있습니다. 가 두 개의 동영상 보다 toomore를 확장할 수 있습니다.

  1. 호출 작업입니다. InputAssets.Add() 반복 해 서 tooadd 순서로 추가 비디오.
  2. Hello에 더 많은 항목을 추가 하 여 hello JSON의에서 "원본" toohello 요소 편집에 해당 하기 순서가 동일 합니다.

### <a name="net-code"></a>.NET 코드

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>JSON 사전 설정

사용자 지정 tooconcatenate, 원하는 hello 자산 id를 가진 및 각 비디오에 대 한 hello 적절 한 시간 세그먼트와 사전 설정을 업데이트 합니다.

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

## <a id="crop"></a>미디어 인코더 표준으로 비디오 자르기
Hello 참조 [비디오 미디어 인코더 표준를 자르려면](media-services-crop-video.md) 항목입니다.

## <a id="no_video"></a>입력에 비디오가 없을 때 비디오 트랙 삽입

기본적으로 오디오와 비디오가 없는 포함 하는 입력된 toohello 인코더를 보낼 경우 hello 출력 자산이 포함만 오디오 데이터를 포함 하는 파일입니다. Azure 미디어 플레이어를 포함 하 여 일부 플레이어 (참조 [이](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) 하지 못할 수 toohandle 이러한 스트림에서 합니다. 이 시나리오에서이 설정을 tooforce hello 인코더 tooadd 단색 비디오 트랙 toohello 출력을 사용할 수 있습니다.

> [!NOTE]
> Hello 인코더 tooinsert 강제로 hello에 대 한 출력 비디오 트랙 증가 hello 크기 출력 자산을 되 고 있으므로 발생 한 인코딩 작업 hello에 대 한 비용을 hello 합니다. Tooverify 테스트를 실행 해야 결과이 처럼 증가 사용자의 월별 요금에만 적당 한 영향을 줍니다.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>만 hello 가장 낮은 비트 전송률 비디오를 삽입

와 같은 미리 설정 된 다중 비트 전송률 인코딩 사용 하는 경우를 가정해 볼 ["H264 다중 비트 전송률 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode 전체 스트리밍에 대 한 다양 한 비디오 파일 및 오디오 전용 파일을 포함 하는 카탈로그를 입력 합니다. 이 시나리오에서는 때 hello 입력 비디오가 없는 수도 있습니다 tooforce hello 인코더 tooinsert 비디오는 단색으로 모든 출력 비트 전송률 비디오 것과 반대로 tooinserting 방금 hello 가장 낮은 비트 전송률을 추적 합니다. tooachieve이 toouse hello 해야 **InsertBlackIfNoVideoBottomLayerOnly** 플래그입니다.

Hello에 문서화 되어 MES 사전 설정을 사용할 수 있는 [이](media-services-mes-presets-overview.md) 섹션을 선택한 다음 수정 하는 hello 확인:

#### <a name="json-preset"></a>JSON 사전 설정
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML 사전 설정

XML을 사용 하는 경우 조건을 사용 하 여 "InsertBlackIfNoVideoBottomLayerOnly" 특성 toohello로 = **H264Video** 요소와 조건 = "InsertSilenceIfNoAudio" 특성으로 너무**AACAudio**합니다.

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

### <a name="inserting-video-at-all-output-bitrates"></a>모든 출력 비트 전송률에서 비디오 삽입
와 같은 미리 설정 된 다중 비트 전송률 인코딩 사용 하는 경우를 가정해 볼 ["H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode 전체 스트리밍에 대 한 다양 한 비디오 파일 및 오디오 전용 파일을 포함 하는 카탈로그를 입력 합니다. 이 시나리오에서는 때 hello 입력 비디오가 없는 수도 있습니다 tooforce hello 인코더 tooinsert 모든 hello 출력 비트 전송률로 단색 비디오를 추적 합니다. 이렇게 하면 출력 자산은 비디오 트랙 및 오디오 트랙의 존중 toonumber와 유형이 같은 모든 합니다. tooachieve이 toospecify hello "InsertBlackIfNoVideo" 플래그를 해야 합니다.

Hello에 문서화 되어 MES 사전 설정을 사용할 수 있는 [이](media-services-mes-presets-overview.md) 섹션을 선택한 다음 수정 하는 hello 확인:

#### <a name="json-preset"></a>JSON 사전 설정
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>XML 사전 설정

XML을 사용 하는 경우 조건을 사용 하 여 "InsertBlackIfNoVideo" 특성 toohello로 = **H264Video** 요소와 조건 = "InsertSilenceIfNoAudio" 특성으로 너무**AACAudio**합니다.

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

## <a id="rotate_video"></a>비디오 회전
hello [미디어 인코더 표준](media-services-dotnet-encode-with-media-encoder-standard.md) 회전 각도 0/90/180/270의를 지원 합니다. hello 기본 동작은 "자동", hello 들어오는 비디오 파일의 toodetect hello 회전 메타 데이터를 시도 하 고 그에 대 한 보정 합니다. Hello 다음이 포함 **소스** hello 사전 설정에 정의 된 요소 tooone [이](media-services-mes-presets-overview.md) 섹션:

### <a name="json-preset"></a>JSON 사전 설정
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
### <a name="xml-preset"></a>XML 사전 설정
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

참고: [이](media-services-mes-schema.md#PreserveResolutionAfterRotation) 회전 보정 트리거될 때 hello 인코더 hello에 hello 너비와 높이 설정을 해석 하는 방법을 대 한 자세한 내용은 항목 미리 설정 합니다.

Hello 입력된 비디오에 있는 경우 hello 값 "0" tooindicate toohello 인코더 tooignore 회전 메타 데이터를 사용할 수 있습니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[미디어 서비스 인코딩 개요](media-services-encode-asset.md)
