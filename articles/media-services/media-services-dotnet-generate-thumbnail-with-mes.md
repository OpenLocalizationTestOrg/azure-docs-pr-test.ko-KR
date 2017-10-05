---
title: ".NET과 함께 미디어 인코더 표준을 사용하여 미리 보기를 생성하는 방법"
description: "이 항목에서는 .NET과 함께 Media Encoder Standard를 사용하여 동시에 자산을 인코드하고 미리 보기를 생성하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="3507b-103">.NET과 함께 미디어 인코더 표준을 사용하여 미리 보기를 생성하는 방법</span><span class="sxs-lookup"><span data-stu-id="3507b-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="3507b-104">Media Encoder Standard를 사용하여 입력 동영상에서 하나 이상의 미리 보기를 [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) 또는 [BMP](https://en.wikipedia.org/wiki/BMP_file_format) 이미지 파일 형식으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="3507b-105">이미지를 생성하는 작업을 제출하거나 미리 보기 생성을 인코딩과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="3507b-106">이 항목에는 이런 시나리오를 위해 몇 가지 예제 XML 및 JSON 미리 보기 사전 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="3507b-107">항목 끝에는 Media Services .NET SDK를 사용하여 인코딩 작업을 완료하는 방법을 보여 주는 [예제 코드](#code_sample)가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="3507b-108">예제 사전 설정에 사용되는 요소에 대한 자세한 내용은 [Media Encoder Standard 스키마](media-services-mes-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3507b-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="3507b-109">[고려 사항](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) 섹션을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="3507b-110">예 – 단일 PNG 파일</span><span class="sxs-lookup"><span data-stu-id="3507b-110">Example – single PNG file</span></span>

<span data-ttu-id="3507b-111">다음 JSON 및 XML 기본 설정은 입력 동영상의 첫 몇 초 분량에서 단일 출력 PNG 파일을 생성하는 데 사용할 수 있습니다. 여기서 인코더는 “흥미로운” 프레임을 찾기 위해 최상의 노력을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="3507b-112">출력 이미지 크기는 100%로 설정되어 있습니다. 다시 말해서, 입력 동영상과 크기와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="3507b-113">또한 “Outputs”의 “Format” 설정이 “Codecs” 섹션의 “PngLayers” 사용과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="3507b-114">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="3507b-115">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="3507b-116">예 – 일련의 JPEG 이미지</span><span class="sxs-lookup"><span data-stu-id="3507b-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="3507b-117">다음 JSON 및 XML 기본 설정은 입력 타임라인의 타임스탬프 5%, 15%, …, 95%에서 일련의 10개의 이미지를 생성하는 데 사용할 수 있습니다. 여기서 이미지 크기는 입력 동영상의 1/4로 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="3507b-118">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="3507b-119">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="3507b-120">예 – 특정 타임스탬프의 1개 이미지</span><span class="sxs-lookup"><span data-stu-id="3507b-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="3507b-121">다음 JSON 및 XML 기본 설정은 입력 동영상의 30초 마크에 단일 JPEG 이미지를 생성하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="3507b-122">이 사전 설정에서는 입력 데이터가 30초를 넘을 것으로 예상합니다(그렇지 않으면 작업이 실패함).</span><span class="sxs-lookup"><span data-stu-id="3507b-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="3507b-123">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="3507b-124">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="3507b-125"><a id="code_sample"></a>예 – 동영상 인코드 및 미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="3507b-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="3507b-126">다음 코드 예제에서는 미디어 서비스 .NET SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="3507b-127">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-127">Create an encoding job.</span></span>
* <span data-ttu-id="3507b-128">미디어 인코더 표준 인코더에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="3507b-129">미리 보기를 생성하는 데 필요한 정보 및 Encoding 기본 설정이 포함된 기본 설정 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="3507b-130">이 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)을 파일에 저장하고 다음 코드를 사용하여 파일을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="3507b-131">작업에 단일 인코딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="3507b-132">인코딩할 입력 자산을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="3507b-133">인코딩된 자산을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="3507b-134">작업 진행 상태를 확인할 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="3507b-135">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-135">Submit the job.</span></span>

<span data-ttu-id="3507b-136">개발 환경을 설정하는 방법에 대한 지침은 [.NET을 사용한 Media Services 개발](media-services-dotnet-how-to-use.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3507b-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

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

            // Encode and generate the thumbnails.
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
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

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

## <span data-ttu-id="3507b-137"><a id="json"></a>미리 보기 JSON 기본 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="3507b-138">스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3507b-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
    
            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="3507b-139"><a id="xml"></a>미리 보기 XML 기본 설정</span><span class="sxs-lookup"><span data-stu-id="3507b-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="3507b-140">스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3507b-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="3507b-141">고려 사항</span><span class="sxs-lookup"><span data-stu-id="3507b-141">Considerations</span></span>
<span data-ttu-id="3507b-142">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-142">The following considerations apply:</span></span>

* <span data-ttu-id="3507b-143">시작/단계/범위에 대한 명시적 타임스탬프 사용 시 입력 소스의 길이가 1분 이상이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="3507b-144">Jpg/Png/BmpImage 요소에는 시작, 단계, 범위 문자열 특성이 있으며, 이러한 특성은 다음과 같이 해석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="3507b-145">음수가 아닌 정수인 경우 프레임 번호, 예:</span><span class="sxs-lookup"><span data-stu-id="3507b-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="3507b-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="3507b-146">"Start": "120",</span></span>
  * <span data-ttu-id="3507b-147">% 접미사로 표시된 경우 원본 기간 기준, 예:</span><span class="sxs-lookup"><span data-stu-id="3507b-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="3507b-148">"Start": "15%", OR</span><span class="sxs-lookup"><span data-stu-id="3507b-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="3507b-149">HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="3507b-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="3507b-150">형식.</span><span class="sxs-lookup"><span data-stu-id="3507b-150">format.</span></span> <span data-ttu-id="3507b-151">예:</span><span class="sxs-lookup"><span data-stu-id="3507b-151">Eg.</span></span> <span data-ttu-id="3507b-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="3507b-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="3507b-153">표기법을 원하는 대로 혼용하거나 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="3507b-154">또한 Start는 콘텐츠의 첫 번째 "흥미로운" 프레임의 결정을 시도하는 특수 Macro:{Best}를 지원합니다. 참고: (Step 및 Range는 Start를 {Best}로 설정하면 무시됨)</span><span class="sxs-lookup"><span data-stu-id="3507b-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="3507b-155">기본값: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="3507b-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="3507b-156">각 이미지 형식에 대해 출력 형식을 명시적으로 제공해야 합니다. Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="3507b-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="3507b-157">있는 경우 MES는 JpgFormat을 JpgVideo에 일치시키는 식으로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="3507b-158">OutputFormat은 새 이미지 코덱 특유의 Macro: {Index}를 도입하며, 이는 이미지 출력 형식에 대해 존재해야(한 번만) 합니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3507b-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3507b-159">Next steps</span></span>

<span data-ttu-id="3507b-160">인코딩 작업이 보류 중인 동안 [작업 진행 상태](media-services-check-job-progress.md)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3507b-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3507b-161">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="3507b-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3507b-162">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="3507b-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="3507b-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3507b-163">See Also</span></span>
[<span data-ttu-id="3507b-164">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="3507b-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

