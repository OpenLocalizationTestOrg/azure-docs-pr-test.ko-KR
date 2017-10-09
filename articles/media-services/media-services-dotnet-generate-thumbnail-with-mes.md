---
title: "미디어 인코더 표준.NET과 함께 사용 하 여 aaaHow toogenerate 미리 보기"
description: "이 항목에서는 방법을 toouse.NET tooencode 자산 hello에 대 한 미리 보기 생성 및 사용 하 여 미디어 인코더 표준 동시 합니다."
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
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="02c39-103">어떻게 미디어 인코더 표준.NET과 함께 사용 하 여 toogenerate 미리 보기</span><span class="sxs-lookup"><span data-stu-id="02c39-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="02c39-104">사용자 입력의 비디오에서 하나 이상의 미리 보기 미디어 인코더 표준 toogenerate를 사용할 수 [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), 또는 [BMP](https://en.wikipedia.org/wiki/BMP_file_format) 이미지 파일 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="02c39-105">이미지를 생성하는 작업을 제출하거나 미리 보기 생성을 인코딩과 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="02c39-106">이 항목에는 이런 시나리오를 위해 몇 가지 예제 XML 및 JSON 미리 보기 사전 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="02c39-107">Hello hello 항목의 끝에는 한 [샘플 코드](#code_sample) toouse hello 미디어 서비스.NET SDK tooaccomplish 인코딩 작업을 hello 하는 방법을 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="02c39-108">샘플 사전 설정에 사용 되는 hello 요소에 대 한 자세한 내용은 검토 해야 [미디어 인코더 표준 스키마](media-services-mes-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="02c39-109">있는지 tooreview hello 확인 [고려 사항](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) 섹션.</span><span class="sxs-lookup"><span data-stu-id="02c39-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="02c39-110">예 – 단일 PNG 파일</span><span class="sxs-lookup"><span data-stu-id="02c39-110">Example – single PNG file</span></span>

<span data-ttu-id="02c39-111">다음 JSON hello 및 XML 사전 설정을 사용 하는 tooproduce 단일 출력 PNG 파일 hello에서 처음 몇 수 hello 인코더의 "흥미로운" 프레임을 찾는 시도 하는 최상의 노력 하면 여기서 hello 입력된 비디오의 초입니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="02c39-112">Note는 hello 출력 이미지 크기를 설정한 too100%, 즉이 hello 입력된 비디오의 hello 크기와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="02c39-113">"출력" hello "형식" 설정이 필요한 어떤가요도 참고 "PngLayers" hello "코덱" 섹션에서 toomatch hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="02c39-114">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="02c39-115">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="02c39-116">예 – 일련의 JPEG 이미지</span><span class="sxs-lookup"><span data-stu-id="02c39-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="02c39-117">다음 JSON hello 및 XML 사전 설정을 사용 하는 tooproduce 일련의 5%의 타임 스탬프에서 10 이미지 될 수 있습니다 15%, …, 여기서 hello 이미지 크기는 지정 된 toobe hello 비디오를 입력 하는 1/4 hello 입력된 타임 라인의 95%입니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="02c39-118">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="02c39-119">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="02c39-120">예 – 특정 타임스탬프의 1개 이미지</span><span class="sxs-lookup"><span data-stu-id="02c39-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="02c39-121">hello 다음 JSON과 XML 사전 설정을 사용 하는 tooproduce hello 입력된 비디오의 hello에 단일 JPEG 이미지 30 초 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="02c39-122">이 사전 설정에서는 hello 입력된 toobe 지속 시간이 30 초 이상 (다른 hello 작업이 실패 합니다.).</span><span class="sxs-lookup"><span data-stu-id="02c39-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="02c39-123">JSON 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="02c39-124">XML 사전 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-124">XML preset</span></span>
    
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

