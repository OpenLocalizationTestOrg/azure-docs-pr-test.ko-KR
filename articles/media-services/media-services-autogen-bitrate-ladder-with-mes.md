---
title: "Azure Media Encoder Standard를 사용하여 비트 전송률 사다리 자동 생성 | Microsoft Docs"
description: "이 항목에서는 MES(Media Encoder Standard)를 사용하여 입력 해상도 및 비트 전송률을 기반으로 비트 전송률 사다리를 자동 생성하는 방법을 보여 줍니다. 입력 해상도 및 비트 전송률은 초과되지 않습니다. 예를 들어, 입력이 3Mbps에서 720p이고 출력이 최적 시 720p로 유지되는 경우 3Mbps보다 낮은 전송률로 시작됩니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 63ed95da-1b82-44b0-b8ff-eebd535bc5c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: b5616aa9f8b15ab576d914fbae89a56f64c27f4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
#  <a name="use-azure-media-encoder-standard-to-auto-generate-a-bitrate-ladder"></a><span data-ttu-id="2ec6e-105">Azure Media Encoder Standard를 사용하여 비트 전송률 사다리 자동 생성</span><span class="sxs-lookup"><span data-stu-id="2ec6e-105">Use Azure Media Encoder Standard to auto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="2ec6e-106">개요</span><span class="sxs-lookup"><span data-stu-id="2ec6e-106">Overview</span></span>

<span data-ttu-id="2ec6e-107">이 항목에서는 MES(Media Encoder Standard)를 사용하여 입력 해상도 및 비트 전송률을 기반으로 비트 전송률 사다리를 자동 생성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-107">This topic shows how to use Media Encoder Standard (MES) to auto-generate a bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate.</span></span> <span data-ttu-id="2ec6e-108">자동 생성된 사전 설정은 입력 해상도 및 비트 전송률을 초과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-108">The auto-generated preset will never exceed the input resolution and bitrate.</span></span> <span data-ttu-id="2ec6e-109">예를 들어, 입력이 3Mbps에서 720p이고 출력이 최적 시 720p로 유지되는 경우 3Mbps보다 낮은 전송률로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-109">For example, if the input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="2ec6e-110">스트리밍 전용 인코딩</span><span class="sxs-lookup"><span data-stu-id="2ec6e-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="2ec6e-111">원본 비디오를 스트리밍 전용으로 인코딩하려는 경우에는 인코딩 작업을 만들 때 "적응 스트리밍" 사전 설정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-111">If your intent is to encode your source video only for streaming, then you shoud use the "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="2ec6e-112">**적응 스트리밍** 사전 설정을 사용할 때 MES 인코더는 비트 전송률 사다리를 지능적으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-112">When using the **Adaptive Streaming** preset, the MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="2ec6e-113">하지만 서비스에서 사용할 레이어 수와 해상도를 결정하므로 인코딩 비용은 제어할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-113">However, you will not be able to control the encoding costs, since the service determines how many layers to use and at what resolution.</span></span> <span data-ttu-id="2ec6e-114">**적응 스트리밍** 사전 설정을 사용하여 인코딩한 결과로 MES에 의해 생성된 출력 계층의 예제는 이 항목의 끝부분에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-114">You can see examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset at the end of this topic.</span></span> <span data-ttu-id="2ec6e-115">출력 자산에는 오디오 및 비디오가 인터리빙되지 않은 MP4 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-115">The output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="2ec6e-116">스트리밍 및 점진적 다운로드용 인코딩</span><span class="sxs-lookup"><span data-stu-id="2ec6e-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="2ec6e-117">스트리밍을 수행하고 점진적 다운로드를 위한 MP4 파일을 생성하기 위해 원본 비디오를 인코딩하려는 경우에는 인코딩 작업을 만들 때 "콘텐츠 적응 다중 비트 전송률 MP4" 사전 설정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-117">If your intent is to encode your source video for streaming as well as to produce MP4 files for progressive download, then you shoud use the "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="2ec6e-118">**콘텐츠 적응 다중 비트 전송률 MP4** 사전 설정을 사용할 때도 MES 인코더는 위에서 설명한 것과 동일한 인코딩 논리를 적용합니다. 그러나 이 경우 출력 자산에는 오디오와 비디오가 인터리빙되는 MP4 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-118">When using the **Content Adaptive Multiple Bitrate MP4** preset, the MES encoder will apply the same encoding logic as above, but now the output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="2ec6e-119">이러한 MP4 파일 중 하나(예: 비트 전송률이 가장 높은 버전)를 점진적 다운로드 파일로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-119">You can use one of these MP4 files (for example, the highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="2ec6e-120"><a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩</span><span class="sxs-lookup"><span data-stu-id="2ec6e-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="2ec6e-121">다음 코드 예제에서는 미디어 서비스 .NET SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-121">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="2ec6e-122">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-122">Create an encoding job.</span></span>
- <span data-ttu-id="2ec6e-123">미디어 인코더 표준 인코더에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-123">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="2ec6e-124">작업에 인코딩 작업(task)을 추가하고 **적응 스트리밍** 사전 설정을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-124">Add an encoding task to the job and specify to use the **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="2ec6e-125">인코딩된 자산을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-125">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="2ec6e-126">작업 진행 상태를 확인할 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-126">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="2ec6e-127">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-127">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2ec6e-128">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2ec6e-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="2ec6e-129">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-129">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="2ec6e-130">예제</span><span class="sxs-lookup"><span data-stu-id="2ec6e-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

