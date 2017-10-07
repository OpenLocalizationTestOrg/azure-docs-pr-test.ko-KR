---
title: "WebJobs SDK hello로 aaaHow toouse Azure 서비스 버스"
description: "Toouse Azure 서비스 버스 큐 및 항목을 WebJobs SDK hello 방법에 대해 알아봅니다."
services: app-service\web, service-bus
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 2114a934-135b-42b8-871c-6cc040214e76
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: cb801a9320a20c276da4f48c8941c09d3f09bb1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-service-bus-with-hello-webjobs-sdk"></a>와 toouse Azure 서비스 버스 방법 hello WebJobs SDK
## <a name="overview"></a>개요
이 가이드에서는 C# 코드 샘플 표시 하는 방법을 tootrigger Azure 서비스 버스 메시지를 받을 때 사용 하는 프로세스입니다. hello 코드 사용 샘플 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 버전 1.x 합니다.

hello 가이드 알고 있다고 가정 [toocreate 연결이 포함 된 Visual Studio에서 WebJob 프로젝트의 해당 지점 tooyour 저장소 계정 문자열 어떻게](websites-dotnet-webjobs-sdk-get-started.md)합니다.

hello를 만드는 코드를 hello hello 코드 조각은 함수, 표시 `JobHost` 다음이 예제와 같이 개체:

```
public class Program
{
   public static void Main()
   {
      JobHostConfiguration config = new JobHostConfiguration();
      config.UseServiceBus();
      JobHost host = new JobHost(config);
      host.RunAndBlock();
   }
}
```

A [전체 서비스 버스에 대 한 코드 예제에서는](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) GitHub.com에 hello webjobs sdk 샘플 azure 저장소에 있습니다.

