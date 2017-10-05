---
title: "Azure Media Hyperlapse에서의 Hyperlapse 미디어 파일 | Microsoft 문서"
description: "Azure 미디어 Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만듭니다. 이 항목에서는 미디어 인덱서를 사용하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: asolanki
manager: johndeu
editor: 
ms.assetid: 37d54db6-9cf3-4ae9-b3c6-0d29c744e965
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/02/2017
ms.author: adsolank
ms.openlocfilehash: 02f634c2af04b6b372642ab0e6a17a5d29f16450
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="c6a02-104">Hyperlapse 미디어 파일 및 Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c6a02-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="c6a02-105">Azure 미디어 Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만드는 미디어 프로세서(MP)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="c6a02-106">[Microsoft Research의 데스크톱 Hyperlapse Pro 및 전화 기반 Hyperlapse 모바일](http://aka.ms/hyperlapse)에 대한 클라우드 기반 형제 제품인 Azure 미디어 서비스용 Microsoft Hyperlapse는 Azure 미디어 서비스 미디어 처리 플랫폼의 상당 부분을 활용하여 대량의 Hyperlapse 처리를 수평적으로 확장하고 병렬 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-106">The cloud-based sibling to [Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes the massive scale of the Azure Media Services Media Processing platform to horizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6a02-107">Microsoft Hyperlapse는 이동 카메라를 사용한 1인칭 콘텐츠에 최적으로 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-107">Microsoft Hyperlapse is designed to work best on first-person content with a moving camera.</span></span>  <span data-ttu-id="c6a02-108">스틸 카메라 영상에도 작동할 수 있지만 다른 형식의 콘텐츠에서는 Azure 미디어 Hyperlapse 미디어 프로세서의 성능 및 품질을 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-108">Although still-camera footage can still work, the performance and quality of the Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="c6a02-109">Azure 미디어 서비스용 Microsoft Hyperlapse에 대해 자세히 알아보고 예제 비디오를 보려면 공개 미리 보기 상태인 [소개 블로그 게시물](http://aka.ms/azurehyperlapseblog) 을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c6a02-109">To learn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out the [introductory blog post](http://aka.ms/azurehyperlapseblog) from the public preview.</span></span>
> 
> 

<span data-ttu-id="c6a02-110">Azure 미디어 Hyperlapse 작업은 MP4, MOV 또는 WMV 자산 파일 및 어떤 비디오 프레임을 어떤 속도로 시간 경과시킬지 지정(예: 2배속으로 처음 10,000프레임)하는 구성 파일을 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and to what speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="c6a02-111">출력은 입력 비디오의 안정화되고 시간 경과된 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-111">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

<span data-ttu-id="c6a02-112">최신 Azure 미디어 Hyperlapse 업데이트는 [미디어 서비스 블로그](https://azure.microsoft.com/blog/topics/media-services/)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6a02-112">For the latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="c6a02-113">자산 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c6a02-113">Hyperlapse an asset</span></span>
<span data-ttu-id="c6a02-114">먼저 원하는 입력 파일을 Azure 미디어 서비스로 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-114">First you will need to upload your desired input file to Azure Media Services.</span></span>  <span data-ttu-id="c6a02-115">콘텐츠 업로드 및 관리와 관련된 개념에 대해 자세히 알아보려면 [콘텐츠 관리 문서](media-services-portal-vod-get-started.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c6a02-115">To learn more about the concepts involved with uploading and managing content, read the [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="c6a02-116"><a id="configuration"></a>Hyperlapse에 대한 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="c6a02-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="c6a02-117">콘텐츠가 미디어 서비스 계정에 있는 경우 구성 사전 설정을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-117">Once your content is in your Media Services account, you will need to construct your configuration preset.</span></span>  <span data-ttu-id="c6a02-118">다음 표에서는 사용자 지정 필드에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-118">The following table explains the user-specified fields:</span></span>

| <span data-ttu-id="c6a02-119">필드</span><span class="sxs-lookup"><span data-stu-id="c6a02-119">Field</span></span> | <span data-ttu-id="c6a02-120">설명</span><span class="sxs-lookup"><span data-stu-id="c6a02-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6a02-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="c6a02-121">StartFrame</span></span> |<span data-ttu-id="c6a02-122">Microsoft Hyperlapse 처리를 시작할 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-122">The frame upon which the Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="c6a02-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="c6a02-123">NumFrames</span></span> |<span data-ttu-id="c6a02-124">처리할 프레임 수</span><span class="sxs-lookup"><span data-stu-id="c6a02-124">The number of frames to process</span></span> |
| <span data-ttu-id="c6a02-125">속도</span><span class="sxs-lookup"><span data-stu-id="c6a02-125">Speed</span></span> |<span data-ttu-id="c6a02-126">입력 비디오를 가속화하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-126">The factor with which to speed up the input video.</span></span> |

<span data-ttu-id="c6a02-127">다음은 XML 및 JSON에서 규칙을 따르는 구성 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-127">The following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="c6a02-128">**XML 사전 설정:**</span><span class="sxs-lookup"><span data-stu-id="c6a02-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="c6a02-129">**JSON 사전 설정:**</span><span class="sxs-lookup"><span data-stu-id="c6a02-129">**JSON preset:**</span></span>

    {
        "Version":1.0,
        "Sources": [
            {
                "StartFrame":0,
                "NumFrames":2147483647
            }
        ],
        "Options": {
            "Speed":1,
            "Stabilize":false
        }
    }

### <span data-ttu-id="c6a02-130"><a id="sample_code"></a> Microsoft Hyperlapse 및 AMS .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c6a02-130"><a id="sample_code"></a> Microsoft Hyperlapse with the AMS .NET SDK</span></span>
<span data-ttu-id="c6a02-131">다음 메서드는 미디어 파일을 자산으로 업로드하고 Azure 미디어 Hyperlapse 미디어 프로세서로 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-131">The following method uploads a media file as an asset and creates a job with the Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="c6a02-132">이 코드가 작동하도록 하려면 "context" 이름의 범위에 CloudMediaContext가 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-132">You should already have a CloudMediaContext in scope with the name "context" for this code to work.</span></span>  <span data-ttu-id="c6a02-133">이에 대한 자세히 알아보려면 [콘텐츠 관리 문서](media-services-dotnet-get-started.md)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c6a02-133">To learn more about this, read the [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="c6a02-134">문자열 인수 "hyperConfig"가 위에 설명된 대로 JSON 또는 XML에서 규칙을 따르는 구성 사전 설정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6a02-134">The string argument "hyperConfig" is expected to be a conformant configuration preset in either JSON or XML as described above.</span></span>
> 
> 

        static bool RunHyperlapseJob(string input, string output, string hyperConfig)
        {
            // create asset with input file
            IAsset asset = context
            .Assets
            .CreateAssetAndUploadSingleFile(input, "My Hyperlapse Input", AssetCreationOptions.None);

            // grab instances of Azure Media Hyperlapse MP
            IMediaProcessor mp = context
            .MediaProcessors
            .GetLatestMediaProcessorByName("Azure Media Hyperlapse");

            // create Job with Hyperlapse task
            IJob job = context
            .Jobs
            .Create(String.Format("Hyperlapse {0}", input));

            if (String.IsNullOrEmpty(hyperConfig))
            {
            // config cannot be empty
            return false;
            }

            hyperConfig = File.ReadAllText(hyperConfig);

            ITask hyperlapseTask = job.Tasks.AddNew("Hyperlapse task",
            mp,
            hyperConfig,
            TaskOptions.None);
            hyperlapseTask.InputAssets.Add(asset);
            hyperlapseTask.OutputAssets.AddNew("Hyperlapse output",
            AssetCreationOptions.None);

            job.Submit();

            // Create progress printing and querying tasks
            Task progressPrintTask = new Task(() =>
            {

            IJob jobQuery = null;
            do
            {
                var progressContext = context;
                jobQuery = progressContext.Jobs
                .Where(j => j.Id == job.Id)
                .First();
                Console.WriteLine(string.Format("{0}\t{1}\t{2}",
                DateTime.Now,
                jobQuery.State,
                jobQuery.Tasks[0].Progress));
                Thread.Sleep(10000);
            }
            while (jobQuery.State != JobState.Finished &&
                                   jobQuery.State != JobState.Error &&
                                   jobQuery.State != JobState.Canceled);
                });
                
            progressPrintTask.Start();

            Task progressJobTask = job.GetExecutionProgressTask(
                                                 CancellationToken.None);
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
                return false;                  
            }

        DownloadAsset(job.OutputMediaAssets.First(), output);
        return true;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }


    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }

### <span data-ttu-id="c6a02-135"><a id="file_types"></a>지원되는 파일 형식</span><span class="sxs-lookup"><span data-stu-id="c6a02-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="c6a02-136">MP4</span><span class="sxs-lookup"><span data-stu-id="c6a02-136">MP4</span></span>
* <span data-ttu-id="c6a02-137">MOV</span><span class="sxs-lookup"><span data-stu-id="c6a02-137">MOV</span></span>
* <span data-ttu-id="c6a02-138">WMV</span><span class="sxs-lookup"><span data-stu-id="c6a02-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c6a02-139">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="c6a02-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6a02-140">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c6a02-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c6a02-141">관련 링크</span><span class="sxs-lookup"><span data-stu-id="c6a02-141">Related links</span></span>
[<span data-ttu-id="c6a02-142">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="c6a02-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c6a02-143">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="c6a02-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

