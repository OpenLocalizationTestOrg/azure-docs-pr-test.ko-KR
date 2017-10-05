---
title: ".NET 응용 프로그램에서 Azure Search를 사용하는 방법 | Microsoft Docs"
description: ".NET 응용 프로그램에서 Azure 검색을 사용하는 방법"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="9cc2c-103">.NET 응용 프로그램에서 Azure 검색을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cc2c-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="9cc2c-104">이 문서는 [Azure 검색.NET SDK](https://aka.ms/search-sdk)를 준비하여 실행하기 위한 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="9cc2c-105">Azure 검색을 사용하여 응용 프로그램에서 풍부한 검색 환경을 구현하는 .NET SDK를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="9cc2c-106">Azure 검색 SDK의 주요 기능</span><span class="sxs-lookup"><span data-stu-id="9cc2c-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="9cc2c-107">SDK는 클라이언트 라이브러리 `Microsoft.Azure.Search`로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="9cc2c-108">인덱스, 데이터 원본 및 인덱서를 관리할 뿐만 아니라 문서를 업로드 및 관리, 쿼리를 실행할 수 있으며, 이 모두를 HTTP와 JSON의 세부 정보를 처리하지 않고 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="9cc2c-109">클라이언트 라이브러리는 `SearchServiceClient` 및 `SearchIndexClient` 클래스에서 `Index`, `Field`, `Document` 등의 클래스와 `Indexes.Create` 및 `Documents.Search` 등의 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="9cc2c-110">이러한 클래스는 다음과 같은 네임 스페이스에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="9cc2c-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="9cc2c-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="9cc2c-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="9cc2c-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="9cc2c-113">Azure 검색 .NET SDK의 현재 버전이 이제 일반 공급됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="9cc2c-114">다음 버전에 반영하기 위한 피드백을 제공하려는 경우 [피드백 페이지](https://feedback.azure.com/forums/263029-azure-search/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="9cc2c-115">.NET SDK는 [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)의 `2016-09-01` 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="9cc2c-116">이 버전에서 이제 사용자 지정 분석기와 Azure Blob 및 Azure 테이블 인덱서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="9cc2c-117">이 버전에 포함되지 *않은* 인덱싱 JSON 및 CSV 파일에 대한 지원 등은 [미리 보기](search-api-2015-02-28-preview.md)로 제공되며 이전에 제공된 [.NET SDK 2.0-preview 버전](https://aka.ms/search-sdk-preview)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="9cc2c-118">이 SDK는 Search 서비스 생성 및 확장, API 키 관리 등의 [관리 작업](https://docs.microsoft.com/rest/api/searchmanagement/)을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="9cc2c-119">.NET 응용 프로그램에서 Search 리소스를 관리해야 하는 경우 [Azure Search .NET 관리 SDK](https://aka.ms/search-mgmt-sdk)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="9cc2c-120">최신 버전의 SDK로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9cc2c-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="9cc2c-121">Azure 검색 .NET SDK 이전 버전을 사용하는 경우 새로운 일반 공급 버전으로 업그레이드하려면 [이 문서](search-dotnet-sdk-migration.md) 에서 방법을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="9cc2c-122">SDK의 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9cc2c-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="9cc2c-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="9cc2c-124">Azure 검색 서비스</span><span class="sxs-lookup"><span data-stu-id="9cc2c-124">Your own Azure Search service.</span></span> <span data-ttu-id="9cc2c-125">SDK를 사용하려면 서비스 이름과 하나 이상의 API 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="9cc2c-126">[포털에서 서비스 만들기](search-create-service-portal.md)는 이들 단계를 통해 도움을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="9cc2c-127">Visual Studio에서 "NuGet 패키지 관리"를 사용하여 Azure 검색.NET SDK [NuGet 패키지](http://www.nuget.org/packages/Microsoft.Azure.Search) 를 다운로드하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="9cc2c-128">NuGet.org에서 패키지 이름 `Microsoft.Azure.Search` 을(를) 검색하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="9cc2c-129">Azure Search .NET SDK는 .NET Framework 4.6 및 .NET Core를 대상으로 하는 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="9cc2c-130">핵심 시나리오</span><span class="sxs-lookup"><span data-stu-id="9cc2c-130">Core scenarios</span></span>
<span data-ttu-id="9cc2c-131">검색 응용 프로그램에서 수행해야 할 몇 가지 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="9cc2c-132">이 자습서에서는 이러한 핵심 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="9cc2c-133">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc2c-133">Creating an index</span></span>
* <span data-ttu-id="9cc2c-134">문서를 사용하여 인덱스 채우기</span><span class="sxs-lookup"><span data-stu-id="9cc2c-134">Populating the index with documents</span></span>
* <span data-ttu-id="9cc2c-135">전체 텍스트 검색 및 필터를 사용하여 문서 검색하기</span><span class="sxs-lookup"><span data-stu-id="9cc2c-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="9cc2c-136">이들 각각을 설명하는 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="9cc2c-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="9cc2c-137">사용자 응용 프로그램에서 코드 조각을 자유롭게 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="9cc2c-138">개요</span><span class="sxs-lookup"><span data-stu-id="9cc2c-138">Overview</span></span>
<span data-ttu-id="9cc2c-139">"호텔"이라는 이름의 새로운 인덱스를 탐색하려는 샘플 응용 프로그램은 몇몇 문서로 채운 다음, 일부 검색 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="9cc2c-140">전체 흐름을 보여주는 주 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="9cc2c-141">[GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)에서 이 연습에 사용된 샘플 응용 프로그램의 전체 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="9cc2c-142">단계별로 연습해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-142">We'll walk through this step by step.</span></span> <span data-ttu-id="9cc2c-143">먼저 새로운 `SearchServiceClient`을(를) 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="9cc2c-144">이 개체를 통해 인덱스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="9cc2c-145">하나를 생성하기 위해 Azure 검색 서비스 이름과 관리 API 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="9cc2c-146">[샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)의 `appsettings.json` 파일에 이 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="9cc2c-147">잘못된 키(예, 관리 키가 필요한 쿼리 키)를 제공하는 경우, `SearchServiceClient`은(는) `Indexes.Create`와(과) 같은 작업 메서드를 처음 호출하면 "사용할 수 없음"이라는 오류 메시지와 함께 `CloudException`을(를) 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="9cc2c-148">이 경우 API 키를 다시 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="9cc2c-149">다음 몇 줄은 "호텔"이라는 인덱스를 만드는 메서드를 호출하며, 이미 있는 경우 이를 먼저 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="9cc2c-150">잠시 후 이들 메서드를 연습해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="9cc2c-151">그런 다음 인덱스를 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="9cc2c-152">이를 위해서는 `SearchIndexClient`이(가) 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="9cc2c-153">두 가지 방법 즉, 키를 생성하거나 `SearchServiceClient`에서 `Indexes.GetClient`을(를) 호출하여 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="9cc2c-154">편의를 위해 후자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="9cc2c-155">일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="9cc2c-156">`Indexes.GetClient`는 다른 `SearchCredentials`를 제공하는 문제를 피할 수 있으므로 인덱스를 생성하기에 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="9cc2c-157">이는 새 `SearchIndexClient`에 `SearchServiceClient`을(를) 만드는 데 사용하는 관리 키를 눌러 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="9cc2c-158">그러나 쿼리를 실행하는 일부 응용 프로그램의 경우, `SearchIndexClient` 을(를) 직접 만들어 관리 키 대신에 쿼리 키에서 전달하는 것이 더 낫습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="9cc2c-159">이는 최소 권한의 원칙와 일치하고 응용 프로그램을 더욱 안전하게 하는데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="9cc2c-160">관리 키와 쿼리 키에 대한 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="9cc2c-161">이제 `SearchIndexClient`이 생겼고 인덱스를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="9cc2c-162">이것은 나중에 연습할 또 다른 메서드에 의해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="9cc2c-163">마지막으로 몇 가지 검색 쿼리를 실행하고 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="9cc2c-164">이번에는 다른 `SearchIndexClient`를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="9cc2c-165">`RunQueries` 메서드에 대해서는 이후에 좀 더 자세히 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="9cc2c-166">다음은 새 `SearchIndexClient`를 만드는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="9cc2c-167">이번에는 인덱스에 대해 쓰기 액세스 권한이 필요하지 않으므로 쿼리 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="9cc2c-168">[샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)의 `appsettings.json` 파일에 이 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="9cc2c-169">유효한 서비스 이름 및 API 키로 이 응용 프로그램을 실행하는 경우, 출력은 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
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
    
    Complete.  Press any key to end application...

<span data-ttu-id="9cc2c-170">응용 프로그램의 전체 소스 코드는이 문서의 마지막 부분에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="9cc2c-171">다음으로, `Main`에 의해 호출된 각 메서드를 좀더 자세히 살펴볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="9cc2c-172">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc2c-172">Creating an index</span></span>
<span data-ttu-id="9cc2c-173">`SearchServiceClient`을(를) 만든 후, `Main`이(가) 하는 다음 일은 이미 있는 "호텔" 인덱스를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="9cc2c-174">작업은 다음과 같은 메서드로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="9cc2c-175">이 메서드는 주어진 `SearchServiceClient` 을(를) 사용하여 인덱스가 존재하는지 확인하고 존재하면 이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-176">이 문서의 예제 코드는 간단히 하기 위해 Azure 검색.NET SDK의 동기 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="9cc2c-177">확장성과 응답성이 유지하기 위해 사용 중인 응용 프로그램에서 비동기 메서드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="9cc2c-178">예를 들어, 위의 메서드의 경우 `Exists` 및 `Delete` 대신`ExistsAsync` 및 `DeleteAsync`을(를) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="9cc2c-179">그 다음 `Main`이(가) 이 메서드를 호출하여 새 "호텔" 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="9cc2c-180">이 메서드는 새 인덱스의 스키마를 정의하는 `Field` 개체 목록과 함께 새 `Index` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="9cc2c-181">각 필드에는 이름, 데이터 유형, 그리고 검색 동작을 정의하는 몇 가지 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="9cc2c-182">`FieldBuilder` 클래스는 리플렉션을 사용하여 지정된 `Hotel` 모델 클래스의 public 속성 및 특성을 검사하고 인덱스에 대한 `Field` 개체 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="9cc2c-183">`Hotel` 클래스에 대해서는 이후에 좀 더 자세히 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-184">필요한 경우 `FieldBuilder`를 사용하는 대신, `Field` 개체 목록을 항상 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="9cc2c-185">예를 들어 모델 클래스를 사용하지 않으려고 하거나, 특성을 추가하여 수정하지 않으려는 기존 모델 클래스를 사용해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="9cc2c-186">필드 외에도, 점수 매기기 프로필, 서제스터 또는 CORS 옵션을 인덱스에 추가할 수도 있습니다(이들 필드는 간단하게 나타내기 위해 샘플에서 생략됩니다).</span><span class="sxs-lookup"><span data-stu-id="9cc2c-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="9cc2c-187">[SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)뿐만 아니라 [Azure Search REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)에서 인덱스 개체와 그 구성 요소에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="9cc2c-188">인덱스 채우기</span><span class="sxs-lookup"><span data-stu-id="9cc2c-188">Populating the index</span></span>
<span data-ttu-id="9cc2c-189">`Main` 의 다음 단계는 새로 만든 인덱스를 채우는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="9cc2c-190">이것은 다음 메서드로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-190">This is done in the following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

<span data-ttu-id="9cc2c-191">이 메서드는 네 부분으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-191">This method has four parts.</span></span> <span data-ttu-id="9cc2c-192">첫 번째 부분은 입력 데이터를 인덱스에 업로드할 때 사용되는 다양한 `Hotel` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="9cc2c-193">이 데이터는 간단히 하기 위해 하드 코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="9cc2c-194">사용 중인 응용 프로그램의 경우, 데이터는 SQL 데이터베이스와 같은 외부 데이터 원본에서 나올 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="9cc2c-195">두 번째 부분은 문서를 포함하는 `IndexBatch`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="9cc2c-196">배치를 만들 때 배치에 적용할 작업을 지정합니다. 이 경우에는 `IndexBatch.Upload`를 호출하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="9cc2c-197">그런 다음 `Documents.Index` 메서드를 통해 Azure 검색 인덱스에 일괄적으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-198">이 예에서는 문서를 업로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="9cc2c-199">변경 사항을 기존 문서에 병합하거나 문서를 삭제하려면 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` 또는 `IndexBatch.Delete`를 호출하여 배치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="9cc2c-200">`IndexBatch.New`를 호출하여 단일 배치 내에 다른 작업들을 혼합할 수 있으며, 이것은 `IndexAction` 개체 컬렉션을 사용하고, 이들 각각은 Azure 검색이 문서의 특정 작업을 수행하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="9cc2c-201">`IndexAction.Merge`, `IndexAction.Upload` 등을 비롯한 해당 메서드를 호출하여 각 `IndexAction`과 자체 작업을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="9cc2c-202">이 메서드의 세 번째 부분은 인덱싱에 중요한 오류 사례를 처리하는 catch 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="9cc2c-203">Azure 검색 서비스가 일괄 처리에서 문서 일부를 인덱싱하는데 실패하는 경우 `Documents.Index`에 의해 `IndexBatchException`이(가) 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="9cc2c-204">이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="9cc2c-205">**이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cc2c-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="9cc2c-206">실패한 문서 인덱싱을 잠시 후 다시 시도하거나, 샘플에서 하던 것처럼 기록하여 계속하거나, 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-207">`FindFailedActionsToRetry` 메서드를 사용하여 이전 `Index` 호출에서 실패한 작업만 포함하는 새 일괄 처리를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="9cc2c-208">이 메서드에 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_)에 설명되어 있으며, 이 메서드를 [StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)에서 적절히 사용하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="9cc2c-209">마지막으로, `UploadDocuments` 메서드가 2초 동안 지연됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="9cc2c-210">Azure 검색 서비스에서 인덱싱이 비동기적으로 발생하기 때문에, 샘플 응용 프로그램은 문서 검색을 위해 잠시 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="9cc2c-211">이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="9cc2c-212">.NET SDK가 문서를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cc2c-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="9cc2c-213">Azure 검색.NET SDK가 어떻게 `Hotel` 와(과) 같은 사용자 정의 클래스의 인스턴스를 업로드할 수 있는지 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="9cc2c-214">이 질문에 대답하기 위해 `Hotel` 클래스를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

<span data-ttu-id="9cc2c-215">먼저 주목할 것은 `Hotel`의 각 공용 속성이 인덱스 정의의 필드와 일치하지만 한 가지 중요한 차이가 있습니다. 각 필드의 이름은 소문자("카멜식 대/소문자")로 시작하지만, `Hotel`의 각 공용 속성 이름은 대문자 문자("파스칼식 대/소문자")로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="9cc2c-216">이것은 대상 스키마가 응용 프로그램 개발자의 제어 범위를 벗어난 데이터 바인딩을 수행하는 .NET 응용 프로그램의 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="9cc2c-217">카멜식 대/소문자 속성으로 이름을 지정하면 .NET 이름 지정 지침을 위반하지 않고 속성 이름을 자동으로 `[SerializePropertyNamesAsCamelCase]` 특성을 지닌 카멜식 대/소문자에 매핑하도록 SDK에 명령할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-218">Azure 검색 .NET SDK는 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리를 사용하여 사용자 지정 모델 개체를 JSON과 직렬화 및 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="9cc2c-219">필요한 경우 직렬화를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="9cc2c-220">자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](#JsonDotNet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="9cc2c-221">두 번째로 유의할 사항은 `IsFilterable`, `IsSearchable`, `Key` 및 `Analyzer`와 같이 각 public 속성을 데코레이트하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="9cc2c-222">이러한 특성은 [Azure Search 인덱스의 해당 특성](https://docs.microsoft.com/rest/api/searchservice/create-index#request)에 직접 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="9cc2c-223">`FieldBuilder` 클래스는 이러한 특성을 사용하여 인덱스에 대한 필드 정의를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="9cc2c-224">`Hotel` 클래스에 대해 세 번째로 중요한 부분은 public 속성의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="9cc2c-225">이러한 속성의 .NET 유형은 인덱스 정의의 동등한 필드 유형에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="9cc2c-226">예를 들어, `Category` 문자열 속성은 `Edm.String` 유형인 `category` 필드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="9cc2c-227">`bool?` 및 `Edm.Boolean`, `DateTimeOffset?` 및 `Edm.DateTimeOffset` 사이에는 유사한 유형 매핑이 있습니다. 유형 매핑에 대한 특정 규칙은 [Azure Search .NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)에 `Documents.Get` 메서드로 문서화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="9cc2c-228">`FieldBuilder` 클래스는 사용자를 위해 이러한 매핑을 처리하는 역할을 하지만 serialization 문제를 해결해야 하는 경우에도 알아두면 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="9cc2c-229">사용자의 클래스를 문서로서 사용하는 이 능력은 양방향으로 사용 가능합니다. 또한 다음 섹션에서 확인할 수 있듯이 검색 결과를 검색하고 이 검색 결과를 SDK가 자동으로 사용자가 선택한 유형으로 역직렬화하도록 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-230">Azure 검색.NET SDK는 필드 이름을 필드 값에 매핑하는 키/값인 `Document` 클래스를 사용하여 동적 유형의 문서도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="9cc2c-231">디자인 타임에서 인덱스 스키마를 알 수 없거나 특정 모델 클래스에 바인딩하기 불편한 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="9cc2c-232">문서를 처리하는 SDK의 모든 메서드에는 `Document` 클래스와 연동하는 오버로드와 제네릭 유형 매개 변수를 취하는 강력한 유형의 오버로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="9cc2c-233">이 자습서의 샘플 코드에서는 후자만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="9cc2c-234">`Document` 클래스는 `Dictionary<string, object>`에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="9cc2c-235">자세한 내용은 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="9cc2c-236">**Null 허용 데이터 형식을 사용해야 하는 이유**</span><span class="sxs-lookup"><span data-stu-id="9cc2c-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="9cc2c-237">고유의 모델 클래스를 Azure 검색 인덱스에 매핑하도록 설계하는 경우 `bool` 및 `int` 등과 같은 값 유형의 속성을 Null이 허용되도록 선언하는 것이 좋습니다(예: `bool` 대신 `bool?`).</span><span class="sxs-lookup"><span data-stu-id="9cc2c-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="9cc2c-238">Null이 허용되지 않는 속성을 사용하는 경우 인덱스의 문서가 해당 필드에 대해 Null 값을 포함하지 않도록 **보장** 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="9cc2c-239">SDK와 Azure 검색 서비스 모두 이를 적용하는 데 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="9cc2c-240">이것은 가상의 문제가 아닙니다. `Edm.Int32` 형식인 기존 인덱스에 새 필드를 추가하는 시나리오를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="9cc2c-241">인덱스 정의를 업데이트한 후 모든 문서는 해당하는 새 필드에 대해 Null 값을 포함하게 됩니다(Azure 검색에서 모든 형식은 Null을 허용하기 때문).</span><span class="sxs-lookup"><span data-stu-id="9cc2c-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="9cc2c-242">그런 다음 해당 필드에 대해 Null이 허용되지 않는 `int` 속성으로 모델 클래스를 사용하는 경우 문서를 검색하려고 시도할 때 다음과 같은 `JsonSerializationException`이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="9cc2c-243">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="9cc2c-244">JSON.NET으로 직렬화 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9cc2c-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="9cc2c-245">이 SDK는 문서를 직렬화 및 역직렬화하는 데 JSON.NET을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="9cc2c-246">사용자 고유의 `JsonConverter` 또는 `IContractResolver`를 정의하여 필요한 경우 직렬화 및 역직렬화를 사용자 지정할 수 있습니다(자세한 내용은 [JSON.NET 설명서](http://www.newtonsoft.com/json/help/html/Introduction.htm) 참조).</span><span class="sxs-lookup"><span data-stu-id="9cc2c-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="9cc2c-247">이 기능은 Azure 검색에 사용할 응용 프로그램에서 기존 모델 클래스를 적용하려는 경우와 기타 고급 시나리오에서 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="9cc2c-248">예를 들어 사용자 지정 serialization으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="9cc2c-249">모델 클래스의 특정 속성을 문서 필드로 저장하는 데 포함 또는 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="9cc2c-250">코드의 속성 이름과 인덱스의 필드 이름을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="9cc2c-251">문서 필드에 속성에 매핑하는 데 사용할 수 있는 사용자 지정 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="9cc2c-252">GitHub에서 Azure 검색 .NET SDK에 대한 단위 테스트에서 사용자 지정 serialization을 구현하는 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="9cc2c-253">적절한 시작 지점은 [이 폴더](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="9cc2c-254">여기에는 사용자 지정 serialization 테스트에 사용되는 클래스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="9cc2c-255">인덱스에서 문서 검색</span><span class="sxs-lookup"><span data-stu-id="9cc2c-255">Searching for documents in the index</span></span>
<span data-ttu-id="9cc2c-256">샘플 응용 프로그램의 마지막 단계는 인덱스의 일부 문서를 검색하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="9cc2c-257">다음 메서드가 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

<span data-ttu-id="9cc2c-258">쿼리를 실행할 때마다 이 메서드는 먼저 새 `SearchParameters` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="9cc2c-259">이는 정렬, 필터링, 페이징, 패시팅 같은 쿼리에 대한 추가 옵션을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="9cc2c-260">이 메서드에서 다른 쿼리에 대해 `Filter`, `Select`, `OrderBy` 및 `Top` 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="9cc2c-261">모든 `SearchParameters` 속성은 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="9cc2c-262">다음 단계를 실제로 검색 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="9cc2c-263">이는 `Documents.Search` 메서드를 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="9cc2c-264">각 쿼리에 대해 문자열(또는 검색 텍스트가 없는 경우 `"*"`)로 사용할 검색 텍스트와 앞서 만든 검색 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="9cc2c-265">또한 SDK에 검색 결과 내 문서를 `Hotel` 유형의 개체로 역직렬화하도록 명령하는 `Documents.Search`에 대한 유형 매개 변수로 `Hotel`을(를) 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc2c-266">검색 쿼리 식 구문에 대한 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="9cc2c-267">마지막으로, 각 쿼리 후에 이 메서드는 검색 결과에서 일치하는 모든 항목을 반복하여 각 문서를 콘솔에 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="9cc2c-268">이러한 각 쿼리를 차례대로 조금 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="9cc2c-269">첫 번째 쿼리를 실행하는 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="9cc2c-270">이 경우 단어 "budget"과 일치하는 호텔을 검색하고 있으며 `Select` 매개 변수로 지정된 호텔 이름만 표시하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="9cc2c-271">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="9cc2c-272">다음에는 숙박 요율이 150달러 미만인 호텔을 찾은 후 호텔 ID와 설명만 반환하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="9cc2c-273">이 쿼리는 OData `$filter` 식 `baseRate lt 150`을 사용하여 인덱스의 문서를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="9cc2c-274">Azure 검색이 지원하는 OData 구문에 대한 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="9cc2c-275">다음은 쿼리 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="9cc2c-276">다음에는 가장 최근에 리모델링한 상위 두 개 호텔을 찾은 후 호텔 이름 및 마지막 보수 날짜를 표시하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="9cc2c-277">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-277">Here is the code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="9cc2c-278">이 경우 OData 구문을 다시 사용하여 `OrderBy` 매개 변수를 `lastRenovationDate desc`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="9cc2c-279">또한 `Top`을 2로 설정하여 상위 2개의 문서만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="9cc2c-280">앞에서 나온 것처럼 `Select`를 설정하여 반환할 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="9cc2c-281">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="9cc2c-282">마지막으로 단어 "motel"과 일치하는 모든 호텔을 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="9cc2c-283">결과는 다음과 같습니다. 여기서는 `Select` 속성을 지정하지 않았으므로 모든 필드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="9cc2c-284">이 단계에서 자습서를 완료하지만 여기서 멈추지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="9cc2c-285">**다음 단계** 에서는 Azure 검색에 대해 자세히 학습하기 위한 추가 리소스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc2c-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cc2c-286">Next steps</span></span>
* <span data-ttu-id="9cc2c-287">[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 및 [REST API](https://docs.microsoft.com/rest/api/searchservice/)에 대한 참고 자료를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="9cc2c-288">[비디오와 기타 샘플 및 자습서](search-video-demo-tutorial-list.md)를 통해 지식을 심화시키십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="9cc2c-289">[명명 규칙](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) 을 검토하여 다양한 개체 명명에 대한 규칙에 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="9cc2c-290">Azure 검색에서 [지원되는 데이터 유형](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 을 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc2c-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
