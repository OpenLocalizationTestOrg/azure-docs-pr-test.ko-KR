---
title: "미디어 인코더 표준 사전 설정 aaaCustomizing | Microsoft Docs"
description: "이 항목에서는 tooperform 고급 미디어 인코더 표준 태스크 사전 설정 사용자 지정 하 여 인코딩을 하는 방법을 보여 줍니다. hello 항목 인코딩 toouse 미디어 서비스.NET SDK toocreate 작업 및 작업 방법을 보여 줍니다. 또한 사용자 지정 toosupply 미리 toohello 인코딩 작업을 설정 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: fa8c3bef63b0c1ecc88a6b8874ecbff3a8028a57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-media-encoder-standard-presets"></a>Media Encoder Standard 사전 설정 사용자 지정

## <a name="overview"></a>개요

이 항목에서는와 미디어 인코더 표준 MES ()는 사용자 정의 인코딩 고급 tooperform 사전 설정 하는 방법을 보여 줍니다. hello 항목 인코딩 작업 하 고이 작업을 실행 하는 작업.NET toocreate를 사용 합니다.  

이 항목에 표시 됩니다 toocustomize 사전 설정을 수행 하 여 hello 어떻게 [H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 레이어의 미리 설정 된 및 줄여서 hello 수 있습니다. hello [미디어 인코더 표준 사용자 지정 사전 설정을](media-services-advanced-encoding-with-mes.md) 항목에 사용 되는 tooperform 고급 인코딩 작업 수 있는 사용자 지정 사전 설정을 보여 줍니다.

## <a id="customizing_presets"></a> MES 사전 설정 사용자 지정

### <a name="original-preset"></a>원래 사전 설정

Hello에 정의 된 JSON 저장 hello [H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) .json 확장명이 일부 파일의 항목입니다. 예를 들어 **CustomPreset_JSON.json**과 같습니다.

### <a name="customized-preset"></a>사용자 지정한 사전 설정

열기 hello **CustomPreset_JSON.json** 파일을 처음 세 계층에서 제거 **H264Layers** 파일에는 다음과 같이 되도록 합니다.

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
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
    

## <a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩

다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.

- 인코딩 작업을 만듭니다.
- 참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.
- 사용자 지정 JSON hello 이전 섹션에서 만든 사전 설정 hello를 로드 합니다. 
  
        // Load hello JSON from hello local file.
        string configuration = File.ReadAllText(fileName);  

- 인코딩 작업 toohello 작업을 추가 합니다. 
- Hello 입력 지정 인코딩된 자산 toobe 합니다.
- Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.
- 이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.
- Hello 작업을 제출 합니다.
   
#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

#### <a name="example"></a>예제   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
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

            // Encode and generate hello output using custom presets.
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
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

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

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[미디어 서비스 인코딩 개요](media-services-encode-asset.md)

