---
title: "aaaAzure 함수 Blob 저장소 바인딩 | Microsoft Docs"
description: "Toouse Azure 저장소의 트리거 방법 및 Azure 함수에서 바인딩 이해 합니다."
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
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="ffd45-104">Azure Functions Blob Storage 바인딩</span><span class="sxs-lookup"><span data-stu-id="ffd45-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ffd45-105">이 문서에서는 설명 어떻게 tooconfigure 정보와 Azure 함수에서 Azure Blob 저장소 바인딩을 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="ffd45-106">Azure Functions는 Azure Blob Storage에 대한 트리거, 입력 및 출력 바인딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ffd45-107">모든 바인딩에서 사용할 수 있는 기능은 [Azure Functions 트리거 및 바인딩 개념](functions-triggers-bindings.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd45-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="ffd45-108">[Blob 전용 저장소 계정](../storage/common/storage-create-storage-account.md#blob-storage-accounts)은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="ffd45-109">Blob Storage 트리거 및 바인딩에는 범용 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="ffd45-110">Blob Storage 트리거 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="ffd45-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="ffd45-111">함수 코드는 hello Azure Blob 저장소 트리거를 사용 하 여 신규 또는 업데이트 된 blob 검색 되 면 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="ffd45-112">입력된 toohello 함수 hello blob 콘텐츠가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="ffd45-113">Hello를 사용 하 여 blob 저장소 트리거를 정의한 다음 **통합** hello 함수 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="ffd45-114">hello 포털에서는 다음 hello에 정의 된 hello **바인딩** 섹션 *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ffd45-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="ffd45-115">Blob 입력 및 출력 바인딩을 사용 하 여 정의 `blob` hello 바인딩 형식으로:</span><span class="sxs-lookup"><span data-stu-id="ffd45-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="ffd45-116">hello `path` 바인딩 식 및 필터 매개 변수 속성은 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="ffd45-117">[이름 패턴](#pattern)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd45-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="ffd45-118">hello `connection` 저장소 연결 문자열을 포함 하는 응용 프로그램 설정의 hello 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ffd45-119">Hello Azure 포털에서에서 hello의 표준 편집기 hello **통합** 탭 저장소 계정을 선택할 때 응용 프로그램 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="ffd45-120">Blob 트리거 소비 계획을 사용 하는 경우에 있을 수 있습니다 켜기 tooa 10 분 지연 함수 앱이 유휴 내려갔습니다 후 새 blob을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="ffd45-121">Hello 함수 응용 프로그램을 실행 한 후 blob 즉시 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="ffd45-122">이 초기 tooavoid 지연 hello 다음 옵션 중 하나를 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffd45-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="ffd45-123">무중단이 사용되는 App Service 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="ffd45-124">예: hello blob 이름을 포함 하는 큐 메시지 처리, 다른 메커니즘 tootrigger hello blob을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="ffd45-125">예를 들어 [Blob 입력 바인딩을 사용하여 큐 트리거](#input-sample)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd45-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="ffd45-126">이름 패턴</span><span class="sxs-lookup"><span data-stu-id="ffd45-126">Name patterns</span></span>
<span data-ttu-id="ffd45-127">Hello에 blob 이름 패턴을 지정할 수 있습니다 `path` 속성 필터 또는 바인딩 식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="ffd45-128">[바인딩 식 및 패턴](functions-triggers-bindings.md#binding-expressions-and-patterns)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffd45-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="ffd45-129">예를 들어 toofilter tooblobs hello 문자열 "원래"로 시작 하는 정의 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="ffd45-130">이 경로 라는 blob를 찾습니다 *원래 Blob1.txt* hello에 *입력* 컨테이너 및 hello hello 값 `name` 함수 코드에서 변수는 `Blob1`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="ffd45-131">toobind toohello blob 파일 이름과 확장명을 별도로 두 개의 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="ffd45-132">이 경로 또한 라는 blob 찾습니다 *원래 Blob1.txt*, 및의 hello hello 값 `blobname` 및 `blobextension` 함수 코드에서 변수는 *원래 Blob1* 및 *txt*.</span><span class="sxs-lookup"><span data-stu-id="ffd45-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="ffd45-133">Hello 파일 확장명에 대 한 고정된 값을 사용 하 여 hello 파일 유형의 blob 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="ffd45-134">예를 들어, tootrigger.png 파일에 대해서만 사용 하 여 hello 패턴:</span><span class="sxs-lookup"><span data-stu-id="ffd45-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="ffd45-135">중괄호는 이름 패턴에서 특수 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="ffd45-136">중괄호 hello 이름에 포함 된 toospecify blob 이름은 중괄호 2 개를 사용 하 여 hello 중괄호를 이스케이프 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="ffd45-137">hello 다음 예제에서는 찾습니다 라는 blob *{20140101}-soundfile.mp3* hello에 *이미지* 컨테이너 및 hello `name` hello 함수 코드에서 변수 값이  *soundfile.mp3*합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="ffd45-138">트리거 메타데이터</span><span class="sxs-lookup"><span data-stu-id="ffd45-138">Trigger metadata</span></span>

<span data-ttu-id="ffd45-139">hello blob 트리거는 여러 가지 메타 데이터 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="ffd45-140">이러한 속성을 다른 바인딩에서 바인딩 식의 일부로 사용하거나 코드에서 매개 변수로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="ffd45-141">이러한 값은 hello와 동일한 의미 체계 [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="ffd45-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="ffd45-142">**BlobTrigger**.</span></span> <span data-ttu-id="ffd45-143">`string`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-143">Type `string`.</span></span> <span data-ttu-id="ffd45-144">hello 트리거 blob 경로</span><span class="sxs-lookup"><span data-stu-id="ffd45-144">hello triggering blob path</span></span>
- <span data-ttu-id="ffd45-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="ffd45-145">**Uri**.</span></span> <span data-ttu-id="ffd45-146">`System.Uri`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-146">Type `System.Uri`.</span></span> <span data-ttu-id="ffd45-147">hello 기본 위치에 대 한 hello blob의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="ffd45-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="ffd45-148">**Properties**.</span></span> <span data-ttu-id="ffd45-149">`Microsoft.WindowsAzure.Storage.Blob.BlobProperties`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="ffd45-150">blob의 시스템 속성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-150">hello blob's system properties.</span></span>
- <span data-ttu-id="ffd45-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="ffd45-151">**Metadata**.</span></span> <span data-ttu-id="ffd45-152">`IDictionary<string,string>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="ffd45-153">hello hello blob에 대 한 사용자 정의 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="ffd45-154">Blob 수신 확인</span><span class="sxs-lookup"><span data-stu-id="ffd45-154">Blob receipts</span></span>
<span data-ttu-id="ffd45-155">런타임 하면 blob 트리거 함수에 대 한 두 번 이상 호출 가져옵니다 hello Azure 함수 hello 동일한 신규 또는 업데이트 된 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="ffd45-156">유지 toodetermine 특정된 blob 버전 처리 된 경우, *수령액 blob*합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="ffd45-157">기능 저장소를 azure blob 라는 컨테이너에 수신 확인 *azure webjobs 호스트* hello 함수 앱에 대 한 Azure 저장소 계정에서에서 (hello 응용 프로그램 설정으로 정의 된 `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="ffd45-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="ffd45-158">Blob 수신 확인에는 다음 정보는 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="ffd45-159">hello 함수를 트리거 ("*&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*", 예:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="ffd45-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="ffd45-160">hello 컨테이너 이름</span><span class="sxs-lookup"><span data-stu-id="ffd45-160">hello container name</span></span>
* <span data-ttu-id="ffd45-161">hello blob 유형 ("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="ffd45-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ffd45-162">hello blob 이름</span><span class="sxs-lookup"><span data-stu-id="ffd45-162">hello blob name</span></span>
* <span data-ttu-id="ffd45-163">hello ETag (예: blob 버전 식별자: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="ffd45-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="ffd45-164">hello에서 해당 blob에 대 한 hello blob 확인을 삭제 하는 blob의 tooforce 재처리 *azure webjobs 호스트* 컨테이너 수동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="ffd45-165">포이즌 Blob 처리</span><span class="sxs-lookup"><span data-stu-id="ffd45-165">Handling poison blobs</span></span>
<span data-ttu-id="ffd45-166">지정된 Blob에 대한 Blob 트리거 함수가 실패한 경우 Azure Functions는 기본적으로 총 5번 해당 함수를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="ffd45-167">모든 5 시도 실패 하는 경우 Azure 함수 추가 라는 메시지 tooa 저장소 큐 *webjobs-blobtrigger-포이즌*합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="ffd45-168">포이즌 blob에 대 한 hello 큐 메시지는 hello 다음과 같은 속성을 포함 하는 JSON 개체:</span><span class="sxs-lookup"><span data-stu-id="ffd45-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="ffd45-169">FunctionId (hello 형태로 표시  *&lt;함수 응용 프로그램 이름 >*합니다. 함수입니다.  *&lt;함수 이름 >*)</span><span class="sxs-lookup"><span data-stu-id="ffd45-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="ffd45-170">BlobType("BlockBlob" 또는 "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="ffd45-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ffd45-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="ffd45-171">ContainerName</span></span>
* <span data-ttu-id="ffd45-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="ffd45-172">BlobName</span></span>
* <span data-ttu-id="ffd45-173">ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="ffd45-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="ffd45-174">큰 컨테이너에 대한 Blob 폴링</span><span class="sxs-lookup"><span data-stu-id="ffd45-174">Blob polling for large containers</span></span>
<span data-ttu-id="ffd45-175">모니터링 되 고 hello blob 컨테이너에 10, 000 개 이상의 blob이 있으면 런타임 검사 hello 함수 파일 toowatch 새롭거나 변경 된 blob에 대 한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="ffd45-176">이 프로세스는 실시간으로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-176">This process is not real time.</span></span> <span data-ttu-id="ffd45-177">함수 수 트리거되지 몇 분까지 또는 그 이상 hello blob가 생성 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="ffd45-178">또한 [저장소 로그는 "최선을 다해" 생성됩니다](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="ffd45-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="ffd45-179">하지만 모든 이벤트가 캡처되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="ffd45-180">경우에 따라 로그가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="ffd45-181">더 빠르거나 안정적인 blob 처리를 필요로 하는 경우 만드십시오는 [큐 메시지](../storage/queues/storage-dotnet-how-to-use-queues.md) hello blob를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="ffd45-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="ffd45-182">그런 다음 사용 하는 [큐 트리거](functions-bindings-storage-queue.md) blob 트리거 tooprocess hello blob 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="ffd45-183">Blob 트리거 및 입력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="ffd45-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="ffd45-184">.NET 함수에서와 같은 메서드 매개 변수를 사용 하 여 hello blob 데이터에 액세스 `Stream paramName`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="ffd45-185">여기에서 `paramName` hello에 지정 된 hello 값인 [트리거 구성](#trigger)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="ffd45-186">Node.js 함수에서 액세스 hello blob 데이터를 사용 하 여 입력 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ffd45-187">.NET에서는 hello 형식의 tooany hello 목록 아래에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="ffd45-188">입력 바인딩으로 사용되는 경우 이러한 형식 중 일부에는 *function.json*에서 `inout` 바인딩 방향이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="ffd45-189">고급 편집기 hello를 사용 해야 하므로이 방향 hello 표준 편집기에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="ffd45-190">`ICloudBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="ffd45-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ffd45-191">`CloudBlockBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="ffd45-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ffd45-192">`CloudPageBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="ffd45-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ffd45-193">`CloudAppendBlob`("inout" 바인딩 방향 필요)</span><span class="sxs-lookup"><span data-stu-id="ffd45-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="ffd45-194">텍스트 blob 예상 되는 경우 바인딩할 수도 있습니다 tooa.NET `string` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="ffd45-195">이 hello blob 크기가 작으면 hello 전체 blob 콘텐츠가 메모리에 로드 될 때에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="ffd45-196">일반적으로 선호 toouse을가 `Stream` 또는 `CloudBlockBlob` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="ffd45-197">트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="ffd45-197">Trigger sample</span></span>
<span data-ttu-id="ffd45-198">Blob 저장소 트리거를 정의 하는 function.json 다음 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="ffd45-199">Toohello 모니터링 대상된 컨테이너에 추가 된 각 blob의 hello 내용을 기록 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffd45-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="ffd45-200">C#</span><span class="sxs-lookup"><span data-stu-id="ffd45-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ffd45-201">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ffd45-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="ffd45-202">C#의 Blob 트리거 예</span><span class="sxs-lookup"><span data-stu-id="ffd45-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="ffd45-203">Node.js의 트리거 예</span><span class="sxs-lookup"><span data-stu-id="ffd45-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="ffd45-204">Blob 출력 바인딩 사용</span><span class="sxs-lookup"><span data-stu-id="ffd45-204">Using a blob output binding</span></span>

<span data-ttu-id="ffd45-205">.NET 함수에서 사용 해야는 `out string` 매개 변수 함수 서명 또는 hello 목록 다음의 hello 형식 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="ffd45-206">에서는 Node.js 함수를 사용 하 여 hello 출력 blob 액세스 `context.bindings.<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ffd45-207">.NET 함수 hello 유형만의 tooany를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="ffd45-208">Blob 입력 및 출력이 있는 큐 트리거 샘플</span><span class="sxs-lookup"><span data-stu-id="ffd45-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="ffd45-209">정의 하는 hello function.json 다음 가정는 [큐 저장소 트리거](functions-bindings-storage-queue.md), blob 저장소 입력 및 blob 저장소에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="ffd45-210">Hello 공지 hello 사용 `queueTrigger` 메타 데이터 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ffd45-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="ffd45-211">hello blob 입력 및 출력에 `path` 속성:</span><span class="sxs-lookup"><span data-stu-id="ffd45-211">in hello blob input and output `path` properties:</span></span>

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

<span data-ttu-id="ffd45-212">Hello 입력된 blob toohello 출력 blob를 복사 하는 hello 언어 관련 샘플을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ffd45-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="ffd45-213">C#</span><span class="sxs-lookup"><span data-stu-id="ffd45-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="ffd45-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ffd45-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="ffd45-215">C#의 Blob 바인딩 예</span><span class="sxs-lookup"><span data-stu-id="ffd45-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="ffd45-216">Node.js의 Blob 바인딩 예</span><span class="sxs-lookup"><span data-stu-id="ffd45-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ffd45-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffd45-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

