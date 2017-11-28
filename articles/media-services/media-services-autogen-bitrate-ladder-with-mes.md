---
title: "Azure 미디어 인코더 표준 tooauto aaaUse-비트 전송률 사다리를 생성 | Microsoft Docs"
description: "이 항목에서는 방법을 toouse 미디어 인코더 표준 MES () tooauto-hello 입력된 해상도 비트 전송률에 따라 비트 전송률 사다리를 생성 합니다. hello 입력된 해상도 비트 전송률 초과 되지 않습니다. 예를 들어 hello 입력이 리디렉션되면 3Mbps, 출력 됩니다에 720p 720p, 유지 및 3Mbps 보다 낮은 요금이 시작 됩니다."
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
ms.openlocfilehash: 5437f54ac28c42ddd4f9d1986549d6da6261c5da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a><span data-ttu-id="313c5-105">Azure 미디어 인코더 표준 tooauto를 사용 하 여-비트 전송률 사다리를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-105">Use Azure Media Encoder Standard tooauto-generate a bitrate ladder</span></span>

## <a name="overview"></a><span data-ttu-id="313c5-106">개요</span><span class="sxs-lookup"><span data-stu-id="313c5-106">Overview</span></span>

<span data-ttu-id="313c5-107">이 항목에서는 방법을 toouse 미디어 인코더 표준 MES () tooauto-hello 입력된 해상도 비트 전송률 기반 비트 전송률 사다리 (비트 전송률 해상도 쌍)를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-107">This topic shows how toouse Media Encoder Standard (MES) tooauto-generate a bitrate ladder (bitrate-resolution pairs) based on hello input resolution and bitrate.</span></span> <span data-ttu-id="313c5-108">hello 자동 생성 된 사전 설정을 초과할 수 없습니다 입력 hello 해상도 비트 전송률.</span><span class="sxs-lookup"><span data-stu-id="313c5-108">hello auto-generated preset will never exceed hello input resolution and bitrate.</span></span> <span data-ttu-id="313c5-109">예를 들어 hello 입력이 리디렉션되면 3Mbps, 출력 됩니다에 720p 720p, 유지 및 3Mbps 보다 낮은 요금이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-109">For example, if hello input is 720p at 3Mbps, output will remain 720p at best, and will start at rates lower than 3Mbps.</span></span>

### <a name="encoding-for-streaming-only"></a><span data-ttu-id="313c5-110">스트리밍 전용 인코딩</span><span class="sxs-lookup"><span data-stu-id="313c5-110">Encoding for Streaming Only</span></span>

<span data-ttu-id="313c5-111">Tooencode 하려는 경우 다음 해야 "적응 스트리밍" hello를 사용 하 여 스트리밍에 대해서만 비디오 원본에는 사전 인코딩 작업을 만들 때 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-111">If your intent is tooencode your source video only for streaming, then you shoud use hello "Adaptive Streaming" preset when creating an encoding task.</span></span> <span data-ttu-id="313c5-112">Hello를 사용 하는 경우 **적응 스트리밍** 사전 설정을 hello MES 인코더는 지능적으로 캡 비트 전송률 사다리 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-112">When using hello **Adaptive Streaming** preset, hello MES encoder will intelligently cap a bitrate ladder.</span></span> <span data-ttu-id="313c5-113">그러나 비용을 인코딩 hello 서비스 레이어 toouse 개수를 결정 하므로 및 해상도에서 수 toocontrol hello 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-113">However, you will not be able toocontrol hello encoding costs, since hello service determines how many layers toouse and at what resolution.</span></span> <span data-ttu-id="313c5-114">MES hello로 인코딩한 결과 생성 되는 출력 계층의 예제를 확인할 수 **적응 스트리밍** 이 항목의 hello 끝에 미리 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-114">You can see examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset at hello end of this topic.</span></span> <span data-ttu-id="313c5-115">hello 출력 자산 오디오를 MP4 파일이 포함 될 및 비디오 인터리브되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-115">hello output Asset will contain MP4 files where audio and video are not interleaved.</span></span>

### <a name="encoding-for-streaming-and-progressive-download"></a><span data-ttu-id="313c5-116">스트리밍 및 점진적 다운로드용 인코딩</span><span class="sxs-lookup"><span data-stu-id="313c5-116">Encoding for Streaming and Progressive Download</span></span>