## <span data-ttu-id="2ec6e-131"><a id="output"></a>출력</span><span class="sxs-lookup"><span data-stu-id="2ec6e-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="2ec6e-132">이 섹션에서는 **적응 스트리밍** 사전 설정으로 인코딩한 결과로 MES에 의해 생성된 출력 계층의 세 가지 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-132">This section shows three examples of output layers produced by MES as a result of encoding with the **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="2ec6e-133">예 1</span><span class="sxs-lookup"><span data-stu-id="2ec6e-133">Example 1</span></span>
<span data-ttu-id="2ec6e-134">높이가 "1080"이고 프레임 속도가 "29.970"인 원본은 6개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="2ec6e-135">계층</span><span class="sxs-lookup"><span data-stu-id="2ec6e-135">Layer</span></span>|<span data-ttu-id="2ec6e-136">높이</span><span class="sxs-lookup"><span data-stu-id="2ec6e-136">Height</span></span>|<span data-ttu-id="2ec6e-137">너비</span><span class="sxs-lookup"><span data-stu-id="2ec6e-137">Width</span></span>|<span data-ttu-id="2ec6e-138">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="2ec6e-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2ec6e-139">1</span><span class="sxs-lookup"><span data-stu-id="2ec6e-139">1</span></span>|<span data-ttu-id="2ec6e-140">1080</span><span class="sxs-lookup"><span data-stu-id="2ec6e-140">1080</span></span>|<span data-ttu-id="2ec6e-141">1920</span><span class="sxs-lookup"><span data-stu-id="2ec6e-141">1920</span></span>|<span data-ttu-id="2ec6e-142">6780</span><span class="sxs-lookup"><span data-stu-id="2ec6e-142">6780</span></span>|
|<span data-ttu-id="2ec6e-143">2</span><span class="sxs-lookup"><span data-stu-id="2ec6e-143">2</span></span>|<span data-ttu-id="2ec6e-144">720</span><span class="sxs-lookup"><span data-stu-id="2ec6e-144">720</span></span>|<span data-ttu-id="2ec6e-145">1280</span><span class="sxs-lookup"><span data-stu-id="2ec6e-145">1280</span></span>|<span data-ttu-id="2ec6e-146">3520</span><span class="sxs-lookup"><span data-stu-id="2ec6e-146">3520</span></span>|
|<span data-ttu-id="2ec6e-147">3</span><span class="sxs-lookup"><span data-stu-id="2ec6e-147">3</span></span>|<span data-ttu-id="2ec6e-148">540</span><span class="sxs-lookup"><span data-stu-id="2ec6e-148">540</span></span>|<span data-ttu-id="2ec6e-149">960</span><span class="sxs-lookup"><span data-stu-id="2ec6e-149">960</span></span>|<span data-ttu-id="2ec6e-150">2210</span><span class="sxs-lookup"><span data-stu-id="2ec6e-150">2210</span></span>|
|<span data-ttu-id="2ec6e-151">4</span><span class="sxs-lookup"><span data-stu-id="2ec6e-151">4</span></span>|<span data-ttu-id="2ec6e-152">360</span><span class="sxs-lookup"><span data-stu-id="2ec6e-152">360</span></span>|<span data-ttu-id="2ec6e-153">640</span><span class="sxs-lookup"><span data-stu-id="2ec6e-153">640</span></span>|<span data-ttu-id="2ec6e-154">1150</span><span class="sxs-lookup"><span data-stu-id="2ec6e-154">1150</span></span>|
|<span data-ttu-id="2ec6e-155">5</span><span class="sxs-lookup"><span data-stu-id="2ec6e-155">5</span></span>|<span data-ttu-id="2ec6e-156">270</span><span class="sxs-lookup"><span data-stu-id="2ec6e-156">270</span></span>|<span data-ttu-id="2ec6e-157">480</span><span class="sxs-lookup"><span data-stu-id="2ec6e-157">480</span></span>|<span data-ttu-id="2ec6e-158">720</span><span class="sxs-lookup"><span data-stu-id="2ec6e-158">720</span></span>|
|<span data-ttu-id="2ec6e-159">6</span><span class="sxs-lookup"><span data-stu-id="2ec6e-159">6</span></span>|<span data-ttu-id="2ec6e-160">180</span><span class="sxs-lookup"><span data-stu-id="2ec6e-160">180</span></span>|<span data-ttu-id="2ec6e-161">320</span><span class="sxs-lookup"><span data-stu-id="2ec6e-161">320</span></span>|<span data-ttu-id="2ec6e-162">380</span><span class="sxs-lookup"><span data-stu-id="2ec6e-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="2ec6e-163">예 2</span><span class="sxs-lookup"><span data-stu-id="2ec6e-163">Example 2</span></span>
<span data-ttu-id="2ec6e-164">높이가 "720"이고 프레임 속도가 "23.970"인 원본은 5개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="2ec6e-165">계층</span><span class="sxs-lookup"><span data-stu-id="2ec6e-165">Layer</span></span>|<span data-ttu-id="2ec6e-166">높이</span><span class="sxs-lookup"><span data-stu-id="2ec6e-166">Height</span></span>|<span data-ttu-id="2ec6e-167">너비</span><span class="sxs-lookup"><span data-stu-id="2ec6e-167">Width</span></span>|<span data-ttu-id="2ec6e-168">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="2ec6e-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2ec6e-169">1</span><span class="sxs-lookup"><span data-stu-id="2ec6e-169">1</span></span>|<span data-ttu-id="2ec6e-170">720</span><span class="sxs-lookup"><span data-stu-id="2ec6e-170">720</span></span>|<span data-ttu-id="2ec6e-171">1280</span><span class="sxs-lookup"><span data-stu-id="2ec6e-171">1280</span></span>|<span data-ttu-id="2ec6e-172">2940</span><span class="sxs-lookup"><span data-stu-id="2ec6e-172">2940</span></span>|
|<span data-ttu-id="2ec6e-173">2</span><span class="sxs-lookup"><span data-stu-id="2ec6e-173">2</span></span>|<span data-ttu-id="2ec6e-174">540</span><span class="sxs-lookup"><span data-stu-id="2ec6e-174">540</span></span>|<span data-ttu-id="2ec6e-175">960</span><span class="sxs-lookup"><span data-stu-id="2ec6e-175">960</span></span>|<span data-ttu-id="2ec6e-176">1850</span><span class="sxs-lookup"><span data-stu-id="2ec6e-176">1850</span></span>|
|<span data-ttu-id="2ec6e-177">3</span><span class="sxs-lookup"><span data-stu-id="2ec6e-177">3</span></span>|<span data-ttu-id="2ec6e-178">360</span><span class="sxs-lookup"><span data-stu-id="2ec6e-178">360</span></span>|<span data-ttu-id="2ec6e-179">640</span><span class="sxs-lookup"><span data-stu-id="2ec6e-179">640</span></span>|<span data-ttu-id="2ec6e-180">960</span><span class="sxs-lookup"><span data-stu-id="2ec6e-180">960</span></span>|
|<span data-ttu-id="2ec6e-181">4</span><span class="sxs-lookup"><span data-stu-id="2ec6e-181">4</span></span>|<span data-ttu-id="2ec6e-182">270</span><span class="sxs-lookup"><span data-stu-id="2ec6e-182">270</span></span>|<span data-ttu-id="2ec6e-183">480</span><span class="sxs-lookup"><span data-stu-id="2ec6e-183">480</span></span>|<span data-ttu-id="2ec6e-184">600</span><span class="sxs-lookup"><span data-stu-id="2ec6e-184">600</span></span>|
|<span data-ttu-id="2ec6e-185">5</span><span class="sxs-lookup"><span data-stu-id="2ec6e-185">5</span></span>|<span data-ttu-id="2ec6e-186">180</span><span class="sxs-lookup"><span data-stu-id="2ec6e-186">180</span></span>|<span data-ttu-id="2ec6e-187">320</span><span class="sxs-lookup"><span data-stu-id="2ec6e-187">320</span></span>|<span data-ttu-id="2ec6e-188">320</span><span class="sxs-lookup"><span data-stu-id="2ec6e-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="2ec6e-189">예 3</span><span class="sxs-lookup"><span data-stu-id="2ec6e-189">Example 3</span></span>
<span data-ttu-id="2ec6e-190">높이가 "360"이고 프레임 속도가 "29.970"인 원본은 3개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ec6e-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="2ec6e-191">계층</span><span class="sxs-lookup"><span data-stu-id="2ec6e-191">Layer</span></span>|<span data-ttu-id="2ec6e-192">높이</span><span class="sxs-lookup"><span data-stu-id="2ec6e-192">Height</span></span>|<span data-ttu-id="2ec6e-193">너비</span><span class="sxs-lookup"><span data-stu-id="2ec6e-193">Width</span></span>|<span data-ttu-id="2ec6e-194">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="2ec6e-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="2ec6e-195">1</span><span class="sxs-lookup"><span data-stu-id="2ec6e-195">1</span></span>|<span data-ttu-id="2ec6e-196">360</span><span class="sxs-lookup"><span data-stu-id="2ec6e-196">360</span></span>|<span data-ttu-id="2ec6e-197">640</span><span class="sxs-lookup"><span data-stu-id="2ec6e-197">640</span></span>|<span data-ttu-id="2ec6e-198">700</span><span class="sxs-lookup"><span data-stu-id="2ec6e-198">700</span></span>|
|<span data-ttu-id="2ec6e-199">2</span><span class="sxs-lookup"><span data-stu-id="2ec6e-199">2</span></span>|<span data-ttu-id="2ec6e-200">270</span><span class="sxs-lookup"><span data-stu-id="2ec6e-200">270</span></span>|<span data-ttu-id="2ec6e-201">480</span><span class="sxs-lookup"><span data-stu-id="2ec6e-201">480</span></span>|<span data-ttu-id="2ec6e-202">440</span><span class="sxs-lookup"><span data-stu-id="2ec6e-202">440</span></span>|
|<span data-ttu-id="2ec6e-203">3</span><span class="sxs-lookup"><span data-stu-id="2ec6e-203">3</span></span>|<span data-ttu-id="2ec6e-204">180</span><span class="sxs-lookup"><span data-stu-id="2ec6e-204">180</span></span>|<span data-ttu-id="2ec6e-205">320</span><span class="sxs-lookup"><span data-stu-id="2ec6e-205">320</span></span>|<span data-ttu-id="2ec6e-206">230</span><span class="sxs-lookup"><span data-stu-id="2ec6e-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="2ec6e-207">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2ec6e-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2ec6e-208">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2ec6e-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2ec6e-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2ec6e-209">See Also</span></span>
[<span data-ttu-id="2ec6e-210">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="2ec6e-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

