---
title: "Storage Client Library for C++을 사용하여 Azure Storage 리소스 나열 | Microsoft Docs"
description: "Microsoft Azure Storage Client Library for C++에서 목록 API를 사용하여 컨테이너, Blob, 큐, 테이블 및 엔터티를 열거하는 방법에 대해 배웁니다."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: 4a4ac7938989f821c092379aff3085f5e440d1c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="b1621-103">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="b1621-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="b1621-104">목록 작업은 Azure 저장소를 사용하는 다양한 배포 시나리오에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-104">Listing operations are key to many development scenarios with Azure Storage.</span></span> <span data-ttu-id="b1621-105">이 문서에서는 Microsoft Azure Storage Client Library for C++에서 제공된 API 목록을 사용하여 Microsoft Azure 저장소에서 개체를 보다 효율적으로 열거하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-105">This article describes how to most efficiently enumerate objects in Azure Storage using the listing APIs provided in the Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="b1621-106">이 가이드는 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp)를 통해 사용할 수 있는 Azure Storage Client Library for C++ 버전 2.x을(를) 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-106">This guide targets the Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="b1621-107">Storage Client Library는 Azure 저장소에서 개체를 나열 또는 쿼리하는 다양한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-107">The Storage Client Library provides a variety of methods to list or query objects in Azure Storage.</span></span> <span data-ttu-id="b1621-108">이 문서는 다음과 같은 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-108">This article addresses the following scenarios:</span></span>

* <span data-ttu-id="b1621-109">계정에서 컨테이너 나열</span><span class="sxs-lookup"><span data-stu-id="b1621-109">List containers in an account</span></span>
* <span data-ttu-id="b1621-110">컨테이너 또는 가상 Blob 디렉터리에서 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="b1621-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="b1621-111">계정에서 큐 나열</span><span class="sxs-lookup"><span data-stu-id="b1621-111">List queues in an account</span></span>
* <span data-ttu-id="b1621-112">계정에서 테이블 나열</span><span class="sxs-lookup"><span data-stu-id="b1621-112">List tables in an account</span></span>
* <span data-ttu-id="b1621-113">테이블에 엔터티 쿼리</span><span class="sxs-lookup"><span data-stu-id="b1621-113">Query entities in a table</span></span>