<span data-ttu-id="313c5-117">Tooencode 하려는 경우 다음 해야 "콘텐츠 적응 다중 비트 전송률 MP4" hello를 사용 하 여 뿐만 아니라 tooproduce MP4 파일 점진적 다운로드에 대 한 스트리밍에 대 한 원본 비디오 사전 인코딩 작업을 만들 때 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-117">If your intent is tooencode your source video for streaming as well as tooproduce MP4 files for progressive download, then you shoud use hello "Content Adaptive Multiple Bitrate MP4" preset when creating an encoding task.</span></span> <span data-ttu-id="313c5-118">Hello를 사용 하는 경우 **적응 콘텐츠 다중 비트 전송률 MP4** hello MES 인코더 hello 위의 동일 하지만 hello 출력 자산에는 MP4 포함 될 이제 동일한 인코딩 논리 오디오 위치 파일에 적용 됩니다 및 비디오를 인터리브 미리 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-118">When using hello **Content Adaptive Multiple Bitrate MP4** preset, hello MES encoder will apply hello same encoding logic as above, but now hello output asset will contain MP4 files where audio and video are interleaved.</span></span> <span data-ttu-id="313c5-119">점진적 다운로드 파일로 이러한 MP4 파일 (예를 들어 hello 가장 높은 비트 전송률 버전) 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-119">You can use one of these MP4 files (for example, hello highest bitrate version) as a progressive download file.</span></span>

## <span data-ttu-id="313c5-120"><a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩</span><span class="sxs-lookup"><span data-stu-id="313c5-120"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="313c5-121">다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-121">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

- <span data-ttu-id="313c5-122">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-122">Create an encoding job.</span></span>
- <span data-ttu-id="313c5-123">참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-123">Get a reference toohello Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="313c5-124">인코딩 작업 toohello 작업을 추가 하 고 toouse hello 지정 **적응 스트리밍** 사전 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-124">Add an encoding task toohello job and specify toouse hello **Adaptive Streaming** preset.</span></span> 
- <span data-ttu-id="313c5-125">Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-125">Create an output asset that will contain hello encoded asset.</span></span>
- <span data-ttu-id="313c5-126">이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-126">Add an event handler toocheck hello job progress.</span></span>
- <span data-ttu-id="313c5-127">Hello 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-127">Submit hello job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="313c5-128">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="313c5-128">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="313c5-129">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-129">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="313c5-130">예제</span><span class="sxs-lookup"><span data-stu-id="313c5-130">Example</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace AdaptiveStreamingMESPresest
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

## <span data-ttu-id="313c5-131"><a id="output"></a>출력</span><span class="sxs-lookup"><span data-stu-id="313c5-131"><a id="output"></a>Output</span></span>

<span data-ttu-id="313c5-132">이 섹션에서는 MES hello로 인코딩한 결과 생성 되는 출력 계층의 세 가지 예제 **적응 스트리밍** 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-132">This section shows three examples of output layers produced by MES as a result of encoding with hello **Adaptive Streaming** preset.</span></span> 

### <a name="example-1"></a><span data-ttu-id="313c5-133">예 1</span><span class="sxs-lookup"><span data-stu-id="313c5-133">Example 1</span></span>
<span data-ttu-id="313c5-134">높이가 "1080"이고 프레임 속도가 "29.970"인 원본은 6개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-134">Source with height "1080" and framerate "29.970" produces 6 video layers:</span></span>

