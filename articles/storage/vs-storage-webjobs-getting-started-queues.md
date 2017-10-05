---
title: "Queue Storage 및 Visual Studio 연결된 서비스 시작(WebJob 프로젝트) | Microsoft Docs"
description: "Visual Studio 연결된 서비스를 사용하여 저장소 계정에 연결한 후 WebJob 프로젝트에서 Azure 큐 저장소 사용을 시작하는 방법입니다."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="18c3f-103">Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(WebJob 프로젝트)</span><span class="sxs-lookup"><span data-stu-id="18c3f-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="18c3f-104">개요</span><span class="sxs-lookup"><span data-stu-id="18c3f-104">Overview</span></span>
<span data-ttu-id="18c3f-105">이 문서에서는 Visual Studio **연결된 서비스 추가** 대화 상자를 사용하여 Azure Storage 계정을 만들거나 참조한 후 Visual Studio Azure WebJob프로젝트에서 Azure Queue Storage를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="18c3f-106">Visual Studio **연결된 서비스 추가** 대화 상자를 사용하여 WebJob 프로젝트에 저장소 계정을 추가하는 경우 적절한 Azure 저장소 NuGet 패키지가 설치되고, 적절한 .NET 참조가 프로젝트에 추가되며, App.config 파일에서 저장소 계정에 대한 연결 문자열이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="18c3f-107">이 문서에서는 Azure 큐 저장소 서비스에서 Azure WebJobs SDK 버전 1.x를 사용하는 방법을 보여 주는 C# 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="18c3f-108">Azure 큐 저장소는 HTTP 또는 HTTPS를 사용하여 인증된 호출을 통해 전 세계 어디에서나 액세스할 수 있는 다수의 메시지를 저장하기 위한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="18c3f-109">단일 큐 메시지의 크기는 최대 64KB일 수 있으며, 하나의 큐에 저장소 계정의 총 용량 제한까지 수백만 개의 메시지가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="18c3f-110">자세한 내용은 [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="18c3f-111">ASP.NET에 대한 자세한 내용은 [ASP.NET(영문)](http://www.asp.net)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="18c3f-112">큐 메시지를 받을 때 함수를 트리거하는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="18c3f-113">큐 메시지가 수신될 때 WebJobs SDK에서 호출하는 함수를 작성하려면 **QueueTrigger** 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="18c3f-114">특성 생성자는 폴링할 큐의 이름을 지정하는 문자열 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="18c3f-115">큐 이름을 동적으로 설정하는 방법을 알아보려면 [구성 옵션을 설정하는 방법](#how-to-set-configuration-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="18c3f-116">문자열 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-116">String queue messages</span></span>
<span data-ttu-id="18c3f-117">다음 예제에서는 큐에 문자열 메시지가 포함되므로 큐 메시지의 콘텐츠를 포함하는 **logMessage**라는 문자열 매개 변수에 **QueueTrigger**가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="18c3f-118">이 함수는 [대시보드에 로그 메시지를 씁니다](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="18c3f-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="18c3f-119">**string** 외에도 매개 변수는 바이트 배열, **CloudQueueMessage** 개체 또는 사용자가 정의한 POCO일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="18c3f-120">POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="18c3f-121">다음 예제에서 큐 메시지에는 **BlobName** 속성을 포함하는 **BlobInformation** 개체에 대한 JSON이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="18c3f-122">SDK에서 자동으로 개체를 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="18c3f-123">이 SDK는 [Newtonsoft.Json NuGet 패키지](http://www.nuget.org/packages/Newtonsoft.Json) 를 사용하여 메시지를 직렬화 및 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="18c3f-124">WebJobs SDK를 사용하지 않는 프로그램에서 큐 메시지를 만드는 경우 다음 예제와 같은 코드를 작성하여 SDK에서 구문 분석할 수 있는 POCO 큐 메시지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="18c3f-125">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="18c3f-125">Async functions</span></span>
<span data-ttu-id="18c3f-126">다음 비동기 함수는 [대시보드에 로그를 씁니다](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="18c3f-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="18c3f-127">Blob을 복사하는 다음 예제와 같이 비동기 함수는 [취소 토큰](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="18c3f-128">**queueTrigger** 자리 표시자에 대한 자세한 내용은 [Blob](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="18c3f-129">QueueTrigger 특성이 작동하는 유형</span><span class="sxs-lookup"><span data-stu-id="18c3f-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="18c3f-130">다음 유형에서 **QueueTrigger** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="18c3f-131">**string**</span><span class="sxs-lookup"><span data-stu-id="18c3f-131">**string**</span></span>
* <span data-ttu-id="18c3f-132">JSON으로 serialize된 POCO 유형</span><span class="sxs-lookup"><span data-stu-id="18c3f-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="18c3f-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="18c3f-133">**byte[]**</span></span>
* <span data-ttu-id="18c3f-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="18c3f-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="18c3f-135">폴링 알고리즘</span><span class="sxs-lookup"><span data-stu-id="18c3f-135">Polling algorithm</span></span>
<span data-ttu-id="18c3f-136">SDK는 무작위 지수 백오프 알고리즘을 구현하여 유휴 큐 폴링이 저장소 트랜잭션 비용에 미치는 영향을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="18c3f-137">메시지가 발견되면 SDK는 2초 대기하고 다른 메시지가 있는지 확인하며, 메시지가 발견되지 않으면 4초 정도 대기하고 나서 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="18c3f-138">후속 시도로 큐 메시지를 가져오지 못하면 최대 대기 시간(기본값 1분)에 도달할 때까지 대기 시간이 계속 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="18c3f-139">[최대 대기 시간은 구성 가능합니다](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="18c3f-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="18c3f-140">여러 인스턴스</span><span class="sxs-lookup"><span data-stu-id="18c3f-140">Multiple instances</span></span>
<span data-ttu-id="18c3f-141">웹 앱이 여러 인스턴스에서 실행되는 경우 연속적인 WebJob이 각 컴퓨터에서 실행되고, 각 컴퓨터는 트리거를 기다렸다가 함수 실행을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="18c3f-142">일부 시나리오에서는 이로 인해 일부 함수가 동일한 데이터를 두 번 처리하게 될 수 있으므로 함수는 역등원이어야 합니다(같은 입력 데이터로 반복 호출해도 중복된 결과가 나오지 않도록 작성).</span><span class="sxs-lookup"><span data-stu-id="18c3f-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="18c3f-143">병렬 실행</span><span class="sxs-lookup"><span data-stu-id="18c3f-143">Parallel execution</span></span>
<span data-ttu-id="18c3f-144">여러 함수가 서로 다른 큐에서 수신 대기 중이면 메시지가 동시에 수신될 경우 SDK에서 병렬로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="18c3f-145">단일 큐에 대해 여러 메시지가 수신되는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="18c3f-146">기본적으로 SDK는 한 번에 16개의 큐 메시지를 일괄로 가져오고 해당 메시지를 병렬로 처리하는 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="18c3f-147">[일괄 처리 크기는 구성 가능합니다](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="18c3f-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="18c3f-148">처리되는 개수가 일괄 처리 크기의 절반으로 감소하면 SDK에서 다른 일괄 처리를 가져와 해당 메시지의 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="18c3f-149">따라서 함수당 처리되는 최대 동시 메시지 수는 일괄 처리 크기의 1.5배입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="18c3f-150">이 제한은 **QueueTrigger** 특성이 있는 각 함수에 개별적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="18c3f-151">하나의 큐에 수신된 메시지에 대해 병렬 실행을 사용하지 않으려면 일괄 처리 크기를 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="18c3f-152">큐 또는 큐 메시지 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="18c3f-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="18c3f-153">메서드 서명에 매개 변수를 추가하여 다음 메시지 속성을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="18c3f-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="18c3f-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="18c3f-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="18c3f-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="18c3f-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="18c3f-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="18c3f-157">**string** queueTrigger(메시지 텍스트 포함)</span><span class="sxs-lookup"><span data-stu-id="18c3f-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="18c3f-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="18c3f-158">**string** id</span></span>
* <span data-ttu-id="18c3f-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="18c3f-159">**string** popReceipt</span></span>
* <span data-ttu-id="18c3f-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="18c3f-160">**int** dequeueCount</span></span>

<span data-ttu-id="18c3f-161">Azure 저장소 API에서 직접 작업하려면 **CloudStorageAccount** 매개 변수를 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="18c3f-162">다음 예제에서는 이러한 모든 메타데이터를 INFO 응용 프로그램 로그에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="18c3f-163">예제에서 logMessage와 queueTrigger에는 둘 다 큐 메시지의 내용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="18c3f-164">다음은 샘플 코드에 의해 작성된 샘플 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="18c3f-165">정상 종료</span><span class="sxs-lookup"><span data-stu-id="18c3f-165">Graceful shutdown</span></span>
<span data-ttu-id="18c3f-166">연속 WebJob에서 실행되는 함수는 WebJob이 종료될 때 운영 체제가 함수에 알릴 수 있게 해주는 **CancellationToken** 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="18c3f-167">이 알림을 통해 함수가 예기치 않게 종료되어 데이터가 일관되지 않은 상태가 되는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="18c3f-168">다음 예제에서는 함수에서 임박한 WebJob 종료를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="18c3f-169">**참고:** 대시보드에 종료된 함수의 상태와 출력이 올바르게 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="18c3f-170">자세한 내용은 [WebJobs 정상 종료](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="18c3f-171">큐 메시지를 처리하는 동안 큐 메시지를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="18c3f-172">새 큐 메시지를 만드는 함수를 작성하려면 **Queue** 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="18c3f-173">**QueueTrigger**와 마찬가지로 큐 이름을 문자열로 전달하거나, [동적으로 큐 이름을 설정](#how-to-set-configuration-options)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="18c3f-174">문자열 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-174">String queue messages</span></span>
<span data-ttu-id="18c3f-175">다음 비동기가 아닌 코드 샘플에서는 "inputqueue"라는 큐에 수신된 큐 메시지와 동일한 콘텐츠를 가진 새로운 큐 메시지를 "outputqueue"라는 큐에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="18c3f-176">비동기 함수는 이 섹션의 뒷부분에 나와 있는 것처럼 **IAsyncCollector<T>** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="18c3f-177">POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="18c3f-178">문자열 대신 POCO가 포함된 큐 메시지를 만들려면 POCO 유형을 출력 매개 변수로 **Queue** 특성 생성자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="18c3f-179">SDK에서 자동으로 개체를 JSON으로 serialize합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="18c3f-180">개체가 null인 경우에도 항상 큐 메시지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="18c3f-181">여러 메시지 만들기 또는 비동기 함수로 큐 메시지 만들기</span><span class="sxs-lookup"><span data-stu-id="18c3f-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="18c3f-182">여러 개의 메시지를 만들려면 다음 예제와 같이 출력 큐의 매개 변수 유형을 **ICollector<T>** 또는 **IAsyncCollector<T>**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="18c3f-183">**Add** 메서드를 호출하면 각 큐 메시지가 즉시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="18c3f-184">큐 특성이 작동하는 유형</span><span class="sxs-lookup"><span data-stu-id="18c3f-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="18c3f-185">다음 매개 변수 유형에서 **Queue** 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="18c3f-186">**out string** (함수가 종료될 때 매개 변수 값이 null이 아닌 경우 큐 메시지 생성)</span><span class="sxs-lookup"><span data-stu-id="18c3f-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="18c3f-187">**out byte[]**(**문자열**처럼 작동)</span><span class="sxs-lookup"><span data-stu-id="18c3f-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="18c3f-188">**out CloudQueueMessage**(**문자열**처럼 작동)</span><span class="sxs-lookup"><span data-stu-id="18c3f-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="18c3f-189">**out POCO** (직렬화 가능한 유형, 함수가 종료될 때 매개 변수가 null인 경우 null 개체가 포함된 메시지 생성)</span><span class="sxs-lookup"><span data-stu-id="18c3f-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="18c3f-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="18c3f-190">**ICollector**</span></span>
* <span data-ttu-id="18c3f-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="18c3f-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="18c3f-192">**CloudQueue** (Azure 저장소 API를 직접 사용하여 수동으로 메시지 생성)</span><span class="sxs-lookup"><span data-stu-id="18c3f-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="18c3f-193">함수 본문에 WebJobs SDK 특성 사용</span><span class="sxs-lookup"><span data-stu-id="18c3f-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="18c3f-194">**Queue**, **Blob** 또는 **Table**과 같은 WebJobs SDK 특성을 사용하기 전에 함수에서 일부 작업을 수행해야 하는 경우 **IBinder** 인터페이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="18c3f-195">다음 예제에서는 입력 큐 메시지를 사용하여 동일한 내용의 새 메시지를 출력 큐에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="18c3f-196">출력 큐 이름은 함수 본문에서 코드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="18c3f-197">**IBinder** 인터페이스를 **Table** 및 **Blob** 특성과 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="18c3f-198">큐 메시지를 처리하는 동안 Blob 및 테이블을 읽고 쓰는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="18c3f-199">**Blob** 및 **Table** 특성을 사용하여 Blob과 테이블을 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="18c3f-200">이 섹션의 샘플은 Blob에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="18c3f-201">Blob이 생성되거나 업데이트될 때 프로세스를 트리거하는 방법을 보여 주는 코드 샘플은 [WebJobs SDK를 사용하여 Azure Blob Storage로 작업하는 방법](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)을 참조하고, 테이블을 읽고 쓰는 코드 샘플은 [WebJobs SDK를 사용하여 Azure Table Storage로 작업하는 방법](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="18c3f-202">Blob 작업을 트리거하는 문자열 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="18c3f-203">문자열이 포함된 큐 메시지의 경우 **queueTrigger**는 메시지 내용이 포함된 **Blob** 특성의 **blobPath** 매개 변수에 사용할 수 있는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="18c3f-204">다음 예제에서는 **Stream** 개체를 사용하여 Blob을 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="18c3f-205">큐 메시지는 textblobs 컨테이너에 있는 Blob의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="18c3f-206">이름에 "-new"가 추가된 Blob 복사본이 동일한 컨테이너에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="18c3f-207">**Blob** 특성 생성자는 컨테이너 및 Blob 이름을 지정하는 **blobPath** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="18c3f-208">이 자리 표시자에 대한 자세한 내용은 [WebJobs SDK에서 Azure blob 저장소를 사용하는 방법](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="18c3f-209">특성이 **Stream** 개체를 데코레이팅하는 경우 또 다른 생성자 매개 변수가 **FileAccess** 모드를 읽기, 쓰기 또는 읽기/쓰기로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="18c3f-210">다음 예제에서는 **CloudBlockBlob** 개체를 사용하여 Blob을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="18c3f-211">큐 메시지는 Blob의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="18c3f-212">POCO( [Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 큐 메시지</span><span class="sxs-lookup"><span data-stu-id="18c3f-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="18c3f-213">큐 메시지에 JSON으로 저장된 POCO의 경우 **Queue** 특성의 **blobPath** 매개 변수에서 개체 속성의 이름을 지정하는 자리 표시자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="18c3f-214">큐 메타데이터 속성 이름을 자리 표시자로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="18c3f-215">[큐 또는 큐 메시지 메타데이터 가져오기](#get-queue-or-queue-message-metadata)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="18c3f-216">다음 예제에서는 Blob을 확장명이 다른 새 Blob에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="18c3f-217">큐 메시지는 **BlobName** 및 **BlobNameWithoutExtension** 속성을 포함하는 **BlobInformation** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="18c3f-218">속성 이름은 **Blob** 특성에 대한 Blob 경로에서 자리 표시자로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="18c3f-219">이 SDK는 [Newtonsoft.Json NuGet 패키지](http://www.nuget.org/packages/Newtonsoft.Json) 를 사용하여 메시지를 직렬화 및 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="18c3f-220">WebJobs SDK를 사용하지 않는 프로그램에서 큐 메시지를 만드는 경우 다음 예제와 같은 코드를 작성하여 SDK에서 구문 분석할 수 있는 POCO 큐 메시지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="18c3f-221">개체에 blob을 바인딩하기 전에 함수에서 일부 작업을 수행해야 하는 경우 [함수 본문에서 WebJobs SDK 특성 사용](#use-webjobs-sdk-attributes-in-the-body-of-a-function)에 표시된 대로 함수 본문에서 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="18c3f-222">Blob 특성을 사용할 수 있는 유형</span><span class="sxs-lookup"><span data-stu-id="18c3f-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="18c3f-223">**Blob** 특성은 다음 유형에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="18c3f-224">**Stream** (읽기 또는 쓰기, FileAccess 생성자 매개 변수를 통해 지정)</span><span class="sxs-lookup"><span data-stu-id="18c3f-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="18c3f-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="18c3f-225">**TextReader**</span></span>
* <span data-ttu-id="18c3f-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="18c3f-226">**TextWriter**</span></span>
* <span data-ttu-id="18c3f-227">**string** (읽기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-227">**string** (read)</span></span>
* <span data-ttu-id="18c3f-228">**out string** (쓰기, 함수가 반환될 때 문자열 매개 변수가 null이 아닌 경우에만 Blob 생성)</span><span class="sxs-lookup"><span data-stu-id="18c3f-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="18c3f-229">POCO(읽기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-229">POCO (read)</span></span>
* <span data-ttu-id="18c3f-230">out POCO(쓰기, 항상 Blob 생성, 함수가 반환될 때 POCO 매개 변수가 null인 경우 null 개체로 생성)</span><span class="sxs-lookup"><span data-stu-id="18c3f-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="18c3f-231">**CloudBlobStream** (쓰기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="18c3f-232">**ICloudBlob** (읽기 또는 쓰기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="18c3f-233">**CloudBlockBlob** (읽기 또는 쓰기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="18c3f-234">**CloudPageBlob** (읽기 또는 쓰기)</span><span class="sxs-lookup"><span data-stu-id="18c3f-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="18c3f-235">포이즌 메시지를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-235">How to handle poison messages</span></span>
<span data-ttu-id="18c3f-236">함수가 실패하게 만드는 내용이 포함된 메시지를 *포이즌 메시지*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="18c3f-237">함수가 실패할 경우 큐 메시지가 삭제되지 않고 결국 다시 선택되어 주기가 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="18c3f-238">SDK에서 제한된 반복 횟수 후에 자동으로 주기를 중단하거나 수동으로 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="18c3f-239">자동 포이즌 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="18c3f-239">Automatic poison message handling</span></span>
<span data-ttu-id="18c3f-240">SDK는 최대 5회까지 함수를 호출하여 큐 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="18c3f-241">다섯 번째 시도가 실패하면 메시지가 포이즌 큐로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="18c3f-242">[구성 옵션을 설정하는 방법](#how-to-set-configuration-options)에서 최대 다시 시도 횟수를 구성하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="18c3f-243">포이즌 큐의 이름은 *{originalqueuename}*-poison으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="18c3f-244">메시지를 기록하거나 수동 작업이 필요하다는 알림을 보내 포이즌 큐의 메시지를 처리하는 함수를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="18c3f-245">다음 예제에서는 큐 메시지에 존재하지 않는 Blob 이름이 포함되어 있을 경우 **CopyBlob** 함수가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="18c3f-246">이 경우 메시지가 copyblobqueue 큐에서 copyblobqueue-poison 큐로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="18c3f-247">**ProcessPoisonMessage** 에서 포이즌 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="18c3f-248">다음 그림에서는 포이즌 메시지를 처리할 때 이러한 함수의 콘솔 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![포이즌 메시지 처리에 대한 콘솔 출력](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="18c3f-250">수동 포이즌 메시지 처리</span><span class="sxs-lookup"><span data-stu-id="18c3f-250">Manual poison message handling</span></span>
<span data-ttu-id="18c3f-251">**dequeueCount**라는 **int** 매개 변수를 함수에 추가하여 메시지가 처리를 위해 선택된 횟수를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="18c3f-252">함수 코드를 통해 큐에서 제거한 횟수를 확인하고 다음 예제와 같이 횟수가 임계값을 초과할 경우 고유한 포이즌 메시지 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="18c3f-253">구성 옵션을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-253">How to set configuration options</span></span>
<span data-ttu-id="18c3f-254">**JobHostConfiguration** 유형을 사용하여 다음 구성 옵션을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="18c3f-255">코드에서 SDK 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="18c3f-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="18c3f-256">최대 큐에서 제거 횟수와 같은 **QueueTrigger** 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="18c3f-257">구성에서 큐 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="18c3f-258">코드에서 SDK 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="18c3f-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="18c3f-259">코드에서 SDK 연결 문자열을 설정하면 다음 예제와 같이 구성 파일이나 환경 변수에 고유한 연결 문자열 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="18c3f-260">QueueTrigger 설정 구성</span><span class="sxs-lookup"><span data-stu-id="18c3f-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="18c3f-261">큐 메시지 처리에 적용되는 다음 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="18c3f-262">병렬로 실행하도록 동시에 선택되는 최대 큐 메시지 수(기본값은 16).</span><span class="sxs-lookup"><span data-stu-id="18c3f-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="18c3f-263">큐 메시지가 포이즌 큐로 전송되기 전의 최대 재시도 횟수(기본값은 5).</span><span class="sxs-lookup"><span data-stu-id="18c3f-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="18c3f-264">큐가 비어 있을 때 다시 폴링하기 전의 최대 대기 시간(기본값은 1분).</span><span class="sxs-lookup"><span data-stu-id="18c3f-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="18c3f-265">다음 예제에서는 이러한 설정을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="18c3f-266">코드에서 WebJobs SDK 생성자 매개 변수 값 설정</span><span class="sxs-lookup"><span data-stu-id="18c3f-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="18c3f-267">경우에 따라 큐 이름, Blob 이름 또는 컨테이너, 테이블 이름을 하드 코드하지 않고 코드에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="18c3f-268">예를 들어 구성 파일 또는 환경 변수에서 **QueueTrigger** 에 대한 큐 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="18c3f-269">이렇게 하려면 **NameResolver** 개체를 **JobHostConfiguration** 유형에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="18c3f-270">WebJobs SDK 특성 생성자 매개 변수에 백분율(%) 기호로 묶어 특정 자리 표시자를 포함하면 **NameResolver** 코드가 해당 자리 표시자 위치에서 사용할 실제 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="18c3f-271">예를 들어 테스트 환경에 logqueuetest라는 큐를 사용하고 프로덕션에 logqueueprod라는 큐를 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="18c3f-272">하드 코드된 큐 이름 대신 실제 큐 이름을 포함하는 **appSettings** 컬렉션의 항목 이름을 지정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="18c3f-273">**appSettings** 키가 logqueue이면 함수가 다음 예제처럼 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="18c3f-274">**NameResolver** 클래스는 다음 예제와 같이 **appSettings**에서 큐 이름을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="18c3f-275">다음 예제와 같이 **NameResolver** 클래스를 **JobHost** 개체에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="18c3f-276">**참고:** 큐, 테이블 및 Blob 이름은 함수가 호출될 때마다 확인되지만 Blob 컨테이너 이름은 응용 프로그램이 시작될 때만 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="18c3f-277">작업이 실행되는 동안에는 Blob 컨테이너 이름을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="18c3f-278">수동으로 함수를 트리거하는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-278">How to trigger a function manually</span></span>
<span data-ttu-id="18c3f-279">수동으로 함수를 트리거하려면 다음 예제와 같이 **JobHost** 개체의 **Call** 또는 **CallAsync** 메서드와 함수의 **NoAutomaticTrigger** 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="18c3f-280">로그를 기록하는 방법</span><span class="sxs-lookup"><span data-stu-id="18c3f-280">How to write logs</span></span>
<span data-ttu-id="18c3f-281">대시보드의 두 곳, 즉 WebJob의 페이지 및 특정 WebJob 호출의 페이지에 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![WebJob 페이지에서 로그](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![함수 호출 페이지에서 로그](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="18c3f-284">함수 또는 **Main()** 메서드에서 호출한 콘솔 메서드의 출력은 특정 메서드 호출에 대한 페이지가 아니라 WebJob에 대한 대시보드 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="18c3f-285">메서드 서명의 매개 변수에서 가져오는 TextWriter 개체의 출력은 메서드 호출에 대한 대시보드 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="18c3f-286">많은 작업 기능이 동시에 실행될 수 있지만 콘솔은 단일 스레드이므로 콘솔 출력을 특정 메서드 호출에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="18c3f-287">따라서 SDK에서는 각 함수 호출에 고유한 로그 작성기 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="18c3f-288">[응용 프로그램 추적 로그](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)를 기록하려면 INFO로 표시되는 로그를 만드는 **Console.Out** 및 ERROR로 표시되는 로그를 만드는 **Console.Error**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="18c3f-289">그렇지 않으면 Info 및 Error 외에 Verbose, Warning 및 Critical 수준을 제공하는 [추적 또는 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="18c3f-290">응용 프로그램 추적 로그는 Azure 웹 앱을 구성한 방식에 따라 웹 앱 로그 파일, Azure 테이블 또는 Azure Blob에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="18c3f-291">모든 콘솔 출력과 마찬가지로 가장 최근 100개의 응용 프로그램 로그도 함수 호출에 대한 페이지가 아니라 WebJob에 대한 대시보드 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="18c3f-292">콘솔 출력은 프로그램이 Azure WebJob에서 실행되는 경우에만 대시보드에 표시되고, 프로그램이 로컬로 실행되거나 다른 환경에서 실행되는 경우에는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="18c3f-293">대시보드 연결 문자열을 null로 설정하면 로깅을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="18c3f-294">자세한 내용은 [구성 옵션을 설정하는 방법](#how-to-set-configuration-options)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="18c3f-295">다음 예제에서는 로그를 작성하는 여러 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="18c3f-296">WebJobs SDK 대시보드에서 **TextWriter** 개체 출력은 특정 함수 호출에 대한 페이지로 이동하여 **출력 토글**을 선택할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![호출 링크](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![함수 호출 페이지에서 로그](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="18c3f-299">WebJobs SDK 대시보드에서 콘솔 출력의 최근 100줄은 함수 호출이 아니라 WebJob에 대한 페이지로 이동하여 **Toggle Output**을 선택할 때 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Toggle Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="18c3f-301">연속 WebJob에서는 응용 프로그램 로그가 웹앱 파일 시스템의 /data/jobs/continuous/*{webjobname}*/job_log.txt에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="18c3f-302">Azure Blob에서 응용 프로그램 로그는 다음과 같습니다. 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="18c3f-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="18c3f-303">Azure 테이블에서 **Console.Out** 및 **Console.Error** 로그는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![테이블에 대한 정보 로그](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![테이블에 대한 오류 로그](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="18c3f-306">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18c3f-306">Next steps</span></span>
<span data-ttu-id="18c3f-307">이 문서에서는 Azure 큐 작업에 대한 일반적인 시나리오를 처리하는 방법을 보여 주는 코드 샘플을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="18c3f-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="18c3f-308">Azure Webjob 및 Webjob SDK를 사용하는 방법에 대한 자세한 내용은 [Azure WebJobs 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18c3f-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

