---
title: "Azure Functions에서 .NET 클래스 라이브러리 사용 | Microsoft Docs"
description: "Azure Functions와 함께 사용할 .NET 클래스 라이브러리를 작성하는 방법을 알아봅니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 0613bb96d3afb85ff7e684246b128e4eef518d23
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a><span data-ttu-id="358b5-104">Azure Functions에서 .NET 클래스 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="358b5-104">Using .NET class libraries with Azure Functions</span></span>

<span data-ttu-id="358b5-105">Azure Functions는 스크립트 파일 외에도 하나 이상의 함수 구현으로서 클래스 라이브러리를 게시하는 것을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-105">In addition to script files, Azure Functions supports publishing a class library as the implementation for one or more functions.</span></span> <span data-ttu-id="358b5-106">[Azure Function Tools for Visual Studio 2017](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-106">We recommend that you use the [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="358b5-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="358b5-107">Prerequisites</span></span> 

<span data-ttu-id="358b5-108">이 문서에는 다음과 같은 필수 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-108">This article has the following prerequisites:</span></span>

- <span data-ttu-id="358b5-109">[Visual Studio 2017 15.3 미리 보기](https://www.visualstudio.com/vs/preview/) -</span><span class="sxs-lookup"><span data-stu-id="358b5-109">[Visual Studio 2017 15.3 Preview](https://www.visualstudio.com/vs/preview/).</span></span> <span data-ttu-id="358b5-110">**ASP.NET 및 웹 개발** 및 **Azure 개발** 워크로드를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-110">Install the workloads **ASP.NET and web development** and **Azure development**.</span></span>
- [<span data-ttu-id="358b5-111">Azure Function Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="358b5-111">Azure Function Tools for Visual Studio 2017</span></span>](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a><span data-ttu-id="358b5-112">Functions 클래스 라이브러리 프로젝트</span><span class="sxs-lookup"><span data-stu-id="358b5-112">Functions class library project</span></span>

<span data-ttu-id="358b5-113">Visual Studio에서 새 Azure Functions 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-113">From Visual Studio, create a new Azure Functions project.</span></span> <span data-ttu-id="358b5-114">새 프로젝트 템플릿은 *host.json* 및 *local.settings.json* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-114">The new project template creates the files *host.json* and *local.settings.json*.</span></span> <span data-ttu-id="358b5-115">[host.json에서 Azure Functions 런타임 설정을 사용자 지정](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-115">You can [customize Azure Functions runtime settings in host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span> 

<span data-ttu-id="358b5-116">*local.settings.json* 파일은 Azure Functions Core Tools에 대한 앱 설정, 연결 문자열 및 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-116">The file *local.settings.json* stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="358b5-117">구조에 대한 자세한 내용은 [로컬로 Azure Functions 코딩 및 테스트](functions-run-local.md#local-settings)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-117">To learn more about its structure, see [Code and test Azure functions locally](functions-run-local.md#local-settings).</span></span>

### <a name="functionname-attribute"></a><span data-ttu-id="358b5-118">FunctionName 특성</span><span class="sxs-lookup"><span data-stu-id="358b5-118">FunctionName attribute</span></span>

<span data-ttu-id="358b5-119">[`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) 특성은 메서드를 함수 진입점으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-119">The attribute [`FunctionNameAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marks a method as a function entry point.</span></span> <span data-ttu-id="358b5-120">정확히 하나의 트리거와 0개 이상의 입력 및 출력 바인딩을 포함하여 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-120">It must be used with exactly one trigger and 0 or more input and output bindings.</span></span>

### <a name="conversion-to-functionjson"></a><span data-ttu-id="358b5-121">Function.json으로 변환</span><span class="sxs-lookup"><span data-stu-id="358b5-121">Conversion to function.json</span></span>

<span data-ttu-id="358b5-122">Azure Functions 프로젝트를 빌드하면 `[FunctionName]`에 정의된 함수 이름과 일치하는 디렉터리에 `function.json` 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-122">When an Azure Functions project is built, it produces a file `function.json` in the directory matching the function name defined by `[FunctionName]`.</span></span> <span data-ttu-id="358b5-123">트리거 및 바인딩을 지정하고 프로젝트 어셈블리 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-123">It specifies triggers and bindings and points to the project assembly file.</span></span>

<span data-ttu-id="358b5-124">이 변환은 [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions) NuGet 패키지에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-124">This conversion is performed by the NuGet package [Microsoft\.NET\.Sdk\.Functions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).</span></span> <span data-ttu-id="358b5-125">원본은 [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk) GitHub 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-125">The source is available in the GitHub repo [azure\-functions\-vs\-build\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).</span></span>

## <a name="triggers-and-bindings"></a><span data-ttu-id="358b5-126">트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="358b5-126">Triggers and bindings</span></span>

<span data-ttu-id="358b5-127">다음 표에서는 Azure Functions 클래스 라이브러리 프로젝트에서 사용할 수 있는 트리거와 바인딩을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-127">The following table lists the triggers and bindings that are available in an Azure Functions class library project.</span></span> <span data-ttu-id="358b5-128">모든 특성은 `Microsoft.Azure.WebJobs` 네임스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-128">All attributes are in the namespace `Microsoft.Azure.WebJobs`.</span></span>

| <span data-ttu-id="358b5-129">바인딩</span><span class="sxs-lookup"><span data-stu-id="358b5-129">Binding</span></span> | <span data-ttu-id="358b5-130">특성</span><span class="sxs-lookup"><span data-stu-id="358b5-130">Attribute</span></span> | <span data-ttu-id="358b5-131">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="358b5-131">NuGet package</span></span> |
|------   | ------    | ------        |
| [<span data-ttu-id="358b5-132">Blob 저장소 트리거, 입력, 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-132">Blob storage trigger, input, output</span></span>](#blob-storage) | <span data-ttu-id="358b5-133">[BlobAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-133">[BlobAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="358b5-134">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="358b5-134">[Microsoft.Azure.WebJobs]</span></span> | <span data-ttu-id="358b5-135">[Blob 저장소]</span><span class="sxs-lookup"><span data-stu-id="358b5-135">[Blob storage]</span></span> |
| [<span data-ttu-id="358b5-136">Cosmos DB 입력 및 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="358b5-136">Cosmos DB input and output binding</span></span>](#cosmos-db) | <span data-ttu-id="358b5-137">[DocumentDBAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-137">[DocumentDBAttribute]</span></span> | <span data-ttu-id="358b5-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span><span class="sxs-lookup"><span data-stu-id="358b5-138">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]</span></span> | 
| [<span data-ttu-id="358b5-139">Event Hubs 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-139">Event Hubs trigger and output</span></span>](#event-hub) | <span data-ttu-id="358b5-140">[EventHubTriggerAttribute], [EventHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-140">[EventHubTriggerAttribute], [EventHubAttribute]</span></span> | <span data-ttu-id="358b5-141">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="358b5-141">[Microsoft.Azure.WebJobs.ServiceBus]</span></span> |
| [<span data-ttu-id="358b5-142">외부 파일 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-142">External file input and output</span></span>](#api-hub) | <span data-ttu-id="358b5-143">[ApiHubFileAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-143">[ApiHubFileAttribute]</span></span> | <span data-ttu-id="358b5-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span><span class="sxs-lookup"><span data-stu-id="358b5-144">[Microsoft.Azure.WebJobs.Extensions.ApiHub]</span></span> |
| [<span data-ttu-id="358b5-145">HTTP 및 웹후크 트리거</span><span class="sxs-lookup"><span data-stu-id="358b5-145">HTTP and webhook trigger</span></span>](#http) | <span data-ttu-id="358b5-146">[HttpTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-146">[HttpTriggerAttribute]</span></span> | <span data-ttu-id="358b5-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span><span class="sxs-lookup"><span data-stu-id="358b5-147">[Microsoft.Azure.WebJobs.Extensions.Http]</span></span> |
| [<span data-ttu-id="358b5-148">Mobile Apps 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-148">Mobile Apps input and output</span></span>](#mobile-apps) | <span data-ttu-id="358b5-149">[MobileTableAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-149">[MobileTableAttribute]</span></span> | <span data-ttu-id="358b5-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span><span class="sxs-lookup"><span data-stu-id="358b5-150">[Microsoft.Azure.WebJobs.Extensions.MobileApps]</span></span> | 
| [<span data-ttu-id="358b5-151">Notification Hubs 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-151">Notification Hubs output</span></span>](#nh) | <span data-ttu-id="358b5-152">[NotificationHubAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-152">[NotificationHubAttribute]</span></span> | <span data-ttu-id="358b5-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span><span class="sxs-lookup"><span data-stu-id="358b5-153">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]</span></span> | 
| [<span data-ttu-id="358b5-154">큐 저장소 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-154">Queue storage trigger and output</span></span>](#queue) | <span data-ttu-id="358b5-155">[QueueAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-155">[QueueAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="358b5-156">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="358b5-156">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="358b5-157">SendGrid 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-157">SendGrid output</span></span>](#sendgrid) | <span data-ttu-id="358b5-158">[SendGridAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-158">[SendGridAttribute]</span></span> | <span data-ttu-id="358b5-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span><span class="sxs-lookup"><span data-stu-id="358b5-159">[Microsoft.Azure.WebJobs.Extensions.SendGrid]</span></span> | 
| [<span data-ttu-id="358b5-160">Service Bus 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-160">Service Bus trigger and output</span></span>](#service-bus) | <span data-ttu-id="358b5-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-161">[ServiceBusAttribute], [ServiceBusAccountAttribute]</span></span> | <span data-ttu-id="358b5-162">[Microsoft.Azure.WebJobs.ServiceBus]</span><span class="sxs-lookup"><span data-stu-id="358b5-162">[Microsoft.Azure.WebJobs.ServiceBus]</span></span>
| [<span data-ttu-id="358b5-163">테이블 저장소 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-163">Table storage input and output</span></span>](#table) | <span data-ttu-id="358b5-164">[TableAttribute], [StorageAccountAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-164">[TableAttribute], [StorageAccountAttribute]</span></span> | <span data-ttu-id="358b5-165">[Microsoft.Azure.WebJobs]</span><span class="sxs-lookup"><span data-stu-id="358b5-165">[Microsoft.Azure.WebJobs]</span></span> | 
| [<span data-ttu-id="358b5-166">타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="358b5-166">Timer trigger</span></span>](#timer) | <span data-ttu-id="358b5-167">[TimerTriggerAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-167">[TimerTriggerAttribute]</span></span> | <span data-ttu-id="358b5-168">[Microsoft.Azure.WebJobs.Extensions]</span><span class="sxs-lookup"><span data-stu-id="358b5-168">[Microsoft.Azure.WebJobs.Extensions]</span></span> | 
| [<span data-ttu-id="358b5-169">Twilio 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-169">Twilio output</span></span>](#twilio) | <span data-ttu-id="358b5-170">[TwilioSmsAttribute]</span><span class="sxs-lookup"><span data-stu-id="358b5-170">[TwilioSmsAttribute]</span></span> | <span data-ttu-id="358b5-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span><span class="sxs-lookup"><span data-stu-id="358b5-171">[Microsoft.Azure.WebJobs.Extensions.Twilio]</span></span> | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a><span data-ttu-id="358b5-172">Blob 저장소 트리거, 입력 및 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="358b5-172">Blob storage trigger, input, and output bindings</span></span>

<span data-ttu-id="358b5-173">Azure Functions는 Azure Blob Storage에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-173">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="358b5-174">식 및 메타데이터 바인딩에 대한 자세한 내용은 [Azure Functions Blob Storage 바인딩](functions-bindings-storage-blob.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-174">For more information on binding expressions and metadata, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>

<span data-ttu-id="358b5-175">Blob 트리거는 `[BlobTrigger]` 특성으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-175">A blob trigger is defined with the `[BlobTrigger]` attribute.</span></span> <span data-ttu-id="358b5-176">`[StorageAccount]` 특성을 사용하여 전체 함수 또는 클래스에서 사용되는 저장소 계정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-176">You can use the attribute `[StorageAccount]` to define the storage account that is used by an entire function or class.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

<span data-ttu-id="358b5-177">Blob 입력 및 출력은 읽기 또는 쓰기를 나타내는 `FileAccess` 매개 변수와 함께 `[Blob]` 특성을 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-177">Blob input and output are defined using the `[Blob]` attribute, along with a `FileAccess` parameter indicating read or write.</span></span> <span data-ttu-id="358b5-178">다음 예제에서는 Blob 트리거와 Blob 출력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-178">The following example uses a blob trigger and blob output binding.</span></span>

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a><span data-ttu-id="358b5-179">Cosmos DB 입력 및 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="358b5-179">Cosmos DB input and output bindings</span></span>

<span data-ttu-id="358b5-180">Azure Functions는 Cosmos DB에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-180">Azure Functions supports input and output bindings for Cosmos DB.</span></span> <span data-ttu-id="358b5-181">Cosmos DB 바인딩의 기능에 대한 자세한 내용은 [Azure Functions Cosmos DB 바인딩](functions-bindings-documentdb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-181">To learn more about the features of the Cosmos DB binding, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>

<span data-ttu-id="358b5-182">Cosmos DB 문서에 바인딩하려면 [Microsoft.Azure.WebJobs.Extensions.DocumentDB] NuGet 패키지에서 `[DocumentDB]` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-182">To bind to a Cosmos DB document, use the attribute `[DocumentDB]` in the NuGet package [Microsoft.Azure.WebJobs.Extensions.DocumentDB].</span></span> <span data-ttu-id="358b5-183">다음 예제에는 큐 트리거와 DocumentDB API 출력 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-183">The following example has a queue trigger and a DocumentDB API output binding:</span></span>

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a><span data-ttu-id="358b5-184">Event Hubs 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-184">Event Hubs trigger and output</span></span>

<span data-ttu-id="358b5-185">Azure Functions는 이벤트 허브에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-185">Azure Functions supports trigger and output bindings for Event Hubs.</span></span> <span data-ttu-id="358b5-186">자세한 내용은 [Azure Functions Event Hub 바인딩](functions-bindings-event-hubs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-186">For more information, see  [Azure Functions Event Hub bindings](functions-bindings-event-hubs.md).</span></span>

<span data-ttu-id="358b5-187">`[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` 및 `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]`형식은 [Microsoft.Azure.WebJobs.ServiceBus] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-187">The types `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` and `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="358b5-188">다음 예제에서는 Event Hub 트리거를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-188">The following example uses an Event Hub trigger:</span></span>

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="358b5-189">다음 예제에는 메서드 반환 값을 출력으로 사용하는 Event Hub 출력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-189">The following example has an Event Hub output, using the method return value as the output:</span></span>

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a><span data-ttu-id="358b5-190">외부 파일 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-190">External file input and output</span></span>

<span data-ttu-id="358b5-191">Azure Functions는 외부 파일(예: Google Drive, Dropbox 및 OneDrive)에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-191">Azure Functions supports trigger, input, and output bindings for external files, such as Google Drive, Dropbox, and OneDrive.</span></span> <span data-ttu-id="358b5-192">자세한 내용은 [Azure Functions 외부 파일 바인딩](functions-bindings-external-file.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-192">To learn more, see [Azure Functions External File bindings](functions-bindings-external-file.md).</span></span> <span data-ttu-id="358b5-193">`[ExternalFileTrigger]` 및 `[ExternalFile]` 특성은 [Microsoft.Azure.WebJobs.Extensions.ApiHub] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-193">The attributes `[ExternalFileTrigger]` and `[ExternalFile]` are defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.ApiHub].</span></span>

<span data-ttu-id="358b5-194">다음 C# 예제에서는 외부 파일 입력 및 출력 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-194">The following C# example demonstrates an external file input and output binding.</span></span> <span data-ttu-id="358b5-195">이 코드는 입력 파일을 출력 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-195">The code copies the input file to the output file.</span></span>

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a><span data-ttu-id="358b5-196">HTTP 및 웹후크</span><span class="sxs-lookup"><span data-stu-id="358b5-196">HTTP and webhooks</span></span>

<span data-ttu-id="358b5-197">`HttpTrigger` 특성을 사용하여 HTTP 트리거 또는 웹후크를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-197">Use the `HttpTrigger` attribute to define an HTTP trigger or webhook.</span></span> <span data-ttu-id="358b5-198">이 특성은 [Microsoft.Azure.WebJobs.Extensions.Http] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-198">This attribute is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.Http].</span></span> <span data-ttu-id="358b5-199">권한 부여 수준, 웹후크 유형, 경로 및 메서드를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-199">You can customize the authorization level, webhook type, route, and methods.</span></span> <span data-ttu-id="358b5-200">다음 예제에서는 익명 인증 및 _genericJson_ 웹후크 유형으로 HTTP 트리거를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-200">The following example defines an HTTP trigger with anonymous authentication and _genericJson_ webhook type.</span></span>

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a><span data-ttu-id="358b5-201">Mobile Apps 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-201">Mobile Apps input and output</span></span>

<span data-ttu-id="358b5-202">Azure Functions는 Mobile Apps에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-202">Azure Functions supports input and output bindings for Mobile Apps.</span></span> <span data-ttu-id="358b5-203">자세한 내용은 [Azure Functions Mobile Apps 바인딩 ](functions-bindings-mobile-apps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-203">To learn more, see [Azure Functions Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span> <span data-ttu-id="358b5-204">`[MobileTable]` 특성은 [Microsoft.Azure.WebJobs.Extensions.MobileApps]NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-204">The attribute `[MobileTable]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.MobileApps].</span></span>

<span data-ttu-id="358b5-205">다음 예제에서는 Mobile Apps 출력 바인딩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-205">The following example demonstrates a Mobile Apps output binding:</span></span>

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a><span data-ttu-id="358b5-206">Notification Hubs 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-206">Notification Hubs output</span></span>

<span data-ttu-id="358b5-207">Azure Functions는 Notification Hubs에 대한 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-207">Azure Functions supports an output binding for Notification Hubs.</span></span> <span data-ttu-id="358b5-208">자세한 내용은 [Azure Functions Notification Hub 출력 바인딩](functions-bindings-notification-hubs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-208">To learn more, see [Azure Functions Notification Hub output binding](functions-bindings-notification-hubs.md).</span></span> <span data-ttu-id="358b5-209">`[NotificationHub]` 특성은 [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-209">The attribute `[NotificationHub]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].</span></span>

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a><span data-ttu-id="358b5-210">큐 저장소 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-210">Queue storage trigger and output</span></span>

<span data-ttu-id="358b5-211">Azure Functions는 Azure 큐에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-211">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="358b5-212">자세한 내용은 [Azure Functions Queue Storage 바인딩](functions-bindings-storage-queue.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-212">For more information, see [Azure Functions Queue Storage bindings](functions-bindings-storage-queue.md).</span></span>

<span data-ttu-id="358b5-213">다음 예제에서는 `[Queue]` 특성을 사용하여 큐 출력 바인딩이 포함된 함수 반환 형식을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-213">The following example shows how to use the function return type with a queue output binding, using the `[Queue]` attribute.</span></span> <span data-ttu-id="358b5-214">큐 트리거를 정의하려면 `[QueueTrigger]` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-214">To define a queue trigger, use the `[QueueTrigger]` attribute.</span></span>

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a><span data-ttu-id="358b5-215">SendGrid 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-215">SendGrid output</span></span>

<span data-ttu-id="358b5-216">Azure Functions는 프로그래밍 방식으로 전자 메일을 보내기 위한 SendGrid 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-216">Azure Functions supports a SendGrid output binding for sending email programmatically.</span></span> <span data-ttu-id="358b5-217">자세한 내용은 [Azure Functions SendGrid 바인딩](functions-bindings-sendgrid.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-217">To learn more, see [Azure Functions SendGrid bindings](functions-bindings-sendgrid.md).</span></span>

<span data-ttu-id="358b5-218">`[SendGrid]` 특성은 [Microsoft.Azure.WebJobs.Extensions.SendGrid] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-218">The attribute `[SendGrid]` is defined in the NuGet package [Microsoft.Azure.WebJobs.Extensions.SendGrid].</span></span>

<span data-ttu-id="358b5-219">다음은 `SendGridMessage`를 사용하여 Service Bus 큐 트리거 및 SendGrid 출력 바인딩을 사용하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-219">The following is an example of using a Service Bus queue trigger and a SendGrid output binding using `SendGridMessage`:</span></span>

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string To { get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a><span data-ttu-id="358b5-220">Service Bus 트리거 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-220">Service Bus trigger and output</span></span>

<span data-ttu-id="358b5-221">Azure Functions는 Service Bus 큐 및 토픽에 대한 트리거 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-221">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span> <span data-ttu-id="358b5-222">바인딩 구성에 대한 자세한 내용은 [Azure Functions Service Bus 바인딩](functions-bindings-service-bus.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-222">For more information on configuring bindings, see [Azure Functions Service Bus bindings](functions-bindings-service-bus.md).</span></span>

<span data-ttu-id="358b5-223">`[ServiceBusTrigger]` 및 `[ServiceBus]` 특성은 [Microsoft.Azure.WebJobs.ServiceBus] NuGet 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-223">The attributes `[ServiceBusTrigger]` and `[ServiceBus]` are defined in the NuGet package [Microsoft.Azure.WebJobs.ServiceBus].</span></span> 

<span data-ttu-id="358b5-224">다음은 Service Bus 큐 트리거의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-224">The following is an example of a Service Bus queue trigger:</span></span>

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<span data-ttu-id="358b5-225">다음은 메서드 반환 형식을 출력으로 사용하는 Service Bus 출력 바인딩의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-225">The following is an example of a Service Bus output binding, using the method return type as the output:</span></span>

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a><span data-ttu-id="358b5-226">테이블 저장소 입력 및 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-226">Table storage input and output</span></span>

<span data-ttu-id="358b5-227">Azure Functions는 Azure Table 저장소에 대한 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-227">Azure Functions supports input and output bindings for Azure Table storage.</span></span> <span data-ttu-id="358b5-228">자세한 내용은 [Azure Functions 테이블 저장소 바인딩 ](functions-bindings-storage-table.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-228">To learn more, see [Azure Functions Table storage bindings](functions-bindings-storage-table.md).</span></span>

<span data-ttu-id="358b5-229">다음 예제에서는 테이블 저장소 출력 및 입력 바인딩을 보여 주는 두 개의 함수가 포함된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-229">The following example is a class with two functions, demonstrating table storage output and input bindings.</span></span> 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use the metadata parameter "queueTrigger" to bind the queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a><span data-ttu-id="358b5-230">타이머 트리거</span><span class="sxs-lookup"><span data-stu-id="358b5-230">Timer trigger</span></span>

<span data-ttu-id="358b5-231">Azure Functions에는 정의된 일정에 따라 함수 코드를 실행할 수 있는 타이머 트리거 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-231">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> <span data-ttu-id="358b5-232">바인딩 기능에 대한 자세한 내용은 [Azure Functions를 사용하여 코드 실행 예약](functions-bindings-timer.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-232">To learn more about the features of the binding, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>

<span data-ttu-id="358b5-233">사용 계획에서 [CRON 식](http://en.wikipedia.org/wiki/Cron#CRON_expression)을 사용하여 일정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-233">On the Consumption plan, you can define schedules with a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression).</span></span> <span data-ttu-id="358b5-234">App Service 계획을 사용하는 경우 TimeSpan 문자열을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-234">If you're using an App Service Plan, you can also use a TimeSpan string.</span></span> 

<span data-ttu-id="358b5-235">다음 예제에서는 5분마다 실행되는 타이머 트리거를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-235">The following example defines a timer trigger that runs every 5 minutes:</span></span>

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a><span data-ttu-id="358b5-236">Twilio 출력</span><span class="sxs-lookup"><span data-stu-id="358b5-236">Twilio output</span></span>

<span data-ttu-id="358b5-237">Azure Functions는 함수에서 SMS 문자 메시지를 보낼 수 있도록 Twilio 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-237">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages.</span></span> <span data-ttu-id="358b5-238">자세한 내용은 [Twilio 출력 바인딩을 사용하여 Azure Functions에서 SMS 메시지 전송](functions-bindings-twilio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-238">To learn more, see [Send SMS messages from Azure Functions using the Twilio output binding](functions-bindings-twilio.md).</span></span> 

<span data-ttu-id="358b5-239">`[TwilioSms]` 특성은 [Microsoft.Azure.WebJobs.Extensions.Twilio] 패키지에 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-239">The attribute `[TwilioSms]` is defined in the package [Microsoft.Azure.WebJobs.Extensions.Twilio].</span></span>

<span data-ttu-id="358b5-240">다음 C# 예제에서는 큐 트리거와 Twilio 출력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="358b5-240">The following C# example uses a queue trigger and a Twilio output binding:</span></span>

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        To = order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a><span data-ttu-id="358b5-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="358b5-241">Next steps</span></span>

<span data-ttu-id="358b5-242">C# 스크립팅에서 Azure Functions 사용에 대한 자세한 내용은 [Azure Functions C\# 스크립트 개발자 참조](functions-reference-csharp.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="358b5-242">For more information on using Azure Functions in C# scripting, see [Azure Functions C\# script developer reference](functions-reference-csharp.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
<span data-ttu-id="358b5-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-243">[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1</span></span>
<span data-ttu-id="358b5-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-244">[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1</span></span>
<span data-ttu-id="358b5-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-245">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="358b5-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-246">[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1</span></span>
<span data-ttu-id="358b5-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-247">[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1</span></span>
<span data-ttu-id="358b5-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-248">[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1</span></span>
<span data-ttu-id="358b5-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-249">[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1</span></span>
<span data-ttu-id="358b5-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-250">[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1</span></span>
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
<span data-ttu-id="358b5-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span><span class="sxs-lookup"><span data-stu-id="358b5-251">[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4</span></span>
<span data-ttu-id="358b5-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-252">[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1</span></span>
<span data-ttu-id="358b5-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span><span class="sxs-lookup"><span data-stu-id="358b5-253">[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1</span></span>


<!-- Links to source --> 
<span data-ttu-id="358b5-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-254">[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs</span></span>
<span data-ttu-id="358b5-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-255">[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs</span></span>
<span data-ttu-id="358b5-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-256">[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs</span></span>
<span data-ttu-id="358b5-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-257">[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs</span></span>
<span data-ttu-id="358b5-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span><span class="sxs-lookup"><span data-stu-id="358b5-258">[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs </span></span>
<span data-ttu-id="358b5-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-259">[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs</span></span>
<span data-ttu-id="358b5-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-260">[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs</span></span>
<span data-ttu-id="358b5-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-261">[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs</span></span>
<span data-ttu-id="358b5-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-262">[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs</span></span>
<span data-ttu-id="358b5-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-263">[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs</span></span>
<span data-ttu-id="358b5-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-264">[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs</span></span>
<span data-ttu-id="358b5-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-265">[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs</span></span>
<span data-ttu-id="358b5-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-266">[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs</span></span>
<span data-ttu-id="358b5-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-267">[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs</span></span>
<span data-ttu-id="358b5-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-268">[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs</span></span>
<span data-ttu-id="358b5-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span><span class="sxs-lookup"><span data-stu-id="358b5-269">[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs</span></span>
