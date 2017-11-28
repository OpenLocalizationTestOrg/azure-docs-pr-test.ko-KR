---
title: "Azure Media Hyperlapse를 사용 하 여 미디어 파일 aaaHyperlapse | Microsoft Docs"
description: "Azure 미디어 Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만듭니다. 이 항목에서는 방법을 toouse Media Indexer 합니다."
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
ms.openlocfilehash: 85bb07206d0ca2f5b2fd0767e6ed4904195d3ab6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hyperlapse-media-files-with-azure-media-hyperlapse"></a><span data-ttu-id="f6117-104">Hyperlapse 미디어 파일 및 Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="f6117-104">Hyperlapse Media Files with Azure Media Hyperlapse</span></span>
<span data-ttu-id="f6117-105">Azure 미디어 Hyperlapse는 1인칭 또는 액션 카메라 콘텐츠에서 부드러운 시간 경과 비디오를 만드는 미디어 프로세서(MP)입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-105">Azure Media Hyperlapse is a Media Processor (MP) that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="f6117-106">클라우드 기반 형제 너무 hello[Microsoft Research 데스크톱 Hyperlapse Pro 및 전화 기반 Hyperlapse Mobile](http://aka.ms/hyperlapse), Azure 미디어 서비스에 대 한 Microsoft Hyperlapse hello 대규모의 hello Azure 미디어 서비스 미디어를 활용 합니다. 확장 및 병렬화 대량 플랫폼 toohorizontally 처리 Hyperlapse 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-106">hello cloud-based sibling too[Microsoft Research's desktop Hyperlapse Pro and phone-based Hyperlapse Mobile](http://aka.ms/hyperlapse), Microsoft Hyperlapse for Azure Media Services utilizes hello massive scale of hello Azure Media Services Media Processing platform toohorizontally scale and parallelize bulk Hyperlapse processing.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6117-107">Microsoft Hyperlapse 이동 카메라와 함께 첫 번째 사람 내용에 가장 좋은 디자인 된 toowork입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-107">Microsoft Hyperlapse is designed toowork best on first-person content with a moving camera.</span></span>  <span data-ttu-id="f6117-108">여전히 카메라 장면 작업 계속할 수 있지만 다른 콘텐츠 형식의 대 한 hello Azure Media Hyperlapse 미디어 프로세서의 hello 성능 및 품질을 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-108">Although still-camera footage can still work, hello performance and quality of hello Azure Media Hyperlapse Media Processor cannot be guaranteed for other types of content.</span></span>  <span data-ttu-id="f6117-109">Azure 미디어 서비스에 대 한 Microsoft Hyperlapse에 대 한 자세한 toolearn 몇 가지 예제 비디오를 참조 하 고 hello를 확인 하십시오 [소개 블로그 게시물](http://aka.ms/azurehyperlapseblog) hello 공개 미리 보기에서.</span><span class="sxs-lookup"><span data-stu-id="f6117-109">toolearn more about Microsoft Hyperlapse for Azure Media Services and see some example videos, check out hello [introductory blog post](http://aka.ms/azurehyperlapseblog) from hello public preview.</span></span>
> 
> 

<span data-ttu-id="f6117-110">작업으로 사용 하는 Azure Media Hyperlapse 입력 된 경과 된 시간 프레임의 비디오 되어야 지정 하는 구성 파일 및 toowhat 속도 함께 MP4, MOV, 또는 WMV 자산 파일 (예: 첫 번째 10000 2 x에서 프레임).</span><span class="sxs-lookup"><span data-stu-id="f6117-110">An Azure Media Hyperlapse job takes as input an MP4, MOV, or WMV asset file along with a configuration file that specifies which frames of video should be time-lapsed and toowhat speed (e.g. first 10,000 frames at 2x).</span></span>  <span data-ttu-id="f6117-111">hello 출력은 hello 입력된 비디오의 안정화 및 된 경과 된 시간 변환을입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-111">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

<span data-ttu-id="f6117-112">최신 Azure Media Hyperlapse 업데이트 hello에 대 한 참조 [미디어 서비스 블로그](https://azure.microsoft.com/blog/topics/media-services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-112">For hello latest Azure Media Hyperlapse updates, see [Media Services blogs](https://azure.microsoft.com/blog/topics/media-services/).</span></span>

## <a name="hyperlapse-an-asset"></a><span data-ttu-id="f6117-113">자산 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="f6117-113">Hyperlapse an asset</span></span>
<span data-ttu-id="f6117-114">먼저 해야 tooupload 프로그램 원하는 입력된 파일 tooAzure 미디어 서비스.</span><span class="sxs-lookup"><span data-stu-id="f6117-114">First you will need tooupload your desired input file tooAzure Media Services.</span></span>  <span data-ttu-id="f6117-115">hello 읽기에 대해 더 알아봅니다 toolearn hello 업로드, 콘텐츠 관리와 관련 된 개념 [콘텐츠 관리 문서](media-services-portal-vod-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-115">toolearn more about hello concepts involved with uploading and managing content, read hello [content management article](media-services-portal-vod-get-started.md).</span></span>

### <span data-ttu-id="f6117-116"><a id="configuration"></a>Hyperlapse에 대한 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="f6117-116"><a id="configuration"></a>Configuration Preset for Hyperlapse</span></span>
<span data-ttu-id="f6117-117">미디어 서비스 계정에 콘텐츠를 tooconstruct 구성 사전 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-117">Once your content is in your Media Services account, you will need tooconstruct your configuration preset.</span></span>  <span data-ttu-id="f6117-118">다음 표에서 hello hello 사용자 지정 필드를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-118">hello following table explains hello user-specified fields:</span></span>

| <span data-ttu-id="f6117-119">필드</span><span class="sxs-lookup"><span data-stu-id="f6117-119">Field</span></span> | <span data-ttu-id="f6117-120">설명</span><span class="sxs-lookup"><span data-stu-id="f6117-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6117-121">StartFrame</span><span class="sxs-lookup"><span data-stu-id="f6117-121">StartFrame</span></span> |<span data-ttu-id="f6117-122">어떤 hello Microsoft Hyperlapse 처리를 시작 하는 hello 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-122">hello frame upon which hello Microsoft Hyperlapse processing should begin.</span></span> |
| <span data-ttu-id="f6117-123">NumFrames</span><span class="sxs-lookup"><span data-stu-id="f6117-123">NumFrames</span></span> |<span data-ttu-id="f6117-124">프레임 tooprocess hello 수</span><span class="sxs-lookup"><span data-stu-id="f6117-124">hello number of frames tooprocess</span></span> |
| <span data-ttu-id="f6117-125">속도</span><span class="sxs-lookup"><span data-stu-id="f6117-125">Speed</span></span> |<span data-ttu-id="f6117-126">hello 비율 hello 입력된 비디오를 어떤 toospeed로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-126">hello factor with which toospeed up hello input video.</span></span> |

<span data-ttu-id="f6117-127">hello 다음은 XML과 JSON와 호환 되 구성 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-127">hello following is an example of a conformant configuration file in XML and JSON:</span></span>

<span data-ttu-id="f6117-128">**XML 사전 설정:**</span><span class="sxs-lookup"><span data-stu-id="f6117-128">**XML preset:**</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
        <Sources>
            <Source StartFrame="0" NumFrames="10000" />
        </Sources>
        <Options>
            <Speed>12</Speed>
        </Options>
    </Preset>

<span data-ttu-id="f6117-129">**JSON 사전 설정:**</span><span class="sxs-lookup"><span data-stu-id="f6117-129">**JSON preset:**</span></span>

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

### <span data-ttu-id="f6117-130"><a id="sample_code"></a>Hello AMS.NET SDK와 Microsoft Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="f6117-130"><a id="sample_code"></a> Microsoft Hyperlapse with hello AMS .NET SDK</span></span>
<span data-ttu-id="f6117-131">hello 다음 미디어 파일을 자산으로 업로드 메서드와 hello Azure Media Hyperlapse 미디어 프로세서를 사용 하 여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-131">hello following method uploads a media file as an asset and creates a job with hello Azure Media Hyperlapse Media Processor.</span></span>

> [!NOTE]
> <span data-ttu-id="f6117-132">이 코드 toowork에 대 한 컨텍스트"hello 이름"을 사용 하 여 범위에는 CloudMediaContext 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-132">You should already have a CloudMediaContext in scope with hello name "context" for this code toowork.</span></span>  <span data-ttu-id="f6117-133">이 읽기 hello에 대 한 자세한 toolearn [콘텐츠 관리 문서](media-services-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-133">toolearn more about this, read hello [content management article](media-services-dotnet-get-started.md).</span></span>
> 
> [!NOTE]
> <span data-ttu-id="f6117-134">hello 문자열 인수 "hyperConfig" 예상된 toobe JSON 또는 위에 설명 된 대로 XML에 맞는 구성 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f6117-134">hello string argument "hyperConfig" is expected toobe a conformant configuration preset in either JSON or XML as described above.</span></span>
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

            // If job state is Error, hello event handling
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

### <span data-ttu-id="f6117-135"><a id="file_types"></a>지원되는 파일 형식</span><span class="sxs-lookup"><span data-stu-id="f6117-135"><a id="file_types"></a>Supported File types</span></span>
* <span data-ttu-id="f6117-136">MP4</span><span class="sxs-lookup"><span data-stu-id="f6117-136">MP4</span></span>
* <span data-ttu-id="f6117-137">MOV</span><span class="sxs-lookup"><span data-stu-id="f6117-137">MOV</span></span>
* <span data-ttu-id="f6117-138">WMV</span><span class="sxs-lookup"><span data-stu-id="f6117-138">WMV</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f6117-139">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f6117-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f6117-140">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f6117-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="f6117-141">관련 링크</span><span class="sxs-lookup"><span data-stu-id="f6117-141">Related links</span></span>
[<span data-ttu-id="f6117-142">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="f6117-142">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="f6117-143">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="f6117-143">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

