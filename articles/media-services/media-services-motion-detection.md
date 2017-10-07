---
title: "Azure 미디어 분석을 aaaDetect 동작 | Microsoft Docs"
description: "hello Azure 미디어 동작 탐지기 미디어 프로세서 (MP) 사용 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a>Azure 미디어 검색으로 동작 검색
## <a name="overview"></a>개요
hello **Azure 미디어 동작 탐지기** 미디어 프로세서 (MP) 사용 하도록 설정 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다. 동작 감지 동작 발생 hello 비디오의 정적 카메라 장면 tooidentify 섹션에서 사용할 수 있습니다. 타임 스탬프 및 hello hello 이벤트가 발생 하는 영역 경계와 메타 데이터를 포함 하는 JSON 파일을 생성 합니다.

이 기술은 보안 비디오 피드를 겨냥 수 toocategorize 동작 관련 이벤트 및 거짓 긍정 그림자 조명 변경 등으로입니다. 이렇게 하면 있습니다 카메라 피드에서 toogenerate 보안 경고 수 tooextract 시간이 매우 긴 거리 내 감시 비디오에서 관심 있는 하면서 무한 관련이 없는 이벤트로 스팸 메일 되지 않고.

hello **Azure 미디어 동작 탐지기** MP는 현재 미리 보기로 합니다.

이 항목에 대 한 세부 정보를 제공 **Azure 미디어 동작 탐지기** 표시 방법을 toouse Media Services SDK for.NET으로

## <a name="motion-detector-input-files"></a>동작 검색기 입력 파일
동영상 파일입니다. 현재 형식에 따라 hello 지원 됩니다: MP4, MOV, 및 WMV입니다.

## <a name="task-configuration-preset"></a>작업 구성(기본 설정)
**Azure 미디어 동작 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다. 

### <a name="parameters"></a>매개 변수
Hello 매개 변수 뒤에 사용할 수 있습니다.

| 이름 | 옵션 | 설명 | 기본값 |
| --- | --- | --- | --- |
| sensitivityLevel |문자열:'low', 'medium', 'high' |보고 되는 동작에 수준 hello 민감도 설정 합니다. 거짓 긍정이 tooadjust 시간을 조정 합니다. |'medium' |
| frameSamplingValue |양의 정수 |어떤 알고리즘 실행에 hello 주파수를 설정합니다. 1은 프레임마다, 2는 두 번째 프레임마다 등을 의미합니다. |1 |
| detectLightChange |부울:'true', 'false' |Hello 결과에 밝은 변경 내용을 보고 있는지 여부를 설정합니다 |'False' |
| mergeTimeThreshold |Xs-time: Hh:mm:ss<br/>예: 00:00:03 |동작 이벤트 2 이벤트가 결합 및 1로 보고 하려는 hello 시간 창을 지정 합니다. |00:00:00 |
| detectionZones |검색 영역 배열:<br/>- 검색 영역은 3개 이상의 지점 배열<br/>-점은 x 및 y 좌표 0 too1에서 합니다. |사용 되는 다각형 검색 영역 toobe hello 목록에 설명 합니다.<br/>첫 번째 되 고 'id' hello로 한 ID로 결과 hello 영역으로 보고 됩니다: 0 |단일 5d; 영역 hello 전체 프레임에 설명 합니다. |

### <a name="json-example"></a>JSON 예제
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a>동작 검색기 출력 파일
동작 검색 작업은 hello 동작 경고와 hello 비디오 내에서 해당 범주를 설명 하는 hello 출력 자산에는 JSON 파일을 반환 합니다. hello 파일에는 hello 시간과 기간, hello 비디오에서 검색 하는 동작에 대 한 정보가 포함 됩니다.

동작에서 개체는 고정된 백그라운드에서 비디오 (예: 한 거리 내 감시 비디오) 되 면 hello 모션 탐지기 API 표시기를 제공 합니다. hello 동작 탐지기는 학습 된 tooreduce 거짓 경보 조명 섀도 변경 등입니다. Hello 알고리즘의 현재 제한 사항 밤 비전 비디오, 반투명 개체 및 작은 개체를 포함 합니다.

### <a id="output_elements"></a>Hello 출력 JSON 파일의 요소
> [!NOTE]
> Hello 최신 릴리스에서 hello JSON 출력 형식 변경 되었으며이 일부 고객에 대 한 주요 변경 내용를 나타낼 수 있습니다.
> 
> 

hello 다음 설명 hello 출력 JSON 파일의 요소입니다.

