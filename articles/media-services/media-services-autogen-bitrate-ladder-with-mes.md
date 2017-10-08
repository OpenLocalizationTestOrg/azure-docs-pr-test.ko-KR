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
#  <a name="use-azure-media-encoder-standard-tooauto-generate-a-bitrate-ladder"></a>Azure 미디어 인코더 표준 tooauto를 사용 하 여-비트 전송률 사다리를 생성 합니다.

## <a name="overview"></a>개요

이 항목에서는 방법을 toouse 미디어 인코더 표준 MES () tooauto-hello 입력된 해상도 비트 전송률 기반 비트 전송률 사다리 (비트 전송률 해상도 쌍)를 생성 합니다. hello 자동 생성 된 사전 설정을 초과할 수 없습니다 입력 hello 해상도 비트 전송률. 예를 들어 hello 입력이 리디렉션되면 3Mbps, 출력 됩니다에 720p 720p, 유지 및 3Mbps 보다 낮은 요금이 시작 됩니다.

### <a name="encoding-for-streaming-only"></a>스트리밍 전용 인코딩

Tooencode 하려는 경우 다음 해야 "적응 스트리밍" hello를 사용 하 여 스트리밍에 대해서만 비디오 원본에는 사전 인코딩 작업을 만들 때 설정 합니다. Hello를 사용 하는 경우 **적응 스트리밍** 사전 설정을 hello MES 인코더는 지능적으로 캡 비트 전송률 사다리 합니다. 그러나 비용을 인코딩 hello 서비스 레이어 toouse 개수를 결정 하므로 및 해상도에서 수 toocontrol hello 되지 않습니다. MES hello로 인코딩한 결과 생성 되는 출력 계층의 예제를 확인할 수 **적응 스트리밍** 이 항목의 hello 끝에 미리 설정 합니다. hello 출력 자산 오디오를 MP4 파일이 포함 될 및 비디오 인터리브되지 않습니다.

### <a name="encoding-for-streaming-and-progressive-download"></a>스트리밍 및 점진적 다운로드용 인코딩

Tooencode 하려는 경우 다음 해야 "콘텐츠 적응 다중 비트 전송률 MP4" hello를 사용 하 여 뿐만 아니라 tooproduce MP4 파일 점진적 다운로드에 대 한 스트리밍에 대 한 원본 비디오 사전 인코딩 작업을 만들 때 설정 합니다. Hello를 사용 하는 경우 **적응 콘텐츠 다중 비트 전송률 MP4** hello MES 인코더 hello 위의 동일 하지만 hello 출력 자산에는 MP4 포함 될 이제 동일한 인코딩 논리 오디오 위치 파일에 적용 됩니다 및 비디오를 인터리브 미리 설정 합니다. 점진적 다운로드 파일로 이러한 MP4 파일 (예를 들어 hello 가장 높은 비트 전송률 버전) 중 하나를 사용할 수 있습니다.

## <a id="encoding_with_dotnet"></a>미디어 서비스 .NET SDK를 사용하여 인코딩

다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.

- 인코딩 작업을 만듭니다.
- 참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.
- 인코딩 작업 toohello 작업을 추가 하 고 toouse hello 지정 **적응 스트리밍** 사전 설정 합니다. 
- Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.
- 이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.
- Hello 작업을 제출 합니다.

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

#### <a name="example"></a>예제

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

## <a id="output"></a>출력

이 섹션에서는 MES hello로 인코딩한 결과 생성 되는 출력 계층의 세 가지 예제 **적응 스트리밍** 사전 설정입니다. 

### <a name="example-1"></a>예 1
높이가 "1080"이고 프레임 속도가 "29.970"인 원본은 6개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|1080|1920|6780|
|2|720|1280|3520|
|3|540|960|2210|
|4|360|640|1150|
|5|270|480|720|
|6|180|320|380|

### <a name="example-2"></a>예 2
높이가 "720"이고 프레임 속도가 "23.970"인 원본은 5개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|720|1280|2940|
|2|540|960|1850|
|3|360|640|960|
|4|270|480|600|
|5|180|320|320|

### <a name="example-3"></a>예 3
높이가 "360"이고 프레임 속도가 "29.970"인 원본은 3개의 비디오 계층을 생성합니다.

|계층|높이|너비|비트 전송률(kbps)|
|---|---|---|---|
|1|360|640|700|
|2|270|480|440|
|3|180|320|230|
## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[미디어 서비스 인코딩 개요](media-services-encode-asset.md)

