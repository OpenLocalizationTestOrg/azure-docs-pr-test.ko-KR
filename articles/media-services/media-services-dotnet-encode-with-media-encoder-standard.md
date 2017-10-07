---
title: "미디어 인코더 표준.NET을 사용 하 여 aaaEncode | Microsoft Docs"
description: "이 항목에서는 방법을 toouse.NET tooencode 미디어 인코더 표준을 사용 하 여 자산입니다."
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
ms.openlocfilehash: 25e274c3b67168f4afc8b8ab04af2d654c9dd6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-with-media-encoder-standard-using-net"></a>.NET을 사용하여 미디어 인코더 표준으로 자산 인코딩
인코딩 작업은 미디어 서비스의 hello 가장 일반적인 처리 작업 중 하나입니다. 하나의 인코딩 tooanother에서 인코딩 작업 tooconvert 미디어 파일을 만듭니다. 인코드할 때는 hello 미디어 인코더를 기본 제공 하는 미디어 서비스를 사용할 수 있습니다. 미디어 서비스 파트너; 제공 하는 인코더를 사용할 수도 있습니다. 타사 인코더는 hello Azure 마켓플레이스를 통해 사용할 수 있습니다. 

이 항목에서는 방법을 toouse.NET tooencode 자산으로 미디어 인코더 표준 MES (). 미디어 인코더 표준 구성 된 설명 hello 인코더 사전 설정 중 하나를 사용 하 여 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)합니다.

Tooalways 소스 파일을 적응 비트 전송률 MP4 세트 인코딩하고 hello 집합 toohello 원하는 서식 hello를 사용 하 여 다음 변환 좋습니다 [동적 패키징](media-services-dynamic-packaging-overview.md)합니다. 

출력 자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 합니다. 자세한 내용은 [자산 배달 정책 구성](media-services-dotnet-configure-asset-delivery-policy.md)을 참조하세요.

> [!NOTE]
> 포함 된 이름으로 출력 파일의 처음 32 자 hello MES 생성 hello 입력된 파일 이름입니다. hello 이름은 hello 미리 설정 된 파일에 지정 된 내용에 기반 합니다. 예를 들어 "FileName": "{Basename}_{Index}{Extension}"과 같습니다. {Basename} hello로 대체 됩니다 hello 입력된 파일 이름의 처음 32 자입니다.
> 
> 

### <a name="mes-formats"></a>MES 형식
[형식 및 코덱](media-services-media-encoder-standard-formats.md)

### <a name="mes-presets"></a>MES 기본 설정
미디어 인코더 표준 구성 된 설명 hello 인코더 사전 설정 중 하나를 사용 하 여 [여기](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)합니다.

### <a name="input-and-output-metadata"></a>입력 및 출력 메타데이터
출력 자산을 가져옵니다 MES를 사용 하 여 입력된 자산 (또는 자산)를 인코딩할 때 hello에 성공적으로 완료 하는 인코딩 작업 합니다. hello 출력 자산은 비디오, 오디오, 미리 보기, 매니페스트 등 hello 인코딩 사전 설정을 사용 하면에 따라 포함 되어 있습니다.

hello 출력 자산도 파일이 hello 입력된 자산 관련 메타 데이터가 있습니다. hello hello 메타 데이터 XML 파일의 이름에 형식에 따라 hello: < t > _ m e (예를 들어 41114ad3-eb5e-4 c 57-8 d 92-5354e2b7d4a4_metadata.xml), 여기서 < t _ i d >는 hello 입력 자산의 AssetId 값 hello 합니다. hello 스키마 입력된이 메타 데이터 XML의 설명 [여기](media-services-input-metadata-schema.md)합니다.

hello 출력 자산에는 hello 출력 자산에 대 한 메타 데이터가 있는 파일도 포함 되어 있습니다. hello hello 메타 데이터 XML 파일의 이름에 형식에 따라 hello: < source_file_name > _manifest.xml (예: BigBuckBunny_manifest.xml). 이 출력 메타 데이터 XML 설명의 hello 스키마 [여기](media-services-output-metadata-schema.md)합니다.

원하는 tooexamine hello 두 메타 데이터 파일의 경우에 SAS 로케이터를 만들고 및 hello 파일 tooyour 로컬 컴퓨터를 다운로드할 수 있습니다. 예제 어떻게 toocreate SAS 로케이터 및 다운로드 한 파일 사용 하 여 hello 미디어 서비스를 찾을 수 있습니다.NET SDK Extensions입니다.

## <a name="download-sample"></a>샘플 다운로드
가져올 하 고 보여 주는 샘플을 실행할 수 있습니다 어떻게에서 MES와 tooencode [여기](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/)합니다.

## <a name="net-sample-code"></a>.NET 샘플 코드

다음 코드 예제는 hello 작업을 수행 하는 미디어 서비스.NET SDK tooperform hello를 사용 합니다.

* 인코딩 작업을 만듭니다.
* 참조 toohello 미디어 인코더 표준 인코더를 가져옵니다.
* Toouse hello 지정 [적응 스트리밍](media-services-autogen-bitrate-ladder-with-mes.md) 사전 설정입니다. 
* 인코딩 작업의 단일 toohello 작업을 추가 합니다. 
* Hello 입력 지정 인코딩된 자산 toobe 합니다.
* Hello 인코딩된 자산에 포함 될 출력 자산을 만듭니다.
* 이벤트 처리기 toocheck hello 작업 진행률을 추가 합니다.
* Hello 작업을 제출 합니다.

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

#### <a name="example"></a>예제 

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

                    // Create a task with hello encoding details, using a string preset.
                    // In this case "Adaptive Streaming" preset is used.
                    ITask task = job.Tasks.AddNew("My encoding task",
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

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>다음 단계
[어떻게 toogenerate 미리 보기 미디어 인코더 표준.NET과 함께 사용 하 여](media-services-dotnet-generate-thumbnail-with-mes.md)
[미디어 서비스 인코딩 개요](media-services-encode-asset.md)

