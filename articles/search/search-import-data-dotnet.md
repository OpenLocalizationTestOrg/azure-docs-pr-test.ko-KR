---
title: "aaa \"(.NET-Azure 검색) 데이터 업로드 | \"Microsoft Docs"
description: "Tooupload 데이터 tooan 인덱스에서 사용 하 여 Azure 검색.NET SDK hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="9cf24-103">.NET SDK hello 업로드 데이터 tooAzure 사용 하 여 검색</span><span class="sxs-lookup"><span data-stu-id="9cf24-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cf24-104">개요</span><span class="sxs-lookup"><span data-stu-id="9cf24-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="9cf24-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9cf24-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="9cf24-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="9cf24-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="9cf24-107">이 문서에서는 보여 어떻게 toouse hello [Azure 검색.NET SDK](https://aka.ms/search-sdk) tooimport 데이터를 Azure 검색 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="9cf24-108">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들어야](search-what-is-an-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="9cf24-109">이 문서도 이미 만들었다고 가정는 `SearchServiceClient` 같이 개체 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md#CreateSearchServiceClient)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="9cf24-110">이 문서의 모든 샘플 코드는 C#으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="9cf24-111">Hello 전체 소스 코드를 찾을 수 [GitHub에서](http://aka.ms/search-dotnet-howto)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="9cf24-112">Hello에 대 한 읽을 수 있습니다 [Azure 검색.NET SDK](search-howto-dotnet-sdk.md) hello 샘플 코드의 자세한 연습 과정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="9cf24-113">Hello.NET SDK를 사용 하 여 인덱스로 toopush 문서 순서에서에서 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="9cf24-114">만들기는 `SearchIndexClient` 개체 tooconnect tooyour 검색 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="9cf24-115">만들기는 `IndexBatch` hello 문서 toobe 포함 된 추가, 수정 또는 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="9cf24-116">Hello 호출 `Documents.Index` 방식의 프로그램 `SearchIndexClient` toosend hello `IndexBatch` tooyour 검색 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="9cf24-117">Hello SearchIndexClient 클래스의 인스턴스를 만들으십시오</span><span class="sxs-lookup"><span data-stu-id="9cf24-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="9cf24-118">tooimport 데이터를 사용 하 여 인덱스를 hello Azure 검색.NET SDK에서는 toocreate hello의 인스턴스를 만들어야 합니다 `SearchIndexClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="9cf24-119">생성할 수 있습니다이 인스턴스를 직접 하지만 쉽게 이미 있는 경우는 `SearchServiceClient` 인스턴스 toocall 해당 `Indexes.GetClient` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9cf24-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="9cf24-120">예를 들어, 가져오는 것 방법을 다음은 한 `SearchIndexClient` 에서 "호텔" 이라는 hello 인덱스에 대 한는 `SearchServiceClient` 라는 `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="9cf24-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="9cf24-121">일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="9cf24-122">`Indexes.GetClient`저장 하기 때문에 인덱스를 채우는 편리한 다른를 제공 하는 데 문제가 hello `SearchCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="9cf24-123">해당 하면 사용한 toocreate hello hello 관리자 키를 전달 하 여 이렇게 `SearchServiceClient` 새 toohello `SearchIndexClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="9cf24-124">그러나 쿼리를 실행 하는 응용 프로그램 부분에서는 hello, 것이 더 나은 toocreate hello `SearchIndexClient` 직접 관리자 키 대신 쿼리 키에 전달할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="9cf24-125">이 hello와 일치 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege) toomake 보다 안전한 응용 프로그램 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="9cf24-126">관리자 키 및 쿼리 키 hello에 대 한 자세한 내용을 확인할 수 [Azure 검색 REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="9cf24-127">`SearchIndexClient`에는 `Documents` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="9cf24-128">이 속성 수정, 삭제 또는 인덱스의 문서를 쿼리 tooadd, 필요한 모든 hello 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="9cf24-129">인덱싱 동작 toouse 결정</span><span class="sxs-lookup"><span data-stu-id="9cf24-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="9cf24-130">hello.NET SDK를 사용 하 여 tooimport 데이터, 해야 toopackage에 데이터를는 `IndexBatch` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="9cf24-131">`IndexBatch` 의 컬렉션을 캡슐화 `IndexAction` 각각 포함 하는 문서와 Azure 검색 어떤 작업 tooperform (업로드, 병합, 삭제 등)에 해당 문서에 지시 하는 속성 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="9cf24-132">Hello 아래의 선택한 작업 중 어느 것을 따라 특정 필드만 각 문서에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="9cf24-133">동작</span><span class="sxs-lookup"><span data-stu-id="9cf24-133">Action</span></span> | <span data-ttu-id="9cf24-134">설명</span><span class="sxs-lookup"><span data-stu-id="9cf24-134">Description</span></span> | <span data-ttu-id="9cf24-135">각 문서에 대해 필요한 필드</span><span class="sxs-lookup"><span data-stu-id="9cf24-135">Necessary fields for each document</span></span> | <span data-ttu-id="9cf24-136">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9cf24-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="9cf24-137">`Upload` 동작은 비슷한 tooan hello 문서를 새이 경우 삽입 및 업데이트/교체 있는 경우 하려는 "upsert"입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="9cf24-138">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="9cf24-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="9cf24-139">기존 문서를 업데이트/교체 hello 요청에 지정 되지 않은 모든 필드 갖게 되며 해당 필드가 너무 설정`null`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="9cf24-140">Hello 필드 tooa null이 아닌 값을 이전에 설정 된 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="9cf24-141">업데이트 hello를 사용 하 여 문서에서 기존 필드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="9cf24-142">Hello 문서 hello 인덱스에 없는 경우 hello 병합 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="9cf24-143">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="9cf24-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="9cf24-144">병합에서 지정 하는 필드로 hello hello 문서의 기존 필드를 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="9cf24-145">여기에는 `DataType.Collection(DataType.String)`형식 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="9cf24-146">예를 들어 경우 hello 문서는 필드가 `tags` 값으로 `["budget"]` 값과 병합을 실행 하 고 `["economy", "pool"]` 에 대 한 `tags`, hello의 최종 값 hello `tags` 필드가 `["economy", "pool"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="9cf24-147">`["budget", "economy", "pool"]`이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="9cf24-148">이 작업 처럼 동작 `Merge` hello 키를 이미 제공 하 여 문서 hello 인덱스에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="9cf24-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="9cf24-149">처럼 동작 하는 hello 문서가 없는 경우 `Upload` 새 문서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="9cf24-150">키와, toodefine를 원하는 다른 모든 필드</span><span class="sxs-lookup"><span data-stu-id="9cf24-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="9cf24-151">Hello 인덱스에서 hello 지정 된 문서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="9cf24-152">키만</span><span class="sxs-lookup"><span data-stu-id="9cf24-152">key only</span></span> |<span data-ttu-id="9cf24-153">Hello 키 필드를 무시 것과 다른 모든 필드 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="9cf24-154">문서에서 개별 필드 tooremove 사용 `Merge` 대신 하 고 간단 하 게 hello 필드를 명시적으로 설정 toonull 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="9cf24-155">와 toouse 원하는 어떤 작업을 지정할 수 있습니다 hello의 다양 한 정적 메서드를 hello `IndexBatch` 및 `IndexAction` hello 다음 섹션에 나와 있는 것 처럼 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="9cf24-156">IndexBatch 생성</span><span class="sxs-lookup"><span data-stu-id="9cf24-156">Construct your IndexBatch</span></span>
<span data-ttu-id="9cf24-157">준비 tooconstruct hello는 문서에는 작업 tooperform를 파악 했으므로 `IndexBatch`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="9cf24-158">다음 예제에서는 어떻게 hello toocreate 몇 가지 다른 동작이 포함 된 일괄 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="9cf24-159">예에서 사용 하 라는 사용자 지정 클래스 `Hotel` tooa 문서 hello "호텔" 인덱스에 매핑하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="9cf24-160">사용 하 여이 경우 `Upload`, `MergeOrUpload`, 및 `Delete` hello에서 호출 하는 hello 메서드에 의해 지정 된 대로 우리의 검색 동작, `IndexAction` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="9cf24-161">이 예제 "호텔" 인덱스는 문서 수로 채워진다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="9cf24-162">어떻게 없는 toospecify hello 가능한 문서 필드를 모두 사용 하는 경우 유의 `MergeOrUpload` 어떻게 hello 문서 키만 지정 하 고 (`HotelId`) 사용 하는 경우 `Delete`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="9cf24-163">또한, 이때 인덱싱 단일 요청에서 too1000 문서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf24-164">이 예제에서는 다양 한 작업 toodifferent 문서 적용 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="9cf24-165">호출 하는 대신 hello 일괄 처리의 모든 문서 전체 tooperform 동일한 동작 hello 하려는 경우 `IndexBatch.New`, 사용할 수 있습니다의 다른 정적 메서드를 hello `IndexBatch`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="9cf24-166">예를 들어 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` 또는 `IndexBatch.Delete`를 호출하여 배치를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="9cf24-167">이러한 메서드는 `IndexAction` 개체 대신 문서의 컬렉션을 가져옵니다(이 예제에서 `Hotel` 유형의 개체).</span><span class="sxs-lookup"><span data-stu-id="9cf24-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="9cf24-168">가져오기 데이터 toohello 인덱스</span><span class="sxs-lookup"><span data-stu-id="9cf24-168">Import data toohello index</span></span>
<span data-ttu-id="9cf24-169">초기화 된 했으므로 `IndexBatch` 개체를 호출 하 여 toohello 인덱스 보낼 수 있습니다 `Documents.Index` 에 프로그램 `SearchIndexClient` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="9cf24-170">hello 방법을 예제와 다음 toocall `Index`외에 일부 추가 단계가 tooperform 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="9cf24-171">참고 hello `try` / `catch` hello 호출 toohello 주변 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9cf24-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="9cf24-172">hello catch 블록에서 인덱싱에 대 한 중요 한 오류 사례를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="9cf24-173">Azure 검색 서비스 tooindex hello의 일부 문서 hello 일괄 처리에 실패 하는 경우는 `IndexBatchException` 가 throw `Documents.Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="9cf24-174">이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="9cf24-175">**이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cf24-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="9cf24-176">지연 하 고, 실패 인덱싱 hello 문서를 다시 시도 하십시오 또는 로그 hello 예제에서는 하거나 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="9cf24-177">마지막으로, hello 코드를 2 초 동안 지연 위의 hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="9cf24-178">인덱싱 발생 비동기적으로 Azure 검색 서비스에 hello 샘플 응용 프로그램 toowait hello 문서는 검색에 사용할 수 있는 짧은 시간 tooensure 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="9cf24-179">이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="9cf24-180">Hello.NET SDK에서 문서를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cf24-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="9cf24-181">Hello Azure 검색.NET SDK와 같은 사용자 정의 클래스의 인스턴스 수 tooupload은 어떻게 할까요 `Hotel` toohello 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="9cf24-182">toohelp 해당 질문에 답변을 사용 hello `Hotel` 클래스에 정의 된 toohello 인덱스 스키마에 매핑하는 [hello.NET SDK를 사용 하 여 Azure 검색 인덱스를 만들](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="9cf24-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="9cf24-183">hello 먼저 toonotice은 각 public 속성의 `Hotel` tooa 필드 hello 인덱스 정의의 하지만 한 가지 중요 한 차이점은 해당: hello 이름은 각 공용 동안 소문자 ("카멜식 대 /")으로 시작 하는 각 필드의 hello 이름 속성의 `Hotel` 대문자 문자 ("파스칼식 대 / 소문자로")로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="9cf24-184">여기서 hello 대상 스키마는 hello 응용 프로그램 개발자의 외부 hello 제어 데이터 바인딩을 수행 하는.NET 응용 프로그램에서 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="9cf24-185">속성 이름은 카멜식 대 / 소문자를 늘려 명명 지침 tooviolate hello.NET 대신 hello SDK toomap hello 속성 이름은 toocamel 사례 hello로 자동으로 알 수 있습니다 `[SerializePropertyNamesAsCamelCase]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf24-186">Azure 검색.NET SDK hello hello를 사용 하 여 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리 tooserialize 하 고 사용자 사용자 지정 모델 개체 tooand JSON에서 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="9cf24-187">필요한 경우 직렬화를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="9cf24-188">자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](search-howto-dotnet-sdk.md#JsonDotNet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cf24-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="9cf24-189">이 한 가지 예로 hello hello 사용 `[JsonProperty]` hello에 대 한 특성 `DescriptionFr` hello 위의 샘플 코드에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="9cf24-190">hello에 대 한 두 번째 중요 한 사항은 hello `Hotel` 클래스는 hello 공용 속성의 hello 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="9cf24-191">이러한 속성의 hello.NET 형식은 hello 인덱스 정의의 해당 필드 형식을 tootheir 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="9cf24-192">예를 들어 hello `Category` 문자열 속성 매핑됩니다 toohello `category` 형식인 필드 `DataType.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="9cf24-193">`bool?` 및 `DataType.Boolean`, `DateTimeOffset?` 및 `DataType.DateTimeOffset` 사이에는 유사한 유형 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="9cf24-194">hello 형식 매핑에 대 한 특정 규칙 hello hello로 사항은 `Documents.Get` hello에 대 한 메서드 [Azure 검색.NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="9cf24-195">이 기능은 toouse 양방향;에서 작동 하는 문서로 서 사용자 고유의 클래스 또한 검색 결과 검색 하 고 수 hello SDK 자동으로 형식을 역직렬화 할에 tooa의 선택한 hello에 나와 있는 것 처럼 [다음 기사](search-query-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9cf24-196">hello Azure 검색.NET SDK에서는 hello를 사용 하 여 동적으로 입력 문서 `Document` 필드 이름 toofield 값의 키/값 매핑이 설정 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="9cf24-197">이 hello 인덱스 스키마 디자인 타임에 알 수 없는 하거나는 것이 불편 toobind toospecific 모델 클래스 시나리오에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="9cf24-198">Hello SDK의에서 문서를 처리 하는 모든 hello 메서드 hello를 사용 하는 오버 로드를 갖고 `Document` 클래스 뿐만 아니라 제네릭 형식 매개 변수를 사용 하는 강력한 형식의 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="9cf24-199">후자의 hello만이 문서에 hello 샘플 코드에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="9cf24-200">**Null 허용 데이터 형식을 사용해야 하는 이유**</span><span class="sxs-lookup"><span data-stu-id="9cf24-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="9cf24-201">사용자 고유의 모델 클래스 toomap tooan Azure 검색 인덱스를 디자인할 때와 같은 값 형식의 속성을 선언 하는 것이 좋습니다 `bool` 및 `int` nullable toobe (예를 들어 `bool?` 대신 `bool`).</span><span class="sxs-lookup"><span data-stu-id="9cf24-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="9cf24-202">Nullable이 아닌 속성을 사용 하면 있으면 너무**보장** 문서가 인덱스에는 hello 해당 필드에 대 한 null 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="9cf24-203">Hello SDK도 아니고 hello Azure 검색 서비스 할 수 있습니다 tooenforce이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="9cf24-204">이 가상의 중요 하지 않은 것: 있는 인덱스를 추가 하면 새 필드 tooan 기존 유형의 경우를 가정해 보십시오 `DataType.Int32`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="9cf24-205">Hello 인덱스 정의 업데이트 한 후 모든 문서 (Azure 검색에서 null을 허용 하지 않는 형식도) 이후 해당 새 필드에 대해 null 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="9cf24-206">다음으로 nullable이 아닌 모델 클래스를 사용 하는 경우 `int` 해당 필드에 대 한 속성을 얻게 됩니다는 `JsonSerializationException` tooretrieve 문서 하려고 할 때 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="9cf24-207">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cf24-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cf24-208">Next steps</span></span>
<span data-ttu-id="9cf24-209">Azure 검색 인덱스를 채울 후 준비 toostart 문서에 대 한 쿼리 toosearch 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cf24-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="9cf24-210">세부 정보는 [Azure 검색 인덱스 쿼리](search-query-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cf24-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

