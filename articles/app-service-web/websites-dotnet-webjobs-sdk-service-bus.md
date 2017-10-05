---
title: "WebJob SDK를 사용하여 Azure 서비스 버스로 작업하는 방법"
description: "WebJobs SDK를 사용하여 Azure 서비스 버스 큐 및 항목으로 작업하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7cec03cae5d20d1ead9eb24e99415c33d8b76f05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-service-bus-with-the-webjobs-sdk"></a><span data-ttu-id="3933f-103">WebJob SDK를 사용하여 Azure 서비스 버스로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="3933f-103">How to use Azure Service Bus with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="3933f-104">개요</span><span class="sxs-lookup"><span data-stu-id="3933f-104">Overview</span></span>
<span data-ttu-id="3933f-105">이 가이드에서는 Azure 서비스 버스 메시지를 받았을 때 프로세스를 트리거하는 방법을 보여 주는 C# 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-105">This guide provides C# code samples that show how to trigger a process when an Azure Service Bus message is received.</span></span> <span data-ttu-id="3933f-106">코드 샘플에서는 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 버전 1.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-106">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="3933f-107">이 가이드에서는 [저장소 계정을 가리키는 연결 문자열을 사용하여 Visual Studio에서 WebJob 프로젝트를 만드는 방법](websites-dotnet-webjobs-sdk-get-started.md)을 알고 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md).</span></span>

<span data-ttu-id="3933f-108">코드 조각은 다음 예제와 같이 `JobHost` 개체를 만드는 코드가 아니라 함수만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-108">The code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

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

<span data-ttu-id="3933f-109">[전체 서비스 버스 코드 예제](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) 는 GitHub.com의 azure-webjobs-sdk-samples 리포지토리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-109">A [complete Service Bus code example](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Program.cs) is in the azure-webjobs-sdk-samples repository on GitHub.com.</span></span>

