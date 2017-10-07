---
title: "미디어 인코더 프리미엄 워크플로 aaaAdvanced 인코딩을 | Microsoft Docs"
description: "자세한 방법을 tooencode 미디어 인코더 프리미엄 워크플로 사용 합니다. 코드 예제는 C#으로 작성 및 hello Media Services SDK for.NET 사용 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0f4c87ac-810a-4d42-8df8-923dff2016c6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 5a1c3d019a5c8fbf9bda2da751a7eff4c4907d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-encoding-with-media-encoder-premium-workflow"></a>미디어 인코더 Premium 워크플로를 사용한 고급 인코딩
> [!NOTE]
> 중국에서는 이 토픽에서 설명하는 미디어 인코더 Premium 워크플로 미디어 프로세서를 사용할 수 없습니다.
>
>

프리미엄 인코더 관련 질문은 mepd@microsoft.com으로 문의하세요.

## <a name="overview"></a>개요
Microsoft Azure 미디어 서비스는 hello 도입 **미디어 인코더 프리미엄 워크플로** 미디어 프로세서. 이 프로세서는 프리미엄 주문형 워크플로에 고급 인코딩 기능을 제공합니다.

hello 다음 항목에 간략하게 설명 너무 관련 된 세부 정보**미디어 인코더 프리미엄 워크플로**:

* [Supported hello 미디어 인코더 프리미엄 워크플로 형식을](media-services-premium-workflow-encoder-formats.md) – hello 파일 형식 및 코덱을 지원에 대해 설명 **미디어 인코더 프리미엄 워크플로**합니다.
* [개요 및 요청 시 미디어 인코더에서 Azure의 비교](media-services-encode-asset.md) 비교 하 여 hello의 인코딩 기능 **미디어 인코더 프리미엄 워크플로** 및 **미디어 인코더 표준**합니다.

이 항목에서 설명 방법을와 tooencode **미디어 인코더 프리미엄 워크플로** .NET을 사용 하 여 합니다.

Hello에 대 한 작업 인코딩 **미디어 인코더 프리미엄 워크플로** 워크플로 파일 라는 별도 구성 파일을 필요 합니다. 이러한 파일은 영숫자이어야 확장명 하며 hello를 사용 하 여 만들어지며 [워크플로 디자이너](media-services-workflow-designer.md) 도구입니다.

가져올 수도 있습니다 hello 기본 워크플로 파일 [여기](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)합니다. hello 폴더에는 이러한 파일에 대 한 hello 설명을 포함 되어 있습니다.

hello 워크플로 파일을 자산으로 업로드 toobe tooyour 미디어 서비스 계정이 필요 하며 인코딩 작업 toohello이이 자산을 전달 해야 합니다.

## <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

## <a name="encoding-example"></a>인코딩 예제

hello 다음 예제에서는 어떻게와 tooencode **미디어 인코더 프리미엄 워크플로**합니다.

단계를 수행 하는 hello 수행 됩니다.

1. 자산을 만들고 워크플로 파일을 업로드합니다.
2. 자산을 만들고 소스 미디어 파일을 업로드합니다.
3. Hello "미디어 인코더 프리미엄 워크플로" 미디어 프로세서를 가져옵니다.
4. 작업 및 태스크를 만듭니다.

    대부분의 경우에서 hello 작업에 대 한 구성 문자열 hello 비어 (hello 다음 예제에서에서와 같이). 몇 가지 고급 시나리오가 (해야 하는 런타임 속성 tootooset 동적으로)는 쿼리에서 XML 문자열 toohello 인코딩 작업을 제공 합니다. 이러한 시나리오의 예로는 오버레이 만들기, 순차 또는 병렬 미디어 연결, 자막 작성 등이 있습니다.
5. 두 개의 입력된 자산 toohello 작업을 추가 합니다.

    1. 1 – hello 워크플로 자산입니다.
    2. 2 – hello 비디오 자산입니다.

    >[!NOTE]
    >hello 워크플로 자산 toohello 작업 전에 hello 미디어 자산을 추가 합니다.
   이 작업에 대 한 hello 구성 문자열은 비어 있어야 합니다.
   
6. Hello 인코딩 작업을 제출 합니다.

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderPremiumWorkflowSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

                private static readonly string _workflowFilePath =
                    Path.GetFullPath(_supportFiles + @"\H264 Progressive Download MP4.workflow");

                private static readonly string _singleMP4InputFilePath =
                    Path.GetFullPath(_supportFiles + @"\BigBuckBunny.mp4");

                static void Main(string[] args)
                {
                    var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                    _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                    var workflowAsset = CreateAssetAndUploadSingleFile(_workflowFilePath);
                    var videoAsset = CreateAssetAndUploadSingleFile(_singleMP4InputFilePath);
                    IAsset outputAsset = CreateEncodingJob(workflowAsset, videoAsset);

                }

                static public IAsset CreateAssetAndUploadSingleFile(string singleFilePath)
                {
                    var assetName = "UploadSingleFile_" + DateTime.UtcNow.ToString();
                    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

                    var fileName = Path.GetFileName(singleFilePath);

                    var assetFile = asset.AssetFiles.Create(fileName);

                    Console.WriteLine("Created assetFile {0}", assetFile.Name);

                    Console.WriteLine("Upload {0}", assetFile.Name);

                    assetFile.Upload(singleFilePath);
                    Console.WriteLine("Done uploading {0}", assetFile.Name);

                    return asset;
                }

                static public IAsset CreateEncodingJob(IAsset workflow, IAsset video)
                {
                    // Declare a new job.
                    IJob job = _context.Jobs.Create("Premium Workflow encoding job");
                    // Get a media processor reference, and pass tooit hello name of the
                    // processor toouse for hello specific task.
                    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

                    // Create a task with hello encoding details, using a string preset.
                    ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                        processor,
                        "",
                        TaskOptions.None);

                    // Specify hello input asset toobe encoded.
                    task.InputAssets.Add(workflow);
                    task.InputAssets.Add(video); // we add one asset
                                                 // Add an output asset toocontain hello results of hello job.
                                                 // This output is specified as AssetCreationOptions.None, which
                                                 // means hello output asset is not encrypted.
                    task.OutputAssets.AddNew("Output asset",
                        AssetCreationOptions.None);

                    // Use hello following event handler toocheck job progress.  
                    job.StateChanged += new
                            EventHandler<JobStateChangedEventArgs>(StateChanged);

                    // Launch hello job.
                    job.Submit();

                    // Check job execution and wait for job toofinish.
                    Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
                    progressJobTask.Wait();

                    // If job state is Error hello event handling
                    // method for job progress should log errors.  Here we check
                    // for error state and exit if needed.
                    if (job.State == JobState.Error)
                    {
                        throw new Exception("\nExiting method due toojob error.");
                    }

                    return job.OutputMediaAssets[0];
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

프리미엄 인코더 관련 질문은 mepd@microsoft.com으로 문의하세요.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
