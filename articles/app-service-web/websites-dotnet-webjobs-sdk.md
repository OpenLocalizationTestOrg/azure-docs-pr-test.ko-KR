---
title: "aaaWhat는 hello Azure WebJobs SDK"
description: "소개 toohello Azure WebJobs SDK입니다. 어떤 hello SDK는, 수행 하는 데 유용 하는 일반적인 시나리오 및 코드 샘플에 설명 합니다."
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
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a><span data-ttu-id="f2b29-104">Hello Azure WebJobs SDK는 무엇입니까</span><span class="sxs-lookup"><span data-stu-id="f2b29-104">What is hello Azure WebJobs SDK</span></span>
## <span data-ttu-id="f2b29-105"><a id="overview"></a>개요</span><span class="sxs-lookup"><span data-stu-id="f2b29-105"><a id="overview"></a>Overview</span></span>
<span data-ttu-id="f2b29-106">이 문서에서는 WebJobs SDK hello 기능 설명를 검토 하는 몇 가지 일반적인 시나리오에 유용 하 고 사용법 코드에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-106">This article explains what hello WebJobs SDK is, reviews some common scenarios it is useful for, and gives an overview of how you use it in your code.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="f2b29-107">[WebJobs](websites-webjobs-resources.md) 는 프로그램 또는 스크립트의 hello toorun 수 있는 Azure 앱 서비스의 기능 웹 응용 프로그램, API 응용 프로그램 또는 모바일 앱으로 동일한 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="f2b29-107">[WebJobs](websites-webjobs-resources.md) is a feature of Azure App Service that enables you toorun a program or script in hello same context as a web app, API app, or mobile app.</span></span> <span data-ttu-id="f2b29-108">hello의 목적은 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 코드가 예: 이미지 처리, 처리 큐, RSS 집계, 파일 유지 관리 같은 웹 작업이 수행할 수 있는 일반적인 작업에 대해 작성 되 고 전자 메일 보내기.</span><span class="sxs-lookup"><span data-stu-id="f2b29-108">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="f2b29-109">hello WebJobs SDK는 Azure 저장소 및 서비스 버스 작업을 위한, 작업을 예약 하 고 오류를 처리 및 기타 여러 가지 일반적인 시나리오에 대 한 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-109">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="f2b29-110">기능은 또한 toobe 확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-110">In addition, it's designed toobe extensible.</span></span> <span data-ttu-id="f2b29-111">hello [WebJobs SDK는 오픈 소스](https://github.com/Azure/azure-webjobs-sdk/), 있으면는 [확장에 대 한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-111">hello [WebJobs SDK is open source](https://github.com/Azure/azure-webjobs-sdk/), and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="f2b29-112">WebJobs SDK hello를 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-112">hello WebJobs SDK includes hello following components:</span></span>

* <span data-ttu-id="f2b29-113">**NuGet 패키지**.</span><span class="sxs-lookup"><span data-stu-id="f2b29-113">**NuGet packages**.</span></span> <span data-ttu-id="f2b29-114">NuGet 패키지 tooa Visual Studio 콘솔 응용 프로그램 프로젝트를 추가 하면 WebJobs SDK 특성으로 메서드를 데코레이팅하 코드에 사용 되는 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-114">NuGet packages that you add tooa Visual Studio Console Application project provide a framework that your code uses by decorating your methods with WebJobs SDK attributes.</span></span>
* <span data-ttu-id="f2b29-115">**대시보드**.</span><span class="sxs-lookup"><span data-stu-id="f2b29-115">**Dashboard**.</span></span> <span data-ttu-id="f2b29-116">Hello WebJobs SDK의 일부 Azure 앱 서비스에 포함 되 고 hello NuGet 패키지를 사용 하는 프로그램에 대 한 다양 한 모니터링 및 진단 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-116">Part of hello WebJobs SDK is included in Azure App Service and provides rich monitoring and diagnostics for programs that use hello NuGet packages.</span></span> <span data-ttu-id="f2b29-117">Toowrite 코드 toouse 이러한 모니터링 및 진단 기능 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-117">You don't have toowrite code toouse these monitoring and diagnostics features.</span></span>

## <span data-ttu-id="f2b29-118"><a id="scenarios"></a>시나리오</span><span class="sxs-lookup"><span data-stu-id="f2b29-118"><a id="scenarios"></a>Scenarios</span></span>
<span data-ttu-id="f2b29-119">Azure WebJobs SDK hello로 더 쉽게 처리할 수는 몇 가지 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-119">Here are some typical scenarios you can handle more easily with hello Azure WebJobs SDK:</span></span>

* <span data-ttu-id="f2b29-120">이미지 처리 또는 기타 CPU 집중 작업.</span><span class="sxs-lookup"><span data-stu-id="f2b29-120">Image processing or other CPU-intensive work.</span></span> <span data-ttu-id="f2b29-121">웹 사이트의 일반적인 기능에는 hello 기능 tooupload 이미지 또는 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-121">A common feature of websites is hello ability tooupload images or videos.</span></span> <span data-ttu-id="f2b29-122">종종을 업로드 하지 않으려는 toomake hello 사용자 대기를 수행 하는 동안 후 toomanipulate hello 콘텐츠가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-122">Often you want toomanipulate hello content after it's uploaded, but you don't want toomake hello user wait while you do that.</span></span>
* <span data-ttu-id="f2b29-123">큐 처리.</span><span class="sxs-lookup"><span data-stu-id="f2b29-123">Queue processing.</span></span> <span data-ttu-id="f2b29-124">백 엔드 서비스와 웹 프런트 엔드 toocommunicate에는 일반적인 방법은 toouse 큐 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-124">A common way for a web frontend toocommunicate with a backend service is toouse queues.</span></span> <span data-ttu-id="f2b29-125">Hello 웹 사이트 tooget 작업을 수행 하면 메시지 큐에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-125">When hello website needs tooget work done, it pushes a message onto a queue.</span></span> <span data-ttu-id="f2b29-126">백 엔드 서비스는 hello 큐에서 메시지를 끌어오는 및 작업 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-126">A backend service pulls messages from hello queue and does hello work.</span></span> <span data-ttu-id="f2b29-127">이미지 처리를 위해 큐를 사용할 수 있습니다: 예를 들어 hello 사용자 많은 파일을 업로드 한 후 hello 파일에에서 이름을 추가할 hello 백 엔드 처리에 의해 선택 큐 메시지 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-127">You could use queues for image processing: for example, after hello user uploads a number of files, put hello file names in a queue message toobe picked up by hello backend for processing.</span></span> <span data-ttu-id="f2b29-128">또는 큐 tooimprove 사이트 응답성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-128">Or you could use queues tooimprove site responsiveness.</span></span> <span data-ttu-id="f2b29-129">예를 들어 직접 tooa SQL 데이터베이스를 작성 하는 대신 tooa 큐 쓰기, 완료 하 고 hello 백 엔드 서비스 핸들 대기 시간이 긴 관계형 데이터베이스 작동 hello 사용자에 게 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-129">For example, instead of writing directly tooa SQL database, write tooa queue, tell hello user you're done, and let hello backend service handle high-latency relational database work.</span></span> <span data-ttu-id="f2b29-130">이미지 프로세스를 사용 하 여 처리 하는 큐의 예를 들어 참조 hello [WebJobs SDK 시작 자습서](websites-dotnet-webjobs-sdk-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-130">For an example of queue processing with image process, see hello [WebJobs SDK Get Started tutorial](websites-dotnet-webjobs-sdk-get-started.md).</span></span>
* <span data-ttu-id="f2b29-131">RSS 집계.</span><span class="sxs-lookup"><span data-stu-id="f2b29-131">RSS aggregation.</span></span> <span data-ttu-id="f2b29-132">RSS 피드 목록이 유지 하는 사이트를 사용 하는 경우에 모든 백그라운드 프로세스에서 hello 피드에서 hello 문서에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-132">If you have a site that maintains a list of RSS feeds, you could pull in all of hello articles from hello feeds in a background process.</span></span>
* <span data-ttu-id="f2b29-133">로그 파일 집계 또는 정리와 같은 파일 유지 관리.</span><span class="sxs-lookup"><span data-stu-id="f2b29-133">File maintenance, such as aggregating or cleaning up log files.</span></span>  <span data-ttu-id="f2b29-134">로그 파일이 별개의 또는 여러 개의 사이트에서 작성 되 고 있을 수 있습니다에 toocombine 변경 되는 시간 범위를 정렬 toorun 분석 작업에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-134">You might have log files being created by several sites or for separate time spans which you want toocombine in order toorun analysis jobs on them.</span></span> <span data-ttu-id="f2b29-135">또는 오래 된 로그 파일을 작업 toorun 매주 tooclean tooschedule 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-135">Or you might want tooschedule a task toorun weekly tooclean up old log files.</span></span>
* <span data-ttu-id="f2b29-136">Azure 테이블로 수신.</span><span class="sxs-lookup"><span data-stu-id="f2b29-136">Ingress into Azure Tables.</span></span> <span data-ttu-id="f2b29-137">수 저장 된 파일 및 blob 있고 tooparse 하 고 hello 데이터 테이블에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-137">You might have files stored and blobs and want tooparse them and store hello data in tables.</span></span> <span data-ttu-id="f2b29-138">수신 함수 hello 여러 행 (경우에 따라 수백만)를 쓸 수 있습니다 및 hello WebJobs SDK 가능한 tooimplement를 사용 하면이 기능 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-138">hello ingress function could be writing lots of rows (millions in some cases), and hello WebJobs SDK makes it possible tooimplement this functionality easily.</span></span> <span data-ttu-id="f2b29-139">hello SDK는 또한 hello hello 테이블에 쓰여진 행 수와 같이 진행률 표시기에 대 한 실시간 모니터링을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-139">hello SDK also provides real-time monitoring of progress indicators such as hello number of rows written in hello table.</span></span>
* <span data-ttu-id="f2b29-140">백그라운드 스레드에서 toorun와 같은 되도록 다른 장기 실행 작업 [전자 메일을 보내는](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-140">Other long-running tasks that you want toorun in a background thread, such as [sending emails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure).</span></span> 
* <span data-ttu-id="f2b29-141">Toorun 매일 밤 백업 작업을 수행 하는 등의 일정에 따라 원하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-141">Any tasks that you want toorun on a schedule, such as performing a back-up operation every night.</span></span>

<span data-ttu-id="f2b29-142">여러 이러한 시나리오에서 여러 Vm 동시에 여러 개의 WebJobs 실행에서 웹 앱 toorun tooscale를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-142">In many of these scenarios you may want tooscale a web app toorun on multiple VMs, which would run multiple WebJobs simultaneously.</span></span> <span data-ttu-id="f2b29-143">이 인해 hello에 동일 데이터를 처리 하는 일부 시나리오에서 여러 번 하지만이 문제가 되지 않습니다는 hello 기본 제공 큐, blob 및 hello WebJobs SDK의 서비스 버스 트리거를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f2b29-143">In some scenarios this could result in hello same data getting processed multiple times, but this is not a problem when you use hello built-in queue, blob, and Service Bus triggers of hello WebJobs SDK.</span></span> <span data-ttu-id="f2b29-144">hello SDK 통해 각 메시지 또는 blob에 대 한 함수를 한 번만 처리할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-144">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>

<span data-ttu-id="f2b29-145">hello WebJobs SDK을 사용 하면 쉽게 toohandle 일반적인 오류 처리 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-145">hello WebJobs SDK also makes it easy toohandle common error handling scenarios.</span></span> <span data-ttu-id="f2b29-146">설정할 수 있습니다 경고를 toosend 알림을 함수 오류가 발생 했으며 함수는 지정한 제한 시간 내에 완료 하지 않는 자동으로 취소 되도록 시간 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-146">You can set up alerts toosend notifications when a function fails, and you can set timeouts so that a function is automatically canceled if it doesn't complete within a specified time limit.</span></span>

## <span data-ttu-id="f2b29-147"><a id="code"></a> 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="f2b29-147"><a id="code"></a> Code samples</span></span>
<span data-ttu-id="f2b29-148">Azure 저장소에서 작동 하는 일반적인 작업을 처리 하기 위한 hello 코드는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-148">hello code for handling typical tasks that work with Azure Storage is simple.</span></span> <span data-ttu-id="f2b29-149">콘솔 응용 프로그램에서 `Main` 만들면 메서드는 `JobHost` hello를 조정 하는 개체 작성 toomethods를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-149">In your Console Application's `Main` method you create a `JobHost` object that coordinates hello calls toomethods you write.</span></span> <span data-ttu-id="f2b29-150">hello WebJobs SDK 프레임 워크를 알고 hello WebJobs SDK를 기반으로 메서드와 어떤 매개 변수 값 toouse toocall 때 특성에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-150">hello WebJobs SDK framework knows when toocall your methods and what parameter values toouse based on hello WebJobs SDK attributes you use in them.</span></span> <span data-ttu-id="f2b29-151">hello SDK 제공 *트리거* 호출 hello 함수 toobe 시키는 조건을 지정 하는 및 *바인더* 지정 하는 방법을 tooget 정보 내부 / 외부로 메서드 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-151">hello SDK provides *triggers* that specify what conditions cause hello function toobe called, and *binders* that specify how tooget information into and out of method parameters.</span></span>

<span data-ttu-id="f2b29-152">예를 들어 hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) 특성을 사용 하면 큐에서 메시지를 수신 하 고 hello 메시지는 자동으로 역직렬화 된 hello 메시지 형식은 바이트 배열 또는 사용자 지정 형식에 대 한 JSON 경우 때 호출 함수 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-152">For example, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribute causes a function toobe called when a message is received on a queue, and if hello message format is JSON for a byte array or a custom type, hello message is automatically deserialized.</span></span> <span data-ttu-id="f2b29-153">hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) 는 Azure 저장소 계정에 새 blob을 만들 때마다 특성 프로세스를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-153">hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribute triggers a process whenever a new blob is created in an Azure Storage account.</span></span>

<span data-ttu-id="f2b29-154">아래에는 큐를 폴링하고 수신된 각 큐 메시지에 대해 Blob를 만드는 간단한 프로그램이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-154">Here is a simple program that polls a queue and creates a blob for each queue message received:</span></span>

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

<span data-ttu-id="f2b29-155">hello `JobHost` 개체는 일련의 배경 함수에 대 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-155">hello `JobHost` object is a container for a set of background functions.</span></span> <span data-ttu-id="f2b29-156">hello `JobHost` 개체 모니터 hello 함수를 트리거하는 이벤트를 감시 하 고 트리거 이벤트가 발생할 때 hello 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-156">hello `JobHost` object monitors hello functions, watches for events that trigger them, and executes hello functions when trigger events occur.</span></span> <span data-ttu-id="f2b29-157">호출 하는 `JobHost` 메서드 tooindicate hello 컨테이너 프로세스 toorun에 연결할지 hello 현재 스레드 또는 백그라운드 스레드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-157">You call a `JobHost` method tooindicate whether you want hello container process toorun on hello current thread or a background thread.</span></span> <span data-ttu-id="f2b29-158">Hello 예에서 hello `RunAndBlock` 메서드 hello 프로세스 지속적으로 hello 현재 스레드의 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-158">In hello example, hello `RunAndBlock` method runs hello process continuously on hello current thread.</span></span>

<span data-ttu-id="f2b29-159">때문에 hello `ProcessQueueMessage` 이 예에서 메서드에 `QueueTrigger` 특성 hello 트리거 해당 함수는 hello 새 큐 메시지의 आ स ा.</span><span class="sxs-lookup"><span data-stu-id="f2b29-159">Because hello `ProcessQueueMessage` method in this example has a `QueueTrigger` attribute, hello trigger for that function is hello reception of a new queue message.</span></span> <span data-ttu-id="f2b29-160">hello `JobHost` hello 지정 된 큐 (이 샘플에서 "webjobsqueue")에 새 큐 메시지 개체를 감시 하 고 발견 되 면 호출 하 고 `ProcessQueueMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-160">hello `JobHost` object watches for new queue messages on hello specified queue ("webjobsqueue" in this sample) and when one is found, it calls `ProcessQueueMessage`.</span></span> 

<span data-ttu-id="f2b29-161">hello `QueueTrigger` 특성 바인딩합니다 hello `inputText` hello 큐 메시지의 매개 변수 toohello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-161">hello `QueueTrigger` attribute binds hello `inputText` parameter toohello value of hello queue message.</span></span> <span data-ttu-id="f2b29-162">Hello 및 `Blob` 바인딩 특성을 `TextWriter` 개체 tooa blob 이름은 "containername" 라는 컨테이너에 "blobname"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-162">And hello `Blob` attribute binds a `TextWriter` object tooa blob named "blobname" in a container named "containername".</span></span>  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

<span data-ttu-id="f2b29-163">hello 함수 hello 큐 메시지 toohello blob의 toowrite hello 이러한 매개 변수 값에 다음 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f2b29-163">hello function then uses these parameters toowrite hello value of hello queue message toohello blob:</span></span>

        writer.WriteLine(inputText);

<span data-ttu-id="f2b29-164">hello WebJobs SDK의 hello 트리거와 바인더 기능 toowrite는 hello 코드를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-164">hello trigger and binder features of hello WebJobs SDK greatly simplify hello code you have toowrite.</span></span> <span data-ttu-id="f2b29-165">hello 필요한 하위 수준 코드 tooprocess 큐, blob 또는 파일 또는 tooinitiate 예약 된 작업은 자동으로 수행 하 여 hello WebJobs SDK 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-165">hello low-level code required tooprocess queues, blobs, or files, or tooinitiate scheduled tasks, is done for you by hello WebJobs SDK framework.</span></span> <span data-ttu-id="f2b29-166">예를 들어 hello 프레임 워크는 아직 존재 하지 않는 큐를 만듭니다, 그리고 열립니다 hello 큐, 메시지를 큐에 읽기, 삭제 큐에 메시지 처리가 완료 된은 존재 하지 않는 blob 컨테이너를 만들고 아직 tooblobs, 및 기타 등등을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-166">For example, hello framework creates queues that don't exist yet, opens hello queue, reads queue messages, deletes queue messages when processing is completed, creates blob containers that don't exist yet, writes tooblobs, and so on.</span></span>

<span data-ttu-id="f2b29-167">hello 다음 코드 예제에서는 다양 한 트리거에서 하나의 WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, 및 `ErrorTrigger`합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-167">hello following code example shows a variety of triggers in one WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, and `ErrorTrigger`.</span></span> 

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
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <span data-ttu-id="f2b29-168"><a id="schedule"></a> 예약</span><span class="sxs-lookup"><span data-stu-id="f2b29-168"><a id="schedule"></a> Scheduling</span></span>
<span data-ttu-id="f2b29-169">hello `TimerTrigger` 특성은 일정에 따라 기능 tootrigger 함수 toorun hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-169">hello `TimerTrigger` attribute gives you hello ability tootrigger functions toorun on a schedule.</span></span> <span data-ttu-id="f2b29-170">WebJobs SDK를 hello를 통해 전체 Azure 또는 일정 개별 함수 사용 하 여 웹 작업으로는 WebJob을 예약할 수 `TimerTrigger`합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-170">You can schedule a WebJob as a whole through Azure or schedule individual functions of a WebJob using hello WebJobs SDK `TimerTrigger`.</span></span> <span data-ttu-id="f2b29-171">코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-171">Here's a code sample.</span></span>

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

<span data-ttu-id="f2b29-172">더 많은 샘플 코드에 대 한 참조 [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) GitHub.com에 hello webjobs sdk 확장 azure 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-172">For more sample code, see [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) in hello azure-webjobs-sdk-extensions repository on GitHub.com.</span></span>

## <a name="extensibility"></a><span data-ttu-id="f2b29-173">확장성</span><span class="sxs-lookup"><span data-stu-id="f2b29-173">Extensibility</span></span>
<span data-ttu-id="f2b29-174">Toobuilt에 제한 되지 하는 기능-hello WebJobs SDK 있습니다 toowrite 사용자 지정 트리거 및 바인더입니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-174">You're not limited toobuilt-in functionality -- hello WebJobs SDK allows you toowrite custom triggers and binders.</span></span>  <span data-ttu-id="f2b29-175">예를 들어, 캐시 이벤트 및 정기적인 일정에 대한 트리거를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-175">For example, you can write triggers for cache events and periodic schedules.</span></span> <span data-ttu-id="f2b29-176">[오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions) 포함 한 [WebJobs SDK 확장성에 대 한 자세한 지침](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) 및 샘플 코드 toohelp 드리겠습니다 자신의 트리거 및 바인더 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-176">An [open source repository](https://github.com/Azure/azure-webjobs-sdk-extensions) contains a [detailed guide on WebJobs SDK extensibility](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) and sample code toohelp get you started writing your own triggers and binders.</span></span>

## <span data-ttu-id="f2b29-177"><a id="workerrole"></a>Hello WebJobs 외부에서 WebJobs SDK를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f2b29-177"><a id="workerrole"></a>Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="f2b29-178">WebJobs SDK는 표준 콘솔 응용 프로그램 및 어느-실행할 있습니다 hello hello를 사용 하는 프로그램 toorun는 WebJob으로 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-178">A program that uses hello hello WebJobs SDK is a standard Console Application and can run anywhere -- it doesn't have toorun as a WebJob.</span></span> <span data-ttu-id="f2b29-179">프로덕션 이러한 환경 중 하나를 선호 하는 경우 클라우드 서비스 작업자 역할 또는 Windows 서비스에서 실행할 수 있습니다 및 개발 컴퓨터에서 로컬로 hello 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-179">You can test hello program locally on your development computer, and in production you can run it in a Cloud Service worker role or a Windows service if you prefer one of those environments.</span></span> 

<span data-ttu-id="f2b29-180">그러나 hello 대시보드는 Azure 앱 서비스 웹 앱에 대 한 확장으로 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-180">However, hello dashboard is only available as an extension for an Azure App Service web app.</span></span> <span data-ttu-id="f2b29-181">WebJob 외부 toorun를 원하고 여전히 hello 대시보드를 사용 하는 경우에 웹을 구성할 수 있습니다 앱 toouse hello 동일한 저장소 계정 연결 문자열을 WebJobs SDK 대시보드 참조 하 고 해당 웹 응용 프로그램의 WebJobs 대시보드 그런 다음 함수에 대 한 데이터를 표시 됩니다 다른 위치를 실행 하는 프로그램에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-181">If you want toorun outside of a WebJob and still use hello Dashboard, you can configure a web app toouse hello same storage account that your WebJobs SDK Dashboard connection string refers to, and that web app's WebJobs Dashboard will then show data about function execution from your program that is running somewhere else.</span></span> <span data-ttu-id="f2b29-182">URL https:// hello를 사용 하 여 toohello 대시보드를 얻을 수*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-182">You can get toohello Dashboard by using hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions.</span></span> <span data-ttu-id="f2b29-183">자세한 내용은 참조 [hello WebJobs SDK로 로컬 개발에 대 한 대시보드를 가져오는](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), 하지만 hello 블로그 게시물 이전 연결 문자열 이름에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-183">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that hello blog post shows an old connection string name.</span></span> 

## <span data-ttu-id="f2b29-184"><a id="nostorage"></a>대시보드 기능</span><span class="sxs-lookup"><span data-stu-id="f2b29-184"><a id="nostorage"></a>Dashboard features</span></span>
<span data-ttu-id="f2b29-185">WebJobs SDK hello WebJobs SDK 트리거 또는 바인더를 사용 하지 않는 경우에 여러 가지 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-185">hello WebJobs SDK provides several advantages even if you don't use WebJobs SDK triggers or binders:</span></span>

* <span data-ttu-id="f2b29-186">대시보드 hello에서 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-186">You can invoke functions from hello Dashboard.</span></span>
* <span data-ttu-id="f2b29-187">대시보드 hello에서 함수를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-187">You can replay functions from hello Dashboard.</span></span>
* <span data-ttu-id="f2b29-188">대시보드, 연결 된 toohello hello에 로그를 볼 수 특정 WebJob (Console.Out, Console.Error, 추적 등을 사용 하 여 작성 된 응용 프로그램 로그) 또는를 생성 toohello 특정 함수 호출 연결 (로그를 사용 하 여 기록는 `TextWriter` SDK toohello 함수를 매개 변수로 전달 하는 hello 개체).</span><span class="sxs-lookup"><span data-stu-id="f2b29-188">You can view logs in hello Dashboard, linked toohello particular WebJob (application logs, written by using Console.Out, Console.Error, Trace, etc.) or linked toohello particular function invocation that generated them (logs written by using a `TextWriter` object that hello SDK passes toohello function as a parameter).</span></span> 

<span data-ttu-id="f2b29-189">자세한 내용은 참조 [toomanually 함수를 호출 하는 방법을](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) 및 [toowrite 기록 하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span><span class="sxs-lookup"><span data-stu-id="f2b29-189">For more information, see [How toomanually invoke a function](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) and [How toowrite logs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)</span></span> 

## <span data-ttu-id="f2b29-190"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2b29-190"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f2b29-191">WebJobs SDK hello에 대 한 자세한 내용은 참조 [Azure WebJobs 리소스 권장](http://go.microsoft.com/fwlink/?linkid=390226)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-191">For more information about hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

<span data-ttu-id="f2b29-192">Hello 최신 향상 기능 toohello WebJobs SDK에 대 한 정보를 참조 hello [릴리스 정보](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2b29-192">For information about hello latest enhancements toohello WebJobs SDK, see hello [Release Notes](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).</span></span>

