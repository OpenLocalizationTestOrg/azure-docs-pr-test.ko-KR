---
title: "WebJob SDK를 사용하여 Azure Blob 저장소로 작업하는 방법"
description: "WebJobs SDK를 사용하여 Azure Blob 저장소로 작업하는 방법에 대해 알아봅니다. 새 Blob이 컨테이너에 표시된 경우 프로세스를 트리거하고 'poison blobs'을 처리합니다."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="57e07-104">WebJob SDK를 사용하여 Azure Blob 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="57e07-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="57e07-105">개요</span><span class="sxs-lookup"><span data-stu-id="57e07-105">Overview</span></span>
<span data-ttu-id="57e07-106">이 가이드에서는 Azure Blob을 만들거나 업데이트할 때 프로세스를 트리거하는 방법을 보여 주는 Azure Blob C# 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="57e07-107">코드 샘플에서는 [WebJobs SDK](websites-dotnet-webjobs-sdk.md) 버전 1.x를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="57e07-108">Blob를 만드는 방법을 보여 주는 코드 샘플은 [WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="57e07-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="57e07-109">이 가이드에서는 저장소 계정 또는 [여러 저장소 계정을](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs) 가리키는[ 연결 문자열을 사용하여 Visual Studio에서 WebJob](websites-dotnet-webjobs-sdk-get-started.md) 프로젝트를 만드는 방법을 알고 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="57e07-110"><a id="trigger"></a> Blob가 만들어지거나 업데이트될 때 함수를 트리거하는 방법</span><span class="sxs-lookup"><span data-stu-id="57e07-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="57e07-111">이 섹션에서는 `BlobTrigger` 특성을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="57e07-112">WebJobs SDK는 로그 파일을 검사하여 새 Blob 또는 변경된 Blob을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="57e07-113">이 프로세스는 실시간으로 처리되지 않으므로 Blob을 만든 후 몇 분이 경과할 때까지 함수가 트리거되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="57e07-114">또한 [저장소 로그를 만들기 위해 “최선”](https://msdn.microsoft.com/library/azure/hh343262.aspx) 을 다하고 있지만 모든 이벤트를 캡처하는 것을 보장하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="57e07-115">경우에 따라 로그가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="57e07-116">응용 프로그램에서 BLOB 트리거의 빠르고 안정성 있는 제한 사항을 사용할 수 없는 경우 BLOB을 만들 때 큐 메시지를 만들고 BLOB을 처리하는 함수의 `BlobTrigger` 특성을 사용하는 대신 [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) 특성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="57e07-117">확장명을 포함하는 Blob 이름에 대한 단일 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="57e07-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="57e07-118">다음 코드 샘플은 *입력* 컨테이너에 표시된 텍스트 Blob를 *출력* 컨테이너에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="57e07-119">특성 생성자는 컨테이너 이름과 Blob 이름의 자리 표시자를 지정하는 문자열 매개 변수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="57e07-120">이 예제에서는 *Blob1.txt*라는 Blob이 *입력* 컨테이너에 생성된 경우 함수가 *출력* 컨테이너에 *Blob1.txt*라는 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="57e07-121">다음 코드 샘플과 같이 Blob 이름 자리 표시자를 사용하여 이름 패턴을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="57e07-122">이 코드는 이름이 "original-"로 시작하는 Blob만 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="57e07-123">예를 들어 *입력* 컨테이너의 *original-Blob1.txt*가 *출력* 컨테이너의 *copy-Blob1.txt*에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="57e07-124">이름에 중괄호가 있는 Blob 이름에 대한 이름 패턴을 지정해야 하는 경우 이중 중괄호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="57e07-125">예를 들어 *images* 컨테이너에서 이름이 다음과 같은 Blob를 찾은 경우</span><span class="sxs-lookup"><span data-stu-id="57e07-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="57e07-126">패턴에 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="57e07-127">예제에서는 *이름* 자리 표시자 값은 *soundfile.mp3*입니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="57e07-128">Blob 이름과 확장명에 대한 별도의 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="57e07-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="57e07-129">다음 코드 샘플은 *입력* 컨테이너에 표시된 텍스트 Blob을 *출력* 컨테이너에 복사할 때 파일 확장명을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="57e07-130">*입력* Blob의 확장명을 기록하고 *출력* Blob의 확장명을 *.txt*로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="57e07-131"><a id="types"></a> Blob에 바인딩할 수 있는 유형</span><span class="sxs-lookup"><span data-stu-id="57e07-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="57e07-132">다음 유형에서 `BlobTrigger` 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="57e07-133">[ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="57e07-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="57e07-134">Azure 저장소 계정으로 직접 작업하려는 경우 메서드 서명에 `CloudStorageAccount` 매개 변수를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="57e07-135">예제는 [GitHub.com의 azure-webjobs-sdk 리포지토리에 있는 Blob 바인딩 코드](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57e07-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="57e07-136"><a id="string"></a> 문자열에 바인딩하여 텍스트 Blob 콘텐츠 가져오기</span><span class="sxs-lookup"><span data-stu-id="57e07-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="57e07-137">텍스트 Blob이 필요한 경우 `BlobTrigger`를 `string` 매개 변수에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="57e07-138">다음 코드 샘플은 텍스트 Blob을 `logMessage`라는 `string` 매개 변수에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="57e07-139">이 함수에서는 이 매개 변수를 사용하여 Blob의 콘텐츠를 WebJobs SDK 대시보드에 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="57e07-140"><a id="icbsb"></a> ICloudBlobStreamBinder를 사용하여 serialize된 Blob 콘텐츠 가져오기</span><span class="sxs-lookup"><span data-stu-id="57e07-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="57e07-141">다음 코드 샘플은 `ICloudBlobStreamBinder`를 구현하여 `BlobTrigger` 특성을 사용하도록 설정하는 클래스를 사용하여 Blob을 `WebImage` 유형에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="57e07-142">`WebImage` 바인딩 코드는 `ICloudBlobStreamBinder`에서 파생된 `WebImageBinder` 클래스에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="57e07-143">Blob 트리거를 위한 Blob 경로 가져오기</span><span class="sxs-lookup"><span data-stu-id="57e07-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="57e07-144">함수를 트리거한 Blob의 컨테이너 이름 및 Blob 이름을 가져오려면 함수 시그니처에 `blobTrigger` 문자열 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="57e07-145"><a id="poison"></a> 포이즌 Blob를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="57e07-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="57e07-146">`BlobTrigger` 함수가 일시적인 오류로 인해 실패한 경우 SDK는 이 함수를 다시 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="57e07-147">그러나 Blob의 콘텐츠로 인해 실패한 경우에는 Blob을 처리하려고 할 때마다 함수가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="57e07-148">기본적으로 SDK는 지정된 Blob에 대해 함수를 최대 5번 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="57e07-149">5번의 시도에 실패하면 *webjobs-blobtrigger-poison*이라는 큐에 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="57e07-150">최대 다시 시도 횟수는 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="57e07-151">동일한 [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) 설정이 포이즌 Blob 처리와 포이즌 큐 메시지 처리에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="57e07-152">포이즌 Blob에 대한 큐 메시지는 다음 속성을 포함하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="57e07-153">FunctionId(*{WebJob 이름}*.Functions.*{함수 이름}* 형식, 예: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="57e07-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="57e07-154">BlobType("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="57e07-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="57e07-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="57e07-155">ContainerName</span></span>
* <span data-ttu-id="57e07-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="57e07-156">BlobName</span></span>
* <span data-ttu-id="57e07-157">ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="57e07-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="57e07-158">다음 코드 샘플의 `CopyBlob` 함수에는 호출될 때마다 실패하게 만드는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="57e07-159">SDK에서 이 함수를 최대 재시도 횟수만큼 호출한 후에는 포이즌 Blob 큐에 메시지가 생성되고, 이 메시지가 `LogPoisonBlob` 함수에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="57e07-160">SDK는 JSON 메시지를 자동으로 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="57e07-161">다음은 `PoisonBlobMessage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="57e07-162"><a id="polling"></a> Blob 폴링 알고리즘</span><span class="sxs-lookup"><span data-stu-id="57e07-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="57e07-163">WebJobs SDK는 응용 프로그램이 시작될 때 `BlobTrigger` 특성에 지정된 모든 컨테이너를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="57e07-164">대용량 저장소 계정의 경우 이러한 검사에 약간의 시간이 걸릴 수 있으므로 새 Blob를 찾고 `BlobTrigger` 함수를 실행하기까지 조금 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="57e07-165">응용 프로그램이 시작된 후 새 Blob 또는 변경된 Blob을 검색하기 위해 SDK는 Blob 저장소 로그를 주기적으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="57e07-166">Blob 로그는 버퍼되고 약 10분마다 실제로 작성되므로 Blob가 생성되거나 업데이트된 후 해당 `BlobTrigger` 함수가 실행되기 전에 지연이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="57e07-167">`Blob` 특성을 사용하여 만드는 Blob에 대한 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="57e07-168">WebJobs SDK는 새 Blob을 만든 경우 일치하는 모든 `BlobTrigger` 함수에 새 Blob을 즉시 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="57e07-169">따라서 Blob 입력 및 출력 체인이 있는 경우 SDK는 이를 효율적으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="57e07-170">그러나 다른 방법으로 만들거나 업데이트한 Blob에 대해 Blob 처리 함수를 실행하는 데 소요되는 지연 시간을 줄이려면 `BlobTrigger`보다 `QueueTrigger`를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="57e07-171"><a id="receipts"></a> Blob 수신 확인</span><span class="sxs-lookup"><span data-stu-id="57e07-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="57e07-172">WebJobs SDK는 동일한 새 Blob 또는 업데이트된 Blob에 대해 `BlobTrigger` 함수가 두 번 이상 호출되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="57e07-173">이를 위해 *blob 수신 확인* 을 유지 관리하여 지정된 Blob 버전이 처리되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="57e07-174">Blob 수신 확인은 AzureWebJobsStorage 연결 문자열에 지정된 Azure 저장소 계정의 *azure-webjobs-hosts* 라는 컨테이너에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="57e07-175">Blob 수신 확인에는 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="57e07-176">Blob에 대해 호출된 함수("*{WebJob 이름}*.Functions.*{함수 이름}*", 예: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="57e07-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="57e07-177">컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="57e07-177">The container name</span></span>
* <span data-ttu-id="57e07-178">Blob 유형("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="57e07-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="57e07-179">Blob 이름</span><span class="sxs-lookup"><span data-stu-id="57e07-179">The blob name</span></span>
* <span data-ttu-id="57e07-180">ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="57e07-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="57e07-181">Blob를 강제로 처리하려면 *azure-webjobs-hosts* 컨테이너에서 해당 Blob에 대한 Blob 수신 확인을 수동으로 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="57e07-182"><a id="queues"></a>큐 문서에서 다루는 관련 항목</span><span class="sxs-lookup"><span data-stu-id="57e07-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="57e07-183">큐 메시지에 의해 트리거되는 Blob을 처리하는 방법 또는 Blob 처리에 특정하지 않은 WebJobs SDK 시나리오에 대한 자세한 내용은 [WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="57e07-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="57e07-184">이 문서에서 다루는 관련 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="57e07-185">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="57e07-185">Async functions</span></span>
* <span data-ttu-id="57e07-186">여러 인스턴스</span><span class="sxs-lookup"><span data-stu-id="57e07-186">Multiple instances</span></span>
* <span data-ttu-id="57e07-187">정상 종료</span><span class="sxs-lookup"><span data-stu-id="57e07-187">Graceful shutdown</span></span>
* <span data-ttu-id="57e07-188">함수 본문에 WebJobs SDK 특성 사용</span><span class="sxs-lookup"><span data-stu-id="57e07-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="57e07-189">코드에서 SDK 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="57e07-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="57e07-190">코드에서 WebJobs SDK 생성자 매개 변수 값 설정</span><span class="sxs-lookup"><span data-stu-id="57e07-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="57e07-191">포이즌 Blob 처리를 위한 `MaxDequeueCount` 구성</span><span class="sxs-lookup"><span data-stu-id="57e07-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="57e07-192">수동으로 함수 트리거</span><span class="sxs-lookup"><span data-stu-id="57e07-192">Trigger a function manually</span></span>
* <span data-ttu-id="57e07-193">로그 작성</span><span class="sxs-lookup"><span data-stu-id="57e07-193">Write logs</span></span>

## <span data-ttu-id="57e07-194"><a id="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="57e07-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="57e07-195">이 가이드에서는 Azure Blob 작업에 대한 일반적인 시나리오를 처리하는 방법을 보여 주는 코드 샘플을 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="57e07-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="57e07-196">Azure WebJob 및 WebJob SDK를 사용하는 방법에 대한 자세한 내용은 [Azure WebJob 권장 리소스](http://go.microsoft.com/fwlink/?linkid=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57e07-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

