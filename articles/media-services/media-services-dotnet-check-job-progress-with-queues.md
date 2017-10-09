---
title: "aaaUse Azure 큐 저장소 toomonitor 미디어 서비스 작업 알림.net | Microsoft Docs"
description: "Toouse Azure 큐 저장소 toomonitor 미디어 서비스 알림 작업 하는 방법에 대해 알아봅니다. hello 코드 예제는 C#으로 작성 하 고 hello Media Services SDK for.NET 사용."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a>.NET과 함께 Azure 큐 저장소 toomonitor 미디어 서비스 작업 알림 사용
인코딩 작업을 실행 하면 일반적 방법을 tootrack 작업 진행 상황을 필요 합니다. 미디어 서비스 toodeliver 알림을 너무 구성할 수 있습니다[Azure 큐 저장소](../storage/storage-dotnet-how-to-use-queues.md)합니다. Hello 큐 저장소에서에서 가져오는 알림에 의해 작업 진행 상황을 모니터링할 수 있습니다. 

TooQueue 저장소 배달 된 메시지에서에서 액세스할 수 있습니다에서 아무 곳 이나 hello world. hello 큐 저장소 메시징 아키텍처의 신뢰성과 확장성이 높은 합니다. 다른 방법을 사용하는 것보다 메시지에 대한 Queue Storage를 폴링하는 것이 좋습니다.

(예: tootrigger hello 다음 단계는 워크플로 또는 toopublish tooMedia 서비스 알림 수신 대기에 대 한 일반적인 시나리오는 tooperform 보내야 하는 콘텐츠 관리 시스템을 개발 하는 경우 하나는 인코딩 작업 후에 몇 가지 추가 작업 완료 콘텐츠 포함)입니다.

이 항목에서는 tooget 알림 큐 저장소에서 메시지 하는 방법을 보여 줍니다.  

## <a name="considerations"></a>고려 사항
큐 저장소를 사용 하는 미디어 서비스 응용 프로그램을 개발할 때 hello 다음을 고려 합니다.

* Queue Storage는 선입 선출(FIFO) 순차적 전달을 보장하지 않습니다. 자세한 내용은 [Azure 큐 및 Azure 서비스 버스 큐 비교 및 대조](https://msdn.microsoft.com/library/azure/hh767287.aspx)를 참조하세요.
* Queue Storage는 푸시 서비스가 아닙니다. Toopoll hello 큐를 만들어야합니다.
* 개수에 관계 없이 큐를 사용할 수 있습니다. 자세한 내용은 [큐 서비스 REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API)를 참조하세요.
* 큐 저장소에 몇 가지 제한 사항 및 세부 사항 toobe 알고 있습니다. 이러한 내용은 [Azure 큐 및 Azure Service Bus 큐 - 비교 및 대조](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted)에 설명되어 있습니다.

## <a name="net-code-example"></a>.NET 코드 예제

이 섹션의 hello 코드 예제에서는 다음 hello지 않습니다.

1. Hello 정의 **EncodingJobMessage** toohello 알림 메시지 형식에 매핑되는 클래스입니다. hello 코드의 hello 개체로 hello 큐에서 받은 메시지를 deserialize **EncodingJobMessage** 유형입니다.
2. 로드에는 미디어 서비스 및 저장소 계정 정보 hello app.config 파일에서 hello 합니다. hello 코드 예제에서는이 정보 toocreate hello를 사용 하 여 **CloudMediaContext** 및 **CloudQueue** 개체입니다.
3. 인코딩 작업 hello에 대 한 알림 메시지를 수신 하는 hello 큐를 만듭니다.
4. 끝점 매핑된 toohello 큐 hello 알림을 만듭니다.
5. Hello 알림 끝점 toohello 작업에 연결 하 고 hello 인코딩 작업을 제출 합니다. 여러 알림 끝점 연결 tooa 작업을 할 수 있습니다.
6. 전달 **NotificationJobState.FinalStatesOnly** toohello **AddNew** 메서드. (이 예제에서는에 관심이 hello 작업 처리의 최종 상태입니다.)

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. 전달 하는 경우 **NotificationJobState.All**, 상태 변경 알림 다음 hello는 모든: 큐에 대기 중인, 예약, 처리 및 완료 합니다. 그러나 앞에서 설명한 대로 Queue Storage가 순차적 전달을 보장하지 않습니다. tooorder 메시지를 사용 하 여 hello **타임 스탬프** 속성 (hello에 정의 된 **EncodingJobMessage** 아래의 hello 예에서 유형). 중복된 메시지도 허용됩니다. 중복을 사용 하 여 hello toocheck **ETag 속성** (hello에 정의 된 **EncodingJobMessage** 유형). 또한 일부 상태 변경 알림을 건너뛸 수 있습니다.
8. 10 초 마다 hello 큐를 확인 하 여 상태를 완료 하는 hello 작업 tooget toohello 때까지 기다립니다. 처리된 후 메시지를 삭제합니다.
9. Hello 큐와 hello 알림 끝점을 삭제합니다.

> [!NOTE]
> hello는 hello 다음 예제에에서 나와 있는 것 처럼 작업의 상태가 toonotification 메시지를 수신 대기 하는 방식으로 toomonitor는 것이 좋습니다.
>
> 또는 검사할 수 있었습니다 작업의 상태에 hello를 사용 하 여 **IJob.State** 속성입니다.  작업의 완료에 대 한 알림 메시지에 hello 상태 이전 도착할 수 있습니다 **IJob** 너무 설정**마침**합니다. hello **IJob.State** 속성은 약간의 지연으로 hello 정확한 상태를 반영 합니다.
>
>

### <a name="create-and-configure-a-visual-studio-project"></a>Visual Studio 프로젝트 만들기 및 구성

1. 개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다. 
2. 새 폴더를 만듭니다 (폴더는 로컬 드라이브에 아무 곳 이나 수 있음) 원하는 tooencode 및 스트림 하거나 점진적으로 다운로드 하는.mp4 파일을 복사 합니다. 이 예제에서는 hello "C:\Media" 경로가 사용 됩니다.

### <a name="code"></a>코드

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want tooget messages from hello queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display hello message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete hello message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
위의 예제에서는 생성 된 hello 출력 뒤 hello 합니다. 값은 달라질 수 있습니다.

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
