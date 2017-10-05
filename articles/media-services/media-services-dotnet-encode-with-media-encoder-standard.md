---
title: ".NET을 사용하여 Media Encoder Standard로 자산 인코딩 | Microsoft 문서"
description: "이 항목에서는 .NET을 사용하여 미디어 인코더 표준으로 자산을 인코딩하는 방법을 설명합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 03431b64-5518-478a-a1c2-1de345999274
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 929592368501c54277748bf46b2160c9058db3fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a><span data-ttu-id="58729-103">.NET을 사용하여 미디어 인코더 표준으로 자산 인코딩</span><span class="sxs-lookup"><span data-stu-id="58729-103">Encode an asset with Media Encoder Standard using .NET</span></span>
<span data-ttu-id="58729-104">인코딩 작업은 미디어 서비스에서 가장 일반적인 처리 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="58729-104">Encoding jobs are one of the most common processing operations in Media Services.</span></span> <span data-ttu-id="58729-105">인코딩 작업을 만들어 한 인코딩에서 다른 인코딩으로 미디어 파일을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-105">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="58729-106">인코딩할 때는 미디어 서비스 기본 제공 미디어 인코더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-106">When you encode, you can use the Media Services built-in Media Encoder.</span></span> <span data-ttu-id="58729-107">또한 미디어 서비스 파트너가 제공하는 인코더를 사용할 수도 있습니다. 타사 인코더는 Azure 마켓플레이스를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-107">You can also use an encoder provided by a Media Services partner; third party encoders are available through the Azure Marketplace.</span></span> 

<span data-ttu-id="58729-108">이 항목에서는 .NET을 사용하여 MES(미디어 인코더 표준)로 자산을 인코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-108">This topic shows how to use .NET to encode your assets with Media Encoder Standard (MES).</span></span> <span data-ttu-id="58729-109">미디어 인코더 표준은 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)에서 설명한 인코더 기본 설정 중 하나를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-109">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

<span data-ttu-id="58729-110">항상 원본 파일을 적응 비트 전송률 MP4 집합으로 인코딩한 다음 [동적 패키징](media-services-dynamic-packaging-overview.md)을 사용하여 원하는 형식으로 집합을 변환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-110">It is recommended to always encode your source files into an adaptive bitrate MP4 set and then convert the set to the desired format using the [Dynamic Packaging](media-services-dynamic-packaging-overview.md).</span></span> 

<span data-ttu-id="58729-111">출력 자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-111">If your output asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="58729-112">자세한 내용은 [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58729-112">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58729-113">MES는 입력 파일 이름의 처음 32개 문자를 포함하는 이름을 가진 출력 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-113">MES produces an output file with a name that contains the first 32 characters of the input file name.</span></span> <span data-ttu-id="58729-114">이름은 미리 설정된 파일에 지정된 내용에 기반합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-114">The name is based on what is specified in the preset file.</span></span> <span data-ttu-id="58729-115">예를 들어 "FileName": "{Basename}_{Index}{Extension}"과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-115">For example, "FileName": "{Basename}_{Index}{Extension}".</span></span> <span data-ttu-id="58729-116">{Basename}은 입력 파일 이름의 처음 32자로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-116">{Basename} is replaced by the first 32 characters of the input file name.</span></span>
> 
> 

### <a name="mes-formats"></a><span data-ttu-id="58729-117">MES 형식</span><span class="sxs-lookup"><span data-stu-id="58729-117">MES Formats</span></span>
[<span data-ttu-id="58729-118">형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="58729-118">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a><span data-ttu-id="58729-119">MES 기본 설정</span><span class="sxs-lookup"><span data-stu-id="58729-119">MES Presets</span></span>
<span data-ttu-id="58729-120">미디어 인코더 표준은 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)에서 설명한 인코더 기본 설정 중 하나를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-120">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="58729-121">입력 및 출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="58729-121">Input and output metadata</span></span>
<span data-ttu-id="58729-122">MES를 사용하여 입력 자산을 인코딩하는 경우 인코딩 작업이 성공적으로 완료되면 출력 자산을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-122">When you encode an input asset (or assets) using MES, you get an output asset at the successful completion of that encode task.</span></span> <span data-ttu-id="58729-123">출력 자산에는 사용하는 인코딩 기본 설정에 따라 비디오, 오디오, 미리 보기, 매니페스트 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-123">The output asset contains video, audio, thumbnails, manifest, etc. based on the encoding preset you use.</span></span>

