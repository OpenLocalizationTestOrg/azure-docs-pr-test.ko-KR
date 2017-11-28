---
title: "데이터 업로드(.NET - Azure Search) | Microsoft Docs"
description: ".NET SDK를 사용하여 Azure 검색에서 인덱스에 데이터를 업로드하는 방법을 알아봅니다."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="428f3-103">.NET SDK를 사용하여 Azure 검색에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="428f3-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="428f3-104">개요</span><span class="sxs-lookup"><span data-stu-id="428f3-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="428f3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="428f3-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="428f3-106">REST</span><span class="sxs-lookup"><span data-stu-id="428f3-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="428f3-107">이 문서에서는 [Azure 검색 .NET SDK](https://aka.ms/search-sdk) 를 사용하여 Azure 검색 인덱스에 데이터를 가져오는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="428f3-108">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들어야](search-what-is-an-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="428f3-109">이 문서에서는 [.NET SDK를 사용하여 Azure 검색 인덱스 만들기](search-create-index-dotnet.md#CreateSearchServiceClient)에서 보여준 것처럼 `SearchServiceClient` 개체를 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="428f3-110">이 문서의 모든 샘플 코드는 C#으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="428f3-111">전체 소스 코드는 [GitHub](http://aka.ms/search-dotnet-howto)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="428f3-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="428f3-112">좀 더 구체적인 샘플 코드 연습은 [Azure Search .NET SDK](search-howto-dotnet-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="428f3-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="428f3-113">.NET SDK를 사용하여 인덱스에 문서를 푸시하기 위해 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="428f3-114">`SearchIndexClient` 개체를 만들어서 검색 인덱스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="428f3-115">추가, 수정 또는 삭제하려는 문서를 포함하는 `IndexBatch`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="428f3-116">`SearchIndexClient`의 `Documents.Index` 메서드를 호출하여 검색 인덱스에 `IndexBatch`를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="428f3-117">SearchIndexClient 클래스의 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="428f3-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="428f3-118">Azure 검색 .NET SDK를 사용하여 인덱스에 데이터를 가져오려면 `SearchIndexClient` 클래스의 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="428f3-119">이 인스턴스를 직접 생성할 수 있지만 `Indexes.GetClient` 메서드를 호출하는 `SearchServiceClient` 인스턴스가 있는 경우 더 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="428f3-120">예를 들어 다음은 `serviceClient`라는 `SearchServiceClient`에서 "호텔"이라는 인덱스에 `SearchIndexClient`를 가져오는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="428f3-121">일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="428f3-122">`Indexes.GetClient`는 다른 `SearchCredentials`를 제공하는 문제를 피할 수 있으므로 인덱스를 생성하기에 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="428f3-123">이는 새 `SearchIndexClient`에 `SearchServiceClient`을(를) 만드는 데 사용하는 관리 키를 눌러 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="428f3-124">그러나 쿼리를 실행하는 일부 응용 프로그램의 경우, `SearchIndexClient` 을(를) 직접 만들어 관리 키 대신에 쿼리 키에서 전달하는 것이 더 낫습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="428f3-125">이는 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege) 과 일치하고 응용 프로그램을 더욱 안전하게 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="428f3-126">관리 키와 쿼리 키에 대한 자세한 내용은 [Azure Search REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="428f3-127">`SearchIndexClient`에는 `Documents` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="428f3-128">이 속성은 인덱스에서 문서를 추가, 수정, 삭제 또는 쿼리해야 하는 모든 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="428f3-129">사용할 인덱싱 동작 결정</span><span class="sxs-lookup"><span data-stu-id="428f3-129">Decide which indexing action to use</span></span>
<span data-ttu-id="428f3-130">.NET SDK를 사용하여 데이터를 가져오려면 데이터를 `IndexBatch` 개체에 패키지로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="428f3-131">`IndexBatch`는 `IndexAction` 개체의 컬렉션을 캡슐화하며 각각은 Azure 검색이 해당 문서에 대해 수행할 작업(업로드, 병합, 삭제 등)을 알려주는 문서 및 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="428f3-132">아래에서 어떤 작업을 선택하는지에 따라 특정 필드는 각 문서에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="428f3-133">조치</span><span class="sxs-lookup"><span data-stu-id="428f3-133">Action</span></span> | <span data-ttu-id="428f3-134">설명</span><span class="sxs-lookup"><span data-stu-id="428f3-134">Description</span></span> | <span data-ttu-id="428f3-135">각 문서에 대해 필요한 필드</span><span class="sxs-lookup"><span data-stu-id="428f3-135">Necessary fields for each document</span></span> | <span data-ttu-id="428f3-136">메모</span><span class="sxs-lookup"><span data-stu-id="428f3-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="428f3-137">`Upload` 작업은 새 문서는 삽입하고 기존 문서는 업데이트/교체하는 "upsert"와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="428f3-138">키, 더하기 정의하려는 기타 필드</span><span class="sxs-lookup"><span data-stu-id="428f3-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="428f3-139">기존 문서를 업데이트/교체하는 경우 요청에 지정되지 않은 필드는 해당 필드를 `null`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="428f3-140">필드가 이전에 null이 아닌 값으로 설정된 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="428f3-141">기존 문서를 지정한 필드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="428f3-142">인덱스에 문서가 없으면 병합이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="428f3-143">키, 더하기 정의하려는 기타 필드</span><span class="sxs-lookup"><span data-stu-id="428f3-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="428f3-144">문서의 기존 필드는 병합에서 지정하는 필드로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="428f3-145">여기에는 `DataType.Collection(DataType.String)`형식 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="428f3-146">예를 들어 값이 `["budget"]`인 `tags` 필드가 포함되어 있는 문서에서 `tags`에 대해 `["economy", "pool"]` 값과의 병합을 실행하면 `tags` 필드의 최종 값은 `["economy", "pool"]`이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="428f3-147">`["budget", "economy", "pool"]`이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="428f3-148">이 작업은 지정된 키를 포함하는 문서가 인덱스에 이미 있는 경우 `Merge`와 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="428f3-149">문서가 없는 경우 새 문서가 있는 `Upload` 와 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="428f3-150">키, 더하기 정의하려는 기타 필드</span><span class="sxs-lookup"><span data-stu-id="428f3-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="428f3-151">삭제 시에는 지정된 문서를 인덱스에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="428f3-152">키만</span><span class="sxs-lookup"><span data-stu-id="428f3-152">key only</span></span> |<span data-ttu-id="428f3-153">키 필드 외의 지정한 모든 필드는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="428f3-154">문서에서 개별 필드를 제거하려는 경우 대신 `Merge` 를 사용하고 필드를 명시적으로 Null로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="428f3-155">다음 섹션에서 보여준 것처럼 다양한 정적 메서드인 `IndexBatch` 및 `IndexAction` 클래스와 함께 사용하려는 동작을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="428f3-156">IndexBatch 생성</span><span class="sxs-lookup"><span data-stu-id="428f3-156">Construct your IndexBatch</span></span>
<span data-ttu-id="428f3-157">이제 문서에서 수행되는 작업을 알고 나면 `IndexBatch`를 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="428f3-158">아래 예제에서는 몇 가지 다른 작업으로 배치를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="428f3-159">이 예제에서는 "호텔" 인덱스에 있는 문서에 매핑되는 `Hotel` 이라는 사용자 지정 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="428f3-160">이 경우에 `IndexAction` 클래스에서 호출된 메서드에 지정된 대로 `Upload`, `MergeOrUpload` 및 `Delete`를 검색 작업으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="428f3-161">이 예제 "호텔" 인덱스는 문서 수로 채워진다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="428f3-162">`MergeOrUpload`를 사용하는 경우 가능한 문서 필드를 모두 지정하지 않는 방법 및 `Delete`를 사용하는 경우 문서 키(`HotelId`)를 지정하는 방법을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="428f3-163">또한 단일 인덱싱 요청에서 최대 1000개의 문서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="428f3-164">이 예제에서는 다른 문서에 다른 동작을 적용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="428f3-165">배치에서 모든 문서에 `IndexBatch.New`를 호출하는 대신 동일한 작업을 수행하려는 경우 `IndexBatch`라는 기타 정적 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="428f3-166">예를 들어 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` 또는 `IndexBatch.Delete`를 호출하여 배치를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="428f3-167">이러한 메서드는 `IndexAction` 개체 대신 문서의 컬렉션을 가져옵니다(이 예제에서 `Hotel` 유형의 개체).</span><span class="sxs-lookup"><span data-stu-id="428f3-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="428f3-168">인덱스에 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="428f3-168">Import data to the index</span></span>
<span data-ttu-id="428f3-169">`IndexBatch` 개체를 초기화했다면 `SearchIndexClient` 개체에서 `Documents.Index`를 호출하여 인덱스로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="428f3-170">다음 예제에서는 수행해야 하는 몇 가지 추가 단계 뿐만 아니라 `Index`를 호출하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="428f3-171">`Index` 메서드에 대한 호출과 관련된 `try`/`catch`를 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="428f3-172">catch 블록은 인덱싱에 대한 중요한 오류 사례를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="428f3-173">Azure 검색 서비스가 일괄 처리에서 문서 일부를 인덱싱하는데 실패하는 경우 `Documents.Index`에 의해 `IndexBatchException`이(가) 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="428f3-174">이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="428f3-175">**이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="428f3-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="428f3-176">실패한 문서 인덱싱을 잠시 후 다시 시도하거나, 샘플에서 하던 것처럼 기록하여 계속하거나, 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="428f3-177">마지막으로 2초 동안 위의 예에서 코드가 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="428f3-178">Azure 검색 서비스에서 인덱싱이 비동기적으로 발생하기 때문에, 샘플 응용 프로그램은 문서 검색을 위해 잠시 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="428f3-179">이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="428f3-180">.NET SDK가 문서를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="428f3-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="428f3-181">Azure 검색.NET SDK가 어떻게 `Hotel` 와(과) 같은 사용자 정의 클래스의 인스턴스를 업로드할 수 있는지 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="428f3-182">질문에 대답하려면 [.NET SDK를 사용하여 Azure 검색 인덱스 만들기](search-create-index-dotnet.md#DefineIndex)에 정의된 인덱스 스키마에 매핑하는 `Hotel` 클래스를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="428f3-183">먼저 주목할 것은 `Hotel`의 각 공용 속성이 인덱스 정의의 필드와 일치하지만 한 가지 중요한 차이가 있습니다. 각 필드의 이름은 소문자("카멜식 대/소문자")로 시작하지만, `Hotel`의 각 공용 속성 이름은 대문자 문자("파스칼식 대/소문자")로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="428f3-184">이것은 대상 스키마가 응용 프로그램 개발자의 제어 범위를 벗어난 데이터 바인딩을 수행하는 .NET 응용 프로그램의 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="428f3-185">카멜식 대/소문자 속성으로 이름을 지정하면 .NET 이름 지정 지침을 위반하지 않고 속성 이름을 자동으로 `[SerializePropertyNamesAsCamelCase]` 특성을 지닌 카멜식 대/소문자에 매핑하도록 SDK에 명령할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="428f3-186">Azure 검색 .NET SDK는 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리를 사용하여 사용자 지정 모델 개체를 JSON과 직렬화 및 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="428f3-187">필요한 경우 직렬화를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="428f3-188">자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](search-howto-dotnet-sdk.md#JsonDotNet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="428f3-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="428f3-189">한 가지 예는 위의 샘플 코드에 있는 `DescriptionFr` 속성의 `[JsonProperty]` 특성을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="428f3-190">`Hotel` 클래스에 대해 두 번째로 중요한 부분은 공용 속성의 데이터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="428f3-191">이러한 속성의 .NET 유형은 인덱스 정의의 동등한 필드 유형에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="428f3-192">예를 들어, `Category` 문자열 속성은 `DataType.String` 유형인 `category` 필드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="428f3-193">`bool?` 및 `DataType.Boolean`, `DateTimeOffset?` 및 `DataType.DateTimeOffset` 사이에는 유사한 유형 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="428f3-194">유형 매핑에 대한 특정 규칙은 [Azure Search .NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)에 `Documents.Get` 메서드로 문서화됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="428f3-195">고유한 클래스를 문서로 사용하는 이 기능은 양방향으로 작동합니다. 또한 [다음 문서](search-query-dotnet.md)에서 보여준 것처럼 검색 결과를 검색하고 SDK가 자동으로 사용자가 선택한 유형으로 deserialize하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="428f3-196">Azure 검색.NET SDK는 필드 이름을 필드 값에 매핑하는 키/값인 `Document` 클래스를 사용하여 동적 유형의 문서도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="428f3-197">디자인 타임에서 인덱스 스키마를 알 수 없거나 특정 모델 클래스에 바인딩하기 불편한 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="428f3-198">문서를 처리하는 SDK의 모든 메서드에는 `Document` 클래스와 연동하는 오버로드와 제네릭 유형 매개 변수를 취하는 강력한 유형의 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="428f3-199">후자는 이 문서의 샘플 코드에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="428f3-200">**Null 허용 데이터 형식을 사용해야 하는 이유**</span><span class="sxs-lookup"><span data-stu-id="428f3-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="428f3-201">고유의 모델 클래스를 Azure 검색 인덱스에 매핑하도록 설계하는 경우 `bool` 및 `int` 등과 같은 값 유형의 속성을 Null이 허용되도록 선언하는 것이 좋습니다(예: `bool` 대신 `bool?`).</span><span class="sxs-lookup"><span data-stu-id="428f3-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="428f3-202">Null이 허용되지 않는 속성을 사용하는 경우 인덱스의 문서가 해당 필드에 대해 Null 값을 포함하지 않도록 **보장** 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="428f3-203">SDK와 Azure 검색 서비스 모두 이를 적용하는 데 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="428f3-204">이것은 가상의 문제가 아닙니다. `DataType.Int32` 형식인 기존 인덱스에 새 필드를 추가하는 시나리오를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="428f3-205">인덱스 정의를 업데이트한 후 모든 문서는 해당하는 새 필드에 대해 Null 값을 포함하게 됩니다(Azure 검색에서 모든 형식은 Null을 허용하기 때문).</span><span class="sxs-lookup"><span data-stu-id="428f3-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="428f3-206">그런 다음 해당 필드에 대해 Null이 허용되지 않는 `int` 속성으로 모델 클래스를 사용하는 경우 문서를 검색하려고 시도할 때 다음과 같은 `JsonSerializationException`이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="428f3-207">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="428f3-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="428f3-208">Next steps</span></span>
<span data-ttu-id="428f3-209">Azure 검색 인덱스를 채운 후에 문서를 검색하기 위해 쿼리를 발급하기 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="428f3-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="428f3-210">세부 정보는 [Azure 검색 인덱스 쿼리](search-query-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="428f3-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