|<span data-ttu-id="313c5-135">계층</span><span class="sxs-lookup"><span data-stu-id="313c5-135">Layer</span></span>|<span data-ttu-id="313c5-136">높이</span><span class="sxs-lookup"><span data-stu-id="313c5-136">Height</span></span>|<span data-ttu-id="313c5-137">너비</span><span class="sxs-lookup"><span data-stu-id="313c5-137">Width</span></span>|<span data-ttu-id="313c5-138">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="313c5-138">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="313c5-139">1</span><span class="sxs-lookup"><span data-stu-id="313c5-139">1</span></span>|<span data-ttu-id="313c5-140">1080</span><span class="sxs-lookup"><span data-stu-id="313c5-140">1080</span></span>|<span data-ttu-id="313c5-141">1920</span><span class="sxs-lookup"><span data-stu-id="313c5-141">1920</span></span>|<span data-ttu-id="313c5-142">6780</span><span class="sxs-lookup"><span data-stu-id="313c5-142">6780</span></span>|
|<span data-ttu-id="313c5-143">2</span><span class="sxs-lookup"><span data-stu-id="313c5-143">2</span></span>|<span data-ttu-id="313c5-144">720</span><span class="sxs-lookup"><span data-stu-id="313c5-144">720</span></span>|<span data-ttu-id="313c5-145">1280</span><span class="sxs-lookup"><span data-stu-id="313c5-145">1280</span></span>|<span data-ttu-id="313c5-146">3520</span><span class="sxs-lookup"><span data-stu-id="313c5-146">3520</span></span>|
|<span data-ttu-id="313c5-147">3</span><span class="sxs-lookup"><span data-stu-id="313c5-147">3</span></span>|<span data-ttu-id="313c5-148">540</span><span class="sxs-lookup"><span data-stu-id="313c5-148">540</span></span>|<span data-ttu-id="313c5-149">960</span><span class="sxs-lookup"><span data-stu-id="313c5-149">960</span></span>|<span data-ttu-id="313c5-150">2210</span><span class="sxs-lookup"><span data-stu-id="313c5-150">2210</span></span>|
|<span data-ttu-id="313c5-151">4</span><span class="sxs-lookup"><span data-stu-id="313c5-151">4</span></span>|<span data-ttu-id="313c5-152">360</span><span class="sxs-lookup"><span data-stu-id="313c5-152">360</span></span>|<span data-ttu-id="313c5-153">640</span><span class="sxs-lookup"><span data-stu-id="313c5-153">640</span></span>|<span data-ttu-id="313c5-154">1150</span><span class="sxs-lookup"><span data-stu-id="313c5-154">1150</span></span>|
|<span data-ttu-id="313c5-155">5</span><span class="sxs-lookup"><span data-stu-id="313c5-155">5</span></span>|<span data-ttu-id="313c5-156">270</span><span class="sxs-lookup"><span data-stu-id="313c5-156">270</span></span>|<span data-ttu-id="313c5-157">480</span><span class="sxs-lookup"><span data-stu-id="313c5-157">480</span></span>|<span data-ttu-id="313c5-158">720</span><span class="sxs-lookup"><span data-stu-id="313c5-158">720</span></span>|
|<span data-ttu-id="313c5-159">6</span><span class="sxs-lookup"><span data-stu-id="313c5-159">6</span></span>|<span data-ttu-id="313c5-160">180</span><span class="sxs-lookup"><span data-stu-id="313c5-160">180</span></span>|<span data-ttu-id="313c5-161">320</span><span class="sxs-lookup"><span data-stu-id="313c5-161">320</span></span>|<span data-ttu-id="313c5-162">380</span><span class="sxs-lookup"><span data-stu-id="313c5-162">380</span></span>|

### <a name="example-2"></a><span data-ttu-id="313c5-163">예 2</span><span class="sxs-lookup"><span data-stu-id="313c5-163">Example 2</span></span>
<span data-ttu-id="313c5-164">높이가 "720"이고 프레임 속도가 "23.970"인 원본은 5개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-164">Source with height "720" and framerate "23.970" produces 5 video layers:</span></span>

|<span data-ttu-id="313c5-165">계층</span><span class="sxs-lookup"><span data-stu-id="313c5-165">Layer</span></span>|<span data-ttu-id="313c5-166">높이</span><span class="sxs-lookup"><span data-stu-id="313c5-166">Height</span></span>|<span data-ttu-id="313c5-167">너비</span><span class="sxs-lookup"><span data-stu-id="313c5-167">Width</span></span>|<span data-ttu-id="313c5-168">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="313c5-168">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="313c5-169">1</span><span class="sxs-lookup"><span data-stu-id="313c5-169">1</span></span>|<span data-ttu-id="313c5-170">720</span><span class="sxs-lookup"><span data-stu-id="313c5-170">720</span></span>|<span data-ttu-id="313c5-171">1280</span><span class="sxs-lookup"><span data-stu-id="313c5-171">1280</span></span>|<span data-ttu-id="313c5-172">2940</span><span class="sxs-lookup"><span data-stu-id="313c5-172">2940</span></span>|
|<span data-ttu-id="313c5-173">2</span><span class="sxs-lookup"><span data-stu-id="313c5-173">2</span></span>|<span data-ttu-id="313c5-174">540</span><span class="sxs-lookup"><span data-stu-id="313c5-174">540</span></span>|<span data-ttu-id="313c5-175">960</span><span class="sxs-lookup"><span data-stu-id="313c5-175">960</span></span>|<span data-ttu-id="313c5-176">1850</span><span class="sxs-lookup"><span data-stu-id="313c5-176">1850</span></span>|
|<span data-ttu-id="313c5-177">3</span><span class="sxs-lookup"><span data-stu-id="313c5-177">3</span></span>|<span data-ttu-id="313c5-178">360</span><span class="sxs-lookup"><span data-stu-id="313c5-178">360</span></span>|<span data-ttu-id="313c5-179">640</span><span class="sxs-lookup"><span data-stu-id="313c5-179">640</span></span>|<span data-ttu-id="313c5-180">960</span><span class="sxs-lookup"><span data-stu-id="313c5-180">960</span></span>|
|<span data-ttu-id="313c5-181">4</span><span class="sxs-lookup"><span data-stu-id="313c5-181">4</span></span>|<span data-ttu-id="313c5-182">270</span><span class="sxs-lookup"><span data-stu-id="313c5-182">270</span></span>|<span data-ttu-id="313c5-183">480</span><span class="sxs-lookup"><span data-stu-id="313c5-183">480</span></span>|<span data-ttu-id="313c5-184">600</span><span class="sxs-lookup"><span data-stu-id="313c5-184">600</span></span>|
|<span data-ttu-id="313c5-185">5</span><span class="sxs-lookup"><span data-stu-id="313c5-185">5</span></span>|<span data-ttu-id="313c5-186">180</span><span class="sxs-lookup"><span data-stu-id="313c5-186">180</span></span>|<span data-ttu-id="313c5-187">320</span><span class="sxs-lookup"><span data-stu-id="313c5-187">320</span></span>|<span data-ttu-id="313c5-188">320</span><span class="sxs-lookup"><span data-stu-id="313c5-188">320</span></span>|

