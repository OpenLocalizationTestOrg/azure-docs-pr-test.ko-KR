---
title: ".NET 응용 프로그램에서 Azure 검색 aaaHow toouse | Microsoft Docs"
description: ".NET 응용 프로그램에서 toouse Azure 검색 하는 방법"
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
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="1a1a2-103">.NET 응용 프로그램에서 toouse Azure 검색 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1a1a2-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="1a1a2-104">이 문서는 연습 tooget hello로 실행 하면 [Azure 검색.NET SDK](https://aka.ms/search-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="1a1a2-105">다양 한 기능의 hello.NET SDK tooimplement를 사용할 수 있습니다 Azure 검색을 사용 하 여 응용 프로그램에서 경험을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="1a1a2-106">무엇이 hello Azure 검색 SDK</span><span class="sxs-lookup"><span data-stu-id="1a1a2-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="1a1a2-107">hello SDK 이루어져 클라이언트 라이브러리 `Microsoft.Azure.Search`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="1a1a2-108">인덱스, 데이터 원본 및 인덱서 toomanage 있습니다를 사용 하면으로 업로드 및 문서를 관리 하 고 HTTP 및 JSON hello 세부 정보와 함께 toodeal 필요 없이 모든 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="1a1a2-109">hello 클라이언트 라이브러리와 같은 클래스를 정의 `Index`, `Field`, 및 `Document`뿐만 아니라 등의 작업 `Indexes.Create` 및 `Documents.Search` hello에 `SearchServiceClient` 및 `SearchIndexClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="1a1a2-110">이러한 클래스는 hello 네임 스페이스를 다음으로 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="1a1a2-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="1a1a2-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="1a1a2-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="1a1a2-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="1a1a2-113">hello 현재 버전의 Azure 검색.NET SDK hello 일반적으로 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="1a1a2-114">Tooprovide 피드백 원하는 경우 우리 tooincorporate hello 다음 버전의를 참조 하십시오 우리의 [피드백 페이지](https://feedback.azure.com/forums/263029-azure-search/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="1a1a2-115">hello.NET SDK 버전을 지원 `2016-09-01` 의 hello [Azure 검색 REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="1a1a2-116">이 버전에서 이제 사용자 지정 분석기와 Azure Blob 및 Azure 테이블 인덱서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="1a1a2-117">미리 보기 기능이 있는 *하지* JSON 및 CSV 파일에 대 한 지원 등이 버전의 일부에 있는 [미리 보기](search-api-2015-02-28-preview.md) 되 고 이전 hello를 통해 사용 가능한 [2.0-미리 보기 버전의.NET SDK hello ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="1a1a2-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="1a1a2-118">이 SDK는 Search 서비스 생성 및 확장, API 키 관리 등의 [관리 작업](https://docs.microsoft.com/rest/api/searchmanagement/)을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="1a1a2-119">.NET 응용 프로그램에서 리소스를 검색 toomanage 해야 할 경우 hello를 사용할 수 있습니다 [Azure 검색.NET 관리 SDK](https://aka.ms/search-mgmt-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="1a1a2-120">Toohello hello SDK의 최신 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="1a1a2-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="1a1a2-121">이전 버전의 hello Azure 검색.NET SDK를 이미 사용 중이 고 tooupgrade toohello 새 일반 공급 버전을 선택 하는 경우 [이 문서](search-dotnet-sdk-migration.md) 설명 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="1a1a2-122">Hello SDK에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="1a1a2-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="1a1a2-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="1a1a2-124">Azure 검색 서비스</span><span class="sxs-lookup"><span data-stu-id="1a1a2-124">Your own Azure Search service.</span></span> <span data-ttu-id="1a1a2-125">순서 toouse hello SDK, 서비스의 hello 이름과 API 키를 하나 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="1a1a2-126">[Hello 포털에 서비스를 만들](search-create-service-portal.md) 이러한 단계를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="1a1a2-127">Hello Azure 검색.NET SDK를 다운로드 [NuGet 패키지](http://www.nuget.org/packages/Microsoft.Azure.Search) Visual Studio에서 "NuGet 패키지 관리"를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="1a1a2-128">방금 hello 패키지 이름에 대 한 검색 `Microsoft.Azure.Search` NuGet.org에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="1a1a2-129">Azure 검색.NET SDK hello hello.NET Framework 4.6 및.NET Core를 대상으로 하는 응용 프로그램을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="1a1a2-130">핵심 시나리오</span><span class="sxs-lookup"><span data-stu-id="1a1a2-130">Core scenarios</span></span>
<span data-ttu-id="1a1a2-131">몇 가지 방법으로 toodo 검색 응용 프로그램에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="1a1a2-132">이 자습서에서는 이러한 핵심 시나리오를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="1a1a2-133">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="1a1a2-133">Creating an index</span></span>
* <span data-ttu-id="1a1a2-134">문서와 함께 hello 인덱스 채우기</span><span class="sxs-lookup"><span data-stu-id="1a1a2-134">Populating hello index with documents</span></span>
* <span data-ttu-id="1a1a2-135">전체 텍스트 검색 및 필터를 사용하여 문서 검색하기</span><span class="sxs-lookup"><span data-stu-id="1a1a2-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="1a1a2-136">hello 다음 예제 코드에서는 이러한 각 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="1a1a2-137">사용자의 응용 프로그램에서 무료 toouse hello 코드 조각을 느낍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="1a1a2-138">개요</span><span class="sxs-lookup"><span data-stu-id="1a1a2-138">Overview</span></span>
<span data-ttu-id="1a1a2-139">hello 살펴보겠습니다 샘플 응용 프로그램에서는 새 "호텔" 라는 인덱스 몇 가지 문서와 함께 정보를 표시 한 후 일부 검색 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="1a1a2-140">다음을 보여 주는 hello 주 프로그램은 전체 흐름 hello:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="1a1a2-141">이 연습 과정에서 사용 되는 hello 샘플 응용 프로그램의 hello 전체 소스 코드를 찾을 수 [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="1a1a2-142">단계별로 연습해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-142">We'll walk through this step by step.</span></span> <span data-ttu-id="1a1a2-143">먼저 새 toocreate 해야 `SearchServiceClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="1a1a2-144">이 개체 toomanage 인덱스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="1a1a2-145">하나 순서 tooconstruct, Azure 검색 서비스 이름 뿐만 아니라 관리자 API 키 tooprovide 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="1a1a2-146">Hello에이 정보를 입력할 수 있습니다 `appsettings.json` 파일의 hello [샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="1a1a2-147">잘못 된 키 (예를 들어 관리자 키가 필요 하는 쿼리 키)를 제공 하는 경우 hello `SearchServiceClient` throw 됩니다는 `CloudException` hello 오류 메시지 "금지 된" hello로 처음으로 작업에서 메서드를 호출,와 같은 `Indexes.Create`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="1a1a2-148">이런 경우가 발생 tooyou 우리의 API 키를 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="1a1a2-149">hello 다음 몇 줄만 작성 호출 메서드 toocreate 이미 있는 경우 먼저 삭제 "호텔" 라는 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="1a1a2-150">잠시 후 이들 메서드를 연습해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="1a1a2-151">다음으로 hello 인덱스 toobe 채워져 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="1a1a2-152">toodo이 필요 합니다는 `SearchIndexClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="1a1a2-153">하나는 두 가지 방법 tooobtain 가지:를 호출 하거나, 구성 하 여 `Indexes.GetClient` hello에 `SearchServiceClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="1a1a2-154">후자의 hello 편의 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="1a1a2-155">일반적인 검색 응용 프로그램에서 인덱스 관리 및 채우기는 검색 쿼리와는 별도의 구성 요소에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="1a1a2-156">`Indexes.GetClient`저장 하기 때문에 인덱스를 채우는 편리한 다른를 제공 하는 데 문제가 hello `SearchCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="1a1a2-157">해당 하면 사용한 toocreate hello hello 관리자 키를 전달 하 여 이렇게 `SearchServiceClient` 새 toohello `SearchIndexClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="1a1a2-158">그러나 쿼리를 실행 하는 응용 프로그램 부분에서는 hello, 것이 더 나은 toocreate hello `SearchIndexClient` 직접 관리자 키 대신 쿼리 키에 전달할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="1a1a2-159">최소 권한의 원칙 hello와 일치 하 고 toomake 보다 안전한 응용 프로그램 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="1a1a2-160">관리 키와 쿼리 키에 대한 자세한 내용은 [여기](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="1a1a2-161">이제는 `SearchIndexClient`, hello 인덱스를 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="1a1a2-162">이것은 나중에 연습할 또 다른 메서드에 의해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="1a1a2-163">마지막으로, 몇 가지 검색 쿼리를 실행 하 고 hello 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="1a1a2-164">이번에는 다른 `SearchIndexClient`를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="1a1a2-165">이전 걸립니다 좀 더 자세히 살펴보고 hello `RunQueries` 나중 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="1a1a2-166">여기서는 hello 코드 toocreate hello 새 `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="1a1a2-167">이 시간 사용은 쿼리 키 이후 쓰기 액세스 toohello 인덱스가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="1a1a2-168">Hello에이 정보를 입력할 수 있습니다 `appsettings.json` 파일의 hello [샘플 응용 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="1a1a2-169">올바른 서비스 이름 및 API 키 사용이 응용 프로그램을 실행 하는 경우 hello 출력은 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="1a1a2-170">hello 응용 프로그램의 hello 전체 소스 코드는이 문서의 hello 끝에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="1a1a2-171">다음으로, 각 hello 메서드에 의해 호출 자세히 보기 메뉴로 이동 합니다 `Main`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="1a1a2-172">인덱스 만들기</span><span class="sxs-lookup"><span data-stu-id="1a1a2-172">Creating an index</span></span>
<span data-ttu-id="1a1a2-173">만든 후는 `SearchServiceClient`, hello 다음으로 `Main` 가 이미 있는 경우에 delete 호텔"hello" 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="1a1a2-174">작업은 hello 메서드 뒤에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="1a1a2-175">이 방법은 제공 하는 hello를 사용 하 여 `SearchServiceClient` toocheck hello 인덱스가 있는 경우 그리고 있다면 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-176">hello 예제 코드에서는이 문서에 간단한 설명을 위해 hello Azure 검색.NET SDK의 hello 동기 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="1a1a2-177">사용자 고유의 응용 프로그램 tookeep에 hello 비동기 메서드를 사용 하는 것이 좋습니다 확장성과 응답성이 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="1a1a2-178">예를 들어 hello 있습니다 위의 메서드에서 사용 하 여 `ExistsAsync` 및 `DeleteAsync` 대신 `Exists` 및 `Delete`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="1a1a2-179">그 다음 `Main`이(가) 이 메서드를 호출하여 새 "호텔" 인덱스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="1a1a2-180">이 메서드가 만드는 새 `Index` 개체 목록이 `Field` hello 새 인덱스의 hello 스키마를 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="1a1a2-181">각 필드에는 이름, 데이터 유형, 그리고 검색 동작을 정의하는 몇 가지 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="1a1a2-182">hello `FieldBuilder` 클래스가 사용 하 여 리플렉션 toocreate 목록이 `Field` 제공 hello의 공용 속성 및 특성 개체를 검사 하 여 hello 인덱스에 대 한 hello `Hotel` 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="1a1a2-183">좀 더 자세히 살펴보고 hello 살펴보겠습니다 `Hotel` 나중에 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-184">항상 hello 목록을 만들 수 있습니다 `Field` 개체를 사용 하는 대신 직접 `FieldBuilder` 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="1a1a2-185">예를 들어 toouse 모델 클래스를 원하지 않을 수 있습니다 또는 toouse 않도록 toomodify 특성을 추가 하 여 기존 모델 클래스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="1a1a2-186">또한 toofields를 추가할 수 있습니다도 점수 매기기 프로필, 확인 기, 또는 CORS 옵션 toohello 인덱스 (이러한 메서드 hello 샘플 코드에서 생략 됩니다).</span><span class="sxs-lookup"><span data-stu-id="1a1a2-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="1a1a2-187">Hello에 hello Index 개체 및 해당 구성 요소에 대 한 자세한 정보를 찾을 수 [SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index)뿐만 아니라 hello 에서처럼에서 [Azure 검색 REST API 참조](https://docs.microsoft.com/rest/api/searchservice/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="1a1a2-188">Hello 인덱스 채우기</span><span class="sxs-lookup"><span data-stu-id="1a1a2-188">Populating hello index</span></span>
<span data-ttu-id="1a1a2-189">다음 단계를 hello `Main` toopopulate hello 새로 만든 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="1a1a2-190">이 메서드를 다음 hello 작업 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-190">This is done in hello following method:</span></span>

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
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

<span data-ttu-id="1a1a2-191">이 메서드는 네 부분으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-191">This method has four parts.</span></span> <span data-ttu-id="1a1a2-192">hello 먼저 이루어진 배열을 만들어 `Hotel` 우리의 입력된 데이터 tooupload toohello 인덱스 역할을 수행 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="1a1a2-193">이 데이터는 간단히 하기 위해 하드 코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="1a1a2-194">사용 중인 응용 프로그램의 경우, 데이터는 SQL 데이터베이스와 같은 외부 데이터 원본에서 나올 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="1a1a2-195">두 번째 부분 hello 만듭니다는 `IndexBatch` hello 문서가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="1a1a2-196">Hello 작업,이 경우 호출 하 여 만든 hello 시 tooapply toohello 일괄 처리를 원하는 지정 `IndexBatch.Upload`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="1a1a2-197">hello 일괄 처리는 hello 여 업로드 된 toohello Azure 검색 인덱스 다음 `Documents.Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-198">이 예에서는 문서를 업로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="1a1a2-199">Toomerge 기존 문서 또는 문서 삭제 포인터가 필요한 경우 일괄 처리를 호출 하 여 일으킬 `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, 또는 `IndexBatch.Delete` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="1a1a2-200">또한 호출 하 여 단일 일괄 처리의 다른 작업을 혼합할 수 있습니다 `IndexBatch.New`, 컬렉션을 사용 하는 `IndexAction` Azure 검색 tooperform를 지시 하며 각 문서에 특정 작업 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="1a1a2-201">각각 만들 수 있습니다 `IndexAction` 와 같은 hello 해당 메서드를 호출 하 여 자체 작업과 `IndexAction.Merge`, `IndexAction.Upload`등입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="1a1a2-202">이 메서드의 세 번째 부분은 hello는 인덱싱에 대 한 중요 한 오류 사례를 처리 하는 catch 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="1a1a2-203">Azure 검색 서비스 tooindex hello의 일부 문서 hello 일괄 처리에 실패 하는 경우는 `IndexBatchException` 가 throw `Documents.Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="1a1a2-204">이는 부하가 높은 상태에서 서비스되는 동안에 문서를 인덱싱하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="1a1a2-205">**이 경우 코드에서 명시적으로 처리하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="1a1a2-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="1a1a2-206">지연 하 고, 실패 인덱싱 hello 문서를 다시 시도 하십시오 또는 로그 hello 예제에서는 하거나 응용 프로그램의 데이터 일관성 요구 사항에 따라 다른 작업을 수행할 수 있습니다를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-207">Hello를 사용할 수 있습니다 `FindFailedActionsToRetry` 메서드 tooconstruct 포함 하는 새 일괄 처리에만 너무 한 이전 호출에 실패 한 작업 hello`Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="1a1a2-208">hello 메서드는 문서화 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) tooproperly 사용 하는 방법에 대 한 내용은 이며 [StackOverflow에](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="1a1a2-209">마지막으로, hello `UploadDocuments` 2 초에 대 한 메서드 지연이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="1a1a2-210">인덱싱 발생 비동기적으로 Azure 검색 서비스에 hello 샘플 응용 프로그램 toowait hello 문서는 검색에 사용할 수 있는 짧은 시간 tooensure 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="1a1a2-211">이와 같이 데모, 테스트, 샘플 응용 프로그램에서는 일반적으로 지연만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="1a1a2-212">Hello.NET SDK에서 문서를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1a1a2-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="1a1a2-213">Hello Azure 검색.NET SDK와 같은 사용자 정의 클래스의 인스턴스 수 tooupload은 어떻게 할까요 `Hotel` toohello 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="1a1a2-214">toohelp 해당 질문에 답변을 사용 hello `Hotel` 클래스:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
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

<span data-ttu-id="1a1a2-215">hello 먼저 toonotice은 각 public 속성의 `Hotel` tooa 필드 hello 인덱스 정의의 하지만 한 가지 중요 한 차이점은 해당: hello 이름은 각 공용 동안 소문자 ("카멜식 대 /")으로 시작 하는 각 필드의 hello 이름 속성의 `Hotel` 대문자 문자 ("파스칼식 대 / 소문자로")로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="1a1a2-216">여기서 hello 대상 스키마는 hello 응용 프로그램 개발자의 외부 hello 제어 데이터 바인딩을 수행 하는.NET 응용 프로그램에서 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="1a1a2-217">속성 이름은 카멜식 대 / 소문자를 늘려 명명 지침 tooviolate hello.NET 대신 hello SDK toomap hello 속성 이름은 toocamel 사례 hello로 자동으로 알 수 있습니다 `[SerializePropertyNamesAsCamelCase]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-218">Azure 검색.NET SDK hello hello를 사용 하 여 [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) 라이브러리 tooserialize 하 고 사용자 사용자 지정 모델 개체 tooand JSON에서 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="1a1a2-219">필요한 경우 직렬화를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="1a1a2-220">자세한 내용은 [JSON.NET으로 직렬화 사용자 지정](#JsonDotNet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="1a1a2-221">hello 두 번째 작업 toonotice hello 특성 같은 `IsFilterable`, `IsSearchable`, `Key`, 및 `Analyzer` 각 공용 속성이 있는 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="1a1a2-222">이러한 특성 매핑 toohello 직접 [hello Azure 검색 인덱스의 해당 특성](https://docs.microsoft.com/rest/api/searchservice/create-index#request)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="1a1a2-223">hello `FieldBuilder` 클래스가 이러한 tooconstruct 필드 정의 사용 하 여 hello 인덱스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="1a1a2-224">hello에 대 한 세 번째 중요 한 사항은 hello `Hotel` 클래스는 hello 공용 속성의 hello 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="1a1a2-225">이러한 속성의 hello.NET 형식은 hello 인덱스 정의의 해당 필드 형식을 tootheir 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="1a1a2-226">예를 들어 hello `Category` 문자열 속성 매핑됩니다 toohello `category` 형식인 필드 `Edm.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="1a1a2-227">간의 비슷한 형식 매핑을 `bool?` 및 `Edm.Boolean`, `DateTimeOffset?` 및 `Edm.DateTimeOffset`, 등 hello hello 형식 매핑에 대 한 특정 규칙 hello로 사항은 `Documents.Get` hello에 대 한 메서드 [Azure 검색.NET SDK 참조](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="1a1a2-228">hello `FieldBuilder` 클래스를이 매핑의 담당 것은 아니지만 수 여전히 도움이 toounderstand serialization 문제 tootroubleshoot 해야 할 경우.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="1a1a2-229">이 기능은 toouse 양방향;에서 작동 하는 문서로 서 사용자 고유의 클래스 또한 검색 결과 검색 하 고 수 hello SDK 자동으로 형식을 역직렬화 할에 tooa의 선택한 hello 다음 섹션에 나와 있듯이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-230">hello Azure 검색.NET SDK에서는 hello를 사용 하 여 동적으로 입력 문서 `Document` 필드 이름 toofield 값의 키/값 매핑이 설정 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="1a1a2-231">이 hello 인덱스 스키마 디자인 타임에 알 수 없는 하거나는 것이 불편 toobind toospecific 모델 클래스 시나리오에서 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="1a1a2-232">Hello SDK의에서 문서를 처리 하는 모든 hello 메서드 hello를 사용 하는 오버 로드를 갖고 `Document` 클래스 뿐만 아니라 제네릭 형식 매개 변수를 사용 하는 강력한 형식의 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="1a1a2-233">이 자습서에서는 hello 샘플 코드에서 hello 후자만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="1a1a2-234">hello `Document` 클래스에서 상속 `Dictionary<string, object>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="1a1a2-235">자세한 내용은 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="1a1a2-236">**Null 허용 데이터 형식을 사용해야 하는 이유**</span><span class="sxs-lookup"><span data-stu-id="1a1a2-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="1a1a2-237">사용자 고유의 모델 클래스 toomap tooan Azure 검색 인덱스를 디자인할 때와 같은 값 형식의 속성을 선언 하는 것이 좋습니다 `bool` 및 `int` nullable toobe (예를 들어 `bool?` 대신 `bool`).</span><span class="sxs-lookup"><span data-stu-id="1a1a2-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="1a1a2-238">Nullable이 아닌 속성을 사용 하면 있으면 너무**보장** 문서가 인덱스에는 hello 해당 필드에 대 한 null 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="1a1a2-239">Hello SDK도 아니고 hello Azure 검색 서비스 할 수 있습니다 tooenforce이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="1a1a2-240">이 가상의 중요 하지 않은 것: 있는 인덱스를 추가 하면 새 필드 tooan 기존 유형의 경우를 가정해 보십시오 `Edm.Int32`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="1a1a2-241">Hello 인덱스 정의 업데이트 한 후 모든 문서 (Azure 검색에서 null을 허용 하지 않는 형식도) 이후 해당 새 필드에 대해 null 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="1a1a2-242">다음으로 nullable이 아닌 모델 클래스를 사용 하는 경우 `int` 해당 필드에 대 한 속성을 얻게 됩니다는 `JsonSerializationException` tooretrieve 문서 하려고 할 때 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="1a1a2-243">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="1a1a2-244">JSON.NET으로 직렬화 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1a1a2-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="1a1a2-245">hello SDK JSON.NET을 사용 하 여 직렬화 및 문서를 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="1a1a2-246">직렬화를 사용자 지정할 수 있으며 필요한 경우를 정의 하 여 사용자 고유의 deserialization `JsonConverter` 또는 `IContractResolver` (hello 참조 [JSON.NET 설명서](http://www.newtonsoft.com/json/help/html/Introduction.htm) 자세한 세부 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="1a1a2-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="1a1a2-247">Azure 검색 및 기타 고급 시나리오에 사용할 응용 프로그램에서 tooadapt 기존 모델 클래스를 사용 하려는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="1a1a2-248">예를 들어 사용자 지정 serialization으로 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="1a1a2-249">모델 클래스의 특정 속성을 문서 필드로 저장하는 데 포함 또는 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="1a1a2-250">코드의 속성 이름과 인덱스의 필드 이름을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="1a1a2-251">매핑 속성 toodocument 필드에 사용할 수 있는 사용자 지정 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="1a1a2-252">GitHub의 Azure 검색.NET SDK hello에 대 한 hello 단위 테스트에서 사용자 지정 직렬화를 구현의 예를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="1a1a2-253">적절한 시작 지점은 [이 폴더](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="1a1a2-254">Hello 사용자 지정 직렬화 테스트에서 사용 되는 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="1a1a2-255">Hello 인덱스의 문서에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="1a1a2-255">Searching for documents in hello index</span></span>
<span data-ttu-id="1a1a2-256">hello hello 샘플 응용 프로그램의 마지막 단계는 toosearch hello 인덱스의 일부 문서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="1a1a2-257">hello 메서드 뒤이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
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

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="1a1a2-258">쿼리를 실행할 때마다 이 메서드는 먼저 새 `SearchParameters` 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="1a1a2-259">사용 되는 toospecify 정렬, 필터링, 페이징, 패싯 등 hello 쿼리에 대 한 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="1a1a2-260">이 방법에서는 hello 설정 하 고 `Filter`, `Select`, `OrderBy`, 및 `Top` 다른 쿼리에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="1a1a2-261">모든 hello `SearchParameters` 속성 설명 [여기](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="1a1a2-262">hello 다음 단계는 tooactually hello 검색 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="1a1a2-263">이 작업은 수행 hello를 사용 하 여 `Documents.Search` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="1a1a2-264">각 쿼리에 대 한 문자열 hello 검색 텍스트 toouse 전달 (또는 `"*"` 없는 검색 텍스트가 있는 경우), 플러스 hello 앞에서 만든 매개 변수를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="1a1a2-265">또한 지정 `Hotel` 에 대 한 형식 매개 변수와 hello `Documents.Search`, 형식의 개체에 hello SDK toodeserialize 문서 hello 검색 결과에 지시 `Hotel`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="1a1a2-266">Hello 검색 쿼리 식 구문에 대 한 자세한 정보를 찾을 수 [여기](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="1a1a2-267">마지막으로, 각 쿼리 한 후이 메서드를 통해 모든 hello hello 검색 결과에서 각 문서 toohello 콘솔 인쇄 반복:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

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

<span data-ttu-id="1a1a2-268">자세히 보기의 각 hello 쿼리를 다시 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="1a1a2-269">Hello 코드 tooexecute hello 첫 번째 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="1a1a2-270">이 경우에서는 hello 단어 "budget"와 일치 하는 호텔 검색할 하 고 tooget 다시 hello 호텔 이름만, hello에 지정 된 대로 원하는 `Select` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="1a1a2-271">Hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="1a1a2-272">다음으로 야간 보다 작은 $150, 속도가 toofind hello 호텔 원하는 하 고 hello 호텔 ID와 설명을 반환:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

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

<span data-ttu-id="1a1a2-273">이 쿼리는 OData를 사용 하 여 `$filter` 식 `baseRate lt 150`, hello 인덱스의 toofilter hello 문서.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="1a1a2-274">Azure 검색에서 지 원하는 OData 구문 hello에 대 한 자세한 내용을 확인할 수 [여기](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="1a1a2-275">Hello hello 쿼리 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="1a1a2-276">다음으로, toofind hello 상위 두 호텔 가장 최근에 리 모델링 되었고, 고 hello 호텔 이름 및 보수의 마지막 날짜를 보여 주는 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="1a1a2-277">Hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-277">Here is hello code:</span></span> 

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

<span data-ttu-id="1a1a2-278">이 경우에서는 다시 사용 하 여 OData 구문을 toospecify hello `OrderBy` 매개 변수로 `lastRenovationDate desc`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="1a1a2-279">또한 설정 `Top` too2 tooensure만 얻을 수 있는 hello 상위 두 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="1a1a2-280">설정 하 여 이전 처럼 `Select` toospecify 필드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="1a1a2-281">Hello 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="1a1a2-282">마지막으로, toofind hello 단어 "motel"와 일치 하는 모든 호텔 원하는:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="1a1a2-283">다음은 hello를 지정 하지 않았기 때문에 모든 필드를 포함 하는 hello 결과 및 `Select` 속성:</span><span class="sxs-lookup"><span data-stu-id="1a1a2-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="1a1a2-284">이 단계는 hello 자습서를 완료 하지만 보십시오.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="1a1a2-285">**다음 단계** 에서는 Azure 검색에 대해 자세히 학습하기 위한 추가 리소스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a1a2-286">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1a1a2-286">Next steps</span></span>
* <span data-ttu-id="1a1a2-287">Hello에 대 한 hello 참조 찾아보기 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) 및 [REST API](https://docs.microsoft.com/rest/api/searchservice/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="1a1a2-288">[비디오와 기타 샘플 및 자습서](search-video-demo-tutorial-list.md)를 통해 지식을 심화시키십시오.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="1a1a2-289">검토 [명명 규칙](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello 규칙의 다양 한 개체 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="1a1a2-290">Azure 검색에서 [지원되는 데이터 유형](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) 을 검토하십시오.</span><span class="sxs-lookup"><span data-stu-id="1a1a2-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