<span data-ttu-id="b1621-114">이러한 각 메서드는 다른 시나리오에 대해 다른 오버로드를 사용하여 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="b1621-115">비동기 및 동기</span><span class="sxs-lookup"><span data-stu-id="b1621-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="b1621-116">Storage Client Library for C++는 [C++ REST 라이브러리](https://github.com/Microsoft/cpprestsdk) 상단에 기본 제공되어 있기 때문에 [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html)를 사용하여 기본적으로 비동기 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-116">Because the Storage Client Library for C++ is built on top of the [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="b1621-117">예:</span><span class="sxs-lookup"><span data-stu-id="b1621-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="b1621-118">동기 작업은 해당하는 비동기 작업을 다음과 같이 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-118">Synchronous operations wrap the corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="b1621-119">다중 스레딩 응용 프로그램 또는 서비스로 작업하는 경우, 성능에 상당한 영향을 미치는 동기 API를 호출하는 스레드를 만드는 대신 비동기 API를 직접 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-119">If you are working with multiple threading applications or services, we recommend that you use the async APIs directly instead of creating a thread to call the sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="b1621-120">분할된 목록</span><span class="sxs-lookup"><span data-stu-id="b1621-120">Segmented listing</span></span>
<span data-ttu-id="b1621-121">클라우드 저장소의 규모에는 분할된 목록이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-121">The scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="b1621-122">예를 들어, Azure Blob 컨테이너에 수백만 이상의 Blob이 있거나 Azure 테이블에 수십억 이상의 엔터티가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="b1621-123">이는 이론적인 수치가 아니라 실제 고객 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="b1621-124">따라서 단일 응답에 모든 개체를 나열하기에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-124">It is therefore impractical to list all objects in a single response.</span></span> <span data-ttu-id="b1621-125">대신 페이징을 사용하여 개체를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="b1621-126">각각의 목록 API에는 *분할된* 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-126">Each of the listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="b1621-127">분할된 목록 작업에 대한 응답에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-127">The response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="b1621-128"><i>_segment</i>은 API 목록에 단일 호출을 반환한 결과 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-128"><i>_segment</i>, which contains the set of results returned for a single call to the listing API.</span></span>
* <span data-ttu-id="b1621-129">*continuation_token*은 결과의 다음 페이지를 가져오기 위해 다음 호출에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-129">*continuation_token*, which is passed to the next call in order to get the next page of results.</span></span> <span data-ttu-id="b1621-130">더 이상 반환할 결과가 없으면 연속 토큰이 null입니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-130">When there are no more results to return, the continuation token is null.</span></span>

<span data-ttu-id="b1621-131">예를 들어 컨테이너의 모든 blob을 나열하는 일반적인 호출은 다음 코드 조각처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-131">For example, a typical call to list all blobs in a container may look like the following code snippet.</span></span> <span data-ttu-id="b1621-132">코드는 다음과 같은 [샘플](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-132">The code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

```cpp
// List blobs in the blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

<span data-ttu-id="b1621-133">예를 들어, 페이지에 반환되는 결과 수는 각 API의 오버로드에서 *max_results* 매개 변수를 통해 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-133">Note that the number of results returned in a page can be controlled by the parameter *max_results* in the overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="b1621-134">*max_results* 매개 변수를 지정하지 않는 경우 한 페이지에 최대 5000개의 기본 최대 결과 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-134">If you do not specify the *max_results* parameter, the default maximum value of up to 5000 results is returned in a single page.</span></span>

<span data-ttu-id="b1621-135">또한 Azure Table Storage에 대한 쿼리는 연속 토큰이 비어 있지 않은 경우에도 사용자가 지정한 *max_results* 매개 변수 값보다 더 적은 레코드를 반환하거나 레코드를 반환하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-135">Also note that a query against Azure Table storage may return no records, or fewer records than the value of the *max_results* parameter that you specified, even if the continuation token is not empty.</span></span> <span data-ttu-id="b1621-136">한 가지 이유는 쿼리가 5초 이내에 완료할 수 없기 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-136">One reason might be that the query could not complete in five seconds.</span></span> <span data-ttu-id="b1621-137">연속 토큰이 비어 있지 않으면 해당 쿼리가 계속되며 코드가 세그먼트 결과의 크기를 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-137">As long as the continuation token is not empty, the query should continue, and your code should not assume the size of segment results.</span></span>

<span data-ttu-id="b1621-138">거의 모든 시나리오에 대한 권장 코딩 패턴은 목록 또는 쿼리의 명시적 진행을 제공하는 목록 및 서비스가 각 요청에 응답하는 방식을 분할하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-138">The recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how the service responds to each request.</span></span> <span data-ttu-id="b1621-139">특히 C++ 응용 프로그램 또는 서비스의 경우, 하위 수준의 목록 진행 제어가 메모리 및 성능 제어에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-139">Particularly for C++ applications or services, lower-level control of the listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="b1621-140">Greedy 목록</span><span class="sxs-lookup"><span data-stu-id="b1621-140">Greedy listing</span></span>
<span data-ttu-id="b1621-141">Storage Client Library for C++ 이전 버전(0.5.0 Preview 버전 이하)에는 다음 예시와 같이 테이블 및 큐에 대해 분할되지 않은 API 목록이 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-141">Earlier versions of the Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in the following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="b1621-142">이러한 메서드는 분할된 API의 래퍼로 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="b1621-143">분할된 목록에 대한 각 응답의 경우, 코드는 벡터에 대한 결과를 추가하고 전체 컨테이너가 검색된 후에 모든 결과를 반환했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-143">For each response of segmented listing, the code appended the results to a vector and returned all results after the full containers were scanned.</span></span>

<span data-ttu-id="b1621-144">이러한 방식은 저장소 계정 또는 테이블이 적은 개체를 포함할 때 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-144">This approach might work when the storage account or table contains a small number of objects.</span></span> <span data-ttu-id="b1621-145">하지만 개체 수가 증가하는 경우에는 모든 결과가 메모리에 유지되기 때문에 필요한 메모리가 제한 없이 증가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-145">However, with an increase in the number of objects, the memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="b1621-146">호출자에게 해당 진행에 대한 정보가 없는 경우 목록 작업 한 번에 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-146">One listing operation can take a very long time, during which the caller had no information about its progress.</span></span>

<span data-ttu-id="b1621-147">이러한 SDK에서 greedy 목록 API는 C#, Java 또는 JavaScript Node.js 환경에는 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-147">These greedy listing APIs in the SDK do not exist in C#, Java, or the JavaScript Node.js environment.</span></span> <span data-ttu-id="b1621-148">이러한 greedy API 사용의 잠재적인 문제를 방지하기 위해 0.6.0 Preview 버전에서 이를 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-148">To avoid the potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="b1621-149">사용자의 코드가 이러한 greedy API를 호출하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b1621-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="b1621-150">분할된 목록 API를 사용하여 코드를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-150">Then you should modify your code to use the segmented listing APIs:</span></span>

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

<span data-ttu-id="b1621-151">세그먼트의 *max_results* 매개 변수를 지정하여 응용 프로그램에 대한 성능 고려 사항을 충족하도록 요청 수와 메모리 사용량 사이의 균형을 조절할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-151">By specifying the *max_results* parameter of the segment, you can balance between the numbers of requests and memory usage to meet performance considerations for your application.</span></span>

<span data-ttu-id="b1621-152">또한 분할된 목록 API를 사용하지만 "greedy" 스타일로 로컬 모음에 데이터를 저장하는 경우, 규모별로 주의 깊게 로컬 모음에서 데이터 저장을 처리하도록 코드를 리펙터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-152">Additionally, if you're using segmented listing APIs, but store the data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code to handle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="b1621-153">Lazy 목록</span><span class="sxs-lookup"><span data-stu-id="b1621-153">Lazy listing</span></span>
<span data-ttu-id="b1621-154">greedy 목록에 잠재적인 문제가 발생했어도 컨테이너에 너무 많은 개체가 있지 않다면 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in the container.</span></span>

<span data-ttu-id="b1621-155">또한 사용자가 C# 또는 Oracle Java SDK를 사용하는 경우, 필요한 경우 특정 오프셋의 데이터만 가져오는 lazy 스타일의 목록을 제공하는 열거 프로그래밍 모델에 친숙해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-155">If you're also using C# or Oracle Java SDKs, you should be familiar with the Enumerable programming model, which offers a lazy-style listing, where the data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="b1621-156">C++에서는 반복기 기반 템플릿이 유사한 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-156">In C++, the iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="b1621-157">예를 들어, **list_blobs**를 사용하는 일반적인 lazy 목록 API는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="b1621-158">lazy 목록 패턴을 사용하는 일반적인 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-158">A typical code snippet that uses the lazy listing pattern might look like this:</span></span>

```cpp
// List blobs in the blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

<span data-ttu-id="b1621-159">lazy 목록은 동기화 모드에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="b1621-160">greedy 목록에 비해 lazy 목록은 필요한 경우에만 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="b1621-161">내부적으로 다음 반복기가 다음 세그먼트로 이동할 때에만 Azure 저장소에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-161">Under the covers, it fetches data from Azure Storage only when the next iterator moves into next segment.</span></span> <span data-ttu-id="b1621-162">따라서 메모리 사용량이 한계 크기로 제어되며 작업이 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-162">Therefore, memory usage is controlled with a bounded size, and the operation is fast.</span></span>

<span data-ttu-id="b1621-163">lazy 목록 API는 Storage Client Library for C++ 버전 2.2.0에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-163">Lazy listing APIs are included in the Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b1621-164">결론</span><span class="sxs-lookup"><span data-stu-id="b1621-164">Conclusion</span></span>
<span data-ttu-id="b1621-165">이 문서에서는 Storage Client Library for C++에서 다양한 개체에 대한 각기 다른 목록 API의 오버로드에 대해 다루었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-165">In this article, we discussed different overloads for listing APIs for various objects in the Storage Client Library for C++ .</span></span> <span data-ttu-id="b1621-166">요약하면</span><span class="sxs-lookup"><span data-stu-id="b1621-166">To summarize:</span></span>

* <span data-ttu-id="b1621-167">여러 스레드 시나리오에서 비동기 API를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="b1621-168">분할된 목록은 대부분의 시나리오에서 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="b1621-169">lazy 목록은 동기 시나리오에서 편리한 래퍼로 라이브러리에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-169">Lazy listing is provided in the library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="b1621-170">greedy 목록은 권장되지 않으며 라이브러리에서 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1621-170">Greedy listing is not recommended and has been removed from the library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1621-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1621-171">Next steps</span></span>
<span data-ttu-id="b1621-172">Azure 저장소 및 Storage Client Library for C++에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1621-172">For more information about Azure Storage and Client Library for C++, see the following resources.</span></span>

* [<span data-ttu-id="b1621-173">C++에서 Blob 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1621-173">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="b1621-174">C++에서 테이블 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1621-174">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="b1621-175">C++에서 큐 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b1621-175">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="b1621-176">Azure Storage Client Library for C++ API 설명서</span><span class="sxs-lookup"><span data-stu-id="b1621-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="b1621-177">Azure 저장소 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="b1621-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="b1621-178">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="b1621-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

