---
title: "Azure 미디어 인덱서 2 미리 보기를 사용 하 여 미디어 파일 aaaIndexing | Microsoft Docs"
description: "Azure Media Indexer 하면 toomake 콘텐츠 검색 가능한 미디어 파일 및 전체 텍스트 대 본 toogenerate 닫힌 캡션 및 키워드에 대 한 있습니다. 이 항목 toouse Media Indexer 2 미리 보기 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 85d25525-a498-44eb-ae3a-2ca5ceb8e53d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: f83fa0db58b828ffa29933d68ce108b4906dcd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer-2-preview"></a>Azure 미디어 인덱서 2 미리 보기를 사용하여 미디어 파일 인덱싱
## <a name="overview"></a>개요
hello **Azure 미디어 인덱서 2 미리 보기** 미디어 프로세서 MP ()를 사용 하면 toomake 미디어 파일 및 콘텐츠를 검색할 수, 닫힌된 캡션 트랙을 생성 합니다. 이전 버전의 비교 toohello [Azure Media Indexer](media-services-index-content.md), **Azure 미디어 인덱서 2 미리 보기** 더 빠른 인덱싱을 수행 하 고는 광범위 한 언어 지원을 제공 합니다. 지원되는 언어는 영어, 스페인어, 프랑스어, 독일어, 이탈리아어, 중국어(북경어, 간체), 포르투갈어, 아랍어, 일본어 등입니다.

hello **Azure 미디어 인덱서 2 미리 보기** MP는 현재 미리 보기로 합니다.

이 항목에서는 방법을와 작업 toocreate 인덱싱 **Azure 미디어 인덱서 2 미리 보기**합니다.

> [!NOTE]
> hello 고려 사항에 따라 적용 됩니다.
> 
> 인덱서 2는 Azure China 및 Azure Government에서 지원되지 않습니다.
> 
> 콘텐츠를 인덱싱할 때는 (배경 음악, 노이즈, 효과 또는 마이크 소음이 없어야 함) 없이 음성이 명확한 미디어 파일 toouse 있는지 확인 합니다. 적절한 콘텐츠의 예: 회의, 강의 또는 프레젠테이션 녹음. hello 다음 콘텐츠 맞지 않을 인덱싱: 영화, TV 쇼 혼합된 오디오와 소리 효과가 있는 어느 것에 저하 배경 노이즈 (소음)로 콘텐츠를 기록 합니다.
> 
> 

이 항목에 대 한 세부 정보를 제공 **Azure 미디어 인덱서 2 미리 보기** 표시 방법을 toouse Media Services SDK for.NET으로

## <a name="input-and-output-files"></a>입력 및 출력 파일
### <a name="input-files"></a>입력 파일
오디오 또는 비디오 파일

### <a name="output-files"></a>출력 파일
한 인덱싱 작업 hello 형식 뒤에 닫힌된 캡션 파일을 생성할 수 있습니다.  

* **SAMI**
* **TTML**
* **WebVTT**

비디오 파일 청각 장애가 있는 toopeople를 액세스할 수 있으며 이러한 형식의 닫힌된 캡션 (CC) 파일 사용된 toomake 오디오를 수 있습니다.

## <a name="task-configuration-preset"></a>작업 구성(기본 설정)
**Azure 미디어 인덱서 2 미리 보기**로 인덱싱 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.

hello 다음 JSON 사용 가능한 매개 변수를 설정 합니다.

    {
      "version":"1.0",
      "Features":
        [
           {
           "Options": {
                "Formats":["WebVtt","ttml"],
                "Language":"enUs",
                "Type":"RecoOptions"
           },
           "Type":"SpReco"
        }]
    }

## <a name="supported-languages"></a>지원되는 언어
Azure 미디어 인덱서 2 미리 보기 (아래와 같이 hello 작업 구성에서 사용 가능한 4 문자 코드 대괄호로 hello 언어 이름 지정) 하는 경우 언어를 다음 hello에 대 한 음성-텍스트를 지원 합니다.

* 영어[EnUs]
* 스페인어[EsEs]
* 중국어 (북경어, 간체) [ZhCn]
* 프랑스어[FrFr]
* 독일어[DeDe]
* 이탈리아어[ItIt]
* 포르투갈어[PtBr]
* 아랍어(이집트)[ArEg]
* 일본어 [JaJp]
* 러시아어[RuRu]
* 영국 영어[EnGb]
* 스페인어(멕시코)[EsMx] 

## <a name="supported-file-types"></a>지원되는 파일 형식

지원 되는 파일 형식에 대 한 정보를 참조 hello [지원 되는 코덱/형식](media-services-media-encoder-standard-formats.md#input-containerfile-formats) 섹션.

## <a name="net-sample-code"></a>.NET 샘플 코드

hello 다음 프로그램 표시 하는 방법:

1. 자산 만들기 hello 자산 미디어 파일을 업로드 합니다.
2. 인덱싱 작업 hello 다음 json 사전 설정을 포함 하는 구성 파일을 기반으로 작업을 만듭니다.
   
        {
          "version":"1.0",
          "Features":
            [
               {
               "Options": {
                    "Formats":["WebVtt","ttml"],
                    "Language":"enUs",
                    "Type":"RecoOptions"
               },
               "Type":"SpReco"
            }]
        }
3. Hello 출력 파일을 다운로드 합니다. 
   
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

    namespace IndexContent
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

                // Run indexing job.
                var asset = RunIndexingJob(@"C:\supportFiles\Indexer\BigBuckBunny.mp4",
                                            @"C:\supportFiles\Indexer\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\Indexer\Output");
            }

            static IAsset RunIndexingJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Indexing Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Indexing Job");

                // Get a reference tooAzure Media Indexer 2 Preview.
                string MediaProcessorName = "Azure Media Indexer 2 Preview";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Indexing Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset toobe indexed.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure Media Services 분석 개요](media-services-analytics-overview.md)

[Azure 미디어 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

