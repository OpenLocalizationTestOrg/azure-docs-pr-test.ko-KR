---
title: "Azure Media Video Thumbnails를 사용하여 비디오 요약 만들기 | Microsoft Docs"
description: "비디오 요약을 사용하면 원본 비디오에서 흥미로운 조각을 자동으로 선택하여 긴 비디오의 요약을 만들 수 있습니다. 이는 긴 비디오에서 예상되는 사항에 대한 빠른 개요를 제공하려는 경우에 유용합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a245529f-3150-4afc-93ec-e40d8a6b761d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 5d5afdaf22ffea8f3b77a154acb5d0a8dda74405
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-video-thumbnails-to-create-a-video-summarization"></a><span data-ttu-id="2a47a-104">Azure 미디어 비디오 미리 보기를 사용하여 비디오 요약 만들기</span><span class="sxs-lookup"><span data-stu-id="2a47a-104">Use Azure Media Video Thumbnails to Create a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="2a47a-105">개요</span><span class="sxs-lookup"><span data-stu-id="2a47a-105">Overview</span></span>
<span data-ttu-id="2a47a-106">**Azure 미디어 비디오 미리 보기** MP(미디어 프로세서)를 사용하여 긴 비디오의 요약만 미리 보려는 고객에게 유용한 비디오 요약을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-106">The **Azure Media Video Thumbnails** media processor (MP) enables you to create a summary of a video that is useful to customers who just want to preview a summary of a long video.</span></span> <span data-ttu-id="2a47a-107">예를 들어 고객은 미리 보기를 가리키면 나타나는 짧은 "요약 비디오"를 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-107">For example, customers might want to see a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="2a47a-108">구성 기본 설정을 통해 **Azure 미디어 비디오 미리 보기** 의 매개 변수를 조정하면 MP의 강력한 장면 감지 및 연결 기술을 사용하여 알고리즘 방식으로 설명이 포함된 하위 클립을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-108">By tweaking the parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use the MP's powerful shot detection and concatenation technology to algorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="2a47a-109">**Azure 미디어 비디오 미리 보기** MP는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-109">The **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="2a47a-110">이 항목에서는 **Azure Media Video Thumbnails**에 대한 세부 정보 및 .NET용 Media Services SDK와 함께 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="2a47a-111">제한 사항</span><span class="sxs-lookup"><span data-stu-id="2a47a-111">Limitations</span></span>

