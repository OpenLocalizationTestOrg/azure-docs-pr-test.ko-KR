---
title: "aaaHow toouse hello WebJobs SDK로 Azure 큐 저장소"
description: "Toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법에 대해 알아봅니다. 큐 만들기 및 삭제, 큐 메시지 삽입, 미리 보기, 가져오기 및 삭제 등의 작업을 알아봅니다."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법
## <a name="overview"></a>개요
이 가이드에서는 C# 코드 샘플 toouse Azure WebJobs SDK 버전을 hello 하는 방법을 보여 주는 제공 1.x hello Azure 큐 저장소 서비스 사용 합니다.

hello 가이드 알고 있다고 가정 [toocreate 연결이 포함 된 Visual Studio에서 WebJob 프로젝트의 해당 지점 tooyour 저장소 계정 문자열 어떻게](websites-dotnet-webjobs-sdk-get-started.md) 또는 너무[여러 저장소 계정을](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)합니다.

Hello를 만드는 코드를 hello 표시 기능을 대부분 hello 코드 조각의 `JobHost` 다음이 예제와 같이 개체:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

hello 가이드 hello를 다음 항목 포함 되어 있습니다.

* [어떻게 tootrigger 큐 메시지를 받을 때 함수](#trigger)
  * 문자열 큐 메시지
  * POCO 큐 메시지
  * 비동기 함수
  * 형식 hello QueueTrigger 특성 사용
  * 폴링 알고리즘
  * 여러 인스턴스
  * 병렬 실행
  * 큐 또는 큐 메시지 메타데이터 가져오기
  * 정상 종료
* [큐 메시지를 처리 하는 동안 toocreate 큐 메시지 하는 방법](#createqueue)
  * 문자열 큐 메시지
  * POCO 큐 메시지
  * 여러 메시지 만들기 또는 비동기 함수로 큐 메시지 만들기
  * 형식 hello 큐 특성 사용
  * WebJobs SDK 특성 hello 함수 본문에서 사용 하 여
* [큐 메시지를 처리 하는 동안 blob tooread 및 쓰기](#blobs)
  * 문자열 큐 메시지
  * POCO 큐 메시지
  * 형식 hello Blob 특성 사용
* [어떻게 toohandle 포이즌 메시지](#poison)
  * 자동 포이즌 메시지 처리
  * 수동 포이즌 메시지 처리
* [어떻게 tooset 구성 옵션](#config)
  * 코드에서 SDK 연결 문자열 설정
  * QueueTrigger 설정 구성
  * 코드에서 WebJobs SDK 생성자 매개 변수 값 설정
* [어떻게 tootrigger 함수 수동으로](#manual)
* [Toowrite 기록 하는 방법](#logs)
* [어떻게 toohandle 오류 시간 제한을 구성 하 고](#errors)
* [다음 단계](#nextsteps)

## <a id="trigger"></a>어떻게 tootrigger 큐 메시지를 받을 때 함수
큐 메시지를 받을 때 toowrite hello WebJobs SDK는 함수 호출, hello를 사용 하 여 `QueueTrigger` 특성입니다. hello 특성 생성자 hello 큐 toopoll의 hello 이름을 지정 하는 문자열 매개 변수를 사용 합니다. 수도 있습니다 [hello 큐 이름을 동적으로 설정할](#config)합니다.

### <a name="string-queue-messages"></a>문자열 큐 메시지
Hello 큐에서 다음 예제는 hello, 문자열 메시지를 따라서 포함 `QueueTrigger` 라는 적용된 tooa 문자열 매개 변수는 `logMessage` hello 큐 메시지의 hello 콘텐츠를 포함 하 합니다. 함수 hello [로그 메시지 toohello 대시보드 씁니다](#logs)합니다.

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

외에 `string`, hello 매개 변수를 바이트 배열로 일 수는 `CloudQueueMessage` 개체 또는 사용자가 정의한 POCO 합니다.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지
다음 예제는 hello, hello 큐 메시지에 대 한 JSON 포함 한 `BlobInformation` 포함 하는 개체는 `BlobName` 속성입니다. hello SDK는 자동으로 hello 개체를 역직렬화합니다.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

hello SDK hello를 사용 하 여 [Newtonsoft.Json NuGet 패키지](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize 및 메시지를 역직렬화 합니다. Hello WebJobs SDK를 사용 하지 않는 프로그램에서 메시지 큐를 만들면 해당 hello SDK 구문 분석할 수 있는 다음 예에서는 toocreate POCO 큐 메시지 hello 같은 코드를 작성할 수 있습니다.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>비동기 함수
async 함수 다음 hello [로그 toohello 대시보드 씁니다](#logs)합니다.

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

비동기 함수 걸릴 수 있습니다는 [취소 토큰](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)hello 다음 blob를 복사 하는 예제에에서 나온 것 처럼 합니다. (에 대 한 설명은 hello `queueTrigger` 자리 표시자를 hello 참조 [Blob](#blobs) 섹션.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>형식 hello QueueTrigger 특성 사용
사용할 수 있습니다 `QueueTrigger` 유형만 hello로:

* `string`
* JSON으로 serialize된 POCO 유형
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a> 폴링 알고리즘
hello SDK 유휴 큐 폴링에 저장소 트랜잭션 비용의 임의 지 수 백오프 알고리즘 tooreduce hello 효과 구현 합니다.  메시지가 발견 되 면 hello SDK 2 초 동안 기다린 후; 다른 메시지를 확인 합니다. 메시지가 발견 되 면 다시 시도 하기 전에 4 초 정도 대기 합니다. 후속 실패 한 시도 tooget 큐 메시지 후 hello 대기 시간이 계속 tooincrease hello 최대 대기 시간에 도달할 때까지 어떤 기본값 tooone 분입니다. [hello 최대 대기 시간은 구성 가능](#config)합니다.

### <a id="instances"></a> 여러 인스턴스
웹 앱이 여러 인스턴스에서 실행 하는 경우 각 컴퓨터에서 실행 되는 연속 WebJob를 각 컴퓨터 트리거에 대 한 대기 되며 toorun 함수를 시도 합니다. WebJobs SDK 큐 트리거 hello에서 여러 번; 큐 메시지를 처리 하는 함수는 자동으로 방지 함수는 toobe toobe idempotent 작성 권한이 없습니다. 그러나 tooensure 하려는 경우 함수의 인스턴스를 하나만 실행 hello 호스트 웹 응용 프로그램의 여러 인스턴스가 있는 경우에, hello를 사용할 수 있습니다 `Singleton` 특성입니다.

### <a id="parallel"></a> 병렬 실행
다른 큐에서 수신 대기 하는 여러 개의 함수를 사용 하도록 설정한 경우 hello SDK는 전화할 동시에 동시에 메시지를 받을 때입니다.

hello는 경우도 마찬가지 단일 큐에 대 한 여러 메시지를 수신 합니다. 기본적으로 hello SDK 한 번에 16 큐 메시지의 일괄 처리를 가져오고을 병렬로 처리 hello 함수를 실행 합니다. [hello 일괄 처리 크기는 구성 가능한](#config)합니다. 처리 중인 hello 번호 hello 일괄 처리 크기의 toohalf 아래로 가져오면 hello SDK는 다른 일괄 처리를 가져오고 해당 메시지의 처리를 시작 합니다. 따라서 함수 당 처리 중인 동시 메시지 hello 최대 수에는 하나의 1.5 배 hello 일괄 처리 크기입니다. 이 제한은 개별적으로 적용 됩니다. 있는 tooeach 함수는 `QueueTrigger` 특성입니다.

하나의 큐에 수신 된 메시지에 대 한 병렬 실행 사용 하지 않으려는 경우에 일괄 처리 크기 too1 hello를 설정할 수 있습니다. **Azure WebJobs SDK 1.1.0 RTM** 에서 [큐 처리에 대한 제어 강화](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)를 참조하세요.

### <a id="queuemetadata"></a>큐 또는 큐 메시지 메타데이터 가져오기
Hello 매개 변수 toohello 메서드 시그니처를 추가 하 여 다음과 같은 메시지 속성을 가져올 수 있습니다.

* `DateTimeOffset` expirationTime
* `DateTimeOffset` insertionTime
* `DateTimeOffset` nextVisibleTime
* `string` queueTrigger(메시지 텍스트 포함)
* `string` id
* `string` popReceipt
* `int` dequeueCount

원하는 경우 toowork hello Azure 저장소 API 사용 하 여 직접 추가할 수도 있습니다는 `CloudStorageAccount` 매개 변수입니다.

hello 다음 예제에서는 모든이 메타 데이터 tooan 정보 응용 프로그램 로그 Hello 예제 logMessage와 queueTrigger hello 큐 메시지의 hello 내용이 포함 됩니다.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Hello 샘플 코드에 의해 작성 된 샘플 로그는 다음과 같습니다.

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>정상 종료
연속 WebJob을 실행 하는 함수를 사용할 수는 `CancellationToken` toobe 종료에 대 한 경우 hello hello 운영 체제 toonotify hello 함수를 사용 하도록 설정 하는 매개 변수 WebJob은 합니다. 이 알림 toomake hello 함수는 데이터 일관성 없는 상태로 유지 하는 방식으로 예기치 않게 종료 하지 않는 있는지를 사용할 수 있습니다.

hello 방법을 예제와 다음 toocheck 함수에 게 컴퓨터가 곧 WebJob 종료 합니다.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**참고:** hello 대시보드 hello 상태 및 종료 된 함수의 출력에 올바르게 표시 되지 않습니다.

자세한 내용은 [WebJobs 정상 종료](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)를 참조하세요.   

## <a id="createqueue"></a>큐 메시지를 처리 하는 동안 toocreate 큐 메시지 하는 방법
새 큐 메시지를 사용 하 여 hello를 만드는 함수를 toowrite `Queue` 특성입니다. 마찬가지로 `QueueTrigger`, hello 큐 이름을 문자열로 전달 또는 할 수 있습니다 [hello 큐 이름을 동적으로 설정할](#config)합니다.

### <a name="string-queue-messages"></a>문자열 큐 메시지
아래의 비동기 코드 예제는 hello hello hello 큐 메시지로 콘텐츠 수신 "inputqueue" 라는 hello 큐에 있는 "outputqueue" 라는 hello 큐에 새 큐 메시지를 만듭니다. 비동기 함수는 이 섹션의 뒷부분에 나와 있는 것처럼 `IAsyncCollector<T>` 를 사용합니다.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지
출력 매개 변수 toohello로 toocreate 문자열로 전달 hello POCO가 아닌는 POCO 포함 하는 큐 메시지 입력 `Queue` 특성 생성자입니다.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

hello SDK hello 개체 tooJSON를 자동으로 serialize합니다. 큐 메시지는 hello 개체가 null 인 경우에 항상 생성 됩니다.

### <a name="create-multiple-messages-or-in-async-functions"></a>여러 메시지 만들기 또는 비동기 함수로 큐 메시지 만들기
toocreate 여러 개의 메시지를 확인 hello 출력 큐에 대 한 hello 매개 변수 형식을 `ICollector<T>` 또는 `IAsyncCollector<T>`hello 다음 예제에에서 나온 것 처럼 합니다.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

각 큐 메시지 즉시 때 만들어집니다 hello `Add` 메서드를 호출 합니다.

### <a name="types-that-hello-queue-attribute-works-with"></a>해당 hello 큐 특성 작동 형식
Hello를 사용할 수 있습니다 `Queue` 특성 매개 변수 유형만 hello에:

* `out string`(hello 함수 종료 될 때 매개 변수 값이 null이 아닌 큐 메시지 생성)
* `out byte[]`(`string`처럼 작동)
* `out CloudQueueMessage`(`string`처럼 작동)
* `out POCO`(직렬화 가능 형식 메시지를 만듭니다는 null 개체에 hello 함수가 종료 되어도 hello 매개 변수가 null 이면)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(사용 하 여 수동으로 메시지를 만들기 위한 hello Azure 저장소 API 직접)

### <a id="ibinder"></a>WebJobs SDK 특성 hello 함수 본문에서 사용 하 여
함수에서와 같은 WebJobs SDK 특성을 사용 하기 전에 작동 toodo 해야 할 경우 `Queue`, `Blob`, 또는 `Table`, hello를 사용할 수 있습니다 `IBinder` 인터페이스입니다.

다음 예제는 hello 입력된 큐 메시지를 출력 큐에서 같은 콘텐츠에 hello로 새 메시지를 만듭니다. hello 출력 큐 이름은 코드 hello hello 함수 본문에 의해 설정 됩니다.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

hello `IBinder` 인터페이스 hello로 사용할 수도 있습니다 `Table` 및 `Blob` 특성입니다.

## <a id="blobs"></a>Tooread 및 쓰기의 blob 및 큐 메시지를 처리 하는 동안 테이블
hello `Blob` 및 `Table` 특성을 사용 하면 tooread 고 blob 및 테이블을 작성 합니다. 이 단원의 샘플 hello tooblobs를 적용 됩니다. Blob 생성 되거나 업데이트 되 면 tootrigger 처리 하는 방법을 보여 주는 코드 샘플을 참조 하십시오. [어떻게 toouse Azure blob 저장소에 hello WebJobs SDK로](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), 읽기 / 테이블을 작성 하는 코드 샘플 및 [어떻게 toouse Azure 테이블 hello WebJobs SDK를 사용 하 여 저장소](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)합니다.

### <a name="string-queue-messages-triggering-blob-operations"></a>Blob 작업을 트리거하는 문자열 큐 메시지
문자열을 포함 하는 큐 메시지에 대 한 `queueTrigger` hello에 사용할 수 있습니다 자리 표시자 `Blob` 특성의 `blobPath` hello hello 메시지에 대 한 콘텐츠를 포함 하는 매개 변수입니다.

hello 다음 예제에서는 `Stream` tooread 및 쓰기 blob 개체입니다. hello 큐 메시지는 hello textblobs 컨테이너에 있는 blob의 hello 이름입니다. 사용 하 여 hello blob의 복사본 "-새로운" 추가 된 toohello 만든 hello 동일한 컨테이너입니다.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

hello `Blob` 특성 생성자는 `blobPath` hello 컨테이너 및 blob 이름을 지정 하는 매개 변수입니다. 이 자리 표시자에 대 한 자세한 내용은 참조 [어떻게 toouse Azure blob 저장소에 hello WebJobs SDK로](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Hello 특성 데코 레이트 하는 경우는 `Stream` 개체를 다른 생성자 매개 변수 지정 hello `FileAccess` 읽기, 쓰기 또는 읽기/쓰기 모드입니다.

hello 다음 예제에서는 한 `CloudBlockBlob` toodelete blob 개체입니다. hello 큐 메시지는 hello blob의 hello 이름입니다.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a> POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지
Hello 큐 메시지의 JSON으로 저장 하는 POCO에 대 한 hello에 hello 개체의 속성 이름을 지정 하는 자리 표시자를 사용할 수 있습니다 `Queue` 특성의 `blobPath` 매개 변수입니다. [큐 메타데이터 속성 이름](#queuemetadata) 을 자리 표시자로 사용할 수도 있습니다.

hello 다음 예제에서는 blob tooa 새 blob을 복사 다른 확장명으로 합니다. hello 큐 메시지는 한 `BlobInformation` 포함 된 개체 `BlobName` 및 `BlobNameWithoutExtension` 속성입니다. hello 속성 이름이 hello에 대 한 hello blob 경로에 대 한 자리 표시자로 사용 됩니다 `Blob` 특성입니다.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

hello SDK hello를 사용 하 여 [Newtonsoft.Json NuGet 패키지](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize 및 메시지를 역직렬화 합니다. Hello WebJobs SDK를 사용 하지 않는 프로그램에서 메시지 큐를 만들면 해당 hello SDK 구문 분석할 수 있는 다음 예에서는 toocreate POCO 큐 메시지 hello 같은 코드를 작성할 수 있습니다.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Blob tooan 개체를 바인딩하기 전에 일부 작동 toodo 함수에서 해야 할 경우 hello 특성 hello hello 함수 본문에 사용할 수 있습니다 [hello 큐 특성에 대해 설명한 것 처럼](#ibinder)합니다.

### <a id="blobattributetypes"></a>형식 hello를 사용할 수 있는 특성 Blob
hello `Blob` 특성 유형만 hello로 사용할 수 있습니다.

* `Stream`(읽기 또는 쓰기 파일 그룹, hello FileAccess 생성자 매개 변수를 사용 하 여 지정)
* `TextReader`
* `TextWriter`
* `string` (읽기)
* `out string`(쓰기; hello 문자열 매개 변수는 hello 함수를 반환 하는 경우 null이 아닌 경우에 blob을 만듭니다.)
* POCO(읽기)
* POCO 아웃 (쓰기; 항상 blob, 만들어집니다 null 개체로 hello 함수가 반환 될 때 POCO 매개 변수가 null 이면)
* `CloudBlobStream` (쓰기)
* `ICloudBlob` (읽기 또는 쓰기)
* `CloudBlockBlob` (읽기 또는 쓰기)
* `CloudPageBlob` (읽기 또는 쓰기)

## <a id="poison"></a>어떻게 toohandle 포이즌 메시지
메시지 내용이 함수 toofail 하면 라고 *포이즌 메시지*합니다. Hello 함수가 실패할 때 hello 큐 메시지는 삭제 되지 않습니다 및 결국 선택 다시 발생 시키는 hello 주기 toobe 반복 합니다. hello SDK 중단할 수 있으며 자동으로 hello 주기 후 제한 된 수의 반복 하거나 수동으로 수행할 수 있습니다.

### <a name="automatic-poison-message-handling"></a>자동 포이즌 메시지 처리
hello SDK too5 번 tooprocess 큐 메시지를 함수를 호출 합니다. Hello 다섯 번째 시도 실패 하면 hello 메시지 이동된 tooa 포이즌 큐는입니다. [hello 최대 재시도 횟수를 구성할 수](#config)합니다.

hello 포이즌 큐 이름은 *{originalqueuename}*-포이즌 합니다. 작성할 수 있습니다 함수 tooprocess 메시지 hello 포이즌 큐에서 해당 로그 하거나 수동 주의가 필요한 알림을 보내기.

다음 예에서는 hello hello에 `CopyBlob` 큐 메시지에는 존재 하지 않는 blob의 hello 이름을 포함 하는 경우 함수 실패 합니다. 에 도달 하면 hello 메시지 hello copyblobqueue 큐 toohello copyblobqueue 포이즌 큐에서 이동 됩니다. hello `ProcessPoisonMessage` 로그 환영 포이즌 메시지가 다음 합니다.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

hello 다음 그림에서는 이러한 함수에서 콘솔 출력 포이즌 메시지를 처리 하는 경우.

![포이즌 메시지 처리에 대한 콘솔 출력](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>수동 포이즌 메시지 처리
Hello 횟수 만큼 메시지 선택 않은 처리를 위해 추가 하 여 가져올 수 있습니다는 `int` 라는 매개 변수 `dequeueCount` tooyour 함수입니다. 검사 hello 함수 코드에서의 개수를 큐에서 제거 하 고 hello 다음 예제와 같이 hello 번호가 임계값을 초과 하는 경우 사용자 고유의 포이즌 메시지 처리를 수행할 수 있습니다.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a>어떻게 tooset 구성 옵션
Hello를 사용할 수 있습니다 `JobHostConfiguration` 형식 tooset hello 다음 구성 옵션:

* 코드에서 hello SDK 연결 문자열을 설정 합니다.
* 최대 큐에서 제거 횟수와 같은 `QueueTrigger` 설정을 구성합니다.
* 구성에서 큐 이름을 가져옵니다.

### <a id="setconnstr"></a>코드에서 SDK 연결 문자열 설정
Hello SDK 연결 문자열에에서 설정 코드 수 있습니다 있습니다 toouse 구성 파일 또는 환경 변수에서 고유한 연결 문자열 이름을 hello 다음 예제와 같이 합니다.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="configqueue"></a>QueueTrigger 설정 구성
Hello 다음 toohello 큐 메시지 처리에 적용 되는 설정을 구성할 수 있습니다.

* hello 병렬 실행 toobe 동시에 선택 하는 큐 메시지의 최대 수 (기본값은 16).
* 큐 메시지 tooa 포이즌 큐를 보내기 전에 최대 재시도 횟수를 hello (기본값은 5).
* 큐가 비어 다시 폴링하기 전에 hello 최대 대기 시간 (기본값은 1 분)입니다.

hello 방법을 예제와 다음 tooconfigure 이러한 설정:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>코드에서 WebJobs SDK 생성자 매개 변수 값 설정
큐 이름, blob 이름 또는 컨테이너 toospecify 사용할 경우에 따라 또는 테이블 이름을 하드 코드 하지 않고 코드. 예를 들어 toospecify hello 큐 이름에 대 한 경우가 `QueueTrigger` 구성 파일이 나 환경 변수에서입니다.

전달 하 여 수행할 수 있습니다는 `NameResolver` toohello 개체 `JobHostConfiguration` 유형입니다. WebJobs SDK 특성 생성자 매개 변수, 백분율 (%) 기호 둘러싸인 특수 한 자리 표시자를 포함 및 `NameResolver` hello 실제 값 toobe 이와 같은 자리 표시자를 대신 사용 되는 코드를 지정 합니다.

예를 들어 toouse 한다고 가정 큐 이름은 hello 테스트 환경에서 logqueuetest과 프로덕션 환경에서 명명된 한 logqueueprod입니다. 원하는 hello에 있는 항목의 toospecify hello 이름을 하드 코드 된 큐 이름 대신 `appSettings` hello 실제 큐 이름이 있는 컬렉션입니다. 경우 hello `appSettings` 키는 logqueue, 다음 예제는 hello 함수 보여 줍니다.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

프로그램 `NameResolver` 클래스에서 hello 큐 이름을 가져올 다음 수 `appSettings` hello 다음 예제와 같이:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Hello 전달 `NameResolver` toohello 클래스 `JobHost` hello 다음 예제와 같이 개체입니다.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**참고:** 큐, 테이블 및 blob 이름 해결 하는 함수를 호출할 때마다 하지만 hello 응용 프로그램을 시작 하는 경우에 blob 컨테이너 이름이 확인 됩니다. Hello 작업이 실행 되는 동안 blob 컨테이너 이름을 변경할 수 없습니다.

## <a id="manual"></a>어떻게 tootrigger 함수 수동으로
tootrigger 함수를 직접 사용 하 여 hello `Call` 또는 `CallAsync` 메서드 hello `JobHost` 개체 및 hello `NoAutomaticTrigger` hello 다음 예제와 같이 hello 함수에 특성입니다.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a id="logs"></a>Toowrite 기록 하는 방법
hello 대시보드 두 위치에서 로그를 보여 줍니다: WebJob hello에 대 한 hello 페이지와 특정 웹 작업 호출에 대 한 hello 페이지입니다.

![WebJob 페이지에서 로그](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![함수 호출 페이지에서 로그](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Hello 또는 함수에서 호출 하는 콘솔 메서드에서 출력 `Main()` 메서드가 특정 메서드 호출에 대 한 hello 페이지 아닌 WebJob hello에 대 한 hello 대시보드 페이지에 나타납니다. 메서드 시그니처의 매개 변수에서 얻을 수 있는 hello TextWriter 개체에서 출력 된 메서드 호출에 대 한 hello 대시보드 페이지에 나타납니다.

Hello 콘솔 단일 스레드 hello에서 많은 작업 함수를 실행 중일 수 있습니다 하는 동안이 콘솔 출력 연결 된 tooa 특정 메서드 호출 수 없습니다 동시 합니다. 바로 이러한 이유로 hello SDK 자체 고유한 로그 기록기 개체와 각 함수 호출을 제공 합니다.

toowrite [응용 프로그램 추적 로그](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)를 사용 하 여 `Console.Out` (정보로 표시 된 로그 생성) 및 `Console.Error` (오류로 표시 된 로그 생성). 대체 항목은 toouse [추적 또는 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), 경고, 자세한 정보를 제공 하 고 더하기 tooInfo 및 오류의 위험 수준. 응용 프로그램 추적 로그 hello 웹 앱 로그 파일, Azure 테이블에에서 표시 하거나 Azure 웹 앱을 구성 하는 방법에 따라 Azure blob 합니다. 모든 콘솔 출력의 true 이면 hello 가장 최근의 100 응용 프로그램 로그는 함수 호출에 대 한 hello 페이지가 아닌 WebJob hello에 대 한 hello 대시보드 페이지에도 표시 됩니다.

콘솔 출력 hello hello 프로그램을 로컬로 실행 하는 경우에 하지는 Azure WebJob에 hello 프로그램을 실행 하는 경우에 대시보드 또는 다른 환경에 나타납니다.

처리량이 많은 시나리오에 대해 대시보드 로깅을 사용하지 않도록 설정합니다. 기본적으로 hello SDK 로그 toostorage 쓰고 많은 메시지를 처리 하는 경우이 작업 성능이 저하 됩니다. 로깅, toodisable hello 다음 예제와 같이 hello 대시보드 연결 문자열 toonull를 설정 합니다.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

hello 다음 예제에서는 여러 가지 방법을 보여 줍니다 toowrite 로그:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

WebJobs SDK 대시보드 hello에서 출력을 hello hello `TextWriter` 개체 toohello 페이지 특정 작업에 대해 수행 하는 경우 나타남 함수 호출 및 클릭 **토글 출력**:

![함수 호출 링크 클릭](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![함수 호출 페이지에서 로그](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

에 hello WebJobs SDK 대시보드, 가장 최근의 100 hello 줄 콘솔의 출력 표시를 하지 않습니다 (hello 함수 호출)을 위해 WebJob hello에 대 한 toohello 페이지로 이동 하 고 클릭 **토글 출력**합니다.

![출력 설정/해제 클릭](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

연속 WebJob에서 응용 프로그램 로그에 표시/데이터/작업/연속/*{webjobname}*/job_log.txt hello 웹 응용 프로그램 파일 시스템에 있습니다.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Azure blob hello 응용 프로그램 로그는 다음과 같이 표시: 26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write-2014-09-Hello world!, 2014-09-26T21:01:13, 오류, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error-Hello world!, 26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out-2014-09-Hello world!,

와 Azure 테이블 hello `Console.Out` 및 `Console.Error` 로그는 다음과 같습니다.

![테이블에 대한 정보 로그](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![테이블에 대한 오류 로그](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

자신만로 거에 tooplug를 원하는 경우 참조 [이 예제](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs)합니다.

## <a id="errors"></a>어떻게 toohandle 오류 시간 제한을 구성 하 고
hello WebJobs SDK도 포함 되어는 [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) toocause 함수 toobe 취소 하는 경우 사용할 수 있는 특성 지정된 된 기간 내에 완료 하지 않습니다. Hello를 사용 하 여 지정 된 기간 내에 너무 많은 오류가 발생 하는 경우 경고 tooraise을 하려는 경우 `ErrorTrigger` 특성입니다. 다음은 [ErrorTrigger 예제](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring)입니다.

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

동적으로 사용 하지 않도록 설정 하을 트리거할 수 있습니다, 응용 프로그램 설정 또는 환경 변수 이름이 될 수 있는 구성 스위치를 사용 하 여 여부 함수 toocontrol 사용 수 있습니다. 샘플 코드에 대 한 참조 hello `Disable` 특성 [hello WebJobs SDK 샘플 리포지토리](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs)합니다.

## <a id="nextsteps"></a> 다음 단계
이 가이드는 코드를 제공 하는 방법을 보여 주는 샘플 toohandle Azure 큐 작업에 대 한 일반적인 시나리오입니다. Azure WebJobs toouse 및 hello WebJobs SDK를 참조 하는 방법에 대 한 자세한 내용은 [Azure WebJobs 리소스 권장](http://go.microsoft.com/fwlink/?linkid=390226)합니다.
