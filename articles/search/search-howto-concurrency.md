---
title: "동시 aaaHow toomanage Azure 검색의 tooresources 기록"
description: "낙관적 동시성 tooavoid 중간 공기 충돌 tooAzure 검색 인덱스는 업데이트 또는 삭제, 인덱서, 데이터 원본에 사용 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="fae12-103">어떻게 Azure 검색에서 toomanage 동시성</span><span class="sxs-lookup"><span data-stu-id="fae12-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="fae12-104">인덱스 및 데이터 원본 등의 Azure 검색 리소스를 관리할 때는 중요 한 tooupdate 리소스를 안전 하 게 특히 경우에 리소스 응용 프로그램의 다른 구성 요소에 의해 동시에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="fae12-105">두 클라이언트가 조정 없이 리소스를 동시에 업데이트하면 경합 상태가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="fae12-106">tooprevent이, Azure 검색 제안은 *낙관적 동시성 모델*합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="fae12-107">이 모델에서는 리소스가 잠기지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-107">There are no locks on a resource.</span></span> <span data-ttu-id="fae12-108">대신, 덮어씁니다 실수로 방지 하는 요청을 만들 수 있도록 hello 리소스 버전을 식별 하는 모든 리소스에 대 한 ETag 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="fae12-109">[샘플 C# 솔루션](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)의 개념 코드를 통해 Azure Search에서 동시성 제어가 작동하는 방식을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="fae12-110">hello 코드 동시성 제어를 호출 하는 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="fae12-111">읽기 hello [아래 코드 조각](#samplecode) 편집 appsettings.json tooadd hello 서비스 이름 및 관리자 api 키 toorun 살펴보려는 경우 대부분의 개발자 아마도 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="fae12-112">서비스 URL을 지정 된 `http://myservice.search.windows.net`, hello 서비스 이름은 `myservice`합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fae12-113">작동 방법</span><span class="sxs-lookup"><span data-stu-id="fae12-113">How it works</span></span>

<span data-ttu-id="fae12-114">낙관적 동시성은 구현 액세스를 통해 조건 확인 tooindexes, 인덱서, datasources, 및 synonymMap 리소스를 작성 하는 API 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="fae12-115">모든 리소스에는 개체 버전 정보를 제공하는 [*ETag(엔터티 태그)*](https://en.wikipedia.org/wiki/HTTP_ETag)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="fae12-116">Hello ETag를 먼저 확인 하 여 일반적인 작업 과정에서 동시 업데이트를 방지할 수 있습니다 (get, 로컬로 수정, 업데이트) hello 리소스의 ETag와 일치 로컬 복사본을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="fae12-117">hello REST API가 사용 하는 [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello 요청 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="fae12-118">hello 설정 accessCondition 개체를 통해 hello ETag를 설정 하는 hello.NET SDK [If-match | If-Match-None 헤더](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello 리소스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="fae12-119">[IResourceWithETag(.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag)에서 상속하는 모든 개체에는 accessCondition 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="fae12-120">리소스를 업데이트할 때마다 ETag는 자동으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="fae12-121">동시성 관리를 구현 하 고 모두 지정 하는 것 전제 조건 hello 원격 리소스를 필요로 하는 hello 업데이트 요청에 toohave hello hello 클라이언트에서 수정 하는 hello 리소스의 hello 복사본으로 동일한 ETag입니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="fae12-122">동시 프로세스 hello 원격 리소스 이미 변경 된 경우 ETag hello hello 전제 조건 일치 하지 않으며 HTTP 412 hello 요청은 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="fae12-123">Hello.NET SDK를 사용 하는 경우 이러한 쿼리는로 `CloudException` 여기서 hello `IsAccessConditionFailed()` 확장 메서드는 true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="fae12-124">동시성의 메커니즘은 한 가지뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="fae12-125">즉, 리소스 업데이트에 사용되는 API에 관계없이 동시성은 항상 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="fae12-126">사용 사례 및 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="fae12-126">Use cases and sample code</span></span>

<span data-ttu-id="fae12-127">코드 다음 hello accessCondition 키 업데이트 작업에 대 한 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="fae12-128">Hello 리소스가 더 이상 존재 하는 경우 업데이트 실패</span><span class="sxs-lookup"><span data-stu-id="fae12-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="fae12-129">Hello 리소스 버전 변경 되 면 업데이트 실패</span><span class="sxs-lookup"><span data-stu-id="fae12-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="fae12-130">[DotNetETagsExplainer 프로그램](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)의 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="fae12-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="fae12-131">디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="fae12-131">Design pattern</span></span>

<span data-ttu-id="fae12-132">낙관적 동시성을 구현 하는 디자인 패턴 hello 액세스 조건 검사를 hello 액세스 조건에 대 한 테스트를 다시 시도 하 고 필요에 따라 toore 시도 하기 전에 업데이트 된 리소스를 검색 하는 루프를 포함 해야-hello 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="fae12-133">이 코드 조각은 hello 이미 있는 synonymMap tooan 인덱스 추가 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="fae12-134">이 코드는 hello에서 [Azure 검색에 대 한 동의어 (미리 보기) C# 자습서](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="fae12-135">hello 조각 호텔"hello" 인덱스를 가져옵니다, 그리고 업데이트 작업에 hello 개체 버전을 확인, hello 조건 실패 하 고 재시도 hello toothree 시간) (업 작업을 인덱스 검색 hello 서버 tooget hello에서 최신 버전으로 시작 하는 경우 예외를 throw 합니다. 버전.</span><span class="sxs-lookup"><span data-stu-id="fae12-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="fae12-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fae12-136">Next steps</span></span>

<span data-ttu-id="fae12-137">검토 hello [동의어 C# 샘플](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) 더 많은 컨텍스트 toosafely 기존 인덱스를 업데이트 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="fae12-138">Hello 다음 중 하나를 수정 하는 시도 tooinclude Etag 또는 AccessCondition 개체를 샘플링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="fae12-139">GitHub의 REST API 샘플</span><span class="sxs-lookup"><span data-stu-id="fae12-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="fae12-140">[GitHub의 .NET SDK 샘플](https://github.com/Azure-Samples/search-dotnet-getting-started)</span><span class="sxs-lookup"><span data-stu-id="fae12-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="fae12-141">이 솔루션에는이 문서에 제공 된 hello 코드를 포함 하는 hello "DotNetEtagsExplainer" 프로젝트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae12-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="fae12-142">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fae12-142">See also</span></span>

  <span data-ttu-id="fae12-143">[일반적인 HTTP 요청 및 응답 헤더](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="fae12-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="fae12-144">[HTTP 상태 코드](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [인덱스 작업(REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="fae12-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>