---
title: "Azure Functions Blob Storage 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure Storage 트리거 및 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="a3fc2-104">Azure Functions Blob Storage 바인딩</span><span class="sxs-lookup"><span data-stu-id="a3fc2-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a3fc2-105">이 문서에서는 Azure Functions에서 Azure Blob Storage 바인딩을 구성하고 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="a3fc2-106">Azure Functions는 Azure Blob Storage에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="a3fc2-107">모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="a3fc2-108">[Blob 전용 저장소 계정](../storage/common/storage-create-storage-account.md#blob-storage-accounts)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="a3fc2-109">Blob Storage 트리거 및 바인딩에는 범용 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="a3fc2-110">Blob Storage 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="a3fc2-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="a3fc2-111">Azure Blob Storage 트리거를 사용하면 새 Blob 또는 업데이트된 Blob이 검색되었을 때 함수 코드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="a3fc2-112">Blob 내용은 함수의 입력으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="a3fc2-113">Functions 포털에서 **통합** 탭을 사용하여 Blob Storage 트리거를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="a3fc2-114">이 포털에서는 *function.json*의 **bindings** 섹션에 다음 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="a3fc2-115">Blob 입력 및 출력 바인딩은 `blob`을 바인딩 형식으로 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="a3fc2-116">`path` 속성은 바인딩 식 및 필터 매개 변수를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="a3fc2-117">[이름 패턴](#pattern)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="a3fc2-118">`connection` 속성은 저장소 연결 문자열을 포함하는 앱 설정의 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a3fc2-119">Azure Portal에서 **통합** 탭에 있는 표준 편집기는 저장소 계정을 선택하는 경우 이 앱 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="a3fc2-120">소비 계획에서 Blob 트리거를 사용하는 경우 함수 앱이 유휴 상태가 된 후 새 Blob을 처리하는 데 최대 10분이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="a3fc2-121">함수 앱이 실행된 후에는 Blob이 즉시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="a3fc2-122">이 초기 지연을 방지하려면 다음 옵션 중 하나를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="a3fc2-123">무중단이 사용되는 App Service 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="a3fc2-124">Blob 이름을 포함하는 큐 메시지와 같은 다른 메커니즘을 사용하여 Blob 처리를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="a3fc2-125">예를 들어 [Blob 입력 바인딩을 사용하여 큐 트리거](#input-sample)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="a3fc2-126">이름 패턴</span><span class="sxs-lookup"><span data-stu-id="a3fc2-126">Name patterns</span></span>
<span data-ttu-id="a3fc2-127">`path` 속성에서 Blob 이름 패턴을 지정할 수 있으며, 이는 필터 또는 바인딩 식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="a3fc2-128">[바인딩 식 및 패턴](functions-triggers-bindings.md#binding-expressions-and-patterns)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="a3fc2-129">예를 들어 문자열 "original"로 시작하는 Blob을 필터링하려면 다음 정의를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="a3fc2-130">이 경로에는 *input* 컨테이너에 *original-Blob1.txt*라는 Blob이 있으며 함수 코드에 있는 `name` 변수의 값은 `Blob1`입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="a3fc2-131">Blob 파일 이름 및 확장명에 별도로 바인딩하려면 두 가지 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="a3fc2-132">또한 이 경로에는 *original-Blob1.txt*라는 Blob이 있으며 함수 코드에 있는 `blobname` 및 `blobextension` 변수의 값은 *original-Blob1* 및 *txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="a3fc2-133">파일 확장명에 고정된 값을 사용하여 Blob의 파일 형식을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="a3fc2-134">예를 들어 .png 파일에 대해서만 트리거하려면 다음 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="a3fc2-135">중괄호는 이름 패턴에서 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="a3fc2-136">이름에 중괄호가 있는 Blob 이름을 지정하려면 중괄호 두 개를 사용하여 중괄호를 이스케이프합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="a3fc2-137">다음 예제에는 *images* 컨테이너에 *{20140101}-soundfile.mp3*라는 Blob이 있으며 함수 코드에 있는 `name` 변수 값은 *soundfile.mp3*입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="a3fc2-138">트리거 메타데이터</span><span class="sxs-lookup"><span data-stu-id="a3fc2-138">Trigger metadata</span></span>

<span data-ttu-id="a3fc2-139">Blob 트리거는 몇 가지 메타데이터 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="a3fc2-140">이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="a3fc2-141">이러한 값은 [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet)과 동일한 의미 체계를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="a3fc2-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-142">**BlobTrigger**.</span></span> <span data-ttu-id="a3fc2-143">`string`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-143">Type `string`.</span></span> <span data-ttu-id="a3fc2-144">Blob 트리거 경로</span><span class="sxs-lookup"><span data-stu-id="a3fc2-144">The triggering blob path</span></span>
- <span data-ttu-id="a3fc2-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-145">**Uri**.</span></span> <span data-ttu-id="a3fc2-146">`System.Uri`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-146">Type `System.Uri`.</span></span> <span data-ttu-id="a3fc2-147">기본 위치에 대한 Blob의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="a3fc2-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-148">**Properties**.</span></span> <span data-ttu-id="a3fc2-149">`Microsoft.WindowsAzure.Storage.Blob.BlobProperties`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="a3fc2-150">Blob의 시스템 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-150">The blob's system properties.</span></span>
- <span data-ttu-id="a3fc2-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-151">**Metadata**.</span></span> <span data-ttu-id="a3fc2-152">`IDictionary<string,string>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="a3fc2-153">Blob에 대한 사용자 정의 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="a3fc2-154">Blob 수신 확인</span><span class="sxs-lookup"><span data-stu-id="a3fc2-154">Blob receipts</span></span>
<span data-ttu-id="a3fc2-155">Azure Functions 런타임은 동일한 새 Blob 또는 업데이트된 Blob에 대해 Blob 트리거 함수가 두 번 이상 호출되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="a3fc2-156">지정된 Blob 버전이 처리되었는지 확인하려면 *Blob 수신 확인*을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="a3fc2-157">Azure Functions는 사용자 함수 앱에서 사용하는(`AzureWebJobsStorage` 앱 설정에서 지정됨) Azure Storage 계정의 *azure-webjobs-hosts*라는 컨테이너에 Blob 수신 확인을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="a3fc2-158">Blob 수신 확인에는 다음 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="a3fc2-159">트리거된 함수("*&lt;함수 앱 이름>*.Functions.*&lt;함수 이름>*", 예: "MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="a3fc2-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="a3fc2-160">컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="a3fc2-160">The container name</span></span>
* <span data-ttu-id="a3fc2-161">Blob 유형("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a3fc2-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a3fc2-162">Blob 이름</span><span class="sxs-lookup"><span data-stu-id="a3fc2-162">The blob name</span></span>
* <span data-ttu-id="a3fc2-163">ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a3fc2-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a3fc2-164">Blob을 강제로 처리하려면 *azure-webjobs-hosts* 컨테이너에서 해당 Blob에 대한 Blob 수신 확인을 수동으로 삭제하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="a3fc2-165">포이즌 Blob 처리</span><span class="sxs-lookup"><span data-stu-id="a3fc2-165">Handling poison blobs</span></span>
<span data-ttu-id="a3fc2-166">지정된 Blob에 대한 Blob 트리거 함수가 실패한 경우 Azure Functions는 기본적으로 총 5번 해당 함수를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="a3fc2-167">5번 모두 실패한 경우 Azure Functions는 *webjobs-blobtrigger-poison*이라는 저장소 큐에 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="a3fc2-168">포이즌 Blob에 대한 큐 메시지는 다음 속성을 포함하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="a3fc2-169">FunctionId(형식에서 *&lt;함수 앱 이름>*.Functions.*&lt;함수 이름>*)</span><span class="sxs-lookup"><span data-stu-id="a3fc2-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="a3fc2-170">BlobType("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a3fc2-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a3fc2-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="a3fc2-171">ContainerName</span></span>
* <span data-ttu-id="a3fc2-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="a3fc2-172">BlobName</span></span>
* <span data-ttu-id="a3fc2-173">ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a3fc2-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="a3fc2-174">큰 컨테이너에 대한 Blob 폴링</span><span class="sxs-lookup"><span data-stu-id="a3fc2-174">Blob polling for large containers</span></span>
<span data-ttu-id="a3fc2-175">모니터링 중인 Blob 컨테이너에 10,000개 이상의 Blob이 포함된 경우 Functions 런타임은 로그 파일을 스캔하여 새롭거나 변경된 Blob을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="a3fc2-176">이 프로세스는 실시간으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-176">This process is not real time.</span></span> <span data-ttu-id="a3fc2-177">Blob을 만든 후 몇 분이 경과할 때까지 함수가 트리거되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="a3fc2-178">또한 [저장소 로그는 "최선을 다해" 생성됩니다](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="a3fc2-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="a3fc2-179">하지만 모든 이벤트가 캡처되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="a3fc2-180">경우에 따라 로그가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="a3fc2-181">더 빠르거나 안정적인 Blob 처리가 필요한 경우 Blob을 만들 때 [큐 메시지](../storage/queues/storage-dotnet-how-to-use-queues.md)를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="a3fc2-182">그런 다음 Blob 트리거 대신 [큐 트리거](functions-bindings-storage-queue.md)를 사용하여 Blob을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="a3fc2-183">Blob 트리거 및 입력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="a3fc2-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="a3fc2-184">.NET 함수에서는 `Stream paramName`과 같은 메서드 매개 변수를 사용하여 Blob 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="a3fc2-185">여기에서 `paramName`은 [트리거 구성](#trigger)에서 지정한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="a3fc2-186">Node.js 함수에서는 `context.bindings.<name>`을 사용하여 입력 Blob 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a3fc2-187">.NET에서는 아래 목록의 형식 중 하나에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="a3fc2-188">입력 바인딩으로 사용되는 경우 이러한 형식 중 일부에는 *function.json*에서 `inout` 바인딩 방향이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="a3fc2-189">이 방향은 표준 편집기에서 지원되지 않으므로 고급 편집기를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="a3fc2-190">`ICloudBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="a3fc2-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a3fc2-191">`CloudBlockBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="a3fc2-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a3fc2-192">`CloudPageBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="a3fc2-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a3fc2-193">`CloudAppendBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="a3fc2-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="a3fc2-194">텍스트 Blob이 필요한 경우 .NET `string` 형식에 바인딩할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="a3fc2-195">전체 Blob 내용이 메모리에 로드되므로 이는 Blob 크기가 작은 경우에만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="a3fc2-196">일반적으로 `Stream` 또는 `CloudBlockBlob` 형식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="a3fc2-197">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="a3fc2-197">Trigger sample</span></span>
<span data-ttu-id="a3fc2-198">Blob Storage 트리거를 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="a3fc2-199">모니터링되는 컨테이너에 추가된 각 Blob의 콘텐츠를 기록하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="a3fc2-200">C#</span><span class="sxs-lookup"><span data-stu-id="a3fc2-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="a3fc2-201">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a3fc2-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="a3fc2-202">C#의 Blob 트리거 예</span><span class="sxs-lookup"><span data-stu-id="a3fc2-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="a3fc2-203">Node.js의 트리거 예</span><span class="sxs-lookup"><span data-stu-id="a3fc2-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="a3fc2-204">Blob 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="a3fc2-204">Using a blob output binding</span></span>

<span data-ttu-id="a3fc2-205">.NET 함수에서는 함수 서명에 `out string` 매개 변수를 사용하거나, 다음 목록의 형식 중 하나를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="a3fc2-206">Node.js 함수에서 `context.bindings.<name>`을 사용하여 출력 Blob 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a3fc2-207">.NET 함수에서는 다음 형식으로 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="a3fc2-208">Blob 입력 및 출력이 있는 큐 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="a3fc2-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="a3fc2-209">[Queue Storage 트리거](functions-bindings-storage-queue.md), Blob Storage 입력 및 Blob Storage 출력을 정의하는 다음과 같은 function.json이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="a3fc2-210">`queueTrigger` 메타데이터 속성이</span><span class="sxs-lookup"><span data-stu-id="a3fc2-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="a3fc2-211">Blob 입력 및 출력 `path` 속성에 사용된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-211">in the blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="a3fc2-212">출력 Blob에 입력 Blob을 복사하는 언어별 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3fc2-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="a3fc2-213">C#</span><span class="sxs-lookup"><span data-stu-id="a3fc2-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="a3fc2-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a3fc2-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="a3fc2-215">C#의 Blob 바인딩 예</span><span class="sxs-lookup"><span data-stu-id="a3fc2-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="a3fc2-216">Node.js의 Blob 바인딩 예</span><span class="sxs-lookup"><span data-stu-id="a3fc2-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="a3fc2-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a3fc2-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

