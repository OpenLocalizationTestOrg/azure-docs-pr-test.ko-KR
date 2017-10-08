---
title: "Azure 미디어 분석을 aaaRedact 면 | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 analytics와 tooredact 직면 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a>Azure 미디어 분석으로 얼굴 편집
## <a name="overview"></a>개요
**Azure 미디어 Redactor** 는 [Azure 미디어 분석](media-services-analytics-overview.md) hello 클라우드에서 확장 가능한 글꼴 교정에서 제공 하는 미디어 프로세서 (MP). Face 교정 있습니다 toomodify 선택한 개인의 순서 tooblur 면에서 비디오를 수 있습니다. 공용 안전과 뉴스 미디어 시나리오에서 toouse hello 얼굴 교정 서비스를 할 수 있습니다. 몇 분 정도 여러 글꼴로 포함 된 장면 시간 tooredact 수동으로 필요로 하지만이 서비스 hello 모양을 가진 교정 프로세스는 몇 가지 간단한 단계만 거치면 요구 됩니다. 자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.

이 항목에 대 한 세부 정보를 제공 **Azure 미디어 Redactor** 표시 방법을 toouse Media Services SDK for.NET으로 합니다.

hello **Azure 미디어 Redactor** MP는 현재 미리 보기로 합니다. 이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다. 이 미리 보기는 현재 무료입니다. 

## <a name="face-redaction-modes"></a>얼굴 편집 모드
비디오의 모든 프레임에서 얼굴 감지 하 고 hello 얼굴 추적 안 면 교정 works 개체 모두 앞으로 및 뒤로 시간 내에 있도록 hello 동일한 개별 수 수 흐려지는 다른 각도도에서 합니다. hello 교정 자동화 된 프로세스는 매우 복잡 하며 미디어 분석을 제공 toomodify hello 최종 출력 하는 여러 가지 방법으로 이러한 이유로 100%의 원하는 출력을 생성 하지 않습니다.

또한 tooa 완전 자동 모드에서는 hello 선택/de-selection Id 목록을 통해 찾은 면 수 있는 2 패스 워크플로입니다. 또한, 프레임 조정 hello MP 당 임의의 toomake JSON 형식의 메타 데이터 파일을 사용합니다. 이 워크플로는 **분석** 및 **편집** 모드로 분할됩니다. 두 작업 모두 하나의 작업이;에서 실행 되는 단일 패스로 hello 두 가지 모드를 결합할 수 있습니다. 이 모드는 무엇 일까요 **조합**합니다.

### <a name="combined-mode"></a>결합된 모드
이 모드는 수동 입력 없이 자동으로 편집된 mp4를 생성합니다.

| 단계 | 파일 이름 | 참고 사항 |
| --- | --- | --- |
| 입력 자산 |foo.bar |WMV, MOV 또는 MP4 형식의 동영상 |
| 입력 구성 |작업 구성 사전 설정 |{'version':'1.0', 'options': {'mode':'combined'}} |
| 출력 자산 |foo_redacted.mp4 |흐리게 표시하기가 적용된 동영상 |

#### <a name="input-example"></a>입력 예:
[이 동영상을 보세요.](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a>출력 예제:
[이 동영상을 보세요.](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a>분석 모드
hello **분석** 각 개의 jpg 이미지가 얼굴 감지 및 hello 2 패스 워크플로의 패스 비디오 입력을 얼굴 위치의 JSON 파일을 생성 합니다.

| 단계 | 파일 이름 | 참고 사항 |
| --- | --- | --- |
| 입력 자산 |foo.bar |WMV, MPV 또는 MP4 형식의 동영상 |
| 입력 구성 |작업 구성 사전 설정 |{'version':'1.0', 'options': {'mode':'analyze'}} |
| 출력 자산 |foo_annotations.json |얼굴 위치의 주석 데이터(JSON 형식). 이 흐리게 하 여 hello 사용자 toomodify hello 경계 상자의 편집할 수 있습니다. 아래 샘플을 참조하세요. |
| 출력 자산 |foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg] |각 자른된 jpg 과제를 여기서 hello 번호 나타냅니다 hello 앞면의 hello labelId를 발견 했습니다. |

#### <a name="output-example"></a>출력 예제:

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a>편집 모드
hello hello 워크플로의 두 번째 단계에서는 단일 자산에 결합 해야 하는 입력 중 더 큰 수 합니다.

여기에 Id tooblur, hello 원본 비디오 및 JSON hello 주석 목록이 포함 됩니다. 이 모드는 hello 입력된 비디오에서 주석 tooapply 흐리게 hello를 사용 합니다.

hello 출력 hello 분석 패스에서는 hello 원본 비디오 비디오 hello toobe hello Redact 모드 작업에 대 한 hello 입력된 자산으로 업로드 하 고 주 파일 hello로 선택 해야 합니다.

| 단계 | 파일 이름 | 참고 사항 |
| --- | --- | --- |
| 입력 자산 |foo.bar |WMV, MPV 또는 MP4 형식의 동영상. 1단계와 동일한 동영상입니다. |
| 입력 자산 |foo_annotations.json |1단계의 주석 메타데이터 파일 및 수정 사항(선택 사항) |
| 입력 자산 |foo_IDList.txt(선택 사항) |(옵션) 새 줄 면 tooredact Id의 목록을 구분합니다. 지정하지 않으면 모든 얼굴이 흐리게 표시됩니다. |
| 입력 구성 |작업 구성 사전 설정 |{'version':'1.0', 'options': {'mode':'redact'}} |
| 출력 자산 |foo_redacted.mp4 |주석을 기반으로 흐리게 표시하기가 적용된 동영상 |

#### <a name="example-output"></a>예제 출력
선택한 한 ID 가진 IDList hello 출력입니다.

[이 동영상을 보세요.](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

예제 foo_IDList.txt
 
     1
     2
     3

## <a name="blur-types"></a>흐리게 형식

Hello에 **조합** 또는 **Redact** 모드를 가지 5 다른 흐림 효과 모드를 통해 hello JSON 입력된 구성에서 선택할 수 있습니다: **낮은**, **Med**, **높은**, **디버그**, 및 **검정**합니다. 기본적으로 **중간**이 사용됩니다.

샘플의 hello 아래의 형식 흐림 효과 찾을 수 있습니다.

### <a name="example-json"></a>예제 JSON:

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a>낮음

![낮음](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a>중간

![중간](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a>높음

![높음](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a>디버그

![디버그](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a>검정

![검정](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a>Hello 출력 JSON 파일의 요소

hello 교정 MP 고정밀 얼굴 위치 검색 및 비디오 프레임에 too64 휴먼 면을 검색할 수 있는 추적을 제공 합니다. 전면 제공 하는 동안 측면 및 작은 면 hello 최상의 결과 (미만 또는 too24x24 픽셀 값이) 하는 어려움이 있습니다.

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a>.NET 샘플 코드

hello 다음 프로그램 표시 하는 방법:

1. 자산 만들기 hello 자산 미디어 파일을 업로드 합니다.
2. 다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 얼굴 교정 작업과 작업을 만듭니다. 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. Hello 출력 JSON 파일을 다운로드 합니다. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

#### <a name="example"></a>예제

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
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

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                   mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
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
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a>다음 단계

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure Media Services 분석 개요](media-services-analytics-overview.md)

[Azure 미디어 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