### <a name="example-3"></a><span data-ttu-id="313c5-189">예 3</span><span class="sxs-lookup"><span data-stu-id="313c5-189">Example 3</span></span>
<span data-ttu-id="313c5-190">높이가 "360"이고 프레임 속도가 "29.970"인 원본은 3개의 비디오 계층을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="313c5-190">Source with height "360" and framerate "29.970" produces 3 video layers:</span></span>

|<span data-ttu-id="313c5-191">계층</span><span class="sxs-lookup"><span data-stu-id="313c5-191">Layer</span></span>|<span data-ttu-id="313c5-192">높이</span><span class="sxs-lookup"><span data-stu-id="313c5-192">Height</span></span>|<span data-ttu-id="313c5-193">너비</span><span class="sxs-lookup"><span data-stu-id="313c5-193">Width</span></span>|<span data-ttu-id="313c5-194">비트 전송률(kbps)</span><span class="sxs-lookup"><span data-stu-id="313c5-194">Bitrate(kbps)</span></span>|
|---|---|---|---|
|<span data-ttu-id="313c5-195">1</span><span class="sxs-lookup"><span data-stu-id="313c5-195">1</span></span>|<span data-ttu-id="313c5-196">360</span><span class="sxs-lookup"><span data-stu-id="313c5-196">360</span></span>|<span data-ttu-id="313c5-197">640</span><span class="sxs-lookup"><span data-stu-id="313c5-197">640</span></span>|<span data-ttu-id="313c5-198">700</span><span class="sxs-lookup"><span data-stu-id="313c5-198">700</span></span>|
|<span data-ttu-id="313c5-199">2</span><span class="sxs-lookup"><span data-stu-id="313c5-199">2</span></span>|<span data-ttu-id="313c5-200">270</span><span class="sxs-lookup"><span data-stu-id="313c5-200">270</span></span>|<span data-ttu-id="313c5-201">480</span><span class="sxs-lookup"><span data-stu-id="313c5-201">480</span></span>|<span data-ttu-id="313c5-202">440</span><span class="sxs-lookup"><span data-stu-id="313c5-202">440</span></span>|
|<span data-ttu-id="313c5-203">3</span><span class="sxs-lookup"><span data-stu-id="313c5-203">3</span></span>|<span data-ttu-id="313c5-204">180</span><span class="sxs-lookup"><span data-stu-id="313c5-204">180</span></span>|<span data-ttu-id="313c5-205">320</span><span class="sxs-lookup"><span data-stu-id="313c5-205">320</span></span>|<span data-ttu-id="313c5-206">230</span><span class="sxs-lookup"><span data-stu-id="313c5-206">230</span></span>|
## <a name="media-services-learning-paths"></a><span data-ttu-id="313c5-207">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="313c5-207">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="313c5-208">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="313c5-208">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="313c5-209">참고 항목</span><span class="sxs-lookup"><span data-stu-id="313c5-209">See Also</span></span>
[<span data-ttu-id="313c5-210">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="313c5-210">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