<span data-ttu-id="58729-124">출력 자산에는 입력된 자산에 대한 메타데이터가 있는 파일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-124">The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="58729-125">메타데이터 XML 파일의 이름 형식은 다음과 같습니다. <asset_id>_metadata.xml(예: 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml). 여기서 <asset_id>는 입력 자산의 AssetId 값입니다.</span><span class="sxs-lookup"><span data-stu-id="58729-125">The name of the metadata XML file has the following format: <asset_id>_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where <asset_id> is the AssetId value of the input asset.</span></span> <span data-ttu-id="58729-126">이 입력 메타데이터 XML의 스키마는 [여기](media-services-input-metadata-schema.md)서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-126">The schema of this input metadata XML is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="58729-127">출력 자산에는 출력된 자산에 대한 메타데이터가 있는 파일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-127">The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="58729-128">메타데이터 XML 파일의 이름은 <source_file_name>_manifest.xml 형식입니다(예: BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="58729-128">The name of the metadata XML file has the following format: <source_file_name>_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span> <span data-ttu-id="58729-129">이 출력 메타데이터 XML의 스키마는 [여기](media-services-output-metadata-schema.md)에 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="58729-129">The schema of this output metadata XML is described [here](media-services-output-metadata-schema.md).</span></span>

<span data-ttu-id="58729-130">두 메타데이터 파일 중 하나를 검사하려는 경우 SAS 로케이터를 만들고 로컬 컴퓨터에 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-130">If you want to examine either of the two metadata files, you can create a SAS locator and download the file to your local computer.</span></span> <span data-ttu-id="58729-131">SAS 로케이터를 만들고 미디어 서비스 .NET SDK 확장을 사용하여 파일을 다운로드하는 방법에 대한 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-131">You can find an example on how to create a SAS locator and download a file Using the Media Services .NET SDK Extensions.</span></span>

## <a name="download-sample"></a><span data-ttu-id="58729-132">샘플 다운로드</span><span class="sxs-lookup"><span data-stu-id="58729-132">Download sample</span></span>
<span data-ttu-id="58729-133">MES를 사용하여 인코딩하는 방법을 보여 주는 샘플은 [여기](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)에서 가져와 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58729-133">You can get and run a sample that shows how to encode with MES from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="58729-134">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="58729-134">.NET sample code</span></span>

<span data-ttu-id="58729-135">다음 코드 예제에서는 미디어 서비스 .NET SDK를 사용하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-135">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="58729-136">인코딩 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58729-136">Create an encoding job.</span></span>
* <span data-ttu-id="58729-137">미디어 인코더 표준 인코더에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58729-137">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="58729-138">[적응 스트리밍](media-services-autogen-bitrate-ladder-with-mes.md) 사전 설정을 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-138">Specify to use the [Adaptive Streaming](media-services-autogen-bitrate-ladder-with-mes.md) preset.</span></span> 
* <span data-ttu-id="58729-139">작업에 단일 인코딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-139">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="58729-140">인코딩할 입력 자산을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-140">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="58729-141">인코딩된 자산을 포함할 출력 자산을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58729-141">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="58729-142">작업 진행 상태를 확인할 이벤트 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-142">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="58729-143">작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="58729-143">Submit the job.</span></span>

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="58729-144">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="58729-144">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="58729-145">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="58729-145">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="58729-146">예제</span><span class="sxs-lookup"><span data-stu-id="58729-146">Example</span></span> 

        using System;
        using System.Linq;
        using System.Configuration;
        using System.IO;
        using System.Threading;
        using Microsoft.WindowsAzure.MediaServices.Client;

        namespace MediaEncoderStandardSample
        {
            class Program
            {
                private static readonly string _AADTenantDomain =
                    ConfigurationManager.AppSettings["AADTenantDomain"];
                private static readonly string _RESTAPIEndpoint =
                    ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

                // Field for service context.
                private static CloudMediaContext _context = null;

                private static readonly string _supportFiles =
                    Path.GetFullPath(@"../..\Media");

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

                    // Create a task with the encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="58729-147">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="58729-147">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="58729-148">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="58729-148">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="58729-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58729-149">Next steps</span></span>
<span data-ttu-id="58729-150">[.NET과 함께 Media Encoder Standard를 사용하여 미리 보기를 생성하는 방법](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services 인코딩 개요](media-services-encode-asset.md)</span><span class="sxs-lookup"><span data-stu-id="58729-150">[How to generate thumbnail using Media Encoder Standard with .NET](media-services-dotnet-generate-thumbnail-with-mes.md)
[Media Services Encoding Overview](media-services-encode-asset.md)</span></span>

