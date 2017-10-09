---
title: "aaaCreate fMP4 청크를 생성 하는 Azure 미디어 서비스 인코딩 작업 | Microsoft Docs"
description: "이 항목에서는 fMP4 생성 되는 인코딩 작업을 분할 하는 toocreate 방법을 보여 줍니다. 이 작업은 사용 되 면 미디어 인코더 표준 hello 또는 미디어 인코더 프리미엄 워크플로 인코더, ISO MP4 파일 대신 fMP4 청크 hello 출력 자산에 포함 됩니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b7029ac5-eadd-4a2f-8111-1fc460828981
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 388f3ccb9865b5c4e159af86d5a9ee2f4e3f6120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="ac30d-104">fMP4 청크를 생성하는 인코딩 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ac30d-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="ac30d-105">개요</span><span class="sxs-lookup"><span data-stu-id="ac30d-105">Overview</span></span>

<span data-ttu-id="ac30d-106">이 항목에서는 어떻게 생성 하는 인코딩 작업 toocreate 조각난 MP4 (fMP4) 청크 ISO MP4 파일 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-106">This topic shows how toocreate an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="ac30d-107">toogenerate fMP4 청크를 사용 하 여 hello **미디어 인코더 표준** 또는 **미디어 인코더 프리미엄 워크플로** 인코더 toocreate 인코딩 작업 및도 지정  **AssetFormatOption.AdaptiveStreaming** 이 코드 조각에 나와 있는 것 처럼 옵션:</span><span class="sxs-lookup"><span data-stu-id="ac30d-107">toogenerate fMP4 chunks, use hello **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder toocreate an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="ac30d-108"><a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩</span><span class="sxs-lookup"><span data-stu-id="ac30d-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="ac30d-109">다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-109">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="ac30d-110">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-110">Create an encoding job.</span></span>
- <span data-ttu-id="ac30d-111">참조 toohello 가져오기 **미디어 인코더 표준** 인코더입니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-111">Get a reference toohello **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="ac30d-112">인코딩 작업 toohello 작업을 추가 하 고 toouse hello 지정 **적응 스트리밍** 사전 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-112">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="ac30d-113">fMP4 청크 및 .ism 파일을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="ac30d-114">이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-114">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="ac30d-115">Hello 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-115">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="ac30d-116">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="ac30d-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="ac30d-117">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac30d-117">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="ac30d-118">예제</span><span class="sxs-lookup"><span data-stu-id="ac30d-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
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

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate hello output using hello "Adaptive Streaming" preset.
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

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job. 

            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            // It is also specified toouse AssetFormatOption.AdaptiveStreaming, 
            // which means hello output asset will contain fMP4 chunks.

            task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks",
            options: AssetCreationOptions.None,
            formatOption: AssetFormatOption.AdaptiveStreaming);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="ac30d-119">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ac30d-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac30d-120">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ac30d-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ac30d-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ac30d-121">See Also</span></span>
[<span data-ttu-id="ac30d-122">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="ac30d-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