## <span data-ttu-id="02c39-125"><a id="code_sample"></a>예 – 동영상 인코드 및 미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="02c39-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="02c39-126">다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="02c39-127">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-127">Create an encoding job.</span></span>
* <span data-ttu-id="02c39-128">참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="02c39-129">부하 hello 사전 설정 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) hello 뿐만 아니라 필요한 정보를 toogenerate 축소판 그림 미리 설정 된 인코딩을 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="02c39-130">이 저장할 수 [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) 또는 [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) 파일 및 사용 하 여 hello 다음 코드 tooload hello 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="02c39-131">인코딩 작업의 단일 toohello 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="02c39-132">Hello 입력 지정 인코딩된 자산 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="02c39-133">Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="02c39-134">이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="02c39-135">Hello 작업을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-135">Submit hello job.</span></span>

<span data-ttu-id="02c39-136">Hello 참조 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md) 방법에 대 한 지침은 항목 tooset 개발 환경 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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
            // Read values from hello App.config file.
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

            // Encode and generate hello thumbnails.
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

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
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

## <span data-ttu-id="02c39-137"><a id="json"></a>미리 보기 JSON 기본 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="02c39-138">스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02c39-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="02c39-139"><a id="xml"></a>미리 보기 XML 기본 설정</span><span class="sxs-lookup"><span data-stu-id="02c39-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="02c39-140">스키마에 대한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/mt269962.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02c39-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="02c39-141">고려 사항</span><span class="sxs-lookup"><span data-stu-id="02c39-141">Considerations</span></span>
<span data-ttu-id="02c39-142">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-142">hello following considerations apply:</span></span>

* <span data-ttu-id="02c39-143">시작/단계/범위에 대 한 명시적 타임 스탬프의 hello 사용 해당 hello 입력된 소스 1 분 이상 오래을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="02c39-144">Jpg/Png/BmpImage 요소에는 시작, 단계, 범위 문자열 특성이 있으며, 이러한 특성은 다음과 같이 해석될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="02c39-145">음수가 아닌 정수인 경우 프레임 번호, 예:</span><span class="sxs-lookup"><span data-stu-id="02c39-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="02c39-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="02c39-146">"Start": "120",</span></span>
  * <span data-ttu-id="02c39-147">예: % 접미사로로 표시 하는 경우 상대 toosource 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="02c39-148">"Start": "15%", OR</span><span class="sxs-lookup"><span data-stu-id="02c39-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="02c39-149">HH:MM:SS...</span><span class="sxs-lookup"><span data-stu-id="02c39-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="02c39-150">형식.</span><span class="sxs-lookup"><span data-stu-id="02c39-150">format.</span></span> <span data-ttu-id="02c39-151">예:</span><span class="sxs-lookup"><span data-stu-id="02c39-151">Eg.</span></span> <span data-ttu-id="02c39-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="02c39-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="02c39-153">표기법을 원하는 대로 혼용하거나 일치시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="02c39-154">시작 특수 매크로 지원 되는 또한: {최고}, toodetermine hello 첫 번째 "흥미로운" 프레임 참고 hello 콘텐츠의 시도: (단계 및 범위 시작 너무 설정 된 경우 무시 됩니다 {최상의})</span><span class="sxs-lookup"><span data-stu-id="02c39-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="02c39-155">기본값: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="02c39-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="02c39-156">출력 형식 필요한 각 이미지 형식에 대해 명시적으로 제공 된 toobe: Jpg/Png/BmpFormat 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="02c39-157">있는 경우 MES JpgVideo tooJpgFormat 등과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="02c39-158">새 이미지 코덱 특정 매크로 소개: {인덱스로} 요구 toobe 있는 (한 번만 한 번)에 있는 이미지 출력 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02c39-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02c39-159">Next steps</span></span>

<span data-ttu-id="02c39-160">Hello를 확인할 수 있습니다 [진행률 작업](media-services-check-job-progress.md) 인코딩 작업 hello 하는 동안 보류 중입니다.</span><span class="sxs-lookup"><span data-stu-id="02c39-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="02c39-161">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="02c39-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="02c39-162">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="02c39-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="02c39-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="02c39-163">See Also</span></span>
[<span data-ttu-id="02c39-164">미디어 서비스 인코딩 개요</span><span class="sxs-lookup"><span data-stu-id="02c39-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

