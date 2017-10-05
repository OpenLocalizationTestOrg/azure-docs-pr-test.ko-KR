---
title: "Azure WebJobs SDK 정의"
description: "Azure WebJobs SDK에 대해 소개하고 SDK의 정의, SDK가 유용한 일반적인 시나리오 및 코드 샘플에 대해 설명합니다."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a><span data-ttu-id="b8b58-104">Azure WebJobs SDK 정의</span><span class="sxs-lookup"><span data-stu-id="b8b58-104">What is the Azure WebJobs SDK</span></span>
## <span data-ttu-id="b8b58-105"><a id="overview"></a>개요</span><span class="sxs-lookup"><span data-stu-id="b8b58-105"><a id="overview"></a>Overview</span></span>
<span data-ttu-id="b8b58-106">이 문서에서는 WebJobs SDK의 정의에 대해 설명하고 이 SDK가 유용한 몇 가지 일반적인 시나리오를 검토하며 코드에서 SDK를 사용하는 방법을 간략하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-106">This article explains what the WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="b8b58-107">[WebJobs](websites-webjobs-resources.md) 는 웹앱, API 앱 또는 모바일 앱과 동일한 컨텍스트에서 프로그램이나 스크립트를 실행할 수 있도록 하는 Azure 앱 서비스의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you to run a program or script in the same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="b8b58-108">[WebJobs SDK](websites-webjobs-resources.md) 의 목적은 WebJob이 이미지 처리, 큐 처리, RSS 집계, 파일 유지 관리, 전자 메일 보내기 등을 수행하는 일반적인 작업에 대해 작성하는 코드를 간소화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-108">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="b8b58-109">WebJobs SDK에는 Azure 저장소 및 서비스 버스 작업, 작업 예약 및 오류 처리, 기타 여러 일반적인 시나리오를 위한 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-109">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="b8b58-110">또한 확장 가능하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-110">In addition, it's designed to be extensible.</span></span> <span data-ttu-id="b8b58-111">[WebJobs SDK는 오픈 소스](https://github.com/Azure/azure-webjobs-sdk/)이며 [확장에 대한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-111">The [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="b8b58-112">WebJob SDK에는 다음 구성 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-112">The WebJobs SDK includes the following components:</span></span>

* <span data-ttu-id="b8b58-113">**NuGet 패키지**.</span><span class="sxs-lookup"><span data-stu-id="b8b58-113">**NuGet packages**.</span></span> <span data-ttu-id="b8b58-114">Visual Studio 콘솔 응용 프로그램 프로젝트에 추가하는 NuGet 패키지는 WebJobs SDK 특성으로 메서드를 데코레이팅하여 코드가 사용하는 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-114">NuGet packages that you add to a Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="b8b58-115">**대시보드**.</span><span class="sxs-lookup"><span data-stu-id="b8b58-115">**Dashboard**.</span></span> <span data-ttu-id="b8b58-116">WebJobs SDK의 일부분은 Azure 앱 서비스에 포함되어 있으며 NuGet 패키지를 사용하여 작성하는 프로그램에 풍부한 모니터링 및 진단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-116">Part of the WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use the NuGet packages.</span></span> <span data-ttu-id="b8b58-117">이러한 모니터링 및 진단 기능을 사용하기 위해 코드를 작성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-117">You don't have to write code to use these monitoring and diagnostics features.</span></span>

## <span data-ttu-id="b8b58-118"><a id="scenarios"></a>시나리오</span><span class="sxs-lookup"><span data-stu-id="b8b58-118"><a id="scenarios"></a>Scenarios</span></span>
<span data-ttu-id="b8b58-119">다음은 Azure WebJobs SDK로 보다 쉽게 처리할 수 있는 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-119">Here are some typical scenarios you can handle more easily with the Azure WebJobs SDK:</span></span>

