---
title: "fMP4 청크를 생성하는 Azure Media Services 인코딩 작업 만들기 | Microsoft Docs"
description: "이 항목에서는 fMP4 청크를 생성하는 인코딩 작업을 만드는 방법을 보여 줍니다. 이 작업을 Media Encoder Standard 또는 Media Encoder Premium 워크플로 인코더와 함께 사용하면 출력 자산에는 ISO MP4 파일 대신 fMP4 청크가 포함됩니다."
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
ms.openlocfilehash: 55dca4bcb80e8daab2b4d293a9cc85a087055110
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
#  <a name="create-an-encoding-task-that-generates-fmp4-chunks"></a><span data-ttu-id="4fac2-104">fMP4 청크를 생성하는 인코딩 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="4fac2-104">Create an encoding task that generates fMP4 chunks</span></span>

## <a name="overview"></a><span data-ttu-id="4fac2-105">개요</span><span class="sxs-lookup"><span data-stu-id="4fac2-105">Overview</span></span>

<span data-ttu-id="4fac2-106">이 항목에서는 ISO MP4 파일 대신 조각화된 MP4(fMP4) 청크를 생성하는 인코딩 작업을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-106">This topic shows how to create an encoding task that generates fragmented MP4 (fMP4) chunks instead of ISO MP4 files.</span></span> <span data-ttu-id="4fac2-107">fMP4 청크를 생성하려면 다음 코드 조각처럼 **Media Encoder Standard** 또는 **Media Encoder Premium 워크플로** 인코더를 사용하여 인코딩 작업을 만들고 **AssetFormatOption.AdaptiveStreaming**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-107">To generate fMP4 chunks, use the **Media Encoder Standard** or **Media Encoder Premium Workflow** encoder to create an encoding task and also specify **AssetFormatOption.AdaptiveStreaming** option, as shown in this code snippet:</span></span>  
    
    task.OutputAssets.AddNew(@"Output Asset containing fMP4 chunks", 
            options: AssetCreationOptions.None, 
            formatOption: AssetFormatOption.AdaptiveStreaming);


## <span data-ttu-id="4fac2-108"><a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩</span><span class="sxs-lookup"><span data-stu-id="4fac2-108"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="4fac2-109">다음 코드 예제에서는 미디어 서비스 .NET SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-109">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="4fac2-110">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-110">Create an encoding job.</span></span>
- <span data-ttu-id="4fac2-111">**Media Encoder Standard** 인코더에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-111">Get a reference to the **Media Encoder Standard** encoder.</span></span>
- <span data-ttu-id="4fac2-112">작업에 인코딩 작업(task)을 추가하고 **적응 스트리밍** 사전 설정을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-112">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="4fac2-113">fMP4 청크 및 .ism 파일을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-113">Create an output asset that will contain fMP4 chunks and an .ism file.</span></span>
- <span data-ttu-id="4fac2-114">작업 진행 상태를 확인할 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-114">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="4fac2-115">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-115">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4fac2-116">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="4fac2-116">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="4fac2-117">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="4fac2-117">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="4fac2-118">예제</span><span class="sxs-lookup"><span data-stu-id="4fac2-118">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreaming
    {
        class Program
        {
        // Read values from the App.config file.
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

            // Encode and generate the output using the "Adaptive Streaming" preset.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
        }
        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");

            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job. 

            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            // It is also specified to use AssetFormatOption.AdaptiveStreaming, 
            // which means the output asset will contain fMP4 chunks.

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="4fac2-119">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="4fac2-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fac2-120">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="4fac2-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4fac2-121">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4fac2-121">See Also</span></span>
[<span data-ttu-id="4fac2-122">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="4fac2-122">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