## <a id="prerequisites"></a> 필수 조건
toowork tooinstall hello 서비스 버스에 있는 [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 패키지로 또한 toohello 다른 WebJobs SDK 패키지 합니다. 

또한 toohello 저장소 연결 문자열에 갖게 tooset hello AzureWebJobsServiceBus 연결 문자열입니다.  Hello에 이렇게 하려면 `connectionStrings` hello 다음 예제와 같이 hello App.config 파일의 섹션:

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

서비스 버스 연결 문자열 설정을 hello hello App.config 파일에 포함 된 샘플 프로젝트에 대 한 참조 [서비스 버스 예제](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)합니다. 

WebJob hello Azure;에서 실행 될 때에 다음 hello App.config 설정 재정의 하는 hello Azure 런타임 환경에 연결 문자열 hello를 설정할 수도 있습니다. 자세한 내용은 참조 [hello WebJobs SDK 시작](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)합니다.

## <a id="trigger"></a>서비스 버스 큐 메시지를 대기 하는 경우 함수 tootrigger 수신 되는 방법
큐 메시지를 받을 때 toowrite hello WebJobs SDK는 함수 호출, hello를 사용 하 여 `ServiceBusTrigger` 특성입니다. hello 특성 생성자 hello 큐 toopoll의 hello 이름을 지정 하는 매개 변수를 사용 합니다.

### <a name="how-servicebustrigger-works"></a>ServiceBusTrigger 작동 방식
hello SDK가 메시지에 `PeekLock` 모드 및 호출 `Complete` hello 함수는 성공적으로 완료 되 면 hello 메시지 또는 호출 `Abandon` hello 함수가 실패 한 경우. Hello 함수 hello 보다 오래 실행 되 면 `PeekLock` hello 잠금 제한 시간이 자동으로 갱신 합니다.

서비스 버스를 제어 하거나 hello WebJobs SDK 여 구성할 수 없는 자체 포이즌 큐 처리를 수행 합니다. 

### <a name="string-queue-message"></a>문자열 큐 메시지
hello 다음 코드 샘플 메시지를 읽고 큐 하는 문자열을 포함 하 고 hello 문자열 toohello WebJobs SDK 대시보드를 씁니다.

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

**참고:** hello 큐 메시지 hello WebJobs SDK를 사용 하지 않는 응용 프로그램에서 만드는 경우 확인 되었는지 tooset [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) 너무 "텍스트/일반"입니다.

### <a name="poco-queue-message"></a>POCO 큐 메시지
hello SDK는 POCO에 대 한 JSON이 포함 된 큐 메시지를 자동으로 deserialize 됩니다 [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 형식입니다. hello 다음 코드 샘플 메시지를 읽고 큐를 포함 하는 `BlobInformation` 있는 개체는 `BlobName` 속성:

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Blob 및 테이블에 있는 hello POCO toowork의 toouse 속성 동일 hello 방법을 보여 주는 코드 샘플에 대 한 함수를 hello 참조 [이 문서의 저장소 큐 버전](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)합니다.

Hello 큐 메시지를 작성 하는 코드 hello WebJobs SDK를 사용 하지 않는 경우 다음 예제 코드와 유사한 toohello를 사용 합니다.

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a>ServiceBusTrigger가 작동하는 유형
외에 `string` 및 POCO 형식 hello를 사용할 수 있습니다 `ServiceBusTrigger` 바이트 배열로 특성 또는 `BrokeredMessage` 개체입니다.

## <a id="create"></a>Toocreate 서비스 버스에서 메시지를 큐 하는 방법
toowrite 새 큐 메시지를 만드는 함수를 사용 하 여 hello `ServiceBus` 특성 및 hello 큐 이름 toohello 특성 생성자에 전달 합니다. 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a>비동기가 아닌 함수로 단일 큐 메시지를 만들기
아래의 코드 예제는 hello는 출력 매개 변수 toocreate hello 큐에서 새 메시지를 라는 "outputqueue" hello "inputqueue" 라는 hello 큐에서 받은 메시지 콘텐츠 다른 이름으로 같은 hello로 사용 합니다.

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

단일 큐 메시지를 만들기 위한 hello 출력 매개 변수 유형만 hello 중 하나일 수 있습니다.

* `string`
* `byte[]`
* `BrokeredMessage`
* 사용자가 정의한 serialize 가능 POCO 유형. JSON으로 자동으로 serialize됨

POCO 형식 매개 변수에 대해 큐 메시지는 항상 생성 hello 함수 끝나면; hello 매개 변수가 null 인 경우 hello SDK hello 메시지를 수신 하 고 역직렬화 하는 경우 null 반환 하는 큐 메시지를 만듭니다. Hello 다른 형식에 대 한, hello 매개 변수가 null 이면 큐 메시지 없이 만들어집니다.

### <a name="create-multiple-queue-messages-or-in-async-functions"></a>여러 큐 메시지 만들기 또는 비동기 함수로 큐 메시지 만들기
toocreate 여러 개의 메시지를 사용 하 여 hello `ServiceBus` 특성이 `ICollector<T>` 또는 `IAsyncCollector<T>`hello 아래의 코드 예제에에서 나온 것 처럼:

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

각 큐 메시지 즉시 때 만들어집니다 hello `Add` 메서드를 호출 합니다.

## <a id="topics"></a>어떻게 서비스 버스 주제와 toowork
서비스 버스 항목에서 메시지를 받으면 toowrite SDK hello 하는 함수 호출, hello를 사용 하 여 `ServiceBusTrigger` hello 아래의 코드 예제와 같이 항목 이름 및 구독 이름을 사용 하는 hello 생성자를 사용 하 여 특성:

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

항목을 사용 하 여 hello에 대 한 메시지 toocreate `ServiceBus` 동일 항목 이름 hello로 특성 큐 이름으로 사용 하는 방식으로 합니다.

## <a name="features-added-in-release-11"></a>버전 1.1에 추가된 기능
같은 기능 hello 버전 1.1에서에서 추가 되었습니다.

* `ServiceBusConfiguration.MessagingProvider`를 통해 메시지 처리를 상세하게 사용자 지정할 수 있습니다.
* `MessagingProvider`에서는 서비스 버스 hello 사용자 지정할 `MessagingFactory` 및 `NamespaceManager`합니다.
* A `MessageProcessor` 전략 패턴 있습니다 toospecify 큐/항목당 프로세서.
* 메시지 처리 동시성이 기본적으로 지원됩니다. 
* `ServiceBusConfiguration.MessageOptions`를 통해 `OnMessageOptions`를 쉽게 사용자 지정할 수 있습니다.
* 허용 [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) 에 지정 된 toobe `ServiceBusTriggerAttribute` / `ServiceBusAttribute` (에 대 한 권한을 관리 하는 시나리오에 없는 것일 수 있습니다). Azure WebJobs 없습니다 tooautomatically 프로 비전 존재 하지 않는 큐 및 항목 AccessRights 관리 하지 않고 인지 확인 합니다.

## <a id="queues"></a>Hello 저장소 큐 방법 tooarticle에서 포함 된 관련된 항목
WebJobs SDK 시나리오에 대 한 정보에 대 한 특정 하지 않은 tooService 버스 참조 [toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법을](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)합니다. 

이 문서에서 다루는 항목 hello 다음과를 같습니다.

* 비동기 함수
* 여러 인스턴스
* 정상 종료
* WebJobs SDK 특성 hello 함수 본문에서 사용 하 여
* 코드에서 hello SDK 연결 문자열을 설정 합니다.
* 코드에서 WebJobs SDK 생성자 매개 변수 값 설정
* 수동으로 함수 트리거
* 로그 작성

## <a id="nextsteps"></a> 다음 단계
이 가이드는 코드를 제공 하는 방법을 보여 주는 샘플 toohandle Azure 서비스 버스를 사용 하기 위한 일반적인 시나리오입니다. Azure WebJobs toouse 및 hello WebJobs SDK를 참조 하는 방법에 대 한 자세한 내용은 [Azure WebJobs 리소스 권장](http://go.microsoft.com/fwlink/?linkid=390226)합니다.

