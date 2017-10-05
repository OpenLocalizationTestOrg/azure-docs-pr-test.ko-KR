---
title: "인덱스 쿼리(.NET API - Azure Search) | Microsoft Docs"
description: "Azure 검색에서 검색 쿼리를 작성하고 검색 매개 변수를 사용하여 검색 결과를 필터링하고 정렬합니다."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="ba72f-103">.NET SDK를 사용하여 Azure 검색 인덱스 쿼리</span><span class="sxs-lookup"><span data-stu-id="ba72f-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba72f-104">개요</span><span class="sxs-lookup"><span data-stu-id="ba72f-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="ba72f-105">포털</span><span class="sxs-lookup"><span data-stu-id="ba72f-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="ba72f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="ba72f-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="ba72f-107">REST</span><span class="sxs-lookup"><span data-stu-id="ba72f-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="ba72f-108">이 문서는 [Azure 검색 .NET SDK](https://aka.ms/search-sdk)를 사용하여 인덱스를 쿼리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="ba72f-109">이 연습을 시작하기 전에 [Azure 검색 인덱스를 만들고](search-what-is-an-index.md) [데이터로 채워야](search-what-is-data-import.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ba72f-110">이 문서의 모든 샘플 코드는 C#으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="ba72f-111">전체 소스 코드는 [GitHub](http://aka.ms/search-dotnet-howto)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba72f-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="ba72f-112">좀 더 구체적인 샘플 코드 연습은 [Azure Search .NET SDK](search-howto-dotnet-sdk.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba72f-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="ba72f-113">Azure 검색 서비스의 쿼리 API 키 식별</span><span class="sxs-lookup"><span data-stu-id="ba72f-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="ba72f-114">Azure 검색 인덱스를 만들었으므로 .NET SDK를 사용하여 쿼리를 발급할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="ba72f-115">먼저 프로비전한 검색 서비스에 대해 생성된 쿼리 API 키 중 하나가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="ba72f-116">.NET SDK는 서비스에 대한 모든 요청에 대해 이 API 키를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="ba72f-117">유효한 키가 있다면 요청을 기반으로 요청을 보내는 응용 프로그램과 이를 처리하는 서비스 사이에 신뢰가 쌓입니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="ba72f-118">[Azure Portal](https://portal.azure.com/)에 로그인하면 서비스의 API 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="ba72f-119">Azure 검색 서비스의 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="ba72f-120">"키" 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="ba72f-121">서비스에는 *관리 키* 및 *쿼리 키*가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="ba72f-122">기본 및 보조 *관리 키* 는 서비스를 관리하며 인덱스, 인덱서 및 데이터 원본을 만들고 삭제하는 기능을 비롯한 모든 작업에 전체 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="ba72f-123">두 개의 키가 있으므로 기본 키를 다시 생성하려는 경우 보조 키를 사용하여 계속할 수 있고 반대도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="ba72f-124">*쿼리 키* 는 인덱스 및 문서에 대한 읽기 전용 액세스를 부여하며 일반적으로 검색 요청을 실행하는 클라이언트 응용 프로그램에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="ba72f-125">인덱스를 쿼리하기 위해 쿼리 키 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="ba72f-126">또한 쿼리에 관리 키를 사용할 수 있지만 [최소 권한의 원칙](https://en.wikipedia.org/wiki/Principle_of_least_privilege)에 따라 응용 프로그램 코드에 쿼리 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="ba72f-127">SearchIndexClient 클래스의 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="ba72f-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="ba72f-128">Azure 검색 .NET SDK로 쿼리를 발급하려면 `SearchIndexClient` 클래스의 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="ba72f-129">이 클래스에는 몇 가지 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-129">This class has several constructors.</span></span> <span data-ttu-id="ba72f-130">그 중에 하나는 검색 서비스 이름, 인덱스 이름 및 `SearchCredentials` 개체를 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="ba72f-131">`SearchCredentials` 는 API 키를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="ba72f-132">아래 코드에서는 응용 프로그램의 구성 파일([샘플 응용 프로그램](http://aka.ms/search-dotnet-howto)의 경우 `appsettings.json`)에 저장된 검색 서비스 이름 및 API 키에 대한 값을 사용하여 ([.NET SDK를 사용하여 Azure Search 인덱스 만들기](search-create-index-dotnet.md)에서 만든) "호텔" 인덱스에 새로운 `SearchIndexClient`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="ba72f-133">`SearchIndexClient`에는 `Documents` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="ba72f-134">이 속성은 Azure 검색 인덱스를 쿼리하는 데 필요한 모든 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="ba72f-135">인덱스 쿼리</span><span class="sxs-lookup"><span data-stu-id="ba72f-135">Query your index</span></span>
<span data-ttu-id="ba72f-136">.NET SDK로 검색하는 작업은 `SearchIndexClient`에서 `Documents.Search` 메서드를 호출하는 것 만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="ba72f-137">이 메서드는 쿼리를 구체화하는 데 사용할 수 있는 `SearchParameters` 개체와 함께 검색 텍스트를 비롯한 몇 가지 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="ba72f-138">쿼리 유형</span><span class="sxs-lookup"><span data-stu-id="ba72f-138">Types of Queries</span></span>
<span data-ttu-id="ba72f-139">사용할 두 가지 기본 [쿼리 유형](search-query-overview.md#types-of-queries)은 `search` 및 `filter`입니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="ba72f-140">`search` 쿼리는 인덱스에서 모든 *검색 가능한* 필드에 대해 하나 이상의 단어를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="ba72f-141">`filter` 쿼리는 인덱스의 *필터링 가능한* 모든 필드에 걸쳐 부울 식을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="ba72f-142">검색 및 필터는 모두 `Documents.Search` 메서드를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="ba72f-143">검색 쿼리는 `searchText` 매개 변수에 전달될 수 있는 반면 필터 식은 `SearchParameters` 클래스의 `Filter` 속성에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="ba72f-144">검색하지 않고 필터링하려면 `searchText` 매개 변수에 `"*"`를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="ba72f-145">필터링하지 않고 검색하려면 `Filter` 속성을 설정하지 않고 그대로 두거나 `SearchParameters` 인스턴스에 전달하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="ba72f-146">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="ba72f-146">Example Queries</span></span>
<span data-ttu-id="ba72f-147">다음 샘플 코드는 [.NET SDK를 사용하여 Azure 검색 인덱스 만들기](search-create-index-dotnet.md#DefineIndex)에 정의된 "호텔" 인덱스를 쿼리하는 몇 가지 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="ba72f-148">검색 결과와 함께 반환된 문서가 `Hotel` 클래스의 인스턴스이며 [.NET SDK를 사용하여 Azure 검색에서 데이터 가져오기](search-import-data-dotnet.md#HotelClass)에 정의되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="ba72f-149">샘플 코드는 `WriteDocuments` 메서드를 사용하여 콘솔에 검색 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="ba72f-150">이 메서드는 다음 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="ba72f-151">검색 결과 처리</span><span class="sxs-lookup"><span data-stu-id="ba72f-151">Handle search results</span></span>
<span data-ttu-id="ba72f-152">`Documents.Search` 메서드는 쿼리의 결과를 포함하는 `DocumentSearchResult` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="ba72f-153">이전 섹션의 예제에서는 콘솔에 검색 결과 출력하기 위해 `WriteDocuments` 이라는 메서드를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="ba72f-154">다음은 이전 섹션의 쿼리 모양에 대한 결과이며 "호텔" 인덱스가 [.NET SDK를 사용하여 Azure 검색에서 데이터 가져오기](search-import-data-dotnet.md)의 샘플 데이터로 채워진다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="ba72f-155">위의 샘플 코드는 콘솔을 사용하여 검색 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="ba72f-156">마찬가지로 고유한 응용 프로그램에 검색 결과를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba72f-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="ba72f-157">ASP.NET MVC 기반 웹 응용 프로그램에서 검색 결과를 렌더링하는 방법의 예는 [GitHub에서 이 샘플](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba72f-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

