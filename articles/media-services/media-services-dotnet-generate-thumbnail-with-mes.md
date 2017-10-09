---
title: "미디어 인코더 표준.NET과 함께 사용 하 여 aaaHow toogenerate 미리 보기"
description: "이 항목에서는 방법을 toouse.NET tooencode 자산 hello에 대 한 미리 보기 생성 및 사용 하 여 미디어 인코더 표준 동시 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a>어떻게 미디어 인코더 표준.NET과 함께 사용 하 여 toogenerate 미리 보기

사용자 입력의 비디오에서 하나 이상의 미리 보기 미디어 인코더 표준 toogenerate를 사용할 수 [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), 또는 [BMP](https://en.wikipedia.org/wiki/BMP_file_format) 이미지 파일 형식입니다. 이미지를 생성하는 작업을 제출하거나 미리 보기 생성을 인코딩과 결합할 수 있습니다. 이 항목에는 이런 시나리오를 위해 몇 가지 예제 XML 및 JSON 미리 보기 사전 설정을 제공합니다. Hello hello 항목의 끝에는 한 [샘플 코드](#code_sample) toouse hello 미디어 서비스.NET SDK tooaccomplish 인코딩 작업을 hello 하는 방법을 보여 주는 합니다.

샘플 사전 설정에 사용 되는 hello 요소에 대 한 자세한 내용은 검토 해야 [미디어 인코더 표준 스키마](media-services-mes-schema.md)합니다.

있는지 tooreview hello 확인 [고려 사항](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) 섹션.

## <a name="example--single-png-file"></a>예 – 단일 PNG 파일

다음 JSON hello 및 XML 사전 설정을 사용 하는 tooproduce 단일 출력 PNG 파일 hello에서 처음 몇 수 hello 인코더의 "흥미로운" 프레임을 찾는 시도 하는 최상의 노력 하면 여기서 hello 입력된 비디오의 초입니다. Note는 hello 출력 이미지 크기를 설정한 too100%, 즉이 hello 입력된 비디오의 hello 크기와 일치 합니다. "출력" hello "형식" 설정이 필요한 어떤가요도 참고 "PngLayers" hello "코덱" 섹션에서 toomatch hello 사용 합니다. 

### <a name="json-preset"></a>JSON 사전 설정

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML 사전 설정

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a>예 – 일련의 JPEG 이미지

다음 JSON hello 및 XML 사전 설정을 사용 하는 tooproduce 일련의 5%의 타임 스탬프에서 10 이미지 될 수 있습니다 15%, …, 여기서 hello 이미지 크기는 지정 된 toobe hello 비디오를 입력 하는 1/4 hello 입력된 타임 라인의 95%입니다.

### <a name="json-preset"></a>JSON 사전 설정

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a>XML 사전 설정
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a>예 – 특정 타임스탬프의 1개 이미지

hello 다음 JSON과 XML 사전 설정을 사용 하는 tooproduce hello 입력된 비디오의 hello에 단일 JPEG 이미지 30 초 표시 될 수 있습니다. 이 사전 설정에서는 hello 입력된 toobe 지속 시간이 30 초 이상 (다른 hello 작업이 실패 합니다.).

### <a name="json-preset"></a>JSON 사전 설정

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a>XML 사전 설정
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a id="code_sample"></a>예 – 동영상 인코드 및 미리 보기 생성

다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.

* 인코딩 작업을 만듭니다.
* 참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.
* 부하 hello 사전 설정 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) hello 뿐만 아니라 필요한 정보를 toogenerate 축소판 그림 미리 설정 된 인코딩을 포함 하는 합니다. 이 저장할 수 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) 파일 및 사용 하 여 hello 다음 코드 tooload hello 파일에에서 있습니다.
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* 인코딩 작업의 단일 toohello 작업을 추가 합니다. 
* Hello 입력 지정 인코딩된 자산 toobe 합니다.
* Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.
* 이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.
* Hello 작업을 제출 합니다.

Hello 참조 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md) 방법에 대 한 지침은 항목 tooset 개발 환경 구성 합니다.

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from hello App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
            }

            private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
            {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
                case JobState.Canceled:
                case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
                default:
                break;
            }
            }

            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
            }
        }
        }

## <a id="json"></a>미리 보기 JSON 기본 설정
스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.

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
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
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
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="xml"></a>미리 보기 XML 기본 설정
스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.
    
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
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a>고려 사항
hello 고려 사항에 따라 적용 됩니다.

* 시작/단계/범위에 대 한 명시적 타임 스탬프의 hello 사용 해당 hello 입력된 소스 1 분 이상 오래을 가정 합니다.
* Jpg/Png/BmpImage 요소에는 시작, 단계, 범위 문자열 특성이 있으며, 이러한 특성은 다음과 같이 해석될 수 있습니다.
  
  * 음수가 아닌 정수인 경우 프레임 번호, 예: "Start": "120",
  * 예: % 접미사로로 표시 하는 경우 상대 toosource 기간입니다. "Start": "15%", OR
  * HH:MM:SS... 형식. 예: "Start" : "00:01:00"
    
    표기법을 원하는 대로 혼용하거나 일치시킬 수 있습니다.
    
    시작 특수 매크로 지원 되는 또한: {최고}, toodetermine hello 첫 번째 "흥미로운" 프레임 참고 hello 콘텐츠의 시도: (단계 및 범위 시작 너무 설정 된 경우 무시 됩니다 {최상의})
  * 기본값: Start:{Best}
* 출력 형식 필요한 각 이미지 형식에 대해 명시적으로 제공 된 toobe: Jpg/Png/BmpFormat 합니다. 있는 경우 MES JpgVideo tooJpgFormat 등과 일치 합니다. 새 이미지 코덱 특정 매크로 소개: {인덱스로} 요구 toobe 있는 (한 번만 한 번)에 있는 이미지 출력 형식의 합니다.

## <a name="next-steps"></a>다음 단계

Hello를 확인할 수 있습니다 [진행률 작업](media-services-check-job-progress.md) 인코딩 작업 hello 하는 동안 보류 중입니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[미디어 서비스 인코딩 개요](media-services-encode-asset.md)