| 요소 | 설명 |
| --- | --- |
| 버전 |이 hello 비디오 API의 toohello 버전을 나타냅니다. hello 현재 버전은 2입니다. |
| 시간 간격 |"틱" hello 비디오의 초 당 합니다. |
| Offset |"틱"의 타임 스탬프에 대 한 hello 시간 오프셋입니다. 동영상 API 버전 1.0에서는 항상 0입니다. 향후 지원하는 시나리오에서는 이 값이 변경될 수 있습니다. |
| 프레임 속도 |Hello 비디오의 초당 프레임 수입니다. |
| 너비, 높이 |픽셀 단위로 비디오 hello의 toohello 너비와 높이 참조합니다. |
| 시작 |hello "틱"의 타임 스탬프를 시작 합니다. |
| 기간 |"틱" hello 이벤트의 hello 길이입니다. |
| 간격 |hello 이벤트 "틱"에 있는 각 항목의 hello 간격입니다. |
| 이벤트 |각 이벤트 조각 해당 기간 내에서 검색 하는 hello 동작을 포함 합니다. |
| 형식 |Hello 현재 버전에서는 이것이 항상 일반 동작에 대 한 ' 2'입니다. 이 레이블은 이후 버전에서 비디오 Api hello 유연성 toocategorize 동작을 제공합니다. |
| RegionID |위에서 설명했듯이 이 버전에서 이 값은 항상 0입니다. 이 레이블은 이후 버전에서는 다양 한 지역에 비디오 API hello 유연성 toofind 동작을 제공합니다. |
| 영역 |동작에 대 한 관심이 비디오에서 toohello 영역을 참조 합니다. <br/><br/>-"id" hello 영역 영역을 나타내는 –이 버전에는 하나의 ID가 0입니다. <br/>-"type" 동작에 대 한 중요 한 hello 영역의 hello 셰이프를 나타냅니다. 현재 "rectangle" 및 "polygon"이 지원됩니다.<br/> "사각형"를 지정한 경우 hello 영역 차원이 x, Y, 너비 및 높이입니다. hello X 및 Y 좌표 0.0 too1.0의 정규화 된 소수에 hello 영역의 hello 왼쪽 위 XY 좌표를 나타냅니다. hello 너비와 높이 0.0 too1.0의 정규화 된 소수에 hello 영역의 hello 크기를 나타냅니다. Hello 현재 버전, X, Y, 너비 및 높이 0, 0 및 1, 1로 고정 항상 있습니다. <br/>"다각형"를 지정한 경우에 hello 지역은 포인트에서 차원이 있습니다. <br/> |
| 조각 |hello 메타 데이터를 조각 이라고 하는 서로 다른 세그먼트에 청크 분할 됩니다. 각 조각에는 시작, 기간, 간격 번호 및 이벤트가 포함됩니다. 이벤트가 없는 조각은 해당 시작 시간 및 기간 동안에 검색된 동작이 없음을 의미합니다. |
| 대괄호 [] |각 괄호 hello 이벤트에서 하나의 간격을 나타냅니다. 해당 간격에 대한 빈 대괄호는 검색된 동작이 없음을 의미합니다. |
| 위치 |이벤트에서이 새 항목 hello 동작 발생 한 hello 위치를 나열 합니다. Hello 검색 영역 보다 더 구체적입니다. |

hello 다음은 JSON의 출력 예

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a>제한 사항
* 입력된 비디오 형식을 지원 hello MP4, MOV, 및 WMV 포함 됩니다.
* 동작 검색은 고정 배경 동영상에 최적화되어 있습니다. hello 알고리즘 조명 변경 내용, 그림자 등에 등 거짓 경보를 단축에 중점을 둡니다.
* Tootechnical 과제; 인해 일부 동작을 검색할 수 없습니다. 예를 들어 밤 비전 비디오, 반투명 개체 및 작은 개체입니다.

## <a name="net-sample-code"></a>.NET 샘플 코드

hello 다음 프로그램 표시 하는 방법:

1. 자산 만들기 hello 자산 미디어 파일을 업로드 합니다.
2. 다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 비디오 동작 검색 작업으로 작업을 만듭니다. 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. Hello 출력 JSON 파일을 다운로드 합니다. 

#### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 

#### <a name="example"></a>예제


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

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
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
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
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }
        }
    }

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure 미디어 서비스 동작 탐지기 블로그](https://azure.microsoft.com/blog/motion-detector-update/)

[Azure 미디어 서비스 분석 개요](media-services-analytics-overview.md)

[Azure 미디어 분석 데모](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

