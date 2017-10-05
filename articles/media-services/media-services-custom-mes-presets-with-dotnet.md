---
title: "Media Encoder Standard 사전 설정 사용자 지정 | Microsoft Docs"
description: "이 항목에서는 미디어 인코더 표준 태스크 사전 설정을 사용자 지정하여 고급 인코딩을 수행하는 방법을 설명합니다. 그리고 Media Services .NET SDK를 사용하여 인코딩 태스크와 작업을 만드는 방법을 설명합니다. 또한 인코딩 작업에 사용자 지정 사전 설정을 제공하는 방법을 보여줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec95392f-d34a-4c22-a6df-5274eaac445b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: b4d25f07349043da8cb745930fde3371c98f9960
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="customizing-media-encoder-standard-presets"></a><span data-ttu-id="0871d-105">Media Encoder Standard 사전 설정 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0871d-105">Customizing Media Encoder Standard presets</span></span>

## <a name="overview"></a><span data-ttu-id="0871d-106">개요</span><span class="sxs-lookup"><span data-stu-id="0871d-106">Overview</span></span>

<span data-ttu-id="0871d-107">이 항목에서는 사용자 지정 사전 설정을 사용하여 MES(Media Encoder Standard)에서 고급 인코딩을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-107">This topic shows how to perform advanced encoding with Media Encoder Standard (MES) using a custom preset.</span></span> <span data-ttu-id="0871d-108">여기서는 .NET을 사용하여 인코딩 태스크 및 이 태스크를 실행하는 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-108">The topic uses .NET to create an encoding task and a job that executes this task.</span></span>  

<span data-ttu-id="0871d-109">이 항목에서는 [H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md)(영문) 사전 설정을 사용하고 레이어 수를 줄여 사전 설정을 사용자 지정하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-109">In this topic you will see how to customize a preset by taking the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) preset and reducing the number of layers.</span></span> <span data-ttu-id="0871d-110">[Media Encoder Standard 사전 설정 사용자 지정](media-services-advanced-encoding-with-mes.md) 항목에서는 고급 인코딩 작업을 수행하는 데 사용할 수 있는 사전 설정 사용자 지정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-110">The [Customizing Media Encoder Standard presets](media-services-advanced-encoding-with-mes.md) topic demonstrates custom presets that can be used to perform advanced encoding tasks.</span></span>

## <span data-ttu-id="0871d-111"><a id="customizing_presets"></a> MES 사전 설정 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0871d-111"><a id="customizing_presets"></a> Customizing a MES preset</span></span>

### <a name="original-preset"></a><span data-ttu-id="0871d-112">원래 사전 설정</span><span class="sxs-lookup"><span data-stu-id="0871d-112">Original preset</span></span>

<span data-ttu-id="0871d-113">[H264 다중 비트 전송률 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) 항목에서 정의한 JSON을 .json 확장명의 일부 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-113">Save the JSON defined in the [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) topic in some file with .json extension.</span></span> <span data-ttu-id="0871d-114">예를 들어 **CustomPreset_JSON.json**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-114">For example, **CustomPreset_JSON.json**.</span></span>

### <a name="customized-preset"></a><span data-ttu-id="0871d-115">사용자 지정한 사전 설정</span><span class="sxs-lookup"><span data-stu-id="0871d-115">Customized preset</span></span>

<span data-ttu-id="0871d-116">**CustomPreset_JSON.json** 파일을 열고 다음과 같이 보이도록 **H264Layers**에서 처음 세 개의 레이어를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-116">Open the **CustomPreset_JSON.json** file and remove first three layers from **H264Layers** so your file looks like this.</span></span>

    
    {  
      "Version": 1.0,  
      "Codecs": [  
        {  
          "KeyFrameInterval": "00:00:02",  
          "H264Layers": [  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 1000,  
              "MaxBitrate": 1000,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 650,  
              "MaxBitrate": 650,  
              "BufferWindow": "00:00:05",  
              "Width": 640,  
              "Height": 360,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            },  
            {  
              "Profile": "Auto",  
              "Level": "auto",  
              "Bitrate": 400,  
              "MaxBitrate": 400,  
              "BufferWindow": "00:00:05",  
              "Width": 320,  
              "Height": 180,  
              "BFrames": 3,  
              "ReferenceFrames": 3,  
              "AdaptiveBFrame": true,  
              "Type": "H264Layer",  
              "FrameRate": "0/1"  
            }  
          ],  
          "Type": "H264Video"  
        },  
        {  
          "Profile": "AACLC",  
          "Channels": 2,  
          "SamplingRate": 48000,  
          "Bitrate": 128,  
          "Type": "AACAudio"  
        }  
      ],  
      "Outputs": [  
        {  
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
          "Format": {  
            "Type": "MP4Format"  
          }  
        }  
      ]  
    }  
    

## <span data-ttu-id="0871d-117"><a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩</span><span class="sxs-lookup"><span data-stu-id="0871d-117"><a id="encoding_with_dotnet"></a>Encoding with Media Services .NET SDK</span></span>

<span data-ttu-id="0871d-118">다음 코드 예제에서는 미디어 서비스 .NET SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-118">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="0871d-119">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-119">Create an encoding job.</span></span>
- <span data-ttu-id="0871d-120">미디어 인코더 표준 인코더에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-120">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="0871d-121">이전 섹션에서 만든 사용자 지정 JSON 사전 설정을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-121">Load the custom JSON preset that you created in the previous section.</span></span> 
  
        // Load the JSON from the local file.
        string configuration = File.ReadAllText(fileName);  

- <span data-ttu-id="0871d-122">작업에 인코딩 작업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-122">Add an encoding task to the job.</span></span> 
- <span data-ttu-id="0871d-123">인코딩할 입력 자산을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-123">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="0871d-124">인코딩된 자산을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-124">Create an output asset that will contain the encoded asset.</span></span>
- <span data-ttu-id="0871d-125">작업 진행 상태를 확인할 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-125">Add an event handler to check the job progress.</span></span>
- <span data-ttu-id="0871d-126">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-126">Submit the job.</span></span>
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0871d-127">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="0871d-127">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0871d-128">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0871d-128">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0871d-129">예제</span><span class="sxs-lookup"><span data-stu-id="0871d-129">Example</span></span>   

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;

    namespace CustomizeMESPresests
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

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the output using custom presets.
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

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("CustomPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="0871d-130">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="0871d-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0871d-131">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="0871d-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0871d-132">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0871d-132">See Also</span></span>
[<span data-ttu-id="0871d-133">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="0871d-133">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