<span data-ttu-id="2a47a-112">여러 장면으로 구성되지 않은 비디오의 경우 하나의 장면만 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-112">In some cases, if your video is not comprised of different scenes, the output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="2a47a-113">비디오 요약 예제</span><span class="sxs-lookup"><span data-stu-id="2a47a-113">Video summary example</span></span>
<span data-ttu-id="2a47a-114">Azure 미디어 비디오 미리 보기 미디어 프로세서에서 수행할 수 있는 작업의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-114">Here are some examples of what the Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="2a47a-115">원본 비디오</span><span class="sxs-lookup"><span data-stu-id="2a47a-115">Original video</span></span>
[<span data-ttu-id="2a47a-116">원본 비디오</span><span class="sxs-lookup"><span data-stu-id="2a47a-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="2a47a-117">비디오 미리 보기 결과</span><span class="sxs-lookup"><span data-stu-id="2a47a-117">Video thumbnail result</span></span>
[<span data-ttu-id="2a47a-118">비디오 미리 보기 결과</span><span class="sxs-lookup"><span data-stu-id="2a47a-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="2a47a-119">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="2a47a-119">Task configuration (preset)</span></span>
<span data-ttu-id="2a47a-120">**Azure 미디어 비디오 미리 보기**로 비디오 미리 보기 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="2a47a-121">위의 미리 보기 샘플은 다음 기본 JSON 구성을 사용하여 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-121">The above thumbnail sample was created with the following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="2a47a-122">현재 다음 매개 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-122">Currently, you can change the following parameters:</span></span>

| <span data-ttu-id="2a47a-123">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2a47a-123">Param</span></span> | <span data-ttu-id="2a47a-124">설명</span><span class="sxs-lookup"><span data-stu-id="2a47a-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a47a-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="2a47a-125">outputAudio</span></span> |<span data-ttu-id="2a47a-126">결과 비디오에 오디오를 포함할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-126">Specifies whether or not the resultant video contains any audio.</span></span> <br/><span data-ttu-id="2a47a-127">허용되는 값은 True 또는 False입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-127">Allowed values are: True or False.</span></span> <span data-ttu-id="2a47a-128">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-128">Default is True.</span></span> |
| <span data-ttu-id="2a47a-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="2a47a-129">fadeInFadeOut</span></span> |<span data-ttu-id="2a47a-130">개별 동작 미리 보기 간에 페이드 전환이 사용되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-130">Specifies whether or not fade transitions are used between the separate motion thumbnails.</span></span>  <br/><span data-ttu-id="2a47a-131">허용되는 값은 True 또는 False입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="2a47a-132">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-132">Default is True.</span></span> |
| <span data-ttu-id="2a47a-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="2a47a-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="2a47a-134">전체 결과 비디오의 길이를 지정하는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-134">Integer that specifies how long the entire resultant video shall be.</span></span>  <span data-ttu-id="2a47a-135">기본값은 원본 비디오의 지속 시간에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="2a47a-136">다음 표에서는 **maxMotionThumbnailInSecs** 가 사용되지 않은 경우의 기본 지속 시간을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-136">The following table describes the default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2a47a-137">비디오 지속 시간</span><span class="sxs-lookup"><span data-stu-id="2a47a-137">Video duration</span></span> |<span data-ttu-id="2a47a-138">d < 3분</span><span class="sxs-lookup"><span data-stu-id="2a47a-138">d < 3 min</span></span> |<span data-ttu-id="2a47a-139">3분 < d < 15분</span><span class="sxs-lookup"><span data-stu-id="2a47a-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="2a47a-140">미리 보기 지속 시간</span><span class="sxs-lookup"><span data-stu-id="2a47a-140">Thumbnail duration</span></span> |<span data-ttu-id="2a47a-141">15초(장면 2~3개)</span><span class="sxs-lookup"><span data-stu-id="2a47a-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="2a47a-142">30초(장면 3~5개)</span><span class="sxs-lookup"><span data-stu-id="2a47a-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="2a47a-143">다음 JSON은 사용 가능한 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-143">The following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="2a47a-144">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="2a47a-144">.NET sample code</span></span>

<span data-ttu-id="2a47a-145">다음 프로그램은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-145">The following program shows how to:</span></span>

1. <span data-ttu-id="2a47a-146">자산을 만들고 미디어 파일을 자산에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-146">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="2a47a-147">다음 json 기본 설정을 포함하는 구성 파일을 기반으로 비디오 미리 보기 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-147">Creates a job with a video thumbnail task based on a configuration file that contains the following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="2a47a-148">출력 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-148">Downloads the output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2a47a-149">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2a47a-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2a47a-150">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2a47a-150">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="2a47a-151">예제</span><span class="sxs-lookup"><span data-stu-id="2a47a-151">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoSummarization
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


                // Run the thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference to Azure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

### <a name="video-thumbnail-output"></a><span data-ttu-id="2a47a-152">비디오 미리 보기 출력</span><span class="sxs-lookup"><span data-stu-id="2a47a-152">Video thumbnail output</span></span>
[<span data-ttu-id="2a47a-153">비디오 미리 보기 출력</span><span class="sxs-lookup"><span data-stu-id="2a47a-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="2a47a-154">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2a47a-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2a47a-155">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2a47a-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="2a47a-156">관련 링크</span><span class="sxs-lookup"><span data-stu-id="2a47a-156">Related links</span></span>
[<span data-ttu-id="2a47a-157">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="2a47a-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="2a47a-158">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="2a47a-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