* <span data-ttu-id="b8b58-120">이미지 처리 또는 기타 CPU 집중 작업.</span><span class="sxs-lookup"><span data-stu-id="b8b58-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="b8b58-121">웹 사이트의 일반적인 기능은 이미지나 비디오를 업로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-121">A common feature of websites is the ability to upload images or videos.</span></span> <span data-ttu-id="b8b58-122">업로드한 후에 콘텐츠를 조작하려는 경우도 많지만 이 작업을 수행하기 위해 사용자를 기다리게 하고 싶지는 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-122">Often you want to manipulate the content after it's uploaded, but you don't want to make the user wait while you do that.</span></span>
* <span data-ttu-id="b8b58-123">큐 처리.</span><span class="sxs-lookup"><span data-stu-id="b8b58-123">Queue processing.</span></span> <span data-ttu-id="b8b58-124">웹 프런트 엔드가 백 엔드 서비스와 통신하는 일반적인 방법은 큐를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-124">A common way for a web frontend to communicate with a backend service is to use queues.</span></span> <span data-ttu-id="b8b58-125">웹 사이트가 작업을 끝내야 할 경우 큐에 메시지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-125">When the website needs to get work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="b8b58-126">백 엔드 서비스는 큐에서 메시지를 풀한 후 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-126">A backend service pulls messages from the queue and does the work.</span></span> <span data-ttu-id="b8b58-127">이미지 처리에 큐를 사용할 수 있습니다. 예를 들어 사용자가 많은 수의 파일을 업로드하면 백 엔드에서 처리를 위해 선택할 수 있게 파일 이름을 큐 메시지에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-127">You could use queues for image processing: for example, after the user uploads a number of files, put the file names in a queue message to be picked up by the backend for processing.</span></span> <span data-ttu-id="b8b58-128">또는 큐를 사용하여 사이트 응답성을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-128">Or you could use queues to improve site responsiveness.</span></span> <span data-ttu-id="b8b58-129">예를 들어 SQL 데이터베이스에 직접 쓰는 대신, 큐에 쓰고 사용자에게 작업이 완료되었다고 알린 후에 백 엔드 서비스가 지연 시간이 긴 관계형 데이터베이스 작업을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-129">For example, instead of writing directly to a SQL database, write to a queue, tell the user you're done, and let the backend service handle high-latency relational database work.</span></span> <span data-ttu-id="b8b58-130">이미지 프로세스가 포함된 큐 처리의 예제는 [WebJobs SDK 시작 자습서](websites-dotnet-webjobs-sdk-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b58-130">For an example of queue processing with image process, see the [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="b8b58-131">RSS 집계.</span><span class="sxs-lookup"><span data-stu-id="b8b58-131">RSS aggregation.</span></span> <span data-ttu-id="b8b58-132">RSS 피드 목록을 유지 관리하는 사이트가 있는 경우 백그라운드 프로세스에서 피드의 모든 문서를 풀할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-132">If you have a site that maintains a list of RSS feeds, you could pull in all of the articles from the feeds in a background process.</span></span>
* <span data-ttu-id="b8b58-133">로그 파일 집계 또는 정리와 같은 파일 유지 관리.</span><span class="sxs-lookup"><span data-stu-id="b8b58-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="b8b58-134">분석 작업을 실행하기 위해 조합하려는 여러 사이트에서 또는 별도의 시간 범위 동안 로그 파일이 만들어지도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-134">You might have log files being created by several sites or for separate time spans which you want to combine in order to run analysis jobs on them.</span></span> <span data-ttu-id="b8b58-135">또는 오래된 로그 파일을 정리하는 작업이 매주 실행되도록 예약할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-135">Or you might want to schedule a task to run weekly to clean up old log files.</span></span>
* <span data-ttu-id="b8b58-136">Azure 테이블로 수신.</span><span class="sxs-lookup"><span data-stu-id="b8b58-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="b8b58-137">파일을 Blob에 저장한 다음 구문 분석하여 테이블에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-137">You might have files stored and blobs and want to parse them and store the data in tables.</span></span> <span data-ttu-id="b8b58-138">수신 기능은 많은 행(경우에 따라 수백만 개)을 쓸 수 있는데 WebJobs SDK를 사용하면 이 기능을 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-138">The ingress function could be writing lots of rows (millions in some cases), and the WebJobs SDK makes it possible to implement this functionality easily.</span></span> <span data-ttu-id="b8b58-139">또한 SDK는 테이블에 작성되는 행의 수와 같은 진행률 표시기의 실시간 모니터링 기능도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-139">The SDK also provides real-time monitoring of progress indicators such as the number of rows written in the table.</span></span>
* <span data-ttu-id="b8b58-140">백그라운드 스레드에서 실행할 기타 장기 실행 작업(예: [전자 메일 전송](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure))</span><span class="sxs-lookup"><span data-stu-id="b8b58-140">Other long-running tasks that you want to run in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="b8b58-141">매일 밤 백업 작업 수행과 같이 일정에 따라 실행하려는 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-141">Any tasks that you want to run on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="b8b58-142">대부분의 이러한 시나리오에서 여러 WebJob을 동시에 실행하는 다수의 VM에서 웹앱이 실행되도록 확장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-142">In many of these scenarios you may want to scale a web app to run on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="b8b58-143">일부 시나리오에서 이렇게 하면 동일한 데이터를 여러 번 처리하지만, 기본 제공 큐, blob 및 WebJobs SDK의 서비스 버스 트리거를 사용하는 경우 이는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-143">In some scenarios this could result in the same data getting processed multiple times, but this is not a problem when you use the built-in queue, blob, and Service Bus triggers of the WebJobs SDK.</span></span> <span data-ttu-id="b8b58-144">SDK는 각 메시지 또는 blob에 대해 함수를 한 번만 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-144">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="b8b58-145">WebJobs SDK는 일반적인 오류 처리 시나리오를 손쉽게 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-145">The WebJobs SDK also makes it easy to handle common error handling scenarios.</span></span> <span data-ttu-id="b8b58-146">함수가 실패하면 알림을 보내도록 경고를 설정할 수 있고, 지정된 시간 내에 함수가 완료되지 않으면 자동으로 취소되도록 시간 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-146">You can set up alerts to send notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <span data-ttu-id="b8b58-147"><a id="code"></a> 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="b8b58-147"><a id="code"></a> Code samples</span></span>
<span data-ttu-id="b8b58-148">Azure 저장소를 사용하는 일반적인 작업을 처리하기 위한 코드는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-148">The code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="b8b58-149">콘솔 응용 프로그램의 `Main` 메서드에 작성한 메서드에 대한 호출을 관장하는 `JobHost` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates the calls to methods you write.</span></span> <span data-ttu-id="b8b58-150">WebJobs SDK 프레임워크는 사용하는 WebJobs SDK 특성을 토대로 메서드를 호출할 시기와 사용할 매개 변수 값을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-150">The WebJobs SDK framework knows when to call your methods and what parameter values to use based on the WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="b8b58-151">SDK는 함수가 호출되도록 하는 조건을 지정하는 *트리거*와 메서드 매개 변수에서 정보를 입출력하는 방법을 지정하는 *바인더*를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-151">The SDK provides *triggers* that specify what conditions cause the function to be called, and *binders* that specify how to get information into and out of method parameters.</span></span>

