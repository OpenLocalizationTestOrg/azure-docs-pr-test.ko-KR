---
title: "비디오 요약 aaaUse Azure 미디어 비디오 축소판 그림 tooCreate | Microsoft Docs"
description: "비디오 요약을 사용 하면 hello 원본 비디오에서 흥미로운 조각을 자동으로 선택 하 여 긴 비디오의 요약을 만들 수 있습니다. Tooprovide 비디오에서 어떤 tooexpect의 간략 한 개요를 원하는 경우에 유용 합니다."
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
ms.openlocfilehash: 0a8f0bba6c12a948b940114fe4937e675688a8c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-video-thumbnails-toocreate-a-video-summarization"></a><span data-ttu-id="f7b01-104">Azure 미디어 비디오 축소판 그림 tooCreate 비디오 요약을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f7b01-104">Use Azure Media Video Thumbnails tooCreate a Video Summarization</span></span>
## <a name="overview"></a><span data-ttu-id="f7b01-105">개요</span><span class="sxs-lookup"><span data-stu-id="f7b01-105">Overview</span></span>
<span data-ttu-id="f7b01-106">hello **Azure 미디어 비디오 축소판** 미디어 프로세서 MP ()를 사용 하면 toocreate 비디오 toopreview 비디오의 요약을 유용한 toocustomers를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-106">hello **Azure Media Video Thumbnails** media processor (MP) enables you toocreate a summary of a video that is useful toocustomers who just want toopreview a summary of a long video.</span></span> <span data-ttu-id="f7b01-107">예를 들어 고객 toosee 짧은 "요약 비디오" 경우가 축소판 그림 가리켜 때.</span><span class="sxs-lookup"><span data-stu-id="f7b01-107">For example, customers might want toosee a short "summary video" when they hover over a thumbnail.</span></span> <span data-ttu-id="f7b01-108">hello 매개 변수를 조정 하 여 **Azure 미디어 비디오 축소판 그림** 연결 기술 tooalgorithmically 설명이 포함 된 하위 클립 생성 및 구성 사전 설정을 통해 hello MP의 강력한 발된 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-108">By tweaking hello parameters of **Azure Media Video Thumbnails** through a configuration preset, you can use hello MP's powerful shot detection and concatenation technology tooalgorithmically generate a descriptive subclip.</span></span>  

<span data-ttu-id="f7b01-109">hello **Azure 미디어 비디오 축소판 그림** MP는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-109">hello **Azure Media Video Thumbnail** MP is currently in Preview.</span></span>

<span data-ttu-id="f7b01-110">이 항목에 대 한 세부 정보를 제공 **Azure 미디어 비디오 축소판 그림** 표시 방법을 toouse Media Services SDK for.NET으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-110">This topic gives details about  **Azure Media Video Thumbnail** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="limitations"></a><span data-ttu-id="f7b01-111">제한 사항</span><span class="sxs-lookup"><span data-stu-id="f7b01-111">Limitations</span></span>

<span data-ttu-id="f7b01-112">경우에 따라 서로 다른 장면으로 이루어진 하지 비디오 hello 출력만 됩니다을 한 번입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-112">In some cases, if your video is not comprised of different scenes, hello output will only be a single shot.</span></span>

## <a name="video-summary-example"></a><span data-ttu-id="f7b01-113">비디오 요약 예제</span><span class="sxs-lookup"><span data-stu-id="f7b01-113">Video summary example</span></span>
<span data-ttu-id="f7b01-114">다음은 어떤 hello Azure 미디어 비디오 축소판 그림 미디어 프로세서 수행할 수 있는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-114">Here are some examples of what hello Azure Media Video Thumbnails media processor can do:</span></span>

### <a name="original-video"></a><span data-ttu-id="f7b01-115">원본 비디오</span><span class="sxs-lookup"><span data-stu-id="f7b01-115">Original video</span></span>
[<span data-ttu-id="f7b01-116">원본 비디오</span><span class="sxs-lookup"><span data-stu-id="f7b01-116">Original video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Faed33834-ec2d-4788-88b5-a4505b3d032c%2FMicrosoft%27s%20HoloLens%20Live%20Demonstration.ism%2Fmanifest)