## <span data-ttu-id="3933f-110"><a id="prerequisites"></a> 필수 조건</span><span class="sxs-lookup"><span data-stu-id="3933f-110"><a id="prerequisites"></a> Prerequisites</span></span>
<span data-ttu-id="3933f-111">서비스 버스로 작업하려면 다른 WebJobs SDK 패키지와 함께 [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-111">To work with Service Bus you have to install the [Microsoft.Azure.WebJobs.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/) NuGet package in addition to the other WebJobs SDK packages.</span></span> 

<span data-ttu-id="3933f-112">또한 저장소 연결 문자열과 함께 AzureWebJobsServiceBus 연결 문자열을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-112">You also have to set the AzureWebJobsServiceBus connection string in addition to the storage connection strings.</span></span>  <span data-ttu-id="3933f-113">다음 예제와 같이 App.config 파일의 `connectionStrings` 섹션에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-113">You can do this in the `connectionStrings` section of the App.config file, as shown in the following example:</span></span>

        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsServiceBus" connectionString="Endpoint=sb://[yourServiceNamespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[yourKey]"/>
        </connectionStrings>

<span data-ttu-id="3933f-114">App.config 파일에 서비스 버스 연결 문자열 설정을 포함하는 샘플 프로젝트의 경우 [서비스 버스 예제](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3933f-114">For a sample project that includes the Service Bus connection string setting in the App.config file, see [Service Bus example](https://github.com/Azure/azure-webjobs-sdk-samples/tree/master/BasicSamples/ServiceBus).</span></span> 

<span data-ttu-id="3933f-115">Azure 런타임 환경에서 연결 문자열을 설정할 수도 있으며, 이 문자열은 Azure에서 WebJob이 실행될 때 App.config 설정을 재정의합니다. 자세한 내용은 [WebJobs SDK 시작](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3933f-115">The connection strings can also be set in the Azure runtime environment, which then overrides the App.config settings when the WebJob runs in Azure; for more information, see [Get Started with the WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md#configure-the-web-app-to-use-your-azure-sql-database-and-storage-account).</span></span>

## <span data-ttu-id="3933f-116"><a id="trigger"></a> 서비스 버스 큐 메시지가 수신될 때 함수를 트리거하는 방법</span><span class="sxs-lookup"><span data-stu-id="3933f-116"><a id="trigger"></a> How to trigger a function when a Service Bus queue message is received</span></span>
<span data-ttu-id="3933f-117">큐 메시지가 수신될 때 WebJobs SDK에서 호출하는 함수를 작성하려면 `ServiceBusTrigger` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-117">To write a function that the WebJobs SDK calls when a queue message is received, use the `ServiceBusTrigger` attribute.</span></span> <span data-ttu-id="3933f-118">특성 생성자는 폴링할 큐의 이름을 지정하는 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-118">The attribute constructor takes a parameter that specifies the name of the queue to poll.</span></span>

### <a name="how-servicebustrigger-works"></a><span data-ttu-id="3933f-119">ServiceBusTrigger 작동 방식</span><span class="sxs-lookup"><span data-stu-id="3933f-119">How ServiceBusTrigger works</span></span>
<span data-ttu-id="3933f-120">SDK는 `PeekLock` 모드로 메시지를 받아 함수가 성공적으로 완료된 경우 메시지에서 `Complete`를 호출하고, 함수가 실패한 경우 `Abandon`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-120">The SDK receives a message in `PeekLock` mode and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> <span data-ttu-id="3933f-121">함수가 `PeekLock` 시간 제한보다 오래 실행되는 경우 잠금이 자동으로 갱신됩니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-121">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<span data-ttu-id="3933f-122">서비스 버스는 WebJobs SDK에 의해 제어 또는 구성할 수 없는 자체 포이즌 큐 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-122">Service Bus does its own poison queue handling which cannot be controlled or configured by the WebJobs SDK.</span></span> 

### <a name="string-queue-message"></a><span data-ttu-id="3933f-123">문자열 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="3933f-123">String queue message</span></span>
<span data-ttu-id="3933f-124">다음 코드 샘플은 문자열이 포함된 큐 메시지를 읽고 WebJobs SDK 대시보드에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-124">The following code sample reads a queue message that contains a string and writes the string to the WebJobs SDK dashboard.</span></span>

        public static void ProcessQueueMessage([ServiceBusTrigger("inputqueue")] string message, 
            TextWriter logger)
        {
            logger.WriteLine(message);
        }

<span data-ttu-id="3933f-125">**참고:** WebJobs SDK를 사용하지 않는 응용 프로그램에서 큐 메시지를 만드는 경우 [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) 을 "text/plain"으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-125">**Note:** If you are creating the queue messages in an application that doesn't use the WebJobs SDK, make sure to set [BrokeredMessage.ContentType](http://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.contenttype.aspx) to "text/plain".</span></span>

### <a name="poco-queue-message"></a><span data-ttu-id="3933f-126">POCO 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="3933f-126">POCO queue message</span></span>
<span data-ttu-id="3933f-127">SDK에서는 POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 유형에 대한 JSON이 포함된 큐 메시지를 자동으로 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-127">The SDK will automatically deserialize a queue message that contains JSON for a POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) type.</span></span> <span data-ttu-id="3933f-128">다음 코드 샘플은 `BlobName` 속성을 가진 `BlobInformation` 개체가 포함된 큐 메시지를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-128">The following code sample reads a queue message that contains a `BlobInformation` object which has a `BlobName` property:</span></span>

        public static void WriteLogPOCO([ServiceBusTrigger("inputqueue")] BlobInformation blobInfo,
            TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="3933f-129">POCO 속성을 사용하여 동일한 함수의 Blob 및 테이블로 작업하는 방법을 보여 주는 코드 샘플은 [이 문서의 저장소 큐 버전](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3933f-129">For code samples showing how to use properties of the POCO to work with blobs and tables in the same function, see the [storage queues version of this article](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#pocoblobs).</span></span>

<span data-ttu-id="3933f-130">큐 메시지를 만든 코드가 WebJobs SDK를 사용하지 않을 경우 다음 예제와 유사한 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-130">If your code that creates the queue message doesn't use the WebJobs SDK, use code similar to the following example:</span></span>

        var client = QueueClient.CreateFromConnectionString(ConfigurationManager.ConnectionStrings["AzureWebJobsServiceBus"].ConnectionString, "blobadded");
        BlobInformation blobInformation = new BlobInformation () ;
        var message = new BrokeredMessage(blobInformation);
        client.Send(message);

### <a name="types-servicebustrigger-works-with"></a><span data-ttu-id="3933f-131">ServiceBusTrigger가 작동하는 유형</span><span class="sxs-lookup"><span data-stu-id="3933f-131">Types ServiceBusTrigger works with</span></span>
<span data-ttu-id="3933f-132">`string` 및 POCO 유형 외에 바이트 배열 또는 `BrokeredMessage` 개체에서 `ServiceBusTrigger` 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-132">Besides `string` and POCO  types, you can use the `ServiceBusTrigger` attribute with a byte array or a `BrokeredMessage` object.</span></span>

## <span data-ttu-id="3933f-133"><a id="create"></a> 서비스 버스 큐 메시지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3933f-133"><a id="create"></a> How to create Service Bus queue messages</span></span>
<span data-ttu-id="3933f-134">새 큐 메시지를 만드는 함수를 작성하려면 `ServiceBus` 특성을 사용하고 특성 생성자로 큐 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-134">To write a function that creates a new queue message use the `ServiceBus` attribute and pass in the queue name to the attribute constructor.</span></span> 

### <a name="create-a-single-queue-message-in-a-non-async-function"></a><span data-ttu-id="3933f-135">비동기가 아닌 함수로 단일 큐 메시지를 만들기</span><span class="sxs-lookup"><span data-stu-id="3933f-135">Create a single queue message in a non-async function</span></span>
<span data-ttu-id="3933f-136">다음 코드 샘플은 출력 매개 변수를 사용하여 "inputqueue"라는 큐에 수신된 메시지와 동일한 콘텐츠를 가진 새 메시지를 "outputqueue"라는 큐에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-136">The following code sample uses an output parameter to create a new message in the queue named "outputqueue" with the same content as the message received in the queue named "inputqueue".</span></span>

        public static void CreateQueueMessage(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] out string outputQueueMessage)
        {
            outputQueueMessage = queueMessage;
        }

<span data-ttu-id="3933f-137">단일 큐 메시지를 만들기 위한 출력 매개 변수는 다음 유형 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-137">The output parameter for creating a single queue message can be any of the following types:</span></span>

* `string`
* `byte[]`
* `BrokeredMessage`
* <span data-ttu-id="3933f-138">사용자가 정의한 serialize 가능 POCO 유형.</span><span class="sxs-lookup"><span data-stu-id="3933f-138">A serializable POCO type that you define.</span></span> <span data-ttu-id="3933f-139">JSON으로 자동으로 serialize됨</span><span class="sxs-lookup"><span data-stu-id="3933f-139">Automatically serialized as JSON.</span></span>

<span data-ttu-id="3933f-140">POCO 유형 매개 변수의 경우 함수가 종료되면 큐 메시지가 항상 만들어집니다. 매개 변수가 null인 경우에는 SDK에서 메시지가 수신되고 deserialize될 때 null을 반환하는 큐 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-140">For POCO type parameters, a queue message is always created when the function ends; if the parameter is null, the SDK creates a queue message that will return null when the message is received and deserialized.</span></span> <span data-ttu-id="3933f-141">다른 유형의 경우 매개 변수가 null이면 큐 메시지가 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-141">For the other types, if the parameter is null no queue message is created.</span></span>

### <a name="create-multiple-queue-messages-or-in-async-functions"></a><span data-ttu-id="3933f-142">여러 큐 메시지 만들기 또는 비동기 함수로 큐 메시지 만들기</span><span class="sxs-lookup"><span data-stu-id="3933f-142">Create multiple queue messages or in async functions</span></span>
<span data-ttu-id="3933f-143">여러 메시지를 만들려면 다음 코드 샘플과 같이 `ICollector<T>` 또는 `IAsyncCollector<T>`에서 `ServiceBus` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-143">To create multiple messages, use  the `ServiceBus` attribute with `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following code sample:</span></span>

        public static void CreateQueueMessages(
            [ServiceBusTrigger("inputqueue")] string queueMessage,
            [ServiceBus("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="3933f-144">`Add` 메서드를 호출하면 각 큐 메시지가 즉시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-144">Each queue message is created immediately when the `Add` method is called.</span></span>

## <span data-ttu-id="3933f-145"><a id="topics"></a>서비스 버스 항목으로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="3933f-145"><a id="topics"></a>How to work with Service Bus topics</span></span>
<span data-ttu-id="3933f-146">서비스 버스 항목에 메시지가 수신될 때 SDK에서 호출하는 함수를 작성하려면 다음 코드 샘플과 같이 항목 이름 및 구독 이름을 가져오는 생성자와 함께 `ServiceBusTrigger` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-146">To write a function that the SDK calls when a message is received on a Service Bus topic, use the `ServiceBusTrigger` attribute with the constructor that takes topic name and subscription name, as shown in the following code sample:</span></span>

        public static void WriteLog([ServiceBusTrigger("outputtopic","subscription1")] string message,
            TextWriter logger)
        {
            logger.WriteLine("Topic message: " + message);
        }

<span data-ttu-id="3933f-147">항목에 대한 메시지를 만들려면 큐 이름과 동일한 방식으로 항목 이름에서 `ServiceBus` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-147">To create a message on a topic, use the `ServiceBus` attribute with a topic name the same way you use it with a queue name.</span></span>

## <a name="features-added-in-release-11"></a><span data-ttu-id="3933f-148">버전 1.1에 추가된 기능</span><span class="sxs-lookup"><span data-stu-id="3933f-148">Features added in release 1.1</span></span>
<span data-ttu-id="3933f-149">릴리스 1.1에서 다음과 같은 기능이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-149">The following features were added in release 1.1:</span></span>

* <span data-ttu-id="3933f-150">`ServiceBusConfiguration.MessagingProvider`를 통해 메시지 처리를 상세하게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-150">Allow deep customization of message processing via `ServiceBusConfiguration.MessagingProvider`.</span></span>
* <span data-ttu-id="3933f-151">`MessagingProvider`는 서비스 버스 `MessagingFactory` 및 `NamespaceManager`의 사용자 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-151">`MessagingProvider` supports customization of the Service Bus `MessagingFactory` and `NamespaceManager`.</span></span>
* <span data-ttu-id="3933f-152">`MessageProcessor` 전략 패턴을 통해 큐/토픽별로 프로세서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-152">A `MessageProcessor` strategy pattern allows you to specify a processor per queue/topic.</span></span>
* <span data-ttu-id="3933f-153">메시지 처리 동시성이 기본적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-153">Message processing concurrency is supported by default.</span></span> 
* <span data-ttu-id="3933f-154">`ServiceBusConfiguration.MessageOptions`를 통해 `OnMessageOptions`를 쉽게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-154">Easy customization of `OnMessageOptions` via `ServiceBusConfiguration.MessageOptions`.</span></span>
* <span data-ttu-id="3933f-155">관리 권한이 없을 수 있는 시나리오에 대해 `ServiceBusTriggerAttribute`/`ServiceBusAttribute`에서 [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71)를 지정하는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-155">Allow [AccessRights](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/ServiceBus/Functions.cs#L71) to be specified on `ServiceBusTriggerAttribute`/`ServiceBusAttribute` (for scenarios where you might not have Manage rights).</span></span> <span data-ttu-id="3933f-156">관리 AccessRights가 없으면 Azure Webjob에서 존재하지 않는 큐 및 토픽을 자동으로 프로비전할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-156">Note that Azure WebJobs is unable to automatically provision non-existent queues and topics without Manage AccessRights.</span></span>

## <span data-ttu-id="3933f-157"><a id="queues"></a>저장소 큐 방법 문서에서 다루는 관련 항목</span><span class="sxs-lookup"><span data-stu-id="3933f-157"><a id="queues"></a>Related topics covered by the storage queues how-to article</span></span>
<span data-ttu-id="3933f-158">서비스 버스에 특정하지 않은 WebJobs SDK 시나리오에 대한 자세한 내용은 [WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3933f-158">For information about WebJobs SDK scenarios not specific to Service Bus, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="3933f-159">이 문서에서 다루는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-159">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="3933f-160">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="3933f-160">Async functions</span></span>
* <span data-ttu-id="3933f-161">여러 인스턴스</span><span class="sxs-lookup"><span data-stu-id="3933f-161">Multiple instances</span></span>
* <span data-ttu-id="3933f-162">정상 종료</span><span class="sxs-lookup"><span data-stu-id="3933f-162">Graceful shutdown</span></span>
* <span data-ttu-id="3933f-163">함수 본문에 WebJobs SDK 특성 사용</span><span class="sxs-lookup"><span data-stu-id="3933f-163">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="3933f-164">코드에서 SDK 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="3933f-164">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="3933f-165">코드에서 WebJobs SDK 생성자 매개 변수 값 설정</span><span class="sxs-lookup"><span data-stu-id="3933f-165">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="3933f-166">수동으로 함수 트리거</span><span class="sxs-lookup"><span data-stu-id="3933f-166">Trigger a function manually</span></span>
* <span data-ttu-id="3933f-167">로그 작성</span><span class="sxs-lookup"><span data-stu-id="3933f-167">Write logs</span></span>

## <span data-ttu-id="3933f-168"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="3933f-168"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="3933f-169">이 가이드에서는 Azure 서비스 버스 작업에 대한 일반적인 시나리오를 처리하는 방법을 보여 주는 코드 샘플을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="3933f-169">This guide has provided code samples that show how to handle common scenarios for working with Azure Service Bus.</span></span> <span data-ttu-id="3933f-170">Azure WebJob 및 WebJob SDK를 사용하는 방법에 대한 자세한 내용은 [Azure WebJob 권장 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3933f-170">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