<span data-ttu-id="b8b58-152">예를 들어 [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) 특성은 큐에 메시지가 수신되면 함수가 호출되도록 할 수 있고, 바이트 배열 또는 사용자 지정 형식에 대해 메시지 형식이 JSON이면 해당 메시지가 자동으로 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-152">For example, the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function to be called when a message is received on a queue, and if the message format is JSON for a byte array or a custom type, the message is automatically deserialized.</span></span> <span data-ttu-id="b8b58-153">[BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) 특성은 Azure 저장소 계정에서 새 Blob을 만들 때마다 프로세스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-153">The [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="b8b58-154">아래에는 큐를 폴링하고 수신된 각 큐 메시지에 대해 Blob를 만드는 간단한 프로그램이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

<span data-ttu-id="b8b58-155">`JobHost` 개체는 백그라운드 함수 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-155">The `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="b8b58-156">`JobHost` 개체는 함수를 모니터링하고, 이러한 함수를 트리거하는 이벤트를 조사하고, 트리거 이벤트가 발생할 때 함수를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-156">The `JobHost` object monitors the functions, watches for events that trigger them, and executes the functions when trigger events occur.</span></span> <span data-ttu-id="b8b58-157">`JobHost` 메서드를 호출하여 컨테이너 프로세스를 현재 스레드에서 실행할지 또는 백그라운드 스레드에서 실행할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-157">You call a `JobHost` method to indicate whether you want the container process to run on the current thread or a background thread.</span></span> <span data-ttu-id="b8b58-158">이 예에서 `RunAndBlock` 메서드는 현재 스레드에서 해당 프로세스를 계속 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-158">In the example, the `RunAndBlock` method runs the process continuously on the current thread.</span></span>

<span data-ttu-id="b8b58-159">이 예의 `ProcessQueueMessage` 메서드는 `QueueTrigger` 특성을 가지므로 새 큐 메시지가 수신되면 해당 함수가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-159">Because the `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, the trigger for that function is the reception of a new queue message.</span></span> <span data-ttu-id="b8b58-160">`JobHost` 개체는 지정된 큐에서 새 큐 메시지를 찾고(이 예에서는 "webjobsqueue") 찾은 후에는 `ProcessQueueMessage`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-160">The `JobHost` object watches for new queue messages on the specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="b8b58-161">`QueueTrigger` 특성은 `inputText` 매개 변수를 큐 메시지의 값에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-161">The `QueueTrigger` attribute binds the `inputText` parameter to the value of the queue message.</span></span> <span data-ttu-id="b8b58-162">또 `Blob` 특성은 `TextWriter` 개체를 "containername"이라는 컨테이너의 "blobname"이라는 blob에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-162">And the `Blob` attribute binds a `TextWriter` object to a blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="b8b58-163">그런 후 함수는 이러한 매개 변수를 사용하여 큐 메시지의 값을 Blob에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-163">The function then uses these parameters to write the value of the queue message to the blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="b8b58-164">WebJobs SDK의 트리거 및 바인더 기능은 작성해야 하는 코드를 획기적으로 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-164">The trigger and binder features of the WebJobs SDK greatly simplify the code you have to write.</span></span> <span data-ttu-id="b8b58-165">큐, Blob 또는 파일을 처리하거나 예약된 작업을 시작하는 데 필요한 하위 수준 코드는 WebJobs SDK 프레임워크에 의해 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-165">The low-level code required to process queues, blobs, or files, or to initiate scheduled tasks, is done for you by the WebJobs SDK framework.</span></span> <span data-ttu-id="b8b58-166">예를 들어, 프레임워크는 아직 존재하지 않는 큐를 만들고, 큐를 열고, 큐 메시지를 읽고, 처리가 완료되면 큐 메시지를 삭제하고, 아직 존재하지 않는 Blob 컨테이너를 만들고, Blob을 작성하는 등, 다양한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-166">For example, the framework creates queues that don't exist yet, opens the queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes to blobs, and so on.</span></span>

<span data-ttu-id="b8b58-167">다음 코드 예제는 하나의 WebJob 내에 다양한 트리거(`QueueTrigger`, `FileTrigger`, `WebHookTrigger`, `ErrorTrigger`)를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-167">The following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <span data-ttu-id="b8b58-168"><a id="schedule"></a> 예약</span><span class="sxs-lookup"><span data-stu-id="b8b58-168"><a id="schedule"></a> Scheduling</span></span>
<span data-ttu-id="b8b58-169">`TimerTrigger` 특성은 일정에 따라 실행할 함수를 트리거할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-169">The `TimerTrigger` attribute gives you the ability to trigger functions to run on a schedule.</span></span> <span data-ttu-id="b8b58-170">WebJobs SDK `TimerTrigger`를 사용하여 WebJob의 개별 함수를 예약하거나 Azure 전체에 WebJob을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using the WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="b8b58-171">코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-171">Here's a code sample.</span></span>

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

<span data-ttu-id="b8b58-172">샘플 코드를 더 보려면 GitHub.com의 azure-webjobs-sdk-extensions 리포지토리에서 [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b58-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in the azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="b8b58-173">확장성</span><span class="sxs-lookup"><span data-stu-id="b8b58-173">Extensibility</span></span>
<span data-ttu-id="b8b58-174">기본 제공되는 기능만 사용하도록 제한되지 않습니다. WebJobs SDK에서는 사용자 지정 트리거와 바인더를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-174">You're not limited to built-in functionality -- the WebJobs SDK allows you to write custom triggers and binders.</span></span>  <span data-ttu-id="b8b58-175">예를 들어, 캐시 이벤트 및 정기적인 일정에 대한 트리거를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="b8b58-176">[오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions)에는 [WebJobs SDK 확장성에 대한 자세한 가이드](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)와 트리거 및 바인더 작성을 시작하는데 도움이 될만한 샘플 코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code to help get you started writing your own triggers and binders.</span></span>

## <span data-ttu-id="b8b58-177"><a id="workerrole"></a>WebJobs 외부에서 WebJobs SDK 사용</span><span class="sxs-lookup"><span data-stu-id="b8b58-177"><a id="workerrole"></a>Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="b8b58-178">WebJobs SDK를 사용하는 프로그램은 표준 콘솔 응용 프로그램이며 WebJob으로 실행할 필요 없이 어디서나 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-178">A program that uses the the WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have to run as a WebJob.</span></span> <span data-ttu-id="b8b58-179">개발 컴퓨터에서는 로컬로 프로그램을 테스트하고, 프로덕션에서는 클라우드 서비스 작업자 역할 또는 Windows 서비스 중 원하는 환경에서 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-179">You can test the program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="b8b58-180">그러나 대시보드는 Azure 앱 서비스 웹 앱에 대한 확장으로만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-180">However, the dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="b8b58-181">WebJob 외부에서 실행하되 대시보드는 계속 사용하려는 경우 WebJobs SDK 대시보드 연결 문자열이 참조하는 것과 같은 저장소 계정을 사용하도록 웹 앱을 구성할 수 있습니다. 그러면 해당 웹 앱의 WebJobs 대시보드에 다른 위치에서 실행 중인 프로그램의 함수 실행에 대한 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-181">If you want to run outside of a WebJob and still use the Dashboard, you can configure a web app to use the same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="b8b58-182">URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions를 사용하여 대시보드로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-182">You can get to the Dashboard by using the URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="b8b58-183">자세한 내용은 [WebJobs SDK를 사용한 로컬 개발을 위해 대시보드 가져오기](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)를 참조하세요. 단, 이 블로그 게시물에는 이전 연결 문자열 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-183">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that the blog post shows an old connection string name.</span></span> 

## <span data-ttu-id="b8b58-184"><a id="nostorage"></a>대시보드 기능</span><span class="sxs-lookup"><span data-stu-id="b8b58-184"><a id="nostorage"></a>Dashboard features</span></span>
<span data-ttu-id="b8b58-185">WebJobs SDK는 WebJobs SDK 트리거 또는 바인더를 사용하지 않더라도 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-185">The WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="b8b58-186">대시보드에서 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-186">You can invoke functions from the Dashboard.</span></span>
* <span data-ttu-id="b8b58-187">대시보드에서 함수를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-187">You can replay functions from the Dashboard.</span></span>
* <span data-ttu-id="b8b58-188">특정 WebJob에 연결되거나(Console.Out, Console.Error, Trace 등을 사용하여 작성된 응용 프로그램 로그) 로그를 생성한 특정 함수 호출에 연결된(SDK가 매개 변수로 함수에 전달하는 `TextWriter` 개체를 사용하여 작성된 로그) 대시보드에서 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b58-188">You can view logs in the Dashboard, linked to the particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked to the particular function invocation that generated them (logs written by using a `TextWriter` object that the SDK passes to the function as a parameter).</span></span> 

<span data-ttu-id="b8b58-189">자세한 내용은 [함수를 수동으로 호출하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) 및 [로그를 작성하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b58-189">For more information, see [How to manually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How to write logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <span data-ttu-id="b8b58-190"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8b58-190"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b8b58-191">WebJobs SDK에 대한 자세한 내용은 [Azure WebJobs 권장 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b58-191">For more information about the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="b8b58-192">WebJobs SDK의 최신 개선 사항에 대한 정보는 [릴리스 정보](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b58-192">For information about the latest enhancements to the WebJobs SDK, see the [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