### <a name="video-thumbnail-result"></a><span data-ttu-id="f7b01-117">비디오 미리 보기 결과</span><span class="sxs-lookup"><span data-stu-id="f7b01-117">Video thumbnail result</span></span>
[<span data-ttu-id="f7b01-118">비디오 미리 보기 결과</span><span class="sxs-lookup"><span data-stu-id="f7b01-118">Video thumbnail result</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Ff5c91052-4232-41d4-b531-062e07b6a9ae%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="task-configuration-preset"></a><span data-ttu-id="f7b01-119">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="f7b01-119">Task configuration (preset)</span></span>
<span data-ttu-id="f7b01-120">**Azure 미디어 비디오 미리 보기**로 비디오 미리 보기 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-120">When creating a video thumbnail task with **Azure Media Video Thumbnails**, you must specify a configuration preset.</span></span> <span data-ttu-id="f7b01-121">미리 보기 샘플 위에 hello은 같은 기본 JSON 구성이 hello로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-121">hello above thumbnail sample was created with hello following basic JSON configuration:</span></span>

    {"version":"1.0"}

<span data-ttu-id="f7b01-122">현재 매개 변수 뒤 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-122">Currently, you can change hello following parameters:</span></span>

| <span data-ttu-id="f7b01-123">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f7b01-123">Param</span></span> | <span data-ttu-id="f7b01-124">설명</span><span class="sxs-lookup"><span data-stu-id="f7b01-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7b01-125">outputAudio</span><span class="sxs-lookup"><span data-stu-id="f7b01-125">outputAudio</span></span> |<span data-ttu-id="f7b01-126">Hello 결과 비디오 오디오가 포함 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-126">Specifies whether or not hello resultant video contains any audio.</span></span> <br/><span data-ttu-id="f7b01-127">허용되는 값은 True 또는 False입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-127">Allowed values are: True or False.</span></span> <span data-ttu-id="f7b01-128">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-128">Default is True.</span></span> |
| <span data-ttu-id="f7b01-129">fadeInFadeOut</span><span class="sxs-lookup"><span data-stu-id="f7b01-129">fadeInFadeOut</span></span> |<span data-ttu-id="f7b01-130">지정 hello 별도 동작 미리 보기 간에 페이드 전환 여부가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-130">Specifies whether or not fade transitions are used between hello separate motion thumbnails.</span></span>  <br/><span data-ttu-id="f7b01-131">허용되는 값은 True 또는 False입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-131">Allowed values are: True or False.</span></span>  <span data-ttu-id="f7b01-132">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-132">Default is True.</span></span> |
| <span data-ttu-id="f7b01-133">maxMotionThumbnailDurationInSecs</span><span class="sxs-lookup"><span data-stu-id="f7b01-133">maxMotionThumbnailDurationInSecs</span></span> |<span data-ttu-id="f7b01-134">전체 결과 시간 비디오 hello를 지정 하는 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-134">Integer that specifies how long hello entire resultant video shall be.</span></span>  <span data-ttu-id="f7b01-135">기본값은 원본 비디오의 지속 시간에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-135">Default depends on original video duration.</span></span> |

<span data-ttu-id="f7b01-136">hello 다음 표에서 hello 기본 기간 때 **maxMotionThumbnailInSecs** 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-136">hello following table describes hello default duration, when **maxMotionThumbnailInSecs** is not used.</span></span>

|  |  |  |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f7b01-137">비디오 지속 시간</span><span class="sxs-lookup"><span data-stu-id="f7b01-137">Video duration</span></span> |<span data-ttu-id="f7b01-138">d < 3분</span><span class="sxs-lookup"><span data-stu-id="f7b01-138">d < 3 min</span></span> |<span data-ttu-id="f7b01-139">3분 < d < 15분</span><span class="sxs-lookup"><span data-stu-id="f7b01-139">3 min < d < 15 min</span></span> |
| <span data-ttu-id="f7b01-140">미리 보기 지속 시간</span><span class="sxs-lookup"><span data-stu-id="f7b01-140">Thumbnail duration</span></span> |<span data-ttu-id="f7b01-141">15초(장면 2~3개)</span><span class="sxs-lookup"><span data-stu-id="f7b01-141">15 sec (2-3 scenes)</span></span> |<span data-ttu-id="f7b01-142">30초(장면 3~5개)</span><span class="sxs-lookup"><span data-stu-id="f7b01-142">30 sec (3-5 scenes)</span></span> |

<span data-ttu-id="f7b01-143">hello 다음 JSON 사용 가능한 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-143">hello following JSON sets available parameters.</span></span>

    {
        "version": "1.0",
        "options": {
            "outputAudio": "true",
            "maxMotionThumbnailDurationInSecs": "10",
            "fadeInFadeOut": "true"
        }
    }

## <a name="net-sample-code"></a><span data-ttu-id="f7b01-144">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="f7b01-144">.NET sample code</span></span>

<span data-ttu-id="f7b01-145">hello 다음 프로그램 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="f7b01-145">hello following program shows how to:</span></span>

1. <span data-ttu-id="f7b01-146">자산 만들기 hello 자산 미디어 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-146">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="f7b01-147">다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 비디오 축소판 작업과 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-147">Creates a job with a video thumbnail task based on a configuration file that contains hello following json preset.</span></span> 
   
        {                
            "version": "1.0",
            "options": {
                "outputAudio": "true",
                "maxMotionThumbnailDurationInSecs": "30",
                "fadeInFadeOut": "false"
            }
        }
3. <span data-ttu-id="f7b01-148">Hello 출력 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-148">Downloads hello output files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="f7b01-149">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="f7b01-149">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="f7b01-150">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b01-150">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="f7b01-151">예제</span><span class="sxs-lookup"><span data-stu-id="f7b01-151">Example</span></span>

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


                // Run hello thumbnail job.
                var asset = RunVideoThumbnailJob(@"C:\supportFiles\VideoThumbnail\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoThumbnail\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoThumbnail\Output");
            }

            static IAsset RunVideoThumbnailJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Thumbnail Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Thumbnail Job");

                // Get a reference tooAzure Media Video Thumbnails.
                string MediaProcessorName = "Azure Media Video Thumbnails";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Thumbnail Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Thumbnail Output Asset", AssetCreationOptions.None);

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

### <a name="video-thumbnail-output"></a><span data-ttu-id="f7b01-152">비디오 미리 보기 출력</span><span class="sxs-lookup"><span data-stu-id="f7b01-152">Video thumbnail output</span></span>
[<span data-ttu-id="f7b01-153">비디오 미리 보기 출력</span><span class="sxs-lookup"><span data-stu-id="f7b01-153">Video thumbnail output</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=http%3A%2F%2Fnimbuscdn-nimbuspm.streaming.mediaservices.windows.net%2Fd06f24dc-bc81-488e-a8d0-348b7dc41b56%2FHololens%2520Demo_VideoThumbnails_MotionThumbnail.mp4)

## <a name="media-services-learning-paths"></a><span data-ttu-id="f7b01-154">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f7b01-154">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f7b01-155">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f7b01-155">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f7b01-156">관련 링크</span><span class="sxs-lookup"><span data-stu-id="f7b01-156">Related links</span></span>
[<span data-ttu-id="f7b01-157">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="f7b01-157">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f7b01-158">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="f7b01-158">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

